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

Para eso es importante hacer **git log --oneline** y capturar los ID **a378677**, no es necesario colocar el git log que muestra mas informacion

```bash
git checkout a378677
```







Search
github esta cambiando de master a main

