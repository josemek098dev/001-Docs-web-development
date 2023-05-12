<div align="center">


![Day 5](./images/banners/React_Banner.png)

  <h1> ReactJs </h1>
  

  <sub>Author:
  <a href="" target="_blank">Jose A. Cordoba</a><br>
  <small> April, 2023</small>
  </sub>
</div>

[<< Seccion 3](https://github.com/josemek098dev/001-Docs-web-development/blob/master/02%20-%20Fronted/08%20-%20ReactJs/803%20-%20React%20-%20GifExpert.md) | [Seccion 4 >>](https://github.com/josemek098dev/001-Docs-web-development/blob/master/02%20-%20Fronted/08%20-%20ReactJs/804%20-%20React%20-%20GifExpert%20pruebas.md)

* [src](#src-gifexpertapp)
  * [GifExpertApp](#src-gifexpertapp)
  * [componentes](#src-gifexpertapp)
    * [AddCategory](#src-componentes-addcategory)
    * [GifGrid](#src-componentes-gifgrid)
    * [GifItem](#src-componentes-gifitem)
  * [helpers](#src-gifexpertapp)
    * [getGifs](#src-helpers-getgifs)
  * [hooks](#src-gifexpertapp)
    * [useFetchGifs](#src-hooks-usefetchgifs)

# Resumen GifExpert

Una pequeña app que obtiene gifs  y los muestra en pantalla

### src GifExpertApp


```jsx

import {useState} from "react";
import { AddCategory, GifGrid   } from "./components"

export const GifExpertApp = () => {

    const [categories, setCategories] = useState(['One Punch']);

    const onAddCategory = (newCategory) => {
        if ( categories.includes(newCategory )) return; 
        setCategories([newCategory, ...categories]) 
    }

    return (
        <>
            {/* título */}
            <h1>GifExpertApp</h1>

            {/* componente AddCategory */}
            <AddCategory 
                onNewCategory = { onAddCategory }
                currentCategories = { categories }
            />

            {/* Listado de Gif */}
            <ol>
                { categories.map( category => 
                    <GifGrid 
                        key = { category } 
                        category={ category }
                    />
                ) }

                {/* Ejemplo de elementos HTML sin key */}
                <li>A</li>
                <li>A</li>
                <li>B</li>
            </ol>

            {/* Componente GifGrid */}
        </>
    )
}
```
Ahora describiré cada parte del código:

import {useState} from "react";: Importa el hook useState de la biblioteca react. Este hook permite agregar estado a un componente de React.

import { AddCategory, GifGrid } from "./components": Importa dos componentes personalizados llamados AddCategory y GifGrid. Los componentes están ubicados en un archivo llamado components.js dentro de la misma carpeta que este archivo.

const [categories, setCategories] = useState(['One Punch']);: Declara el estado categories y la función setCategories utilizando el hook useState. Inicializa el estado con un arreglo que contiene la categoría "One Punch".

const onAddCategory = (newCategory) => {...}: Define la función onAddCategory que se utiliza para agregar una nueva categoría al estado categories. La función comprueba si la categoría ya existe en el arreglo utilizando includes, y si no existe, agrega la nueva categoría al principio del arreglo utilizando el operador spread ....

return (<>...</>): Devuelve el JSX del componente. En este caso, el componente devuelve un fragmento (<>...</>) que contiene varios elementos HTML y componentes de React.

`<h1>GifExpertApp</h1>`: Muestra el título de la aplicación.

`<A ddCategory onNewCategory={onAddCategory} currentCategories={categories}/>`: Renderiza el componente AddCategory con dos props. La primera prop onNewCategory se utiliza para pasar la función onAddCategory al componente. La segunda prop currentCategories se utiliza para pasar el estado categories al componente.

`<ol>...</ol>`: Renderiza una lista ordenada que contiene elementos de la categoría.

{ categories.map( category => `<GifGrid key={category} category={category} />` ) }: Utiliza el método map para crear un componente GifGrid para cada categoría en el estado categories. Cada componente GifGrid recibe una prop category con el nombre de la categoría y una prop key que se utiliza para identificar de manera única cada elemento en la lista.

`<>A</li><li>A</li><li>B</li>`: Muestra elementos HTML simples sin una prop key definida.

### src componentes AddCategory


```jsx
import { useState } from "react"

export const AddCategory = ({ onNewCategory }) => {

  const [inputValue, setInputValue] = useState('One Punch')

  //creamos un imput en react
  const onInputChange = (event) => {
    setInputValue(event.target.value)
  }

  const onSubmit = (event) =>{
    event.preventDefault()
    if(inputValue.trim().length <= 1) return;
    console.log(inputValue)
    onNewCategory(inputValue.trim())
    setInputValue(" ")
  }

//manejamos un formularo capturamos el valor lo asociamos
//conservamos las practicas de react
  return (
    <form onSubmit={onSubmit}>
      <input 
        type="text"
        placeholder="BuscarGif"
        value={inputValue}
        onChange={onInputChange}
      />
    </form>
  )
}
```
  
Este componente permite agregar nuevas categorías a la lista de categorías. Aquí está una descripción de las partes del componente:

- `import { useState } from "react"`: Importamos el hook useState de React para manejar el estado del componente.
- `export const AddCategory = ({ onNewCategory }) => { ... }`: Declaramos el componente como una función de flecha y aceptamos una prop llamada `onNewCategory`, que es una función que se encargará de agregar una nueva categoría.
- `const [inputValue, setInputValue] = useState('One Punch')`: Usamos el hook useState para crear una variable de estado `inputValue`, que representa el valor actual del input de búsqueda. El valor inicial se establece en `'One Punch'`.
- `const onInputChange = (event) => { setInputValue(event.target.value) }`: Creamos una función llamada `onInputChange` que se encargará de actualizar el valor de `inputValue` cada vez que el usuario escriba algo en el input de búsqueda.
- `const onSubmit = (event) => { ... }`: Creamos una función llamada `onSubmit` que se ejecutará cuando el usuario envíe el formulario. En esta función, primero prevenimos el comportamiento por defecto del evento y luego comprobamos si el valor de `inputValue` tiene más de un caracter. Si es así, llamamos a la función `onNewCategory` con el valor de `inputValue` y lo reseteamos a un valor vacío.
- `<form onSubmit={onSubmit}> ... </form>`: Creamos un formulario que se ejecutará cuando el usuario presione Enter o haga clic en el botón de búsqueda. Le pasamos la función `onSubmit` como callback para manejar el evento de envío.
- `<input type="text" placeholder="BuscarGif" value={inputValue} onChange={onInputChange} />`: Creamos un input que permitirá al usuario ingresar la categoría que desea buscar. Le pasamos el valor de `inputValue` como valor actual del input y la función `onInputChange` como callback para manejar el evento de cambio. Además, establecemos un placeholder para indicar al usuario qué debe escribir en el input.

### src componentes GifGrid

```jsx
import {useState,useEffect } from "react"

import { GifItem } from "./GifItem"
import { getGifs } from "../helpers/getGifs"
import { useFetchGifs } from "../hooks/useFetchGifs"
export const GifGrid = ({ category }) => {

    const { images, isLoading } = useFetchGifs(category)
    getGifs(category)
    return (

        <>
            <h3>{category}</h3>
            {
                isLoading && ( <h2 >Cargando...</h2>)              
            }
            
            <div className = "card-grid">
                {
                    images.map( (image) =>  (
                        <GifItem 
                    key = { image.id}{...image /* esparcimos la imagen*/}

                        />
                    ))
                }
            </div>
        </>

    )
}
```

Este componente `GifGrid` muestra una lista de imágenes GIF asociadas a una categoría. A continuación, se detalla cada parte del mismo:

- `useEffect` y `useState`: estos son hooks de React que permiten manejar el estado del componente y realizar efectos secundarios cuando este cambia. Sin embargo, en este componente, el hook `useEffect` no se está utilizando en este momento.

- `useFetchGifs`: es un custom hook que se utiliza para realizar la petición HTTP para obtener los GIF asociados a la categoría. Este hook tiene una lógica interna que maneja el estado de carga (`isLoading`) y las imágenes obtenidas (`images`).

- `h3`: es un encabezado que muestra el título de la categoría.

- `isLoading`: es una variable que indica si el componente está cargando datos y se muestra un mensaje de "Cargando..." si es verdadero.

- `card-grid`: es una clase de CSS que se utiliza para aplicar estilos al contenedor de las imágenes GIF.

- `images.map`: se utiliza para iterar sobre cada imagen obtenida de la petición HTTP y renderizar un componente `GifItem` por cada imagen. Se pasa la imagen como propiedades (usando el operador de propagación) para que el componente hijo pueda mostrarla.

- `GifItem`: es un componente que muestra una imagen GIF con su título y url. Este componente se renderiza por cada imagen obtenida de la petición HTTP.

En resumen, el componente `GifGrid` maneja el estado de carga de la petición HTTP y renderiza los componentes `GifItem` para cada imagen obtenida, todo dentro de un contenedor con el título de la categoría.

### src componentes GifItem

```jsx

export const GifItem = ({ title, url, id }) => {
  return (
    <div className="card">

      <img src={url} alt={title} />
      <p>{title}</p>
    </div>
  )
}
```

Este componente es una presentacional que se encarga de mostrar la información de cada GIF en una tarjeta. Toma como parámetros `title`, `url` e `id` y los utiliza para renderizar la imagen y el título del GIF dentro de una tarjeta.

- `title`: El título del GIF que se muestra en la tarjeta.
- `url`: La URL de la imagen del GIF que se muestra en la tarjeta.
- `id`: El ID del GIF que se utiliza como clave única para el elemento de la lista. 

El componente devuelve un div con la clase `card` que contiene una etiqueta `img` con el atributo `src` establecido en la URL de la imagen del GIF y un texto alternativo en el atributo `alt` con el título del GIF. Además, se muestra el título del GIF debajo de la imagen en un elemento `p`.

### src helpers getGifs

```jsx
export const getGifs = async (category) => {

    const url = `https://api.giphy.com/v1/gifs/search?api_key=CxOvWOD91NRxunyrNFZ2BKd87xa989hr&q=${category}&limit=10`
    const resp = await fetch(url)
    const { data } = await resp.json()

    const gifs = data.map(img => ({
        id: img.id,
        title: img.title,
        url: img.images.downsized_medium.url
    }))

    return gifs
}
```

Este código no es un componente de React, sino una función que utiliza la API de Giphy para obtener un array de objetos de gifs. Aquí hay una descripción de cada parte de la función:

- `getGifs`: es el nombre de la función.
- `async`: indica que la función es asincrónica, lo que significa que devuelve una promesa.
- `(category)`: es un parámetro de la función, que se utiliza para hacer una búsqueda de gifs de esa categoría específica.
- `const url`: es una constante que almacena la URL de la API de Giphy con el `api_key` y la `category` especificados en la búsqueda.
- `const resp`: es una constante que usa `await fetch` para enviar una solicitud a la URL y espera la respuesta.
- `const { data }`: es una constante que utiliza la desestructuración para extraer la propiedad `data` de la respuesta como un objeto.
- `const gifs`: es una constante que usa el método `map()` para recorrer cada objeto de la matriz `data` y devuelve un nuevo objeto solo con las propiedades que necesitamos, como `id`, `title` y `url`.
- `return gifs`: devuelve la matriz de gifs al componente que llamó a la función.

### src hooks useFetchGifs

```jsx
import { useEffect, useState } from "react"
import { getGifs } from "../helpers/getGifs"

export const useFetchGifs = (category) => {

    const [images, setImages] = useState([])
    const [isLoading, setIsLoading] = useState(true)

    const getImages = async() => {
        const newImages = await getGifs(category)
        setImages(newImages)
        setIsLoading(false)
    }

    useEffect(() => {
        getImages()
    }, [])

 return{
    images,
    isLoading
 }
}
```
Este es un hook personalizado de React llamado useFetchGifs que se encarga de obtener un conjunto de imágenes GIF utilizando la función getGifs definida en el archivo helpers/getGifs.js.

El hook utiliza los hooks de estado useState y useEffect para almacenar el estado de las imágenes y el estado de carga (isLoading), respectivamente.

La función getImages es una función asíncrona que llama a la función getGifs y actualiza el estado de las imágenes y el estado de carga utilizando las funciones setImages y setIsLoading, respectivamente.

El hook utiliza el hook useEffect para llamar a la función getImages cuando el componente se monta ([] indica que sólo se debe llamar una vez).

Por último, el hook devuelve un objeto con dos propiedades: images (que almacena un arreglo de objetos con la información de cada imagen) y isLoading (que indica si las imágenes están cargando o no).