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



