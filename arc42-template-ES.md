---
date: Enero 2023
title: Plantilla ![arc42](images/arc42-logo.png)
---

# 

**Acerca de arc42**

arc42, La plantilla de documentación para arquitectura de sistemas y de
software.

Por Dr. Gernot Starke, Dr. Peter Hruschka y otros contribuyentes.

Revisión de la plantilla: 7.0 ES (basada en asciidoc), Enero 2017

© Reconocemos que este documento utiliza material de la plantilla de
arquitectura arc42, <https://www.arc42.org>. Creada por Dr. Peter
Hruschka y Dr. Gernot Starke.

# Introducción y Metas {#section-introduction-and-goals}

## Vista de Requerimientos {#_vista_de_requerimientos}

El **Sistema ERP** tiene como objetivo centralizar e integrar los procesos operativos y administrativos de la empresa en una única plataforma, reemplazando el manejo disperso de información entre áreas. El sistema cubre seis módulos de negocio: **Compras**, **Facturación**, **Stock/Costos**, **Activos Fijos**, **Empleados** y **EIS (Executive Information System)**.

Este documento profundiza en el **Módulo de Compras**, alcance detallado de este taller. A partir de las historias de usuario definidas en el backlog (Épica "Módulo de Compras"), los requisitos de negocio prioritarios son:

1. **Registrar productos**: mantener un catálogo de productos actualizado (nombre, descripción, unidad de medida y precio).
2. **Registrar proveedores**: mantener un directorio de proveedores con sus datos de contacto y razón social.
3. **Crear órdenes de compra**: formalizar las solicitudes de abastecimiento hacia un proveedor específico.
4. **Consultar órdenes de compra**: dar seguimiento al historial y al estado de cada orden (pendiente, aprobada, recibida, etc.).
5. **Registrar recepción de productos**: confirmar la llegada de la mercancía adquirida y actualizar el inventario automáticamente, incluso cuando la recepción se realiza en varias entregas parciales.

## Metas de Calidad {#_metas_de_calidad}

| Prioridad | Meta de calidad | Motivación |
|---|---|---|
| 1 | Trazabilidad | Toda orden de compra debe poder rastrearse desde su creación hasta la recepción total de la mercancía. |
| 2 | Usabilidad | Los formularios de registro (productos, proveedores, órdenes) deben ser simples de operar por perfiles no técnicos. |
| 3 | Disponibilidad de información | El estado del inventario y de las órdenes debe reflejar cambios en tiempo real tras cada operación. |

## Partes interesadas (Stakeholders) {#_partes_interesadas_stakeholders}

| Rol/Nombre | Contacto | Expectativas |
|---|---|---|
| Gestor de Inventario | Área de Compras | Mantener el catálogo de productos actualizado y confiable. |
| Administrador de Compras | Área de Compras | Gestionar proveedores y generar órdenes de compra sin fricción. |
| Encargado de Almacén | Área de Almacén | Registrar recepciones de forma ágil y que el inventario se actualice solo. |
| Contador | Área de Contabilidad | Contar con información de compras sincronizada para la contabilidad. |
| Gerente | Dirección | Consultar indicadores y reportes consolidados del área de compras. |

# Restricciones de la Arquitectura {#section-architecture-constraints}

## Restricciones técnicas

| Decisión | Elección | Justificación |
|---|---|---|
| Backend | Java + Spring Boot (API REST monolítica) | Framework robusto para lógica de negocio empresarial, suficiente para el alcance del taller sin la complejidad de microservicios. |
| Frontend | SPA en React | Interfaz de usuario ágil y desacoplada, consumiendo la API vía HTTPS/JSON. |
| Base de datos | PostgreSQL | Motor relacional adecuado para el modelo transaccional de Compras (productos, proveedores, órdenes, recepciones). |
| Comunicación Frontend–Backend | HTTPS / JSON | Estándar de facto para APIs REST consumidas por SPAs. |
| Comunicación Backend–Base de datos | JPA / JDBC | Persistencia estándar en el ecosistema Spring Boot. |
| Notificaciones | Servicio de correo externo | Se delega el envío de notificaciones a un proveedor externo en vez de construir uno propio. |

## Restricciones organizativas

- El sistema se documenta con el modelo **C4** (Contexto y Contenedores) y notación **UML** (secuencia, entidad-relación), usando **PlantUML**.
- La gestión del backlog (épicas, historias de usuario, criterios de aceptación y priorización MoSCoW) se realiza en **Jira**.
- El código y la documentación se versionan en **GitHub**, en el repositorio `erp-software-architecture`.
- Las historias de usuario siguen el formato `Como <rol>, quiero <acción>, para que <beneficio>` y sus criterios de aceptación el formato `Dado-Cuando-Entonces`.
- Se prioriza una arquitectura **monolítica simple** sobre microservicios, dado el alcance académico del taller y el tamaño reducido del equipo.

# Alcance y Contexto del Sistema {#section-context-and-scope}

