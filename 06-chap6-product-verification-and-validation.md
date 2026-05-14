# Part II: Verification, Validation & Pipeline

# Capítulo VI: Product Verification & Validation

## 6.1. Testing Suites & Validation

### 6.1.1. Core Entities Unit Tests

En esta sección se detallan las pruebas unitarias realizadas sobre las entidades y agregados core del sistema Restock, asegurando la integridad de las reglas de negocio y la consistencia de los datos.

#### IAM (Identity and Access Management) Bounded Context Unit Tests

Se validaron las entidades `User` y `Role`, asegurando la correcta asignación de roles y la integridad de los datos de perfil de usuario.

![IAM Unit Tests Evidence](assets/images/chapter6/unit-test-evidence/iam-unit-tests.png)

#### Subscriptions Bounded Context Unit Tests

Se realizaron pruebas sobre el agregado `Subscription`, verificando la lógica de cambio de planes, estados de suscripción y fechas de vigencia.

![Subscriptions Unit Tests Evidence](assets/images/chapter6/unit-test-evidence/subscriptions-unit-tests.png)

#### Resource Bounded Context Unit Tests

Se validaron las entidades `Order` y `Alert`, incluyendo el cálculo de totales en pedidos, transiciones de estado y la generación correcta de alertas de inventario.

![Resource Unit Tests Evidence](assets/images/chapter6/unit-test-evidence/resource-unit-tests.png)

### 6.1.2. Core Integration Tests

Las pruebas de integración verifican que los módulos del sistema interactúen correctamente entre sí. Para ello se utilizó `@SpringBootTest`, que levanta el contexto completo de Spring Boot, y Flapdoodle Embedded MongoDB, que provee una instancia de base de datos en memoria durante la ejecución de los tests. Esto permite probar el flujo real desde la capa HTTP hasta la persistencia, sin depender de infraestructura externa.

Se implementaron tres clases de prueba que cubren las interacciones principales del sistema.
---

## Prueba 1 — Flujo de autenticación (IAM)

**Clase:** `AuthenticationIntegrationTest`

Valida la comunicación entre un cliente HTTP y los endpoints REST del módulo IAM. Cubre el ciclo completo de registro e inicio de sesión, incluyendo la generación del token JWT y el manejo de errores por credenciales inválidas o usuarios duplicados.

| Caso | Endpoint | Resultado esperado |
|---|---|---|
| Registro con credenciales válidas | `POST /api/v1/authentication/sign-up` | `201 Created` + datos del usuario |
| Registro con username duplicado | `POST /api/v1/authentication/sign-up` | `409 Conflict` |
| Inicio de sesión válido | `POST /api/v1/authentication/sign-in` | `200 OK` + token JWT |
| Contraseña incorrecta | `POST /api/v1/authentication/sign-in` | `401 Unauthorized` |
| Usuario inexistente | `POST /api/v1/authentication/sign-in` | `401 Unauthorized` |

![Ejecución de AuthenticationIntegrationTest con los 5 casos en verde](assets/images/chapter6/integration-test-evidence/AuthenticationIntegrationTest.png)

---

## Prueba 2 — Interacción entre contextos: Monitoring → Planning (ACL)

**Clase:** `ExternalPlanningServiceIntegrationTest`

Valida la capa Anti-Corruption Layer (ACL) entre los bounded contexts de **Monitoring** y **Planning**. El servicio `ExternalPlanningService` consume `PlanningContextFacade` para obtener datos de recetas sin acoplamiento directo entre contextos. Se verifica que la integración entre ambos contextos devuelva los datos correctos y maneje adecuadamente los identificadores inexistentes.

| Caso | Resultado esperado |
|---|---|
| Consultar receta con ID inexistente | `Optional.empty()` |
| Consultar receta existente por ID | `Optional` con el `RecipeId` correcto |
| Consultar precio de receta existente | Precio exacto registrado |
| Consultar precio con ID inexistente | `0.0` |

![Ejecución de ExternalPlanningServiceIntegrationTest con los 4 casos en verde](assets/images/chapter6/integration-test-evidence/ExternalPlanningServiceIntegrationTest.png)

---

## Prueba 3 — Endpoints de insumos (Resource)

**Clase:** `SupplyControllerIntegrationTest`

Valida los endpoints REST del contexto **Resource** para la consulta del catálogo de insumos. Al iniciar el contexto de prueba, el evento `ApplicationReadyEvent` ejecuta el seeding de insumos desde `supplies.json`, por lo que la base de datos embebida contiene datos reales al momento de ejecutar los casos.

