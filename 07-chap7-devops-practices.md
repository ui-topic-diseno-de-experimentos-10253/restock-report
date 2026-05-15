# Capítulo VII: DevOps Practices

## 7.1. Continuous Integration

### 7.1.1. Tools and Practices

Para la etapa de Continuous Integration (CI) del proyecto Restock, se han definido herramientas y prácticas que garantizan la calidad y estabilidad del código de las tres plataformas (Backend, Frontend y Móvil) antes de llegar a la fase de despliegue continuo.

GitHub Actions
Se utiliza como orquestador nativo de integración continua. Evalúa automáticamente el código fuente compilándolo y ejecutando la suite de pruebas cada vez que se detectan cambios, bloqueando cualquier integración defectuosa.

SonarCloud
Herramienta integrada en el flujo de CI para realizar análisis estático de código. Permite evaluar la calidad estructural del backend desarrollado en Spring Boot y del frontend en Angular, detectando vulnerabilidades de seguridad, code smells y midiendo la cobertura de las pruebas.

JUnit 5 y Mockito
Son los frameworks elegidos para la automatización de pruebas en el backend Java. JUnit 5 estructura el ciclo de vida de los tests, mientras que Mockito aísla los componentes de negocio (como el procesamiento de datos del ESP32) simulando el comportamiento de las dependencias externas.

Práctica: Single Branch Architecture y Validación Estricta
Para mantener la máxima coherencia del sistema Restock, la arquitectura del proyecto se enfoca en el uso de una única rama principal (main) por cada sistema, evitando la complejidad de múltiples ramas divergentes. La regla fundamental del equipo dicta que ningún cambio puede permanecer en la rama principal si no ha superado con éxito el 100% de las pruebas automatizadas del pipeline. Además, se exigen Conventional Commits para mantener la trazabilidad del historial.

### 7.1.2. Build & Test Suite Pipeline Components

## 7.2. Continuous Delivery

### 7.2.1. Tools and Practices

Para la etapa de *Continuous Delivery* (Entrega Continua) del proyecto Restock, el objetivo es garantizar que cualquier versión del código del Backend que haya superado la Integración Continua esté empaquetada y lista para ser desplegada en un entorno de pruebas (Staging), exigiendo una validación humana antes de su pase a Producción.

#### Herramientas (Tools)
* **GitHub Actions:** Actúa como el orquestador principal. Tras un *push* o *merge* en la rama `develop`, desencadena los flujos para construir el artefacto candidato a *release* (Release Candidate).
* **Docker:** Se utiliza para contenerizar el backend (Spring Boot). Se ha implementado un `Dockerfile` con arquitectura *multi-stage build* usando OpenJDK 21, lo que garantiza que el artefacto del entorno de Staging sea idéntico al que se desplegará en Producción, eliminando discrepancias entre entornos.
* **Render (Staging Environment):** Plataforma Cloud utilizada para alojar el entorno de pruebas. Mediante integraciones de *Deploy Hooks* (Webhooks) gestionados como *Secrets*, el orquestador notifica a Render para que descargue y levante el contenedor del API REST.
* **GitHub Environments:** Herramienta de seguridad y control de despliegues utilizada para gestionar reglas de protección y aislar lógicamente los entornos del servidor.

#### Prácticas (Practices)
* **Separación de Entornos (Environment Promotion):** Se mantiene una estricta separación lógica entre el entorno de Staging y Producción. Ningún artefacto pasa a producción sin haber sido probado primero en el entorno de entrega.
* **Aprobación Manual (Manual Release Gates):** Es la práctica central del *Continuous Delivery*. El pipeline se detiene en seco antes de tocar el servidor de Staging hasta que el equipo de QA o el Product Owner valide el estado del repositorio y apruebe manualmente la ejecución.

### 7.2.2. Stages Deployment Pipeline Components

