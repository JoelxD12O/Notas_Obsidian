### 1. **Preguntas teóricas de conceptos**

- **Pregunta 1**: ¿Cuál es la diferencia entre un usuario normal y el usuario "root" en Linux?  
    **Respuesta esperada**: El usuario "root" es el administrador del sistema con privilegios completos para modificar todos los archivos, ejecutar cualquier comando, y gestionar otros usuarios. Los usuarios normales tienen permisos limitados, dependiendo de su rol y configuración.
    
- **Pregunta 2**: ¿Qué es un "grupo" en Linux y cómo se relaciona con los usuarios?  
    **Respuesta esperada**: Un grupo en Linux es un conjunto de usuarios que tienen permisos comunes sobre ciertos recursos (como archivos). Los usuarios pueden pertenecer a uno o más grupos, lo que facilita la administración de permisos.
    
- **Pregunta 3**: Explica qué es un UID (Identificador de Usuario) y cómo se usa para distinguir entre usuarios del sistema y usuarios normales.  
    **Respuesta esperada**: Los UID menores a 1000 son reservados para usuarios del sistema (como "root" o servicios internos). Los UID mayores a 1000 corresponden a usuarios creados para personas que acceden al sistema.
    

### 2. **Preguntas sobre comandos y su uso**

- **Pregunta 4**: ¿Qué hace el comando `useradd` y cómo se usa?  
    **Respuesta esperada**: El comando `useradd` se usa para crear un nuevo usuario en el sistema. Por ejemplo, `useradd -m jperez` crea un usuario llamado "jperez" y su directorio home automáticamente.
    
- **Pregunta 5**: ¿Cuál es la diferencia entre los comandos `chmod 664` y `chmod 660` en cuanto a permisos de archivos?  
    **Respuesta esperada**: `chmod 664` otorga permisos de lectura y escritura al propietario y al grupo, y solo lectura a los demás. `chmod 660` otorga permisos de lectura y escritura al propietario y al grupo, pero no otorga permisos a los demás usuarios.
    
- **Pregunta 6**: ¿Cómo puedes cambiar la contraseña de un usuario en Linux?  
    **Respuesta esperada**: Usando el comando `passwd nombre_usuario`, donde "nombre_usuario" es el usuario cuya contraseña deseas cambiar. Ejemplo: `passwd jperez`.
    

### 3. **Preguntas de comprensión**

- **Pregunta 7**: En un sistema Linux, ¿qué ocurre si asignas permisos `777` a un archivo?  
    **Respuesta esperada**: Asignar permisos `777` a un archivo otorga permisos de lectura, escritura y ejecución a todos los usuarios (propietario, grupo y otros). Esto puede ser un riesgo de seguridad, ya que cualquier usuario puede modificar el archivo.
    
- **Pregunta 8**: ¿Cómo puedes agregar un usuario a un grupo adicional en Linux y qué impacto tendría esto en sus permisos?  
    **Respuesta esperada**: Puedes agregar un usuario a un grupo adicional con el comando `usermod -a -G grupo nombre_usuario`. Esto permite que el usuario tenga los permisos asociados a ese grupo adicional sin cambiar su grupo primario.
    
- **Pregunta 9**: ¿Qué comandos usarías para verificar el espacio ocupado por los archivos en un directorio?  
    **Respuesta esperada**: Se pueden usar comandos como `du` para ver el espacio ocupado por archivos en un directorio, o `df` para ver el espacio disponible en el sistema de archivos.
    

### 4. **Preguntas de escenarios prácticos**

- **Pregunta 10**: Imagina que tienes un directorio con archivos importantes y deseas que solo el propietario pueda escribir en el archivo, pero que el grupo y los demás usuarios solo puedan leerlo. ¿Qué permisos usarías?  
    **Respuesta esperada**: Usarías el comando `chmod 644 archivo`, que otorga permisos de lectura y escritura al propietario y solo lectura a los demás usuarios.
    
