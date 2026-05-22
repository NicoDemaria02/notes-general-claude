# Databricks integration — architecture, AWS setup, and implementation plan
**Date:** May 21, 2026
**Folder:** general

---

### Proyecto Databricks - Configuración y Arquitectura

- Necesidad de definir servicios y configuración para Databricks
- Workspace a crear en AWS (experiencia previa en Azure)
  - Integración mejor con AWS según expectativas
  - Access connectors por definir
- Requerimiento de bucket S3 para Databricks
  - Creación de delta files
  - Estructura de carpetas por importador y entry
  - Visualización y descarga de documentos desde ClearBond

### Especificación Técnica Solicitada

- Deyna requiere documentación adicional más allá de especificación funcional
- Elementos pendientes para mañana:
  1. Diagrama de arquitectura actualizado incluyendo Databricks
  2. Configuración específica de Databricks con infraestructura actual
  3. Plan de escalabilidad (batch actual → real-time futuro)
  4. Análisis de costos y componentes a utilizar

### Accesos y Configuración de Cuentas

- Full ownership del lado del cliente
- Cliente debe crear cuenta Databricks y usuarios para el equipo
- Sesión de guía paso a paso necesaria con cliente
- Credenciales a documentar en vault para acceso compartido
- Pendientes de acceso:
  - Base de datos (Aurora RDS)
  - Documentación compartida (agregar Nico al team Slack)

### Arquitectura de Datos

- Base de datos operativa separada para Databricks
  - Evitar saturación de base operativa del SaaS
  - Sincronización con cron diario desde S3
  - Reflejo de la verdad del SaaS principal
- Posibilidad de usar S3 existente con nuevo container

### Próximos Pasos

- Nico: Investigar integración y mejores prácticas con Lucas
- Félix: Reunión mañana con cliente para mostrar especificación funcional
- Equipo: Preparar documentación técnica para luz verde del lunes
- Implementación programada para comenzar el lunes
