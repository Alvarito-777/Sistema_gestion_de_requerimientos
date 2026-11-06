### Entidad: `rol`

#### Diccionario de datos de la tabla `rol`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_rol` | INT UNSIGNED | — | PK | Sí | Identificador único autoincremental del perfil de acceso. | — | AUTO_INCREMENT | `pk_rol` | PRIMARY KEY, AUTO_INCREMENT |
| `nombre_rol` | VARCHAR | 50 | — | Sí | Nombre único del perfil de acceso. Dominio autorizado (RN-03): 'Solicitante', 'Aprobador', 'Gestion_Personal', 'Gerente', 'Administrador'. | — | Sin valor | `uq_rol_nombre` | NOT NULL, UNIQUE (nombre_rol) |
| `descripcion` | VARCHAR | 255 | — | Sí | Explicación del alcance y las responsabilidades funcionales del rol. | — | Sin valor | — | NOT NULL |
| `permiso_administrar` | BOOLEAN | — | — | Sí | Indica si el perfil posee privilegios de superusuario técnico: configuración del sistema y desblindaje de identidades anónimas. No controla los permisos operativos ordinarios, que se derivan del rol asignado. | — | FALSE | — | NOT NULL |
| `fecha_creacion` | DATETIME | — | — | Sí | Fecha y hora exacta de creación del registro del rol. | — | CURRENT_TIMESTAMP | — | NOT NULL |

> **Justificación sobre el campo `permiso_administrar`:** Cada uno de los cinco roles tiene sus funciones operativas definidas en la lógica de la aplicación. El campo no es un interruptor que controle todas las acciones del sistema, sino un permiso especial de superusuario. Su única función a nivel de base de datos es identificar si un rol accede a la administración técnica global. Los demás permisos se resuelven según el rol asignado a cada usuario.

---

### Entidad: `usuario`

#### Diccionario de datos de la tabla `usuario`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_usuario` | INT UNSIGNED | — | PK | Sí | Identificador único autoincremental de la cuenta de usuario. | — | AUTO_INCREMENT | `pk_usuario` | PRIMARY KEY, AUTO_INCREMENT |
| `nombre_completo` | VARCHAR | 150 | — | Sí | Nombres y apellidos completos del titular de la cuenta. | — | Sin valor | — | NOT NULL |
| `correo_corporativo` | VARCHAR | 150 | — | Sí | Correo institucional único; constituye la credencial de acceso. Regla RN-01: debe pertenecer al dominio corporativo. La validación se realiza en la capa de aplicación para no fijar el dominio en el esquema y evitar un `ALTER TABLE` ante cualquier cambio corporativo. | — | Sin valor | `uq_usuario_correo` | NOT NULL, UNIQUE (correo_corporativo) |
| `contrasena_hash` | VARCHAR | 255 | — | Sí | Resumen criptográfico de la contraseña (bcrypt o Argon2). Nunca se almacena la contraseña en texto plano. | — | Sin valor | — | NOT NULL |
| `estado_cuenta` | ENUM | — | — | Sí | Estado operativo de la cuenta: 'activo' (operativa), 'suspendido' (bloqueada automáticamente por intentos fallidos) e 'inactivo' (desactivada por el administrador). | — | 'activo' | `idx_usuario_estado` | NOT NULL, ENUM('activo','inactivo','suspendido') |
| `intentos_fallidos` | TINYINT UNSIGNED | — | — | Sí | Contador de intentos consecutivos de inicio de sesión fallidos. Regla RN-02: al llegar a 3 la cuenta pasa a suspendido y se registra `fecha_bloqueo`. Se reinicia en cero tras un acceso exitoso. | — | 0 | — | NOT NULL |
| `fecha_bloqueo` | DATETIME | — | — | No | Marca de tiempo del momento en que la cuenta pasó a estado suspendido. Permanece en `NULL` mientras la cuenta no haya sido bloqueada. | — | NULL | — | `chk_usuario_bloqueo` CHECK (estado_cuenta <> 'suspendido' OR fecha_bloqueo IS NOT NULL) |
| `fecha_creacion` | DATETIME | — | — | Sí | Fecha y hora exacta de creación de la cuenta. | — | CURRENT_TIMESTAMP | — | NOT NULL |

---

### Entidad: `usuario_rol`

