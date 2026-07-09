# Conclusiones

### Conclusiones y recomendaciones

A lo largo del presente proyecto, el equipo de UI-Topic ha ejecutado un ciclo completo de ingeniería de software que abarca el análisis del problema, el diseño y desarrollo de la plataforma Restock, su verificación y validación, la implementación del pipeline de DevOps y el diseño de experimentos orientados a validar hipótesis de valor para el negocio. A continuación se presentan las conclusiones derivadas del trabajo realizado en cada dimensión del proyecto.

**Sobre los Problem Statements y el contexto de la problemática**

El análisis inicial confirmó que los restaurantes pequeños y medianos en Lima enfrentan una problemática real, persistente y transversal al sector HORECA latinoamericano: la dependencia de métodos manuales —hojas de cálculo, cuadernos físicos y mensajería informal— para gestionar inventarios y pedidos a proveedores genera errores frecuentes, desperdicio de insumos, desabastecimiento y falta de visibilidad operativa (Cross, 2024). Las entrevistas realizadas a administradores de restaurantes y proveedores validaron que esta problemática no responde a una única causa, sino a la combinación de procesos fragmentados, bajo acceso a soluciones tecnológicas accesibles y una curva de adopción digital aún en desarrollo en el segmento PyME del sector gastronómico peruano.

**Sobre los Assumptions y el comportamiento real de los segmentos**

Los supuestos de negocio planteados durante el proceso Lean UX han sido parcialmente validados a través de las entrevistas de discovery y las sesiones de validación con usuarios. Los administradores de restaurante confirmaron su disposición a adoptar soluciones tecnológicas, condicionada a que sean intuitivas, económicamente accesibles y que ofrezcan retorno operativo tangible —principalmente en forma de control de inventario y reducción de compras de emergencia—. Esta confirmación respalda el supuesto de que el valor percibido número uno por los clientes es la visibilidad y el control operativo en tiempo real. Del mismo modo, los proveedores mostraron una apertura genuina hacia la digitalización de su operación, especialmente en lo referente a la gestión de pedidos, seguimiento de entregas y facturación, lo cual valida el supuesto de que los beneficios adicionales valorados incluyen la trazabilidad de pagos y la mejora en la relación restaurante–proveedor. Sin embargo, el supuesto sobre la disposición a invertir hasta 800 USD en una solución tecnológica fue matizado por las entrevistas: los administradores consultados manejan presupuestos menores, lo que refuerza la necesidad de un modelo de suscripción escalonado y accesible.

**Sobre las hipótesis Lean UX y los criterios de éxito**

Las cuatro hipótesis formuladas en el proceso Lean UX —reducción de mermas en un 35 %, alcance de 500 usuarios activos en 6 meses, reducción de errores de pedido en un 25 % e incremento del 40 % en pedidos gestionados en plataforma— representan metas ambiciosas y coherentes con la evidencia cuantitativa identificada en la literatura (Tan et al., 2022; Zamora Saltos & Rodríguez Borges, 2024; Cabrera-Gala et al., 2021). La validación cualitativa de estas hipótesis, obtenida a través de las entrevistas y sesiones de evaluación heurística, genera señales positivas respecto a la viabilidad de alcanzar dichos umbrales. Sin embargo, la validación cuantitativa definitiva requiere la ejecución completa de los experimentos diseñados en el Capítulo VIII, con grupos de usuarios reales operando en condiciones controladas durante un período suficiente para detectar efectos medibles.

**Sobre el producto implementado**

La plataforma Restock fue implementada con una arquitectura orientada a servicios y separación de responsabilidades por bounded context, utilizando Vue.js para la aplicación web frontend, ASP.NET Core con C# para los servicios RESTful, y Flutter como canal nativo móvil. Los módulos implementados cubren los flujos críticos del negocio: gestión de inventario con alertas automáticas, gestión de pedidos a proveedores con seguimiento de estados, registro de ventas, sistema de notificaciones y calificaciones entre restaurante y proveedor. El pipeline de DevOps implementado mediante integración continua (GitHub Actions) y entrega continua garantiza la calidad del código a través de etapas automatizadas de construcción, prueba, análisis estático y despliegue, contribuyendo a la sostenibilidad del ciclo de vida del producto.

**Sobre el proceso de verificación y validación**

El proceso de testing implementado incluyó pruebas unitarias sobre entidades de dominio, pruebas de integración sobre la comunicación entre componentes y pruebas de comportamiento bajo el enfoque BDD con escenarios Gherkin ejecutados mediante SpecFlow. El análisis estático de código garantizó el cumplimiento de los estándares de codificación establecidos y la ausencia de vulnerabilidades conocidas en los patrones de desarrollo utilizados. Las entrevistas de validación con usuarios de ambos segmentos revelaron una percepción positiva de la interfaz y las funcionalidades implementadas, con áreas de mejora identificadas principalmente en la configuración inicial de alertas personalizadas, la generación de reportes para períodos históricos extensos y la experiencia de onboarding en el módulo de recetas.