- **Pregunta 11**: Si un usuario "jperez" pertenece al grupo "estudiantes", pero debe poder realizar tareas administrativas, ¿qué grupo adicional le añadirías?  
    **Respuesta esperada**: Le añadirías al grupo `sudo` para que pueda ejecutar comandos con privilegios de administrador.
    
- **Pregunta 12**: En un entorno multiusuario en Linux, ¿cómo se garantizaría que solo un grupo específico de usuarios tenga acceso a ciertos archivos, mientras que otros no?  
    **Respuesta esperada**: Crearías un grupo para esos usuarios específicos, asignarías los archivos al grupo, y luego usarías `chmod` para establecer los permisos apropiados, por ejemplo: `chmod 770 archivo` para dar acceso solo al propietario y al grupo.


taller 2 - lab 1

### **1. Conceptos básicos**

**Pregunta:** ¿Cuál es la diferencia entre publicar una página web estática y ejecutar una API REST en una máquina virtual?  
**Respuesta:**

- Una página web estática consiste en archivos HTML, CSS y JS que el servidor entrega directamente al navegador.
    
- Una API REST es un servicio que expone endpoints para enviar y recibir datos, normalmente en formato JSON, y requiere ejecutar un programa en la MV (por ejemplo, Flask o Node.js).
### **2. Página web estática simple**

**Pregunta:** Menciona los pasos para desplegar una página web estática simple en la MV.  
**Respuesta:**

1. Crear un repositorio en GitHub con los archivos de la página (`websimple`).
    
2. Acceder a la MV y entrar a `/var/www/html/`.
    
3. Clonar el repositorio con:
    
    `sudo git clone https://github.com/<usuario>/websimple.git`
    
1. Abrir el navegador y visitar `http://<IP_PUBLICA>/websimple`.
### **3. API REST con Python**

**Pregunta:** ¿Qué pasos sigues para ejecutar una API REST con Flask en la máquina virtual?  
**Respuesta:**

1. Crear y subir un repositorio `api-students` a GitHub.
    
2. En la MV, crear directorio `/home/ubuntu/python3` y clonar el repo:
    
    `git clone https://github.com/<usuario>/api-students.git`
    
3. Instalar Flask:
    
    `pip3 install flask`
    
4. Crear la base de datos:
    
    `python3 db.py`
    
5. Abrir el puerto 8000 en AWS (grupo de seguridad).
    
6. Ejecutar la API:
    
    `python3 app.py`
    
1. Probar con Postman o navegador: `http://<IP_PUBLICA>:8000`.
### **4. Puertos y seguridad**

**Pregunta:** ¿Por qué es necesario abrir el puerto 8000 en el grupo de seguridad de la MV para la API?  
**Respuesta:**  
Porque por defecto, AWS bloquea las conexiones entrantes a la MV. Abrir el puerto 8000 permite que clientes externos (como Postman o un navegador) accedan al servicio que corre en ese puerto.

### **5. Pregunta de razonamiento**

**Pregunta:** ¿Por qué es importante detener la MV desde la consola de AWS y no solo cerrar la terminal SSH?  
**Respuesta:**  
Porque cerrar la terminal no apaga la instancia, solo cierra la sesión. La MV sigue consumiendo recursos y costos en AWS hasta que se detenga explícitamente desde la consola o con un comando de apagado.



taller 2 lab 2

trata de **Infraestructura como Código (IaC)** con **AWS CloudFormation**, para crear, automatizar y eliminar máquinas virtuales (EC2). Esto es más teórico-práctico que los talleres anteriores, porque ya no se trata de ejecutar manualmente comandos, sino de describir infraestructura en plantillas (YAML/JSON) y gestionarla desde consola o AWS CLI.

Aquí tienes un **banco de preguntas y respuestas tipo examen escrito**:

---

### **1. Conceptos**

**Pregunta:** ¿Qué es _Infraestructura como Código (IaC)_?  
**Respuesta:** Es la práctica de aprovisionar y gestionar infraestructura (como servidores, redes, bases de datos) mediante código en lugar de configuraciones manuales. Permite automatizar, replicar entornos y reducir errores de configuración.

---

### **2. Beneficios**

