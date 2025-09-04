Actividad 1 - Mathias Joaquin Vilca Perez
01/09/25 - ???
Hecho en Ubuntu 24.04.3 LTS

#### 4.1 DevOps vs. cascada tradicional (investigación + comparación)

* Agrega una **imagen comparativa** en `imagenes/devops-vs-cascada.png`. Puede ser un diagrama propio sencillo.

* Explica por qué DevOps acelera y reduce riesgo en software para la nube frente a cascada (feedback continuo, pequeños lotes, automatización).

DevOps acelera el desarrollo al contar con actualizaciones frecuentes (gracias a la integración continua o CI) las cuales pasan siempre por pruebas exhaustivas tanto unitarias como en entornos de prueba, estas dan retroalimentación constante a los desarrolladores debido a su carácter automatizado y permiten atrapar errores rápidamente, asegurando actualizaciones pequeñas pero frecuentes y seguras.

* **Pregunta retadora:** señala un **contexto real** donde un enfoque cercano a cascada sigue siendo razonable (por ejemplo, sistemas con certificaciones regulatorias estrictas o fuerte acoplamiento hardware). Expón **dos criterios verificables** y **los trade-offs** (velocidad vs. conformidad/seguridad).

Un contexto donde podria ser aplicable es en la industria aeroespacial, la cual tiene regulaciones estrictas, cuya duración podria llevar mucho tiempo, el cual impide la integración continua de cambios. Entre los criterios estarían el tiempo promedio de validación de cumplimiento de regulaciones y nivel de rigurosidad de estas regulaciones. El trade-off mas evidente es el hecho que se esta cambiando la velocidad con las que se pueden entregar/desarrollar cambios por seguridad en el cumplimiento de las regulaciones, lo cual a la larga incluso puede salvar más tiempo en caso se tenga un tiempo de validación extenso.

#### 4.2 Ciclo tradicional de dos pasos y silos (limitaciones y anti-patrones)

* Inserta una imagen de **silos organizacionales** en `imagenes/silos-equipos.png` (o un dibujo propio).
* Identifica **dos limitaciones** del ciclo "construcción -> operación" sin integración continua (por ejemplo, grandes lotes, colas de defectos).

Una evidente limitación de este ciclo es la "acumulación de errores", al los cambios ser más espaciados entre sí, los errores pequeños al inicio del desarrollo de una versión pueden crecer para cuando llegue a la etapa de pruebas, lo cual puede requerir grandes cambios en el código para su solución.Esto también lleva a largos tiempos de espera entre actualizaciones, lo cual puede llegar a ser insatisfactorio para los clientes del producto.

* **Pregunta retadora:** define **dos anti-patrones** ("throw over the wall", seguridad como auditoría tardía) y explica **cómo** agravan incidentes (mayor MTTR, retrabajos, degradaciones repetitivas).

Existe el antipatrón "Parálisis por análisis" en el cual el desarollo se atora en la fase del análisis, generalmente por tener altas expectativas.También está el antipatrón "thrown over the wall", el cual consiste en que el proyecto va pasando entre equipos del desarrollo con poca o nula comunicación. Esto puede llevar a la asimetría de información entre equipos (La información que ambos tienen del mismo proyecto es diferente), lo que puede generar objetivos contradictorios entre equipos y falta de colaboración. Ambos afectan la frecuencia de despliegue y el flujo acumulado (el como fluye el proceso de desarrollo).

#### 4.3 Principios y beneficios de DevOps (CI/CD, automatización, colaboración; Agile como precursor)

* Describe CI y CD destacando **tamaño de cambios**, **pruebas automatizadas cercanas al código** y **colaboración**.

Integración Continua: Es la constante introducción de cambios pequeños en el código (commits constantes a un mismo repositorio), lo cual permite la detección temprana de errores al pasar por pruebas automatizadas en commit, este código pasa por revisiones grupales, en las cuales se comparte conocimiento entre equipos.

Entrega Continua: Es una expansión de la Integración Continua, en la cual se da un paso más al prepararse estos cambios de forma automática para la fase de producción, con el fin de tener versiones seguras listas para el despliegue lo antes posible.

* Explica cómo **una práctica Agile** (reuniones diarias, retrospectivas) alimenta decisiones del pipeline (qué se promueve, qué se bloquea).