**Sobre la auditoría de experiencias de usuario**

El proceso de auditoría realizada permitió al equipo evaluar en profundidad la experiencia de usuario de otro grupo, aplicando las heurísticas de usabilidad, arquitectura de información y diseño inclusivo, e identificando problemas concretos con niveles de severidad definidos. La auditoría recibida, a su vez, aportó retroalimentación externa valiosa que el equipo incorporó en mejoras al flujo de navegación y a la accesibilidad de los módulos principales de la plataforma.

**Sobre el proceso de trabajo del equipo**

El desarrollo del proyecto permitió al equipo consolidar competencias en diseño y ejecución de experimentos de software, arquitectura orientada a servicios, prácticas de DevOps, y aplicación del marco de trabajo Lean UX como eje conductor del ciclo de vida del producto. La adopción de GitFlow, Conventional Commits y pipelines automatizados favoreció la colaboración efectiva y la trazabilidad del trabajo de cada integrante. El uso de herramientas como UXPressia, Figma, Structurizr y Jira permitió mantener coherencia entre los artefactos de análisis, diseño e implementación a lo largo de las entregas.

**Sobre el proceso del trabajo Final**

El desarrollo del proyecto Final ayudo a todo el equipo en mejorar varios apartados que no nos dimos cuenta, como la modificaciones que tuvimos que hacer gracias a la actualizacion de statemnt project actualizado hace poco, y aun asi el equipo logro cumplir de la mejor forma posible, restrucutrando el diseño y mejorando apartados fundamentales para completar el proyecto de la mejor manera posible

**Recomendaciones**

- Ejecutar los cuatro experimentos planificados con grupos de usuarios reales para obtener validación cuantitativa de las hipótesis formuladas y respaldar decisiones de roadmap con datos medibles.
- Ampliar la cobertura de pruebas automatizadas en los módulos de generación de reportes y exportación a Excel, que actualmente presentan menor densidad de pruebas respecto al resto de la plataforma.
- Explorar la integración con pasarelas de pago locales como Yape, Plin o Culqi para completar el flujo de facturación entre restaurantes y proveedores dentro de la plataforma, eliminando la necesidad de gestionar pagos por canales externos.
- Implementar un módulo de análisis predictivo sobre los datos históricos de inventario para ofrecer sugerencias proactivas de reabastecimiento basadas en patrones de consumo estacionales y tendencias de demanda.
- Diseñar flujos de onboarding diferenciados según el rol del usuario (administrador de restaurante vs. proveedor), con quick-wins configurados por defecto que reduzcan el tiempo de obtención del primer valor percibido.
- Evaluar la certificación en estándares de seguridad y privacidad de datos (ISO 27001 o similares) para fortalecer la confianza de los usuarios ante el manejo de información operativa y financiera sensible.
- Desarrollar una estrategia de expansión geográfica progresiva hacia otras ciudades del Perú con alta densidad del sector gastronómico (Arequipa, Trujillo, Cusco), aprovechando el modelo SaaS escalable implementado.
- Desarrollar estrategia de entrevista para las pruebas de uso del proyecto por medio de otros usuarios ademas del equipo en cuestion, para obtener un feedback mas a profundidar para mejorar con las experimentaciones.

---

### Video App Validation

> *Incluir en esta sección el resumen del proceso de validación mediante Firebase App Distribution, los dispositivos utilizados, los usuarios participantes y el enlace al video de demostración.*

| Campo | Detalle |
|---|---|
| Herramienta utilizada | Firebase App Distribution |
| Usuario que realizó la prueba | Larry |
| Dispositivo utilizado | Dispositivo local |
| Enlace al video | https://shorturl.at/1PkOk |
| Duración | 00:15:18 |
| Timing de inicio | 00:01:22 |

---

### Video About-The-Team

> *Incluir en esta sección el resumen del proceso de trabajo del equipo, los testimonios de cada integrante y el enlace al video.*

| Campo | Detalle |
|---|---|
| Enlace (Microsoft Stream) | https://shorturl.at/onDYe |
| Enlace (YouTube) | https://youtu.be/hmCdb-iKpmA |
| Duración total | 00:08:19 |

**Pauta de contenido:**

| Sección | Timing |
|---|---|
| Presentación del equipo | 00:00:00 |
| Resumen del proceso de trabajo | 00:00:08 |
| Testimonio — Julio Castro Alejos | 00:02:09 |
| Testimonio — Ario Chavez Uribe | 00:03:40 |
| Testimonio — José Jahaziel Guerra Perez | 00:04:41 |
| Testimonio — Ivan Fernando Sanchez Guevara | 00:05:18 |
| Testimonio — Gabriela Nicole Shapiama Rivera | 00:07:00 |
| Cierre y reflexión grupal | 00:08:15 |

---