El pipeline de Entrega Continua de Restock está diseñado exclusivamente para el ciclo de vida del **Backend (API REST)**. A continuación, se detalla la configuración secuencial automatizada:

#### 1. Pipeline Definition & Branching
Para mantener la trazabilidad de GitFlow, se implementó el archivo orquestador `cd-staging.yml` dentro de una rama específica (`feature/cd-staging-pipeline`). Este archivo define los pasos de preparación del JDK 21, empaquetado de Maven, construcción de Docker y notificación a Render.

![Creación de rama y definición del pipeline CD](assets/images/chapter7/continuous_delivery/step1.png)

#### 2. Verification & Manual Approval Gate (Entorno Protegido)
Para garantizar la intervención humana, se configuró un entorno lógico denominado **"Staging"** utilizando las reglas de protección de *GitHub Environments*. Se designaron revisores obligatorios del equipo central para evitar despliegues no autorizados.

![Configuración del entorno Staging y revisores requeridos](assets/images/chapter7/continuous_delivery/step4.png)

Al dispararse el pipeline, el flujo reconoce la dependencia del entorno y entra en un estado de pausa (`Waiting`). Queda a la espera de que los revisores evalúen la estabilidad del código.

![Pipeline en pausa esperando aprobación manual](assets/images/chapter7/continuous_delivery/step5.png)

Una vez confirmada la integridad del repositorio, el revisor asignado autoriza el despliegue dejando un comentario de conformidad y ejecutando la acción **"Approve and deploy"**.

![Aprobación manual del despliegue por parte del equipo](assets/images/chapter7/continuous_delivery/step6.png)

#### 3. Trigger & Artifact Generation Stage
Tras la aprobación manual, el servidor virtual retoma la ejecución. Procede con el empaquetado del `.jar` de Spring Boot y ejecuta la directiva `docker build`. Como se evidencia en los *logs* del orquestador, el proceso *multi-stage* descarga las dependencias de Java 21, empaqueta el sistema y genera la imagen candidata (`restock-backend-staging:latest`) de forma exitosa.

![Logs de construcción exitosa de la imagen Docker en la nube](assets/images/chapter7/continuous_delivery/step3.png)

#### 4. Staging Deployment Stage
Finalmente, mediante el uso de credenciales encriptadas (*GitHub Secrets*), el orquestador dispara un webhook (`curl -X POST`) hacia Render. Render detecta la petición, extrae la imagen generada y la publica en su infraestructura de nube gratuita, finalizando el pipeline de Entrega Continua con éxito.

![Ejecución finalizada y aprobada del pipeline de Entrega Continua](assets/images/chapter7/continuous_delivery/step7.png)

## 7.3. Continuous deployment

### 7.3.1. Tools and Practices

Para la estrategia de *Continuous Deployment* del proyecto Restock se seleccionaron herramientas que ya forman parte del stack documentado en el Capítulo V, con el objetivo de automatizar la publicación de cada entrega estable y reducir la intervención manual en el proceso de despliegue.

#### GitHub Actions

GitHub Actions se utiliza como orquestador de automatización para ejecutar los flujos de build, validación y despliegue a partir de cambios en la rama principal. Esta elección permite centralizar la lógica de entrega continua dentro del mismo repositorio del proyecto, mantener trazabilidad sobre cada versión publicada y asegurar que el proceso sea repetible.

#### GitHub Pages

GitHub Pages se emplea para alojar el frontend web de Restock. Es una opción adecuada para la Landing Page y la interfaz web porque permite publicar contenido estático de manera directa desde GitHub, con despliegue automático luego de cada actualización aprobada en el repositorio. Además, simplifica la distribución del frontend al no requerir infraestructura adicional para el hosting estático.

#### Render

Render se utiliza como servicio de hosting para el backend RESTful desarrollado con Java y Spring Boot. En este caso, la plataforma resulta conveniente porque detecta el repositorio conectado, construye la aplicación de forma automática a partir del `Dockerfile` y expone una URL pública para consumir la API. Esto facilita desplegar una versión funcional del backend sin administrar servidores manualmente.

