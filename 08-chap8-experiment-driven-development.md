# Part III: Experiment-Driven Lifecycle

# Capítulo VIII: Experiment-Driven Development

## 8.1. Experiment Planning

En esta sección se define la planificación de experimentos como punto de partida del enfoque  Experiment-Driven Development . Su objetivo es identificar qué se conoce actualmente, qué dudas existen y qué supuestos deben validarse antes de tomar decisiones sobre el producto. Para ello, se organiza la información en preguntas, brechas de conocimiento, ideas y tarjetas de experimento, permitiendo priorizar aprendizajes clave y reducir riesgos durante el desarrollo.

### 8.1.1. As-Is Summary

Hasta este punto, el proyecto Restock ha culminado la fase de diseño e implementación técnica, consolidando un ecosistema digital funcional que comprende una Landing Page, una aplicación web de gestión administrativa, aplicaciones móviles (Nativa y Flutter) y una arquitectura de servicios basada en una API RESTful con persistencia en MongoDB.

A pesar de contar con una solución "To-Be" ya construida, el estado actual de nuestro conocimiento se caracteriza por una **incertidumbre operativa**. Actualmente, el éxito de la plataforma depende de premisas críticas (como la capacidad de las alertas automáticas para reducir la merma en un 35%) que hasta el momento son suposiciones basadas en la sabiduría de la industria y no en datos quirúrgicos recolectados del comportamiento real de los usuarios.

Este resumen establece que el punto de partida de la fase actual no es la generación de nuevas soluciones técnicas, sino la recolección de material bruto (suposiciones, vacíos de conocimiento, ideas y afirmaciones) para transformar nuestras creencias en preguntas de investigación. El objetivo primordial es validar si las funcionalidades ya implementadas realmente generan el impacto social y económico previsto para los administradores y proveedores de restaurantes en Lima, antes de proceder con el lanzamiento final.

### 8.1.2. Raw Material: Assumptions, Knowledge Gaps, Ideas, Claims

Esta sección presenta las fuentes de inspiración que dieron origen a las preguntas de investigación del proyecto Restock. El material bruto recopilado aquí fue el insumo principal para construir las *Experiment-Ready Questions* de 8.1.3 y el Question Backlog de 8.1.4. Se organiza en cuatro categorías: **Ideas**, **Claims**, **Assumptions** y **Knowledge Gaps**.

---

#### Ideas

Las ideas son propuestas para resolver un problema o alcanzar un objetivo del producto. La premisa central de esta sección es que el equipo **no experimenta directamente con la idea**, sino con las suposiciones subyacentes que harían que la idea funcione o fracase.

|  ID  | Idea                                                                                                    | Premisa subyacente a probar                                                                                                                                                               |
| :--: | ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| I-01 | Sistema de alertas automáticas de stock bajo y vencimiento próximo enviadas por notificaciones push   | Los administradores actuarán sobre una alerta automática de la misma forma que actuarían si hubieran detectado el problema manualmente, reduciendo la merma en al menos un 35%.        |
| I-02 | Flujo de onboarding guiado paso a paso para administradores que nunca han usado software de gestión    | El diseño guiado es suficiente para que un usuario con baja afinidad digital complete su primer pedido de forma autónoma en menos de 5 minutos, sin necesitar soporte externo.          |
| I-03 | Dashboard web con columna de indicador de rotación (Alta / Media / Baja) en el módulo de Inventario   | Ver el nivel de rotación de un insumo antes de generar una orden cambiará el comportamiento de compra del administrador, reduciendo el volumen de pedidos de insumos de baja rotación. |
| I-04 | Portal de gestión de catálogo para proveedores, integrado con el flujo de pedidos de los restaurantes | La eficiencia de tener todos los pedidos centralizados en un solo panel es un incentivo suficiente para que el proveedor tradicional abandone WhatsApp/Excel y digitalice su catálogo.   |

---

#### Claims

Los claims son afirmaciones realizadas sobre el producto, ya sea por el equipo, stakeholders o por los propios usuarios durante sesiones de descubrimiento previas.

|  ID  | Afirmación (Claim)                                                                                                                             | Fuente                                                                                      | Vinculada a |
| :--: | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ----------- |
| C-01 | "Las alertas automáticas de Restock permitirán reducir el desperdicio de insumos perecibles en un 35%."                                       | Equipo de producto (basado en benchmarks del sector restaurantero).                         | EQ1, Q1     |
| C-02 | "Los administradores de restaurantes medianos en Lima no están dispuestos a aprender una nueva aplicación si el proceso inicial es complejo." | Retroalimentación cualitativa de entrevistas de usuario en fases previas del proyecto.     | EQ2, Q2     |
| C-03 | "Los proveedores tradicionales se integrarán a Restock si perciben que el volumen de pedidos que gestionan aumentará."                        | Hipótesis del equipo fundada en la lógica de incentivos B2B del mercado local.            | EQ3, Q3     |
| C-04 | "Mostrar datos de rotación en el inventario no cambia la conducta de compra de los administradores; siguen confiando en su intuición."        | Observación del equipo durante sesiones de prueba de usabilidad internas.                  | EQ4, Q4     |
| C-05 | "El onboarding guiado reduce el tiempo de activación del usuario de 15 minutos a menos de 5 minutos."                                          | Estimación del equipo de diseño basada en el análisis del flujo actual de la app móvil. | EQ2, Q2     |

#### Assumptions

Las suposiciones son creencias preexistentes sobre el producto o la audiencia —frecuentemente basadas en la sabiduría del sector o en conocimiento previo— que deben ser probadas mediante experimentación antes de convertirse en decisiones de producto definitivas.

|  ID  | Suposición (Assumption)                                                                                                                                                        | Categoría | Riesgo si resulta falsa                                                                                              | Vinculada a |
| :--: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | -------------------------------------------------------------------------------------------------------------------- | ----------- |
| A-01 | Los administradores de restaurantes medianos en Lima gestionan hoy su inventario de forma manual (Excel, cuadernos, WhatsApp) y no mediante un sistema digital.                 | Audiencia  | Alto: si ya usan software, la propuesta de valor de Restock pierde diferenciación.                                  | EQ1, EQ2    |
| A-02 | La principal causa de mermas en restaurantes medianos es la falta de visibilidad oportuna del nivel de stock, no el desperdicio en cocina ni el sobrestock deliberado.          | Producto   | Alto: si la causa raíz es otra, las alertas automáticas no reducirán la merma.                                    | EQ1, Q1     |
| A-03 | Un usuario con baja afinidad digital puede aprender a usar una aplicación móvil de gestión si el flujo es lo suficientemente sencillo y guiado.                              | Audiencia  | Medio: si la barrera cognitiva es mayor a la esperada, ningún onboarding resolverá el problema de adopción.       | EQ2, Q2     |
| A-04 | Los proveedores de insumos en Lima que operan informalmente (menos de 10 empleados, sin sistema propio) están en búsqueda activa de herramientas que centralicen sus pedidos. | Ecosistema | Alto: si no existe demanda latente, la estrategia de adquisición de proveedores requiere ser rediseñada.           | EQ3, Q3     |
| A-05 | La visualización de una métrica de rotación histórica es suficiente señal para que el administrador tome una decisión de compra diferente a la habitual.                  | Producto   | Medio: si el usuario ignora el dato o no confía en él, el desarrollo del módulo de reportes no generará retorno. | EQ4, Q4     |
| A-06 | El canal preferido por los administradores para recibir soporte inicial es el tutorial in-app o el tooltip contextual, por encima de WhatsApp o soporte humano.                 | Audiencia  | Bajo: impacta el diseño del canal de soporte, no la propuesta de valor central.                                     | EQ5         |

#### Knowledge Gaps

Las brechas de conocimiento son áreas donde el equipo reconoce explícitamente que carece de información. A diferencia de las suposiciones (donde existe una creencia, aunque no confirmada), los Knowledge Gaps son preguntas abiertas sin respuesta inicial, que frecuentemente dan lugar a preguntas exploratorias.

|  ID  | Brecha de Conocimiento                                                                                                                                                                              | Impacto en el producto                                                                                        | Vinculada a |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ----------- |
| KG-01 | Se desconoce el volumen real de mermas semanales (en kg o costo) que registran los restaurantes objetivo*antes* de usar Restock. Sin esta línea base, es imposible medir la reducción del 35%.  | Crítico: sin baseline, el KPI principal (WRR) no es calculable.                                              | Q1, EQ1     |
| KG-02 | No se sabe cuánto tiempo tardan actualmente los administradores en realizar un pedido de insumos por sus canales habituales (llamada, WhatsApp, visita presencial).                                | Moderado: impide establecer el umbral realista de "menos de 5 minutos" como mejora significativa.             | Q2, EQ2     |
| KG-03 | Se ignora qué porcentaje de los proveedores de insumos en Lima ya cuenta con alguna herramienta digital propia (aunque sea básica), lo que afecta la segmentación del experimento de adopción.  | Moderado: podría sesgar la muestra del Experimento 03 si se incluyen proveedores ya digitalizados.           | Q3, EQ3     |
| KG-04 | No se conocen las principales barreras operativas que impiden a los proveedores actualizar su inventario digital con frecuencia (tiempo, privacidad de precios, dificultad técnica, desconfianza). | Alto: sin entender la barrera real, el diseño del portal de proveedores puede atacar el problema equivocado. | EQ6         |
| KG-05 | No existe evidencia interna sobre si los administradores realmente leen los reportes de métricas generados por el sistema, o si los ignoran al tomar decisiones de compra.                         | Moderado: determina si vale la pena invertir en el módulo de reportes avanzados antes de validar su uso.     | Q4, EQ4     |

### 8.1.3. Experiment-Ready Questions

Para transformar la materia prima y la incertidumbre operativa descrita en el As-Is Summary en elementos accionables, se han formulado *Experiment-Ready Questions*. Estas preguntas delimitan el alcance de los experimentos para la plataforma Restock y se dividen en dos categorías principales.

Para descubrir las premisas ocultas detrás de los problemas de gestión de inventarios y adopción B2B, y así generar las preguntas adecuadas, el equipo aplicó la técnica de las **"Cinco Ws (y una H)"**:

* **Who (Quién):** Administradores de restaurantes con baja afinidad digital y proveedores de insumos tradicionales en Lima.
* **What (Qué):** Desperdicio de insumos por falta de control, fricción tecnológica en la adopción de nuevas herramientas, y resistencia para digitalizar catálogos.
* **Where (Dónde):** En el ecosistema operativo de los restaurantes (almacén, cocina) y en los canales de venta de los proveedores.
* **When (Cuándo):** Durante el monitoreo diario de caducidad/stock y el proceso de reabastecimiento o creación de órdenes de compra.
* **Why (Por qué):** Porque la dependencia de procesos manuales, la falta de datos históricos y la intuición generan ineficiencias, sobrestock y mermas que afectan directamente la rentabilidad de ambos actores.
* **How (Cómo):** Mediante la implementación del ecosistema digital (Web, App Nativa y Flutter) que automatiza alertas, simplifica el flujo de pedidos y ofrece métricas de rotación accionables.

A partir de este análisis, se han definido las siguientes preguntas listas para experimentación, las cuales alimentan directamente el Backlog y las Tarjetas de Experimento del proyecto:

#### A. Preguntas Impulsadas por Creencias (Belief-led Questions)

Estas preguntas buscan probar una creencia o premisa específica sobre la solución propuesta frente a los problemas críticos de negocio definidos previamente.

* **EQ1:** ¿Reducen las alertas automáticas de "stock bajo" y "vencimiento" en tiempo real el desperdicio de insumos perecibles en un 35%?
* **EQ2:** ¿Son capaces los administradores con baja afinidad digital de completar un pedido de insumos de forma autónoma sin asistencia externa?
* **EQ3:** ¿Están los proveedores tradicionales dispuestos a digitalizar sus catálogos para integrarse a Restock a cambio de una gestión de pedidos centralizada?
* **EQ4:** ¿Influye la visualización de métricas de rotación en el dashboard web en la decisión de compra de nuevos insumos por parte de los administradores?

#### B. Preguntas Exploratorias (Exploratory Questions)

Estas preguntas buscan recopilar conocimiento cualitativo y explorar áreas del comportamiento de los usuarios donde el equipo aún tiene vacíos de información (*Knowledge Gaps*), sirviendo como complemento a los experimentos principales.

