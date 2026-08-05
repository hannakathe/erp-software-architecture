# Documentación de Arquitectura — Sistema ERP (arc42)

*Enero 2023*

**Acerca de arc42**

arc42, la plantilla de documentación para arquitectura de sistemas y de software.

Por Dr. Gernot Starke, Dr. Peter Hruschka y otros contribuyentes.

Revisión de la plantilla: 7.0 ES (basada en asciidoc), Enero 2017.

© Reconocemos que este documento utiliza material de la plantilla de arquitectura arc42, <https://www.arc42.org>. Creada por Dr. Peter Hruschka y Dr. Gernot Starke.

---

## Índice

Este documento describe la arquitectura del **Sistema ERP**, con foco en el **Módulo de Compras**. Cada sección se desarrolla en un archivo independiente dentro de [`docs/`](docs):

1. [Introducción y Metas](docs/01_introduction_and_goals.md) — objetivo del sistema y requisitos de negocio del Módulo de Compras.
2. [Restricciones de la Arquitectura](docs/02_architecture_constraints.md) — decisiones tecnológicas (Java/Spring Boot, React, PostgreSQL).
3. [Alcance y Contexto del Sistema](docs/03_system_scope_and_context.md) — Diagrama de Contexto (C1).
5. [Vista de Bloques](docs/05_building_block_view.md) — Diagrama de Contenedores (C2) y Modelo de Datos (MER).
6. [Vista de Ejecución](docs/06_runtime_view.md) — escenario "Registrar un Producto" y Diagrama de Secuencia.
7. [Vista de Despliegue](docs/07_deployment_view.md) — propuesta de despliegue (opcional).
10. [Glosario](docs/10_glossary.md) — términos clave del dominio.

> Las secciones 4 (Estrategia de solución), 8 (Conceptos transversales), 9 (Decisiones de diseño) y 11 (Riesgos y deuda técnica) de la plantilla arc42 no forman parte del alcance de este taller y quedan pendientes para una futura iteración del proyecto.

## Diagramas fuente

Los diagramas se modelan en PlantUML y se encuentran en [`docs/`](docs); las imágenes exportadas usadas en la documentación están en [`docs/images/`](docs/images):

- [diagrama_contexto.plantuml](docs/diagrama_contexto.plantuml) → `docs/images/diagrama_contexto.png`
- [diagrama_contenedores.plantuml](docs/diagrama_contenedores.plantuml) → `docs/images/diagrama_contenedores.png`
- [diagrama_secuencia.plantuml](docs/diagrama_secuencia.plantuml) → `docs/images/diagrama_secuencia.png`
- [diagrama_MER.plantuml](docs/diagrama_MER.plantuml) → `docs/images/diagrama_MER.png`
