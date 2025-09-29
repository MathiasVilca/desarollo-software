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
## Ejercicios:
Nota, en el repositorio en el que se esta trabajando, la rama principal es master
### Ejercicio 1:
Luego de hacer los commits en cada rama y que Git indicara conflicto, el archivo `main.py` queda así:
```python
<<<<<<< HEAD
print('Hello World-actualiado en main')
=======
print('Hello World')

def greet():
    print('Hello como una función avanzada')

greet()
>>>>>>> feature/advanced-feature
```
Se decidio mantener ambas partes:
```python
print('Hello World-actualiado en main')
print('Hello World')

def greet():
    print('Hello como una función avanzada')

greet()
```
Se ejecuto `git add .` y `git commit -m 'Solucion de conflicto: se combinan ambas versiones'`, merge resultó exitoso.
### Ejercicio 2:
- Luego de ejecutar `git log`, se ven las diferencias en main, desde el primer commit con `README.md`, luego la adición de `CONTRIBUTING.md` y la version inicial de `main.py` (en commits separados), despues la adición de la funcion avanzada `greet()` y la actualización del mensaje main.py, y por último la solucion de conflicto.
- Luego de ejecutar `git log --author="MathiasVilca"`
```bash
commit 38b992f1f751d0d17678107dcb5e135ac60dc846 (HEAD -> master)
Merge: b168882 cb8f9df
Author: MathiasVilca <email>
Date:   Sun Sep 28 12:30:21 2025 -0500

    Solucion de conflicto: Se combinan ambas versiones

commit b168882331ec79321859b1fda6f067e601f5468d
Author: MathiasVilca <email>
Date:   Sun Sep 28 00:22:05 2025 -0500

    Actualizar el mensaje main.py en la rama main

commit cb8f9dffc19f9476880300d394afb6f81bef5fe8
Author: MathiasVilca <email>
Date:   Sun Sep 28 00:21:16 2025 -0500

    Agrega la funcion greet como función avanzada

commit 820d606581cad8b1b8bf28341a069747977e2630

```
- NOTA: aqui se cometio un error en el cual por accidente se creo la rama `caracteristica/collect/MathiasVilca` y se hizo el siguiente ejercicio, de todas formas se volvio a ejecutar `git revert HEAD` lo que revertió el anterior git revert
- El ejecutar `git revert HEAD` falla al ser el anterior commit una fusión y no proveer la opción `-m` la cual especifica cual es la linea principal. Al especificar `master` como la principal, se obtiene:
```bash
[master d3a59be] Revert "Solucion de conflicto: Se combinan ambas versiones"
 1 file changed, 6 deletions(-)
```
y el archivo `main.py` vuelve a estar en 
```python
print('Hello World-actualiado en main')
```
En `git log`:
```bash
commit d3a59be6416ed13fdddd76d66a78fda070dd586e (HEAD -> caracteristica/collect/MathiasVilca, master)
Author: MathiasVilca <email>
Date:   Sun Sep 28 12:51:30 2025 -0500

    Revert "Solucion de conflicto: Se combinan ambas versiones"
    
    This reverts commit 38b992f1f751d0d17678107dcb5e135ac60dc846, reversing
    changes made to b168882331ec79321859b1fda6f067e601f5468d.
```
- `git log` luego de eliminar la rama extra y volver a revertir (ya en `master`)
```bash
commit eef14d7b60dfd702d0ef9d28d70abc574774342e (HEAD -> master)
Author: MathiasVilca <email>
Date:   Sun Sep 28 15:42:45 2025 -0500

    Reapply "Solucion de conflicto: Se combinan ambas versiones"
    
    This reverts commit d3a59be6416ed13fdddd76d66a78fda070dd586e.

commit d3a59be6416ed13fdddd76d66a78fda070dd586e
Author: MathiasVilca <email>
Date:   Sun Sep 28 12:51:30 2025 -0500

    Revert "Solucion de conflicto: Se combinan ambas versiones"
    
    This reverts commit 38b992f1f751d0d17678107dcb5e135ac60dc846, reversing
    changes made to b168882331ec79321859b1fda6f067e601f5468d.
```
- Al ejecutar `git rebase -i HEAD~3` se edita el interactivo
```bash
pick cb8f9df Agrega la funcion greet como función avanzada
s d3a59be Revert "Solucion de conflicto: Se combinan ambas versiones"
s eef14d7 Reapply "Solucion de conflicto: Se combinan ambas versiones"
```
Se crea un conflicto en `main.py` el cual rapidamente se soluciona, y luego de añadirse y terminarse el rebase queda como:
```bash
commit 83b42cfe3cf360561bf123a48d1f67f6d0a215b6 (HEAD -> master)
Author: MathiasVilca <email>
Date:   Sun Sep 28 00:21:16 2025 -0500

    Agrega la funcion greet como función avanzada
    
    Revert "Solucion de conflicto: Se combinan ambas versiones"
    
    This reverts commit 38b992f1f751d0d17678107dcb5e135ac60dc846, reversing
    changes made to b168882331ec79321859b1fda6f067e601f5468d.
    
    Reapply "Solucion de conflicto: Se combinan ambas versiones"
    
    This reverts commit d3a59be6416ed13fdddd76d66a78fda070dd586e.

```

