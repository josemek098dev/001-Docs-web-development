<div align="center">


![Day 5](./images/banners/React_Banner.png)

  <h1> ReactJs </h1>
  

  <sub>Author:
  <a href="" target="_blank">Jose A. Cordoba</a><br>
  <small> April, 2023</small>
  </sub>
</div>

[<< Seccion 3](https://github.com/josemek098dev/001-Docs-web-development/blob/master/02%20-%20Fronted/08%20-%20ReactJs/803%20-%20React%20-%20GifExpert.md) | [Home >>](https://github.com/josemek098dev/001-Docs-web-development/tree/master)

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

# Resumen GifExpert pruebas

xxxxxxxxx

### src GifExpertApp


```jsx
import { fireEvent, render, screen } from "@testing-library/react"
import { GifExpertApp } from "../src/GifExpertApp"
 
 
describe('Pruebas en GifExpertApp', () => { 
 
    test('debe agregar una nueva categoria', () => { 
        render(<GifExpertApp/>)
 
        const input = screen.getByRole('textbox');
        const form = screen.getByRole('form');
 
        fireEvent.input(input, {target: {value: 'One'}});
        fireEvent.submit( form );
        fireEvent.input(input, {target: {value: 'Two'}});
        fireEvent.submit( form );
        expect(screen.getAllByRole('heading', { level: 3 }).length).toBe(3);
        //screen.debug()
     })
 
     test('No debe agregar una categoria repetida', () => { 
        const inputValue = 'Two';
        
        render(<GifExpertApp/>)
        
        const input = screen.getByRole('textbox');
        const form = screen.getByRole('form');
 
        fireEvent.input(input, {target: {value: inputValue}});
        fireEvent.submit( form );
        fireEvent.input(input, {target: {value: inputValue}});
        fireEvent.submit( form );
        expect(screen.getAllByText(inputValue).length).toBe(1)
        //screen.debug()
     })
 })
```
Este código describe un conjunto de pruebas unitarias para la aplicación web "GifExpertApp". La prueba verifica si la aplicación web agrega correctamente una nueva categoría a través de un formulario de entrada. La segunda prueba verifica si la aplicación web no agrega categorías repetidas.

La primera prueba comienza renderizando la aplicación web `GifExpertApp`. Luego, utilizando `screen.getByRole` obtiene una referencia al campo de entrada de texto y al formulario. Después, se usa `fireEvent.input` para simular el evento de entrada de texto y se proporciona el valor "One". Posteriormente, se simula el evento de envío de formulario a través de `fireEvent.submit`. Después, se repiten estos pasos con un valor diferente "Two". Por último, se utiliza `expect` y `screen.getAllByRole` para verificar que se han agregado tres categorías al elemento `heading`.

La segunda prueba comienza de manera similar a la primera. Se renderiza la aplicación web y se obtiene una referencia al campo de entrada de texto y al formulario. Luego, se utiliza `fireEvent.input` para simular el evento de entrada de texto y se proporciona el valor "Two". Posteriormente, se simula el evento de envío de formulario a través de `fireEvent.submit`. Después, se repiten estos pasos con el mismo valor "Two". Finalmente, se utiliza `expect` y `screen.getAllByText` para verificar que solo se ha agregado una categoría con el valor "Two".
### src componentes AddCategory


```jsx
import { fireEvent, render,screen } from "@testing-library/react"
import { AddCategory } from "../../src/components/AddCategory"


describe('Pruebas en Add Category', () => { 
    
    test('debe de cambiar el valor de la caja de texto', () => { 
        render( <AddCategory onNewCategory={ ()=> {} }/>)
        const input = screen.getByRole('textbox')
        fireEvent.input( input, { target: {value:'Saitama'} } )
        expect( input.value).toBe('Saitama')
       // screen.debug()
     }) 


     test('debe de llamar onNewCategory si el input tiene un valor', () => {
        const onNewCategory = jest.fn()        
        const inputValue = 'Saitama';
        render( <AddCategory onNewCategory={ onNewCategory }/>)    
        const input = screen.getByRole('textbox') 
        const form = screen.getByRole('form')      
        fireEvent.input( input, { target: {value: inputValue } } )
        fireEvent.submit( form )
        //screen.debug( );
        expect( input.value ).toBe('');
        expect( onNewCategory ).toHaveBeenCalled( )
        expect( onNewCategory ).toHaveBeenCalledTimes(1)
        expect( onNewCategory ).toHaveBeenCalledWith( inputValue )
      })

      test('no debe de llamar el onNewCategory si el input esta vacio', () => { 
        const onNewCategory = jest.fn();
        render (<AddCategory onNewCategory={ onNewCategory} />)
        const form = screen.getByRole('form');
        fireEvent.submit(form);
        expect( onNewCategory ).toHaveBeenCalledTimes(0);
        expect( onNewCategory ).not.toHaveBeenCalled();
       })

})
```
Este código describe un conjunto de pruebas unitarias para el componente `AddCategory`. El primer test verifica si el valor de la caja de texto cambia al escribir en ella.

El segundo test verifica si se llama a la función `onNewCategory` con el valor correcto del input cuando se envía el formulario con un valor en la caja de texto. Se utiliza `jest.fn()` para crear una función simulada que se llamará al enviar el formulario. Luego, se renderiza el componente `AddCategory` con la función simulada como prop. Se obtiene una referencia al campo de entrada de texto y al formulario y se simula el evento de entrada de texto y envío de formulario. Finalmente, se utilizan `expect` y `jest.fn()` para verificar que se llama a la función simulada con el valor correcto y solo una vez.

El tercer test verifica si la función `onNewCategory` no se llama cuando se envía el formulario con un valor vacío en la caja de texto. Se utiliza `jest.fn()` para crear una función simulada que no debe ser llamada en esta prueba. Se renderiza el componente `AddCategory` con la función simulada como prop. Se obtiene una referencia al formulario y se simula el evento de envío de formulario. Finalmente, se utilizan `expect` y `jest.fn()` para verificar que la función simulada no se llama.
  
### src componentes GifGrid

```jsx
import { render, screen } from "@testing-library/react"
import { GifGrid } from "../../src/components/GifGrid"
import { useFetchGifs } from "../../src/hooks/useFetchGifs"

jest.mock("../../src/hooks/useFetchGifs")

describe('Pruebas en GifGrid', () => {

    const category = 'One punch'

    test('debe de mostrar el loading inicialmente', () => {
        useFetchGifs.mockReturnValue({
            images: [],
            isLoading: true
        })
        render(<GifGrid category={category} />);
        expect(screen.getByText('Cargando...'));
        expect(screen.getByText(category))
    })

    test('debe de mostrar items cuando se cargan las imagenes', () => {
        const gifs = [
            {
                id: 'ABC',
                title: 'Saitama',
                url: 'https://saitama.jpn'
            },
            {
                id: 'ABaC',
                title: 'Saitaama',
                url: 'https://saiatama.jpn'
            },
        ]
        useFetchGifs.mockReturnValue({
            images: gifs,
            isLoading: false
        })
        render(<GifGrid category={category} />)
        expect(screen.getAllByRole('img').length).toBe(2)
    })

})
```

Este código describe dos pruebas para el componente `GifGrid`. La primera prueba, `debe de mostrar el loading inicialmente`, comprueba si se muestra el mensaje "Cargando..." cuando se llama al componente `GifGrid` y `useFetchGifs` devuelve un objeto con un array de imágenes vacío y `isLoading` en `true`. La segunda prueba, `debe de mostrar items cuando se cargan las imagenes`, comprueba si se muestran las imágenes correctamente cuando `useFetchGifs` devuelve un objeto con un array de imágenes y `isLoading` en `false`. Se utiliza `jest.mock` para hacer una simulación del comportamiento del hook `useFetchGifs` y poder controlar lo que devuelve en cada prueba.


### src componentes GifItem

```jsx

import { render, screen } from '@testing-library/react'
import { GifItem } from '../../src/components/GifItem'

describe('Pruebas en GifItem', () => { 

    const title = 'Saitama'
    const url = 'https://one-punch.com/saitama.jpg'
    
    test('debe de hacer match con el snapshot', () => {
        const { container } = render(<GifItem title ={title} url ={url} />)
        // eslint-disable-next-line jest/valid-expect
        expect( container ).toMatchSnapshot();
     })

     test('debe de mostrar la imagen con el URL y el ALT indicado', () => {

        render(<GifItem title={title} url={url} />)
        //expect( screen.getByRole('img').src).toBe(url)
        const{ src, alt } = screen.getByRole('img');
        expect(src).toBe(url);
        expect(alt).toBe(alt);
     })

     test('debe de mostrar el titulo en el componente', () => {
        render(<GifItem title={title} url={url} />)
        expect(screen.getByText(title)).toBeTruthy()
     })

 })
```
El código proporciona pruebas unitarias para el componente GifItem, que muestra un gif con su título. Las pruebas incluyen:

1. Prueba de snapshot: asegura que el componente coincida con una instantánea previamente guardada.
2. Prueba de imagen: verifica que la imagen se muestre correctamente con la URL y el atributo ALT.
3. Prueba de título: asegura que el título se muestre correctamente en el componente.

Se utilizan las bibliotecas @testing-library/react para crear el entorno de pruebas y la biblioteca GifItem para importar el componente a probar. Además, se definen las constantes title y url que se utilizan en todas las pruebas.


### src helpers getGifs

```jsx
import { getGifs } from "../../src/helpers/getGifs"

describe('Pruebas en getGifs', () => { 
    
    test('Debe de retronar un arreglo de figs', async() => {
        
        const gifs = await getGifs('One Punch')

        expect ( gifs.length ).toBeGreaterThan(0)
        expect ( gifs[0] ).toEqual({
            
                id: expect.any(String),
                title:expect.any(String),
                url:expect.any(String)
            
        })

     })

 })
```
Este código es un conjunto de pruebas para el archivo `getGifs.js` que contiene la función `getGifs()`. La función se utiliza para obtener gifs a través de la API de GIPHY. 

La prueba comprueba que se obtenga un arreglo de gifs y que el primer elemento del arreglo tenga una estructura específica con los campos `id`, `title` y `url`. La prueba es asíncrona ya que `getGifs()` realiza una llamada a una API externa y puede tomar algún tiempo en obtener la respuesta. 

En resumen, este conjunto de pruebas verifica que `getGifs()` funcione correctamente al obtener gifs de la API de GIPHY y devolver un arreglo de gifs con la estructura deseada.

### src hooks useFetchGifs

```jsx

import { renderHook,waitFor } from "@testing-library/react"
import { useFetchGifs } from "../../src/hooks/useFetchGifs"

describe('Pruebas en el hook useFecthGifs', () => { 

    test('debe de regresar el estado inicial', () => {

        const { result } =renderHook(()=> useFetchGifs('One Punch'))
        const { images, isLoading } = result.current
        expect ( images.length ).toBe( 0 )
        expect( isLoading ).toBeTruthy()
        //const {images,isLoading } = use useFetchGifs();
    })


    test('debe de retornar un arreglo de imagenes y isLoading en false',async () => {

        const { result } =renderHook(()=> useFetchGifs('One Punch'))
        await waitFor(
            ()=> expect (result.current.images.length).toBeGreaterThan(0)

        )
       
         const { images, isLoading } = result.current
        expect ( images.length ).toBeGreaterThan( 0 )
        expect( isLoading ).toBeFalsy()
        //const {images,isLoading } = use useFetchGifs();
    })

 })
```
Este código es una suite de pruebas para un hook personalizado llamado useFetchGifs que se utiliza para obtener gifs de una API.

La primera prueba (test) verifica si el estado inicial es correcto y si el isLoading está en verdadero.

La segunda prueba prueba si el useFetchGifs devuelve un arreglo de imágenes después de hacer una solicitud a la API y si el isLoading está en falso. Para esperar a que se resuelva la promesa que devuelve useFetchGifs, se utiliza waitFor de la biblioteca @testing-library/react.