* **EQ5:** ¿Qué canales o métodos de soporte (tutoriales interactivos, tooltips, asistencia humana por WhatsApp) prefieren los administradores de restaurantes para superar la fricción inicial durante su primer pedido en la app?
* **EQ6:** ¿Cuáles son las principales barreras operativas o temores (inversión de tiempo, privacidad de precios, dificultad técnica) que impiden a los proveedores actualizar su inventario digital de manera frecuente en la plataforma web?

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

##### **Tarjeta de Experimento 01: Validación de Impacto en Mermas**

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

**Artefacto que se usará como Simplest Useful Thing: Notificaciones en mobile**

<img src="assets/images/chapter8/experiment-cards/exp_card_1.png" height="400px" alt="experiment card 1">

##### **Tarjeta de Experimento 02: Validación de Adopción Digital**

Esta tarjeta mitiga el riesgo técnico y de usuario identificado en el segmento de administradores tradicionales.

| LADO FRONTAL: Concepto y Motivación                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pregunta:** ¿Son capaces los administradores con baja afinidad digital de completar su primer pedido de insumos de forma autónoma?                                                                                                                       |
| **Por qué:** El mayor riesgo de abandono de la plataforma es la fricción inicial; si el proceso es complejo, el usuario no regresará.                                                                                                                      |
| **Hipótesis:** Creemos que con un onboarding guiado simplificado, los usuarios nuevos completarán su pedido en menos de 5 minutos, cuya evidencia se verá en el éxito de la tarea, bajo la circunstancia de uso por primera vez sin capacitación previa. |
| **Qué (Simplest Useful Thing):** Una sesión de prueba de usuario remota utilizando el flujo de "Primer Pedido" implementado actualmente en la aplicación móvil.                                                                                           |

| LADO POSTERIOR: Configuración Técnica                                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Medidas:**<br />• Métrica Principal: Tasa de éxito de la tarea (Task Success Rate).<br />• Métrica Secundaria: Tiempo promedio en tarea (Time on Task) y número de errores críticos durante el flujo.             |
| **Condiciones:**<br />• Segmento: Usuarios que declaran usar menos de 2 aplicaciones de gestión en su día a día.                                                                                                       |
| **Escala:**<br />• Certeza: Basado en el estándar de Nielsen, una muestra de 5 usuarios para detectar hasta el 85% de los problemas de usabilidad.<br />• Tiempo: Una sesión única por usuario de máximo 30 minutos. |

**Artefacto que se usará como Simplest Useful Thing: Flujo de Primer pedido implementado en la aplicación móvil**

<img src="assets/images/chapter8/experiment-cards/exp_card_2.png" height="400px" alt="experiment card 2">

##### **Tarjeta de Experimento 03: Viabilidad del Ecosistema de Proveedores**

Esta tarjeta mitiga el riesgo de que el sistema no sea útil si los proveedores no están dispuestos a abandonar sus métodos tradicionales (WhatsApp/Excel).

| LADO FRONTAL: Concepto y Motivación                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pregunta:** ¿Están los proveedores tradicionales dispuestos a digitalizar sus catálogos para integrarse a Restock a cambio de una gestión de pedidos centralizada?                                                                                                                          |
| **Por qué:** Validar si el valor percibido de tener todos los pedidos en un solo panel compensa el esfuerzo de mantener el catálogo digitalizado. Sin proveedores activos, el restaurante no puede reabastecerse automáticamente                                                               |
| **Hipótesis:** Creemos que al ofrecer una herramienta de visualización de pedidos en tiempo real y gestión de productos, el 60% de los proveedores aceptará la migración digital, cuya evidencia se verá en firmas de intención de uso, bajo la circunstancia de proveedores tradicionales |
| **Qué (Simplest Useful Thing):** Realizar una Prueba de Conserje (*Concierge Test* ) donde el equipo carga manualmente el catálogo de 3 proveedores reales y les muestra el funcionamiento de los módulos Gestión de pedidos y Gestión de Insumos para medir su intención de adopción.   |

| LADO POSTERIOR: Configuración Técnica                                                                                                                                                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Medidas:**<br />• Métrica Principal: Tasa de conversión de interés (número de proveedores que firman la carta de intención de uso).<br />• Métrica Secundaria: Número de "puntos de fricción" identificados durante la navegación del módulo de gestión de insumos.                |
| **Condiciones:**<br />• Segmento: Proveedores con más de 10 años en el rubro que actualmente gestionan pedidos solo por canales informales.                                                                                                                                                    |
| **Escala:**<br />• Certeza: Nivel de confianza del 90% para validar un mercado B2B pequeño.<br />• MDE (Efecto Mínimo): Interés positivo de al menos el 50% de la muestra para considerar el feature como viable.<br />• Tiempo: Sesiones de validación individuales con 3-5 proveedores. |

**Artefacto que se usará como Simplest Useful Thing:**

- Módulo de Gestión de pedidos

<img src="assets/images/chapter8/experiment-cards/exp_card_3-1.png" width="600px" alt="experiment card 3.1">

- Módulo de Gestión de insumos

<img src="assets/images/chapter8/experiment-cards/exp_card_3-2.png" width="600px" alt="experiment card 3.2">

##### **Tarjeta de Experimento 04: Comportamiento basado en Datos**

Esta tarjeta investiga si añadir indicadores de rotación directamente en la lista de inventario impacta la toma de decisiones.

| LADO FRONTAL: Concepto y Motivación                                                                                                                                                                                                                                                                 |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pregunta:** ¿Influye la visualización de métricas de rotación en la decisión de compra de nuevos insumos?                                                                                                                                                                              |
| **Por qué:** Validar si el usuario confía en datos analíticos para gestionar su capital. Si ver que un producto "no se mueve" no cambia su conducta de compra, no vale la pena desarrollar el módulo de reportes avanzado.                                                                |
| **Hipótesis:** Creemos que al mostrar un indicador de rotación en el inventario, los administradores reducirán los errores de sobrestock en un 25%, cuya evidencia se verá en la disminución de cantidades en las órdenes de compra, bajo la circunstancia de reabastecimiento semanal. |
| **Qué (Simplest Useful Thing):** Modificar la tabla del módulo Overview en la aplicación web Angular para incluir una columna extra llamada "Rotation" (con etiquetas: Alta, Media, Baja) calculada manualmente con datos históricos para 3 administradores de prueba.                    |

| LADO POSTERIOR: Configuración Técnica                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Medidas:**<br />• Métrica Principal: Porcentajede reducción en el volumen de pedidos para insumos marcados con "Baja Rotación".<br />• Métrica Secundaria: Tiempo de permanencia del usuario en la vista de métricas de rotación.                                             |
| **Condiciones:**<br />• Experimental: Administradores con acceso al dashboard principal con métricas de rotación.<br />• Control: Administradores realizando su pedido basándose únicamente en su revisión manual de inventario física.                                         |
| **Escala:**<br />• Certeza: Nivel de significancia del 5% y potencia estadística del 80%.<br />• MDE (Efecto Mínimo): Se busca detectar una mejora mínima del 10% en la precisión del pedido.<br />• Tiempo: Una sesión de observación por usuario durante un ciclo de compra. |

**Artefacto que se usará como Simplest Useful Thing: Módulo Overview con métricas de rotación**

<img src="assets/images/chapter8/experiment-cards/exp_card_4.png" width="600px" alt="experiment card 4">

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

* **Hipótesis de Trabajo (H1):** Creemos que la respuesta sobre la viabilidad del ecosistema es que  **proporcionar herramientas de carga de catálogos y gestión centralizada de pedidos entrantes incentiva la migración digital del proveedor**, cuya evidencia se reflejará en **un 60% de conversión de interés (firmas de intención de uso o aceptación de capacitación)**, bajo las circunstancias de **proveedores tradicionales con más de 10 años en el rubro que actualmente usan canales informales.**
* **Hipótesis Nula (H0):** No existe una relación entre las herramientas de gestión de pedidos y la disposición del proveedor a digitalizarse; la tasa de interés se mantendrá por debajo del umbral del 60% debido a la persistencia y preferencia por métodos tradicionales como WhatsApp o Excel.

**Experimento 04: Influencia de Indicadores de Rotación en el Inventario**

* **Hipótesis de Trabajo (H1):** Creemos que la respuesta a nuestra incertidumbre es que **al incluir una columna de nivel de rotación en el módulo de Inventario, los administradores tomarán decisiones de compra más precisas**, cuya evidencia se reflejará en **una reducción del 25% en el volumen de pedidos de insumos de baja rotación**, bajo las circunstancias de **uso durante el cierre de inventario semanal por dueños de restaurantes.**
* **Hipótesis Nula (H0):** La visualización de la rotación en el inventario no tendrá un efecto medible; los administradores seguirán pidiendo las mismas cantidades basándose en su intuición o hábitos previos, independientemente del dato mostrado por Restock.

### 8.2.2. Domain Business Metrics

El objetivo fundamental de esta sección es alinear estratégicamente la medición de los experimentos con los objetivos comerciales core de la plataforma Restock. Al definir métricas de negocio concretas, estandarizadas y predefinidas, el equipo mitiga el riesgo de evaluar el éxito de las intervenciones basándose en *vanity metrics* (métricas de vanidad) o datos aislados que no aportan valor real a la toma de decisiones.

Cada una de las métricas detalladas a continuación se vincula directamente con las hipótesis planteadas en la fase de diseño (sección 8.2.1), asegurando que no se utilicen métricas *ad-hoc* durante la ejecución del experimento.

#### 1. Tasa de Reducción de Mermas (Waste Reduction Rate - WRR)

* **Descripción:** Mide la disminución porcentual en el volumen o costo de los insumos perecibles que se reportan como desperdicio dentro del restaurante, validando la eficacia de las alertas automáticas.
* **Fórmula de cálculo:**
  $$
  \text{WRR} = \left( \frac{\text{Mermas en Período de Control} - \text{Mermas en Período Experimental}}{\text{Mermas en Período de Control}} \right) \times 100
  $$
* **Técnica de recolección:** Extracción automatizada de los reportes semanales de mermas registrados en la base de datos de la plataforma por los usuarios del grupo experimental.
* **Meta deseada:** Una reducción mínima del 35% en el desperdicio de insumos perecibles.

#### 2. Tasa de Éxito de la Tarea (Task Success Rate - TSR)

* **Descripción:** Evalúa la eficacia del flujo de *onboarding* guiado midiendo el porcentaje de administradores (con baja afinidad digital) que logran enviar su primer pedido de forma completamente autónoma en menos de 5 minutos.
* **Fórmula de cálculo:**
  $$
  \text{TSR} = \left( \frac{\text{Usuarios que completan el pedido sin asistencia en < 5 min}}{\text{Total de usuarios evaluados en la muestra}} \right) \times 100
  $$
* **Técnica de recolección:** Pruebas de usabilidad remotas y registro de eventos (Event Tracking) en la herramienta de analítica integrada en la aplicación móvil (Firebase Analytics).
* **Meta deseada:** 100% de éxito autónomo en la muestra de usuarios evaluada.

#### 3. Tasa de Conversión de Interés del Proveedor (Supplier Conversion Rate - SCR)

* **Descripción:** Determina la viabilidad comercial de digitalizar a los proveedores midiendo la proporción de negocios tradicionales que muestran una intención firme de integrarse a Restock tras interactuar con la gestión de pedidos centralizada.
* **Fórmula de cálculo:**
  $$
  \text{SCR} = \left( \frac{\text{Número de proveedores que firman la intención de uso}}{\text{Total de proveedores expuestos al experimento}} \right) \times 100
  $$
* **Técnica de recolección:** Registro cualitativo y cuantitativo al finalizar las sesiones individuales de capacitación o demostración.
* **Meta deseada:** Un mínimo de 60% de conversión de interés sobre la muestra evaluada.

#### 4. Índice de Precisión de Compra (Purchase Precision Index - PPI)

* **Descripción:** Evalúa el impacto de la visualización de métricas de rotación en el comportamiento de compra del administrador, midiendo la disminución en el volumen de pedidos excesivos para insumos catalogados con "Baja Rotación".
* **Fórmula de cálculo:**
  $$
  \text{PPI} = \left( \frac{\text{Volumen de pedido histórico As-Is} - \text{Volumen de pedido con métrica visible To-Be}}{\text{Volumen de pedido histórico As-Is}} \right) \times 100
  $$
* **Técnica de recolección:** Comparación de los datos históricos de órdenes previas contra las nuevas órdenes de compra generadas a través del módulo de inventario.
* **Meta deseada:** Una reducción del 25% en el volumen de pedidos de insumos de baja rotación en un ciclo de cierre semanal.

