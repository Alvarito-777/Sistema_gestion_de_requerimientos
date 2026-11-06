# 2.2.2 Reglas de Negocio

### Tabla 93. Regla de negocio RN-01 — Dominio de correo corporativo

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-01 |
| **Enunciado** | Toda cuenta de usuario debe registrarse obligatoriamente con los campos pedidos, incluyendo una dirección de correo perteneciente al dominio corporativo autorizado (`@nexaservicios.com`). |
| **Origen** | Criterio de rechazo HU05 CA2 (Validación de dominio corporativo). |
| **RF que la vigilan** | RF-05, RF-07 |

---

### Tabla 94. Regla de negocio RN-02 — Bloqueo por intentos fallidos

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-02 |
| **Enunciado** | Una cuenta de usuario se suspenderá automáticamente tras acumular 3 intentos fallidos consecutivos de autenticación, asignando un bloqueo de 15 min. |
| **Origen** | Criterios de rechazo HU07 CA2, HU09 CA2 y HU10 CA2 (Suspensión por intentos fallidos y control de bloqueo). |
| **RF que la vigilan** | RF-07, RF-09, RF-10 |

---

### Tabla 95. Regla de negocio RN-03 — Dominio de perfiles autorizados

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-03 |
| **Enunciado** | El nombre asignado a un rol debe pertenecer al catálogo de dominios autorizados en el sistema (`Administrador`, `Solicitante`, `Aprobador`, `Gerente`, `Gestion_Personal`, `Auditor`) y no puede registrarse duplicado. |
| **Origen** | Criterios de rechazo HU01 CA2, HU01 CA3 y HU03 CA2 (Restricción de unicidad y dominio de rol). |
| **RF que la vigilan** | RF-01, RF-03 |

> **Nota:** El rol *Auditor* aparece en esta regla y en la RN-25, pero no forma parte del dominio de `rol.nombre_rol` del diccionario (3.1) ni de los datos semilla del script (4.1), que definen cinco roles: Solicitante, Aprobador, Gestion_Personal, Gerente y Administrador. En la versión 1.1 se unificó el nombre «Gestor» como «Gestion_Personal». La incorporación o el retiro del rol Auditor queda pendiente de decisión del equipo mediante CRF (observación OA-01).

---

### Tabla 96. Regla de negocio RN-04 — Desblindaje de identidad anónima

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-04 |
| **Enunciado** | La revelación de la identidad de un solicitante en peticiones marcadas como anónimas (`anonimo_bloqueado = true`) solo puede ser ejecutada por usuarios con rol Gerente o Administrador, requiriendo un registro inmutable en la bitácora de auditoría. |
| **Origen** | Criterio de rechazo HU26 CA2 (Control de permisos sobre identidades protegidas). |
| **RF que la vigilan** | RF-22, RF-26 |

---

### Tabla 97. Regla de negocio RN-05 — Impedimento de autoaprobación

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-05 |
| **Enunciado** | Un usuario evaluador no puede aprobar, rechazar o devolver una solicitud si es el mismo usuario que la radicó original o anónimamente (Prohibición de autoaprobación por conflicto de interés). |
| **Origen** | Criterio de rechazo HU28 CA2 (Disparador `trg_validar_aprobador`). |
| **RF que la vigilan** | RF-28, RF-29, RF-30 |

---

### Tabla 98. Regla de negocio RN-06 — Justificación obligatoria en fallos

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-06 |
| **Enunciado** | Todo dictamen de rechazo o devolución para ajustes sobre una solicitud exige obligatoriamente un comentario o justificación escrita no vacía. |
| **Origen** | Criterios de rechazo HU29 CA2 y HU30 CA2 (Restricción `chk_aprobacion_comentario`). |
| **RF que la vigilan** | RF-29, RF-30 |

