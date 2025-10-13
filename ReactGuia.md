# Guía de React - Componentes Funcionales

## ¿Qué es un Componente Funcional?

Un componente funcional es una **función de JavaScript que retorna JSX** (código que parece HTML). Es la forma moderna de crear componentes en React.

```javascript
function Saludo() {
  return <h1>¡Hola Mundo!</h1>;
}

// O con arrow function
const Saludo = () => {
  return <h1>¡Hola Mundo!</h1>;
};
```

## Props (Propiedades)

### ¿Qué son las Props?

Las props son **datos que se pasan de un componente padre a un componente hijo**. Son como parámetros de una función.

### ¿De dónde salen?

Las props vienen del **componente padre** cuando renderiza el componente hijo.

```javascript
// Componente hijo que recibe props
function Tarjeta(props) {
  return (
    <div>
      <h2>{props.titulo}</h2>
      <p>{props.descripcion}</p>
    </div>
  );
}

// Componente padre que envía props
function App() {
  return (
    <div>
      <Tarjeta 
        titulo="React tiene virtual DOM" 
        descripcion="Las funciones son trozos de código reutilizables, que pueden recibir parametros para utilizar dentro"
      />
    </div>
  );
}
```

### Destructuring de Props

Es común destructurar las props para un código más limpio:
***Destructurar un objeto es crear variables a partir de sus llaves/claves que contendran el valor que tienen en esa llave/clave***
```javascript
//Destructuración
const persona={
    nombre:"John",
    apellido:"Smith"
}
// Si queremos obetener el valor lo mas comun es 
console.log(persona.nombre)
console.log(persona.apellido)
// Muchas veces no queremos todos los datos del objeto, para evitar datos que se utilizan se pueden crear variables con solo lo que queremos

const nombre = persona.nombre // Ejemplo
// 👆 esta forma es mas explicita pero esta la destructuración que es mas simple en una sola linea

console.log(nombre) // mostrara "John"
const {nombre} = persona
//      👆 entre llaves podemos extraer una de las claves/llaves que queremos, este va a tomar el valor de esa clave.
console.log(nombre) // mostrara "John"


```

```javascript
function Tarjeta({ titulo, descripcion }) {
  return (
    <div>
      <h2>{titulo}</h2>
      <p>{descripcion}</p>
    </div>
  );
}
```

## Conceptos Clave

### 1. JSX
Es la sintaxis que parece HTML pero está en JavaScript. Debes usar `className` en lugar de `class` y `htmlFor` en lugar de `for`.

```javascript
function Boton() {
  return <button className="btn-primary">Click</button>;
}
```

### 2. Estado (useState)
Para manejar datos que cambian en el tiempo:

```javascript
import { useState } from 'react';

function Contador() {
  const [cuenta, setCuenta] = useState(0);
  
  return (
    <div>
      <p>Cuenta: {cuenta}</p>
      <button onClick={() => setCuenta(cuenta + 1)}>
        Incrementar
      </button>
    </div>
  );
}
```

### 3. Efectos (useEffect)
Para ejecutar código cuando el componente se monta o actualiza:

```javascript
import { useEffect } from 'react';

function Componente() {
  useEffect(() => {
    console.log('Componente montado');
    
    // Cleanup (opcional)
    return () => {
      console.log('Componente desmontado');
    };
  }, []); // [] = solo ejecuta una vez al montar
  
  return <div>Componente</div>;
}
```

## Estructura Básica de un Proyecto React

```
src/
  ├── App.js          // Componente principal
  ├── index.js        // Punto de entrada
  └── components/     // Tus componentes
      ├── Header.js
      ├── Footer.js
      └── Card.js
```

## Ejemplo Completo

```javascript
import { useState } from 'react';

// Componente hijo
function Producto({ nombre, precio }) {
  return (
    <div className="producto">
      <h3>{nombre}</h3>
      <p>Precio: ${precio}</p>
    </div>
  );
}

// Componente padre
function Tienda() {
  const [productos] = useState([
    { id: 1, nombre: 'Laptop', precio: 1000 },
    { id: 2, nombre: 'Mouse', precio: 25 },
    { id: 3, nombre: 'Teclado', precio: 75 }
  ]);
  
  return (
    <div>
      <h1>Mi Tienda</h1>
      {productos.map(prod => (
        <Producto 
          key={prod.id}
          nombre={prod.nombre}
          precio={prod.precio}
        />
      ))}
    </div>
  );
}

export default Tienda;
```

## Reglas Importantes

1. **Los componentes deben empezar con mayúscula:** `Componente` no `componente`
2. **Las props son de solo lectura:** No puedes modificarlas en el hijo
3. **Siempre usa `key` al mapear listas:** Para que React identifique elementos, esto es cuando se trata de mostrar una lista que cada elemento utiliza el mismo componente o etiqueta html
4. **Un componente retorna un solo elemento:** Usa `<div>` o `<>` para envolver múltiples elementos. `<>` se llama Fragment, tambien es un componente que se puede extraer de la biblioteca de React.