#### Diccionario de datos de la tabla `usuario_rol`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_usuario` | INT UNSIGNED | — | PK / FK | Sí | Referencia a la cuenta que recibe el rol. Integra la clave primaria compuesta junto con `id_rol`. | `usuario.id_usuario` (1:N) | Sin valor | `pk_usuario_rol` (id_usuario, id_rol) | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `id_rol` | INT UNSIGNED | — | PK / FK | Sí | Referencia al perfil otorgado. Integra la clave primaria compuesta junto con `id_usuario`. | `rol.id_rol` (1:N) | Sin valor | `idx_usuario_rol_rol` | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `fecha_asignacion` | DATETIME | — | — | Sí | Fecha y hora exacta en que se asignó el rol a la cuenta. La revocación se registra en `bitacora_auditoria` con la acción 'Asignacion_Rol'. | — | CURRENT_TIMESTAMP | — | NOT NULL |

---

### Entidad: `tipo_solicitud`

#### Diccionario de datos de la tabla `tipo_solicitud`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_tipo_solicitud` | INT UNSIGNED | — | PK | Sí | Identificador único del tipo de requerimiento o trámite. | — | AUTO_INCREMENT | `pk_tipo_solicitud` | PRIMARY KEY, AUTO_INCREMENT |
| `codigo_tipo` | VARCHAR | 20 | — | Sí | Código alfanumérico único estandarizado para la categoría de trámite (ejemplos: 'PET-001', 'INC-002'). | — | Sin valor | `uq_tipo_codigo` | NOT NULL, UNIQUE (codigo_tipo) |
| `nombre_tipo` | VARCHAR | 50 | — | Sí | Nombre descriptivo oficial del tipo de solicitud. | — | Sin valor | — | NOT NULL |
| `descripcion` | VARCHAR | 255 | — | Sí | Explicación del propósito y alcance de este tipo de solicitud. | — | Sin valor | — | NOT NULL |
| `activo` | BOOLEAN | — | — | Sí | Regla RN-16: permite retirar la categoría de los formularios sin eliminarla, preservando la integridad de las solicitudes históricas que la referencian. | — | TRUE | — | NOT NULL |

---

### Entidad: `estado_solicitud`

#### Diccionario de datos de la tabla `estado_solicitud`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_estado_solicitud` | INT UNSIGNED | — | PK | Sí | Identificador único del estado dentro del catálogo centralizado. | — | AUTO_INCREMENT | `pk_estado_solicitud` | PRIMARY KEY, AUTO_INCREMENT |
| `codigo_estado` | VARCHAR | 30 | — | Sí | Código lógico único en mayúscula sostenida usado por la aplicación (ejemplos: 'BORRADOR', 'PENDIENTE'). Es el valor que consulta el código fuente, nunca el nombre visible. | — | Sin valor | `uq_estado_codigo` | NOT NULL, UNIQUE (codigo_estado) |
| `nombre_estado` | VARCHAR | 50 | — | Sí | Nombre visible único del estado: Borrador, Pendiente, Pendiente_Ajustes, Aprobada, En_Gestion, Solucionado, Rechazado. | — | Sin valor | `uq_estado_nombre` | NOT NULL, UNIQUE (nombre_estado) |
| `descripcion` | VARCHAR | 255 | — | No | Explicación del significado o etapa del estado dentro del flujo de trabajo. | — | NULL | — | — |
| `es_final` | BOOLEAN | — | — | Sí | Marca los estados terminales del flujo (Solucionado y Rechazado). Permite que la aplicación bloquee toda transición de salida sin codificar nombres de estado. | — | FALSE | — | NOT NULL |

---

### Entidad: `solicitud`

