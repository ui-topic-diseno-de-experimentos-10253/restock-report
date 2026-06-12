# Part III: Experiment-Driven Lifecycle

# Capítulo VIII: Experiment-Driven Development

## 8.1. Experiment Planning

En esta sección se define la planificación de experimentos como punto de partida del enfoque  Experiment-Driven Development . Su objetivo es identificar qué se conoce actualmente, qué dudas existen y qué supuestos deben validarse antes de tomar decisiones sobre el producto. Para ello, se organiza la información en preguntas, brechas de conocimiento, ideas y tarjetas de experimento, permitiendo priorizar aprendizajes clave y reducir riesgos durante el desarrollo.

### 8.1.1. As-Is Summary

Hasta este punto, el proyecto Restock ha culminado la fase de diseño e implementación técnica, consolidando un ecosistema digital funcional que comprende una Landing Page, una aplicación web de gestión administrativa, aplicaciones móviles (Nativa y Flutter) y una arquitectura de servicios basada en una API RESTful con persistencia en MongoDB.

A pesar de contar con una solución "To-Be" ya construida, el estado actual de nuestro conocimiento se caracteriza por una **incertidumbre operativa**. Actualmente, el éxito de la plataforma depende de premisas críticas (como la capacidad de las alertas automáticas para reducir la merma en un 35%) que hasta el momento son suposiciones basadas en la sabiduría de la industria y no en datos quirúrgicos recolectados del comportamiento real de los usuarios.

Este resumen establece que el punto de partida de la fase actual no es la generación de nuevas soluciones técnicas, sino la recolección de material bruto (suposiciones, vacíos de conocimiento, ideas y afirmaciones) para transformar nuestras creencias en preguntas de investigación. El objetivo primordial es validar si las funcionalidades ya implementadas realmente generan el impacto social y económico previsto para los administradores y proveedores de restaurantes en Lima, antes de proceder con el lanzamiento final.

### 8.1.3. Experiment-Ready Questions

### 8.1.4. Question Backlog

Siguiendo la metodología XDPD, se transformaron las premisas e incertidumbres en un backlog de preguntas de investigación en lugar de una lista de funcionalidades. Este enfoque permite priorizar el aprendizaje y mitigar los riesgos más altos del proyecto Restock antes de consolidar la solución técnica final.

**Estructura del Backlog**

Se opta por un backlog amplio (broad) para esta fase inicial, con el objetivo de sondear diferentes áreas críticas: la adopción del usuario, la viabilidad del ecosistema de proveedores y la efectividad real de la automatización en la reducción de mermas.

**Sistema de Puntuación y Priorización**

Cada pregunta ha sido evaluada bajo cuatro criterios en una escala del 1 al 5 (donde 5 es el valor máximo): **Confianza (C)**, **Riesgo (R)**, **Impacto (I)** e **Interés (Int)**. En cumplimiento con el marco de trabajo, en caso de empate en el puntaje total, se ha priorizado la pregunta con mayor índice de Riesgo.

| ID | Pregunta de Investigación (Question)                                                                      | Motivación (The "Why")                                                                                                                | C | R | I | Int | Total |
| -- | ---------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | - | - | - | --- | ----- |
| Q1 | ¿Reducen las alertas en tiempo real el desperdicio de insumos en un 35% como se ha previsto?              | Validar la propuesta de valor core. Si la automatización no impacta la merma, el beneficio económico para el restaurante desaparece. | 2 | 5 | 5 | 5   | 17    |
| Q2 | ¿Son capaces los administradores con baja afinidad digital de completar un pedido sin asistencia externa? | Mitigar el riesgo de adopción. El mayor riesgo identificado es que la complejidad de la UI aleje al usuario tradicional.             | 3 | 5 | 4 | 4   | 16    |
| Q3 | ¿Están los proveedores tradicionales dispuestos a digitalizar sus catálogos para integrarse a Restock?  | Asegurar la viabilidad del ecosistema. El sistema depende de que el proveedor alimente los datos de stock y precios.                   | 2 | 4 | 4 | 5   | 15    |
| Q4 | ¿Influye la visualización de métricas de rotación en la decisión de compra de nuevos insumos?         | Validar el cambio de comportamiento. Queremos saber si el usuario toma decisiones basadas en datos o sigue usando su intuición.       | 4 | 2 | 3 | 4   | 13    |

### 8.1.5. Experiment Cards

