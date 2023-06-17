# Git y github bluuweb


- Con `git add` pasa de *working directory* a *staging area*
- Con `git commit` pasa de *staging area* a *local repo*
- Con `git push` pasa de *local repo* a *remote repo*
- Con `git fetch` pasa de *remote repo* a * *local repo*
-
-


## Comandos

```shell
git status -s // ver que archivos han sido registrados
```


```shell
git log --oneline // muestra la lista de commit del mas reciente al mas antiguo
```

## Notas

Salir del modo *Vim*
Para salir del modo de edicion de las lineas de comandos presionar :q en caso de realizar algun cambio sin guardar escribir :qa o :q!

Al colocar los mensajes de commit no usar tildes porque saldran unos signos extraños

-Si estoy trabajando en otra computadora y ya estaba registrada con git, necesito eliminar esos certificados
-Busco en el panel de control -> administrar credenciales -> quitar
-Desconozco si se puede trabajar con dos cuentas a la vez?
-

Tambien se pueden probar las paginas web estaticas en netlify.com



## GitHub

Antes los repositorios privados eran pagos, ahora son gratis

Agregar repositorio local a github:
git remote add origin https://github.com/repositorio/.git
git branch -M main
git push -u origin main

Con `git log --online` verificamos el nombre de la rama principal, para saber si es *main* o *master* y lo colocamos des pues de -M y despues de -u origin

Luego abre un login y pedirá las credenciales de mi cuenta

En los siguientes cambios que realizemos solo habrá que escribir 
`git push` y se subiran los cambios

```shell
git remote -v // Nos muestra en que repositorio estamos trabajado remotamente
```



## Git hub pages

-Se podra probar los proyectos (estaticos) (HTML, CSS JS) en un hosting gratuito, en un servidor utilizando github pages
-Para que éste proyecto nos lo muestre en una URL voy a *Settings* -> *Pages*
-Seleccionamos la rama *main o master* y nos indica el  /(root), osea que en la raiz está nuestro HTML para que se lea
-Click en guardar
-Se demora un rato porque tiene que hacer todo l proceso para habilitar ese servidor, si nos genera la URL y al darle click aparece la ventana con un error (ej 404), es porque hay que esperar mas. Puede tardar 5min o se puede bugear y tardar mas (10min)


Para pasar un repositorio remoto a local:

```shell
git clone "nombre del repo"
```

## Git intermedio

Ignorar archivos con .gitignore

Creamos un archivo .env
Crear archivo .gitignore
Este archivo es para variables de entorno, aqui colocamos por ejemplo claves de acceso o contraseñas, nombres de usuario, etc

Para que ésto no aparezca en nuestro repositorio al subirlo, lo agregamos dentro del .gitignore

Al trabajar con node se crea una carpeta que se llama *node_modules*
esa carpeta tampoco la subimos ya sea a un hosting, servidor o a github
por lo tanto ignoramos la carpeta agregandola a .gitignore

Hay mas opciones como ignorar todos los archivos .js o si se quiere ignorar un archivo en especifico dentro de una carpeta

## Retroceder en el tiempo

Trabajando de manera lineal (aun no con ramas)

```bash
git log --oneline
```
Aqui tenemos el registro de todo lo que está pasando en git

Creamos mas archivos y commits -> about.html, contact.html

**git checkout**

Si queremos visitar un commit en especifico
Esto no es para viajar, es solamente para revisar
Para saber por ejemplo, que hicimos en el primer commit, que cambios se habian efectuado en ese momento o como estaba nuestro proyecto en ese espacio del tiempo

Para eso es importante hacer `git log --oneline` y capturar los ID **a378677**, no es necesario colocar el git log que muestra mas informacion

```bash
git checkout a378677
```

Estabamos trabajando en esa linea que se llamaba **master** y ahora no esta, solamente tenemos **(HEAD)**. Con checkout nos hemos movido en este espacio del tiempo, pero solo hemos movido el HEAD, no movimos la rama entera o el master no lo hemos traido, por eso no es recomendable hacer cambios aqui y solamente revisar

Durante el curso normal de desarrollo, HEAD apunta por lo general a la rama main u otra rama local (HEAD -> master), pero cuando extraes una confirmacion anterior, HEAD ya no apunta a una rama, sino que apunta directamente a una confirmacion. Este estado recibe el nombre de "HEAD desasociado" (detached HEAD)
*Ej: a00beae (HEAD) a1-html*

Comprobar un commit estecifico pondra el repositorio en un estado "HEAD desasociado". Esto significa que ya no estas trabajando en ninguna rama

Para cambiarme denuevo al ultimo commit realizado, si ejecute en la terminal git log antes de hacer el checkout, busco el historial y copio el primer ID, ya que despues de hacer el checkout desapareceran del comando git log, todos los commits superiores al que me cambie.
Otra manera de llegar al ultimo commit es con la ayuda de VS Code, en la esquina inferior izquierda me aparece en que rama y en que rama estoy actualmente, en este caso me aparecera el ID dende estoy y al darle click, en la parte superior aparece la opcion de cambiar al master (ultimo cambio)
Tambien al indicar con master/main, me enviara al ultimo commit

```bash
git checkout master
```

Si se hace un commit estando en detached HEAD, en caso de no hacer esa rama, va a quedar como flotando en el espacio ese commit y posteriormente git lo va a eliminar

Por ejemplo realizo cambios en un commit anterior, vuelvo a la rama principal master o main, git recomiendo hacer una nueva rama para el commit huerfano