### 8.2.3. Measures

En esta sección se definen los criterios específicos seleccionados para recopilar la evidencia que permitirá responder a las preguntas de investigación (*Experiment-Ready Questions*) establecidas. Para asegurar la efectividad del proceso, se ha distinguido entre la evidencia primaria (que responde directamente a la pregunta) y la evidencia secundaria (que proporciona contexto sobre el comportamiento del usuario).

Adicionalmente, el diseño de estas medidas se rige bajo el principio de **economía de rastreo** (*economy of tracking*). Esto significa que el equipo utilizará y recolectará únicamente los datos estrictamente necesarios, activando las herramientas de analítica (como Firebase Analytics) por el tiempo justo que dure cada experimento, con el objetivo de minimizar costos de infraestructura, reducir el ruido en los datos y mitigar riesgos de privacidad.

A continuación, se detallan las medidas estructuradas para cada uno de los experimentos planificados:

#### Experimento 01: Impacto de Alertas en la Reducción de Mermas

* **Evidencia Principal (Primary Measure):**
  * Reducción porcentual del volumen (en kg/litros) de mermas reportadas semanalmente en el sistema por el restaurante. (Representativa del *Waste Reduction Rate*).
* **Evidencia Secundaria (Secondary Measure):**
  * *Click-Through Rate (CTR)* de las notificaciones push de alerta de stock.
  * Tiempo de respuesta (en horas/minutos) desde la recepción de la alerta hasta la confirmación de una nueva orden de compra preventiva.
* **Principio de Economía:** El rastreo de estas métricas se activará exclusivamente durante los 14 días (dos ciclos semanales) que dura la prueba piloto. No se rastrearán clics en notificaciones ajenas al módulo de inventario.

#### Experimento 02: Eficacia del Onboarding en Usuarios no Digitales

* **Evidencia Principal (Primary Measure):**
  * Tasa de finalización exitosa (Booleano: Sí/No) en el envío del primer pedido sin intervención de soporte técnico. (Representativa del *Task Success Rate*).
* **Evidencia Secundaria (Secondary Measure):**
  * *Time on Task*: Tiempo cronometrado desde el inicio del onboarding hasta la pantalla de confirmación de pedido (buscando que sea < 5 minutos).
  * Tasa de abandono (Drop-off rate) en pantallas específicas del flujo de onboarding guiado.
* **Principio de Economía:** La captura de estos eventos se limitará a la primera sesión de inicio de los nuevos usuarios (Cohorte experimental). Una vez completado el primer pedido, el seguimiento detallado de estos eventos se apagará automáticamente.

#### Experimento 03: Disposición de Proveedores a la Integración Digital

* **Evidencia Principal (Primary Measure):**
  * Número absoluto de proveedores que firman la carta de intención de uso o agendan oficialmente el despliegue de la herramienta. (Representativa del *Supplier Conversion Rate*).
* **Evidencia Secundaria (Secondary Measure):**
  * Número de preguntas, bloqueos o dudas expresadas verbalmente sobre el catálogo digital durante la sesión de *Concierge Test*.
  * Nivel de fricción técnica observada (escala del 1 al 5) durante la demostración en vivo de los módulos.
* **Principio de Economía:** Debido a que este experimento evalúa viabilidad B2B temprana, las medidas son predominantemente cualitativas y se recolectarán de forma manual durante las sesiones presenciales o por videollamada, evitando el desarrollo prematuro de telemetría en el portal de proveedores.

#### Experimento 04: Influencia de Indicadores de Rotación en el Inventario

* **Evidencia Principal (Primary Measure):**
  * Variación en las cantidades solicitadas en órdenes de compra para aquellos insumos etiquetados visualmente con "Baja Rotación" en el dashboard. (Representativa del *Purchase Precision Index*).
* **Evidencia Secundaria (Secondary Measure):**
  * *Dwell Time* (Tiempo de permanencia) del administrador en la columna de métricas de rotación antes de hacer clic en el botón de "Añadir a orden".
  * Cantidad de insumos de "Baja rotación" que son eliminados del carrito de compras antes del checkout.
* **Principio de Economía:** El seguimiento de eventos (*Event Tracking*) se implementará a nivel de componente en la tabla de Angular del módulo de Inventario, y los datos se evaluarán únicamente durante el día específico en que cada restaurante suele hacer su cierre y pedido semanal, limitando el procesamiento de logs innecesarios el resto de la semana.

### 8.2.4. Conditions

Esta sección describe las condiciones definidas para cada experimento planificado en la plataforma Restock, en función de los factores que permiten identificar el motivo subyacente detrás de cada respuesta esperada. Para cada experimento derivado de las hipótesis de negocio (sección 8.2.1), se establece la **condición experimental** —orientada a obtener evidencia a favor de la hipótesis alternativa— y la **condición de control** —que representa el estado base bajo la suposición de que la hipótesis nula es correcta—.

---

### Experimento 1 — Módulo de inventario automatizado con alertas en tiempo real

**Pregunta:** ¿La activación del módulo de inventario automatizado con alertas reduce las mermas de insumos en los restaurantes?

|                                       | Descripción                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Condición Experimental (A)** | Los administradores de restaurante acceden a la plataforma Restock con el módulo de inventario activo. Reciben alertas automáticas clasificadas por tipo (stock bajo, exceso de stock, vencimiento próximo) y visualizan el nivel de stock actualizado en tiempo real desde el dashboard. El sistema descuenta insumos automáticamente al registrar ventas. |
| **Condición de Control (B)**   | Los administradores gestionan su inventario mediante métodos manuales convencionales: hojas de cálculo (Excel o Google Sheets), cuadernos físicos o mensajería (WhatsApp). No tienen acceso al módulo automatizado de Restock durante el período de medición.                                                                                            |

**Variable independiente:** Activación del módulo de inventario automatizado con alertas en tiempo real.
**Variable dependiente:** Porcentaje de reducción en mermas de insumos por período de medición.
**H₀:** El módulo de inventario automatizado no produce una reducción significativa de mermas respecto al método manual.
**H₁:** El módulo reduce las mermas en al menos un **35 %** respecto al método manual.

**Criterio de asignación:** Asignación aleatoria por restaurante participante. Cada restaurante opera exclusivamente bajo una de las dos condiciones durante el período del experimento para evitar contaminación cruzada.

---

### Experimento 2 — Onboarding guiado e interfaz móvil-first

**Pregunta:** ¿Un onboarding guiado combinado con acceso móvil como canal principal incrementa la retención temprana de usuarios?

|                                       | Descripción                                                                                                                                                                                                                                                                                                    |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Condición Experimental (A)** | Los nuevos usuarios (administradores y proveedores) reciben un flujo de onboarding guiado paso a paso al registrarse: tour interactivo, tooltips contextuales en los módulos principales y configuración asistida del primer insumo y primera orden. El canal de acceso recomendado es el dispositivo móvil. |
| **Condición de Control (B)**   | Los nuevos usuarios acceden a la plataforma sin guía de onboarding: navegan libremente desde la pantalla de inicio sin asistencia contextual. No se sugiere ningún canal preferente de acceso.                                                                                                                |

**Variable independiente:** Presencia de onboarding guiado y disponibilidad de acceso móvil-first.
**Variable dependiente:** Número de usuarios que inician sesión 3 o más veces durante sus primeros 7 días tras el registro (retención temprana).
**H₀:** El onboarding guiado y el acceso móvil no incrementan significativamente la retención temprana de usuarios.
**H₁:** El onboarding guiado permite que al menos **500 usuarios activos** registren 3 o más sesiones en sus primeros 7 días dentro de los primeros 6 meses de operación.

**Criterio de asignación:** Asignación por cohorte de registro. Los usuarios registrados durante las primeras 4 semanas corresponden a la condición de control; los registrados durante las siguientes 4 semanas corresponden a la condición experimental, en un esquema de despliegue progresivo (feature flag).

---

### Experimento 3 — Reportes automáticos con métricas de rotación y márgenes

**Pregunta:** ¿El acceso a reportes automáticos reduce los errores al generar órdenes de compra?

|                                       | Descripción                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Condición Experimental (A)** | Los administradores de restaurante tienen acceso al módulo de reportes de Restock, el cual genera automáticamente informes con métricas de rotación de insumos, nivel promedio de stock por período y sugerencias de cantidad de pedido basadas en el historial de consumo. Los reportes están disponibles previo a la generación de cada orden. |
| **Condición de Control (B)**   | Los administradores generan órdenes de compra sin acceso a reportes automatizados. Toman decisiones de abastecimiento basadas en la observación directa del inventario, criterio propio o registros históricos elaborados manualmente fuera de la plataforma.                                                                                        |

**Variable independiente:** Disponibilidad de reportes automáticos con métricas de rotación y márgenes previo a la generación de órdenes.
**Variable dependiente:** Porcentaje de líneas de pedido que requieren corrección (edición o eliminación) antes de ser enviadas al proveedor.
**H₀:** El acceso a reportes automáticos no reduce significativamente los errores en la generación de órdenes de compra.
**H₁:** Los reportes automáticos reducen en al menos un **25 %** las líneas de pedido que necesitan corrección.

**Criterio de asignación:** Asignación aleatoria por restaurante. Se controla que el restaurante no haya utilizado el módulo de reportes previamente (no contaminación de cohorte).

---

### Experimento 4 — Canal centralizado proveedor–restaurante (catálogo, pedidos y comunicación)

**Pregunta:** ¿La centralización del catálogo, pedidos y comunicación dentro de la plataforma incrementa el volumen de pedidos gestionados y reduce los errores de pedido?

|                                       | Descripción                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Condición Experimental (A)** | Los administradores de restaurante y sus proveedores asociados gestionan catálogos de productos, creación y seguimiento de pedidos, y comunicación exclusivamente dentro de Restock (módulo de órdenes + catálogo del proveedor + sistema de notificaciones de estado). No se permite el uso de canales externos para estas interacciones durante el período del experimento. |
| **Condición de Control (B)**   | La gestión de pedidos y comunicación se realiza a través de los canales fragmentados habituales: WhatsApp, llamadas telefónicas, correo electrónico o visitas presenciales. La plataforma Restock no se utiliza para estas interacciones.                                                                                                                                       |

**Variable independiente:** Uso exclusivo del canal centralizado de Restock para gestión de catálogos, pedidos y comunicación entre restaurante y proveedor.
**Variable dependiente (primaria):** Número de pedidos creados dentro de la plataforma por restaurante por mes.
**Variable dependiente (secundaria):** Porcentaje de órdenes con devoluciones, ajustes o errores de pedido sobre el total de órdenes creadas.
**H₀:** La centralización del canal no produce un incremento significativo en pedidos gestionados dentro de la plataforma ni reduce los errores de pedido.
**H₁:** La centralización incrementa en al menos un **40 %** los pedidos gestionados en la plataforma y reduce en al menos un **25 %** las devoluciones o ajustes.

**Criterio de asignación:** Asignación por par restaurante–proveedor. Ambos actores del par deben pertenecer a la misma condición para garantizar que la interacción sea consistente con el canal asignado.

---

### 8.2.5. Scale Calculations and Decisions

Esta sección describe la determinación de la cantidad de evidencia necesaria para la investigación. Expone que la escala se basa en la **Certeza**, entendida como la probabilidad de error aceptable, y la **Precisión**, que corresponde a la granularidad del cambio a detectar. La certeza se define mediante el **Poder Estadístico**, que ayuda a evitar errores Tipo II, y el **Nivel de Significación**, que previene errores Tipo I. La precisión se representa con el **Efecto Mínimo Detectable (MDE)**, que indica el tamaño mínimo de diferencia valiosa para detectar.

Al momento de elegir la escala, se ajustará el nivel de significancia, que normalmente se debe establecer en un 5%, para minimizar los errores atribuibles al azar. Asimismo, se determinará el efecto mínimo detectable (MDE) para establecer la magnitud de la diferencia que debe identificarse, ya sea pequeña o grande. Además, se seleccionará un nivel adecuado de potencia estadística, típicamente entre el 80% y el 95%, con el fin de reducir la probabilidad de cometer errores Tipo II. Finalmente, se utilizarán datos representativos para asegurar que los hallazgos sean aplicables al grupo de interés.

#### Experimento 1 — Validación de Impacto en Mermas