**Pregunta:** Menciona dos beneficios de usar IaC en proyectos de computación en la nube.  
**Respuesta:**

1. Configurar rápidamente entornos completos, desde desarrollo hasta producción.
    
2. Duplicar fácilmente entornos y reducir errores humanos al evitar configuraciones manuales.
    

---

### **3. CloudFormation**

**Pregunta:** ¿Qué es AWS CloudFormation y para qué sirve?  
**Respuesta:** Es un servicio de AWS que permite definir y aprovisionar infraestructura en la nube mediante plantillas en YAML o JSON. Con estas plantillas se pueden crear, modificar o eliminar recursos como máquinas virtuales (EC2), redes, volúmenes, etc., de manera automatizada.

---

### **4. Ejercicio práctico**

**Pregunta:** ¿Cuáles son los pasos básicos para crear una máquina virtual en AWS usando CloudFormation desde la consola web?  
**Respuesta:**

1. Ingresar a CloudFormation y crear una pila (stack).
    
2. Subir o elegir una plantilla (YAML/JSON).
    
3. Asignar un nombre a la pila y modificar parámetros por defecto.
    
4. Confirmar y enviar.
    
5. Verificar que la pila y la instancia EC2 se hayan creado correctamente.
    

---

### **5. Plantilla avanzada**

**Pregunta:** ¿Cómo se puede crear una máquina virtual que automáticamente sirva dos páginas web (websimple y webplantilla) usando CloudFormation?  
**Respuesta:** Se usa una plantilla (ej. `plantilla_crear_mv_con_webs.yaml`) que incluye un script en _UserData_ para instalar dependencias y clonar los repositorios de GitHub (`websimple` y `webplantilla`). Luego, al crear la pila con esa plantilla, la MV quedará lista con ambas webs disponibles en enlaces distintos.

---

### **6. Eliminación de recursos**

**Pregunta:** ¿Qué ocurre al eliminar una pila (stack) en CloudFormation?  
**Respuesta:** Al eliminar una pila, todos los recursos que fueron creados con esa plantilla (como máquinas virtuales EC2) también se eliminan automáticamente, evitando costos innecesarios.

---

### **7. Uso de AWS CLI**

**Pregunta:** Escribe el comando de AWS CLI para crear una pila llamada `"crear-mv-con-webs"` con una plantilla YAML.  
**Respuesta:**

`aws cloudformation create-stack --stack-name "crear-mv-con-webs" --template-body file://plantilla_crear_mv_con_webs.yaml --parameters ParameterKey=InstanceName,ParameterValue="MV con 2 Webs" ParameterKey=AMI,ParameterValue="ami-xxxxxxxx"`

---

### **8. Verificación**

**Pregunta:** ¿Qué comando de AWS CLI se usa para verificar los resultados (outputs) de una pila creada?  
**Respuesta:**

`aws cloudformation describe-stacks --stack-name "crear-mv-con-webs"`

---

### **9. Eliminación con AWS CLI**

**Pregunta:** ¿Cómo eliminas una pila desde AWS CLI y cómo confirmas que se eliminó?  
**Respuesta:**

1. Eliminar:
    
    `aws cloudformation delete-stack --stack-name "crear-mv-con-webs"`
    
2. Confirmar:
    
    `aws cloudformation describe-stacks --stack-name "crear-mv-con-webs"`
    
    (Debe indicar que la pila ya no existe).
    

---

### **10. Razonamiento**

**Pregunta:** Explica por qué usar IaC con CloudFormation es mejor que crear manualmente instancias EC2 desde la consola de AWS.  
**Respuesta:**  
Porque permite automatizar la infraestructura, replicarla en distintos entornos, mantener un control de versiones (ya que las plantillas son código), y reducir errores humanos. Además, facilita el despliegue de proyectos grandes con múltiples recursos de forma consistente.




comandos docker 
![[Pasted_image_20250929165529.jpg]]


![[Pasted_image_20250929165637.jpg]]
semana 3 lab 1
## 📦 Preguntas Teóricas sobre Contenedores

