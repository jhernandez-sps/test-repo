# Bitácora de Motor de Pagos
[![GoDoc](https://godoc.org/github.com/openshift/origin?status.png)](https://anypoint.mulesoft.com/exchange/0e23ebaf-97be-445d-8b12-86ae12f2ed1c/bitacoramotorpagos/)
Este repositorio contiene el código y pruebas unitarias del API de Bitácora de Motor de Pagos para el `Motor de reglas` como parte de la reingeniería de los procesos de recepción de solicitudes de pagos y la validación de pagos.

## Especificación de la API
[Aquí](https://anypoint.mulesoft.com/exchange/0e23ebaf-97be-445d-8b12-86ae12f2ed1c/bitacoramotorpagos/) encontraremos los recursos de esta API así como sus payloads de entrada y salida

# Diagramas de sequencia 

# Pagos 

**Los pagos recibidos y de los que se requiere registrar eventos clave durante el procesamiento son:**

- SPEI (Pagos Nacionales)

**Estos pagos tendrán como origen los siguientes canales:**

- HUB. Sistema de Pagos Masivos HOST TO HOST.
- MOBILE. Servicios en línea a través de celular.
- API. Externalización a clientes Monex de todos los procesos de pago.

# Detalles del API

**Tecnologias:**
- Mule 4. Runtime 4.3.0 EE

**Versión:** 1.0

**Dependencias:**
- Core Bancario 
- Elastic Search
- Message Broker

**Desarrollador:** Team SPS [[jhernandezr_ext@monex.com.mx](mailto:jhernandezr_ext@monex.com.mx)]

# Consumo del API

Endpoints:
- Mocking Service: https://anypoint.mulesoft.com/mocking/api/v1/sources/exchange/assets/0e23ebaf-97be-445d-8b12-86ae12f2ed1c/bitacoramotorpagos/0.0.100/

- Dev-On-Premise: 
http://172.28.230.25:8081/api/gestionPagos/monitoreo/v1/eventos

**NOTA:** cada endpoint representa un ambiente distinto:
- Mocking Service: especificación de la API, como su nombre lo indica, solo es un mock.
- Desarrollo On-Premise.

# Ejecución de pruebas unitarias

Como parte de asegurar un desarrollo de API's bajo las mejores practicas se hacen pruebas unitarias para evaluar el correcto funcionamiento del desarrollo.

A continuación se muestra el estado actual de la ejecución de las pruebas unitarias aplicadas a los recursos del API Mesa de control:

| Id del Caso | Descripción | Resultado esperado |
|---|---|---|
|C1.1. Registrar información de pago a evaluar| Registrar información recibida del pago de forma satisfactorio en el repositorio alterno | 200. Registro satisfactorio | 
|C1.2. Petición errónea en registro información pago| Error por datos requeridos no especificados en el registro de un pago recibido para evaluarse en el motor de pagos | 400. Petición errónea | 
|C1.3. Error comunicación en message broker en registro información pago| Error en comunicación con message broker al tratar de encolar evento de registro información del pago | 500. Error de comunicación | 
|C2.1. Registro reglas a aplicar a pago a evaluar| Registrar las reglas a aplicar a un pago evaluado en el motor de pagos | 200. Registro satisfactorio | 
|C2.2. Petición errónea en registro de reglas aplicar a pago| Error por valor en clave medio no válido en el registro de las reglas aplicar a un pago | 400. Petición errónea | 
|C2.3. Error comunicación en message broker por registro de reglas aplicar a pago| Error en comunicación con message broker al tratar de encolar evento de registro de reglas a aplicar a un pago | 500. Error de comunicación | 
|C3.1. Registrar resultado de regla aplicada a pago| Registrar el resultado de una regla aplicada a un pago evaluado en el motor de pagos | 200. Registro satisfactorio | 
|C3.2. Petición errónea en registro de resultado regla aplicada pago| Error por dato requerido (bandera error) no especificados en el registro del resultado de una regla aplicada a un pago evaluado | 400. Petición errónea | 
|C3.3. Error comunicación en message broker por registro resultado regla aplicada pago| Error en comunicación con message broker al tratar de encolar evento de registro del resultado de una regla aplicada a un pago | 500. Error de comunicación | 
|C4.1. Registrar errores en proceso evaluación de pago| Registrar error ocurrido durante el proceso de evaluación de un pago | 200. Registro satisfactorio | 
|C4.2. Petición errónea de registro de excepción en proceso evaluación de pago| Error por dato requerido (etapa proceso) no especificado en el registro de un error de un pago evaluado | 400. Petición errónea | 
|C4.3. Error de comunicación en message broker por registro de excepción de pago| Error en comunicación con message broker al tratar de encolar evento de registro de error en el proceso de valuación de un pago | 500. Error de comunicación | 
|C5.1. Registrar alerta en proceso evaluación de pago| Registrar alerta de evento relevante ocurrido durante el proceso de evaluación de un pago | 200. Registro satisfactorio | 
|C5.2. Petición errónea en registro de alerta en proceso evaluación de pago| Error por dato requerido (fecha registro evento) no especificado en el registro de una alerta de un pago evaluado | 400. Petición errónea | 
|C5.3. Error comunicación en message broker por registro de alerta para pago| Error en comunicación con message broker al tratar de encolar evento de registro de alerta en el proceso de valuación de un pago | 500. Error de comunicación | 
|C6.1. Consultar información pago por id orden pago| Consultar el último registro de un pago por id orden pago. Restringido a obtener información del pago al día de la consulta | 200. Consulta satisfactoria | 
|C6.2. Consultar información pago por id orden pago y transacción| Consultar el último registro de un pago por id orden pago y transacción | 200. Consulta satisfactoria | 
|C6.3. Pago no encontrado en consulta información pago| Consultar el último registro de un pago por id orden pago y transacción | 200. Consulta sin resultados | 
|C6.4. Error comunicación elastic en consulta información pago por id orden pago| Error en comunicación con Elastic en consulta del último registro de un pago por id orden pago | 500. Error de comunicación | 
|C7.1. Consultar pagos por estado evaluación| Consultar pagos por estado evaluación. Restringido a obtener información del pago al día de la consulta | 200. Consulta satisfactoria | 
|C7.2. Pagos no encontrados con consulta por estado evaluación| Pago no encontrado en consulta por estado evaluación | 200. Consulta sin resultados | 
|C7.3 Error de comunicación en consulta pagos por estado evaluación| Error de comunicación con Elastic en consulta de pagos por estado evaluación | 500. Error de comunicación | 
|C8.1. Consultar bloques prioridad evaluadas de pago| Consultar el estado de los bloques de reglas por prioridad de un pago en evaluación | 200. Consulta satisfactoria | 
|C8.2. Pago no encontrado en cosulta bloques prioridad evaluadas| Pago no encontrado en consulta del estado de los bloques de las reglas por prioridad en evaluación | 200. Consulta sin resultados | 
|C8.3. Error de comunicacion en consulta bloques prioridad evaluadas de pago| Error de comunicación con Elastic en consulta del estado de los bloques de reglas por prioridad | 500. Error de comunicación | 
|C9.1. Consultar resultado reglas pago evaluado| Consultar el resultado de las reglas aplicadas a un pago evaluado por id orden pago y transacción | 200. Consulta satisfactoria | 
|C9.2. Error de comunicación en consulta resultado reglas pago evaluado| Error de comunicación en consulta del resultado de las reglas aplicadas a un pago evaluado por id orden pago y transacción | 500. Error de comunicación | 
|C10.1. Actualizar estado evaluación de pago| Actualizar el estado de evaluación de un pago de forma satisfactoria | 200.Actualización satisfactoria | 
|C10.2. Actualizar el resultado de evaluación de pago| Actualizar el resultado de evaluación de un pago | 200.Actualización satisfactoria | 
|C10.3. Actualizar reintento de evaluación de pago| Actualizar el reintento de evaluación de un pago de forma satisfactoria | 200.Actualización satisfactoria | 
|C10.4. Actualizar estado final de un pago evaluado| Actualizar de forma satisfactoria el estdo final de una pago evaluado | 200.Actualización satisfactoria | 
|C10.5. Error de comunicación al actualizar estado de pago| Error en comunicación con Elastic en actualización del estado de un pago | 500. Error de comunicación | 
|C10.6. Error en actualización del estado de pago| Error por datos en la actualización del estado de un pago | 400. Petición errónea | 
|C11.1. Actualizar estado de regla aplicada a pago| Actualizar de forma exitosa el estado de aplicación de regla a un pago evaluado | 200.Actualización satisfactoria | 
|C11.2. Error al actualizar estado de regla aplicada a pago| Error al actualizar el estado de aplicación de regla a un pago evaluado | 400. Petición errónea | 
|C11.3. Error de comunicación al actualizar estado de regla aplicada a pago| Error en comunicación con Elastic en actualización del estado de una regla aplicado a un pago evaluado | 500. Error de comunicación | 
|C12.1. Actualizar estado evaluación bloque prioridad reglas| Actualizar exitosamente las reglas del bloque de prioridad evaluado para un pago | 200. Actualización satisfactoria | 
|C12.2. Error en actualización estado evaluación bloque prioridad reglas| Errror al actualizar estado del bloque de prioridad de las reglas aplicadas a un pago | 500. Error interno al actualizar documento no encontrado | 
|C12.3. Error comunicación en actualización estado evaluación bloque prioridad reglas| Error en comunicación con Elastic en actualización del estado de bloque de las reglas aplicadas a un pago | 500. Error de comunicación | 
|C13.1. Consultar detenciones autorizadas de pago| Consultar exitosamente las detenciones autorizadas de un pago evaluado | 200. Consulta satisfactoria | 
|C13.2. Consulta sin detenciones autorizadas de pago| Consulta sin detenciones autorizadas para un pago | 200. Consulta sin detenciones autorizadas | 
|C13.3. Consultar detenciones autorizadas de pago no existente| Consultar detenciones autorizadas de una orden de pago no existente | 200. Consulta sin resultados | 
|C13.4. Error de comunicación en consulta de detenciones autorizadas de pago| Error de comunicación en consulta del resultado de las reglas aplicadas a un pago evaluado por id orden pago y transacción | 500. Error de comunicación | 
|C14.1. Registrar detenciones autorizadas de pago| Registrar las detenciones autorizadas encontradas en el core Monex antes de que el pago sea reprocesado en el motor de pagos | 200. Registro satisfactorio | 
|C14.2. Petición errónea en registro de detenciones autorizadas de pago| Recibir y registrar las detenciones autorizadas encontradas en el core Monex antes de que el pago sea reprocesado en el motor de pagos | 400. Petición errónea | 
|C14.3. Error de comunicación en message broker por registro de detenciones autorizadas de pago| Error en comunicación con message broker al tratar de encolar evento de registro de detenciones autorizadas para un pago a reprocesar | 500. Error de comunicación | 
|C15.1. Consultar reglas aplicar pago reevaluado| Consulta exitosa de las reglas a aplicar para un pago que requiere evaluarse en un reproceso | 200. Consulta satisfactoria | 
|C15.2. Consultar reglas aplicar pago reevaluado por bloque prioridad| Consulta exitosa de las reglas de un bloque de prioridad a aplicar para un pago que requiere evaluarse en un reproceso | 200. Consulta satisfactoria | 
|C15.3. Error de comunicación en consultar reglas aplicar pago reevaluado| rror de comunicación en consulta de las reglas a aplicar para un pago reprocesado | 500. Error de comunicación | 
|C16.1. Consultar pagos procesados| Consultar exitosamente los pagos procesados en motor de reglas en MuleSoft y Core Monex de acuerdo con el rango de fechas especificado | 200. Consulta satisfactoria | 
|C16.2. Pagos procesados no encontrados en consulta| No se encontraron pagos procesados de acuerdo con el rango de fechas especificado | 200. Consulta sin resultados | 
|C16.3. Error de comunicación en consulta pagos procesados| Error de comunicación hacia la base de datos Monex o Elastic en consulta de pagos procesados | 500. Error de comunicación | 
|C17.1. Consultar evaluaciones pago| Consultar exitosamente las evaluaciones que ha tenido una orden de pago | 200. Consulta satisfactoria | 
|C17.2. Consultar evaluaciones pago no existente| Consultar evaluaciones que ha tenido una orden de pago no existente | 200. Consulta sin resultados | 
|C17.3. Error de comunicación en consulta de evaluaciones de pago| Error en comunicación con Elastic en consulta de evaluaciones de un pago | 500. Error de comunicación | 
|C18.1. Consultar resultado regla pago| Consultar exitosamente el resultado de una regla aplicada a un pago | 200. Consulta satisfactoria | 
|C18.2. Error en consulta del resultado de regla pago| Consultar exitosamente el resultado de una regla aplicada a un pago | 400. Petición errónea | 
|C18.3. Error de comunicación en consulta del resultado de regla pago| Error en comunicación con Elastic en consulta del resultado de una regla aplicada a un pago | 500. Error de comunicación | 
|C19.1. Eliminar detenciones autorizadas| Eliminar registro de detenciones autorizadas para un pago evaluado | 200. Eliminación satisfactoria | 
|C19.2. Error en eliminación de detenciones autorizadas de pago no existente| Error al eliminar detenciones autorizadas no encontradas para un pago evaluado | 500. Error interno al eliminar documento no encontrado | 
|C19.3. Error de comunicación en eliminación de detenciones autorizadas de pago| Error en comunicación con Elastic en eliminación de detenciones autorizadas de una pago evaluado | 500. Error de comunicación | 

**NOTA:** Para poder ejecutar las reglas es necesario contar con una VPN para poder llegar al mule on-premise

![enter image description here](https://www.baeldung.com/wp-content/uploads/2019/02/postman7.png)

En color **rojo** las pruebas con excepciones que no satisfacen los requisitos para decir que la prueba fue exitosa, y en color **verde** las pruebas que se ejecutaron satisfactoriamente.

**NOTA:** Los casos de comunicación requieren que la aplicación no pueda comunicarse con el Message broker o con Elastic.

## Pasos para replicar la ejecución 

# Pruebas MUnit

A nivel de `codigo` también se ejecutaron pruebas unitarias, con la finalidad de hacer una revisión de todo el código escrito en la aplicación de Mulesoft y como parte de la estrategia de integración continua `(CI-CD)`

> Para mas información sobre MUnit [clic aqui](https://docs.mulesoft.com/munit/2.3/munit-test-concept)

A continuación una imagen del coverage que cumple actualmente el `API Bitácora Motor Pagos`:

![enter image description here](https://docs.mulesoft.com/munit/2.3/_images/munit-coverage-report-in-anypoint-studio.png)

**NOTA:** El coverage establecido como mínimo estándar para evaluar la implementación del API es del 75%.

## Pasos para replicar la ejecución 
- Dentro de Anypoint studio en el apartado de Package Explorer nos dirigiremos a `api-bitacora-motor-pagos/src/test/munit`y veremos los archivos de las MUnit, por ejemplo `interfaz-test-suite.xml` daremos clic derecho sobre este archivo y seleccionaremos Munit > Run Tests

![enter image description here](https://blogs.infomentum.com/hubfs/Blogs/MuleSoft/MUnit%20Test%20Recorder%201.png)

- Una vez que el proceso termino, de lado inferior izquierdo veremos 2 pestañas, una nos muestra los errores que se produjeron y la otra nos dice las pruebas hechas y nos da la posibilidad de generar un reporte con el porcentaje de código cubierto.

> Importar una aplicación a anypoint  studio [clic aqui](https://docs.mulesoft.com/studio/7.7/import-export-packages)

# Despliegue del API

Cómo desarrollador el despliegue puede ser realizado en ambiente de Mulesoft On-Premise de forma manual o usando la estrategia de CI/CD. La recomentación es utilizar la segunda opción una vez se han realizado los ajustes correspondientes mencionados en <Liga Gitea>. 

**NOTA:** Para siguientes ambientes a desarrollo forzosamente se deberá hacer uso de la estrategia de CI/CD.

## Consideraciones

- Autodiscovery [clic aqui](https://docs.mulesoft.com/api-manager/2.x/configure-autodiscovery-4-task)

- Client Secret [clic aqui](https://docs.mulesoft.com/anypoint-security/index-secrets-manager)
**nota:** dependerá del administrador de la plataforma por ambiente

- El controlador Oracle JDBC no siempre reconoce correctamente la misma zona horaria utilizada por Java. La zona horaria debe establecerse explícitamente de manera compatible con el controlador de Oracle., el valor que se deberá dar es el siguiente `user.timezone=Etc/UTC`

- Cada API contiene archivos de propiedades para cada ambiente, estos archivos contienen host, puertos, etc. estos archivos los encontramos en la siguiente ruta: `api-bitacora-motor-pagos/src/main/resources` con el nombre de `application-config.yaml`, la asignación de las credenciales por ambiente serán gestionadas por medio de un repositorio de configuración que el administrador Monex encriptará y proveer establecera al realizar el despliegue al ambiente correspondiente, para mayor información ver <Liga Gitea>.

- La gestión de la información de bitáora será sobre Elastic o distribución de éste, en el caso del proyecto (Distro for Elastic), por lo que es requerido contar con comunicación desde el ambiente en el que se encuentre desplegada la aplicación de la bitácora, tener creados los ínices que la aplicación requiere para gestionar la información y las credenciales de aplicación con permisos necesarios para la manipulación de los índices. La estructura de los índices se encuentra en la siguiente carpeta del repositorio de código: <Liga Gitea>

- Se requiere tener comunicación hacia el Message Broker desde el ambiente de mulesoft en el que se encuentra desplegada la aplicación.

- Se requieren credenciales para consumir las siguientes APIs: API de catálogos del motor de pagos.

- El API bitácora del motor de reglas, se encuentra asegurada con una politíca de Client ID Enforcement por lo que el consumidor de esta deberá solicitar las credenciales y autorización correspondiente, y proporcionar estos datos en forma de cabeceras en la petición al API (client_id/client_secret).

## Pasos para despliegue OnPremise

Referencia a la documentación (generar ficha técnica)

## Pasos para despliegue CloudHub

De acuerdo con los cambios en la forma de despliegue definidos en el alcance del proyecto, la opción en CloudHub quedo fuera, sin embargo, se comenta la forma de forma informativa.

Referencia a la documentación (generar ficha técnica)