#### Diccionario de datos de la tabla `solicitud`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_solicitud` | INT UNSIGNED | — | PK | Sí | Número de radicado oficial e identificador único de la solicitud. | — | AUTO_INCREMENT | `pk_solicitud` | PRIMARY KEY, AUTO_INCREMENT |
| `id_solicitante` | INT UNSIGNED | — | FK | Sí | Usuario que radica la solicitud. | `usuario.id_usuario` (1:N) | Sin valor | `idx_solicitud_solicitante` | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `id_tipo_solicitud` | INT UNSIGNED | — | FK | Sí | Categoría de trámite asignada a la solicitud. | `tipo_solicitud.id_tipo_solicitud` (1:N) | Sin valor | `idx_solicitud_tipo` | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `id_estado_solicitud` | INT UNSIGNED | — | FK | Sí | Estado vigente de la solicitud dentro del flujo de trabajo. | `estado_solicitud.id_estado_solicitud` (1:N) | Sin valor | `idx_solicitud_estado_fecha` (id_estado_solicitud, fecha_radicacion) | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `asunto` | VARCHAR | 200 | — | Sí | Resumen ejecutivo o título breve del requerimiento. | — | Sin valor | — | NOT NULL |
| `descripcion` | TEXT | — | — | Sí | Detalle completo, justificación y alcance de la solicitud. | — | Sin valor | — | NOT NULL |
| `anonimo_bloqueado` | BOOLEAN | — | — | Sí | Bandera de confidencialidad. Regla RN-04: si es true la identidad del solicitante permanece oculta y solo los roles 'Gerente' y 'Administrador' pueden desblindarla. Todo desblindaje se audita. | — | FALSE | — | NOT NULL |
| `fecha_radicacion` | DATETIME | — | — | Sí | Marca de tiempo oficial de la radicación en el sistema. No es editable desde la interfaz. | — | CURRENT_TIMESTAMP | `idx_solicitud_estado_fecha` (compuesto) | NOT NULL; `trg_solicitud_fecha_radicacion` BEFORE INSERT y `trg_solicitud_fecha_inalterable` BEFORE UPDATE (RN-14). No implementable como CHECK: MySQL 8 rechaza funciones no deterministas. |
| `fecha_actualizacion` | DATETIME | — | — | Sí | Marca de tiempo de la última modificación del registro. Permite ordenar la bandeja de trabajo por actividad reciente y detectar casos estancados. | — | CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP | — | NOT NULL |

---

### Entidad: `aprobacion_solicitud`

#### Diccionario de datos de la tabla `aprobacion_solicitud`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_aprobacion` | INT UNSIGNED | — | PK | Sí | Identificador único del dictamen de aprobación emitido. | — | AUTO_INCREMENT | `pk_aprobacion` | PRIMARY KEY, AUTO_INCREMENT |
| `id_solicitud` | INT UNSIGNED | — | FK | Sí | Solicitud sobre la cual se emite el dictamen. Una solicitud acumula varios dictámenes cuando es devuelta para ajustes y reenviada. | `solicitud.id_solicitud` (1:N) | Sin valor | `idx_aprobacion_solicitud` | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `id_aprobador` | INT UNSIGNED | — | FK | Sí | Usuario que evalúa la solicitud. Regla RN-05: debe poseer rol Aprobador o Gerente y no puede coincidir con el solicitante. | `usuario.id_usuario` (1:N) | Sin valor | `idx_aprobacion_aprobador` | ON DELETE RESTRICT, ON UPDATE CASCADE; `trg_validar_aprobador` BEFORE INSERT; `trg_validar_aprobador_upd` BEFORE UPDATE |
| `decision` | ENUM | — | — | Sí | Dictamen emitido sobre la solicitud. Dominio: 'Aprobado', 'Rechazado', 'Devuelto_Para_Ajustes'. | — | Sin valor | — | NOT NULL, ENUM('Aprobado','Rechazado','Devuelto_Para_Ajustes') |
| `comentario` | TEXT | — | — | No | Justificación del dictamen. Regla RN-06: es obligatoria cuando la decisión es Rechazado o Devuelto_Para_Ajustes. | — | NULL | — | `chk_aprobacion_comentario` CHECK (decision = 'Aprobado' OR (comentario IS NOT NULL AND TRIM(comentario) <> '')) |
| `fecha_decision` | DATETIME | — | — | Sí | Fecha y hora en que se emitió el dictamen oficial. | — | CURRENT_TIMESTAMP | — | NOT NULL |

---

### Entidad: `gestion_solicitud`