## Contexto de Negocio {#_contexto_de_negocio}

El Sistema ERP es utilizado por cinco roles principales y se comunica con dos sistemas externos. Para el Módulo de Compras, los actores relevantes son:

- **Gestor de Inventario**: registra y mantiene actualizado el catálogo de productos.
- **Administrador de Compras**: gestiona proveedores y genera órdenes de compra.
- **Encargado de Almacén**: registra la recepción de mercancía, lo que actualiza el inventario.

Adicionalmente, el sistema es usado por el **Contador** (facturación y pagos) y el **Gerente** (consulta de reportes ejecutivos), y se integra con:

- **Servicio de Correo**: para el envío de notificaciones (ej. confirmaciones de órdenes de compra).
- **Sistema Contable**: para sincronizar información financiera generada por las operaciones del ERP.

![Diagrama de Contexto](./docs/images/c1_context.png)

Como muestra el diagrama, el Sistema ERP actúa como una caja negra: los actores interactúan directamente con él sin conocer su estructura interna, y es el propio sistema quien se comunica con los sistemas externos.

## Contexto Técnico {#_contexto_técnico}

La interacción entre los usuarios y el sistema se realiza vía **HTTPS** a través de un navegador web (aplicación SPA). Las integraciones con los sistemas externos (correo, contabilidad) se realizan desde el backend del ERP, sin exponer estas dependencias a los usuarios finales.

# Estrategia de solución {#section-solution-strategy}

# Vista de Bloques {#section-building-block-view}

## Sistema General de Caja Blanca {#_sistema_general_de_caja_blanca}

![Diagrama de Contenedores](./docs/images/c2_containers.png)

Motivación

:   El Sistema ERP está compuesto por tres contenedores principales, siguiendo una arquitectura monolítica simple.

Bloques de construcción contenidos

:   Aplicación Web (React), API REST (Spring Boot) y Base de Datos (PostgreSQL).

Interfases importantes

:   Aplicación Web ↔ API REST vía HTTPS/JSON; API REST ↔ Base de Datos vía JPA/JDBC; API REST ↔ Servicio de Correo externo.

### Aplicación Web (React) {#_caja_negra_1}

*Propósito/Responsabilidad*: interfaz de usuario para todos los roles del ERP (Gestor de Inventario, Administrador de Compras, Encargado de Almacén, Contador, Gerente).

*Interfase(s)*: consume la API REST vía HTTPS/JSON.

*Ubicación*: se ejecuta en el navegador del usuario (SPA).

### API REST (Spring Boot) {#_caja_negra_2}

*Propósito/Responsabilidad*: concentra toda la lógica de negocio del ERP (validaciones, reglas de compras, cálculo de estados de órdenes, etc.).

*Interfase(s)*: expone endpoints REST consumidos por la Aplicación Web; se comunica con la Base de Datos vía JPA/JDBC; envía notificaciones al Servicio de Correo externo.

### Base de Datos (PostgreSQL) {#_caja_negra_n}

*Propósito/Responsabilidad*: almacenamiento persistente de toda la información del ERP (productos, proveedores, órdenes de compra, recepciones, facturación, etc.).

*Interfase(s)*: accedida exclusivamente por la API REST.

## Modelo de Datos (MER) - Módulo de Compras {#_modelo_de_datos_mer}

![Modelo Entidad-Relación - Compras](./docs/images/mer_compras.png)

- **Producto**: catálogo de artículos que pueden comprarse.
- **Proveedor**: catálogo de proveedores habilitados para recibir órdenes de compra.
- **Orden_Compra**: encabezado de una solicitud de abastecimiento a un proveedor, con su estado y fecha.
- **Detalle_Orden**: líneas de producto y cantidad solicitadas dentro de una orden de compra.
- **Recepcion**: registra un evento de llegada de mercancía asociado a una orden de compra, ya que una orden puede recibirse en una o varias entregas parciales.
- **Recepcion_Detalle**: cantidad efectivamente recibida por cada línea de la orden en una recepción determinada.

## Nivel 2 {#_nivel_2}

### Caja Blanca *\<bloque de construcción 1\>* {#_caja_blanca_bloque_de_construcción_1}

*\<plantilla de caja blanca\>*

### Caja Blanca *\<bloque de construcción 2\>* {#_caja_blanca_bloque_de_construcción_2}

*\<plantilla de caja blanca\>*

...​

### Caja Blanca *\<bloque de construcción m\>* {#_caja_blanca_bloque_de_construcción_m}

*\<plantilla de caja blanca\>*

## Nivel 3 {#_nivel_3}

### Caja Blanca \<\_bloque de construcción x.1\_\> {#_caja_blanca_bloque_de_construcción_x_1}

*\<plantilla de caja blanca\>*

### Caja Blanca \<\_bloque de construcción x.2\_\> {#_caja_blanca_bloque_de_construcción_x_2}

*\<plantilla de caja blanca\>*