| Caso | Endpoint | Resultado esperado |
|---|---|---|
| Consultar todos los insumos | `GET /api/v1/supplies` | `200 OK` + lista no vacía |
| Consultar insumo por ID válido | `GET /api/v1/supplies/1` | `200 OK` + datos del insumo |
| Consultar insumo con ID inexistente | `GET /api/v1/supplies/99999` | `404 Not Found` |
| Consultar categorías de insumos | `GET /api/v1/supplies/categories` | `200 OK` + lista de categorías |

![Ejecución de SupplyControllerIntegrationTest con los 4 casos en verde](assets/images/chapter6/integration-test-evidence/SupplyControllerIntegrationTest.png)



### 6.1.3. Core Behavior-Driven Development

### 6.1.4. Core System Tests

En esta sección se presentan las pruebas de sistema realizadas sobre Restock, con el objetivo de validar que los productos implementados funcionen correctamente como una solución integrada. Estas pruebas verifican flujos completos desde la perspectiva del usuario final, considerando navegación, autenticación, interacción con APIs, validación de formularios, persistencia de datos y respuesta del sistema ante escenarios exitosos y alternativos.

Para esta entrega, las pruebas de sistema se aplicaron sobre los principales productos de la solución: Landing Page, Web Application Angular desplegada en GitHub Pages, backend Spring Boot desplegado en Render, aplicación móvil Flutter para proveedores y aplicación móvil Kotlin para restaurantes.

### Testing Strategy

La estrategia de pruebas de sistema se definió según el tipo de producto evaluado. Para los productos web se utilizó Selenium IDE, debido a que permite grabar y reproducir flujos reales desde el navegador. Para el backend se utilizó Apache JMeter, con el fin de validar solicitudes HTTP hacia la API desplegada. Para las aplicaciones móviles se realizaron pruebas manuales documentadas en emulador o dispositivo Android. Finalmente, se realizó un flujo end-to-end cruzado para comprobar la comunicación entre restaurante, proveedor y backend.

| Producto              | Entorno                      | Herramienta               | Tipo de prueba         | Propósito                                                                                       |
| --------------------- | ---------------------------- | ------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------ |
| Landing Page          | GitHub Pages                 | Selenium IDE              | Smoke/System Web Test  | Validar carga, navegación, botones, enlaces y visualización responsive básica.                |
| Web Application       | GitHub Pages                 | Selenium IDE              | System UI Test         | Validar login, dashboard, navegación, inventario y formularios.                                 |
| Backend API           | Render                       | Apache JMeter             | System API Test        | Validar login, token JWT, endpoints protegidos, creación/consulta de datos y manejo de errores. |
| Supplier Mobile App   | Emulador/dispositivo Android | Prueba manual documentada | Mobile System Test     | Validar login, catálogo de productos, órdenes recibidas y cambio de estado.                    |
| Restaurant Mobile App | Emulador/dispositivo Android | Prueba manual documentada | Mobile System Test     | Validar login, inventario, ventas, pedidos y seguimiento de estados.                             |
| Flujo E2E cruzado     | Web + Mobile + API           | Video de ejecución       | End-to-End System Test | Validar el flujo restaurante → backend → proveedor → restaurante.                             |

### System Test Cases

| ID        | Producto              | Escenario                                         | Herramienta        | Resultado esperado                                                                                           | Estado |
| --------- | --------------------- | ------------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------ | ------ |
| ST-LP-01  | Landing Page          | Cargar la página pública                        | Selenium IDE       | El sitio carga correctamente y muestra la sección principal.                                                | Passed |
| ST-LP-02  | Landing Page          | Validar botones principales                       | Selenium IDE       | Los botones redirigen o desplazan al usuario hacia la sección esperada.                                     | Passed |
| ST-WEB-01 | Web Application       | Iniciar sesión como administrador de restaurante | Selenium IDE       | El usuario accede al dashboard correspondiente.                                                              | Passed |
| ST-WEB-02 | Web Application       | Navegar al módulo de inventario                  | Selenium IDE       | El sistema muestra el listado de insumos registrados.                                                        | Passed |
| ST-WEB-03 | Web Application       | Registrar insumo con datos válidos               | Selenium IDE       | El insumo se registra y aparece en el inventario.                                                            | Passed |
| ST-BE-01  | Backend API           | Iniciar sesión mediante API                      | JMeter             | La API retorna estado 200 OK y un token JWT.                                                                 | Passed |
| ST-BE-02  | Backend API           | Consultar recurso protegido con token             | JMeter             | La API retorna la información solicitada.                                                                   | Passed |
| ST-BE-03  | Backend API           | Crear un recurso válido                          | JMeter             | La API retorna 200 OK o 201 Created y persiste la información.                                              | Passed |
| ST-FL-01  | Supplier Mobile App   | Iniciar sesión como proveedor                    | Manual documentada | El proveedor accede a su pantalla principal.                                                                 | Passed |
| ST-FL-02  | Supplier Mobile App   | Gestionar catálogo de productos                  | Manual documentada | El producto se registra o actualiza correctamente.                                                           | Passed |
| ST-FL-03  | Supplier Mobile App   | Actualizar estado de una orden                    | Manual documentada | La orden cambia de estado correctamente.                                                                     | Passed |
| ST-KT-01  | Restaurant Mobile App | Iniciar sesión como usuario restaurante          | Manual documentada | El usuario accede a los módulos correspondientes a su rol.                                                  | Passed |
| ST-KT-02  | Restaurant Mobile App | Consultar inventario                              | Manual documentada | El sistema muestra insumos y niveles de stock.                                                               | Passed |
| ST-KT-03  | Restaurant Mobile App | Registrar order                                   | Manual documentada | La venta queda registrada y el stock se actualiza correctamente.                                             | Passed |
| ST-E2E-01 | Sistema completo      | Crear y seguir un pedido restaurante-proveedor    | Video E2E          | El restaurante crea el pedido, el proveedor lo visualiza, actualiza su estado y el restaurante ve el cambio. | Passed |