| Parámetro                   | Valor                                 | Justificación                                                     |
| ---------------------------- | ------------------------------------- | ------------------------------------------------------------------ |
| Nivel de significancia (α)  | 5%                                    | Estándar científico para minimizar falsos positivos              |
| Potencia estadística (1-β) | 80%                                   | Balance aceptable entre tamaño de muestra y fiabilidad            |
| MDE                          | 10% de reducción en mermas           | Diferencia mínima con impacto económico real para el restaurante |
| Duración                    | 14 días (2 ciclos de abastecimiento) | Cubre al menos dos ciclos operativos completos                     |
| Tamaño de muestra           | 5 por grupo (experimental + control)  | Piloto inicial acotado; suficiente para detectar señal fuerte     |

**Decisión:** Se acepta una muestra reducida (n=5 por grupo) dado el carácter exploratorio del piloto. Si la señal inicial supera el MDE del 10%, se escalaría a una muestra mayor en una segunda iteración.

#### Experimento 2 — Validación de Adopción Digital

| Parámetro                  | Valor                                      | Justificación                                                |
| --------------------------- | ------------------------------------------ | ------------------------------------------------------------- |
| Nivel de significancia (α) | N/A (prueba de usabilidad cualitativa)     | El método no requiere test de hipótesis estadístico formal |
| Potencia estadística       | N/A                                        | Basado en el estándar de Nielsen para pruebas de usabilidad  |
| MDE                         | Tasa de éxito de tarea ≥ 80% en ≤ 5 min | Umbral operativo definido por el equipo de producto           |
| Tamaño de muestra          | 5 usuarios                                 | Nielsen: detecta hasta el 85% de los problemas de usabilidad  |
| Duración                   | Sesión única de ≤ 30 min por usuario    | Tiempo razonable sin fatiga del participante                  |

**Decisión:** Para esta prueba de usabilidad, la escala sigue el benchmark de Nielsen (n=5). No se aplica test estadístico formal; el criterio de éxito es cualitativo-cuantitativo: ≥ 4 de 5 usuarios completan el flujo de forma autónoma.

#### Experimento 3 — Validación de Adopción de Proveedores

| Parámetro                  | Valor                                     | Justificación                                                            |
| --------------------------- | ----------------------------------------- | ------------------------------------------------------------------------- |
| Nivel de significancia (α) | N/A (entrevistas cualitativas)            | Investigación exploratoria de intención                                 |
| MDE                         | Tasa de disposición a digitalizar ≥ 60% | Umbral mínimo para justificar inversión en onboarding de proveedores    |
| Tamaño de muestra          | 6 proveedores (3 formales, 3 informales)  | Muestra estratificada para detectar diferencias entre perfiles            |
| Duración                   | 1 semana                                  | Tiempo suficiente para coordinar y ejecutar entrevistas semiestructuradas |

**Decisión:** Se prioriza investigación cualitativa con muestra estratificada. La señal de interés mínima es que al menos 4 de 6 proveedores expresen disposición a digitalizar su catálogo.

#### Experimento 4 — Validación de Decisiones Basadas en Datos

| Parámetro                   | Valor                                                | Justificación                                                |
| ---------------------------- | ---------------------------------------------------- | ------------------------------------------------------------- |
| Nivel de significancia (α)  | 5%                                                   | Estándar para comparación entre grupos                      |
| Potencia estadística (1-β) | 80%                                                  | Nivel convencional para estudios de comportamiento            |
| MDE                          | 20% de aumento en precisión de decisiones de compra | Cambio observable en el patrón de órdenes del administrador |
| Duración                    | 14 días                                             | Equivalente a 2 semanas operativas de observación            |
| Tamaño de muestra           | 5 por grupo                                          | Piloto inicial; alineado con Experimento 1                    |

**Decisión:** Se replica el diseño del Experimento 1 (A/B entre grupo con dashboard y grupo sin dashboard). El MDE del 20% refleja un cambio observable con impacto directo en el volumen de pedidos innecesarios.

---

### 8.2.6. Methods Selection

En esta sección se describe cómo se llevará a cabo la investigación para la plataforma Restock. El diseño de cada intervención se rige por el principio fundamental de utilizar el **Simplest Useful Thing** (la cosa más simple y útil). Esto garantiza que se alcance el tamaño de muestra requerido y las condiciones necesarias con el menor esfuerzo de ingeniería posible, evitando el desarrollo de soluciones definitivas antes de validar el aprendizaje.

Es vital establecer la diferencia clara entre el **objeto de investigación** (la pregunta de negocio o hipótesis que queremos responder) y el **método** (la técnica o herramienta específica elegida para ejecutar la prueba, como un A/B Test o un Concierge Test).

A continuación, se detallan los métodos seleccionados para cada experimento:

* **Experimento 01 (Impacto de Alertas en Mermas):**

  * **Objeto:** Evaluar si las notificaciones automáticas previenen el desperdicio de insumos.
  * **Método (Simplest Useful Thing):** *A/B Testing* mediante un piloto operativo. Se activarán las notificaciones push nativas utilizando Firebase/OneSignal solo para la cohorte experimental, comparando sus niveles de merma contra un grupo de control que no recibirá alertas.
* **Experimento 02 (Eficacia del Onboarding):**

  * **Objeto:** Validar la autonomía de los administradores con baja afinidad digital al realizar su primer pedido.
  * **Método (Simplest Useful Thing):** *Prueba de Usabilidad Remota Moderada*. En lugar de programar un complejo sistema de tutoriales dinámicos, se observará a los usuarios interactuar en tiempo real con el flujo de primer pedido, capturando su *Task Success Rate* en la primera sesión.
* **Experimento 03 (Integración de Proveedores):**

  * **Objeto:** Determinar la disposición de los proveedores tradicionales a digitalizar sus catálogos.
  * **Método (Simplest Useful Thing):** *Concierge Test (Prueba de Conserje)*. En lugar de desarrollar un portal de autogestión para proveedores, el equipo de Restock subirá manualmente el catálogo de 3 proveedores al sistema y les hará una demostración en vivo de la gestión de pedidos para medir su intención real de adopción.
* **Experimento 04 (Indicadores de Rotación):**

  * **Objeto:** Analizar si la visualización de métricas históricas influye en la reducción del sobrestock.
  * **Método (Simplest Useful Thing):** *Feature Flagging (A/B Testing)*. Se añadirá una columna estática básica en la vista de Angular llamada "Rotación" (Alta/Media/Baja), calculada previamente por el equipo. Mediante un *feature flag*, esta columna solo será visible para el grupo experimental durante su cierre semanal.

#### Consideraciones Normativas y Éticas

Para garantizar la integridad técnica y moral del proceso de experimentación, el equipo aplicará dos directrices inquebrantables:

1. **Prevención de Simultaneidad:** Se prohíbe estrictamente ejecutar dos o más experimentos sobre el mismo tema o módulo al mismo tiempo. Ningún usuario (restaurante o proveedor) será expuesto a múltiples intervenciones superpuestas, evitando así la contaminación cruzada de los datos y asegurando que los cambios de comportamiento sean atribuibles a una única variable.
2. **Consideración Ética (No causar daño):** Los experimentos se han diseñado para no generar ningún impacto negativo, pérdida de datos críticos o perjuicio económico en las operaciones reales de los restaurantes y proveedores. Las intervenciones se limitan a ofrecer asistencia, enviar alertas preventivas o mostrar información adicional, manteniendo siempre protegida la confidencialidad de la información comercial de ambas partes.

### 8.2.7. Data Analytics: Goals, KPIs and Metrics Selection

En esta sección se define la estrategia de recolección de datos necesaria para responder a las preguntas de investigación. Siguiendo la filosofía XDPD, se seleccionaron un conjunto mínimo de medidas para garantizar la eficiencia operativa y la precisión en la detección de cambios significativos, evitando la acumulación de datos irrelevantes o "vanity metrics".

**1. Metas de Análisis (Goals)**

El objetivo principal de la analítica es transformar las interacciones de los usuarios en el ecosistema Restock en conocimiento validado sobre:

* La efectividad de la automatización en la gestión de inventarios.
* La autonomía del usuario tradicional en flujos digitales críticos.
* La intención de migración digital por parte de proveedores tradicionales.
* La influencia de los analíticos en la precisión de la toma de decisiones.

**2. Selección de KPIs y Métricas**

Para asegurar que las métricas permitan detectar cambios precisos, se estructura la selección en los siguientes niveles:

| Nivel             | Nombre del Indicador               | Métrica Atómica (Data Point)                                                 | Justificación de Selección (Economy of Tracking)                                      |
| ----------------- | ---------------------------------- | ------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------- |
| KPI de Negocio    | Tasa de Reducción de Mermas       | Peso (kg/l) de insumos desechados por semana.                                  | Directamente vinculado a la propuesta de valor core de ahorro del 35%.                  |
| KPI de Adopción  | Task Success Rate (TSR)            | Booleano (éxito/fallo) en el primer pedido.                                   | Métrica binaria simple que elimina la ambigüedad sobre la usabilidad del onboarding.  |
| KPI de Ecosistema | Tasa de Conversión de Proveedores | Número de firmas de intención vs. total contactados.                         | Permite validar la viabilidad del mercado B2B con el menor esfuerzo de rastreo posible. |
| KPI Estratégico  | Precisión de Compra               | % de líneas de pedido corregidas tras ver reportes.                           | Mide si los datos realmente influyen en el usuario.                                     |
| Métrica de Salud | Latencia de Alerta Push            | Tiempo (ms) desde el evento de stock bajo hasta el envío de la notificación. | Asegura que la tecnología no sea un obstáculo para la experiencia del usuario.        |

**3. Estrategia de Economía de Datos**

En cumplimiento con el requisito de economía en el rastreo, se decide:

* Rastreo Temporal: Las métricas de comportamiento (onboarding) solo se capturarán durante la sesión inicial de los sujetos de prueba.
* Focalización: No se rastrearán eventos de navegación general (clics en "Acerca de nosotros") para evitar el ruido en el análisis de las hipótesis críticas.
* Herramientas Seleccionadas: Se usará Firebase Analytics para la consolidación de reportes, permitiendo una visualización limpia sin necesidad de procesar datos crudos masivos.

**4. Evidencias de preparación analítica**

Habilitación de Google Analytics en Firebase:

<img src="assets/images/chapter8/data-analytics/1-firebase-analytics.png" width="600px" alt="Habilitacion de google analytics">

Integración del archivo google-services.json en Android Studio:

<img src="assets/images/chapter8/data-analytics/2-google-services.png" width="600px" alt="Integracion google services">

Definición de eventos analíticos en Kotlin:

<img src="assets/images/chapter8/data-analytics/3-eventos-kotlin.png" width="600px" alt="Eventos en kotlin">

Ejecución de la app y activación de DebugView:

<img src="assets/images/chapter8/data-analytics/4-ejecucion-app.png" width="600px" alt="Ejecucion app kotlin">

Validación de eventos en Firebase DebugView:

<img src="assets/images/chapter8/data-analytics/5-firebase-debugview.png" width="600px" alt="Firebase debug view">

### 8.2.8. Web and Mobile Tracking Plan

El Plan de Rastreo define qué eventos se capturarán, en qué plataforma y durante qué ventana de tiempo, en cumplimiento con el principio de **economía de rastreo** establecido en 8.2.3. El objetivo es instrumentar únicamente los eventos que responden directamente a las hipótesis definidas en 8.2.1, evitando acumular datos de navegación general que generen ruido o costos innecesarios de infraestructura.

La herramienta central es **Firebase Analytics**, cuya integración con la aplicación móvil Kotlin ya fue verificada en 8.2.7. Para el frontend web Angular, los eventos se emiten desde los componentes afectados por los experimentos y se envían al mismo proyecto de Firebase mediante el SDK web.

---

#### Catálogo de Eventos — Aplicación Móvil (Kotlin / Android)

Los eventos móviles cubren los Experimentos 01 y 02, ya que ambos ocurren sobre la app nativa Kotlin donde ya está integrado Firebase Analytics.

