# Capítulo VII: DevOps Practices

## 7.1. Continuous Integration

### 7.1.1. Tools and Practices


### 7.1.2. Build & Test Suite Pipeline Components

El flujo de Integración Continua para el backend REST de Restock se compone de etapas secuenciales que el orquestador (GitHub Actions) ejecuta de forma automatizada para validar la integridad del software. A continuación, se detalla el proceso de implementación y configuración de los componentes del pipeline:

#### 1. Gestión de Ramas y Entorno (Source & Environment Setup)
Para mantener la coherencia con el flujo de trabajo establecido (GitFlow), se creó una rama específica para la configuración de la integración continua denominada `feature/ci-pipeline-setup` a partir de la rama `develop`.

![Creación de la rama feature/ci-pipeline-setup en GitHub](assets/images/chapter7/continuous_integration/step1.png)

#### 2. Verificación de Versiones y Creación del Orquestador
Previo a la configuración del pipeline en la nube, se verificó la versión del Java Development Kit (JDK) utilizada localmente en el archivo `pom.xml`, confirmando el uso de Java 24. Con esta información, se procedió a crear el archivo orquestador `.github/workflows/ci-backend.yml` en la raíz del proyecto.

![Verificación de la versión de Java en el pom.xml](assets/images/chapter7/continuous_integration/step2_1.png)

Este archivo define los *triggers* (disparadores) para que el pipeline se ejecute automáticamente ante eventos de tipo `push` o `pull_request` dirigidos a las ramas principales, y declara los pasos de *Checkout* del código.

![Creación y primer commit del archivo ci-backend.yml](assets/images/chapter7/continuous_integration/step2_2.png)

#### 3. Configuración del Componente de Compilación (Build Component)
Para evitar discrepancias entre el entorno local y el servidor de CI, se actualizó el paso de configuración del entorno (`setup-java`) en el archivo YAML, forzando al *runner* a descargar e instalar explícitamente el JDK 24 (`java-version: '24'`). Esto garantiza que el `maven-compiler-plugin` compile el código fuente sin arrojar errores de versión no soportada.

![Actualización de la versión de JDK a 24 en el pipeline](assets/images/chapter7/continuous_integration/step4.png)

#### 4. Configuración del Entorno de Pruebas de Integración (Test Suite Component)
Dado que los *Core Integration Tests* dependen de una base de datos embebida utilizando **Flapdoodle**, se identificó la necesidad de definir explícitamente la versión de MongoDB a descargar en el entorno de pruebas automatizado para evitar fallos de carga en el `ApplicationContext` de Spring Boot.

Se implementó la solución creando el archivo de configuración `application-test.properties` dentro del directorio `src/test/resources/`, asignando la propiedad `de.flapdoodle.mongodb.embedded.version=7.0.2`. Esta acción estabilizó el entorno de ejecución en el servidor Linux de GitHub Actions.

![Configuración de la versión de Flapdoodle en application-test.properties](assets/images/chapter7/continuous_integration/step6.png)

#### 5. Ejecución y Validación del Pipeline
Una vez consolidados los componentes de construcción, resolución de dependencias (Maven) y el entorno de pruebas, los *commits* fueron integrados al repositorio. El orquestador de GitHub Actions ejecutó el flujo completo exitosamente (`exit code 0`), validando tanto los *Unit Tests* como los *Integration Tests*, y finalizando con el empaquetado del artefacto `.jar` listo para el despliegue continuo.

![Ejecución exitosa del pipeline de Integración Continua en Local](assets/images/chapter7/continuous_integration/step8.png)

![Ejecución exitosa del pipeline de Integración Continua en GitHub Actions](assets/images/chapter7/continuous_integration/step7.png)



## 7.2. Continuous Delivery

### 7.2.1. Tools and Practices

### 7.2.2. Stages Deployment Pipeline Components

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
