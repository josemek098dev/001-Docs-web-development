# JavaScript

Se reocomienda buscar informacion adicional en  MDN web docs

 Iniciar un proyecto
npx create-react-app my-app // creamos la base de un doc de react
cd my-app
npm start // iniciamos la app en localhost 3000
# Variables y constantes
var // ya no se usa
let // si voy a cambiar el valor
const // si jamas voy a cambiar el valor de la constante
No puede haber dos constantes en el mismo scope con el mismo nombre
 Template String
`  Hola ${ saludo } `  // puedo poner codigo de js dentro de {}  y br dentro de (templates strings)

 Objetos literales
const persona = {
            	nombre: ' Tony'
apellido: ' Tony'
edad: 45
}
{ persona } || persona:persona
# Arreglo
            	const arreglo = [1,2,3,4]
No se reocomienda usar push por q modifica el arreglo, usar en su lugar el operador spread que manda indivudalmente cada uno de los elementos del arreglo
            	const arreglo2 = [...arreglo,5]
            	const arreglo3 = arreglo2.map(function(numero){
                           	return numero*2
}) // salida [2,4,6,8,10] crea un nuevo arreglo y no modifica el anterior


## Instalación

1. Clone el repositorio.
2. Ejecute el comando `npm install`.
3. Ejecute el comando `npm start`.

## Uso

Breve descripción de cómo usar el proyecto.

## Contribución

1. Cree un fork del repositorio.
2. Cree una nueva rama con `git checkout -b nueva-rama`.
3. Haga sus cambios y confirme con `git commit -m 'descripción de los cambios'`.
4. Empuje la rama a su repositorio con `git push origin nueva-rama`.
5. Cree una nueva solicitud de extracción en Github.

## Código de ejemplo

Aquí hay un ejemplo de cómo imprimir "Hola, mundo!" en Python:

```python
print("Hola, mundo!")