| Evento                        | Experimento | Disparador                                                                          | Parámetros clave                                               | Ventana activa              |
| ----------------------------- | :---------: | ----------------------------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------- |
| `notification_received`     |   Exp 01   | El sistema operativo Android entrega la notificación push de alerta de stock       | `notification_type` (stock_low / expiry), `supply_id`       | 14 días (Exp 01)           |
| `notification_clicked`      |   Exp 01   | El usuario toca la notificación push recibida                                      | `notification_type`, `supply_id`, `timestamp_ms`          | 14 días (Exp 01)           |
| `order_created_after_alert` |   Exp 01   | El usuario confirma una orden dentro de las 2 horas siguientes a recibir una alerta | `supply_id`, `alert_type`, `time_delta_minutes`           | 14 días (Exp 01)           |
| `onboarding_step_viewed`    |   Exp 02   | El usuario llega a un paso del flujo de onboarding guiado                           | `step_number` (1–5), `step_name`                           | Primera sesión del usuario |
| `onboarding_step_completed` |   Exp 02   | El usuario avanza al siguiente paso del onboarding                                  | `step_number`, `time_on_step_seconds`                       | Primera sesión del usuario |
| `onboarding_abandoned`      |   Exp 02   | La app pasa a segundo plano o se cierra sin completar el onboarding                 | `last_step_number`, `total_time_seconds`                    | Primera sesión del usuario |
| `first_order_submitted`     |   Exp 02   | El usuario envía su primer pedido (botón de confirmación)                        | `total_time_seconds`, `assisted` (boolean), `error_count` | Primera sesión del usuario |

#### Catálogo de Eventos — Aplicación Web (Angular)

Los eventos web cubren el Experimento 04. Se instrumentan en el componente de la tabla de inventario del módulo *Overview*, activados únicamente para el grupo experimental mediante *feature flag*.

| Evento                            | Experimento | Disparador                                                                     | Parámetros clave                                                      | Ventana activa                         |
| --------------------------------- | :---------: | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------- | -------------------------------------- |
| `rotation_column_viewed`        |   Exp 04   | El componente de tabla con la columna "Rotación" termina de renderizar        | `user_id`, `items_visible`                                         | Día de cierre semanal del restaurante |
| `rotation_level_hovered`        |   Exp 04   | El cursor permanece más de 1 segundo sobre una celda de rotación             | `supply_id`, `rotation_level` (Alta/Media/Baja), `dwell_time_ms` | Día de cierre semanal                 |
| `order_quantity_entered`        |   Exp 04   | El usuario introduce o modifica una cantidad en el campo de cantidad de pedido | `supply_id`, `rotation_level`, `quantity_entered`                | Día de cierre semanal                 |
| `low_rotation_item_removed`     |   Exp 04   | El usuario elimina un ítem de baja rotación del carrito antes del checkout   | `supply_id`, `quantity_removed`                                    | Día de cierre semanal                 |
| `order_submitted_with_rotation` |   Exp 04   | El usuario confirma la orden habiendo tenido la columna de rotación visible   | `low_rotation_items_count`, `total_items`, `total_quantity`      | Día de cierre semanal                 |

---

#### Ventanas de Activación por Experimento

| Experimento            | Plataforma       | Inicio del rastreo                                  | Fin del rastreo                    | Criterio de apagado                                                        |
| ---------------------- | ---------------- | --------------------------------------------------- | ---------------------------------- | -------------------------------------------------------------------------- |
| Exp 01 — Alertas push | Kotlin / Android | Día 1 del piloto (grupo experimental)              | Día 14 del piloto                 | Al completarse los 14 días o al alcanzar n=5 en el grupo                  |
| Exp 02 — Onboarding   | Kotlin / Android | Primera apertura de la app por el usuario de prueba | Confirmación del primer pedido    | Evento`first_order_submitted` recibido (apagado automático por cohorte) |
| Exp 03 — Concierge    | N/A              | N/A                                                 | N/A                                | Medición cualitativa manual; no requiere telemetría digital              |
| Exp 04 — Rotación    | Angular (Web)    | Día del cierre semanal del grupo experimental      | Al finalizar la sesión del cierre | Flag apagado automáticamente al terminar la sesión de inventario         |

---

#### Reglas de Economía de Rastreo

1. **Sin rastreo cruzado:** Los eventos del Exp 01 no se activan para usuarios del Exp 02, y viceversa. El SDK diferencia usuarios mediante el parámetro `experiment_id` en las propiedades de usuario de Firebase.
2. **Sin rastreo de navegación general:** No se capturan eventos de tipo *page_view*, *scroll* ni *session_start* fuera de los módulos instrumentados. Solo se activan los eventos del catálogo anterior.
3. **Apagado automático:** Los eventos del Exp 02 se desactivan al recibir `first_order_submitted`, sin necesidad de intervención manual.
4. **Feature flag para Exp 04:** La columna de rotación y sus eventos asociados se controlan mediante un *feature flag* booleano en Angular. El flag solo está activo para los usuarios asignados al grupo experimental durante su día de cierre semanal.

## 8.3. Experimentation

### 8.3.1. To-Be User Stories

Las siguientes historias de usuario amplían el catálogo establecido en el capítulo 3 (US-01 a US-36). Cada historia representa una funcionalidad específica que debe implementarse como *Simplest Useful Thing* para ejecutar uno de los experimentos definidos en 8.2.6. Los IDs continúan la numeración existente (US-37 en adelante) y se vinculan a las epics del capítulo 3.

<table border="1" cellpadding="8" cellspacing="0" width="100%" style="margin-bottom:18px;">
  <thead>
    <tr>
      <th>Story ID</th>
      <th>User</th>
      <th>Priority</th>
      <th>Epic</th>
    </tr>
    <tr>
      <td>US-37</td>
      <td>Administrador de restaurante</td>
      <td>High</td>
      <td>EP-10</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Title</strong></td>
      <td colspan="3">Notificaciones push automáticas de inventario en dispositivo móvil</td>
    </tr>
    <tr>
      <td colspan="4" align="left"><strong>Description</strong><br/>
      Como administrador de restaurante, quiero recibir una notificación push en mi dispositivo móvil cuando un insumo alcance su stock mínimo o tenga fecha de vencimiento en los próximos 5 días, para actuar de forma preventiva sin tener que revisar activamente el inventario.</td>
    </tr>
    <tr>
      <td colspan="4" align="left"><strong>Acceptance Criteria</strong>
        <ul>
          <li><strong>Escenario 1: Notificación por stock bajo.</strong><br/>
          Dado que un insumo registrado tiene definido un stock mínimo,<br/>
          cuando el stock actual cae por debajo de dicho umbral,<br/>
          entonces el sistema envía una notificación push al dispositivo del administrador indicando el nombre del insumo y el nivel actual de stock.</li>
          <li><strong>Escenario 2: Notificación por vencimiento próximo.</strong><br/>
          Dado que un insumo tiene una fecha de vencimiento registrada,<br/>
          cuando faltan 5 días o menos para su vencimiento,<br/>
          entonces el sistema envía una notificación push al dispositivo del administrador indicando el nombre del insumo y la fecha de vencimiento.</li>
          <li><strong>Escenario 3: Navegación desde la notificación.</strong><br/>
          Dado que el administrador recibe la notificación push,<br/>
          cuando la toca,<br/>
          entonces la app abre directamente la vista del insumo afectado dentro del módulo de inventario.</li>
          <li><strong>Escenario 4: Sin notificación si el stock es suficiente.</strong><br/>
          Dado que un insumo tiene stock por encima del mínimo y su fecha de vencimiento es mayor a 5 días,<br/>
          cuando el sistema realiza la verificación periódica,<br/>
          entonces no se genera ninguna notificación push para ese insumo.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

<table border="1" cellpadding="8" cellspacing="0" width="100%" style="margin-bottom:18px;">
  <thead>
    <tr>
      <th>Story ID</th>
      <th>User</th>
      <th>Priority</th>
      <th>Epic</th>
    </tr>
    <tr>
      <td>US-38</td>
      <td>Nuevo usuario administrador de restaurante</td>
      <td>High</td>
      <td>EP-03</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Title</strong></td>
      <td colspan="3">Flujo de onboarding guiado para el primer pedido</td>
    </tr>
    <tr>
      <td colspan="4" align="left"><strong>Description</strong><br/>
      Como nuevo usuario administrador de restaurante, quiero seguir un flujo de onboarding guiado paso a paso al usar la aplicación móvil por primera vez, para poder completar mi primer pedido de forma autónoma en menos de 5 minutos sin necesitar asistencia externa.</td>
    </tr>
    <tr>
      <td colspan="4" align="left"><strong>Acceptance Criteria</strong>
        <ul>
          <li><strong>Escenario 1: Inicio automático del onboarding en primera sesión.</strong><br/>
          Dado que el usuario inicia sesión por primera vez en la aplicación,<br/>
          cuando accede al módulo principal,<br/>
          entonces el sistema muestra automáticamente el primer paso del flujo de onboarding guiado sin necesidad de acción adicional.</li>
          <li><strong>Escenario 2: Progresión paso a paso con indicador de avance.</strong><br/>
          Dado que el usuario se encuentra en el flujo de onboarding,<br/>
          cuando completa cada paso (registrar insumo, seleccionar proveedor, confirmar pedido),<br/>
          entonces el sistema muestra un indicador de progreso y lo lleva automáticamente al siguiente paso.</li>
          <li><strong>Escenario 3: Confirmación del primer pedido como finalización del onboarding.</strong><br/>
          Dado que el usuario ha completado todos los pasos del onboarding,<br/>
          cuando confirma su primer pedido,<br/>
          entonces el sistema registra la finalización del onboarding y muestra un mensaje de bienvenida.</li>
          <li><strong>Escenario 4: Omisión del onboarding en sesiones posteriores.</strong><br/>
          Dado que el usuario ya completó el primer pedido,<br/>
          cuando vuelve a iniciar sesión en la aplicación,<br/>
          entonces el sistema no vuelve a mostrar el flujo de onboarding guiado.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

<table border="1" cellpadding="8" cellspacing="0" width="100%" style="margin-bottom:18px;">
  <thead>
    <tr>
      <th>Story ID</th>
      <th>User</th>
      <th>Priority</th>
      <th>Epic</th>
    </tr>
    <tr>
      <td>US-39</td>
      <td>Proveedor de insumos (sin experiencia digital)</td>
      <td>Medium</td>
      <td>EP-13</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Title</strong></td>
      <td colspan="3">Carga asistida del catálogo de productos del proveedor</td>
    </tr>
    <tr>
      <td colspan="4" align="left"><strong>Description</strong><br/>
      Como proveedor de insumos sin experiencia en herramientas digitales, quiero que el equipo de Restock cargue mi catálogo de productos en la plataforma durante una sesión de demostración asistida, para comenzar a recibir pedidos digitalmente sin barreras técnicas y evaluar si el sistema se adapta a mi operación.</td>
    </tr>
    <tr>
      <td colspan="4" align="left"><strong>Acceptance Criteria</strong>
        <ul>
          <li><strong>Escenario 1: Carga exitosa de productos por parte del equipo Restock.</strong><br/>
          Dado que el equipo tiene acceso al perfil del proveedor y la lista de productos proporcionada,<br/>
          cuando registra cada producto con nombre, precio unitario y unidad de medida,<br/>
          entonces los productos quedan visibles en el catálogo del proveedor dentro de la plataforma.</li>
          <li><strong>Escenario 2: El proveedor visualiza su catálogo cargado.</strong><br/>
          Dado que los productos fueron cargados por el equipo,<br/>
          cuando el proveedor accede a su módulo de gestión de productos,<br/>
          entonces ve el listado completo con la información ingresada y puede confirmar su exactitud.</li>
          <li><strong>Escenario 3: Recepción de un pedido de prueba durante la demostración.</strong><br/>
          Dado que el catálogo está cargado y el equipo simula un pedido desde una cuenta de restaurante,<br/>
          cuando el proveedor accede al módulo de órdenes,<br/>
          entonces visualiza el pedido simulado con el detalle de productos, cantidades y restaurante solicitante.</li>
          <li><strong>Escenario 4: Registro de intención de uso al finalizar la sesión.</strong><br/>
          Dado que la demostración ha concluido,<br/>
          cuando el proveedor confirma su disposición a continuar usando la plataforma,<br/>
          entonces el sistema registra la sesión como una conversión positiva en el módulo de seguimiento del equipo.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

