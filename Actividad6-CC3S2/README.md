# Actividad 6
## Resumen del entorno:
- OS: Ubuntu 24.04.3 LTS
- Shell(Bash): 5.2.21(1)-release
- git: git version 2.43.0
Con `git config` se puede configurar Git en diferentes niveles, en general se suele usar para configurar el nombre de usuario y email de forma global usando `git config --global user.name` y `git config --global user.email`
## git init
Con `git init` se inicia un repositorio git en el folder actual, en el cual se crea un directorio `.git` (oculto por defecto) el cual tiene la configuración necesaria para el control de versiones.
## git add
Con `git add` se le indica a git que haga un seguimiento de ciertos cambios hechos en un repositorio, ya sea en archivos especificos si se nombran luego de `add`, o todos los cambios hechos con `git add .`.
## git commit
Con `git commit` se registran los cambios en el repositorio de los cuales se tenia seguimiento, como hacer una marca en una linea de tiempo, a la cual se le adjunta un mensaje corto con `git commit -m "<Mensaje aqui>"` con el cual se añade claridad.
## git log
Siguiendo la analogía anterior, con `git log` se puede ver esta linea de tiempo con todos los cambios hechos, incluyendo quien hizo el commit, marca de tiempo de cuando se hizo, un identificador hash y el mensaje del commit
### Pregunta 1: ¿Cual es la salida de este comando?
La salida de `git log --graph --pretty=format:'%x09 %h %ar ("%an") %s'` lo que hace es mostrar los commits con una estructura parecida de arbol a la izquierda, mostrando las ramas y merges, e imprime solo información pertinente (hace cuanto tiempo se realizo el commit, nombre de usuario, primeros caracteres de hash y mensaje) con un formato definito por `--pretty=format:'%x09 %h %ar ("%an") %s'`
### Pregunta 2:
Se ejecutan los comandos... 
```bash
820d606 (HEAD -> master) Agrega main.py
f598d64 Configura la documentación base del repositorio
acb8d73 Commit inicial con README.md
```
## git branch
`git branch` permite tanto ver todas las ramas del repositorio como crear nuevas a partir de otras o de commits especificos, dependiendo de que argumentos y opciones se le pase al comando. También se pueden eliminar usando `git branch -d`
## git checkout/git switch
Con `git checkout` se puede cambiar la posición actual en la que nos encontramos, sea en la punta de una rama en especifico o incluso un commit específico (en modo de `detached-HEAD`).
## git merge
`git merge` permite la combinación de dos ramas (conocida como fusión), lo cual puede ser util si por ejemplo se desarrollaron cambios de una rama en otra para evitar interferir con la principal y estos cambios ya han pasado las pruebas requeridas para reincorporarse. Se puede complicar si hay conflictos entre ramas.
##PREGUNTAS:
### ¿Cómo te ha ayudado Git a mantener un historial claro y organizado de tus cambios?
El historial de git, visible con `git log` fue de gran ayuda para esto, me permitió ver mis cambios de forma ordenada, junto con las descripciones breves que le daba a cada cambio para cada commit.
### ¿Qué beneficios ves en el uso de ramas para desarrollar nuevas características o corregir errores?
Uno de los mas grandes beneficios es que permite poder desarrollar nuevas caracteristicas de forma segura sin tener que interferir con la version estable (el main), pudiendo volver a esta en caso ocurra un error fatal. Tambien que permite que varias características se puedan desarrollar de forma paralela, sin tener que esperar que una termine para empezar otra, y sin una interferir con otra.
### Realiza una revisión final del historial de commits para asegurarte de que todos los cambios se han registrado correctamente.
```bash
commit 820d606581cad8b1b8bf28341a069747977e2630 (HEAD -> master, feature/new-feature, feature/another-new-feature)
Author: MathiasVilca <email>
Date:   Sat Sep 27 23:41:22 2025 -0500

    Agrega main.py

commit f598d641f1b11546fec75768a797d95ffbf91517
Author: MathiasVilca <email>
Date:   Sat Sep 27 23:36:09 2025 -0500

    Configura la documentación base del repositorio

commit acb8d73f29142fcbe30ebbb9d393098265eaa179
Author: MathiasVilca <email>
Date:   Sat Sep 27 22:21:27 2025 -0500

    Commit inicial con README.md

```
### Revisa el uso de ramas y merges para ver cómo Git maneja múltiples líneas de desarrollo.
Se ejecuta `git branch`...
```bash
  feature/another-new-feature
  feature/new-feature
* master
```
##Ejercicio


