[← Volver al índice](../arc42-template-ES.md)

# 2. Restricciones de la Arquitectura

## 2.1 Restricciones técnicas

| Decisión | Elección | Justificación |
|---|---|---|
| Backend | Java + Spring Boot (API REST monolítica) | Framework robusto para lógica de negocio empresarial, suficiente para el alcance del taller sin la complejidad de microservicios. |
| Frontend | SPA en React | Interfaz de usuario ágil y desacoplada, consumiendo la API vía HTTPS/JSON. |
| Base de datos | PostgreSQL | Motor relacional adecuado para el modelo transaccional de Compras (productos, proveedores, órdenes, recepciones). |
| Comunicación Frontend–Backend | HTTPS / JSON | Estándar de facto para APIs REST consumidas por SPAs. |
| Comunicación Backend–Base de datos | JPA / JDBC | Persistencia estándar en el ecosistema Spring Boot. |
| Notificaciones | Servicio de correo externo | Se delega el envío de notificaciones a un proveedor externo en vez de construir uno propio. |

## 2.2 Restricciones organizativas

- El sistema se documenta con el modelo **C4** (Contexto y Contenedores) y notación **UML** (secuencia, entidad-relación), usando **PlantUML**.
- La gestión del backlog (épicas, historias de usuario, criterios de aceptación y priorización MoSCoW) se realiza en **Jira**.
- El código y la documentación se versionan en **GitHub**, en el repositorio `erp-software-architecture`.
- Las historias de usuario siguen el formato `Como <rol>, quiero <acción>, para que <beneficio>` y sus criterios de aceptación el formato `Dado-Cuando-Entonces`.
- Se prioriza una arquitectura **monolítica simple** sobre microservicios, dado el alcance académico del taller y el tamaño reducido del equipo.

---
[← Anterior: Introducción y Metas](01_introduction_and_goals.md) · [Volver al índice](../arc42-template-ES.md) · [Siguiente: Alcance y Contexto del Sistema →](03_system_scope_and_context.md)
