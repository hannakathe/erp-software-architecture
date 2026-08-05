[← Volver al índice](../arc42-template-ES.md)

# 7. Vista de Despliegue

*(Sección opcional.)*

## 7.1 Nivel de infraestructura 1

Se describe una propuesta simple de despliegue para la arquitectura monolítica definida en la [Vista de Bloques](05_building_block_view.md).

**Motivación**: para el alcance de este taller, un despliegue simple en un único servidor (o un conjunto reducido de servicios administrados en la nube) es suficiente para soportar los tres contenedores del sistema.

**Características de Calidad/Rendimiento**: separar la base de datos de la API permite escalar o respaldar la base de datos de forma independiente; servir el frontend como archivos estáticos reduce la carga sobre el backend. Todas las comunicaciones se realizan sobre HTTPS.

**Mapeo de los Bloques de Construcción a Infraestructura**:

| Contenedor | Infraestructura propuesta |
|---|---|
| Aplicación Web (React) | Build estático servido desde un hosting de archivos estáticos / CDN. |
| API REST (Spring Boot) | Empaquetada como contenedor Docker, desplegada en un servidor de aplicaciones o servicio administrado en la nube. |
| Base de Datos (PostgreSQL) | Instancia de base de datos administrada, separada del servidor de la API. |

---
[← Anterior: Vista de Ejecución](06_runtime_view.md) · [Volver al índice](../arc42-template-ES.md) · [Siguiente: Glosario →](10_glossary.md)
