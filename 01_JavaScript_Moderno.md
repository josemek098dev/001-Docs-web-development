<div align="center">

![Day 5](./images/banners/js.jpg)

  <h1> JavaScript Moderno </h1>
  

  <sub>Author:
  <a href="" target="_blank">Jose A. Cordoba</a><br>
  <small> April, 2023</small>
  </sub>
</div>

  - [Indice](##Variables_y_constantes)
    - [Variables y constantes](###Variables_y_constantes)
    - [Template String](#TemplateString)
    - [Arreglo](#Arreglo)
    - [Funciones](#Funciones)
    - [Desestructuracion de Objetos](#Desestructuracion_de_Objetos)
    - [Desestructuracion de Arreglos](#Desestructuracion_de_Arreglos)
    - [Import, export y funciones comunes de arreglos](#Import,_export_y_funciones_comunes_de_arreglos)
    - [Multiples exportaciones y exportaciones por defecto](#Multiples_exportaciones_y_exportaciones_por_defecto)
    - [Promesas](#Promesas)
    - [Fetch API](#Fetch_API)
    - [Async - Await](#Async_-_Await)
    - [Operador condicional ternario](#Operador_condicional_ternario)
  

##  Resumen
### Variables y constantes
```js
var // ya no se usa
let // si voy a cambiar el valor
const // si jamas voy a cambiar el valor de la constante
No puede haber dos constantes en el mismo scope con el mismo nombre
```

### Template String

```js
`  Hola ${ saludo } `  // puedo poner codigo de js dentro de { }  y br dentro de ``
```

### Objetos literales

```js
const persona = {
    nombre: ' Tony'
    apellido: ' Tony'
    edad: 45
}
{ persona } || persona:persona

```

### Arreglo

```js
const arreglo = [1,2,3,4]
```
No se reocomienda usar push por q modifica el arreglo, usar en su lugar el operador spread que manda indivudalmente cada uno de los elementos del arreglo.

```js
const arreglo2 = [...arreglo,5]
const arreglo3 = arreglo2.map(function(numero){
    return numero*2
}) // salida [2,4,6,8,10] crea un nuevo arreglo y no modifica el anterior

```

### Funciones
No se recomienda esta forma de escribir una funcion fomenta errores en las asignaciones de nombres

```js
function saludar(nombre){
return `Hola, ${nombre}`
}

```
Funciones de flecha

```js
const saludar2 = (nombre) => {
    return `Hola, ${nombre}`
}
const saludar3 = (nombre) => `Hola, ${nombre}`
const saludar4 = () => `Hola, Mundo`

```

### Desestructuracion de Objetos
Extrae lo que pongo dentro de las llaves del objeto persona, no es necesario seguir un orden.

```js
const persona = {
    nombre: 'Tony',
    edad: '45',
    clave: 'Iroman',
};

const{ nombre, edad,clave  } = persona; || { nombre:nombre2 }

console.log( nombre ) // Tony

```
Puedo desestructurar en el argumento de una funcion ademas de crear una propieadd y definirla.

```js
const retronaPersona = ({ nombre, edad, rango ='Capitan' }) => {
    console.log( nombre, edad, rango)
}
retornaPersona( persona) // Tony 45 Capitan
```
Desestructuracion anidadad. Extrae el objeto dentro del objeto y lo reasigna.

```js
const { objeto1:{objeto12} } = obj12 
```


### Desestructuracion de Arreglos

```js
const personajes = ['Goku', 'Vegeta', 'Trunks''];
const [ goku ] = personajes;
console.log( goku ) // Goku
const [ , vegueta ] = personajes;
console.log( vegueta ) // Vegueta
```
Saltea el nombre de goku al restructurar al poner la ","

```js
const retornaArreglos = () => [ 'ABC', 123 ];
const [ letras, numeros ] = retornaArreglo();
console.log( letras, numeros ); // ABC 123

```
Se puede desestructurar el resultado de una funcion
```js
const useState = ( valor ) => {
	return [ valor, ( ) => { console.log( 'Hola Mundo' ) } ]
};

const arr = useState ('Goku')
arr[1]( ); // Hola mundo

```
Esto no es recomendable es mejor desestructurar y llamar a la funcion, en vez de arr usar algo asi [ val, funhm] = …

### Import, export y funciones comunes de arreglos

```js
export const heroes = [ { , ,  }, { , , }, { , , }, { , , }, … ] // esto esta en otro archivo 
	import { heroes } from ' ./data/heroes '
	console.log( heroes )
	const getHeroeById = ( id ) => {
		return heroes.find( ( heroe )  => heroe.id === id
}
console.log( getHeroeById( 2 ) ); //{ id:2, name: "Spiderman", owner: "Marvel" }
```
Find recorre cada objeto dentro del objeto heroes y al encontrar una coincidencia devuelve el objeto
```js
const getHeroeByOwner = ( owner ) => {
		return heroes.filter( ( heroe )  => heroe.owner === owner
}

```
Filter recorre cada objeto dentro del arreglo heroes y al encontrar coincidencias devuelve todos los objetos con coincidencias
### Multiples exportaciones y exportaciones por defecto

```js
export default [ { , ,  }, { , , }, { , , }, { , , }, … ] // no hace falta " const heroes = "
```
Al hacer la importacion podemos pooner cualquier nombre luego del import y funciona igual. Es mas recomendable dejar " const heroes = " y poner al final:

```js
export default heroes
```
Si estamos ocupando en simultaneo exportaciones por defecto y una exportacion individual vamos a importarlos

```js
import heroes, { owners } from ' ./data/heroes '
```
Otra forma de exportar seria
```js
export { 
    heroes as default,
    owners
}

```

### Promesas
Tenemos que ver este tema de manera similar a como son las promesas en la vida real

```js
const promesa = new Promise( ( resolve, reject ) => {
	setTimeout( ( ) => {
		const heroe = 'Spiderman'
		resolve( heroe ); || reject ( ' error ')
	} , 2000 )
} );
promesa.then( (heroe ) => {
console.log( 'heroe' ) // dos segundos despues se ejecuta esto
})
.catch( err => console.warm ( err ) )
```
resolve se ejecuta cuando la promesa se cumple 
reject cuando la promesa falla


### Fetch API
Viene incluida en los navegadores. ( se uso Json Viewer Awesome)

```js
const peticion = fetch ( url-giphy )
	peticion
.then ( resp => resp.json ( ) )
.then ( { data } => console.log ( data.images.orginal.url  ) ) 
.catch( console.warm )
	console.log( resp )
}

```

### Async - Await

```js
const getImagen = async( ) => {   // al escribir async ya  tengo una promesa
	return ' link'
}
getImagen( ).then( console.log )
```
Await cuado se usa junto con Async permite ejecutar el codigo como si fuera sincrono. Para manejar errores podemos usar try { } catch { }. 

```js
const getImagen = async( ) => {   
	const resp = await fetch ( … )
	const data = await resp.json();
	console.log( data )
}
getImagen( )

```

### Operador condicional ternario

```js
	const activo = true
	const mensaje = (activo === true) &&  'Activo'
	console.log( mensaje ) // Activo

```
### Otros sitios interesantes para aprender

1. 📜 [Developer-Mozilla](https://developer.mozilla.org/es/docs/Web/JavaScript)

2. 📜 [ Airbnb-JavaScript](https://github.com/paolocarrasco/javascript-style-guide)

3. 📜 [ 30-Days-Of-JavaScript](https://github.com/Asabeneh/30-Days-Of-JavaScript#-day-1)


