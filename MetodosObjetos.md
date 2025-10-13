# Métodos de Objetos en JavaScript

## Object.keys()
Retorna un **arreglo con las claves (keys)** del objeto.

```javascript
const persona = {
  nombre: 'Juan',
  edad: 25,
  ciudad: 'Buenos Aires'
};

const claves = Object.keys(persona);
// claves = ['nombre', 'edad', 'ciudad']
```

**Uso:** Cuando necesitas iterar sobre las propiedades de un objeto o saber qué propiedades tiene.

## Object.values()
Retorna un **arreglo con los valores** del objeto.

```javascript
const persona = {
  nombre: 'Juan',
  edad: 25,
  ciudad: 'Buenos Aires'
};

const valores = Object.values(persona);
// valores = ['Juan', 25, 'Buenos Aires']
```

**Uso:** Cuando solo necesitas los valores sin importar las claves.

## Object.entries()
Retorna un **arreglo de arreglos [clave, valor]** del objeto.

```javascript
const persona = {
  nombre: 'Juan',
  edad: 25,
  ciudad: 'Buenos Aires'
};

const entradas = Object.entries(persona);
// entradas = [['nombre', 'Juan'], ['edad', 25], ['ciudad', 'Buenos Aires']]
```

**Uso:** Cuando necesitas tanto la clave como el valor para cada propiedad.

## Nota: Object.from vs Object.fromEntries

Probablemente te referías a **Object.fromEntries()** (no Object.from):

### Object.fromEntries()
Convierte un arreglo de pares [clave, valor] en un objeto. **Es el inverso de Object.entries()**.

```javascript
const entradas = [['nombre', 'Juan'], ['edad', 25]];
const persona = Object.fromEntries(entradas);
// persona = { nombre: 'Juan', edad: 25 }
```

**Uso:** Cuando tienes pares clave-valor y necesitas crear un objeto.

## Diferencias Clave

| Método | Entrada | Retorna | Propósito |
|--------|---------|---------|-----------|
| Object.keys() | Objeto | Arreglo de strings | Obtener claves |
| Object.values() | Objeto | Arreglo de valores | Obtener valores |
| Object.entries() | Objeto | Arreglo de pares | Obtener claves y valores |
| Object.fromEntries() | Arreglo de pares | Objeto | Crear objeto |

## Ejemplo Práctico

```javascript
const usuario = { nombre: 'Ana', edad: 30, rol: 'admin' };

// Iterar sobre claves
Object.keys(usuario).forEach(clave => {
  console.log(`${clave}: ${usuario[clave]}`);
});

// Filtrar propiedades
const entries = Object.entries(usuario);
const filtrado = entries.filter(([key, value]) => typeof value === 'string');
const nuevoObjeto = Object.fromEntries(filtrado);
// nuevoObjeto = { nombre: 'Ana', rol: 'admin' }
```
