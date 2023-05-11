<div align="center">


![Day 5](./images/banners/React_Banner.png)

  <h1> ReactJs </h1>
  

  <sub>Author:
  <a href="" target="_blank">Jose A. Cordoba</a><br>
  <small> April, 2023</small>
  </sub>
</div>

[<< Seccion 1](https://github.com/josemek098dev/001-Docs-web-development/blob/master/02-Fronted/02-ReactJS.md) | [Seccion 3 >>](https://github.com/josemek098dev/001-Docs-web-development/blob/master/02-Fronted/03.1-REACT_GifExpert.md)

  - [Indice](##Variables_y_constantes)
    - [React](###React)
    - [Componentes](###Componentes)

##  Resumen Pruebas unitarias

En esta sección del curso se aborda la importancia de las pruebas en el desarrollo de software y se explican los conceptos básicos de las pruebas de software, como la preparación del ambiente de pruebas y la aplicación de estímulos para verificar que la funcionalidad de la aplicación es la esperada. Se recomienda probar primero la ruta crítica de la aplicación y, con el tiempo, crear más pruebas para asegurarse de que la aplicación esté lo más limpia y depurada posible antes de pasarla a producción. La sección incluye ejercicios y tareas y es una introducción a las siguientes secciones de pruebas, que serán cada vez más complejas.

### Que son las pruebas?

Las pruebas son una herramienta esencial en el desarrollo de software que no son una pérdida de tiempo. Hay dos tipos principales de pruebas: las unitarias y las de integración. Las pruebas unitarias prueban pequeñas funcionalidades de la aplicación, mientras que las pruebas de integración prueban cómo reaccionan varias piezas juntas. Las pruebas deben ser fáciles de escribir, fáciles de leer, confiables, rápidas y principalmente unitarias. El proceso de prueba sigue los pasos de arreglar, actuar y afirmar. Además, hay ciertos mitos que rodean las pruebas, como que hacer pruebas significa que la aplicación no tendrá errores, lo cual no es cierto.

### 1 - Prueba / configuracion

```jsx
1. yarn add --dev jest
2. "scripts":{....."test":"jest"} //agregamos el script
3. "test":"jest --watchAll" // esta pendiente de todos los cambios
```

Ahora para ejecutar la prueba creamos ./test/demo.test.js

```jsx
test('esta prueba no falla',()=>{
    if( 1=== 0){
        throw new Error('No puede dividir en cero')
    }
});
```

Ejecutamos nuestra primera prueba con

```jsx
yarn test
```

Instalamos comandos para que sea mas facil recordar los comandos

```jsx
yarn add -D @types/jest
```

Con describe agregamos titulos a nuestras pruebas

```jsx
describe('Pruebas en <DemoComponent/>',()=>{
    test('esta prueba no falla',()=>{
        //1.Inicializacion 
        const message1 = 'Hola Mundo';
        //2.Estimulo
        const message2 = message1.trim();
        //3.Observar el Comportamiento
        expect(message1).toBe( message2 )
    });
})
```

### Solucion a error de compatibilidad con JS moderno

Instalamos babel-jest para evitar problemas de js moderno

```jsx
yarn add --dev babel-jest @babel/core @babel/preset-env
```

Ademas debemos crear babel.config.cjs en la raiz con:

```jsx
module.exports = {
  presets: [['@babel/preset-env', {targets: {node: 'current'}}]],
};

```

### 2 - Prueba

Se crea en en directorio espejo dentro de Test. Esta prueba devuelve error porq se incluyen !!! que no estan presentes en message

```jsx

import { getSaludo } from "../../base-pruebas/base-pruebas/02-template-string";

describe('Pruebas en 02-template-string',()=>{
    test('getSaludo debe retornar Hola Fernando', ()=>{
        const name = 'Fernando'
        const message = getSaludo(name)
        expect(message).toBe(`Hola ${ name }!!!`)
    });
});

```

### 3 - Prueba con objetos

Se utiliza .toStrictEqual para comparar objetos. En este ejemplo recibiremos un error cuando por ejemplo se manda un objeto sin una propiedad

```jsx
import { getUser } from "../../base-pruebas/base-pruebas/05-funciones"
import { getUsuarioActivo } from "../../base-pruebas/base-pruebas/05-funciones"


describe('Pruebas en 05-funciones',()=>{

    test('getUser debe de retornar un objeto', () => {
        const testUser = {
            uid: 'ABC123',
            username: 'El_Papi1502'
        }
        const user = getUser()
        expect( testUser).toStrictEqual(user);
    })

    test('getUsuarioActivo debe de retornar un objeto', () => {

        const name = 'Fernando'
        const testUserActivo = {
            uid: 'ABC567',
            username: name
        }
        const user = getUsuarioActivo(name)
        expect( user ).toStrictEqual(testUserActivo);

    })
})
```

### 4 - Prueba Tipos de elementos de un array

Esta prueba devolvera error porque typeof numbers no es un 'string'

```jsx
import { retornaArreglo } from "../../base-pruebas/base-pruebas/07-deses-arr"

describe('Pruebas en 07-deses-arr', () => { 

    test('Debe de retornar un string y un numero', () => {    
    const [letters,numbers]  = retornaArreglo()
    expect(letters).toBe( 'ABC' );
    expect(numbers).toBe( 123 );
    expect(typeof letters).toBe('string')
    expect(typeof numbers).toBe('string')
    expect(letters).toEqual(expect.any(String)) //espera cualquier tipo de string

    })
})
```

### 5 - Prueba

Esta prueba compara resultados de funciones con objetos y arreglos

```jsx
import { getHeroeById, getHeroesByOwner } from "../../base-pruebas/base-pruebas/08-imp-exp";

describe('Pruebas en 08-imp-exp', () => {

    test('getHeroeById debe de retornar un heroe por ID', () => {
        const id = 1
        const hero = getHeroeById(id);
        expect(hero).toEqual({ id: 1, name: 'Batman', owner: 'DC' })
    })

    test('getHeroeById debe de retornar undefined si no existe ID', () => {
        const id = 100
        const hero = getHeroeById(id);
        expect(hero).toBe(undefined)
    })

    test('getHeroeByOwner debe de retornar undefined si no existe ID', () => {
        const owner = 'DC'
        const heroes = getHeroesByOwner(owner);
        expect(heroes.length).toBe(3)
        expect(heroes).toEqual([
            { "id": 1, "name": "Batman", "owner": "DC" },
            { "id": 3, "name": "Superman", "owner": "DC" },
            { "id": 4, "name": "Flash", "owner": "DC" }])
    })

    test('getHeroeByOwner debe de retornar heroes de Marvel', () => {
        const owner = 'Marvel'
        const heroes = getHeroesByOwner(owner);
        expect(heroes.length).toBe(2)
        expect(heroes).toEqual(heroes.filter((heroe) => heroe.owner === owner))
    })

})
```

### 7 - Prueba asincronas con then y catch

Se usa return resolve y rejects para retornar las pruebas

```jsx
import { getHeroeByIdAsync } from "../../base-pruebas/base-pruebas/09-promesas";
import heroes from '../../src/data/heroes';
describe('Pruebas en 09-promesas', () => { 

    describe('Pruebas en 09-promesas', () => {
    
        test('getHeroesByIdAsync debe retornar un héroe async', ()  => {
            const id = 1;
            return expect(getHeroeByIdAsync(id)).resolves.toBe(heroes[0]);
        });
         
        test('debe de obtener un error si el heroe por id no existe', () => {
            const id = 10;
            return expect(getHeroeByIdAsync(id)).rejects.toMatch('No se pudo encontrar el héroe');
        });
    })
})
```

### 8 - Prueba async y await

Se hicieron pruebas donde se comprueba q el url sea un string

```jsx
import { getImagen } from "../../base-pruebas/base-pruebas/11-async-await";

describe('Pruebas en 11-async-await.js', () => { 

    test('getimagen debe de retornar un URL', async() => { 
        const url = await getImagen();
        expect(typeof url).toBe('string')
     })

     test('getimagen debe de retornar un error si no tenemos apikey', async() => { 
        const resp = await getImagen();
        expect(resp).toBe('No se encontro la imagen') 
     })

 })
```

### 9 - Prueba en componentes de React

La idea de las pruebas es q evealuemos todas las posibilidades para asegurarnos de que nuestra aplicacion ande de la manera esperada, ejemplo queremos asegurarnos de que se renderize el logo de una empresa. nos aseguramos de q el codigo ande como cuando creamos el componente.
Desde react 18 existen problemas para usar solo jest por lo que vamos a usar tambien react testing library. Vamos a usar jest para usar el tobe el test etc.
React testing library es muy bueno para trabajar en el DOM virtual. React testing library por ejemplo hace clic en un boton y observamos si la respuesta es la que queriamos. Si queremos evaluar si algo llego al backend podemos crear una funcion ficticia para evaluarlo (jest no es tan bueno para hacer evaluaciones del DOM).

1 - Instalamos react testing library

```bash
yarn add --dev @testing-library/react
yarn add -D jest-environment-jsdom
```

Creamos el siguiente archivo de configuracion en la raiz ./jest.config.cjs

```jsx
module.exports = {
    testEnvironment: 'jest-environment-jsdom',
    setupFiles: ['./jest.setup.js']
}
```

El codigo para este test es

```jsx
import { render } from "@testing-library/react"
import { FirstApp } from "../src/FirstApp"

describe('Pruebas en <First App />', () => { 
    
    test('Debe hacer match con el snapshot', () => { 
        render(<FirstApp />)

     })
 })
```

El render como tal hace varias cosas allá ya había mencionado.Una de ellas es que actualiza el objeto screen, que es propio del viaje Testing Library. El render también expone ciertas. Bueno, retorna un objeto que expone ciertas propiedades, una de ellas es el container, el container.

 -expect(container).toMatchSnapshot()

Ahora la barra lateral y van a ver que ahora, como por arte de magia, apareció una carpeta que se llama Snapshot. Toma una fotografia del componente y lo almacena fisicamente. Si modificamos algo en jsx de mi First App vemos q se modifico con respecto al snapshot si presionamos la tecla u ahce otra snapshot. esta prueba se ahcegura de q no vaya a cambiar mi componente de manera accidental. Con w y luego u actualizamos el snapshot

```jsx
import { render } from "@testing-library/react"
import { FirstApp } from "../src/FirstApp"

describe('Pruebas en <First App />', () => { 
    
    // test('Debe hacer match con el snapshot', () => { 
    //     const title = 'Hola, Soy Goku'
    //     const {container} = render (<FirstApp title = {title} />)
    //     expect(container).toMatchSnapshot()
    //  })

    test('Debe mostrar el titulo en un h1', () => { 
        const title = 'Hola, Soy Goku'
        const {container, getByText } = render (<FirstApp title = {title} />)
        expect(getByText(title)).toBeTruthy()
        // const h1 = container.querySelector('h1')
        // expect(h1.innerHTML).toBe(title) //o toContain en caso q haya espacios en el titulo
    })

 })
 ```

### 10 - Prueba en componentes de React con getBytestId

La prueba del snapshot ayuda a asegurarse que el componente se queda así por un periodo de tiempo. Pero si están en desarrollo, no hagan la prueba del snapshot porque les va a dar mucho dolor de cabeza.

Ahora nuestras pruebas tienen que ser relativamente flexibles.Siempre tienen que evaluar lo que nosotros creemos, pero a la vez tienen que ser flexibles.Lo realmente importante es solamente que no sean un verdadero dolor de cabeza, porque si yo los hago tan estrictas como yo necesito, puede que perdamos flexibilidad y pues después puede ser que ustedes

<h 1 data-testid="test-title">{ title }</h1> puedo dar un test id, entonces puedo buscar por mi test id

```jsx
import { render } from "@testing-library/react"
import { FirstApp } from "../src/FirstApp"

describe('Pruebas en <First App />', () => {

    test('Debe mostrar el titulo en un h1', () => {
        const title = 'Hola, Soy Goku'
        const { container, getByText, getByTestId } = render(<FirstApp title={title} />)
        expect(getByText(title)).toBeTruthy()
        const h1 = container.querySelector('h1')
        expect(h1.innerHTML).toBe(title) //o toContain en caso q haya espacios en el titulo
        expect(getByTestId('test-title').innerHTML).toBe(title)
    })

    test('Debe de mostrar el subitiulo enviado por props', () => {
        const title = 'Hola, Soy Goku';
        const subTitle = 'Soy un subtitulo';
        const { getByText } = render(
            <FirstApp
                title={ title } 
                subTitle={ subTitle }
                />
            );
        expect(getByText(subTitle)).toBeTruthy() 

    })
})
 ```

Ojo si hay mas de 1 subTitle encontrado ddara error usar getAllByText pero devuelve un arreglo ahi tebemos usar por ej ...getAllByText(subtitle).length).ToBe(3)

### 12 - Screen Testing Library
La refactorización se realiza con el objetivo de hacer el código más legible y fácil de mantener. En lugar de definir variables y utilizar contenedores para cada prueba, se utilizan constantes y se importa el objeto "screen" de React Testing Library para acceder al DOM renderizado. También se muestra cómo se pueden crear snapshots y hacer comprobaciones más precisas utilizando el objeto "screen".

```jsx
import { render, screen } from "@testing-library/react"
import { FirstApp } from "../src/FirstApp"

describe('Pruebas en <First App />', () => {

    const title = 'Hola, Soy Goku'
    const subTitle = 'Soy un subtitulo'

    test('debe de hacer match con el snapshot', () => {
        const { container } = render(<FirstApp title={title} />)
        expect(container).toMatchSnapshot();
    })

    test('debe de mostrar el mensaje "Hola, Soy Goku"', () => {
        render(<FirstApp title={title} />)
        expect(screen.getByText(title)).toBeTruthy()
        // es todo el componente renderizado (el body) la ultima version actualizada despues de los camibos del DOM
    })

    test('debe de mostrar el titulo en un h1', () => {
        render(<FirstApp title={title} />);
        expect(screen.getByRole('heading', { level: 1 }).innerHTML).toContain(title)

    })

    test('debe de mostrar el subtitulo enviado por props', () => {
        render(
            <FirstApp
                title={title}
                subTitle={subTitle}
            />
        );
        expect(screen.getAllByText(subTitle).length).toBe(1)
    })

})
```

### 13 - CounterApp

 La primera prueba consiste en hacer un expect del container para que haga match con un snapshot, y la segunda prueba es que debe demostrar el valor inicial de 100. Los estudiantes deben asegurarse de importar correctamente los componentes necesarios y seguir las instrucciones dadas.

```jsx
import { render, screen } from "@testing-library/react"
import { CounterApp } from "../src/CounterApp"

describe('Pruebas en el <CounterApp/>', () => {

    const initialValue = 10

    test('debe hacer match con el snapshot', () => {
        const { container } = render(<CounterApp value={initialValue} />)
        expect(container).toMatchSnapshot()
    })

    test('debe de mostrar el valir inicial de 100 <CounterApp value={100}', () => {
        render(<CounterApp value={100} />)
        expect(screen.getByText(100)).toBeTruthy()
    })

})
```

### 13 - CounterApp simulador de clicks

El evento "click", el cual nos permite simular cualquier interacción que una persona puede hacer en nuestra página. Recordemos que nosotros estaremos haciendo los clics directamente en el DOM o en la representación que tenemos en nuestro componente, y no en el HTML.
Para empezar, creamos un texto que dice "debe incrementar con el botón más uno". Hay diferentes maneras de tomar los elementos del DOM, y en este video se enseñan varias para que puedas elegir la que más te guste o resulte más fácil para ti. Luego, inicializamos nuestro objeto de pruebas y lo configuramos para que comience en el valor de 10.

Una vez que tenemos nuestro objeto de pruebas, podemos proceder a simular el evento "click". Para hacerlo, utilizamos la función "fireEvent" de Testing Library. Le indicamos que queremos hacer un "click" en el elemento que hemos elegido, en este caso un botón con la etiqueta "más uno".

Después, hacemos una aserción para verificar que el valor del texto ha incrementado en 1 unidad. Para ello, utilizamos el método "getByText" de nuestro objeto de pruebas para obtener la referencia al elemento que contiene el valor actual, que debe ser 10. Finalmente, esperamos que el valor del texto sea igual a 11 y utilizamos el método "toBeTrue()" para verificar que la aserción se cumple.

En general, hay muchas formas de tomar elementos del DOM y probarlos. 

```jsx
import { render, screen,fireEvent } from "@testing-library/react"
import { CounterApp } from "../src/CounterApp"

describe('Pruebas en el <CounterApp/>', () => {

    const initialValue = 10

    test('debe hacer match con el snapshot', () => {
        const { container } = render(<CounterApp value={initialValue} />)
        expect(container).toMatchSnapshot()
    })

    test('debe de mostrar el valir inicial de 100 <CounterApp value={100}', () => {
        render(<CounterApp value={100} />)
        expect(screen.getByText(100)).toBeTruthy()
    })

    test('debe de incrementar con el boton +1', () => {
        render(<CounterApp value={initialValue} />)
        fireEvent.click( screen.getByText('+1') )
        expect(screen.getByText('11')).toBeTruthy();
    })

    test('debe de incrementar con el boton -1', () => {
        render(<CounterApp value={initialValue} />)
        fireEvent.click( screen.getByText('-1') )
        expect(screen.getByText('9')).toBeTruthy();
    })

    test('debe de funcionar el boton de reset', () => {
        render(<CounterApp value={initialValue} />)
        fireEvent.click( screen.getByText('+1') )
        fireEvent.click( screen.getByText('+1') )
        fireEvent.click( screen.getByText('Reset') )

        fireEvent.click(screen.getByRole('button', {name: 'btn-reset'}) )
        expect(screen.getByText(initialValue)).toBeTruthy();
    })

})
```


### Documentacion

1. 📜 [jestjs-oficial](https://jestjs.io/docs/expect)
