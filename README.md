# Linktic
**Prueba alternativa:** [Ver Gist](https://gist.github.com/AndresLinktic/a00ef10d5f99a59830a65c5385052e95)

## Requerimiento
La prueba presentada consiste en una serie de microservicios que permiten personalizar la administración de dispositivos IoT.

## Componentes

### 1. Gateway
Este componente es una implementación de **Spring Cloud Gateway** ([ver más](https://spring.io/projects/spring-cloud-gateway)), encargada de orquestar las peticiones y aplicar filtros personalizados, como la validación de autenticación en las solicitudes.

- **Repositorio:** [https://github.com/yaku-wm/api-gateway](https://github.com/yaku-wm/api-gateway)
- **URL:** [https://yaku-gateway.innovatexiot.com/](https://yaku-gateway.innovatexiot.com/)

### 2. Identity Management
Este microservicio se encarga de la creación de usuarios y de exponer servicios relacionados con la gestión de roles, grupos y autenticación. Está basado en **Identity Platform** de Google Cloud Platform (GCP).

- **Repositorio:** [https://github.com/yaku-wm/identity-management](https://github.com/yaku-wm/identity-management)
- **Swagger UI:** [https://yaku-gateway.innovatexiot.com/identity-management/swagger-ui/index.html](https://yaku-gateway.innovatexiot.com/identity-management/swagger-ui/index.html)

### 3. ChirpStack Management
Microservicio encargado de la comunicación vía **gRPC** con el servidor de red **ChirpStack** ([ver más](https://www.chirpstack.io/)), usado para la administración de dispositivos IoT.

- **Repositorio:** [https://github.com/yaku-wm/chirpstack-management](https://github.com/yaku-wm/chirpstack-management)
- **Swagger UI:** [https://yaku-gateway.innovatexiot.com/chirpstack-management-api/swagger-ui/index.html](https://yaku-gateway.innovatexiot.com/chirpstack-management-api/swagger-ui/index.html)

### 4. Device
Este microservicio se comunica vía **gRPC** con el microservicio **ChirpStack Management**, aplicando reglas de negocio y exponiendo funcionalidades a través de una API **REST**.

- **Repositorio:** [https://github.com/yaku-wm/device](https://github.com/yaku-wm/device)
- **Swagger UI:** [https://yaku-gateway.innovatexiot.com/device-api/swagger-ui/index.html](https://yaku-gateway.innovatexiot.com/device-api/swagger-ui/index.html)

## Arquitectura y Componentes Cloud

- **Cloud DNS:** Utilizado para mapear el dominio `innovatexiot.com` a los servicios desplegados en **Cloud Run**.
- **Cloud Load Balancing:** Recibe y distribuye las solicitudes hacia los contenedores ejecutados en **Cloud Run**.
- **Cloud Run:** Servicio serverless que ejecuta los microservicios contenerizados.
- **Firestore:** Base de datos NoSQL utilizada como principal.
- **Identity Platform:** Gestiona la administración de usuarios de forma centralizada.
- **Cloud Storage:** Almacenamiento en la nube para archivos y datos no estructurados.
- **Secret Manager:** Maneja información sensible como llaves privadas y API keys.
- **Cloud IAM:** Gestiona los permisos y roles para las cuentas de servicio que interactúan con los servicios de GCP.
- **Cloud Logging:** Recolecta y gestiona los logs de los servicios de backend para su monitoreo y análisis.
- **Artifact Registry:** Almacena las imagenes generadas por Cloud Build que posteriormente se despliegan en Cloud Run.
- **Cloud Build:** Herramienta de compilacion y despliegue automatico usada para publicar una nueva version cada vez que se hace un commit a la rama principal.
- **Github:** Utilizado como repositorio remoto y conectado a Cloud Build para el proceso de CI/CD.

![image](https://github.com/user-attachments/assets/cc0bca27-4031-4a4b-b65a-7cc34ccb240a)