<table border="1" cellpadding="8" cellspacing="0" width="100%" style="margin-bottom:18px;">
  <thead>
    <tr>
      <th>Story ID</th>
      <th>User</th>
      <th>Priority</th>
      <th>Epic</th>
    </tr>
    <tr>
      <td>US-40</td>
      <td>Administrador de restaurante</td>
      <td>Medium</td>
      <td>EP-06</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Title</strong></td>
      <td colspan="3">Indicador de nivel de rotación por insumo en el módulo de inventario</td>
    </tr>
    <tr>
      <td colspan="4" align="left"><strong>Description</strong><br/>
      Como administrador de restaurante, quiero ver el nivel de rotación (Alta / Media / Baja) de cada insumo en la tabla del módulo de inventario, para tomar decisiones más precisas al generar mis órdenes de compra y evitar el sobrestock de insumos con baja demanda.</td>
    </tr>
    <tr>
      <td colspan="4" align="left"><strong>Acceptance Criteria</strong>
        <ul>
          <li><strong>Escenario 1: Visualización de la columna de rotación.</strong><br/>
          Dado que el administrador accede al módulo de inventario con el indicador de rotación habilitado,<br/>
          cuando se carga la tabla de insumos,<br/>
          entonces cada fila muestra una etiqueta de rotación (Alta / Media / Baja) calculada a partir del historial de consumo.</li>
          <li><strong>Escenario 2: Etiqueta de rotación consistente con el historial.</strong><br/>
          Dado que un insumo tiene un bajo volumen de consumo en las últimas 4 semanas,<br/>
          cuando el administrador consulta la tabla,<br/>
          entonces la etiqueta del insumo muestra "Baja" y se resalta visualmente para atraer la atención del usuario.</li>
          <li><strong>Escenario 3: La columna no afecta la funcionalidad existente.</strong><br/>
          Dado que la columna de rotación está visible,<br/>
          cuando el administrador realiza acciones sobre el inventario (editar, agregar al pedido, filtrar),<br/>
          entonces todas las funcionalidades previas operan con normalidad sin interferencias.</li>
          <li><strong>Escenario 4: Columna invisible para el grupo de control (feature flag).</strong><br/>
          Dado que un administrador pertenece al grupo de control del experimento,<br/>
          cuando accede al módulo de inventario,<br/>
          entonces la columna de rotación no es visible en la tabla y la interfaz es idéntica a la versión previa.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### 8.3.2. To-Be Product Backlog

El siguiente backlog prioriza las cuatro historias de usuario To-Be derivadas directamente de los experimentos planificados. El orden de prioridad se determina por el puntaje total del Question Backlog (sección 8.1.4): Q1 (17 pts) > Q2 (16 pts) > Q3 (15 pts) > Q4 (13 pts). Las estimaciones de esfuerzo en Story Points siguen la misma escala de Fibonacci utilizada en el backlog del capítulo 3.

<table border="1" cellpadding="8" cellspacing="0" width="100%">
  <thead>
    <tr>
      <th># Order</th>
      <th>User Story ID</th>
      <th>Título</th>
      <th>Descripción</th>
      <th>Experimento vinculado</th>
      <th>Story Points</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>US-37</td>
      <td>Notificaciones push automáticas de inventario en dispositivo móvil</td>
      <td>Como administrador de restaurante, quiero recibir una notificación push en mi dispositivo móvil cuando un insumo alcance su stock mínimo o tenga fecha de vencimiento próxima, para actuar de forma preventiva sin revisar activamente el inventario.</td>
      <td>Experimento 01 — Validación de Impacto en Mermas (Q1, puntaje 17)</td>
      <td>3</td>
    </tr>
    <tr>
      <td>2</td>
      <td>US-38</td>
      <td>Flujo de onboarding guiado para el primer pedido</td>
      <td>Como nuevo usuario administrador de restaurante, quiero seguir un flujo de onboarding guiado paso a paso al usar la app por primera vez, para completar mi primer pedido de forma autónoma en menos de 5 minutos.</td>
      <td>Experimento 02 — Validación de Adopción Digital (Q2, puntaje 16)</td>
      <td>5</td>
    </tr>
    <tr>
      <td>3</td>
      <td>US-39</td>
      <td>Carga asistida del catálogo de productos del proveedor</td>
      <td>Como proveedor sin experiencia digital, quiero que el equipo de Restock cargue mi catálogo durante una sesión asistida, para comenzar a recibir pedidos digitalmente sin barreras técnicas.</td>
      <td>Experimento 03 — Viabilidad del Ecosistema de Proveedores (Q3, puntaje 15)</td>
      <td>2</td>
    </tr>
    <tr>
      <td>4</td>
      <td>US-40</td>
      <td>Indicador de nivel de rotación por insumo en el módulo de inventario</td>
      <td>Como administrador de restaurante, quiero ver el nivel de rotación (Alta / Media / Baja) de cada insumo en la tabla de inventario, para tomar decisiones más precisas al generar mis órdenes de compra.</td>
      <td>Experimento 04 — Comportamiento Basado en Datos (Q4, puntaje 13)</td>
      <td>2</td>
    </tr>
  </tbody>
</table>

### 8.3.3. Pipeline-supported, Experiment-Driven To-Be Software Platform  Lifecycle

#### 8.3.3.1. To-Be Sprint Backlogs

##### Sprint Backlog 4

El presente Sprint Backlog corresponde al sprint de experimentación To-Be de Restock. El objetivo principal del sprint es implementar las funcionalidades mínimas necesarias para ejecutar los experimentos definidos en la fase de Experiment-Driven Development: notificaciones push de inventario, onboarding guiado para el primer pedido, carga asistida de catálogo de proveedores e indicador de rotación en el módulo de inventario.

**Board Screenshot:**

<img src="assets/images/chapter8/to-be-sprint-backlog-4.png" alt="Board of Sprint Backlog 4 " width="600px">

**Board URL:** https://shorturl.at/cbftm

**Sprint #: Sprint 4**

| User Story Id | User Story Title                                                       | Work-Item / Task Id | Work-Item / Task Title                              | Description                                                                                                                                                               | Estimation (Hours) | Assigned To          | Status |
| ------------- | ---------------------------------------------------------------------- | ------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -----------------: | -------------------- | ------ |
| US-37         | Notificaciones push automáticas de inventario en dispositivo móvil   | T-37-01             | Configurar servicio de notificaciones push          | Configurar Firebase Cloud Messaging / OneSignal en la aplicación móvil para permitir el envío de alertas de stock bajo y vencimiento próximo.                         |                  4 | Gabriela N. Shapiama | Done   |
| US-37         | Notificaciones push automáticas de inventario en dispositivo móvil   | T-37-02             | Definir reglas de alerta de inventario              | Implementar la lógica que identifica insumos con stock por debajo del mínimo o con fecha de vencimiento dentro de los próximos 5 días.                                |                  5 | Julio D. Castro      | Done   |
| US-37         | Notificaciones push automáticas de inventario en dispositivo móvil   | T-37-03             | Construir payload de notificación                  | Definir el contenido de la notificación, incluyendo nombre del insumo, tipo de alerta, stock actual o fecha de vencimiento.                                              |                  3 | José J. Guerra      | Done   |
| US-37         | Notificaciones push automáticas de inventario en dispositivo móvil   | T-37-04             | Implementar navegación desde la notificación      | Habilitar que, al tocar la notificación, la aplicación móvil abra directamente la vista del insumo afectado.                                                           |                  4 | Gabriela N. Shapiama | Done   |
| US-37         | Notificaciones push automáticas de inventario en dispositivo móvil   | T-37-05             | Registrar eventos analíticos de alertas            | Registrar eventos`notification_received`, `notification_clicked` y `order_created_after_alert` para medir la conversión de alerta a orden.                         |                  3 | Ario Chavez          | Done   |
| US-37         | Notificaciones push automáticas de inventario en dispositivo móvil   | T-37-06             | Probar flujo de alerta de inventario                | Ejecutar pruebas funcionales para verificar que no se envían alertas cuando el stock es suficiente o el vencimiento no es próximo.                                      |                  3 | José J. Guerra      | Done   |
| US-38         | Flujo de onboarding guiado para el primer pedido                       | T-38-01             | Diseñar pasos del onboarding                       | Definir los pasos del flujo guiado: registro de insumo, selección de proveedor, creación y confirmación del primer pedido.                                             |                  4 | Fernando I. Sanchez  | Done   |
| US-38         | Flujo de onboarding guiado para el primer pedido                       | T-38-02             | Detectar primera sesión del usuario                | Implementar la validación que identifica si el administrador inicia sesión por primera vez en la aplicación móvil.                                                    |                  3 | Gabriela N. Shapiama | Done   |
| US-38         | Flujo de onboarding guiado para el primer pedido                       | T-38-03             | Implementar avance paso a paso                      | Desarrollar la navegación guiada entre los pasos del onboarding, mostrando el progreso hasta la confirmación del pedido.                                                |                  6 | Gabriela N. Shapiama | Done   |
| US-38         | Flujo de onboarding guiado para el primer pedido                       | T-38-04             | Persistir finalización del onboarding              | Registrar que el usuario completó su primer pedido para evitar que el onboarding vuelva a mostrarse en sesiones posteriores.                                             |                  4 | Julio D. Castro      | Done   |
| US-38         | Flujo de onboarding guiado para el primer pedido                       | T-38-05             | Registrar eventos del onboarding                    | Implementar los eventos`onboarding_step_viewed`, `onboarding_step_completed`, `onboarding_abandoned` y `first_order_submitted`.                                   |                  4 | Ario Chavez          | Done   |
| US-38         | Flujo de onboarding guiado para el primer pedido                       | T-38-06             | Preparar prueba de usabilidad                       | Elaborar el guion de prueba, criterios de observación y matriz para registrar tiempo en tarea, errores y éxito del primer pedido.                                       |                  3 | Fernando I. Sanchez  | Done   |
| US-38         | Flujo de onboarding guiado para el primer pedido                       | T-38-07             | Validar flujo móvil completo                       | Ejecutar pruebas del flujo de primer pedido verificando autonomía, continuidad del onboarding y ausencia de bloqueos críticos.                                          |                  4 | José J. Guerra      | Done   |
| US-39         | Carga asistida del catálogo de productos del proveedor                | T-39-01             | Definir plantilla de catálogo del proveedor        | Elaborar una plantilla con nombre de producto, precio unitario, unidad de medida y disponibilidad para cargar productos del proveedor.                                    |                  2 | Fernando I. Sanchez  | Done   |
| US-39         | Carga asistida del catálogo de productos del proveedor                | T-39-02             | Cargar productos de prueba en catálogo             | Registrar manualmente productos de proveedores seleccionados para simular la carga asistida durante el Concierge Test.                                                    |                  3 | Fernando I. Sanchez  | Done   |
| US-39         | Carga asistida del catálogo de productos del proveedor                | T-39-03             | Validar visualización del catálogo                | Verificar que el proveedor pueda visualizar el listado de productos cargados con información correcta en su módulo web.                                                 |                  3 | Ario Chavez          | Done   |
| US-39         | Carga asistida del catálogo de productos del proveedor                | T-39-04             | Simular pedido desde cuenta de restaurante          | Crear un pedido de prueba desde una cuenta de restaurante para que el proveedor visualice productos, cantidades y solicitante.                                            |                  3 | Julio D. Castro      | Done   |
| US-39         | Carga asistida del catálogo de productos del proveedor                | T-39-05             | Registrar intención de uso del proveedor           | Preparar el formulario o registro manual para documentar si el proveedor acepta continuar usando la plataforma después de la demostración.                              |                  2 | Ario Chavez          | Done   |
| US-40         | Indicador de nivel de rotación por insumo en el módulo de inventario | T-40-01             | Definir cálculo de rotación de insumos            | Establecer la regla de clasificación Alta, Media o Baja según el historial de consumo de las últimas semanas.                                                          |                  3 | Ario Chavez          | Done   |
| US-40         | Indicador de nivel de rotación por insumo en el módulo de inventario | T-40-02             | Agregar columna de rotación en inventario          | Implementar la columna Rotation en la tabla del módulo de inventario de la aplicación web.                                                                              |                  4 | Gabriela N. Shapiama | Done   |
| US-40         | Indicador de nivel de rotación por insumo en el módulo de inventario | T-40-03             | Implementar feature flag para grupo experimental    | Configurar que la columna de rotación sea visible únicamente para administradores asignados al grupo experimental.                                                      |                  4 | Julio D. Castro      | Done   |
| US-40         | Indicador de nivel de rotación por insumo en el módulo de inventario | T-40-04             | Mantener interfaz sin cambios para grupo de control | Verificar que los administradores del grupo de control visualicen la versión previa del inventario sin la columna de rotación.                                          |                  2 | José J. Guerra      | Done   |
| US-40         | Indicador de nivel de rotación por insumo en el módulo de inventario | T-40-05             | Registrar eventos de interacción con rotación     | Implementar eventos`rotation_column_viewed`, `rotation_level_hovered`, `order_quantity_entered`, `low_rotation_item_removed` y `order_submitted_with_rotation`. |                  4 | Ario Chavez          | Done   |
| US-40         | Indicador de nivel de rotación por insumo en el módulo de inventario | T-40-06             | Probar comportamiento del indicador de rotación    | Validar que la columna no interfiera con acciones existentes como edición, filtrado, agregado al pedido y confirmación de orden.                                        |                  3 | José J. Guerra      | Done   |