### Caja Blanca \<\_bloque de construcción y.1\_\> {#_caja_blanca_bloque_de_construcción_y_1}

*\<plantilla de caja blanca\>*

# Vista de Ejecución {#section-runtime-view}

## Registrar un Producto (HU-CP-01) {#_escenario_de_ejecución_1}

Historia de usuario: *"Como gestor de inventario, quiero registrar nuevos productos con su información básica (nombre, descripción, unidad de medida y precio), para que el catálogo de compras permanezca actualizado."*

![Diagrama de Secuencia - Registrar Producto](./docs/images/sequence_registrar_producto.png)

**Flujo:**

1.  El Gestor de Inventario completa el formulario de nuevo producto en la Aplicación Web.
2.  La Aplicación Web envía una petición `POST /productos` a la API REST con los datos ingresados.
3.  La API REST valida la información recibida (campos obligatorios, formatos).
4.  Si los datos son válidos: la API REST inserta el producto en PostgreSQL, responde `201 Created` y la Aplicación Web muestra el mensaje "Producto registrado correctamente".
5.  Si los datos son inválidos: la API REST responde con un error de validación (sin escribir en la base de datos) y la Aplicación Web muestra el mensaje de error correspondiente.

**Aspectos notables**: la validación ocurre en el backend, no solo en el frontend, para garantizar la integridad del catálogo. El flujo cubre explícitamente el caso de error, lo que se traduce en los criterios de aceptación de la historia de usuario (ej. rechazar el registro si el campo "nombre" está vacío).

# Vista de Despliegue {#section-deployment-view}

## Nivel de infraestructura 1 {#_nivel_de_infraestructura_1}

> Sección opcional. Se describe una propuesta simple de despliegue para la arquitectura monolítica definida en la Vista de Bloques.

Motivación

:   Para el alcance de este taller, un despliegue simple en un único servidor (o un conjunto reducido de servicios administrados en la nube) es suficiente para soportar los tres contenedores del sistema.

Características de Calidad/Rendimiento

:   Separar la base de datos de la API permite escalar o respaldar la base de datos de forma independiente; servir el frontend como archivos estáticos reduce la carga sobre el backend. Todas las comunicaciones se realizan sobre HTTPS.

Mapeo de los Bloques de Construcción a Infraestructura

:   Ver tabla a continuación.

| Contenedor | Infraestructura propuesta |
|---|---|
| Aplicación Web (React) | Build estático servido desde un hosting de archivos estáticos / CDN. |
| API REST (Spring Boot) | Empaquetada como contenedor Docker, desplegada en un servidor de aplicaciones o servicio administrado en la nube. |
| Base de Datos (PostgreSQL) | Instancia de base de datos administrada, separada del servidor de la API. |

# Conceptos Transversales (Cross-cutting) {#section-concepts}

## *\<Concepto 1\>* {#_concepto_1}

*\<explicación\>*

## *\<Concepto 2\>* {#_concepto_2}

*\<explicación\>*

...​

## *\<Concepto n\>* {#_concepto_n}

*\<explicación\>*

# Decisiones de Diseño {#section-design-decisions}

# Requerimientos de Calidad {#section-quality-scenarios}

## Árbol de Calidad {#_árbol_de_calidad}

## Escenarios de calidad {#_escenarios_de_calidad}

# Riesgos y deuda técnica {#section-technical-risks}

# Glosario {#section-glossary}

| Término | Definición |
|---|---|
| Producto | Artículo del catálogo que puede ser solicitado a un proveedor mediante una orden de compra. |
| Proveedor | Persona o empresa externa que suministra productos a la organización. |
| Orden de Compra | Documento formal mediante el cual el Administrador de Compras solicita productos a un proveedor. |
| Detalle de Orden | Línea de una orden de compra que especifica un producto, la cantidad solicitada y su precio unitario. |
| Recepción de Mercancía | Evento en el que el Encargado de Almacén confirma la llegada física de los productos de una orden de compra, total o parcialmente. |
| Gestor de Inventario | Rol responsable de mantener actualizado el catálogo de productos. |
| Administrador de Compras | Rol responsable de gestionar proveedores y generar órdenes de compra. |
| Encargado de Almacén | Rol responsable de registrar la recepción de mercancía y mantener el inventario actualizado. |
| Épica | Historia de usuario de gran tamaño que agrupa funcionalidades de un mismo módulo (ej. "Módulo de Compras"). |
| Historia de Usuario (HU) | Descripción breve de una funcionalidad desde la perspectiva de un rol, con el formato "Como \<rol\>, quiero \<acción\>, para que \<beneficio\>". |
| Criterio de Aceptación | Condición verificable, en formato Dado-Cuando-Entonces, que determina si una historia de usuario está correctamente implementada. |
| MER | Modelo de Entidad-Relación: representación de las entidades de datos y sus relaciones. |
| C4 Model | Notación de diagramas de arquitectura de software en niveles (Contexto, Contenedores, Componentes, Código). |
