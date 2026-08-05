[← Volver al índice](../arc42-template-ES.md)

# 5. Vista de Bloques

## 5.1 Sistema General de Caja Blanca (Nivel 1)

![Diagrama de Contenedores](./images/diagrama_contenedores.png)

**Motivación**: el Sistema ERP está compuesto por tres contenedores principales, siguiendo una arquitectura monolítica simple.

**Bloques de construcción contenidos**: Aplicación Web (React), API REST (Spring Boot) y Base de Datos (PostgreSQL).

**Interfases importantes**: Aplicación Web ↔ API REST vía HTTPS/JSON; API REST ↔ Base de Datos vía JPA/JDBC; API REST ↔ Servicio de Correo externo.

### Aplicación Web (React)

- **Propósito/Responsabilidad**: interfaz de usuario para todos los roles del ERP (Gestor de Inventario, Administrador de Compras, Encargado de Almacén, Contador, Gerente).
- **Interfase(s)**: consume la API REST vía HTTPS/JSON.
- **Ubicación**: se ejecuta en el navegador del usuario (SPA).

### API REST (Spring Boot)

- **Propósito/Responsabilidad**: concentra toda la lógica de negocio del ERP (validaciones, reglas de compras, cálculo de estados de órdenes, etc.).
- **Interfase(s)**: expone endpoints REST consumidos por la Aplicación Web; se comunica con la Base de Datos vía JPA/JDBC; envía notificaciones al Servicio de Correo externo.

### Base de Datos (PostgreSQL)

- **Propósito/Responsabilidad**: almacenamiento persistente de toda la información del ERP (productos, proveedores, órdenes de compra, recepciones, facturación, etc.).
- **Interfase(s)**: accedida exclusivamente por la API REST.

## 5.2 Modelo de Datos (MER) — Módulo de Compras

![Modelo Entidad-Relación - Compras](./images/diagrama_MER.png)

- **Producto**: catálogo de artículos que pueden comprarse.
- **Proveedor**: catálogo de proveedores habilitados para recibir órdenes de compra.
- **Orden_Compra**: encabezado de una solicitud de abastecimiento a un proveedor, con su estado y fecha.
- **Detalle_Orden**: líneas de producto y cantidad solicitadas dentro de una orden de compra.
- **Recepcion**: registra un evento de llegada de mercancía asociado a una orden de compra, ya que una orden puede recibirse en una o varias entregas parciales.
- **Recepcion_Detalle**: cantidad efectivamente recibida por cada línea de la orden en una recepción determinada.

## 5.3 Nivel 2 y Nivel 3

*(No aplica para el alcance de este taller — se documentaría aquí el desglose interno de la API REST en componentes, si el proyecto avanzara a ese nivel de detalle.)*

---
[← Anterior: Alcance y Contexto del Sistema](03_system_scope_and_context.md) · [Volver al índice](../arc42-template-ES.md) · [Siguiente: Vista de Ejecución →](06_runtime_view.md)
