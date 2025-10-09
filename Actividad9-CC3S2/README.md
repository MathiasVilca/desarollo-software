# Actividad 9
## Resumen del entorno:
- OS: Ubuntu 24.04.3 LTS
- Shell(Bash): 5.2.21(1)-release
- make: GNU Make 4.3
- tar: (GNU tar) 1.35
- python3: Python 3.12.3
## Como ejecutar
En esta carpeta, se inicia ejecutando `make venv` para crear

### 1. Uso de aserciones 
Las aserciones en los test se usan para aseverar que ciertas condiciones se cumplan en los tests. En `test_stack.py` se usaron para verificar que los elementos de una clase Stack (definida en `stack.py`) se actualizaran correctamente (en el caso de los test de los métodos de clase `pop()`, `push()` y `peek()`), o verificar que se retornaba el booleano esperado (para test de `is_empty()`). Ejemplo:
```python
self.stack.push(3)
self.assertEqual(self.stack.peek(), 3)
```
Asegura que el método `push(3)` haya funcionado al verificar que el elemento de la parte superior del stack sea igual a 3 (vía `peek()`)