**P1. ¿Qué problema soluciona Docker con los contenedores?**  
👉 Permite empaquetar aplicaciones con todas sus dependencias en un entorno aislado, asegurando que funcionen igual en cualquier máquina.

---

**P2. ¿Cuál es la diferencia entre un contenedor y una máquina virtual?**  
👉

- **VM**: incluye un sistema operativo completo → más pesado.
    
- **Contenedor**: comparte el kernel del SO anfitrión → más liviano, rápido y eficiente.
    

---

**P3. ¿Qué es una imagen en Docker?**  
👉 Una plantilla de solo lectura que contiene todo lo necesario (código, librerías, dependencias) para ejecutar un contenedor.

---

**P4. ¿Qué es un contenedor en Docker?**  
👉 Una instancia en ejecución de una imagen, que corre de forma aislada pero puede comunicarse con el exterior a través de puertos.

---

**P5. ¿Qué rol cumple el archivo Dockerfile?**  
👉 Define las instrucciones para construir una imagen automáticamente (qué imagen base usar, qué dependencias instalar, qué archivos copiar y qué comando ejecutar al inicio).

---

**P6. ¿Qué significa mapear puertos al ejecutar un contenedor?**  
👉 Relacionar un puerto de la máquina anfitriona con un puerto interno del contenedor, para poder acceder desde fuera (ejemplo: `8080:80`).

---

**P7. ¿Qué diferencia hay entre ejecutar un contenedor en primer plano y en segundo plano (detached)?**  
👉

- **Primer plano**: se ve la ejecución directamente en la consola.
    
- **Segundo plano (`-d`)**: corre en background y no interrumpe la terminal.
    

---

**P8. ¿Qué es la opción `--rm` en la ejecución de un contenedor?**  
👉 Hace que el contenedor se elimine automáticamente al detenerse, evitando acumular contenedores innecesarios.

---

**P9. ¿Cuál es la utilidad de los comandos `logs` y `exec` en Docker?**  
👉

- `logs`: ver lo que está ocurriendo dentro del contenedor (ej. errores o mensajes del servidor).
    
- `exec`: ejecutar comandos dentro de un contenedor que ya está corriendo (ej. abrir una consola bash).
    

---

**P10. ¿Cuál fue la diferencia entre el contenedor de la página web y el de la API REST del taller?**  
👉

- **Página web**: usa Apache (`httpd:2.4`) como base y solo copia los archivos estáticos.
    
- **API REST**: usa Python (`python:3-slim`), instala Flask, crea base de datos y ejecuta un programa (`app.py`).



sem 3 taller 2 
## 📦 Preguntas Teóricas para Repaso

**P1. ¿Cuál es el objetivo principal del Taller 2 de contenedores?**  
👉 Aprender a subir imágenes a Docker Hub, desplegar contenedores en otras máquinas y comparar implementación en MV vs contenedores.

---

**P2. ¿Qué es Docker Hub y para qué se usa?**  
👉 Es el **registro oficial de imágenes Docker** (Docker Registry). Sirve para almacenar y compartir imágenes públicamente o de forma privada.

---

**P3. ¿Qué pasos básicos se siguen para subir una imagen a Docker Hub?**  
👉

1. Crear cuenta en Docker Hub.
    
2. Crear un repositorio.
    
3. Iniciar sesión con `docker login`.
    
4. Etiquetar (`tag`) la imagen local.
    
5. Subir con `docker push`.
    
6. Salir con `docker logout`.
    

---

**P4. ¿Qué ventaja tiene usar Docker Hub en comparación con solo trabajar en la máquina virtual?**  
👉 Permite **compartir y reutilizar imágenes** en cualquier computadora o servidor, sin necesidad de copiar archivos manualmente.

---

**P5. ¿Qué diferencia hay entre ejecutar un contenedor en la misma MV y en otra computadora?**  
👉 En otra computadora se descarga la imagen desde Docker Hub, lo que permite **portabilidad** y facilita el despliegue en distintos entornos

taller 
### 🔹 Docker Hub y portabilidad

