Entidad: Usuario

atributo | tipo | PK | Req | regla de negocio
--------|------|----|-----|-----------------
id_usuario | INT | Sí | Sí | Identificador único autoincremental de la cuenta.
nombre_completo | VARCHAR(150) | No | Sí | Nombre y apellido del usuario.
correo_corporativo | VARCHAR(150) | No | Sí | Correo único. Solo se permiten dominios empresariales.
contrasena_hash | VARCHAR(255) | No | Sí | Contraseña encriptada. Bloqueo automático al tercer intento fallido.
rol | ENUM | No | Sí | Valores: Solicitante, Aprobador, Gestion_Personal, Administrador.
estado_cuenta | BOOLEAN | No | Sí | true = Activo; false = Suspendido/Inactivo.

Entidad: solicitud

atributo | tipo | PK/FK | Req | regla de negocio
--------|------|--------|-----|-----------------
id_solicitud | INT | PK | Sí | Identificador único autoincremental (Número de Radicado oficial).
id_solicitante | INT | FK | Sí | Referencia a Usuario.id_usuario. Solo usuarios con rol Solicitante.
tipo_tramite | ENUM | — | Sí | Valores: Peticion, Queja_Anonima.
asunto | VARCHAR(200) | — | Sí | Breve descripción del requerimiento.
descripcion | TEXT | — | Sí | Detalle completo de la solicitud.
estado | ENUM | — | Sí | Borrador, Pendiente, Pendiente_Ajustes, Solucionado, Rechazado.
fecha_radicacion | DATETIME | — | Sí | Fecha y hora exacta generada por el Estampado de Tiempo.
anonimo_bloqueado | BOOLEAN | — | Sí | true oculta datos del creador; solo el Gerente puede levantar la restricción.

Entidad: Soporte

atributo | tipo | PK/FK | Req | regla de negocio
--------|------|--------|-----|-----------------
id_soporte | INT | PK | Sí | Identificador único autoincremental.
id_solicitud | INT | FK | Sí | Referencia a Solicitud.id_solicitud.
nombre_archivo | VARCHAR(255) | — | Sí | Nombre original del documento cargado.
ruta_almacenamiento | VARCHAR(500) | — | Sí | Ruta segura donde se almacena el archivo.
tamano_kb | INT | — | Sí | Tamaño del archivo en KB. Máximo permitido: 2048 KB (2 MB).

Entidad: Evaluacion

atributo | tipo | PK/FK | Req | regla de negocio
--------|------|--------|-----|-----------------
id_evaluacion | INT | PK | Sí | Identificador único autoincremental.
id_solicitud | INT | FK | Sí | Relación 1:1 con Solicitud.id_solicitud.
id_revisor | INT | FK | Sí | Referencia a Usuario.id_usuario. Rol requerido: Evaluador/Aprobador.
decision | ENUM | — | Sí | Valores: Aprobar, Rechazar, Devolver_Ajustes.
justificacion | TEXT | — | No | Obligatoria si la decisión es Rechazar. Mínimo 50 caracteres.
sello_digital | VARCHAR(500) | — | Sí | Token criptográfico inalterable que certifica el cierre.

Entidad: Log_auditoria

atributo | tipo | PK/FK | Req | regla de negocio
--------|------|--------|-----|-----------------
id_log | INT | PK | Sí | Identificador único autoincremental. No permite borrado ni edición.
id_usuario | INT | FK | No | Usuario responsable del evento. Puede ser nulo si proviene de proceso automático.
accion | VARCHAR(100) | — | Sí | Acción registrada. Ejemplos: AUTENTICACION_FALLIDA, REVELAR_ANONIMATO.
direccion_ip | VARCHAR(45) | — | Sí | Dirección IP del origen. Compatible con IPv4 e IPv6.
detalles_justificados | TEXT | — | No | Motivos de fuerza mayor o explicaciones adicionales.
fecha_evento | DATETIME | — | Sí | Fecha y hora del evento, registrada automáticamente.
