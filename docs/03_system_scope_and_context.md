[← Volver al índice](../arc42-template-ES.md)

# 3. Alcance y Contexto del Sistema

## 3.1 Contexto de Negocio

El Sistema ERP es utilizado por cinco roles principales y se comunica con dos sistemas externos. Para el Módulo de Compras, los actores relevantes son:

- **Gestor de Inventario**: registra y mantiene actualizado el catálogo de productos.
- **Administrador de Compras**: gestiona proveedores y genera órdenes de compra.
- **Encargado de Almacén**: registra la recepción de mercancía, lo que actualiza el inventario.

Adicionalmente, el sistema es usado por el **Contador** (facturación y pagos) y el **Gerente** (consulta de reportes ejecutivos), y se integra con:

- **Servicio de Correo**: para el envío de notificaciones (ej. confirmaciones de órdenes de compra).
- **Sistema Contable**: para sincronizar información financiera generada por las operaciones del ERP.

![Diagrama de Contexto](./images/diagrama_contexto.png)

Como muestra el diagrama, el Sistema ERP actúa como una caja negra: los actores interactúan directamente con él sin conocer su estructura interna, y es el propio sistema quien se comunica con los sistemas externos.

## 3.2 Contexto Técnico

La interacción entre los usuarios y el sistema se realiza vía **HTTPS** a través de un navegador web (aplicación SPA). Las integraciones con los sistemas externos (correo, contabilidad) se realizan desde el backend del ERP, sin exponer estas dependencias a los usuarios finales.

---
[← Anterior: Restricciones de la Arquitectura](02_architecture_constraints.md) · [Volver al índice](../arc42-template-ES.md) · [Siguiente: Vista de Bloques →](05_building_block_view.md)