**P4. ¿Qué es Docker Hub?**  
👉 Es un servicio en la nube que funciona como registro oficial de imágenes Docker, permitiendo almacenar y compartir imágenes.

**P5. ¿Por qué es importante subir imágenes a Docker Hub?**  
👉 Porque permite distribuir las imágenes en cualquier computadora o servidor, facilitando el despliegue en distintos entornos.

**P6. ¿Qué pasos se siguen para subir una imagen a Docker Hub?**  
👉 Iniciar sesión (`docker login`), etiquetar la imagen (`docker tag`), subirla (`docker push`) y cerrar sesión (`docker logout`).

**P7. ¿Cuál es la diferencia entre construir una imagen localmente y usar una imagen desde Docker Hub?**  
👉 La imagen local debe generarse con un Dockerfile en tu máquina, mientras que la de Docker Hub se descarga directamente y está lista para usarse.

---

### 🔹 Despliegue en múltiples máquinas

**P8. ¿Qué ventaja tiene usar imágenes de Docker Hub para desplegar contenedores en otra computadora?**  
👉 Permite ejecutar la aplicación en cualquier máquina sin necesidad de copiar manualmente el código o reconstruir la imagen.

**P9. ¿Qué significa mapear puertos al ejecutar un contenedor?**  
👉 Es la relación entre un puerto del sistema anfitrión y un puerto dentro del contenedor, lo que permite acceder al servicio desde fuera.

**P10. ¿Qué rol cumple AWS CloudFormation en el despliegue de contenedores?**  
👉 Permite automatizar la creación de instancias EC2 y otros recursos necesarios mediante una plantilla declarativa.

---

### 🔹 Docker Compose

**P11. ¿Qué es Docker Compose?**  
👉 Es una herramienta que permite definir y ejecutar aplicaciones multicontenedor mediante un archivo `docker-compose.yml`.

**P12. ¿Qué información se define en un archivo `docker-compose.yml`?**  
👉 Servicios, imágenes o Dockerfiles, puertos expuestos, redes, volúmenes y variables de entorno.

**P13. ¿Qué ventajas ofrece Docker Compose frente a ejecutar contenedores manualmente?**  
👉 Facilita levantar y detener todos los servicios con un solo comando, maneja redes internas automáticamente y simplifica la configuración.

**P14. ¿Cuál es la diferencia entre los comandos `docker compose up` y `docker compose down`?**  
👉 `up` levanta los contenedores definidos en `docker-compose.yml`, mientras que `down` los detiene y elimina.

**P15. ¿Por qué es útil Docker Compose en arquitecturas de microservicios?**  
👉 Porque permite ejecutar simultáneamente varios servicios (por ejemplo, una API y un servidor web) de forma integrada y orquestada.



sem 4 taller 2 
**P1. ¿Qué es una aplicación multicontenedor en Docker?**  
👉 Es una aplicación que se compone de varios contenedores independientes que trabajan juntos, cada uno ejecutando un servicio específico.

**P2. ¿Qué herramienta se utiliza para definir y ejecutar aplicaciones multicontenedor?**  
👉 Docker Compose, mediante un archivo `docker-compose.yml`.

**P3. ¿Qué ventajas tiene una aplicación multicontenedor frente a una aplicación en un solo contenedor?**  
👉 Permite separar responsabilidades (por ejemplo, API, base de datos, frontend), facilita el escalamiento independiente y mejora el mantenimiento.

**P4. ¿Qué es un microservicio dentro de una arquitectura multicontenedor?**  
👉 Es un servicio autónomo y especializado que corre en su propio contenedor y se comunica con otros microservicios mediante redes internas.

**P5. ¿Qué pasos son necesarios para publicar una aplicación multicontenedor en Docker Hub?**  
👉 Construir las imágenes de cada servicio, etiquetarlas con el nombre de usuario de Docker Hub, hacer `docker push` de cada imagen y luego referenciarlas en `docker-compose.yml`.

**P6. ¿Cuál es el propósito de la carpeta `compose push` en este taller?**  
👉 Contiene la configuración y comandos necesarios para preparar y subir las imágenes de la aplicación multicontenedor a Docker Hub.

