# Part II: Verification, Validation & Pipeline

# Capítulo VI: Product Verification & Validation

## 6.1. Testing Suites & Validation

### 6.1.1. Core Entities Unit Tests

### 6.1.2. Core Integration Tests

### 6.1.3. Core Behavior-Driven Development

## Introducción  
En esta sección se aplican técnicas de **Behavior-Driven Development (BDD)** para definir y validar el comportamiento esperado del sistema Restock desde la perspectiva del usuario.  
BDD permite crear una especificación ejecutable que sirve como documentación viva del sistema y como base para las pruebas automatizadas.  

Se utiliza **Gherkin** como lenguaje de especificación, estructurando los escenarios con el formato **Given-When-Then**, lo que facilita la comunicación entre el equipo técnico y los stakeholders del negocio.  

---

## Herramientas Utilizadas  
- **Gherkin:** Lenguaje para escribir especificaciones legibles por humanos  
- **Cucumber/SpecFlow:** Frameworks para ejecutar especificaciones BDD  
- **Formato:** Given-When-Then para describir comportamientos  

---

## Feature Files - Funcionalidades Core  

### Feature 1: Gestión de Inventario   

```gherkin
Feature: Gestión manual de inventario de insumos
  Como administrador de restaurante
  Quiero gestionar manualmente mi inventario de insumos
  Para mantener control preciso de las existencias y evitar faltantes

  Background:
    Given el usuario ha iniciado sesión como administrador
    And se encuentra en la sección de Inventario

  Scenario: Crear un nuevo insumo exitosamente
    Given no existe el insumo "Aceite de Oliva" en el sistema
    When el administrador completa el formulario con:

    --------------------------------
    | Campo      | Valor           |
    | Nombre     | Aceite de Oliva |
    | Categoría  | Aceites         |
    | Unidad     | Litros          |
    | Stock Min  | 5               |
    | Stock Max  | 20              |
    --------------------------------

    And hace clic en "Guardar"
    Then el sistema muestra el mensaje "Insumo creado exitosamente"
    And el insumo "Aceite de Oliva" aparece en la lista de inventario
    And el stock actual es 0


```
### Feature 2: Sistema de Alertas de Inventario

```Gherkin

Feature: Notificaciones automáticas de inventario
  Como administrador de restaurante
  Quiero recibir alertas sobre el estado de mi inventario
  Para tomar decisiones oportunas y evitar problemas operativos

  Background:
    Given el usuario ha iniciado sesión como administrador
    And tiene insumos registrados en el sistema

  Scenario: Alerta por stock bajo
    Given el insumo "Tomate" tiene:
      | Stock Actual | Stock Mínimo |
      | 3 kg         | 10 kg        |
    When el sistema ejecuta la verificación de inventario
    Then se genera una alerta de tipo "Stock Bajo"
    And la alerta muestra el mensaje "El stock de Tomate está por debajo del mínimo"
    And el insumo se resalta en color naranja en el dashboard

```
### Feature 3: Gestión de Recetas

```Gherkin
Feature: Creación y gestión de recetas vinculadas al inventario
  Como administrador de restaurante
  Quiero crear recetas con ingredientes específicos
  Para calcular costos y controlar el consumo de insumos

  Background:
    Given el usuario ha iniciado sesión como administrador
    And tiene insumos registrados en el inventario
    And se encuentra en la sección de Recetas

  Scenario: Crear una receta nueva
    Given no existe la receta "Lomo Saltado"
    When el administrador completa el formulario:
      | Campo       | Valor                |
      | Nombre      | Lomo Saltado         |
      | Descripción | Plato criollo peruano|
      | Porciones   | 4                    |
      | Precio      | 35.00                |
    And agrega los siguientes ingredientes:
      | Ingrediente | Cantidad | Unidad |
      | Lomo        | 500      | g      |
      | Cebolla     | 200      | g      |
      | Tomate      | 150      | g      |
      | Papas       | 400      | g      |
      | Arroz       | 300      | g      |
    And guarda la receta
    Then el sistema calcula el costo total de ingredientes
    And muestra "Receta creada exitosamente"
    And la receta aparece en el catálogo

```