---

### Evidence

1. **Selenium IDE tests for Landing Page**

ST-LP-01: Se evidencia la ejecución del test de carga del Landing Page, validando que la página pública desplegada en GitHub Pages se abra correctamente y muestre el contenido principal del producto.

<img src="assets/images/chapter6/core-system-tests/landing-page/test1-load.png" width="600px" alt="selenium-landing-load-test">

ST-LP-02: Semuestra la ejecución del test sobre el botón principal del Landing Page, validando que el call-to-action funcione correctamente y redirija o desplace al usuario hacia la sección esperada.

<img src="assets/images/chapter6/core-system-tests/landing-page/test2-calltoaction.png" width="600px" alt="selenium-landing-call-to-action-test">

2. **Selenium IDE tests for Web Application**

ST-WEB-01: Se evidencia la ejecución del test de inicio de sesión en la Web Application, validando que el usuario pueda autenticarse correctamente y acceder al sistema.

<img src="assets/images/chapter6/core-system-tests/app-web/test1-sig-in.png" width="600px" alt="selenium-webapp-sign-in-test">

ST-WEB-02: Se muestra la ejecución del test de navegación dentro de la Web Application, validando que el usuario pueda acceder correctamente a los módulos principales del sistema.

<img src="assets/images/chapter6/core-system-tests/app-web/test2-navigate.png" width="600px" alt="selenium-webapp-navigation-test">

ST-WEB-03: Se evidencia la ejecución del test de registro de insumo desde la Web Application, validando que el sistema permita crear un nuevo recurso y mostrarlo correctamente en la interfaz.

<img src="assets/images/chapter6/core-system-tests/app-web/test3-create.png" width="600px" alt="selenium-webapp-create-supply-test">

3. **JMeter backend system tests**

ST-BE-01: Se evidencia la ejecución del request de login en JMeter, utilizado para validar la autenticación del usuario y la obtención del token JWT desde el backend desplegado en Render.

<img src="assets/images/chapter6/core-system-tests/backend/test1-login.png" width="600px" alt="jmeter-login-test">

ST-BE-02: Se muestra la ejecución del request GET para consultar insumos, validando que la API permita acceder a recursos protegidos cuando se envía un token válido.

<img src="assets/images/chapter6/core-system-tests/backend/test2-get-supplies.png" width="600px" alt="jmeter-get-supplies-test">

ST-BE-03: Se evidencia la ejecución del request POST para registrar un nuevo insumo, verificando que el backend procese correctamente datos válidos enviados desde JMeter.

<img src="assets/images/chapter6/core-system-tests/backend/test3-post.png" width="600px" alt="jmeter-post-supply-test">

Resumen de ejecución de las pruebas de sistema del backend, mostrando los resultados generales de los requests ejecutados, tiempos de respuesta y porcentaje de error.

<img src="assets/images/chapter6/core-system-tests/backend/tests-summary.png" width="600px" alt="jmeter-backend-tests-summary">

4. **Mobile system test evidence - (Kotlin, administradores de restaurantes)**

ST-KT-01: Se evidencia la pantalla inicial de autenticación en la aplicación móvil Kotlin, validando que el administrador de restaurante pueda acceder al flujo de inicio de sesión.

<img src="assets/images/chapter6/core-system-tests/mobile-kotlin-admin/test1-0-login.jpeg" height="350px"  alt="kotlin-restaurant-login-screen">

<img src="assets/images/chapter6/core-system-tests/mobile-kotlin-admin/test1-2-login.jpeg" height="350px" alt="kotlin-restaurant-successful-login">

ST-KT-02: Se evidencia la consulta del módulo de inventario desde la aplicación Kotlin, validando que el administrador pueda visualizar los insumos registrados y sus niveles de stock.