**P7. ¿Cuál es el propósito de la carpeta `compose deploy` en este taller?**  
👉 Contiene la configuración y comandos necesarios para desplegar la aplicación multicontenedor en otra máquina descargando las imágenes desde Docker Hub.



**P9. ¿Por qué es importante definir redes internas en Docker Compose para aplicaciones multicontenedor?**  
👉 Porque permiten la comunicación entre contenedores sin exponer todos los servicios al exterior, mejorando la seguridad y el aislamiento.




**P1. ¿Qué es Amazon S3?**  
👉 Es un servicio de almacenamiento de objetos en la nube de AWS, escalable, duradero y de alta disponibilidad.

**P2. ¿Qué se almacena dentro de un bucket en S3?**  
👉 Objetos, que consisten en un archivo (de cualquier tipo) más metadatos asociados.

**P3. ¿Qué tipos de archivos se pueden guardar en S3?**  
👉 Cualquier tipo de archivo: CSV, JSON, imágenes, vídeos, PDFs, logs, backups, etc.

**P4. ¿Cuál es el tamaño máximo de un objeto en S3?**  
👉 Hasta 5 TB por objeto.

**P5. ¿Es cierto que S3 tiene almacenamiento infinito?**  
👉 No es literalmente infinito, pero es prácticamente ilimitado: no hay límite en el número de objetos ni en la capacidad total de un bucket; solo se paga por lo que se usa.

**P6. ¿Cuál es la diferencia entre S3 y una base de datos tradicional?**  
👉 S3 almacena objetos sin un esquema fijo, mientras que una base de datos organiza datos en tablas estructuradas con un esquema definido.

**P7. ¿Qué rol cumple AWS Glue en relación con S3?**  
👉 Glue se encarga de catalogar los datos almacenados en S3, creando metadatos y esquemas que describen esos datos como si fueran tablas.

**P8. ¿Qué permite hacer Amazon Athena sobre los datos de S3?**  
👉 Permite ejecutar consultas SQL directamente sobre los archivos en S3, usando los metadatos catalogados por Glue.

**P9. ¿Qué formatos de archivos son ideales para consultar con Athena?**  
👉 Formatos tabulares y optimizados para analítica, como CSV, JSON, Parquet y ORC.

**P10. ¿Cuál es el flujo típico entre S3, Glue y Athena?**  
👉 1) Los datos se almacenan en S3.  
👉 2) Glue detecta y cataloga esos datos, creando tablas con metadatos.  
👉 3) Athena permite consultar esas tablas con SQL sin mover los datos de S3.

**P11. ¿Por qué es importante que S3 sea altamente escalable y duradero?**  
👉 Porque garantiza que los datos se puedan almacenar sin preocuparse por el tamaño o la disponibilidad, siendo accesibles en cualquier momento.

**P12. ¿Qué ventaja tiene usar Athena frente a copiar los datos de S3 a una base de datos relacional?**  
👉 Se pueden consultar directamente los datos en su ubicación original, sin necesidad de cargarlos o transformarlos previamente en otra base.

# Preguntas y Respuestas – Arquitectura MySQL + API REST + Web

**P1. ¿Qué componentes forman una arquitectura básica de aplicación en contenedores con base de datos, API y frontend?**  
👉 Una base de datos (ej. MySQL), una API REST (ej. FastAPI) y una aplicación web frontend.

**P2. ¿Qué función cumple la base de datos MySQL en esta arquitectura?**  
👉 Almacena de manera persistente los datos de empleados u otra información que será consultada por la API.

**P3. ¿Qué función cumple la API REST construida con FastAPI?**  
👉 Actúa como intermediario entre la base de datos y el frontend, ofreciendo endpoints para crear, leer, actualizar y eliminar información.

**P4. ¿Por qué se necesita habilitar CORS en la API REST?**  
👉 Para permitir que el frontend web, que corre en un origen distinto, pueda consumir los endpoints de la API sin restricciones de navegador.