#### Firebase App Distribution

Firebase App Distribution se usa para compartir versiones preliminares de la aplicación móvil Android con testers internos y externos. Esta herramienta es útil porque permite distribuir APKs de prueba de forma controlada, recopilar retroalimentación temprana y mantener un ciclo de validación ágil antes de una publicación formal.

#### Docker

Docker complementa el despliegue del backend al encapsular la aplicación y sus dependencias en una imagen reproducible. Con ello, se reducen diferencias entre entornos, se estandariza la ejecución y se facilita que Render construya y publique la API con consistencia en cada actualización.

En conjunto, estas herramientas permiten que el flujo de despliegue del proyecto sea coherente con su arquitectura real: frontend estático en GitHub Pages, backend REST en Render y distribución móvil de pruebas mediante Firebase App Distribution, todo coordinado desde GitHub.

### 7.3.2. Production Deployment Pipeline Components

El pipeline de despliegue en producción de Restock se compone de etapas automatizadas y componentes de infraestructura que permiten publicar cambios de forma segura, trazable y consistente para frontend web y backend REST, además de una etapa controlada para distribución móvil.

#### 1. Source Stage (Control de código fuente)

- Repositorios en GitHub para frontend, backend y móvil.
- Estrategia de integración sobre la rama principal (`main`) luego de revisión y aprobación de cambios.
- Commits versionados que funcionan como punto de trazabilidad para cada despliegue.

#### 2. Pipeline Orchestrator (Automatización)

- GitHub Actions como orquestador central del flujo.
- Disparadores automáticos por `push` en `main` y, cuando corresponde, por ejecución manual para despliegues controlados.
- Separación por jobs para construir, validar y desplegar cada componente de la plataforma.

#### 3. Build and Validation Stage

- Frontend web: compilación con Angular CLI para generar artefactos estáticos de producción.
- Backend: construcción de imagen Docker a partir del proyecto Java Spring Boot.
- Validaciones previas de calidad y consistencia antes de liberar artefactos.

#### 4. Artifact and Configuration Stage

- Artefacto frontend: salida estática lista para publicación en GitHub Pages.
- Artefacto backend: imagen Docker lista para ejecución en Render.
- Variables de entorno administradas fuera del código fuente para credenciales, conexiones y URLs de servicios.

#### 5. Production Deploy Stage

- Frontend web en GitHub Pages con publicación automática de la versión compilada.
- Backend REST en Render con build y despliegue automático a partir del repositorio conectado.
- Exposición de endpoints productivos mediante URL pública para consumo desde clientes web y móvil.

#### 6. Post-Deployment Verification Stage

- Verificación funcional de disponibilidad del frontend publicado.
- Verificación de salud de la API REST y consulta de documentación Swagger/OpenAPI.
- Validación de conectividad frontend-backend y de variables de entorno en producción.

#### 7. Mobile Release Distribution (Controlado)

- Generación de APK firmado de la aplicación móvil.
- Distribución mediante Firebase App Distribution para validación con testers.
- Retroalimentación previa a una liberación formal en tiendas, manteniendo control de calidad sobre cada versión.

#### Flujo resumido del pipeline

1. Un cambio aprobado se integra a `main`.
2. GitHub Actions inicia el pipeline y ejecuta build y validaciones.
3. Se generan artefactos de frontend y backend.
4. GitHub Pages publica el frontend y Render actualiza la API REST.
5. Se ejecutan verificaciones posteriores de disponibilidad e integración.
6. Para móvil, la versión se distribuye en Firebase App Distribution para validación controlada.

## 7.4. Continuous Monitoring

### 7.4.1. Tools and Practices

### 7.4.2. Monitoring Pipeline Components

### 7.4.3. Alerting Pipeline Components

### 7.4.4. Notification Pipeline Components
