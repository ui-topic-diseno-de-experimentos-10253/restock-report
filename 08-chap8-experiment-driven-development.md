# Part III: Experiment-Driven Lifecycle

# Capítulo VIII: Experiment-Driven Development

## 8.1. Experiment Planning

### 8.1.1. As-Is Summary

### 8.1.2. Raw Material: Assumptions, Knowledge Gaps, Ideas, Claims

### 8.1.3. Experiment-Ready Questions

### 8.1.4. Question Backlog

### 8.1.5. Experiment Cards

## 8.2. Experiment Design

### 8.2.1. Hypotheses

### 8.2.2. Domain Business Metrics

### 8.2.3. Measures

### 8.2.4. Conditions

Esta sección describe las condiciones definidas para cada experimento planificado en la plataforma Restock, en función de los factores que permiten identificar el motivo subyacente detrás de cada respuesta esperada. Para cada experimento derivado de las hipótesis de negocio (sección 8.2.1), se establece la **condición experimental** —orientada a obtener evidencia a favor de la hipótesis alternativa— y la **condición de control** —que representa el estado base bajo la suposición de que la hipótesis nula es correcta—.

---

### Experimento 1 — Módulo de inventario automatizado con alertas en tiempo real

**Pregunta:** ¿La activación del módulo de inventario automatizado con alertas reduce las mermas de insumos en los restaurantes?

| | Descripción |
|---|---|
| **Condición Experimental (A)** | Los administradores de restaurante acceden a la plataforma Restock con el módulo de inventario activo. Reciben alertas automáticas clasificadas por tipo (stock bajo, exceso de stock, vencimiento próximo) y visualizan el nivel de stock actualizado en tiempo real desde el dashboard. El sistema descuenta insumos automáticamente al registrar ventas. |
| **Condición de Control (B)** | Los administradores gestionan su inventario mediante métodos manuales convencionales: hojas de cálculo (Excel o Google Sheets), cuadernos físicos o mensajería (WhatsApp). No tienen acceso al módulo automatizado de Restock durante el período de medición. |

**Variable independiente:** Activación del módulo de inventario automatizado con alertas en tiempo real.  
**Variable dependiente:** Porcentaje de reducción en mermas de insumos por período de medición.  
**H₀:** El módulo de inventario automatizado no produce una reducción significativa de mermas respecto al método manual.  
**H₁:** El módulo reduce las mermas en al menos un **35 %** respecto al método manual.

**Criterio de asignación:** Asignación aleatoria por restaurante participante. Cada restaurante opera exclusivamente bajo una de las dos condiciones durante el período del experimento para evitar contaminación cruzada.

---

### Experimento 2 — Onboarding guiado e interfaz móvil-first

**Pregunta:** ¿Un onboarding guiado combinado con acceso móvil como canal principal incrementa la retención temprana de usuarios?

| | Descripción |
|---|---|
| **Condición Experimental (A)** | Los nuevos usuarios (administradores y proveedores) reciben un flujo de onboarding guiado paso a paso al registrarse: tour interactivo, tooltips contextuales en los módulos principales y configuración asistida del primer insumo y primera orden. El canal de acceso recomendado es el dispositivo móvil. |
| **Condición de Control (B)** | Los nuevos usuarios acceden a la plataforma sin guía de onboarding: navegan libremente desde la pantalla de inicio sin asistencia contextual. No se sugiere ningún canal preferente de acceso. |

**Variable independiente:** Presencia de onboarding guiado y disponibilidad de acceso móvil-first.  
**Variable dependiente:** Número de usuarios que inician sesión 3 o más veces durante sus primeros 7 días tras el registro (retención temprana).  
**H₀:** El onboarding guiado y el acceso móvil no incrementan significativamente la retención temprana de usuarios.  
**H₁:** El onboarding guiado permite que al menos **500 usuarios activos** registren 3 o más sesiones en sus primeros 7 días dentro de los primeros 6 meses de operación.

**Criterio de asignación:** Asignación por cohorte de registro. Los usuarios registrados durante las primeras 4 semanas corresponden a la condición de control; los registrados durante las siguientes 4 semanas corresponden a la condición experimental, en un esquema de despliegue progresivo (feature flag).

---

### Experimento 3 — Reportes automáticos con métricas de rotación y márgenes

**Pregunta:** ¿El acceso a reportes automáticos reduce los errores al generar órdenes de compra?

| | Descripción |
|---|---|
| **Condición Experimental (A)** | Los administradores de restaurante tienen acceso al módulo de reportes de Restock, el cual genera automáticamente informes con métricas de rotación de insumos, nivel promedio de stock por período y sugerencias de cantidad de pedido basadas en el historial de consumo. Los reportes están disponibles previo a la generación de cada orden. |
| **Condición de Control (B)** | Los administradores generan órdenes de compra sin acceso a reportes automatizados. Toman decisiones de abastecimiento basadas en la observación directa del inventario, criterio propio o registros históricos elaborados manualmente fuera de la plataforma. |

**Variable independiente:** Disponibilidad de reportes automáticos con métricas de rotación y márgenes previo a la generación de órdenes.  
**Variable dependiente:** Porcentaje de líneas de pedido que requieren corrección (edición o eliminación) antes de ser enviadas al proveedor.  
**H₀:** El acceso a reportes automáticos no reduce significativamente los errores en la generación de órdenes de compra.  
**H₁:** Los reportes automáticos reducen en al menos un **25 %** las líneas de pedido que necesitan corrección.

**Criterio de asignación:** Asignación aleatoria por restaurante. Se controla que el restaurante no haya utilizado el módulo de reportes previamente (no contaminación de cohorte).

---

### Experimento 4 — Canal centralizado proveedor–restaurante (catálogo, pedidos y comunicación)

**Pregunta:** ¿La centralización del catálogo, pedidos y comunicación dentro de la plataforma incrementa el volumen de pedidos gestionados y reduce los errores de pedido?

| | Descripción |
|---|---|
| **Condición Experimental (A)** | Los administradores de restaurante y sus proveedores asociados gestionan catálogos de productos, creación y seguimiento de pedidos, y comunicación exclusivamente dentro de Restock (módulo de órdenes + catálogo del proveedor + sistema de notificaciones de estado). No se permite el uso de canales externos para estas interacciones durante el período del experimento. |
| **Condición de Control (B)** | La gestión de pedidos y comunicación se realiza a través de los canales fragmentados habituales: WhatsApp, llamadas telefónicas, correo electrónico o visitas presenciales. La plataforma Restock no se utiliza para estas interacciones. |

**Variable independiente:** Uso exclusivo del canal centralizado de Restock para gestión de catálogos, pedidos y comunicación entre restaurante y proveedor.  
**Variable dependiente (primaria):** Número de pedidos creados dentro de la plataforma por restaurante por mes.  
**Variable dependiente (secundaria):** Porcentaje de órdenes con devoluciones, ajustes o errores de pedido sobre el total de órdenes creadas.  
**H₀:** La centralización del canal no produce un incremento significativo en pedidos gestionados dentro de la plataforma ni reduce los errores de pedido.  
**H₁:** La centralización incrementa en al menos un **40 %** los pedidos gestionados en la plataforma y reduce en al menos un **25 %** las devoluciones o ajustes.

**Criterio de asignación:** Asignación por par restaurante–proveedor. Ambos actores del par deben pertenecer a la misma condición para garantizar que la interacción sea consistente con el canal asignado.

---

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
