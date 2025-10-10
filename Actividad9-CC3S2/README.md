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
Asegura que el método `push(3)` haya funcionado al verificar que el elemento de la parte superior del stack sea igual a 3 (vía `peek()`).  
Se tuvo que arreglar error en `test_is_empty()` ya que siempre se requiere poner `self` como primer argumento en unittest, esto se puede ver en los ejemplos brindados en `Instrucciones.md` de la actividad.
### 2. `pruebas_pytest`
Para ejecutar `pytest --cov=pruebas_pytest` se debe hacer una carperta arriba (en `soluciones`) y especificando que se quiere ejecutar en esa carpeta (en este caso al estar las otras actividades), asi que se ejecuta:
```python
pytest --cov=pruebas_pytest pruebas_pytest/
```
Se guardaron reportes html en la misma carpeta de la actividad (diferenciando el reporte generado por el modulo con el nombre `htmlcov_modulo`, el cual se ejecuto en `soluciones/`).
## 3. Fixtures
En el archivo `test_account.py` se usa el fixture:
```python
@pytest.fixture(scope="module", autouse=True)
def setup_database():
    """Configura la base de datos antes y después de todas las pruebas"""
    # Se ejecuta antes de todas las pruebas
    db.create_all()
    yield
    # Se ejecuta después de todas las pruebas
    db.session.close()
```

El cual esta a nivel de módulo (lo que significa que se ejecuta una vez por archivo de pruebas), y `autouse=True` significa que todos los test pan a usar ese fixture (el cual normalmente se pide). Este fixture inicia la conexión con la base de datos antes de ejecutar todas las pruebas del módulo, y posterior a ejecución, cierra esta conexión.  
Mientras tanto, el método `setup_class(cls)` carga los datos del json a la base de datos, y `teardown_class(cls)` no hace nada (`pass` no hace nada, de la desconexión se encarga el fixture). Por último, `setup_method(cls)` limpia los datos antes de cada prueba y `teardown_method(cls)` cierra la sesion despues de cada prueba
