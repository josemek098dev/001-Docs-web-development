<div align="center">


![Day 5](./images/banners/Git_Banner1.png)

  <h1> Git y Github </h1>
  

  <sub>Author:
  <a href="" target="_blank">Jose A. Cordoba</a><br>
  <small> April, 2023</small>
  </sub>
</div>

## Resumen

### Comandos útiles de consola

- `touch`: crea un archivo
- `ls -a`: muestra todos los archivos y carpetas ocultos
- `q`: salir de donde estemos

### Comandos útiles de Git-Github (S21)

- `git init`: inicia git en la ruta (1)
- `git status`: muestra los archivos sin seguimiento
- `git add`: Working Directory  ->  Staging Area  (2)
- `git add .`: agrega todos los archivos al área de seguimiento
- `git commit -m “…”`:  Staging Area  ->  Local Repository  (3)
- `git log`: muestra información de todos los commits
- `git checkout`:  Working Directory  <-  Local Repository
- `git diff`: muestra las diferencias entre los commits
- `git remote add origin https://github.com/josemek098dev/EP-.git`: agrega la ruta a la que se subirá el repositorio (4)
- `git push -u origin master`:  Local Repository  ->  Remote Repository  (5)
- `git pull https://github.com/josemek098dev/EP-.git master`:  Working Directory  <-  Remote Repository
- `git rm --cached -r .`: remueve todos los archivos de Staging Area 
- `!folder .gitignore`: agrega archivos que no queremos subir
- `git clone ***`: clona repositorio en el directorio actual
- `git branch ***`: crea una nueva rama con el nombre ***
- `git branch`: muestra la rama en uso
- `git checkout “la rama”`: cambia a “la rama”
- `git merge “la rama”`: estando en master combinamos “la rama” con master
- `! -insights -network`: ve la gráfica de los merges y los commits
- `! README.md`: se puede poner una ayuda para entender el repositorio
- `! challenge de Angela`: https://learngitbranching.js.org/
- `! Fork`: hace una copia de un repositorio remoto de otra persona solo en Github

### Flujo de trabajo con Fork y Pull request

- `WD -> SA -> LR -> RR |Fork->|v|<-Pullreq| RR <-> LR`
- `1—--2—--3   (mi computadora)`
- `|---1*--|`
- `–3! (computadora de otra persona)`
- `A! Create pull request: sugiero cambios al autor del primer repositorio`
- `B! Pull request: veo lo que me sugirieron`
- `1! Review changes`
- `2! Submit review`
- `3! Merge pull request`
- `4! Confirm the merge`
- `.Comment`
- `.Approve`
- `.Request changes`

### Tips de Angela (S21)

- Repetir espaciado, revisar cada semana un tema o algo similar.
- Utilizar `git checkout --.` para volver a la última versión de los archivos.
- Se puede hacer control de versiones desde VSCode sin necesidad de la consola.
- No trabajar en la rama principal (`main` o `master`). Siempre crear una nueva rama.
- Observar cómo se cargan los cambios en el círculo naranja de VSCode. Luego aparecerá en verde.
- Ver el proceso de pages build and deployment y hacer clic en el enlace que nos lleva a la página.
- Configurar para que un archivo pueda ser subido a pages

Claro, continuando con la lista:

### Comandos esenciales de Git

Aquí hay una lista de comandos esenciales de Git que son útiles para trabajar con repositorios:

1. `git init`: inicializa un nuevo repositorio Git vacío en la carpeta actual.
2. `git add <file>`: agrega un archivo al área de preparación (también conocida como área de ensayo o staging area).
3. `git add .`: agrega todos los archivos nuevos o modificados al área de preparación.
4. `git commit -m "<mensaje>"`: guarda los cambios en el repositorio y registra un mensaje descriptivo.
5. `git status`: muestra el estado actual del repositorio.
6. `git log`: muestra una lista de todos los commits realizados en el repositorio.
7. `git checkout <commit>`: cambia al commit especificado.
8. `git branch`: muestra una lista de todas las ramas en el repositorio.
9. `git branch <name>`: crea una nueva rama con el nombre especificado.
10. `git checkout <name>`: cambia a la rama especificada.
11. `git merge <name>`: fusiona la rama especificada con la rama actual.
12. `git remote add origin <url>`: agrega un repositorio remoto con el nombre "origin".
13. `git push -u origin master`: empuja los cambios locales al repositorio remoto "origin" en la rama "master".

### Modificar un commit

Si es necesario modificar un commit existente, se puede utilizar el siguiente comando:

```
git commit --amend
```

Este comando abre el editor de texto predeterminado y le permite cambiar el mensaje del commit. También se puede utilizar para agregar o eliminar archivos del commit.

### Crear y eliminar ramas

Para crear una nueva rama, se puede utilizar el siguiente comando:

```
git branch <nombre-de-la-rama>
```

Para cambiar a una rama existente, se puede utilizar el siguiente comando:

```
git checkout <nombre-de-la-rama>
```

Para fusionar una rama en otra, primero se debe cambiar a la rama que se desea actualizar y luego utilizar el siguiente comando:

```
git merge <nombre-de-la-rama-a-fusionar>
```

Para eliminar una rama, se puede utilizar el siguiente comando:

```
git branch -d <nombre-de-la-rama-a-eliminar>
```

### Git y GitHub Pages

GitHub Pages es un servicio de alojamiento web que permite a los usuarios publicar sitios web directamente desde un repositorio de GitHub. Para habilitar GitHub Pages para un repositorio, se debe seguir los siguientes pasos:

1. Crear un archivo README.md en la carpeta raíz del repositorio.
2. Configurar el archivo `_config.yml` con información básica del sitio web, como el título y la descripción.
3. Habilitar GitHub Pages en la configuración del repositorio.

Después de hacer estos pasos, se puede acceder al sitio web en `https://<nombre-de-usuario>.github.io/<nombre-del-repositorio>`.

Espero que esto te haya sido de ayuda. Si tienes alguna otra pregunta, ¡no dudes en preguntar!

### Documentacion

1. 📜 [Git-GitHub FreeCodeCamp](https://www.youtube.com/watch?v=mBYSUUnMt9M)