> **Nota:** En la versión 1.1 se retiró de la regla la exigencia de «archivo adjunto» y de «mínimo 10 caracteres», porque no está respaldada por los criterios de aceptación de la HU-29 y la HU-30, ni por `aprobacion_solicitud` (que no tiene campo de adjunto), ni por la restricción `chk_aprobacion_comentario` del script.

---

### Tabla 99. Regla de negocio RN-07 — Rango de calificación de servicio

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-07 |
| **Enunciado** | La calificación del servicio prestado debe registrarse únicamente como un número entero dentro del rango del 1 al 5 inclusive y permitir acciones como comentarios, observaciones, validaciones, etc. |
| **Origen** | Criterio de rechazo HU37 CA4 (Validación de rango de evaluación). |
| **RF que la vigilan** | RF-37 |

---

### Tabla 100. Regla de negocio RN-08 — Contenido mínimo de la interacción

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-08 |
| **Enunciado** | Toda interacción o detalle registrado en el expediente de una solicitud debe contener obligatoriamente un mensaje de texto descriptivo, una ruta de archivo adjunto válida o ambos (Prohibición de registros vacíos). |
| **Origen** | Criterio de rechazo HU39 CA3 (Restricción `chk_detalle_contenido`). |
| **RF que la vigilan** | RF-39 |

---

### Tabla 101. Regla de negocio RN-09 — Trazabilidad inalterable de auditoría

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-09 |
| **Enunciado** | Los registros almacenados en la bitácora de auditoría son de solo lectura, inmutables e imperecederos; bajo ninguna circunstancia se permiten operaciones de modificación (`UPDATE`) o eliminación (`DELETE`). |
| **Origen** | Criterio de rechazo HU41 CA2 (Disparadores `trg_bitacora_no_update` y `trg_bitacora_no_delete`). |
| **RF que la vigilan** | RF-41, RF-45 |

---

### Tabla 102. Regla de negocio RN-10 — Integridad de eliminación

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-10 |
| **Enunciado** | Queda estrictamente prohibida la eliminación física (`DELETE`) de cuentas de usuario o roles que tengan transacciones o registros históricos asociados en el sistema; únicamente se permite su inactivación lógica. |
| **Origen** | Criterio de rechazo HU04 CA3 y HU08 CA2 (Restricción de integridad referencial `ON DELETE RESTRICT`). |
| **RF que la vigilan** | RF-04, RF-08 |

---

### Tabla 103. Regla de negocio RN-11 — Unicidad de gestión activa

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-11 |
| **Enunciado** | Una solicitud solo puede poseer una única gestión activa simultáneamente en estado `En_Proceso`. Toda reasignación debe marcar el registro previo como `Reasignado` antes de habilitar el nuevo. |
| **Origen** | Criterios de rechazo HU32 CA2 y HU33 CA1 (Disparador `trg_gestion_unica_activa`). |
| **RF que la vigilan** | RF-32, RF-33 |

---

### Tabla 104. Regla de negocio RN-12 — Coherencia del cierre de gestión

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-12 |
| **Enunciado** | La fecha y hora de finalización de una gestión (`fecha_cierre`) debe ser estrictamente igual o posterior a la fecha y hora de asignación del gestor (`fecha_vinculacion`). |
| **Origen** | Criterio de rechazo HU35 CA2 (Restricción temporal `chk_gestion_fechas`). |
| **RF que la vigilan** | RF-35 |

---

### Tabla 105. Regla de negocio RN-13 — Habilitación y unicidad de la evaluación

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-13 |
| **Enunciado** | Un solicitante únicamente puede registrar la evaluación de servicio cuando el estado de la gestión asociada se encuentre formalmente marcado como `Finalizado`. |
| **Origen** | Criterio de rechazo HU37 CA2 (Validación de estado para evaluación). |
| **RF que la vigilan** | RF-37 |

---

