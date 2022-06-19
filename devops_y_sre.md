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
    ![](/Images/cloud-storage.png)

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

## Linux en Servers y Lenguajes para Alta Concurrencia.

### Linux
- Open Source
- En terminos generales es un más seguro.
- Lenguajes de programación:
    - Java
    - Python
    - Go
- No necesitas reiniciarlo por largo tiempo.

## Usuarios en Entoros de Staging y Producción.

- Los log files no se usan para guardar los tokens ó credenciales.
- Usuarios - Contraseñas - Tokens
    - Sistema externo.
    - Redis y Mencach son sistemas más rapidos.
    - Tomar encuenta que el backend debe ser de forma segura
    para contraseñas de Bases de Datos.

## Orquestador y Serverless.

### Orquestador

- **Kubernetes** corre contenedores [Docker](https://www.docker.com) y _Docker_
necesita de [Kubernetes](https://kubernetes.io) para correr en producción.
- Sí se cae un contenedor, se puede armar otro rapidamente.

### Serverless

- Funciones en la nube.
- Escala automaticamente.
- Cuando el tráfico séa mayor las fuciones _serverless_
escalarán automaticamente y de pendiendo del tamaño del escalamiento
será el cobro.

## Motores de Bases de Datos u Cache.

### Motores.

> **NOTA:** Es más común realizar lecturas de una
BD que realizar escrituras. - replicas de lectura.

- SQL.
    - MySQL (relacionales) se escala con replicas
    ó verticalmente.

- NoSQL
    - MongoDB (Documentos) se pueden escalar de manera
    más fácil.
    - Un servidor para lecturas.
    - Un servidor para escrituras.

- Cache.
    - Redis
    - Memecached
    - CDNs
    - Autenticación y sesiones.

## Uso de CDN en Alta Concurrencia.

### CDN

Nos ayuda a replicar nuestro contenido por zonas geográficas, así
el acceso es más rapido.

    > Si accesas a _Youtube_ **Japón**, hay un servidor cerca para que
    el contenido sea más rapido de accesar.

### CDNs

1. Permite correr un _proxy_ delante de nuestra app.
2. Cachea (cache) archivos estaticos.
3. ssl
4. Pone lógica rn algunos proveedores.
5. Mejora la seguridad.
6. Ayuda a tener la app replicada en zonas geográficas.

### Proveedores

- [Cloudflare](https://www.cloudflare.com)
- [Fasty](https://www.fastly.com)

## Ataques DDoS

- [DDoS](https://www.cloudflare.com/learning/ddos/what-is-a-ddos-attack/) es un intento
malintencionado de interrupir el trafico normal de un servidor, servicio ó red determinada
con:
    - sobrecarga de infraestructura.
    - avalancha de tráfico de internet.

- Se usan sistemas informáticos vulnerables para originar el ataque de tráfico.

- Enterminos generales un ataque DDoS impide que llegues a tu destino.

- [WAF](https://www.cloudflare.com/learning/ddos/glossary/web-application-firewall-waf/) Nos ayuda a
filtrar [DDoS](https://en.wikipedia.org/wiki/Denial-of-service_attack)

## gRPC ó REST

### [gRPC](https://grpc.io)

- Recomendado para uso de microservicios.
- Integración de APIs internas.
- Ofrece mayor escalabilidad.
- Optimiza la respuesta por su baja latencia.
- Mensajes en formato binario.
- Protocolo [HTTP/2](https://en.wikipedia.org/wiki/HTTP/2)

### [REST](https://www.redhat.com/en/topics/api/what-is-a-rest-api)

- Integración con clientes y APIs publicas.
- Fácil de usar con restricciones sencillas de implementar.
- Usa archivos _JSON_
- La desventaja es que es más pesado.

## Consideraciones de Negocio para Alta Concurrencia.

### Crear un _monolito_

- Se puede utilizar cache (sesiones - autenticaciones) [CDN](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/)
contenedores - orquestadores.
- Separar en funciones.
- Usar funciones _serverless_ para tareas asincronas.
- Todo en contenedores [Docker](https://www.docker.com) y un orquestaador
[K8s](https://kubernetes.io)
- Metricas: _RAM_ _CPU_ _colas de mensaje_