### Feature 4: Gestión de Pedidos a Proveedores


```Gherkin

Feature: Solicitud y seguimiento de pedidos a proveedores
  Como administrador de restaurante
  Quiero realizar y hacer seguimiento de pedidos
  Para mantener abastecido mi inventario de manera eficiente

  Background:
    Given el usuario ha iniciado sesión como administrador
    And tiene proveedores registrados en el sistema

  Scenario: Crear un pedido a proveedor
    Given el proveedor "Distribuidora Don José" ofrece:
      | Producto | Precio Unitario |
      | Arroz    | 3.50 / kg       |
      | Azúcar   | 2.80 / kg       |
      | Sal      | 1.20 / kg       |
    When el administrador crea un nuevo pedido
    And selecciona el proveedor "Distribuidora Don José"
    And agrega los productos:
      | Producto | Cantidad |
      | Arroz    | 50 kg    |
      | Azúcar   | 25 kg    |
    And confirma el pedido
    Then el sistema calcula el total: S/. 245.00
    And envía la orden al proveedor
    And el estado del pedido es "Pendiente"

```
### Feature 5: Registro de Ventas

```Gherkin

Feature: Registro de ventas del restaurante
  Como empleado del restaurante
  Quiero registrar las ventas realizadas
  Para actualizar el inventario y generar reportes precisos

  Background:
    Given el usuario ha iniciado sesión como empleado
    And tiene acceso al módulo de ventas
    And existen recetas registradas en el sistema

  Scenario: Registrar venta con recetas del menú
    Given el cliente ordena:
      | Plato        | Cantidad |
      | Lomo Saltado | 2        |
      | Ceviche      | 1        |
    When el empleado registra la venta
    Then el sistema calcula el total: S/. 105.00
    And descuenta los ingredientes de las recetas del inventario
    And registra la venta con fecha y hora actuales
    And genera un ID único de venta

```
### Feature 6: Gestión de Suscripción

```Gherkin

Feature: Gestión de planes de suscripción
  Como suscriptor
  Quiero administrar mi plan de suscripción
  Para acceder a las funcionalidades según mis necesidades

  Background:
    Given el usuario ha iniciado sesión
    And accede a la sección de Suscripción

  Scenario: Visualizar plan actual y características
    Given el usuario tiene el plan "Profesional"
    When accede a "Mi Suscripción"
    Then visualiza:
      | Información               |
      | Nombre del plan           |
      | Precio mensual            |
      | Fecha de inicio           |
      | Próxima fecha de renovación |
      | Funcionalidades incluidas |
      | Límites de uso            |


```

### Feature 7: Gestión de Proveedores

```Gherkin

Feature: Administración de proveedores
  Como administrador de restaurante
  Quiero gestionar mi red de proveedores
  Para mantener relaciones comerciales organizadas y eficientes

  Background:
    Given el usuario ha iniciado sesión como administrador
    And accede a la sección de Proveedores

  Scenario: Registrar un nuevo proveedor
    Given no existe el proveedor "Mercado Fresh SAC"
    When el administrador completa el formulario:
      | Campo              | Valor                    |
      | Nombre comercial   | Mercado Fresh SAC        |
      | RUC                | 20601234567              |
      | Contacto           | Juan Pérez               |
      | Teléfono           | +51 987654321            |
      | Email              | ventas@mercadofresh.com  |
      | Dirección          | Av. Industrial 456, Lima |
      | Categoría          | Frutas y Verduras        |
    And hace clic en "Registrar Proveedor"
    Then el sistema muestra "Proveedor registrado exitosamente"
    And el proveedor aparece en la lista de proveedores activos
    And se envía email de bienvenida al proveedor

```

### Feature 8: Reportes y Analíticas

