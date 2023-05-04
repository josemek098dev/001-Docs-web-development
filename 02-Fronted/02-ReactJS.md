<div align="center">


![Day 5](./images/banners/React_Banner.png)

  <h1> ReactJs </h1>
  

  <sub>Author:
  <a href="" target="_blank">Jose A. Cordoba</a><br>
  <small> April, 2023</small>
  </sub>
</div>

[<< Home](https://github.com/josemek098dev/001-Docs-web-development/blob/master/README.md) | [Seccion 2 >>](https://github.com/josemek098dev/001-Docs-web-development/blob/master/02-Fronted/02.1-ReactJS-pruebas.md)

- [Resumen](#resumen)
  - [React](#react)
  - [Componentes](#componentes)
  - [Iniciar un proyecto - vite](#iniciar-un-proyecto---vite)
  - [Iniciar un proyecto - cra](#iniciar-un-proyecto---cra)
  - [Diferencias Cra - Vite](#diferencias-cra---vite)
  - [Hola Mundo en React](#hola-mundo-en-react)
  - [Snippets en React](#snippets-en-react)
  - [Componentes](#componentes-1)
  - [Comunicacion entre componentes](#comunicacion-entre-componentes)
  - [PropTypes](#proptypes)
  - [DefaultProps](#defaultprops)
  - [Eventos](#eventos)
  - [useState – Hook](#usestate--hook)
  - [Otros sitios interesantes para aprender](#otros-sitios-interesantes-para-aprender)

##  Resumen
### React 
En resumen, React es una librería que permite crear aplicaciones con interfaces de usuario interactivas de manera eficiente y predecible. Los componentes son piezas de código encapsuladas que permiten romper una aplicación compleja en piezas más sencillas y fáciles de mantener. React también puede trabajar del lado del servidor, crear aplicaciones móviles y de escritorio. El código de React utiliza jsx, una mezcla de JavaScript y XML que simplifica la creación de elementos de interfaz de usuario. En el siguiente video se trabajará con código en React.# Iniciar un proyecto
Se recomienda trabajar con la documentacion oficial

### Componentes

Pequeña pieza de cédigo encapsulada re-utilizable que puede tener estado o no. componente(componente(componente))). Se reocmienda q tengan uppercamelcase (TwitterApp). Creamos arboles de componentes dentro de nuestras aplicaciones. Cada componente se encarga de una accion especifica

### Iniciar un proyecto - vite 

	1. yarn create vite
	2. tu-app-vite > react
	3. yarn // instala las dependecias del proyecto
	4. yarn dev || npm run dev// inicia la aplicacion en el localhost

### Iniciar un proyecto - cra

npx create-react-app counter-app // counter-app-cra (create react app)

Creado con npm porq tiene un packaje.json
node_modules dependencias de desarrollo no todas llegan a produccion
packaje contiene comandos nombre del projecto version
pubic contiene informacion index.html donde esta el div clase root donde se monta toda la aplicación
src contiene muchos archivos q no son todos necesarios. index.js es el archivo de entrada para unesta aplicación. React.StrictMode envia informacion de errores.

### Diferencias Cra - Vite

packaje tiene menos dependencias, pero luego necesitara mas configuraciones cambia modulos en caliente lo q es muy rapido. dev ejecuta la app , dependencias hay q aseguarse q este la version 18. 
index.html es diferente esta mas simplificado, el proyecto por defecto esta mas simplificado
vite.config.js configuracion de vite
yarn.lock indica q el proyecto fue creado con yarn, no se recomienda mezclar ambos
src tiene menos cosas q en cra maneja por defecto jsx. app.jsx es un poco mas extenso q el el otro archivo

### Hola Mundo en React

```jsx
//# main.jsx-------
	//IMPORTACION
import React from 'react';
import ReactDOM from 'react-dom/client';
//COMPONENTE (en otra ruta)
import { App } from './HelloWorldApp';
//RENDERIZACION
ReactDOM.createRoot ( document.getElementById('root')).render(
<React.StrictMode>
    <App />
</React.StrictMode>
)	
//# HelloWorldApp ---------
export function App ( ) {
    return (<h1>Hola Mundo</h1>)
}
// || tambien se puede poner… export default App;
```

### Snippets en React

Crean automaticamente codigo
imr – import react app
imp - para importar mas facil 
rafc - de Simple React Snippets crea automaticamente el esqueleto del componente

### Componentes
Para no poner un div inecesario que este dentro de un div se usan los fragmentos
return( <> … </>)
podemos poner dentro de { } expresiones primitivas de js ( objetos.propiedad si pero objeto entero no, para hacerlo hacemos esto <cod e>JSON.stringify(objeto) <cod e>)
Ojo no podemos devolver una promesa por ser asincrona
Se recomienda  q las funciones se pongan fuera de los funcional compoents
en el main con import './styles.css' importamos el estilo q queramos
### Comunicacion entre componentes
en devtools >>componentes vemos todos los componentes
podemos acceder con props a las propiedades del componente padre
tambien se puede desestructurar el argumento asi ({title}) , titulo de de props.title
<FirstApp title= “hola soy una propiedad”>
Ojo si queremos mandar un numero debe ir entre { } para las strings si se peude sin ‘’

### PropTypes
sirven para definierle el tipo a las propieties las instalamos con yarn add ‘prop-types’

```jsx
FirstApp.propTypes = {
    title: PropTypes.string
}
```
si escribimos este codigo cuando se envie una propiedad ej de tipo numero tenemos un error
si mandamos una propiedad solo con su nombre y no definimos ningun valor esta se manda como true
Con title: PropTypes.string.isRequired hacemos obligatoria el tipo de propiedad
### DefaultProps
	Entran antes q los proptypes
```jsx
FirstApp.defaultProps = {
    title: ' no hay titulo'
}
```
### Eventos
Se recomienda leer la documentacion oficial

```jsx
    <button onClick={++value}>
        +1
    </button>
```
si cambiamos value no se va a cambiar porq es un cambio de estado, por lo q necesitamos useState

### useState – Hook
Los  hooks no son mas q funciones, se recomienda leer la documentacion oficial del tema

Contador simple
```jsx
import PropTypes from 'prop-types'
import { useState } from 'react'
export const CounterApp = ({value}) => {
    const [ counter, setCounter ] = useState ( 10 )
    const handleAdd = () =>{ // parece q si o si tiene q ser una funcion esto
        setCounter (counter+1)
    }

  return (
    <>
    <div>CounterApp</div>
    <p>{counter}</p>
    <button onClick={handleAdd}>
        +1
    </button>
    </>
  )
}

```


### Otros sitios interesantes para aprender

1. 📜 [React-Oficial](https://es.react.dev/ )


