[← Volver al índice](../arc42-template-ES.md)

# 1. Introducción y Metas

## 1.1 Vista de Requerimientos

El **Sistema ERP** tiene como objetivo centralizar e integrar los procesos operativos y administrativos de la empresa en una única plataforma, reemplazando el manejo disperso de información entre áreas. El sistema cubre seis módulos de negocio: **Compras**, **Facturación**, **Stock/Costos**, **Activos Fijos**, **Empleados** y **EIS (Executive Information System)**.

Este documento profundiza en el **Módulo de Compras**, alcance detallado de este taller. A partir de las historias de usuario definidas en el backlog (Épica "Módulo de Compras"), los requisitos de negocio prioritarios son:

1. **Registrar productos**: mantener un catálogo de productos actualizado (nombre, descripción, unidad de medida y precio).
2. **Registrar proveedores**: mantener un directorio de proveedores con sus datos de contacto y razón social.
3. **Crear órdenes de compra**: formalizar las solicitudes de abastecimiento hacia un proveedor específico.
4. **Consultar órdenes de compra**: dar seguimiento al historial y al estado de cada orden (pendiente, aprobada, recibida, etc.).
5. **Registrar recepción de productos**: confirmar la llegada de la mercancía adquirida y actualizar el inventario automáticamente, incluso cuando la recepción se realiza en varias entregas parciales.

## 1.2 Metas de Calidad

| Prioridad | Meta de calidad | Motivación |
|---|---|---|
| 1 | Trazabilidad | Toda orden de compra debe poder rastrearse desde su creación hasta la recepción total de la mercancía. |
| 2 | Usabilidad | Los formularios de registro (productos, proveedores, órdenes) deben ser simples de operar por perfiles no técnicos. |
| 3 | Disponibilidad de información | El estado del inventario y de las órdenes debe reflejar cambios en tiempo real tras cada operación. |

## 1.3 Partes interesadas (Stakeholders)

| Rol/Nombre | Contacto | Expectativas |
|---|---|---|
| Gestor de Inventario | Área de Compras | Mantener el catálogo de productos actualizado y confiable. |
| Administrador de Compras | Área de Compras | Gestionar proveedores y generar órdenes de compra sin fricción. |
| Encargado de Almacén | Área de Almacén | Registrar recepciones de forma ágil y que el inventario se actualice solo. |
| Contador | Área de Contabilidad | Contar con información de compras sincronizada para la contabilidad. |
| Gerente | Dirección | Consultar indicadores y reportes consolidados del área de compras. |

---
[← Volver al índice](../arc42-template-ES.md) · [Siguiente: Restricciones de la Arquitectura →](02_architecture_constraints.md)