```Gherik

Feature: Generación de reportes e indicadores
  Como administrador de restaurante
  Quiero generar reportes del sistema
  Para analizar el desempeño y tomar decisiones informadas

  Background:
    Given el usuario ha iniciado sesión como administrador
    And accede a la sección de Reportes

  Scenario: Generar reporte de ventas mensual
    Given existen ventas registradas en el mes de abril 2026
    When el administrador selecciona "Reporte de Ventas"
    And elige el período "Abril 2026"
    And hace clic en "Generar Reporte"
    Then el sistema muestra:
      | Métrica                  |
      | Total de ventas          |
      | Número de transacciones  |
      | Ticket promedio          |
      | Plato más vendido        |
      | Día con más ventas       |
    And puede exportar en formato Excel o PDF

```

### Feature 9: Notificaciones Push

```Gherik
Feature: Sistema de notificaciones en tiempo real
  Como usuario del sistema
  Quiero recibir notificaciones relevantes
  Para estar informado de eventos importantes sin consultar constantemente

  Background:
    Given el usuario ha iniciado sesión
    And tiene notificaciones habilitadas

  Scenario: Recibir notificación de stock crítico
    Given un insumo "Sal" alcanza el stock mínimo
    When el sistema detecta la condición
    Then se envía notificación push al administrador
    And la notificación muestra "⚠️ Stock crítico: Sal - 2 kg restantes"
    And aparece en el centro de notificaciones de la app
    And se marca como "No leída"

  Scenario: Notificación de pedido recibido (para proveedor)
    Given un restaurante crea un pedido al proveedor
    When el pedido se confirma en el sistema
    Then el proveedor recibe notificación push
    And el mensaje indica "📦 Nuevo pedido de Restaurante XYZ - S/. 450.00"
    And puede acceder directamente al detalle del pedido

  Scenario: Alerta de producto próximo a vencer
    Given un lote de "Yogurt" vence en 2 días
    When el sistema ejecuta la verificación diaria
    Then se notifica al administrador
    And el mensaje dice "⏰ Yogurt vence en 2 días - 15 unidades"
    And sugiere crear promoción o descuento

  Scenario: Confirmar recepción de notificación
    Given el usuario tiene 5 notificaciones no leídas
    When abre el centro de notificaciones
    And visualiza las alertas
    Then puede marcar individualmente como leídas
    Or marcar todas como leídas con un solo clic

  Scenario: Configurar preferencias de notificaciones
    Given el usuario accede a Configuración
    When selecciona "Notificaciones"
    Then puede activar/desactivar:
      | Tipo de Notificación        |
      | Stock bajo                  |
      | Productos por vencer        |
      | Nuevos pedidos              |
      | Cambios de estado de pedido |
      | Reportes programados        |
    And guardar sus preferencias


```
### Feature 10: Autenticación y Seguridad



```Gherkin

Feature: Gestión de autenticación y seguridad
  Como usuario del sistema
  Quiero gestionar mi acceso de forma segura
  Para proteger la información de mi negocio

  Scenario: Inicio de sesión exitoso
    Given el usuario tiene credenciales válidas
    When ingresa email "admin@restaurante.com"
    And ingresa contraseña correcta
    And hace clic en "Iniciar Sesión"
    Then accede al dashboard del sistema
    And se registra la fecha y hora del acceso
    And se muestra mensaje "Bienvenido de nuevo, [Nombre]"

  Scenario: Intento de inicio de sesión con credenciales incorrectas
    Given el usuario ingresa email válido
    When ingresa contraseña incorrecta
    And hace clic en "Iniciar Sesión"
    Then el sistema muestra "Email o contraseña incorrectos"
    And no permite el acceso
    And registra el intento fallido

  Scenario: Bloqueo de cuenta por múltiples intentos fallidos
    Given un usuario ha intentado 5 veces con contraseña incorrecta
    When intenta ingresar por sexta vez
    Then el sistema bloquea la cuenta temporalmente por 15 minutos
    And muestra "Cuenta bloqueada por seguridad. Intente más tarde o recupere su contraseña"
    And envía email de alerta al propietario

  Scenario: Recuperación de contraseña
    Given el usuario olvidó su contraseña
    When selecciona "¿Olvidaste tu contraseña?"
    And ingresa su email registrado
    And hace clic en "Enviar enlace de recuperación"
    Then recibe email con enlace temporal
    And el enlace expira en 1 hora
    And puede crear nueva contraseña desde el enlace

  Scenario: Cambiar contraseña desde configuración
    Given el usuario ha iniciado sesión
    When accede a "Seguridad y Privacidad"
    And selecciona "Cambiar Contraseña"
    And ingresa:
      | Campo                  | Valor          |
      | Contraseña actual      | [contraseña]   |
      | Nueva contraseña       | [nueva]        |
      | Confirmar contraseña   | [nueva]        |
    And hace clic en "Actualizar"
    Then el sistema valida la contraseña actual
    And actualiza a la nueva contraseña
    And muestra "Contraseña actualizada exitosamente"

  Scenario: Cerrar sesión de forma segura
    Given el usuario ha terminado su trabajo
    When selecciona "Cerrar Sesión"
    Then el sistema invalida el token de sesión
    And redirige a la página de inicio de sesión
    And limpia datos sensibles del navegador


```