La práctica de las revisiones de código colaborativas promueve el compartir conocimiento entre los equipos de desarrollo y las retrospectivas ayudan a identificar que practicas o herramientas llegan a ser útiles o no, mejorando el flujo del pipeline.

* Propón **un indicador observable** (no financiero) para medir mejora de colaboración Dev-Ops (por ejemplo, tiempo desde PR listo hasta despliegue en entorno de pruebas; proporción de rollbacks sin downtime).

Un ejemplo sería el número de errores que escapan las revisiones de código por sesión o por ciclo, medible al fin de cada ciclo vía registros luego de las pruebas.

#### 4.4 Evolución a DevSecOps (seguridad desde el inicio: SAST/DAST; cambio cultural)

* Diferencia **SAST** (estático, temprano) y **DAST** (dinámico, en ejecución), y ubícalos en el pipeline.

Mientras SAST (Static Application Security Testing) hace las revisiones del código sin ejecutarlo, con un enfoque de caja transparente o "white box" (se "ve" el interior del sistema), DAST (Dynamic Application Security Testing) se realizan pruebas desde un punto de vista externo o "black box" (no se "ve" el interior del sistema), con el fin de identificar vulnerabilidades durante la ejecución. Lo mejor es ubicar el SAST justo despues del commit del código, mientras DAST esta mejor posicionado en fases de staging/producción.

* Define un **gate mínimo de seguridad** con **dos umbrales cuantitativos** (por ejemplo, "cualquier hallazgo crítico en componentes expuestos **bloquea** la promoción"; "cobertura mínima de pruebas de seguridad del **X%**").

Si no se cubren un minimo del 85% de las pruebas de seguridad o la totalidad de un conjunto clave de estas (como pueden ser aquellas que verifiquen cumplimiento de estándares o la seguridad de información sensible), se bloquea la promocióń.

* Incluye una **política de excepción** con **caducidad**, responsable y plan de corrección.




* **Pregunta retadora:** ¿cómo evitar el "teatro de seguridad" (cumplir checklist sin reducir riesgo)? Propón **dos señales de eficacia** (disminución de hallazgos repetidos; reducción en tiempo de remediación) y **cómo** medirlas.

**Validación:** que los umbrales sean **concretos** y la excepción tenga fecha límite y dueño.

#### 4.5 CI/CD y estrategias de despliegue (sandbox, canary, azul/verde)

* Inserta una imagen del pipeline o canary en `imagenes/pipeline_canary.png`.
* Elige **una estrategia** para un microservicio crítico (por ejemplo, autenticación) y justifica.

Siguiendo el ejemplo, para el microservicio de autenticación, yo eligira personalmente la estrategia sandbox, pricipalmente porque la autenticación es un sistema bastante sensible, que si una falla critica se llegase a encontrar en una version ya deslpegada, podria llevar a brechas de información, algo que un simple rollback no podría arreglar.

* Crea una **tabla breve** de **riesgos vs. mitigaciones** (al menos tres filas), por ejemplo:

  * Regresión funcional -> validación de contrato antes de promover.
  * Costo operativo del doble despliegue -> límites de tiempo de convivencia.
  * Manejo de sesiones -> "draining" y compatibilidad de esquemas.
  
| Riesgo                              | Mitigación                                                                                                      |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------|
| Detección por malware               | Simular un entorno realista, cambiar configuraciones de tiempo, desplegar la sandbox en un entorno aparte       |
| Uso intensivo de recursos           | Crear la sandbox con lo estrictamente necesario para las pruebas de ejecución                                   |
| Impresición de comportamiento       | Usar datos reales y basado en estos ajustar el entorno, puede usarse herramientas avanzadas para esto           |  

* Define un **KPI primario** (p. ej., error 5xx, latencia p95) y un **umbral numérico** con **ventana de observación** para **promoción/abortado**.

Ejemplo: Si luego de observar por 10 minutos, la latencia p95 < 350ms, entonces pasa a producción, sino, se hace un rollback.

* **Pregunta retadora:** si el KPI técnico se mantiene, pero cae una métrica de producto (conversión), explica por qué **ambos tipos de métricas** deben coexistir en el gate.



#### 4.6 Fundamentos prácticos sin comandos (evidencia mínima)

Realiza comprobaciones **con herramientas estándar**, pero **no** pegues los comandos. En el README escribe los **hallazgos** y la **interpretación**. Adjunta tus capturas en `imagenes/` y **marca** los campos relevantes (códigos, cabeceras, TTL, CN/SAN, fechas, puertos).