**P5. ¿Qué rol cumple la aplicación web frontend en la arquitectura?**  
👉 Proporcionar una interfaz gráfica para que los usuarios interactúen con los datos que expone la API.

**P6. ¿Qué herramienta se utiliza normalmente para probar los endpoints de una API REST antes de conectarla al frontend?**  
👉 Postman, que permite enviar peticiones a los endpoints y validar sus respuestas.

**P7. ¿Por qué es útil usar Docker Compose en una arquitectura con base de datos, API y frontend?**  
👉 Porque permite levantar todos los servicios con un solo comando, conectándolos en la misma red interna de contenedores.

**P8. ¿Qué ventaja ofrece ejecutar la base de datos, la API y el frontend en contenedores frente a instalarlos directamente en una máquina virtual?**  
👉 Facilita la portabilidad, el despliegue repetible y la escalabilidad independiente de cada servicio.

**P9. ¿Qué beneficio ofrece definir la infraestructura con una plantilla de CloudFormation en lugar de crear manualmente una máquina virtual en AWS?**  
👉 Automatiza la creación de recursos, asegura consistencia y ahorra tiempo en el despliegue.

**P10. ¿Cómo se comunican entre sí la base de datos, la API REST y el frontend en esta arquitectura?**  
👉 La API envía consultas y actualizaciones a la base de datos MySQL, y el frontend consume los endpoints expuestos por la API para mostrar los datos a los usuarios.

**P1. ¿Qué es el balanceo de carga en sistemas distribuidos?**  
👉 Es la técnica de distribuir solicitudes entrantes entre varios servidores para mejorar el rendimiento y evitar sobrecargas.

**P2. ¿Qué es la alta disponibilidad en sistemas de TI?**  
👉 Es la capacidad de un sistema para seguir funcionando correctamente incluso cuando falla alguno de sus componentes.

**P3. ¿Qué ventaja ofrece el balanceo de carga frente a usar un solo servidor?**  
👉 Permite manejar más tráfico, evitar cuellos de botella y mejorar tiempos de respuesta.

**P4. ¿Qué ventaja ofrece desplegar instancias en distintas zonas de disponibilidad (AZs)?**  
👉 Garantiza que si una zona falla, las demás sigan prestando servicio, aumentando la disponibilidad del sistema.

**P5. ¿Qué servicio de AWS se utiliza comúnmente como balanceador de carga?**  
👉 Elastic Load Balancer (ELB).

**P6. ¿Qué diferencia hay entre escalabilidad vertical y horizontal?**  
👉

- Vertical: mejorar la capacidad de un solo servidor (más CPU, más RAM).
    
- Horizontal: añadir más servidores que trabajan en paralelo.
    

**P7. ¿Por qué balanceo de carga y alta disponibilidad suelen ir de la mano?**  
👉 Porque el balanceo distribuye el tráfico y la alta disponibilidad garantiza que siempre haya servidores disponibles para atenderlo.

**P8. ¿Qué beneficios principales aporta una arquitectura con balanceo y alta disponibilidad?**  
👉 Mayor rendimiento, resiliencia ante fallos, escalabilidad y mejor experiencia de usuario.



**P1. ¿Qué significa el término “ingesta de datos” en un proceso de Data Science?**  
👉 Es el proceso de recolectar y trasladar datos desde múltiples fuentes hacia un sistema central de almacenamiento o análisis.

**P2. ¿Cuáles son los dos enfoques principales de ingesta de datos?**  
👉 Ingesta por lotes (batch ingestion) e ingesta en tiempo real (streaming ingestion).

**P3. ¿Qué caracteriza a la ingesta por lotes?**  
👉 Los datos se cargan en bloques grandes, de forma periódica, como archivos diarios o semanales.

**P4. ¿Qué caracteriza a la ingesta en tiempo real?**  
👉 Los datos se capturan y procesan de manera continua a medida que llegan, útil para aplicaciones como IoT o monitoreo en línea.

**P5. ¿Qué tipos de fuentes pueden alimentar un proceso de ingesta de datos?**  
👉 Bases de datos relacionales, APIs, archivos CSV/JSON, logs, sensores IoT, redes sociales.