### Tabla 106. Regla de negocio RN-14 — Validez de la fecha de radicación

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-14 |
| **Enunciado** | La fecha de radicación (`fecha_radicacion`) asignada a una solicitud al pasar del estado `BORRADOR` a `PENDIENTE` es inalterable e inmutable a lo largo de todo el ciclo de vida del trámite. |
| **Origen** | Criterio de rechazo HU24 CA1 y HU24 CA2 (Preservación del sello de tiempo de radicación). |
| **RF que la vigilan** | RF-24 |

---

### Tabla 107. Regla de negocio RN-15 — Estado nuevo condicionado a la acción

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-15 |
| **Enunciado** | Todo cambio en el estado de una solicitud exige la inserción automática y obligatoria del registro de transición en la bitácora de auditoría, incluyendo el estado previo, el nuevo estado y el usuario responsable. |
| **Origen** | Criterios de rechazo HU25 CA1, HU25 CA2 y HU41 CA1 (Trazabilidad obligatoria de flujo). |
| **RF que la vigilan** | RF-24, RF-25, RF-28, RF-29, RF-30, RF-32, RF-35, RF-41 |

---

### Tabla 108. Regla de negocio RN-16 — Inactivación lógica de catálogos

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-16 |
| **Enunciado** | Un tipo de solicitud marcado como inactivo (`activo = false`) no puede ser seleccionado para la creación o radicación de nuevos formularios de requerimiento. |
| **Origen** | Criterios de rechazo HU17 CA2 y HU21 CA2 (Inactivación lógica de catálogos). |
| **RF que la vigilan** | RF-17, RF-21, RF-24 |

---

### Tabla 109. Regla de negocio RN-17 — Validación de unicidad y estado para asignación de rol

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-17 |
| **Enunciado** | El sistema debe impedir la asignación de un rol a un usuario si la cuenta se encuentra en estado inactivo o si el usuario ya posee dicho rol asignado, mostrando el mensaje de error correspondiente (*"El usuario ya cuenta con el rol asignado"*). |
| **Origen** | Criterios de rechazo HU-11 CA-2 y HU-11 CA-3 (Validación de unicidad de asignación y estado activo de la cuenta). |
| **RF que la vigilan** | RF-11, RF-44 |

---

### Tabla 110. Regla de negocio RN-18 — Mantenimiento de rol mínimo por usuario

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-18 |
| **Enunciado** | Toda cuenta de usuario registrada en la plataforma debe mantener al menos un rol asignado de forma activa, impidiendo la revocación total de sus perfiles. |
| **Origen** | Criterio de aceptación CA-2 de la historia de usuario HU-13 (Control de permisos y restricción de rol único mínimo). |
| **RF que la vigilan** | RF-13 |

---

### Tabla 111. Regla de negocio RN-19 — Bloqueo de edición en estados no permitidos

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-19 |
| **Enunciado** | El sistema debe bloquear la modificación del contenido o la descripción de una solicitud cuando esta ya no se encuentre en estado `"BORRADOR"` o `"PENDIENTE_AJUSTES"` (es decir, cuando esté en trámite o cerrada). |
| **Origen** | Criterio de aceptación CA-2 de la historia de usuario HU-23 (Restricción de estado permitido para la modificación de solicitudes). |
| **RF que la vigilan** | RF-23 |

---

### Tabla 112. Regla de negocio RN-20 — Control de privilegios para baja lógica

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-20 |
| **Enunciado** | La ejecución de la baja lógica sobre una solicitud exige la validación estricta de que el usuario emisor posea el rol de Administrador y que el identificador del trámite exista formalmente en el sistema, bloqueando la operación de lo contrario. |
| **Origen** | Criterio de aceptación CA-2 de la historia de usuario HU-27 (Restricción de privilegios y existencia de registro para inactivación). |
| **RF que la vigilan** | RF-27 |

---