La Tarjeta de Experimento es el artefacto clave que sustenta el proceso XDPD y sirve como contrato de aprendizaje para el equipo. Estas tarjetas permiten capturar la información esencial antes de la ejecución, asegurando que cada intervención en el producto Restock tenga un propósito claro y una forma objetiva de medir el éxito o fracaso.

**Tarjeta de Experimento 01: Validación de Impacto en Mermas**

Esta tarjeta aborda la premisa principal de negocio: la capacidad de la automatización para generar ahorros reales.

| LADO FRONTAL: Concepto y Motivación                                                                                                                                                                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Pregunta:** ¿Reducen las alertas automáticas de "stock bajo" y "vencimiento" el desperdicio de insumos perecibles en un 35%?                                                                                                                                                                            |
| **Por qué:** Si la automatización no genera una reducción tangible en la merma, la propuesta de valor económica de Restock para el dueño del restaurante desaparece.                                                                                                                                    |
| **Hipótesis:** Creemos que al ofrecer notificaciones push automáticas, los administradores realizarán pedidos preventivos, cuya evidencia se reflejará en una disminución del 35% en los reportes de mermas, bajo la circunstancia de uso diario por dueños de restaurantes medianos.                  |
| **Qué (Simplest Useful Thing):** Ejecución de un piloto operativo utilizando la aplicación móvil nativa (Kotlin) ya implementada, activando el módulo de notificaciones automáticas mediante OneSignal para enviar alertas reales de inventario a los dispositivos de 5 administradores seleccionados. |

| LADO POSTERIOR: Configuración Técnica                                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Medidas:**<br />• Métrica Principal: Reducción porcentual de mermas registradas por semana.<br />• Métrica Secundaria: Tasa de conversión de alerta (clic en notificación) a creación de orden de compra.                                                                      |
| **Condiciones:**<br />• Experimental: 5 administradores usando el sistema de alertas activas.<br />• Control: 5 administradores usando su método manual actual (Excel/WhatsApp).                                                                                                      |
| **Escala:**<br />• Certeza: Nivel de significancia del 5% y potencia estadística del 80%.<br />• MDE (Efecto Mínimo): Se busca detectar una diferencia mínima del 10% en el volumen de desperdicio.<br />• Tiempo: El experimento durará 14 días (dos ciclos de abastecimiento). |

**Tarjeta de Experimento 02: Validación de Adopción Digital**

Esta tarjeta mitiga el riesgo técnico y de usuario identificado en el segmento de administradores tradicionales.

| LADO FRONTAL: Concepto y Motivación                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pregunta:** ¿Son capaces los administradores con baja afinidad digital de completar su primer pedido de insumos de forma autónoma?                                                                                                                            |
| **Por qué:** El mayor riesgo de abandono de la plataforma es la fricción inicial; si el proceso es complejo, el usuario no regresará.                                                                                                                      |
| **Hipótesis:** Creemos que con un onboarding guiado simplificado, los usuarios nuevos completarán su pedido en menos de 5 minutos, cuya evidencia se verá en el éxito de la tarea, bajo la circunstancia de uso por primera vez sin capacitación previa. |
| **Qué (Simplest Useful Thing):** Una sesión de prueba de usuario remota (u observada) utilizando el flujo de "Primer Pedido" implementado actualmente en la aplicación Flutter.                                                                            |

| LADO POSTERIOR: Configuración Técnica                                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Medidas:**<br />• Métrica Principal: Tasa de éxito de la tarea (Task Success Rate).<br />• Métrica Secundaria: Tiempo promedio en tarea (Time on Task) y número de errores críticos durante el flujo.             |
| **Condiciones:**<br />• Segmento: Usuarios que declaran usar menos de 2 aplicaciones de gestión en su día a día.                                                                                                       |
| **Escala:**<br />• Certeza: Basado en el estándar de Nielsen, una muestra de 5 usuarios para detectar hasta el 85% de los problemas de usabilidad.<br />• Tiempo: Una sesión única por usuario de máximo 30 minutos. |

**Tarjeta de Experimento 03: Viabilidad del Ecosistema de Proveedores**

Esta tarjeta mitiga el riesgo de que el sistema no sea útil si los proveedores no están dispuestos a abandonar sus métodos tradicionales (WhatsApp/Excel).