**P6. ¿Por qué es importante la ingesta en un pipeline de analítica de datos?**  
👉 Porque garantiza que los datos lleguen al sistema central de manera oportuna, confiable y con un formato adecuado para su análisis posterior.

**P7. ¿Qué retos presenta la ingesta de datos?**  
👉 Manejar diferentes formatos de origen, asegurar la calidad, limpiar inconsistencias y garantizar la confiabilidad del flujo de datos.

**P8. ¿Cómo se relaciona la ingesta con un data lake o un data warehouse?**  
👉 La ingesta alimenta el data lake o warehouse con datos crudos o procesados, que luego serán transformados y analizados.


## 📦 Preguntas y Respuestas – Balanceo de Carga y Alta Disponibilidad (Parte 2 y 3)

**P1. ¿Cuál es el objetivo del balanceo de carga en aplicaciones desplegadas en contenedores?**  
👉 Distribuir las solicitudes entrantes entre múltiples instancias de un servicio para mejorar rendimiento y evitar sobrecargas.

**P2. ¿Qué significa que una aplicación tenga alta disponibilidad?**  
👉 Que puede seguir funcionando correctamente incluso si una instancia o zona de disponibilidad falla.

**P3. ¿Cómo se puede lograr alta disponibilidad en una API desplegada en contenedores?**  
👉 Ejecutando múltiples instancias de la API en diferentes máquinas o zonas y conectándolas detrás de un balanceador de carga.

**P4. ¿Por qué se habilita CORS en algunas APIs dentro de estas arquitecturas?**  
👉 Para permitir que clientes web en dominios distintos puedan consumir los endpoints sin restricciones del navegador.

**P5. ¿Qué herramienta se usa para probar las APIs balanceadas en estos talleres?**  
👉 Postman, mediante colecciones preparadas para las APIs (ej. `api-employees` o `api-fruits`).

**P6. ¿Qué beneficio ofrece un diagrama de arquitectura en estos casos?**  
👉 Ayuda a visualizar cómo se conectan los componentes: balanceador, instancias de la API, base de datos y clientes.

**P7. ¿Qué diferencia hay entre el ejemplo de la API de empleados y el de la API de frutas?**  
👉 Ambos ilustran el mismo concepto de balanceo y alta disponibilidad, pero aplicados a APIs distintas para reforzar la práctica.

**P8. ¿Qué ocurre si una de las instancias detrás del balanceador falla?**  
👉 El balanceador redirige automáticamente las solicitudes hacia las instancias que sigan disponibles, manteniendo el servicio activo.

**P9. ¿Por qué balanceo de carga y alta disponibilidad suelen ser implementados juntos?**  
👉 Porque el balanceo distribuye el tráfico, y la alta disponibilidad asegura que siempre existan instancias activas para atenderlo.

**P10. ¿Qué ventaja general aporta esta arquitectura a un sistema de microservicios?**  
👉 Escalabilidad, resiliencia ante fallas, mejor experiencia de usuario y capacidad de manejar más tráfico concurrente.


**P1.** En un sistema con balanceo de carga, todas las solicitudes entran a un único servidor.  
👉 **Falso** – El balanceador reparte solicitudes entre varias instancias.

**P2.** Alta disponibilidad significa que el sistema sigue funcionando incluso si una instancia falla.  
👉 **Verdadero**.

**P3.** La escalabilidad horizontal consiste en mejorar el hardware de una sola máquina con más CPU o RAM.  
👉 **Falso** – Eso es escalabilidad vertical. La horizontal es añadir más instancias.

**P4.** Con un balanceador de carga, si una instancia deja de responder, las demás pueden seguir atendiendo solicitudes.  
👉 **Verdadero**.

**P5.** El balanceo de carga y la alta disponibilidad son conceptos independientes y nunca se usan juntos.  
👉 **Falso** – Normalmente se implementan en conjunto.

**P6.** Una arquitectura con balanceo de carga y alta disponibilidad ofrece mejor tolerancia a fallos y mejor experiencia de usuario.  
👉 **Verdadero**.