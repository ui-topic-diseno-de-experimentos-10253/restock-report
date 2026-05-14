# Part II: Verification, Validation & Pipeline

# Capítulo VI: Product Verification & Validation

## 6.1. Testing Suites & Validation

### 6.1.1. Core Entities Unit Tests

### 6.1.2. Core Integration Tests

### 6.1.3. Core Behavior-Driven Development

### 6.1.4. Core System Tests

En esta sección se presentan las pruebas de sistema realizadas sobre Restock, con el objetivo de validar que los productos implementados funcionen correctamente como una solución integrada. Estas pruebas verifican flujos completos desde la perspectiva del usuario final, considerando navegación, autenticación, interacción con APIs, validación de formularios, persistencia de datos y respuesta del sistema ante escenarios exitosos y alternativos.

Para esta entrega, las pruebas de sistema se aplicaron sobre los principales productos de la solución: Landing Page, Web Application Angular desplegada en GitHub Pages, backend Spring Boot desplegado en Render, aplicación móvil Flutter para proveedores y aplicación móvil Kotlin para restaurantes.

### Testing Strategy

La estrategia de pruebas de sistema se definió según el tipo de producto evaluado. Para los productos web se utilizó Selenium IDE, debido a que permite grabar y reproducir flujos reales desde el navegador. Para el backend se utilizó Apache JMeter, con el fin de validar solicitudes HTTP hacia la API desplegada. Para las aplicaciones móviles se realizaron pruebas manuales documentadas en emulador o dispositivo Android. Finalmente, se realizó un flujo end-to-end cruzado para comprobar la comunicación entre restaurante, proveedor y backend.

| Producto              | Entorno                      | Herramienta               | Tipo de prueba         | Propósito                                                                                       |
| --------------------- | ---------------------------- | ------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------ |
| Landing Page          | GitHub Pages                 | Playwright                | Smoke/System Web Test  | Validar carga, navegación, botones, enlaces y visualización responsive básica.                |
| Web Application       | GitHub Pages                 | Playwright                | System UI Test         | Validar login, dashboard, navegación, inventario y formularios.                                 |
| Backend API           | Render                       | Apache JMeter             | System API Test        | Validar login, token JWT, endpoints protegidos, creación/consulta de datos y manejo de errores. |
| Supplier Mobile App   | Emulador/dispositivo Android | Prueba manual documentada | Mobile System Test     | Validar login, catálogo de productos, órdenes recibidas y cambio de estado.                    |
| Restaurant Mobile App | Emulador/dispositivo Android | Prueba manual documentada | Mobile System Test     | Validar login, inventario, ventas, pedidos y seguimiento de estados.                             |
| Flujo E2E cruzado     | Web + Mobile + API           | Video de ejecución       | End-to-End System Test | Validar el flujo restaurante → backend → proveedor → restaurante.                             |

> **Evidencia a insertar:**
> Colocar una captura general de los entornos utilizados: Landing Page en GitHub Pages, Web App en GitHub Pages, backend activo en Render y aplicaciones móviles ejecutándose en emulador o dispositivo.
>
> **Figura 6.X. Entornos utilizados para las pruebas de sistema.**
> `![Figura 6.X. Entornos utilizados para las pruebas de sistema](assets/core-system-tests/environments.png)`

---

### System Test Cases