- se ejecuta `git log` se puede ver:
```bash
* 83b42cf (HEAD -> master) Agrega la funcion greet como función avanzada
* b168882 Actualizar el mensaje main.py en la rama main
* 820d606 Agrega main.py
* f598d64 Configura la documentación base del repositorio
* acb8d73 Commit inicial con README.md
```
Se puede inferir merges de diferentes ramas (si estas no se eliminan por supuesto), el número de ramas.
### Ejercicio 3
- De los commits, se crea una nueva rama desde `820d606`
```bash
83b42cf (HEAD -> master) Agrega la funcion greet como función avanzada
b168882 Actualizar el mensaje main.py en la rama main
820d606 Agrega main.py
f598d64 Configura la documentación base del repositorio
acb8d73 Commit inicial con README.md
```
Se cambia `main.py`
```python
print('Hello World')

def greet():
    print('Error corregido en la función')
    
greet()
```
Luego de solucionar conflicto, `git log --graph --oneline` muestra:
```bash
*   6e45828 (HEAD -> master) Solucion de conflicto en main.py
|\  
| * d0f873e (bugfix/rollback-feature) Corregir error en la funcionalidad de rollback
* | 83b42cf Agrega la funcion greet como función avanzada
* | b168882 Actualizar el mensaje main.py en la rama main
|/  
* 820d606 Agrega main.py
* f598d64 Configura la documentación base del repositorio
* acb8d73 Commit inicial con README.md
```
Se puede notar la rama bugfix/rollback-feature en el gráfico a la izquierda
### Ejercicio 4
- Se hacen los cambios y se notan en `git log`
```bash
76a35f6 (HEAD -> master) Introduce un cambio para restablecer
6e45828 Solucion de conflicto en main.py
d0f873e Corregir error en la funcionalidad de rollback
...
```
Luego de `git reset --hard HEAD~1`
```bash
6e45828 (HEAD -> master) Solucion de conflicto en main.py
d0f873e Corregir error en la funcionalidad de rollback
83b42cf Agrega la funcion greet como función avanzada
...
```
- Hacemos cambios en readme sin confirmar:
```bash
En la rama master
Cambios no rastreados para el commit:
  (usa "git add <archivo>..." para actualizar lo que será confirmado)
  (usa "git restore <archivo>..." para descartar los cambios en el directorio de trabajo)
	modificados:     README.md

sin cambios agregados al commit (usa "git add" y/o "git commit -a")
```
Luego de ejecutar `git restore`:
```bash
En la rama master
nada para hacer commit, el árbol de trabajo está limpio
```
### Ejercicio 5
- luego de crear `act6-repo` en github y clonarlo
```bash
* commit 384100e256c572ab4c4958fea500742c36fbd210 (HEAD -> feature/team-feature, origin/feature/team-feature)
| Author: MathiasVilca <email>
| Date:   Sun Sep 28 22:38:18 2025 -0500
| 
|     Agrega script de colaboración
| 
* commit 3379a415db9908ed518bbdac4a189191c08d1373 (origin/main, origin/HEAD, main)
  Author: MathiasVilca <email>
  Date:   Sun Sep 28 22:34:41 2025 -0500
  
      Initial commit

```
Luego de generar PR y de eliminar rama `feature/team-feature`
```bash
* commit 384100e256c572ab4c4958fea500742c36fbd210 (HEAD -> main)
| Author: MathiasVilca <email>
| Date:   Sun Sep 28 22:38:18 2025 -0500
| 
|     Agrega script de colaboración
| 
* commit 3379a415db9908ed518bbdac4a189191c08d1373 (origin/main, origin/HEAD)
  Author: MathiasVilca <email>
  Date:   Sun Sep 28 22:34:41 2025 -0500
  
      Initial commit

```

### Ejercicio 6
- Luego del cambio a `main.py` (se hace un cambio adicional en otro commit por comodidad) y los commits, se elige el previo al cambio (`4c4694d`)
```bash
8ab86cd (HEAD -> feature/cherry-pick) Agrega segundo ejemplo
4c4694d (master) Agrega ejemplo de cherry-pick 
6e45828 Solucion de conflicto en main.py
...
```
Luego de resolver conflicto, y guardar cambio de stash
```bash
* commit 9ed5b0f0cbbb3287107761c90c622bed7250e649 (HEAD -> feature/cherry-pick)
| Author: MathiasVilca <email>
| Date:   Sun Sep 28 23:11:47 2025 -0500
| 
|     cherry pick
| 
* commit 8ab86cd468a8e161adb56b8912223147c7041468
| Author: MathiasVilca <email>
| Date:   Sun Sep 28 22:54:59 2025 -0500
| 
|     Agrega segundo ejemplo
| 
* commit 4c4694d6996eca1f9d7eef9a6d16fb6dcc95c0fc (master)
| Author: MathiasVilca <email>
| Date:   Sun Sep 28 22:54:59 2025 -0500
| 
|     Agrega ejemplo de cherry-pick
|   
*   commit 6e4582853635213670bbd9a0f64b33e4094d1d7e
|\  Merge: 83b42cf d0f873e
...
```
