## Infraestructura y Alta Concurrencia.
---

> **Note:** En terminos generales, la adaptación de un _desarrollador_ (developer) a un equipo de _SRE_ sería menos complicada.
Un _sysadmin_ tardaría más tiempo en adaptarse porque tendría que adquirir conceptos nuevos en cuanto a desarrollo se refiere.

![DevOps - SRE](/Images/cultura.png)

---
![SRE](/Images/sre_img.png)

### SRE 
#### Habilidades/Skills

- Servidores Linux
- Manejo de Paquetes
- Servicios de Base de Datos
- Servicios Web
    - Apache
    - Nginx
- Bash Scripting
- Python, Go (GoLang)

## Alta Concurrencia.

Se puede pensar en _Alta Concurrencia_ cuando un
sistema no puede soportar una alta cantidad de trafico ó cuando
el numero de usuarios no puede ser soportado por tu _monolito_.

### Microservicios.

- Escalamiento independiente.
- Separar los procesos.
    - Autenticación.
    - el/la procesamiento/edición de un video.
- La mayoria de las veces hay que pensar si es bueno separar
las tareas.

### Modelos y Patrones.

![](/Images/cloud_service.png)
> _pixabay:WilliamCreativity_

- Cloud Services.
    - Storage Bucket
    - Espacio en la nube
    - ObjectStore


## Escalamiento.
---

- Vertical.

    ![](/Images/vertical.png)

    > Hacemos crecer un solo servidor.

    > Mas memoria RAM, CPU, HDD  
    ![](/Images/ram.png)
    ![](/Images/cpu.png)
    ![](/Images/hdd.png)

- Horizontal.

    ![](/Images/horizontal.png)
    ![](/Images/horizontal.png)
    ![](/Images/horizontal.png)

    > Agregamos más servidores.

Otra manera de describir un **Escalamiento Vertical**
es cuando aumentas la potencia del servidor.
**Escalamiento Horizontal** es cuando se aumenta el numero de
servidores.

> Ejemplos:
- MySQL -> Escalamiento Vertical - Bases de Daatos relacionales.
- MongoDB -> Escalamiento Horizontal - Bases de Datos no relacionales.

Si tu app parte de sesiones concurrentes estariamos ante
un escenario de *escalamiento horizontal*.

Si se trata de la edición de un video estamos ante un escenario
de *escalamiento vertical*. 

## Stateless y Statefull en Alta Concurrencia.

**Stateless**
- El estado se encuentra fuera de la app - Un servicio 
de procesamiento de datos.
- No necesitas el historial de sesiones previas (Base de Datos)
- Una de sus ventajas es el escalamiento.
    
    > **Nota:**
    Un servicio de almacenamiento s3, bucket. Muchos servidores conectados
    a ese servicio de almacenamiento.

**Statefull**
- El estado se encuentra dentro de la app.
- Si se necesita el historial de la Base de Datos. 
- _WordPress Blog_ es un ejemplo de _statefull_ la 
desventaja sería cuando queremos cambiar de servidor
donde esta hospedado mi blog porque todos los archivos están 
el servidor anterior.

## Resilencia y Pruebas Efectivas.

Para mejorar la resilencia de los servidores en alta
concurrencia se usará CDN - _Content Distribution Network_ - que
nos permite cachear - _cache_ - ó hospedar contenido estatico.
> Proxy - Server
Redistribuir contenido estatico.

Para las pruebas efectivas nos ayudaremos de _Stress Testing_
para medir la carga de trafico de la app y utilizaremos 
orquestadores como **Kubernetes**.
También podemos utilizar _Load Testing_ que basicamente es DDoS
con benas intenciones, basicamente anticipa eventos no deseados.

## Que metricas usar para escalar?

El orquestador puede realizar las metricas:
- Memoria RAM
- cpu - Algún proceso utliza más cpu de lo normal.

> Pregunta clave:
Que tipo de operación realizará más tu app.

**Ejemplo:**
Los indices deben ser bién usados para ganar rendimiento
en la lectura de las tablas pero agregas complejidad e la lrctura.
Los indices son fundamentales en la estructura de datos para
una busqueda rápida a la hora de actualizarla por cada registro agregado
costara más trabajo modificar dicha estructura.

> [SQL vs. NoSQL Databases](https://www.mongodb.com/nosql-explained/nosql-vs-sql)

## Tráfico por Paises.

### CDN
Distribuye el contenido estático por regiones.
- Geographical proxy server.

Los usuarios se conectan al CDN más cercano y la latencia
es menor.
Garantiza la disponibilidad de tu contenido en más de un
servidor de contenido.
Soporta alta concurrrencia entre la carga de requests para
no saturar un solo servidor.