| ID        | Producto              | Escenario                                         | Herramienta        | Resultado esperado                                                                                           | Estado                     |
| --------- | --------------------- | ------------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------ | -------------------------- |
| ST-LP-01  | Landing Page          | Cargar la página pública                        | Selenium IDE       | El sitio carga correctamente y muestra la sección principal.                                                | Passed / Observed / Failed |
| ST-LP-02  | Landing Page          | Navegar entre secciones principales               | Selenium IDE       | Las secciones se muestran correctamente y los enlaces funcionan.                                             | Passed / Observed / Failed |
| ST-LP-03  | Landing Page          | Validar botones principales                       | Selenium IDE       | Los botones redirigen o desplazan al usuario hacia la sección esperada.                                     | Passed / Observed / Failed |
| ST-WEB-01 | Web Application       | Iniciar sesión como administrador de restaurante | Selenium IDE       | El usuario accede al dashboard correspondiente.                                                              | Passed / Observed / Failed |
| ST-WEB-02 | Web Application       | Navegar al módulo de inventario                  | Selenium IDE       | El sistema muestra el listado de insumos registrados.                                                        | Passed / Observed / Failed |
| ST-WEB-03 | Web Application       | Registrar insumo con datos válidos               | Selenium IDE       | El insumo se registra y aparece en el inventario.                                                            | Passed / Observed / Failed |
| ST-WEB-04 | Web Application       | Registrar insumo con datos inválidos             | Selenium IDE       | El sistema muestra mensajes de validación y evita el registro.                                              | Passed / Observed / Failed |
| ST-BE-01  | Backend API           | Iniciar sesión mediante API                      | JMeter             | La API retorna estado 200 OK y un token JWT.                                                                 | Passed / Observed / Failed |
| ST-BE-02  | Backend API           | Consultar recurso protegido con token             | JMeter             | La API retorna la información solicitada.                                                                   | Passed / Observed / Failed |
| ST-BE-03  | Backend API           | Crear un recurso válido                          | JMeter             | La API retorna 200 OK o 201 Created y persiste la información.                                              | Passed / Observed / Failed |
| ST-FL-01  | Supplier Mobile App   | Iniciar sesión como proveedor                    | Manual documentada | El proveedor accede a su pantalla principal.                                                                 | Passed / Observed / Failed |
| ST-FL-02  | Supplier Mobile App   | Gestionar catálogo de productos                  | Manual documentada | El producto se registra o actualiza correctamente.                                                           | Passed / Observed / Failed |
| ST-FL-03  | Supplier Mobile App   | Actualizar estado de una orden                    | Manual documentada | La orden cambia de estado correctamente.                                                                     | Passed / Observed / Failed |
| ST-KT-01  | Restaurant Mobile App | Iniciar sesión como usuario restaurante          | Manual documentada | El usuario accede a los módulos correspondientes a su rol.                                                  | Passed / Observed / Failed |
| ST-KT-02  | Restaurant Mobile App | Consultar inventario                              | Manual documentada | El sistema muestra insumos y niveles de stock.                                                               | Passed / Observed / Failed |
| ST-KT-03  | Restaurant Mobile App | Registrar venta y actualizar inventario           | Manual documentada | La venta queda registrada y el stock se actualiza correctamente.                                             | Passed / Observed / Failed |
| ST-E2E-01 | Sistema completo      | Crear y seguir un pedido restaurante-proveedor    | Video E2E          | El restaurante crea el pedido, el proveedor lo visualiza, actualiza su estado y el restaurante ve el cambio. | Passed / Observed / Failed |

---

### Evidence

Las evidencias de las pruebas de sistema se organizaron mediante capturas de pantalla y videos cortos. Para Selenium IDE se consideraron capturas de los comandos grabados y de la ejecución exitosa. Para JMeter se consideraron capturas del Test Plan, View Results Tree y Summary Report. Para las aplicaciones móviles se consideraron capturas del emulador o dispositivo físico. Para el flujo E2E se consideró un video corto del flujo completo.

| Evidencia                    | Descripción                                              |
| ---------------------------- | --------------------------------------------------------- |
| Landing Page en GitHub Pages | Captura del sitio público cargado correctamente.         |
| Playwright - Landing Page    | Captura de tests grabados y ejecución exitosa.           |
| Playwright - Web App        | Captura de tests de login, navegación e inventario.      |
| JMeter Test Plan             | Captura de los requests configurados para la API.         |
| JMeter View Results Tree     | Captura de respuestas exitosas y errores controlados.     |
| JMeter Summary Report        | Captura del resumen de ejecución de las pruebas API.     |
| Flutter Supplier App         | Capturas de login, catálogo y órdenes.                  |
| Kotlin Restaurant App        | Capturas de login, inventario, ventas o pedidos.          |
| Video E2E                    | Grabación del flujo restaurante → proveedor → backend. |

> **Figura 6.X. Selenium IDE tests for Landing Page and Web Application.**
> `![Figura 6.X. Selenium IDE tests for Landing Page and Web Application](assets/core-system-tests/selenium-tests.png)`
>
> **Figura 6.X. JMeter backend system tests.**
> `![Figura 6.X. JMeter backend system tests](assets/core-system-tests/jmeter-tests.png)`
>
> **Figura 6.X. Mobile system test evidence.**
> `![Figura 6.X. Mobile system test evidence](assets/core-system-tests/mobile-tests.png)`
>
> **Video 6.X. Cross-platform E2E system test.**
> URL del video: `<insertar enlace del video>`

---

### Cross-platform E2E Test

La prueba E2E cruzada permitió validar el flujo principal entre restaurante y proveedor. En este escenario, el restaurante genera un pedido de insumos, el backend registra la operación, el proveedor visualiza la orden recibida, actualiza su estado y el restaurante consulta el cambio realizado.

| Paso | Producto             | Acción                                            | Resultado esperado                               |
| ---- | -------------------- | -------------------------------------------------- | ------------------------------------------------ |
| 1    | Web App o Kotlin App | El administrador de restaurante inicia sesión.    | El sistema muestra el panel del restaurante.     |
| 2    | Web App o Kotlin App | El administrador crea un pedido de insumos.        | El pedido queda registrado con estado pendiente. |
| 3    | Backend API          | Se consulta la orden creada.                       | La API retorna la orden registrada.              |
| 4    | Flutter Supplier App | El proveedor inicia sesión y revisa sus órdenes. | La orden aparece en la lista del proveedor.      |
| 5    | Flutter Supplier App | El proveedor cambia el estado del pedido.          | El sistema actualiza el estado de la orden.      |
| 6    | Web App o Kotlin App | El restaurante consulta el pedido.                 | El restaurante visualiza el estado actualizado.  |

---

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
