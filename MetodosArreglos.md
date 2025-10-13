# Métodos de Arreglos en JavaScript

## forEach
Ejecuta una función para cada elemento del arreglo. **No retorna nada** (undefined).

```javascript
const numeros = [1, 2, 3, 4];
numeros.forEach(num => console.log(num * 2));
// Imprime: 2, 4, 6, 8
```

**Uso:** Cuando necesitas ejecutar una acción por cada elemento sin crear un nuevo arreglo.

## map
Ejecuta una función para cada elemento y **retorna un nuevo arreglo** con los resultados.

```javascript
const numeros = [1, 2, 3, 4];
const dobles = numeros.map(num => num * 2);
// dobles = [2, 4, 6, 8]
```

**Uso:** Cuando necesitas transformar cada elemento y obtener un nuevo arreglo.

## filter
Filtra elementos según una condición y **retorna un nuevo arreglo** solo con los que cumplen.

```javascript
const numeros = [1, 2, 3, 4, 5, 6];
const pares = numeros.filter(num => num % 2 === 0);
// pares = [2, 4, 6]
```

**Uso:** Cuando necesitas seleccionar solo algunos elementos del arreglo.

## some
Verifica si **al menos un elemento** cumple con la condición. **Retorna true o false**.

```javascript
const numeros = [1, 2, 3, 4];
const hayPares = numeros.some(num => num % 2 === 0);
// hayPares = true
```

**Uso:** Cuando necesitas saber si existe al menos un elemento que cumpla una condición.

## includes
Verifica si un arreglo **contiene un valor específico**. **Retorna true o false**.

```javascript
const frutas = ['manzana', 'banana', 'naranja'];
frutas.includes('banana'); // true
frutas.includes('uva'); // false
```

# slice
Obtiene sin modificar el original una parte del arreglo. **Retorna un nuevo arreglo**.

```javascript
const numeros = [1, 2, 3, 4, 5];
const parte = numeros.slice(1, 4);
// parte = [2, 3, 4]

```

**Uso:** Cuando necesitas verificar si un valor exacto existe en el arreglo.

## Diferencias Clave

| Método | Retorna | Modifica Original | Propósito |
|--------|---------|-------------------|-----------|
| forEach | undefined | No | Ejecutar acciones |
| map | Nuevo arreglo | No | Transformar elementos |
| filter | Nuevo arreglo | No | Filtrar elementos |
| some | Boolean | No | Verificar existencia |
| includes | Boolean | No | Buscar valor exacto |
