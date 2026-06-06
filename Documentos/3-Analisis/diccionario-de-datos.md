Campo | Descripción
--------|-------------
Entidad | Usuario
Campo | id_usuario
Tipo | INT
Longitud | —
PK | Sí
Req. | Sí
Descripción / Regla de Negocio | Identificador único autoincremental de la cuenta.

Campo | Descripción
--------|-------------
Entidad | Usuario
Campo | nombre_completo
Tipo | VARCHAR
Longitud | 150
PK | No
Req. | Sí
Descripción / Regla de Negocio | Nombre y apellido del usuario.

Campo | Descripción
--------|-------------
Entidad | Usuario
Campo | correo_corporativo
Tipo | VARCHAR
Longitud | 150
PK | No
Req. | Sí
Descripción / Regla de Negocio | Correo único. Solo se permiten dominios empresariales.

Campo | Descripción
--------|-------------
Entidad | Usuario
Campo | contrasena_hash
Tipo | VARCHAR
Longitud | 255
PK | No
Req. | Sí
Descripción / Regla de Negocio | Contraseña encriptada. Bloqueo automático al tercer intento fallido.

Campo | Descripción
--------|-------------
Entidad | Usuario
Campo | rol
Tipo | ENUM
Longitud | —
PK | No
Req. | Sí
Descripción / Regla de Negocio | Valores: Solicitante, Aprobador, Gestion_Personal, Administrador.

Campo | Descripción
--------|-------------
Entidad | Usuario
Campo | estado_cuenta
Tipo | BOOLEAN
Longitud | —
PK | No
Req. | Sí
Descripción / Regla de Negocio | true = Activo; false = Suspendido/Inactivo.


Campo | Descripción
--------|-------------
Entidad | Solicitud
Campo | id_solicitud
Tipo | INT
Longitud | —
PK/FK | PK
Req. | Sí
Descripción / Regla de Negocio | Identificador único autoincremental (Número de Radicado oficial).

Campo | Descripción
--------|-------------
Entidad | Solicitud
Campo | id_solicitante
Tipo | INT
Longitud | —
PK/FK | FK
Req. | Sí
Descripción / Regla de Negocio | Referencia a Usuario.id_usuario. Solo usuarios con rol Solicitante.

Campo | Descripción
--------|-------------
Entidad | Solicitud
Campo | tipo_tramite
Tipo | ENUM
Longitud | —
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Valores: Peticion, Queja_Anonima.

Campo | Descripción
--------|-------------
Entidad | Solicitud
Campo | asunto
Tipo | VARCHAR
Longitud | 200
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Breve descripción del requerimiento.

Campo | Descripción
--------|-------------
Entidad | Solicitud
Campo | descripcion
Tipo | TEXT
Longitud | —
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Detalle completo de la solicitud.

Campo | Descripción
--------|-------------
Entidad | Solicitud
Campo | estado
Tipo | ENUM
Longitud | —
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Valores: Borrador, Pendiente, Pendiente_Ajustes, Solucionado, Rechazado.

Campo | Descripción
--------|-------------
Entidad | Solicitud
Campo | fecha_radicacion
Tipo | DATETIME
Longitud | —
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Fecha y hora exacta generada por el Estampado de Tiempo.

Campo | Descripción
--------|-------------
Entidad | Solicitud
Campo | anonimo_bloqueado
Tipo | BOOLEAN
Longitud | —
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | true oculta datos del creador; solo el Gerente puede levantar la restricción.


Campo | Descripción
--------|-------------
Entidad | Soporte
Campo | id_soporte
Tipo | INT
Longitud | —
PK/FK | PK
Req. | Sí
Descripción / Regla de Negocio | Identificador único autoincremental.

Campo | Descripción
--------|-------------
Entidad | Soporte
Campo | id_solicitud
Tipo | INT
Longitud | —
PK/FK | FK
Req. | Sí
Descripción / Regla de Negocio | Referencia a Solicitud.id_solicitud.

Campo | Descripción
--------|-------------
Entidad | Soporte
Campo | nombre_archivo
Tipo | VARCHAR
Longitud | 255
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Nombre original del documento cargado.

Campo | Descripción
--------|-------------
Entidad | Soporte
Campo | ruta_almacenamiento
Tipo | VARCHAR
Longitud | 500
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Ruta segura donde se almacena el archivo.

Campo | Descripción
--------|-------------
Entidad | Soporte
Campo | tamano_kb
Tipo | INT
Longitud | —
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Tamaño del archivo en KB. Máximo permitido: 2048 KB (2 MB).


Campo | Descripción
--------|-------------
Entidad | Evaluacion
Campo | id_evaluacion
Tipo | INT
Longitud | —
PK/FK | PK
Req. | Sí
Descripción / Regla de Negocio | Identificador único autoincremental.

Campo | Descripción
--------|-------------
Entidad | Evaluacion
Campo | id_solicitud
Tipo | INT
Longitud | —
PK/FK | FK
Req. | Sí
Descripción / Regla de Negocio | Relación 1:1 con Solicitud.id_solicitud.

Campo | Descripción
--------|-------------
Entidad | Evaluacion
Campo | id_revisor
Tipo | INT
Longitud | —
PK/FK | FK
Req. | Sí
Descripción / Regla de Negocio | Referencia a Usuario.id_usuario. Rol requerido: Evaluador / Aprobador.

Campo | Descripción
--------|-------------
Entidad | Evaluacion
Campo | decision
Tipo | ENUM
Longitud | —
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Valores: Aprobar, Rechazar, Devolver_Ajustes.

Campo | Descripción
--------|-------------
Entidad | Evaluacion
Campo | justificacion
Tipo | TEXT
Longitud | —
PK/FK | —
Req. | No
Descripción / Regla de Negocio | Obligatoria si la decisión es Rechazar. Mínimo 50 caracteres.

Campo | Descripción
--------|-------------
Entidad | Evaluacion
Campo | sello_digital
Tipo | VARCHAR
Longitud | 500
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Token criptográfico inalterable que certifica el cierre.


Campo | Descripción
--------|-------------
Entidad | Log_auditoria
Campo | id_log
Tipo | INT
Longitud | —
PK/FK | PK
Req. | Sí
Descripción / Regla de Negocio | Identificador único autoincremental. No permite borrado ni edición.

Campo | Descripción
--------|-------------
Entidad | Log_auditoria
Campo | id_usuario
Tipo | INT
Longitud | —
PK/FK | FK
Req. | No
Descripción / Regla de Negocio | Usuario responsable del evento. Puede ser nulo si proviene de proceso automático.

Campo | Descripción
--------|-------------
Entidad | Log_auditoria
Campo | accion
Tipo | VARCHAR
Longitud | 100
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Acción registrada. Ejemplos: AUTENTICACION_FALLIDA, REVELAR_ANONIMATO.

Campo | Descripción
--------|-------------
Entidad | Log_auditoria
Campo | direccion_ip
Tipo | VARCHAR
Longitud | 45
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Dirección IP del origen. Compatible con IPv4 e IPv6.

Campo | Descripción
--------|-------------
Entidad | Log_auditoria
Campo | detalles_justificados
Tipo | TEXT
Longitud | —
PK/FK | —
Req. | No
Descripción / Regla de Negocio | Motivos de fuerza mayor o explicaciones adicionales.

Campo | Descripción
--------|-------------
Entidad | Log_auditoria
Campo | fecha_evento
Tipo | DATETIME
Longitud | —
PK/FK | —
Req. | Sí
Descripción / Regla de Negocio | Fecha y hora del evento, registrada automáticamente con zona horaria del servidor.