## Renombrar rama

Para cambiar, por ejemplo, de master a main

Esto cuando estamos trabajando de forma lineal, en una sola rama

De forma global

```shell
git config --global init.defaultBranch main
```

Para un unico proyecto

```shell
git branch -m master main
```


## git reset

Viajar a travez de diferentes commits
Esto es util si aun no has subido tu commit a GitHub

Si estamos por ejemplo en el quinto commit, y queremos ir al primer commit, seria git reset (id del commit al que queremos ir) --mixed

Aqui el mixed se hace por defecto asi que no lo escribimos

```shell
git reset 0a72f38
```

Viajamos a esa parte del tiempo, pero perdemos los cambios que se hicieron despues de ese commit (solo se pierden los commit, pero el codigo que se habia en esos commits, sigue en el archivo, pero ha dejado de darles seguimiento)

Podemos volver al commit que teniamos antes, restaurando asi los commits que desaparecieron despues de viajar
Escribimos el mismo comando, con el ID del commit que estabamos

Se van a reestablecer los commit y los archivos que estaban sin seguimiento, vuelven a la normalidad


## reset hard

Ahora vamos a utilizar un metodo mas destructivo: viajamos al commit en especifico y eliminamos los cambios futuros a ese commit, aqui si se eliminan tanto los commits como los archivos que se crearon posterior al ID que coloquemos

```shell
git reset --hard c97d996
```
En caso de restaurar los cambios podemos utilizar reflog: muestra todos los cambios incluso si borramos los commit

```bash
git reflog
```

Si utilizamos el --hard por equivocacion y no tenemos el ID del commit donde estabamos, usamos el git reflog para ver todo el historial de commits que hecho. Asi podemos buscar el ID del ultimo commit que realizamos y volver ahi usando `git reset --hard` de igual manera, pero esta vez con este ID y restauramos todos los archivos

### Nota: Tener cuidado con reset

Ambos comandos `git revert` y `git reset` deshacen commits anteriores. Pero si ya has subido tu commit a un repositorio remoto, se recomienda que no uses git reset, ya que reescribe el historial de commits

**Solucion: Restaurar la ultima version remota. Con pull**

```bash
 git pull origin YOUR_BRANCH_NAME
```

Ejemplo.
Subimos el repositorio a github, luego escribimos `git reset --hard 346e753`.

Se van los cambios que hice posterior a ese commit.

Prosigo agregando codigo y hago un commit

Y cuando lo subo al repositorio remoto con git push, dará error

Hay un conflicto, ya que en github tenemos un commit con un ID que no existe, es el que elimimamos al hacer reset

Cuando pase esto, escribir el `git pull origin YOUR_BRANCH_NAME`

Si verificamos con `git log`, aparece que hicimos un merged y aparecen todos los commits mezclados. Esa es una alternativa

Como estamos trabajando en una sol rama, esto tambien ocaciona esos problemas

La solucion para esto es revert


## git revert

En lugar de usar git reset, git revert deshace los cambios realizados por un commit anterior creando un commit completamente nuevo, todo ésto sin alterar el historial de commits 

Por ejemplo tenemos 5 commits, el tercero es el que tiene errores o queremos eliminar, seleccionamos su ID y escribimos:

```bash
git revert 346e753
```
El commit seguirá en el historial (al escribir git log, seguira el mismo ID), pero sacamos los cambios que estaban en ese commit e hicmos otro commit, entonces lo tenemos como respaldo

Ahora no habrá problemas al subirlo a github

**Nota**
El git revert cuando lo aplico para eliminar un archivo creado en un commit en especifoco si lo elimina sin alterar ningun otro archivo posterior.
Pero cuando en un mismo archivo, ej h1, h2, h3. tengo varios commits y quiero eliminar el h2, entonces elimina todos los cambios posteriores al h2 o el editor de VSCode me da la opcion de dejar todos los cambios, pero no me da la opcion de quitar unicamente los cambios de un commit sin alterar el resto del codigo, tal como lo haria con un archivo independiente,
Como se hace?


## Ramas o branch

`git branch` // Para ver las ramas que tengo y en cual estoy

`git branch "nombreRama"` //Para crear una nueva rama

`git checkout nombreRama` // Para movernos a la nueva rama

**Atajo**
Podemos utilizar `git checkout -b nombreRama` para crear la nueva rama y viajar a ella directamente

`git log --oneline --graph` // Nos muestra visualmente las ramas. Como funciona?

`git push --set-upstream origin 02-rama` // Para subir la rama a github


## Git Merge

Para unir una rama con la nueva, para eso tenemos que estar en la rama que está esperando los cambios

`git merge nombreRama`

Si aparece **Fast-forward* quiere decir que no hubo ningun conflicto

`git branch -d nombreRama` // Eliminar una rama


### Conflictos

Si se realizan varios cambios en el mismo lugar de un archivo en diferentes ramas, se va a sobreponer un codigo encima del otro

Esto pasaria con diferentes personas en diferentes ramas

Creo un nuevo archivo **services.html** con una estructura html y hago commit, me cambio a la rama `03-services` agrego un h1 con un "hola" y hago commit, cambio a la rama `main` y no tendra titulo, agrego h1 con un "lorem" y hago commit.

Al hacer `git merge` se genera un conflicto



Search
github esta cambiando de master a main
cambiar comentario de un commit
`git log --oneline --graph` como funciona para ver las ramas?