| LADO FRONTAL: Concepto y Motivación                                                                                                                                                                                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pregunta:** ¿Están los proveedores tradicionales dispuestos a digitalizar sus catálogos para integrarse a Restock a cambio de una mejor gestión de pagos?                                                                                                       |
| **Por qué:** Asegurar la viabilidad del ecosistema. Restock depende de que el proveedor alimente los datos; si el esfuerzo de carga es mayor al beneficio percibido de cobranza, el sistema colapsará.                                                              |
| **Hipótesis:** Creemos que al ofrecer una herramienta de carga masiva de catálogos y trazabilidad de pagos, el 60% de los proveedores contactados aceptará integrarse, cuya evidencia se reflejará en el número de catálogos activos creados durante la prueba. |
| **Qué (Simplest Useful Thing):** Realizar una Prueba de Conserje(Concierge Test) donde el equipo carga manualmente el catálogo de 3 proveedores reales y les muestra el módulo de "Seguimiento de Pagos" para medir su intención de uso.                          |

| LADO POSTERIOR: Configuración Técnica                                                                                                                                                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Medidas:**<br />• Métrica Principal: Tasa de conversión de interés (número de proveedores que firman la carta de intención de uso).<br />• Métrica Secundaria: Tiempo promedio que el proveedor dedica a revisar el estado de sus facturas en el prototipo.                             |
| **Condiciones:**<br />• Segmento: Proveedores tradicionales de abarrotes y bebidas con más de 10 años en el rubro.                                                                                                                                                                             |
| **Escala:**<br />• Certeza: Nivel de confianza del 90% para validar un mercado B2B pequeño.<br />• MDE (Efecto Mínimo): Interés positivo de al menos el 50% de la muestra para considerar el feature como viable.<br />• Tiempo: Sesiones de validación individuales con 3-5 proveedores. |

**Tarjeta de Experimento 04: Comportamiento basado en Datos (Q4)**

Esta tarjeta investiga si las funcionalidades analíticas de Restock realmente impactan el proceso de toma de decisiones del usuario core.

| LADO FRONTAL: Concepto y Motivación                                                                                                                                                                                                                                                          |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pregunta:** ¿Influye la visualización de métricas de rotación en la decisión de compra de nuevos insumos?                                                                                                                                                                       |
| **Por qué:** Validar si el usuario confía en los reportes analíticos de Restock para gestionar su capital o si prefiere seguir operando bajo su intuición habitual. Si los datos no influyen en la compra, el módulo de "Reports" pierde su valor estratégico.                  |
| **Hipótesis:** Creemos que al incorporar reportes de rotación, los administradores reducirán los errores al generar órdenes de compra en un 25%, cuya evidencia se reflejará en la disminución de líneas de pedido corregidas, bajo la circunstancia de abastecimiento semanal. |
| **Qué (Simplest Useful Thing):** Ejecución de una sesión de prueba utilizando el módulo "Overview" de la aplicación web ya implementada en Angular , presentando datos simulados de rotación alta/baja a 3 administradores antes de que realicen sus pedidos reales de la semana. |

| LADO POSTERIOR: Configuración Técnica                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Medidas:**<br />• Métrica Principal: Porcentaje de reducción en líneas de pedido que deben corregirse tras consultar el reporte (meta: 25%).<br />• Métrica Secundaria: Tiempo de permanencia del usuario en la vista de métricas de rotación.                                |
| **Condiciones:**<br />• Experimental: Administradores con acceso al dashboard de métricas de rotación ("Top Selling vs Dead Stock").<br />• Control: Administradores realizando su pedido basándose únicamente en su revisión manual de inventario física.                      |
| **Escala:**<br />• Certeza: Nivel de significancia del 5% y potencia estadística del 80%.<br />• MDE (Efecto Mínimo): Se busca detectar una mejora mínima del 10% en la precisión del pedido.<br />• Tiempo: Una sesión de observación por usuario durante un ciclo de compra. |

## 8.2. Experiment Design

En esta sección se diseña la estructura de los experimentos que permitirán validar las hipótesis del producto de manera ordenada y medible. Para ello, se definen las métricas de negocio, las medidas específicas, las condiciones de evaluación, el tamaño o escala del experimento y los métodos más adecuados para recolectar evidencia. Además, se establecen los objetivos de analítica, KPIs y el plan de seguimiento web y móvil, asegurando que cada experimento genere datos útiles para la toma de decisiones.

### 8.2.1. Hypotheses

En esta fase de diseño, se transforman las premisas en declaraciones de creencia específicas, falsables y medibles. Siguiendo el rigor del método científico aplicado al software, cada hipótesis de trabajo (H1) se presenta junto a su hipótesis nula (H0), la cual actúa como un espejo que atribuye cualquier cambio observado al azar o a la falta de relación entre las variables.

**Experimento 01: Impacto de Alertas en la Reducción de Mermas**