<img src="assets/images/chapter6/core-system-tests/mobile-kotlin-admin/test2-inventory.jpeg" height="350px"  alt="kotlin-restaurant-inventory-test">

ST-KT-03: Se muestra el inicio del flujo de creación de pedido desde la aplicación móvil Kotlin, validando que el administrador pueda seleccionar insumos para generar una orden.

<img src="assets/images/chapter6/core-system-tests/mobile-kotlin-admin/test3-0-create-order.jpeg" height="350px" alt="kotlin-restaurant-create-order-flow">

<img src="assets/images/chapter6/core-system-tests/mobile-kotlin-admin/test3-1-create-order.jpeg" height="350px"  alt="kotlin-restaurant-order-created">

5. **Mobile system test evidence - (Flutter, proveedores de insumos)**

ST-FL-01: Esta prueba valida que el proveedor pueda acceder correctamente a la aplicación móvil Flutter mediante credenciales válidas. El flujo inicia en la pantalla de autenticación y finaliza cuando el usuario ingresa a la interfaz principal del proveedor.

<img src="assets/images/chapter6/core-system-tests/mobile-flutter-supplier/test1-login.png" height="350px" alt="flutter-supplier-login-screen">

<img src="assets/images/chapter6/core-system-tests/mobile-flutter-supplier/test1-2-login.png" height="350px" alt="flutter-supplier-successful-login">

ST-FL-02: Esta prueba valida que el proveedor pueda acceder al módulo de inventario o catálogo de productos, visualizando correctamente los insumos registrados en la aplicación móvil.

<img src="assets/images/chapter6/core-system-tests/mobile-flutter-supplier/test2-inventory.png" height="350px" alt="flutter-supplier-inventory-list">

<img src="assets/images/chapter6/core-system-tests/mobile-flutter-supplier/test2-2-inventory.png" height="350px" alt="flutter-supplier-inventory-detail">

ST-FL-03: Esta prueba valida que el proveedor pueda acceder al módulo de órdenes, revisar los pedidos recibidos por parte de los restaurantes y consultar la información asociada a cada orden desde la aplicación móvil Flutter.

<img src="assets/images/chapter6/core-system-tests/mobile-flutter-supplier/test3-order.png" height="350px" alt="flutter-supplier-order-list">

<img src="assets/images/chapter6/core-system-tests/mobile-flutter-supplier/test3-2-order.png" height="350px" alt="flutter-supplier-order-detail">

<img src="assets/images/chapter6/core-system-tests/mobile-flutter-supplier/test3-3-order.png" height="350px" alt="flutter-supplier-order-management">

6. **Cross-platform E2E system test**

ST-E2E-01: Evidencia de flujo para gestion de inventario y pedidos restaurante-proveedor. Interacción entre landing page, aplicacion web, aplicación mobile Flutter, aplicación mobile Kotlin y backend.

<img src="assets/images/chapter6/core-system-tests/test-e2e.png" width="600px" alt="jmeter-backend-tests-summary">

Link del video: https://shorturl.at/btd62

### Resultados

Como resultado de las pruebas de sistema, se verificó que los productos principales de Restock funcionan de manera integrada. La Landing Page y la Web Application publicadas en GitHub Pages fueron evaluadas mediante Selenium IDE; el backend desplegado en Render fue validado mediante Apache JMeter; y las aplicaciones móviles Flutter y Kotlin fueron evaluadas mediante pruebas manuales documentadas.

Además, el flujo E2E cruzado permitió comprobar que una operación iniciada por el restaurante puede ser procesada por el backend, visualizada por el proveedor y actualizada nuevamente para el restaurante. Esto evidencia que Restock funciona como una solución integrada orientada a los principales flujos del negocio.

## 6.2. Static testing & Verification

### 6.2.1. Static Code Analysis

#### 6.2.1.1. Coding standard & Code conventions

#### 6.2.1.2. Code Quality & Code Security

### 6.2.2. Reviews

## 6.3. Validation Interviews

### 6.3.1. Diseño de Entrevistas

### 6.3.2. Registro de Entrevistas

### 6.3.3. Evaluaciones según heurísticas

## 6.4. Auditoría de Experiencias de Usuario

### 6.4.1. Auditoría realizada

#### 6.4.1.1. Información del grupo auditado

#### 6.4.1.2. Cronograma de auditoría realizada

#### 6.4.1.3. Contenido de auditoría realizada

### 6.4.2. Auditoría recibida

#### 6.4.2.1. Información del grupo auditor

#### 6.4.2.2. Cronograma de auditoría recibida

#### 6.4.2.3. Contenido de auditoría recibida

#### 6.4.2.4. Resumen de modificaciones para subsanar hallazgos