### Feature 11: Perfil de Usuario

```Gherkin


gherkin
Feature: Gestión de perfil personal y empresarial
  Como usuario registrado
  Quiero gestionar mi información de perfil
  Para mantener mis datos actualizados y personalizados

  Background:
    Given el usuario ha iniciado sesión
    And accede a la sección "Mi Perfil"

  Scenario: Actualizar información personal
    When el usuario edita los siguientes campos:
      | Campo           | Valor Nuevo         |
      | Nombre          | Carlos              |
      | Apellido        | Rodríguez           |
      | Teléfono        | +51 999888777       |
      | País            | Perú                |
    And hace clic en "Guardar Cambios"
    Then el sistema actualiza la información
    And muestra "Perfil actualizado correctamente"

  Scenario: Cargar foto de perfil
    When el usuario selecciona "Cambiar Foto"
    And carga una imagen válida (JPG/PNG, <5MB)
    Then el sistema sube la imagen a Cloudinary
    And actualiza la foto de perfil
    And la nueva imagen se refleja en toda la aplicación

  Scenario: Actualizar datos empresariales (restaurante)
    Given el usuario es administrador de restaurante
    When accede a "Datos del Negocio"
    And actualiza:
      | Campo                 | Valor                |
      | Nombre del restaurante| El Buen Sabor        |
      | RUC                   | 20501234567          |
      | Dirección             | Jr. Lima 123, Lima   |
      | Categoría             | Comida Criolla       |
    And guarda los cambios
    Then la información se actualiza en el sistema
    And aparece en facturas y documentos oficiales

  Scenario: Visualizar estadísticas del perfil
    When el usuario accede a su perfil
    Then visualiza métricas como:
      | Métrica                    |
      | Fecha de registro          |
      | Último acceso              |
      | Número de ventas (si admin)|
      | Pedidos completados        |
      | Calificación promedio      |

  Scenario: Desactivar cuenta
    Given el usuario desea desactivar su cuenta
    When selecciona "Desactivar Cuenta"
    And confirma con su contraseña
    And acepta los términos de desactivación
    Then la cuenta se marca como inactiva
    And los datos se conservan por 30 días
    And puede reactivar dentro de ese período



```

### Feature 12: Gestión de Roles y Permisos