#### 8.3.3.2. Implemented To-Be Landing Page Evidence

#### 8.3.3.3. Implemented To-Be Frontend-Web Application Evidence

#### 8.3.3.4. Implemented To-Be Native-Mobile Application Evidence

#### 8.3.3.5. Implemented To-Be RESTful API and/or Serverless Backend Evidence

En esta sección se presenta la evidencia de implementación del backend RESTful correspondiente al Sprint Backlog 4 de experimentación To-Be. Los cambios realizados en el backend permiten dar soporte a las historias de usuario experimentales definidas anteriormente: notificaciones automáticas de inventario, estado de activación para el primer pedido, carga asistida del catálogo de proveedores e indicador de rotación por insumo.

El objetivo de esta implementación no fue construir módulos finales de alta complejidad, sino habilitar los endpoints necesarios para ejecutar y evidenciar los experimentos definidos en el ciclo Experiment-Driven Development. Por ello, los endpoints implementados se enfocan en exponer datos accionables para la aplicación web y móvil, permitiendo validar hipótesis asociadas a reducción de mermas, adopción digital, digitalización de proveedores y toma de decisiones basada en datos.

##### Backend Repository Evidence

| Repository       | Branch            | Commit Id | Commit Message                                                       | Committed on (Date) |
| :--------------- | :---------------- | :-------- | :------------------------------------------------------------------- | :------------------ |
| restock-platform | feature/orders    | 987a2be   | feat(iam): add parameter activation state for first order onboarding | 03/07/2026          |
| restock-platform | feature/inventory | 62b92c0   | feat(resource): add endpoint for upload custom supplies catalog      | 03/07/2026          |
| restock-platform | feature/inventory | 4ea56cf   | feat(resource): add push notification resource                       | 03/07/2026          |
| restock-platform | feature/inventory | c6d35d1   | feat(resource): add inventory rotation resource and endpoint         | 03/07/2026          |

<img src="assets/images/chapter8/to-be-backend/backend_repository_commits.png" width="700px" alt="backend repository commits for to-be experiment sprint">

##### Implemented Backend Features by To-Be User Story

###### US-37 — Notificaciones push automáticas de inventario en dispositivo móvil

Para la historia US-37, se implementó un recurso orientado a identificar insumos candidatos a generar alertas automáticas de inventario. Esta funcionalidad permite detectar situaciones relevantes para el experimento de reducción de mermas, principalmente insumos con riesgo operativo por stock bajo o vencimiento próximo.

El endpoint implementado expone los candidatos a notificación para que la aplicación móvil o el servicio de notificaciones pueda utilizarlos como base.

| Method | Endpoint                                                           | Description                                                                                                                                                           | Related User Story |
| :----- | :----------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------- |
| GET    | `/api/v1/inventory/users/{userId}/push-notifications-candidates` | Obtiene los candidatos a notificación automática de inventario para un usuario, considerando insumos que requieren atención por stock bajo o vencimiento próximo. | US-37              |

Este endpoint contribuye al experimento porque permite obtener la evidencia base para validar si las alertas automáticas pueden ayudar al administrador a actuar preventivamente sobre insumos en riesgo. Además, permite sustentar técnicamente la existencia de una fuente backend para generar alertas de inventario.

###### US-38 — Flujo de onboarding guiado para el primer pedido

Para la historia US-38, el backend no implementa el flujo visual del onboarding, ya que este pertenece a la experiencia de usuario en el frontend. Sin embargo, se incorporó soporte en el contexto de IAM para exponer un parámetro relacionado con el estado de activación del usuario frente a su primer pedido.

Este cambio permite identificar si el usuario ya realizó la acción clave del negocio, es decir, completar o iniciar su primer pedido. De esta manera, la aplicación puede decidir si debe mostrar nuevamente el flujo guiado.

| Method | Endpoint                                    | Description                                                                                                                                                                | Related User Story |
| :----- | :------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------- |
| GET    | `/api/v1/users/{userId}/activation-state` | Se agregó un parámetro de estado de activación asociado al primer pedido, permitiendo que el frontend o mobile determine si corresponde mostrar el flujo de onboarding. | US-38              |

###### US-39 — Carga asistida del catálogo de productos del proveedor

Para la historia US-39, se implementó un endpoint que permite cargar insumos personalizados al catálogo del proveedor. Esta funcionalidad da soporte al experimento de viabilidad del ecosistema de proveedores, en el cual el equipo de Restock puede asistir al proveedor durante la digitalización inicial de su catálogo.

La carga asistida permite registrar productos con información relevante para que luego puedan ser visualizados y utilizados dentro del flujo de pedidos. Esto reduce la fricción inicial del proveedor tradicional, ya que no necesita realizar toda la configuración por sí mismo durante la primera sesión de demostración.

| Method | Endpoint                                   | Description                                                                                                                          | Related User Story |
| :----- | :----------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------- | :----------------- |
| POST   | `/api/v1/custom-supplies/catalog/upload` | Permite cargar productos o insumos personalizados al catálogo, facilitando la digitalización asistida del catálogo del proveedor. | US-39              |

Este endpoint contribuye directamente al Concierge Test definido para proveedores, ya que permite preparar o registrar un catálogo digital mínimo para demostrar cómo el proveedor podría recibir pedidos desde la plataforma.

###### US-40 — Indicador de nivel de rotación por insumo en el módulo de inventario

Para la historia US-40, se implementó un recurso backend de rotación de inventario. Este endpoint permite obtener el nivel de rotación de los insumos asociados a un usuario, información que será consumida por la aplicación web para mostrar una columna de rotación en el módulo de inventario.

La funcionalidad permite clasificar los insumos según su comportamiento de consumo o movimiento, devolviendo información útil para que el administrador tome decisiones de compra más precisas. Esto soporta el experimento de comportamiento basado en datos, orientado a validar si mostrar indicadores de rotación influye en la reducción de sobrestock.

| Method | Endpoint                                      | Description                                                                                            | Related User Story |
| :----- | :-------------------------------------------- | :----------------------------------------------------------------------------------------------------- | :----------------- |
| GET    | `/api/v1/inventory/users/{userId}/rotation` | Obtiene el nivel de rotación de inventario por insumo para apoyar decisiones de compra y reposición. | US-40              |

Este endpoint permite que la aplicación web muestre información de rotación en el inventario y sustenta la hipótesis de que los administradores pueden tomar mejores decisiones cuando reciben datos operativos claros antes de generar una orden de compra.

##### Swagger / OpenAPI Evidence

La documentación de los nuevos endpoints fue expuesta mediante Swagger UI, permitiendo validar las rutas implementadas y su disponibilidad para consumo desde las aplicaciones cliente. En la categoría **Inventory Insights**, se evidencian los endpoints asociados a rotación de inventario y candidatos de notificaciones push.

| Swagger Section    | Endpoint                                                               | Purpose                                                                 |
| :----------------- | :--------------------------------------------------------------------- | :---------------------------------------------------------------------- |
| Inventory Insights | `GET /api/v1/inventory/users/{userId}/rotation`                      | Consultar el nivel de rotación de inventario por insumo.               |
| Inventory Insights | `GET /api/v1/inventory/users/{userId}/push-notifications-candidates` | Consultar candidatos de notificación automática de inventario.        |
| Custom Supplies    | `POST /api/v1/custom-supplies/catalog/upload`                        | Cargar productos del catálogo del proveedor de forma asistida.         |
| Users              | `GET /api/v1/users/{userId}/activation-state`                        | Exponer estado de activación relacionado al primer pedido del usuario. |

<img src="assets/images/chapter8/to-be-backend/inventory_insights_swagger.png" width="600px" alt="swagger evidence for inventory insights endpoints">

##### Backend Deployment Evidence

El backend se mantiene desplegado en Render, permitiendo el acceso público a la documentación Swagger y la validación de los endpoints implementados para el Sprint Backlog 4. El despliegue permite que los servicios RESTful puedan ser consumidos por la aplicación web y móvil durante la ejecución de los experimentos To-Be.