### Tabla 113. Regla de negocio RN-21 — Unicidad del código de tipo de solicitud

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-21 |
| **Enunciado** | El código alfanumérico identificador de un tipo de solicitud debe ser estrictamente único en el sistema, impidiendo cualquier intento de registro o actualización que genere duplicidad (`uq_tipo_codigo`). |
| **Origen** | Criterios de aceptación CA-2 de la HU-14 y CA-2 de la HU-16 (Validación de unicidad del código de tipos de solicitud). |
| **RF que la vigilan** | RF-14, RF-16 |

---

### Tabla 114. Regla de negocio RN-22 — Unicidad de código y nombre de estados

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-22 |
| **Enunciado** | El código lógico y el nombre visible de un estado de solicitud deben ser estrictamente únicos en el sistema, impidiendo cualquier intento de registro que genere duplicidad en dichos catálogos (`uq_estado_codigo` y `uq_estado_nombre`). |
| **Origen** | Criterio de aceptación CA-2 de la historia de usuario HU-18 (Validación de unicidad de código y nombre de estados de solicitud). |
| **RF que la vigilan** | RF-18 |

---

### Tabla 115. Regla de negocio RN-23 — Restricción de alteración de estado final

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-23 |
| **Enunciado** | Se prohíbe modificar o alterar la bandera indicadora de estado final (`es_final`) en un estado de solicitud si existen trámites activos o registros vinculados que dependan de dicha configuración, protegiendo la integridad del flujo de trabajo. |
| **Origen** | Criterio de aceptación CA-2 de la historia de usuario HU-20 (Restricción de alteración de la bandera de estado final). |
| **RF que la vigilan** | RF-20 |

---

### Tabla 116. Regla de negocio RN-24 — Dominio de valores de prioridad de gestión

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-24 |
| **Enunciado** | El valor asignado al campo de prioridad de una gestión debe pertenecer obligatoriamente al dominio definido dentro de la enumeración autorizada `PrioridadGestion` (Baja, Media, Alta, Crítica), rechazando cualquier valor fuera de dicho catálogo. |
| **Origen** | Criterio de aceptación CA-2 de la historia de usuario HU-34 (Validación de dominio para el campo de prioridad de gestión). |
| **RF que la vigilan** | RF-34 |

---

### Tabla 117. Regla de negocio RN-25 — Control de acceso al módulo de auditoría

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-25 |
| **Enunciado** | La consulta de los reportes y módulos de auditoría exige de forma obligatoria que el usuario posea el rol de Gerente o Auditor, restringiendo el acceso y emitiendo una alerta de seguridad en caso de que un perfil sin dichos privilegios intente ingresar. |
| **Origen** | Criterio de aceptación CA-2 de la historia de usuario HU-42 (Control de acceso por rol para el módulo de auditoría y consultas gerenciales). |
| **RF que la vigilan** | RF-42, RF-45 |

---

### Tabla 118. Regla de negocio RN-26 — Consistencia de rangos de fechas en reportes

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-26 |
| **Enunciado** | El sistema debe rechazar y bloquear la ejecución de cualquier consulta o filtro de reportes cuando la fecha de inicio (*desde*) sea cronológicamente posterior a la fecha de término (*hasta*), previniendo rangos temporales inconsistentes. |
| **Origen** | Criterio de aceptación CA-2 de la historia de usuario HU-43 (Validación de consistencia en el rango de fechas para reportes). |
| **RF que la vigilan** | RF-43 |

---

### Tabla 119. Regla de negocio RN-27 — Validación de rol de gestión de personal

| Atributo | Detalle |
| ----- | ----- |
| **Código** | RN-27 |
| **Enunciado** | El sistema debe validar estrictamente que el usuario asignado como gestor posea formalmente el rol autorizado (`Gestion_Personal`), rechazando la operación o bloqueando el flujo si no cumple con este perfil mediante la validación del disparador (`trg_validar_gestor`). |
| **Origen** | Validación directa de diagrama de proceso y propuesta de regla de negocio (`trg_validar_gestor`). |
| **RF que la vigilan** | RF-32, RF-33 |