```Gherkin
Feature: Control de acceso basado en roles
  Como administrador del sistema
  Quiero gestionar roles y permisos
  Para controlar el acceso a funcionalidades según el tipo de usuario

  Background:
    Given el usuario ha iniciado sesión como administrador principal

  Scenario: Asignar rol a un nuevo usuario
    Given se ha registrado un nuevo usuario "empleado@restaurante.com"
    When el administrador accede a "Gestión de Usuarios"
    And selecciona el usuario
    And asigna el rol "Empleado - Ventas"
    Then el usuario solo tiene acceso a:
      | Módulo permitido    |
      | Registro de Ventas  |
      | Ver Recetas         |
      | Consultar Stock     |
    And no puede acceder a:
      | Módulo restringido       |
      | Gestión de Proveedores   |
      | Configuración            |
      | Reportes Financieros     |

  Scenario: Crear rol personalizado
    When el administrador crea un nuevo rol "Jefe de Cocina"
    And configura permisos:
      | Módulo              | Permiso          |
      | Inventario          | Lectura/Escritura|
      | Recetas             | Lectura/Escritura|
      | Proveedores         | Solo Lectura     |
      | Ventas              | Solo Lectura     |
      | Reportes            | Denegado         |
    And guarda el rol
    Then queda disponible para asignar a usuarios
    And aparece en la lista de roles del sistema

  Scenario: Modificar permisos de un rol existente
    Given existe el rol "Empleado - Ventas"
    When el administrador edita el rol
    And agrega permiso de "Lectura" en "Recetas"
    And guarda los cambios
    Then todos los usuarios con ese rol obtienen el nuevo permiso
    And se registra el cambio en el log de auditoría

  Scenario: Intentar acceder a módulo sin permisos
    Given un usuario tiene rol "Empleado - Ventas"
    When intenta acceder a "Gestión de Proveedores"
    Then el sistema muestra "No tienes permisos para acceder a esta sección"
    And redirige al dashboard
    And registra el intento en el log de seguridad
```

 #### 6.1.3.1. Estructura de Archivos

```bash

features/
├── inventory/
│   ├── inventory_management.feature
│   ├── inventory_alerts.feature
│   └── step_definitions/
│       ├── inventory_steps.ts
│       └── alerts_steps.ts
├── recipes/
│   ├── recipe_management.feature
│   └── step_definitions/
│       └── recipe_steps.ts
├── orders/
│   ├── supplier_orders.feature
│   └── step_definitions/
│       └── orders_steps.ts
├── sales/
│   ├── sales_registration.feature
│   └── step_definitions/
│       └── sales_steps.ts
├── subscriptions/
│   ├── subscription_management.feature
│   └── step_definitions/
│       └── subscription_steps.ts
├── suppliers/
│   ├── supplier_management.feature
│   └── step_definitions/
│       └── supplier_steps.ts
├── reports/
│   ├── reports_analytics.feature
│   └── step_definitions/
│       └── reports_steps.ts
├── notifications/
│   ├── push_notifications.feature
│   └── step_definitions/
│       └── notifications_steps.ts
├── authentication/
│   ├── auth_security.feature
│   └── step_definitions/
│       └── auth_steps.ts
├── profile/
│   ├── user_profile.feature
│   └── step_definitions/
│       └── profile_steps.ts
└── permissions/
    ├── roles_permissions.feature
    └── step_definitions/
        └── permissions_steps.ts
```

#### 6.1.3.2. Ejemplo de Step Definitions (TypeScript + Cucumber)

```typescript
// inventory_steps.ts
import { Given, When, Then } from '@cucumber/cucumber';
import { expect } from 'chai';

Given('el usuario ha iniciado sesión como administrador', async function() {
  await this.loginPage.login('admin@restaurant.com', 'password');
  expect(await this.dashboardPage.isDisplayed()).to.be.true;
});

When('el administrador completa el formulario con:', async function(dataTable) {
  const data = dataTable.rowsHash();
  await this.inventoryPage.fillSupplyForm(data);
});

Then('el sistema muestra el mensaje {string}', async function(message) {
  const actualMessage = await this.notificationComponent.getMessage();
  expect(actualMessage).to.equal(message);
});

```

#### 6.1.3.2.3. Integración con CI/CD

```yaml
name: BDD Tests

on: [push, pull_request]

jobs:
  bdd-tests:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        feature: 
          - inventory
          - recipes
          - orders
          - sales
          - subscriptions
          - suppliers
          - reports
          - notifications
          - authentication
          - profile
          - permissions
    
    steps:
      - uses: actions/checkout@v2
      
      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '18'




```

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
