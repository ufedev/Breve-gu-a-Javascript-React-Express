# COMPONENTE DE REACT
 Todo componente actualmente es una función que retorna obligatoriamente HTML o mejor dicho JSX que es una sintaxis especial de HTML
**El JSX se compila en HTML**
Los componentes de react inician con mayuscula, y pueden recibir parametros como props
**En react todas las etiquetas que no tengan etiqueta de cierre deben cerrarse a si mismas al final con `/>`** 

> Ejemplo
```jsx
// Componente React
const Titulo=(props)=>{
    return <h1>{props.app}</h1> {/* Aqui se reciben los props */}

}

// Otra forma de extraer los props es con destructuring de objetos

export const Titulo2=({app})=>{ // Exportación nombrada, cuando se lo extraiga desde otro archivo debe llamarse igual que aquí
    return <h1>{app}</h1>
}

export default Titulo // Expor por defecto puede recibir cualquier nombre desde donde se lo importe
```

```jsx
// Uso
import Titulo from './Titulo' // Import default
import {Titulo2} from "./Titulo" // Import nombrado
const App=()=>{

    return (
        <div>
            <Titulo app={`Mi app`}/> {/* Aqui se llama el componente */}
            <Titulo2 app={`Mi app 2`}/>
        </div>
    )
}

```