#### Diccionario de datos de la tabla `gestion_solicitud`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_gestion` | INT UNSIGNED | — | PK | Sí | Identificador único del registro de asignación y operación del caso. | — | AUTO_INCREMENT | `pk_gestion` | PRIMARY KEY, AUTO_INCREMENT |
| `id_solicitud` | INT UNSIGNED | — | FK | Sí | Solicitud asignada para su resolución. Permite obtener los datos del solicitante por esta vía, sin redundancia transitiva. | `solicitud.id_solicitud` (1:N) | Sin valor | `idx_gestion_solicitud` | ON DELETE RESTRICT, ON UPDATE CASCADE; `trg_gestion_unica_activa` BEFORE INSERT y `trg_validar_gestor_upd` BEFORE UPDATE (RN-11) |
| `id_gestor` | INT UNSIGNED | — | FK | Sí | Usuario con rol 'Gestion_Personal' responsable del caso. | `usuario.id_usuario` (1:N) | Sin valor | `idx_gestion_gestor` | ON DELETE RESTRICT, ON UPDATE CASCADE; `trg_validar_gestor` BEFORE INSERT; `trg_validar_gestor_upd` BEFORE UPDATE |
| `prioridad` | ENUM | — | — | Sí | Nivel de urgencia asignado al caso: 'Baja', 'Media', 'Alta' o 'Critica'. | — | 'Media' | `idx_gestion_prioridad` | NOT NULL, ENUM('Baja','Media','Alta','Critica') |
| `estado_gestion` | ENUM | — | — | Sí | Estado propio de la asignación: 'En_Proceso', 'Reasignado', 'Finalizado'. Permite controlar cuál asignación está vigente cuando existe historial de reasignaciones. | — | 'En_Proceso' | `idx_gestion_estado` | NOT NULL, ENUM('En_Proceso','Reasignado','Finalizado') |
| `fecha_vinculacion` | DATETIME | — | — | Sí | Fecha y hora en que el gestor tomó o recibió la solicitud. | — | CURRENT_TIMESTAMP | — | NOT NULL |
| `fecha_cierre` | DATETIME | — | — | No | Fecha y hora de finalización operativa de la gestión. Regla RN-12: es obligatoria cuando estado_gestion es Finalizado. | — | NULL | — | `chk_gestion_fechas` CHECK (fecha_cierre IS NULL OR fecha_cierre >= fecha_vinculacion); `chk_gestion_cierre` CHECK (estado_gestion <> 'Finalizado' OR fecha_cierre IS NOT NULL) |

---

### Entidad: `evaluacion`

#### Diccionario de datos de la tabla `evaluacion`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_evaluacion` | INT UNSIGNED | — | PK | Sí | Identificador único de la encuesta de satisfacción emitida. | — | AUTO_INCREMENT | `pk_evaluacion` | PRIMARY KEY, AUTO_INCREMENT |
| `id_gestion` | INT UNSIGNED | — | FK | Sí | Asocia la evaluación con el registro de gestión que resolvió el caso, permitiendo métricas de desempeño por gestor sin cruces frágiles. | `gestion_solicitud.id_gestion` (1:0..1) | Sin valor | `uq_evaluacion_gestion` | UNIQUE (id_gestion), ON DELETE RESTRICT, ON UPDATE CASCADE; `trg_validar_evaluacion` BEFORE INSERT (RN-13) |
| `id_evaluador` | INT UNSIGNED | — | FK | Sí | Usuario que emite la evaluación. Regla RN-13: debe corresponder con el solicitante del radicado. Sustenta la asociación Usuario–Evaluacion del diagrama de clases. | `usuario.id_usuario` (1:N) | Sin valor | `idx_evaluacion_evaluador` | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `calificacion` | TINYINT UNSIGNED | — | — | Sí | Puntaje de satisfacción otorgado, de 1 a 5 estrellas. | — | Sin valor | — | NOT NULL, `chk_evaluacion_calificacion` CHECK (calificacion BETWEEN 1 AND 5) |
| `comentario` | TEXT | — | — | No | Opinión opcional sobre la calidad del servicio recibido. | — | NULL | — | — |
| `fecha_evaluacion` | DATETIME | — | — | Sí | Marca de tiempo del momento exacto en que el solicitante envió la evaluación. | — | CURRENT_TIMESTAMP | — | NOT NULL |

---

### Entidad: `detalle_solicitud`

#### Diccionario de datos de la tabla `detalle_solicitud`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_detalle` | INT UNSIGNED | — | PK | Sí | Identificador único de la interacción o respuesta en el historial del caso. | — | AUTO_INCREMENT | `pk_detalle` | PRIMARY KEY, AUTO_INCREMENT |
| `id_solicitud` | INT UNSIGNED | — | FK | Sí | Solicitud a la que pertenece la interacción. Relación de composición: el historial no tiene existencia sin la solicitud que lo contiene. | `solicitud.id_solicitud` (1:N Composición) | Sin valor | `idx_detalle_solicitud` (id_solicitud, fecha_registro) | ON DELETE CASCADE, ON UPDATE CASCADE |
| `id_usuario` | INT UNSIGNED | — | FK | Sí | Usuario autor del mensaje o del archivo adjunto. | `usuario.id_usuario` (1:N) | Sin valor | `idx_detalle_usuario` | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `mensaje` | TEXT | — | — | No | Contenido textual de la interacción. Regla RN-08: es opcional si se incluye un archivo adjunto. | — | NULL | — | `chk_detalle_contenido` CHECK (mensaje IS NOT NULL OR ruta_adjunto IS NOT NULL) |
| `ruta_adjunto` | VARCHAR | 512 | — | No | Ubicación o URL del archivo adjunto soportado. Regla RN-08: es opcional si se incluye contenido textual. La longitud se amplía a 512 porque las URL firmadas de los servicios de almacenamiento superan con frecuencia los 255 caracteres. | — | NULL | — | Ver `chk_detalle_contenido` |
| `fecha_registro` | DATETIME | — | — | Sí | Fecha y hora exacta en que se registró la interacción. | — | CURRENT_TIMESTAMP | — | NOT NULL |