**Link de despliegue del backend:**
[https://restock-platform-10253.onrender.com/swagger-ui/index.html](https://restock-platform-10253.onrender.com/swagger-ui/index.html)

<img src="assets/images/chapter8/to-be-backend/backend_swagger_deployment.png" width="600px" alt="to-be backend swagger deployment evidence">

##### Summary of Implemented To-Be RESTful API Support

| To-Be User Story                                                 | Backend Evidence                                                             | Experiment Supported                                        |
| :--------------------------------------------------------------- | :--------------------------------------------------------------------------- | :---------------------------------------------------------- |
| US-37 — Notificaciones push automáticas de inventario          | Endpoint para obtener candidatos de notificación de inventario por usuario. | Experimento 01 — Validación de impacto en mermas.         |
| US-38 — Flujo de onboarding guiado para el primer pedido        | Parámetro de estado de activación relacionado con el primer pedido.        | Experimento 02 — Validación de adopción digital.         |
| US-39 — Carga asistida del catálogo de productos del proveedor | Endpoint para carga asistida de insumos personalizados al catálogo.         | Experimento 03 — Viabilidad del ecosistema de proveedores. |
| US-40 — Indicador de nivel de rotación por insumo              | Endpoint para consultar rotación de inventario por insumo.                  | Experimento 04 — Comportamiento basado en datos.           |

Con estos cambios, el backend RESTful de Restock queda alineado con el Sprint Backlog 4 y proporciona soporte técnico suficiente para ejecutar los experimentos To-Be. Las funcionalidades implementadas permiten recolectar evidencia operativa sobre alertas, activación del usuario, digitalización de proveedores y decisiones de compra basadas en indicadores de inventario.

#### 8.3.3.6. Team Collaboration Insights

### 8.3.4. To-Be Validation Interviews

#### 8.3.4.1. Diseño de Entrevistas

Para garantizar que las funcionalidades To-Be implementadas en Restock respondan a las necesidades reales de los usuarios finales, se diseñó un proceso de entrevistas de validación centrado en los dos segmentos objetivo del proyecto: administradores de restaurantes y proveedores de insumos. Cada sesión incluirá interacción con el Landing Page, la aplicación web y las aplicaciones móviles correspondientes a cada segmento.

A diferencia de la validación anterior, esta etapa se enfoca en evaluar las funcionalidades implementadas para el ciclo de Experiment-Driven Development, especialmente aquellas relacionadas con las To-Be User Stories US-37, US-38, US-39 y US-40. Por ello, las entrevistas buscarán recoger evidencia cualitativa sobre la comprensión, utilidad percibida, facilidad de uso y viabilidad operativa de las funcionalidades experimentales: notificaciones automáticas de inventario, onboarding guiado para el primer pedido, carga asistida del catálogo del proveedor e indicador de rotación por insumo.

### Objetivo General

Validar la usabilidad, comprensión y utilidad de las funcionalidades To-Be de Restock a través de sesiones controladas de interacción con usuarios reales de los segmentos objetivo, aplicando principios de evaluación heurística y recogiendo observaciones cualitativas que permitan complementar el análisis de los experimentos definidos en el ciclo de Experiment-Driven Development.

### Objetivos Específicos

- Evaluar si los administradores de restaurantes comprenden y consideran útiles las notificaciones automáticas por stock bajo o vencimiento próximo.
- Validar si el flujo guiado permite que un nuevo administrador pueda completar su primer pedido de forma autónoma.
- Evaluar si el indicador de rotación por insumo es comprendido por los administradores y si influye en sus decisiones de compra.
- Validar si los proveedores de insumos perciben valor en la carga asistida de su catálogo y en la recepción de pedidos dentro de la plataforma.
- Identificar problemas de usabilidad, arquitectura de información e inclusive design durante la interacción con las funcionalidades To-Be.
- Recoger comentarios cualitativos que permitan sustentar la interpretación posterior de los resultados de experimentación.

### Segmento 1: Administradores de Restaurantes

#### Elementos a validar

- Claridad del valor ofrecido en el Landing Page.
- Comprensión del beneficio de reducción de mermas mediante alertas automáticas.
- Flujo de suscripción y acceso inicial a la plataforma.
- Registro, edición y revisión de insumos en el inventario.
- Visualización de alertas por stock bajo o vencimiento próximo.
- Uso de la aplicación móvil para recibir o revisar alertas de inventario.
- Flujo guiado para completar el primer pedido de insumos.
- Visualización y selección de proveedores.
- Realización y seguimiento de pedidos.
- Panel de alertas, resumen e indicadores.
- Comprensión del indicador de rotación Alta / Media / Baja.
- Uso del indicador de rotación para tomar decisiones de compra.
- Gestión complementaria de ventas y recetas, como flujos relacionados al consumo de inventario.

#### Flujos de Usuario a evaluar

- Desktop & Mobile User Flow 1: Suscripción y pago con Stripe.
- Desktop & Mobile User Flow 3: Registro y gestión de insumos.
- Desktop & Mobile User Flow 4: Resumen e indicadores.
- Desktop & Mobile User Flow 5: Visualización de proveedores y productos.
- Desktop & Mobile User Flow 6: Seguimiento de pedidos.
- Desktop & Mobile User Flow 7: Comentarios a proveedores.
- Desktop & Mobile User Flow 8: Registro y visualización de ventas.
- Desktop & Mobile User Flow 9: Creación y gestión de recetas.

#### Relación con funcionalidades To-Be

| Funcionalidad To-Be | User Story relacionada | User Flow existente asociado | Propósito dentro de la entrevista |
| :--- | :--- | :--- | :--- |
| Notificaciones automáticas de inventario | US-37 | Desktop & Mobile User Flow 3 y User Flow 4 | Validar si el administrador comprende las alertas por stock bajo o vencimiento próximo y si sabe qué acción tomar. |
| Onboarding guiado para el primer pedido | US-38 | Desktop & Mobile User Flow 5 y User Flow 6 | Validar si el administrador puede seleccionar proveedor y completar su primer pedido con mínima asistencia. |
| Indicador de rotación por insumo | US-40 | Desktop & Mobile User Flow 3 y User Flow 4 | Validar si el administrador entiende la rotación Alta, Media o Baja y si esta información influye en su decisión de compra. |
| Relación ventas, recetas e inventario | Validación complementaria | Desktop & Mobile User Flow 8 y User Flow 9 | Validar si el usuario comprende cómo las ventas y recetas se relacionan con el consumo de insumos. |

#### Actividades durante la sesión

- Navegar el Landing Page y explicar con sus propias palabras qué entiende sobre Restock.
- Identificar si el mensaje del Landing Page comunica correctamente la reducción de mermas, el control de inventario y la conexión con proveedores.
- Simular una suscripción desde un plan disponible.
- Ingresar a la plataforma como administrador de restaurante.
- Acceder al módulo de inventario siguiendo el Desktop & Mobile User Flow 3.
- Registrar, editar o revisar insumos registrados en el inventario.
- Revisar alertas generadas por stock bajo o vencimiento próximo.
- Explicar qué acción tomaría al recibir una alerta automática de inventario.
- Acceder al panel de resumen e indicadores siguiendo el Desktop & Mobile User Flow 4.
- Revisar el indicador de rotación de insumos y explicar qué entiende por rotación Alta, Media o Baja.
- Modificar o decidir una cantidad de compra considerando el indicador de rotación mostrado.
- Navegar por proveedores y productos siguiendo el Desktop & Mobile User Flow 5.
- Simular la creación de un primer pedido a proveedor como parte del flujo guiado.
- Revisar el seguimiento de un pedido siguiendo el Desktop & Mobile User Flow 6.
- Realizar un comentario o calificación sobre un proveedor siguiendo el Desktop & Mobile User Flow 7.
- Registrar o revisar una venta siguiendo el Desktop & Mobile User Flow 8.
- Crear o revisar una receta siguiendo el Desktop & Mobile User Flow 9.
- Usar la aplicación móvil de restaurantes para revisar inventario, alertas o pedidos.

#### Preguntas guía para administradores

- ¿Qué problema crees que busca resolver Restock para tu restaurante?
- ¿La alerta de stock bajo o vencimiento próximo fue clara para ti?
- Después de ver la alerta, ¿supiste qué acción tomar?
- ¿El flujo para realizar el primer pedido te pareció fácil de seguir?
- ¿En qué parte del pedido necesitaste más ayuda o explicación?
- ¿Entendiste qué significa que un insumo tenga rotación Alta, Media o Baja?
- ¿Cambiarías la cantidad de compra de un insumo si el sistema indica que tiene baja rotación?
- ¿Confiarías en estos indicadores para tomar decisiones reales de compra?
- ¿Qué información adicional necesitarías para sentirte seguro usando la plataforma?
- ¿Usarías Restock en la operación diaria de tu restaurante? ¿Por qué?

---

### Segmento 2: Proveedores de Restaurantes

#### Elementos a validar

- Claridad del valor ofrecido en el Landing Page para proveedores.
- Comprensión del beneficio de centralizar catálogo, pedidos y comunicación.
- Flujo de suscripción y acceso inicial a la plataforma.
- Gestión de catálogo de productos.
- Carga asistida de productos ofrecidos.
- Registro y edición de productos del catálogo.
- Eliminación o desactivación de insumos o productos no disponibles.
- Revisión de pedidos realizados por restaurantes.
- Gestión de órdenes recibidas.
- Consulta del detalle de una orden recibida.
- Actualización del estado de pedidos.
- Interacción con comentarios o calificaciones recibidas.
- Uso de la aplicación móvil para proveedores.
- Disposición del proveedor a continuar usando Restock después de la demostración asistida.

#### Flujos de Usuario a evaluar

- Desktop & Mobile User Flow 1: Suscripción y pago.
- Desktop & Mobile User Flow 10: Registro y gestión de productos en el catálogo.
- Desktop & Mobile User Flow 11: Eliminación de insumos.
- Desktop & Mobile User Flow 12: Gestión de órdenes recibidas.
- Desktop & Mobile User Flow 13: Panel principal del proveedor.

#### Relación con funcionalidades To-Be

| Funcionalidad To-Be | User Story relacionada | User Flow existente asociado | Propósito dentro de la entrevista |
| :--- | :--- | :--- | :--- |
| Carga asistida del catálogo del proveedor | US-39 | Desktop & Mobile User Flow 10 | Validar si el proveedor comprende cómo sus productos se digitalizan y quedan disponibles para restaurantes. |
| Revisión y mantenimiento del catálogo | US-39 | Desktop & Mobile User Flow 10 y User Flow 11 | Validar si el proveedor entiende cómo editar, actualizar o eliminar productos de su catálogo. |
| Recepción de pedido de prueba | US-39 | Desktop & Mobile User Flow 12 | Validar si el proveedor comprende cómo recibiría y gestionaría pedidos desde restaurantes. |
| Panel principal del proveedor | Validación complementaria | Desktop & Mobile User Flow 13 | Validar si el proveedor entiende la información principal sobre pedidos, productos y feedback recibido. |

#### Actividades durante la sesión

- Explorar el Landing Page y describir qué entiende sobre Restock desde el punto de vista de un proveedor.
- Identificar si el mensaje del Landing Page comunica correctamente el valor de centralizar catálogo y pedidos.
- Simular el proceso de registro y suscripción.
- Ingresar al sistema como proveedor.
- Acceder al flujo de gestión de cuenta siguiendo el Desktop & Mobile User Flow 1.
- Entregar o simular una lista de productos para realizar la carga asistida del catálogo.
- Registrar productos en el catálogo siguiendo el Desktop & Mobile User Flow 10.
- Revisar si los productos cargados muestran correctamente nombre, precio, unidad de medida y disponibilidad.
- Editar información de productos registrados.
- Eliminar o desactivar productos no disponibles siguiendo el Desktop & Mobile User Flow 11.
- Revisar pedidos recibidos de restaurantes siguiendo el Desktop & Mobile User Flow 12.
- Consultar el detalle de una orden recibida.
- Actualizar el estado de una orden.
- Revisar comentarios o calificaciones recibidas.
- Acceder al panel principal del proveedor siguiendo el Desktop & Mobile User Flow 13.
- Usar la aplicación móvil de proveedores para revisar pedidos y actualizar estados.
- Comentar sobre la utilidad de la interfaz de pedidos, catálogo y feedback.
- Indicar si estaría dispuesto a continuar usando Restock después de la sesión asistida.

#### Preguntas guía para proveedores

- ¿Qué problema crees que Restock busca resolver para proveedores como tú?
- ¿El Landing Page explica claramente cómo te ayudaría la plataforma?
- ¿La carga asistida del catálogo te pareció clara y útil?
- ¿El catálogo cargado representa correctamente los productos que ofreces?
- ¿Qué información agregarías o cambiarías en la ficha de producto?
- ¿Te resultó claro cómo editar o eliminar productos no disponibles?
- ¿El pedido de prueba fue fácil de entender?
- ¿Qué harías al recibir una orden dentro de la plataforma?
- ¿Consideras que gestionar pedidos desde Restock sería mejor que hacerlo por WhatsApp, llamadas o visitas?
- ¿Qué barreras tendrías para actualizar tu catálogo frecuentemente?
- ¿Estarías dispuesto a continuar usando Restock después de esta demostración? ¿Por qué?
- ¿Qué condición tendría que cumplirse para que uses la plataforma en tu operación real?

---

### Herramientas y Recursos para Validación

- **Formato de Evaluación Heurística:** Se aplicarán los 10 principios heurísticos de Nielsen en cada sesión, de acuerdo con el formato de evaluación indicado para el proyecto.
- **Instrumento de observación:** Se utilizará una lista de verificación con sección de notas abiertas para registrar errores, dudas, bloqueos, comentarios espontáneos y oportunidades de mejora.
- **Grabación de pantalla y voz:** Se solicitará autorización previa al participante para grabar la interacción y utilizarla como evidencia académica y material de análisis posterior.
- **Productos a validar:** Landing Page, aplicación web, aplicación móvil para restaurantes y aplicación móvil para proveedores.
- **Cuentas de prueba:** Se utilizarán cuentas preconfiguradas para administrador de restaurante y proveedor, con datos de inventario, productos, pedidos, alertas y rotación.
- **Datos de prueba:** Se utilizarán insumos con stock bajo, insumos con vencimiento próximo, productos de catálogo, pedidos de prueba y registros de rotación para simular escenarios operativos.
- **Herramienta de registro:** Se utilizará una matriz de observación para vincular cada hallazgo con el flujo evaluado, segmento, tarea realizada y severidad del problema detectado.
- **Repositorio de evidencia:** Los videos de entrevista se subirán a Microsoft Stream y se referenciarán posteriormente en la sección 8.3.4.2 Registro de Entrevistas.

### Criterios de Observación

| Criterio | Aspecto a observar | Evidencia esperada |
| :--- | :--- | :--- |
| Comprensión | Si el participante entiende el propósito de la funcionalidad sin explicación adicional. | Comentarios verbales, dudas o reformulación del valor percibido. |
| Facilidad de uso | Si el participante completa la tarea sin bloqueos críticos. | Tiempo de ejecución, errores, retrocesos o abandono de tarea. |
| Utilidad percibida | Si el participante considera que la funcionalidad resuelve un problema real de su operación. | Opiniones posteriores y comentarios espontáneos. |
| Confianza | Si el usuario confiaría en alertas, indicadores o información del sistema para tomar decisiones. | Comentarios sobre precisión, seguridad o necesidad de confirmación manual. |
| Arquitectura de información | Si las secciones, etiquetas y rutas de navegación son claras. | Dudas sobre dónde encontrar funciones o información. |
| Inclusive design | Si textos, botones, tamaños, contrastes e interacciones permiten una experiencia accesible. | Dificultades visuales, confusión en mensajes o problemas de interacción. |

### Consideraciones Éticas y de Registro

Antes de iniciar cada entrevista, se explicará al participante que la sesión tiene fines académicos y que se evaluará la solución, no su desempeño personal. Asimismo, se solicitará autorización para grabar pantalla, voz y/o cámara. La información recolectada será utilizada únicamente para documentar la validación del producto y analizar oportunidades de mejora.


#### 8.3.4.2. Registro de Entrevistas

## 8.4. Experiment Aftermath & Analysis

### 8.4.1. Analysis and Interpretation of Results

### 8.4.2. Re-scored and Re-prioritized Question Backlog

## 8.5. Continuous Learning

### 8.5.1. Shareback Session Artifacts: Learning Workflow

## 8.6. To-Be Software Platform Pre-launch

### 8.6.1. About-the-Product Intro Video
