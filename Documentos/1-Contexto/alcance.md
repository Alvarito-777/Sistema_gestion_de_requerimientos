## Alcance 

### Módulo de Gestión de Tickets - Solicitudes
* **Registro de solicitudes:** Permitir a estudiantes, docentes y administrativos radicar solicitudes de soporte técnico especificando el equipo afectado y la descripción de la falla.
* **Radicación única:** Generación automática de un código de radicado único por ticket para su posterior trazabilidad.
* **Flujo de estados:** Transición controlada del ticket a través de estados predefinidos (`Abierto`, `En proceso`, `Cerrado`, `Rechazado`) mediante tipos de datos restringidos (`ENUM`).
* **Cierre justificado:** Obligatoriedad de ingresar una descripción técnica de la solución antes de permitir el cierre definitivo de una solicitud.
* **Reapertura de solicitudes:** Opción para que el usuario pueda rechazar el cierre de un ticket dentro de un plazo límite si considera que el problema persiste.

### Módulo de Gestión de Técnicos y Atención
* **Visualización de cola de trabajo:** Panel para que los técnicos consulten tickets pendientes (`Abiertos` o `En proceso`) ordenados por prioridad o fecha.
* **Asignación de responsables:** Vinculación directa de un técnico a cada solicitud de soporte.
* **Alertas por inactividad:** Notificación automática al Jefe de TI cuando un ticket supere las 48 horas sin asignación.

### Módulo de Inventario de Equipos
* **Registro de activos:** Control centralizado de equipos de cómputo indicando su responsable, ubicación (aula/oficina) y estado de garantía.
* **Trazabilidad de fallas:** Asociación directa entre el equipo registrado en el inventario y los tickets de soporte generados.

### Módulo de Reportes y Métrica (Jefe de TI)
* **Panel de control (Dashboard):** Visualización de métricas mensuales sobre tickets pendientes, resueltos por período y rendimiento por técnico.