---

### Entidad: `bitacora_auditoria`

#### Diccionario de datos de la tabla `bitacora_auditoria`

| Campo | Tipo | Longitud | PK / FK | Req. | Descripción / Regla de Negocio | Relación / Destino FK | Valor por defecto | Índices | Restricciones |
| :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| `id_bitacora` | BIGINT UNSIGNED | — | PK | Sí | Identificador único del evento de auditoría. Se usa BIGINT por el volumen esperado: la tabla registra incluso inicios y cierres de sesión. | — | AUTO_INCREMENT | `pk_bitacora` | PRIMARY KEY, AUTO_INCREMENT |
| `id_solicitud` | INT UNSIGNED | — | FK | No | Solicitud afectada cuando el evento se relaciona con un radicado. Permanece en NULL para eventos de seguridad o de administración de usuarios. | `solicitud.id_solicitud` (1:N) | NULL | `idx_bitacora_solicitud` | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `entidad_afectada` | VARCHAR | 50 | — | Sí | Nombre de la tabla sobre la cual se ejecutó la acción (ejemplos: 'usuario', 'usuario_rol', 'solicitud', 'gestion_solicitud'). | — | Sin valor | `idx_bitacora_entidad_registro` (entidad_afectada, id_registro_afectado) | NOT NULL |
| `id_registro_afectado` | INT UNSIGNED | — | — | Sí | Identificador del registro modificado dentro de la entidad indicada. | — | Sin valor | `idx_bitacora_entidad_registro` (compuesto) | NOT NULL |
| `id_usuario_accion` | INT UNSIGNED | — | FK | Sí | Usuario autor de la acción o cambio ejecutado en el sistema. | `usuario.id_usuario` (1:N) | Sin valor | `idx_bitacora_usuario` | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `accion_realizada` | ENUM | — | — | Sí | Tipo de operación ejecutada, bajo dominio controlado para facilitar la agrupación e informes de auditoría. Valores: 'Creacion', 'Modificacion', 'Eliminacion', 'Inicio_Sesion', 'Cierre_Sesion', 'Bloqueo_Cuenta', 'Cambio_Estado', 'Asignacion_Rol', 'Desbloqueo_Identidad'. | — | Sin valor | `idx_bitacora_accion` | NOT NULL, ENUM de 9 valores |
| `estado_anterior` | INT UNSIGNED | — | FK | No | Estado previo de la solicitud antes de la acción. Es nulo en la radicación inicial y en los eventos que no modifican el estado. | `estado_solicitud.id_estado_solicitud` (1:N) | NULL | `idx_bitacora_est_ant` | ON DELETE RESTRICT, ON UPDATE CASCADE |
| `estado_nuevo` | INT UNSIGNED | — | FK | No | Estado alcanzado tras la acción. Regla RN-15: es obligatorio únicamente cuando la acción registrada es 'Cambio_Estado'; un inicio de sesión o una asignación de rol no producen estado de solicitud. | `estado_solicitud.id_estado_solicitud` (1:N) | NULL | `idx_bitacora_est_nuev` | `trg_bitacora_cambio_estado` BEFORE INSERT. Equivale a `chk_bitacora_cambio_estado` (accion_realizada <> 'Cambio_Estado' OR estado_nuevo IS NOT NULL), que MySQL 8 no admite como CHECK sobre una columna FK con ON UPDATE CASCADE (error 3823). |
| `observaciones` | TEXT | — | — | No | Detalle o motivo de la transacción o modificación auditada. | — | NULL | — | — |
| `fecha_registro` | DATETIME | — | — | Sí | Estampa de tiempo inalterable del momento exacto de la acción. | — | CURRENT_TIMESTAMP | `idx_bitacora_fecha` | NOT NULL. Regla RN-09: REVOKE UPDATE, DELETE sobre la tabla y disparadores `trg_bitacora_no_update` y `trg_bitacora_no_delete` con SIGNAL SQLSTATE 45000. |
