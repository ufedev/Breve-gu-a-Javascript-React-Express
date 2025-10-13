# Guía de Express.js

## ¿Qué es Express?

Express es un **framework minimalista de Node.js** para crear servidores web y APIs.

## Creación de la App

### Instalación
```bash
npm install express
```

### Estructura Básica

***Para que sea mas similar a React vamos a utilizar todo como si fuera React con import/export, esto se llama ECMAScript Modules***
```javascript
import express from 'express' // 1. Importar Express
const app = express();              // 2. Crear la aplicación
const PORT = 3000;                  // 3. Definir el puerto

// 4. Configurar middlewares
app.use(express.json()); // Para recibir JSON en el body

// 5. Definir rutas (ver más abajo)
app.get('/', (req, res) => {
  res.send('¡Hola Mundo!');
});

// 6. Iniciar el servidor
app.listen(PORT, () => {
  console.log(`Servidor corriendo en http://localhost:${PORT}`);
});
```

## Partes de la Aplicación

### 1. `import express from 'express'`
Importa el módulo de Express.

### 2. `const app = express()`
Crea una instancia de la aplicación Express. Esta instancia (`app`) es tu servidor.

### 3. Middlewares - `app.use()`
Son funciones que se ejecutan antes de llegar a las rutas. Procesan las solicitudes.

```javascript
// Middleware para procesar JSON
app.use(express.json());

// Middleware para servir archivos estáticos
app.use(express.static('public'));

// Middleware personalizado
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next(); // Pasa al siguiente middleware o ruta
});
```

### 4. Rutas
Definen los endpoints de tu API y qué hacer cuando se accede a ellos.

### 5. `app.listen(PORT, callback)`
***El callback es una función anomina, puede definirse como función flecha o como funcion declarada, y siempre recibe 3 parametros en el siguiente orden, `req` la solucitud, `res` la respuesta y `next` el siguiente middleware(función a ejecutar).***
Inicia el servidor en el puerto especificado.

## Métodos HTTP en Express

### GET - Obtener datos
```javascript
app.get('/usuarios', (req, res) => {
  res.json([
    { id: 1, nombre: 'Juan' },
    { id: 2, nombre: 'María' }
  ]);
});

// Con parámetros de ruta
app.get('/usuarios/:id', (req, res) => {
  const id = req.params.id;
  res.json({ id, nombre: 'Juan' });
});
```

### POST - Crear datos
```javascript
app.post('/usuarios', (req, res) => {
  const nuevoUsuario = req.body;
  // Aquí guardarías en la base de datos
  res.status(201).json({
    mensaje: 'Usuario creado',
    usuario: nuevoUsuario
  });
});
```

### PUT - Actualizar datos completos
```javascript
app.put('/usuarios/:id', (req, res) => {
  const id = req.params.id;
  const datosActualizados = req.body;
  res.json({
    mensaje: `Usuario ${id} actualizado completamente`,
    datos: datosActualizados
  });
});
```

### PATCH - Actualizar datos parciales
```javascript
app.patch('/usuarios/:id', (req, res) => {
  const id = req.params.id;
  const cambios = req.body;
  res.json({
    mensaje: `Usuario ${id} actualizado parcialmente`,
    cambios: cambios
  });
});
```

### DELETE - Eliminar datos
```javascript
app.delete('/usuarios/:id', (req, res) => {
  const id = req.params.id;
  res.json({ mensaje: `Usuario ${id} eliminado` });
});
```

## Componentes de una Ruta

```javascript
app.get('/usuarios/:id', (req, res) => {
  // Explicación:
  // '/usuarios/:id' -> La ruta (path)
  // ':id' -> Parámetro de ruta
  // req -> Request (solicitud)
  // res -> Response (respuesta)
});
```

### Objeto `req` (Request)
Contiene información de la solicitud:
- `req.params` - Parámetros de la URL (`/usuarios/:id`)
- `req.query` - Query strings (`/usuarios?edad=25`)
- `req.body` - Datos del cuerpo (en POST/PUT)
- `req.headers` - Encabezados HTTP

### Objeto `res` (Response)
Envía respuestas al cliente:
- `res.send()` - Envía cualquier tipo de respuesta
- `res.json()` - Envía JSON
- `res.status()` - Define código de estado
- `res.sendFile()` - Envía un archivo

## Ejemplo Completo - API de Tareas

```javascript
const express = require('express');
const app = express();
const PORT = 3000;

// Middleware
app.use(express.json());

// "Base de datos" temporal
let tareas = [
  { id: 1, titulo: 'Aprender Express', completada: false },
  { id: 2, titulo: 'Crear una API', completada: true }
];

// GET - Obtener todas las tareas
app.get('/tareas', (req, res) => {
  res.json(tareas);
});

// GET - Obtener una tarea específica
app.get('/tareas/:id', (req, res) => {
  const tarea = tareas.find(t => t.id === parseInt(req.params.id));
  if (!tarea) {
    return res.status(404).json({ error: 'Tarea no encontrada' });
  }
  res.json(tarea);
});

// POST - Crear una tarea
app.post('/tareas', (req, res) => {
  const nuevaTarea = {
    id: tareas.length + 1,
    titulo: req.body.titulo,
    completada: false
  };
  tareas.push(nuevaTarea);
  res.status(201).json(nuevaTarea);
});

// PUT - Actualizar una tarea completa
app.put('/tareas/:id', (req, res) => {
  const tarea = tareas.find(t => t.id === parseInt(req.params.id));
  if (!tarea) {
    return res.status(404).json({ error: 'Tarea no encontrada' });
  }
  tarea.titulo = req.body.titulo;
  tarea.completada = req.body.completada;
  res.json(tarea);
});

// DELETE - Eliminar una tarea
app.delete('/tareas/:id', (req, res) => {
  const index = tareas.findIndex(t => t.id === parseInt(req.params.id));
  if (index === -1) {
    return res.status(404).json({ error: 'Tarea no encontrada' });
  }
  tareas.splice(index, 1);
  res.json({ mensaje: 'Tarea eliminada' });
});

// Iniciar servidor
app.listen(PORT, () => {
  console.log(`Servidor en http://localhost:${PORT}`);
});
```

## Códigos de Estado HTTP Comunes

- **200** - OK (éxito)
- **201** - Created (recurso creado)
- **400** - Bad Request (solicitud incorrecta)
- **404** - Not Found (no encontrado)
- **500** - Internal Server Error (error del servidor)
