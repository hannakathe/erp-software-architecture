[← Volver al índice](../arc42-template-ES.md)

# 6. Vista de Ejecución

## 6.1 Escenario: Registrar un Producto (HU-CP-01)

Historia de usuario: *"Como gestor de inventario, quiero registrar nuevos productos con su información básica (nombre, descripción, unidad de medida y precio), para que el catálogo de compras permanezca actualizado."*

![Diagrama de Secuencia - Registrar Producto](./images/diagrama_secuencia.png)

**Flujo:**

1. El Gestor de Inventario completa el formulario de nuevo producto en la Aplicación Web.
2. La Aplicación Web envía una petición `POST /productos` a la API REST con los datos ingresados.
3. La API REST valida la información recibida (campos obligatorios, formatos).
4. Si los datos son válidos: la API REST inserta el producto en PostgreSQL, responde `201 Created` y la Aplicación Web muestra el mensaje "Producto registrado correctamente".
5. Si los datos son inválidos: la API REST responde con un error de validación (sin escribir en la base de datos) y la Aplicación Web muestra el mensaje de error correspondiente.

**Aspectos notables**: la validación ocurre en el backend, no solo en el frontend, para garantizar la integridad del catálogo. El flujo cubre explícitamente el caso de error, lo que se traduce en los criterios de aceptación de la historia de usuario (ej. rechazar el registro si el campo "nombre" está vacío).

---
[← Anterior: Vista de Bloques](05_building_block_view.md) · [Volver al índice](../arc42-template-ES.md) · [Siguiente: Vista de Despliegue →](07_deployment_view.md)
