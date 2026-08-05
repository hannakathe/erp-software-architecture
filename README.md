# erp-software-architecture

Repositorio del taller de **Arquitectura de Software para un Sistema ERP**. El taller consistió en gestionar el backlog del proyecto en Jira (épicas, historias de usuario, criterios de aceptación y priorización MoSCoW) y en documentar la arquitectura del sistema con el modelo **C4**, diagramas **UML** (secuencia y entidad-relación) y la plantilla **arc42**, con foco en el **Módulo de Compras**.

## Gestión del backlog (Jira)

[Tablero de Jira — Proyecto ERP](https://abrilhanna6.atlassian.net/jira/software/projects/KAN/list?jql=project+%3D+KAN+ORDER+BY+cf%5B10019%5D+ASC)

Incluye las 6 épicas del ERP (Compras, Facturación, Stock/Costos, Activos Fijos, Empleados, EIS), con las historias de usuario del Módulo de Compras, sus criterios de aceptación (formato Dado-Cuando-Entonces) y su priorización MoSCoW.

## Documentación de arquitectura (arc42)

La documentación completa empieza en **[arc42-template-ES.md](arc42-template-ES.md)**, que sirve de índice hacia cada capítulo:

| Capítulo | Contenido |
|---|---|
| [1. Introducción y Metas](docs/01_introduction_and_goals.md) | Objetivo del ERP y requisitos de negocio de Compras |
| [2. Restricciones de la Arquitectura](docs/02_architecture_constraints.md) | Decisiones tecnológicas (Java/Spring Boot, React, PostgreSQL) |
| [3. Alcance y Contexto del Sistema](docs/03_system_scope_and_context.md) | Diagrama de Contexto (C1) |
| [5. Vista de Bloques](docs/05_building_block_view.md) | Diagrama de Contenedores (C2) y Modelo de Datos (MER) |
| [6. Vista de Ejecución](docs/06_runtime_view.md) | Escenario "Registrar un Producto" y Diagrama de Secuencia |
| [7. Vista de Despliegue](docs/07_deployment_view.md) | Propuesta de despliegue (opcional) |
| [10. Glosario](docs/10_glossary.md) | Términos clave del dominio |

## Diagramas

Fuente en PlantUML (`docs/*.plantuml`) e imágenes exportadas en [`docs/images/`](docs/images):

- Diagrama de Contexto (C1): [fuente](docs/diagrama_contexto.plantuml) · [imagen](docs/images/diagrama_contexto.png)
- Diagrama de Contenedores (C2): [fuente](docs/diagrama_contenedores.plantuml) · [imagen](docs/images/diagrama_contenedores.png)
- Diagrama de Secuencia (Registrar Producto): [fuente](docs/diagrama_secuencia.plantuml) · [imagen](docs/images/diagrama_secuencia.png)
- Modelo Entidad-Relación (MER — Compras): [fuente](docs/diagrama_MER.plantuml) · [imagen](docs/images/diagrama_MER.png)