* **Hipótesis de Trabajo (H1):** Creemos que la respuesta a nuestra incertidumbre sobre el ahorro de insumos es que  **al ofrecer notificaciones push automáticas de stock bajo y vencimiento, los administradores realizarán pedidos preventivos**, cuya evidencia se reflejará en **una disminución del 35% en los reportes de mermas semanales**, bajo las circunstancias de **uso diario por parte de dueños de restaurantes medianos en Lima**.
* **Hipótesis Nula (H0):** Las alertas automáticas no causarán una reducción significativa del 35% en las mermas; cualquier fluctuación observada en el desperdicio de insumos será producto del azar o factores externos ajenos a la intervención del sistema.

**Experimento 02: Eficacia del Onboarding en Usuarios no Digitales**

* **Hipótesis de Trabajo (H1):** Creemos que la respuesta sobre la barrera de adopción es que  **un flujo de onboarding guiado y simplificado permite la autonomía del usuario**, cuya evidencia se reflejará en **una Tasa de Éxito de la Tarea (Task Success Rate) del 100% y un tiempo menor a 5 minutos en el primer pedido**, bajo las circunstancias de **uso por primera vez por sujetos con baja afinidad digital (que usan < 2 apps de gestión)**.
* **Hipótesis Nula (H0):** El onboarding guiado no tendrá un efecto medible en el éxito o la velocidad de la tarea; los usuarios no digitales seguirán requiriendo asistencia externa o tardarán más de 5 minutos independientemente de la interfaz.

**Experimento 03: Disposición de Proveedores a la Integración Digital**

* **Hipótesis de Trabajo (H1):** Creemos que la respuesta sobre la viabilidad del ecosistema es que  **proporcionar herramientas de carga de catálogos y trazabilidad de pagos incentiva la migración digital del proveedor**, cuya evidencia se reflejará en **un 60% de conversión de interés (firmas de intención de uso)**, bajo las circunstancias de **proveedores tradicionales con más de 10 años en el rubro**.
* **Hipótesis Nula (H0):** No existe una relación entre las herramientas de gestión de pagos y la disposición del proveedor a digitalizarse; la tasa de interés se mantendrá por debajo del umbral del 60% debido a la preferencia por métodos tradicionales (WhatsApp/Excel)

**Experimento 04: Influencia de Analíticos en la Precisión de Compra**

* **Hipótesis de Trabajo (H1):** Creemos que la respuesta a nuestra incertidumbre sobre el uso de datos es que  **al incorporar reportes automáticos con métricas de rotación, los administradores tomarán mejores decisiones de reabastecimiento**, cuya evidencia se reflejará en **una reducción del 25% en los errores o correcciones al generar órdenes de compra**, bajo las circunstancias de **uso en el cierre de inventario semanal por administradores experimentados**.
* **Hipótesis Nula (H0):** La visualización de métricas de rotación no tendrá un efecto medible en la precisión de las compras; cualquier cambio en el volumen de errores de pedido será producto del azar o de la experiencia previa del administrador, independientemente del uso de los reportes de Restock.

### 8.2.2. Domain Business Metrics

### 8.2.3. Measures

### 8.2.4. Conditions

### 8.2.5. Scale Calculations and Decisions

### 8.2.6. Methods Selection

### 8.2.7. Data Analytics: Goals, KPIs and Metrics Selection

### 8.2.8. Web and Mobile Tracking Plan

## 8.3. Experimentation

### 8.3.1. To-Be User Stories

### 8.3.2. To-Be Product Backlog

### 8.3.3. Pipeline-supported, Experiment-Driven To-Be Software Platform  Lifecycle

#### 8.3.3.1. To-Be Sprint Backlogs

#### 8.3.3.2. Implemented To-Be Landing Page Evidence

#### 8.3.3.3. Implemented To-Be Frontend-Web Application Evidence

#### 8.3.3.4. Implemented To-Be Native-Mobile Application Evidence

#### 8.3.3.5. Implemented To-Be RESTful API and/or Serverless Backend Evidence

#### 8.3.3.6. Team Collaboration Insights

### 8.3.4. To-Be Validation Interviews

#### 8.3.4.1. Diseño de Entrevistas

#### 8.3.4.2. Registro de Entrevistas

## 8.4. Experiment Aftermath & Analysis

### 8.4.1. Analysis and Interpretation of Results

### 8.4.2. Re-scored and Re-prioritized Question Backlog

## 8.5. Continuous Learning

### 8.5.1. Shareback Session Artifacts: Learning Workflow

## 8.6. To-Be Software Platform Pre-launch

### 8.6.1. About-the-Product Intro Video
