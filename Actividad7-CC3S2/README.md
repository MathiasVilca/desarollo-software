# Actividad 7
## Resumen del entorno:
- OS: Ubuntu 24.04.3 LTS
- Shell(Bash): 5.2.21(1)-release
- git: git version 2.43.0
## Ejercicios
### Pregunta: ¿Cuándo evitarías --ff en un equipo y por qué?
Evitaria usar --ff al trabajar en un equipo en el cual se trabaja en pararelo porque el registro de commits queda mucho mas claro, por ejemplo, si se trabaja en varias funcionalidades al mismo tiempo y se hace merge con fast-fowarding, el historial puede quedar desordenado al verse seguidos commits de funcionalidades diferentes en una misma rama, en lugar que estos esten en ramas separadas (resultado de usar `--no-ff`).
### Pregunta: ¿Qué ventajas de trazabilidad aporta?
Permite ver cada proceso de desarrollo de cada rama por separado, evitando desorden en la rama principal
### Pregunta: ¿Qué problemas surgen con exceso de merges?
El problema es que el grafico se puede hacer muy enreversado cuando hay un exceso de merges, y no necesariamente siempre es necesario ver los cambios de forma separada por ramas como, por ejemplo, en procesos secuenciales. Un ejemplo de ejecución:
```bash
* cf2e024 (alt1) c
| * 5909533 (HEAD -> main) 3
| *   53b8d5e Merge branch 'alt1': ¡!¡!¡!¡!¡!¡!¡!¡
| |\  
| |/  
|/|   
* | d332ebe a y b
| * cd1669b 2 y 1
|/  
* b95f263 Inicial
```
### Pregunta: ¿Cuándo conviene? ¿Qué se pierde respecto a merges estándar?
Conviene cuando se considera que hubieron muchos commits en una rama (muchos commits pequeños se aplanan en uno solo).respecto a los merges estandar, se pierde el parent original de los commits que se aplanan (visble en el DAG, al los commits originales no estar conectados al squash), solo quedando en el que se ejecuta el `git merge --squash`
### Ejercicio 4
#### ¿Qué pasos adicionales hiciste para resolverlo?
Tuve que resolver el conflicto, en este caso decidi hacer una especie de combinación de ambos al tener en cuante ambas contribuciones:
```html
<h1>Proyecto CC3S2 (main) (feature)</h1>
```
obviamente luego tuve que añadir este cambio
#### ¿Qué prácticas (convenciones, PRs pequeñas, tests) lo evitarían?
Entre algunas recomendaciones están: tener estándares en el formato del código para evitar conflictos en lineas, hacer commits con PRs pequeños y frecuentes (esto porque en general no suelen tener muchos conflictos, al ser pocos los cambios, en lugar de un gran commit el cual crea demasiados conflictos y cuyo PR es complicado de revisar), y el tener una buena comunicación para evitar cruces en las áreas en las que se trabaja.

### Ejercicio 5-7
NOTA: PARA LAS VISTAS 05-07, SE USO UN MISMO REPOSITORIO, SE PUEDE VER DAG DE ESTE EN `evidencias/capturas/DAG-evidencias05-07`
#### ¿Cómo se ve el DAG en cada caso?
- En la vista fast foward, se pierde la conexión de rama 2 con el merge, y por lo tanto se pierde el dato que se fusiono desde 1.txt
- En la vista solo merges, solo se aprecia el unico merge que se hizo, sin fast foward
- En la vista completa, se aprecian todos los detalles, incluidos la conexión de rama 1 desde el commit de `1.txt` con el merge y los commits de rama1 que se aplanaron con el squash
#### ¿Qué método prefieres para: trabajo individual, equipo grande, repos con auditoría estricta?
Personalmente, para trabajos individuales el método fast-fowarding deberia ser suficiente, ya que al trabajar una sola persona, esta sabe los cambios que hizo y la información que se pierde seria redundante, tambien para auditoría estricta para mantener linealidad. En cambio, para equipos grandes, el que se sepa que se hace en cada rama es fundamental para los miembros del equipo, para que esten al tanto de que hizo cada quien, por esto, creo que aqui lo optimo seria trabajar sin fast-fowarding.
### Ejercicio 8
#### ¿Cuándo usar git revert en vez de git reset?
Se usa `git revert` cuando se quiere mantener el historial de commits, porque este crea un commit nuevo deshaciendo commits anteriores, mientras tanto `git reset` directamente vuelve a ese commit, eliminando el historial de commits hasta ese commit
#### ¿Impacto en un repo compartido con historial público?
Por lo general, es mala idea usar `git reset` en un repositorio público, ya que al reescribir el historial de commits, puede confundir a otros desarrolladores
### E) Subtree (integrar subproyecto conservando historial)
Se uso el ejemplo del Rebase + FF para el subtree
### F) Sesgos de resolución y normalización (algoritmo ORT)
Use `git merge -X find-renames=90% feature-rename` porque hize otro archivo `archivo1.txt` el cual tenia practicamente el mismo contenido que el original `archivo.txt` , cambiando solo en el último caracter: El archivo `archivo.txt` en `main`
```bash
123456789 texto de ejemplo 1
```
Fue cambiado en `archivo1.txt` en `feature-rename`
```bash
123456789 texto de ejemplo 2
```
