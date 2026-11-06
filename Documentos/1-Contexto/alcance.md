# Alcance Técnico de la Solución

El sistema está diseñado para gestionar de forma centralizada las solicitudes y requerimientos estratégicos de la gerencia en la empresa **Nexa Servicios**. A continuación, se define el alcance técnico de la solución:

## Módulos y Entidades dentro del Alcance (Lo que hace el sistema)

### 1. Gestión de Accesos y Seguridad
* **Entidades:** `rol`, `usuario`, `usuario_rol`
* **Funcionalidad:**
  * Administración de cuentas de usuario corporativas y asignación de roles estructurados (`Solicitante`, `Aprobador`, `Gestion_Personal`, `Gerente` y `Administrador`; véase la nota de la RN-03 sobre el rol `Auditor`).
  * Control de autenticación, control de intentos fallidos y protección de identidades anónimas.

### 2. Radicación y Ciclo de Vida de Peticiones
* **Entidades:** `solicitud`, `estado_solicitud`, `tipo_solicitud`
* **Funcionalidad:**
  * Creación de borradores y radicación formal de solicitudes estratégicas por parte de los usuarios (`solicitud`).
  * Trazabilidad de estados y cambios de flujo respaldados por la bitácora del sistema.

### 3. Evaluación y Aprobación de Solicitudes
* **Entidades:** `aprobacion_solicitud`
* **Funcionalidad:**
  * Módulo para que los aprobadores autoricen, rechacen o devuelvan solicitudes para ajustes, exigiendo justificaciones obligatorias y previniendo conflictos de interés.

### 4. Atención y Ejecución Operativa
* **Entidades:** `gestion_solicitud`
* **Funcionalidad:**
  * Asignación de requerimientos a gestores, priorización de casos y registro de tiempos de vinculación y cierre operativo.

### 5. Interacción y Seguimiento
* **Entidades:** `detalle_solicitud`
* **Funcionalidad:**
  * Registro cronológico de mensajes y documentos adjuntos en un hilo conversacional unificado para cada expediente.

### 6. Evaluación de Satisfacción
* **Entidades:** `evaluacion`
* **Funcionalidad:**
  * Calificación del servicio recibido por parte del solicitante una vez la gestión se encuentre finalizada.

### 7. Auditoría e Inalterabilidad
* **Entidades:** `bitacora_auditoria`
* **Funcionalidad:**
  * Registro automático, permanente e inalterable de cada evento transaccional y cambio de estado ocurrido en la plataforma.