1. **HTTP - contrato observable**

   * Reporta: **método**, **código de estado** y **dos cabeceras** clave (por ejemplo, una de control de caché y otra de traza/diagnóstico).
   Método: GET
   Codigo de estado: 200 (Solicitud procesada con éxito)
   Control de caché: s-maxage=86400, must-revalidate, max-age=3600
   HSTS (HTTP strict-transport-security): max-age=106384710; includeSubDomains; preload
   * Explica por qué esas cabeceras influyen en **rendimiento**, **caché** u **observabilidad**.
   
   cache-control determina el comportamiento del cache del navegador, como puede ser el si va a guardar los recursos en el cache, o va a pedir estos al servidor
   HSTS: Comunica al navegador que el sitio solo debe ser accesible con HTTPS en lugar de HTTP, puede tener impacto en rendimiento al tener que hacerse la conexion en HTTPS
   
   * **Captura:** `imagenes/http-evidencia.png`, con los campos resaltados.

2. **DNS - nombres y TTL**

   * Reporta: **tipo de registro** (A o CNAME) y **TTL** de un dominio.
   * Explica cómo el **TTL** afecta **rollbacks** y cambios de IP (propagación, ventanas de inconsistencia).
   * **Captura:** `imagenes/dns-ttl.png`, con el TTL destacado.

3. **TLS - seguridad en tránsito**

   * Reporta: **CN/SAN**, **vigencia (desde/hasta)** y **emisora** del certificado de un sitio seguro.
   * Explica qué sucede si **no valida** la cadena (errores de confianza, riesgo de MITM, impacto en UX).
   * **Captura:** `imagenes/tls-cert.png`, con CN/SAN, emisora y fechas.

4. **Puertos - estado de runtime**

   * Enumera **dos puertos en escucha** en tu máquina o entorno y **qué servicios** sugieren.
   * Explica cómo esta evidencia ayuda a detectar **despliegues incompletos** (puerto no expuesto) o **conflictos** (puerto ocupado).
   * **Captura:** `imagenes/puertos.png`, con los puertos resaltados.

5. **12-Factor - port binding, configuración, logs**

   * Describe **cómo** parametrizarías el puerto sin tocar código (config externa).
   * Indica **dónde** verías los logs en ejecución (flujo estándar) y **por qué** no deberías escribirlos en archivos locales rotados a mano.
   * Señala un **anti-patrón** (p. ej., credenciales en el código) y su impacto en reproducibilidad.

6. **Checklist de diagnóstico (incidente simulado)**

   * **Escenario:** usuarios reportan intermitencia. Formula un checklist de **seis pasos ordenados** que permita discriminar:
     a) contrato HTTP roto, b) resolución DNS inconsistente, c) certificado TLS caducado/incorrecto, d) puerto mal configurado/no expuesto.
   * Para cada paso, indica: **objetivo**, **evidencia esperada**, **interpretación** y **acción siguiente**.
   * Evita generalidades; sé **operacional** (si X ocurre, entonces Y decisión).


#### 4.7 Desafíos de DevOps y mitigaciones

* Inserta un diagrama propio o ilustración en `imagenes/desafios_devops.png` con **tres desafíos** anotados (culturales, técnicos, de gobernanza).
* Enumera **tres riesgos** con su **mitigación concreta** (rollback, despliegues graduales, revisión cruzada, límites de "blast radius").
* Diseña un **experimento controlado** para validar que el despliegue gradual reduce riesgo frente a uno "big-bang": define **métrica primaria**, **grupo control**, **criterio de éxito** y **plan de reversión**.



#### 4.8 Arquitectura mínima para DevSecOps (HTTP/DNS/TLS + 12-Factor)

* Dibuja un **diagrama propio** en `imagenes/arquitectura-minima.png` con el flujo: **Cliente -> DNS -> Servicio (HTTP) -> TLS**, e indica **dónde** aplicar controles (políticas de caché, validación de certificados, contratos de API, límites de tasa).
* Explica cómo cada capa contribuye a **despliegues seguros y reproducibles**.
* Relaciona **dos principios 12-Factor** (config por entorno; logs a stdout) con **evidencias operativas** que un docente podría revisar (por ejemplo, diffs mínimos entre entornos, trazabilidad de logs).



