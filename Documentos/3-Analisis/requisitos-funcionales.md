### Requisitos Funcionales

---

## Entidad: Rol

### RF-01 — Registrar nuevo rol de usuario
* **Código:** RF-01
* **Nombre corto:** Registrar nuevo rol de usuario
* **Descripción:** El sistema debe permitir al Administrador registrar un nuevo rol pidiendo el nombre, la descripción y si tiene permisos de administración. Además, debe verificar que el nombre no esté repetido y que sea uno de los permitidos por el sistema.
* **HU de origen:** HU-01
* **RN que hace cumplir:** RN-03 (Dominio de perfiles autorizados)
* **Prioridad:** Alta

---

### RF-02 — Consultar roles del sistema
* **Código:** RF-02
* **Nombre corto:** Consultar roles del sistema
* **Descripción:** El sistema debe permitir consultar la lista general de todos los roles registrados o buscar un rol específico por su código de identificación para ver su información detallada.
* **HU de origen:** HU-02
* **RN que hace cumplir:** Ninguna (Consulta general del catálogo)
* **Prioridad:** Media

---

### RF-03 — Actualizar información de un rol
* **Código:** RF-03
* **Nombre corto:** Actualizar información de un rol
* **Descripción:** El sistema debe permitir al Administrador modificar la descripción o los permisos de un rol ya existente, asegurándose de que los campos obligatorios no queden vacíos y que no se repita con el nombre de otro rol.
* **HU de origen:** HU-03
* **RN que hace cumplir:** RN-03 (Dominio de perfiles autorizados)
* **Prioridad:** Media

---

### RF-04 — Inactivar rol del sistema
* **Código:** RF-04
* **Nombre corto:** Inactivar rol del sistema
* **Descripción:** El sistema debe permitir desactivar un rol del catálogo de forma lógica tras una confirmación. El sistema debe bloquear la acción y avisar si el rol tiene usuarios activos asignados para proteger la integridad de los datos.
* **HU de origen:** HU-04
* **RN que hace cumplir:** RN-10 (Integridad de eliminación)
* **Prioridad:** Baja

---

## Entidad: Usuario

### RF-05 — Registrar usuario en la plataforma
* **Código:** RF-05
* **Nombre corto:** Registrar usuario en la plataforma
* **Descripción:** El sistema debe permitir al Administrador registrar un nuevo usuario pidiendo su correo corporativo y contraseña, asignándole automáticamente un estado activo y cero intentos fallidos. Además, debe validar que el correo pertenezca obligatoriamente al dominio autorizado y que no se encuentre duplicado.
* **HU de origen:** HU-05
* **RN que hace cumplir:** RN-01 (Dominio de correo corporativo)
* **Prioridad:** Alta

---

### RF-06 — Consultar expediente de usuario
* **Código:** RF-06
* **Nombre corto:** Consultar expediente de usuario
* **Descripción:** El sistema debe permitir consultar la información completa de un usuario específico buscando por su código de identificación, mostrando su correo, estado de cuenta, intentos fallidos y fecha de bloqueo en caso de tenerla.
* **HU de origen:** HU-06
* **RN que hace cumplir:** Ninguna (Control y auditoría de cuentas)
* **Prioridad:** Media

---

### RF-07 — Actualizar datos de usuario
* **Código:** RF-07
* **Nombre corto:** Actualizar datos de usuario
* **Descripción:** El sistema debe permitir al Administrador modificar la contraseña o los datos de un usuario existente. Si el estado de la cuenta cambia a suspendido, el sistema debe registrar automáticamente la fecha y hora actual del bloqueo.
* **HU de origen:** HU-07
* **RN que hace cumplir:** RN-01 (Dominio de correo corporativo); RN-02 (Bloqueo por intentos fallidos)
* **Prioridad:** Alta

---

### RF-08 — Inactivar cuenta de usuario
* **Código:** RF-08
* **Nombre corto:** Inactivar cuenta de usuario
* **Descripción:** El sistema debe permitir desactivar la cuenta de un usuario de forma lógica previa confirmación del Administrador, bloqueando su inicio de sesión pero manteniendo intactos sus registros históricos y relaciones en la base de datos.
* **HU de origen:** HU-08
* **RN que hace cumplir:** RN-10 (Integridad de eliminación)
* **Prioridad:** Alta

---

### RF-09 — Registrar intento fallido de autenticación
* **Código:** RF-09
* **Nombre corto:** Registrar intento fallido de autenticación
* **Descripción:** El sistema debe incrementar el contador de intentos fallidos cada vez que se ingrese una contraseña incorrecta. Si se alcanza el límite máximo permitido, la cuenta debe suspenderse automáticamente registrando la fecha y hora del bloqueo.
* **HU de origen:** HU-09
* **RN que hace cumplir:** RN-02 (Bloqueo por intentos fallidos)
* **Prioridad:** Alta

---

### RF-10 — Reiniciar intentos fallidos de autenticación
* **Código:** RF-10
* **Nombre corto:** Reiniciar intentos fallidos de autenticación
* **Descripción:** El sistema debe restablecer a cero el contador de intentos fallidos de forma automática tras un inicio de sesión exitoso, o de manera manual cuando un Administrador desbloquea y reactiva la cuenta limpiando su fecha de bloqueo.
* **HU de origen:** HU-10
* **RN que hace cumplir:** RN-02 (Bloqueo por intentos fallidos)
* **Prioridad:** Media

---

## Entidad: usuario_rol

### RF-11 — Asignar rol a usuario
* **Código:** RF-11
* **Nombre corto:** Asignar rol a usuario
* **Descripción:** El sistema debe permitir al Administrador asociar un rol específico a un usuario activo mediante sus identificadores, registrando automáticamente la fecha y hora de la asignación. Además, debe validar que el usuario no tenga el rol repetido y que la cuenta del usuario se encuentre activa.
* **HU de origen:** HU-11
* **RN que hace cumplir:** RN-17 (Validación de unicidad y estado para asignación de rol)
* **Prioridad:** Alta

---

### RF-12 — Consultar asignación de rol de un usuario
* **Código:** RF-12
* **Nombre corto:** Consultar asignación de rol de un usuario
* **Descripción:** El sistema debe permitir al Administrador verificar la relación específica entre un usuario y un rol utilizando sus identificadores, mostrando los detalles completos del vínculo y la fecha en que fue asignado.
* **HU de origen:** HU-12
* **RN que hace cumplir:** Ninguna (Consulta y control de asignaciones)
* **Prioridad:** Media

---

### RF-13 — Revocar rol asignado a usuario
* **Código:** RF-13
* **Nombre corto:** Revocar rol asignado a usuario
* **Descripción:** El sistema debe permitir al Administrador desvincular un rol específico de un usuario mediante sus identificadores para retirar sus permisos. El sistema debe validar obligatoriamente que el usuario conserve al menos un rol asignado en la plataforma antes de permitir la eliminación del vínculo.
* **HU de origen:** HU-13
* **RN que hace cumplir:** RN-18 (Mantenimiento de rol mínimo por usuario)
* **Prioridad:** Alta

---

### RF-44 — Actualizar asignación de rol de usuario
* **Código:** RF-44
* **Nombre corto:** Actualizar asignación de rol de usuario
* **Descripción:** El sistema debe permitir al Administrador modificar el rol asociado a un usuario existente, validando que el nuevo rol se encuentre activo y que no genere duplicidad en los permisos del usuario dentro de la plataforma.
* **HU de origen:** HU-44
* **RN que hace cumplir:** RN-17 (Validación de unicidad y estado para asignación de rol)
* **Prioridad:** Media

---

## Entidad: tipo_solicitud

### RF-14 — Crear tipo de solicitud
* **Código:** RF-14
* **Nombre corto:** Crear tipo de solicitud
* **Descripción:** El sistema debe permitir al Administrador registrar una nueva categoría o tipo de solicitud ingresando su código único, nombre y descripción, habilitándolo de forma automática con un estado activo. Además, debe validar que el código no se encuentre duplicado y que no falten campos obligatorios.
* **HU de origen:** HU-14
* **RN que hace cumplir:** RN-21 (Unicidad del código de tipo de solicitud)
* **Prioridad:** Alta

---

### RF-15 — Consultar tipo de solicitud
* **Código:** RF-15
* **Nombre corto:** Consultar tipo de solicitud
* **Descripción:** El sistema debe permitir consultar la información completa de un tipo de solicitud específico buscando por su identificador único, mostrando su código, nombre, descripción y estado actual (activo o inactivo).
* **HU de origen:** HU-15
* **RN que hace cumplir:** Ninguna (Consulta general de catálogo)
* **Prioridad:** Alta

---

### RF-16 — Actualizar tipo de solicitud
* **Código:** RF-16
* **Nombre corto:** Actualizar tipo de solicitud
* **Descripción:** El sistema debe permitir al Administrador modificar el nombre o la descripción de un tipo de solicitud existente. Asimismo, debe validar que si se modifica el código alfanumérico, este no colisione ni se duplique con otro registro previo.
* **HU de origen:** HU-16
* **RN que hace cumplir:** RN-21 (Unicidad del código de tipo de solicitud)
* **Prioridad:** Baja

---

### RF-17 — Inactivar tipo de solicitud
* **Código:** RF-17
* **Nombre corto:** Inactivar tipo de solicitud
* **Descripción:** El sistema debe permitir al Administrador inactivar de forma lógica un tipo de solicitud cambiando su atributo a falso, retirándolo de los formularios disponibles para nuevos trámites sin afectar ni eliminar los registros históricos previos.
* **HU de origen:** HU-17
* **RN que hace cumplir:** RN-16 (Inactivación lógica de catálogos)
* **Prioridad:** Media

---

## Entidad: estado_solicitud

### RF-18 — Crear estado de solicitud
* **Código:** RF-18
* **Nombre corto:** Crear estado de solicitud
* **Descripción:** El sistema debe permitir al Administrador registrar un nuevo estado de solicitud especificando su código único, nombre, descripción y si corresponde a un estado final, validando que no existan duplicados en el código o en el nombre.
* **HU de origen:** HU-18
* **RN que hace cumplir:** RN-22 (Unicidad de código y nombre de estados)
* **Prioridad:** Media

---

### RF-19 — Consultar estado de solicitud
* **Código:** RF-19
* **Nombre corto:** Consultar estado de solicitud
* **Descripción:** El sistema debe permitir a los usuarios consultar los datos descriptivos y la ficha de un estado de solicitud específico mediante su identificador único, mostrando su código, nombre, descripción y si es un estado final.
* **HU de origen:** HU-19
* **RN que hace cumplir:** Ninguna (Consulta general de catálogo)
* **Prioridad:** Alta

---

### RF-20 — Actualizar estado de solicitud
* **Código:** RF-20
* **Nombre corto:** Actualizar estado de solicitud
* **Descripción:** El sistema debe permitir al Administrador modificar el nombre o la descripción de un estado de solicitud existente. Además, debe bloquear la alteración de la bandera de estado final (`es_final`) si existen solicitudes activas vinculadas a dicho estado.
* **HU de origen:** HU-20
* **RN que hace cumplir:** RN-23 (Restricción de alteración de estado final)
* **Prioridad:** Baja

---

## Entidad: Solicitud

### RF-21 — Crear borrador de solicitud
* **Código:** RF-21
* **Nombre corto:** Crear borrador de solicitud
* **Descripción:** El sistema debe permitir al Solicitante crear una solicitud en estado de borrador ingresando un asunto, descripción y seleccionando un tipo de solicitud, asociando automáticamente el código del usuario, estableciendo el estado en "BORRADOR" y dejando la fecha de radicación en nulo. El sistema debe validar que el tipo de solicitud seleccionado esté activo[cite: 2].
* **HU de origen:** HU-21[cite: 2]
* **RN que hace cumplir:** RN-16 (Inactivación lógica de catálogos)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-22 — Consultar expediente de solicitud
* **Código:** RF-22
* **Nombre corto:** Consultar expediente de solicitud
* **Descripción:** El sistema debe permitir consultar los datos detallados de una solicitud mediante su identificador único, mostrando el asunto, descripción, tipo, estado, fecha de radicación y el solicitante. Si la solicitud es anónima (`anonimo_bloqueado = true`), el sistema debe proteger la identidad ocultando el nombre del solicitante con una etiqueta genérica[cite: 2].
* **HU de origen:** HU-22[cite: 2]
* **RN que hace cumplir:** RN-04 (Desblindaje de identidad anónima)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-23 — Actualizar contenido de solicitud
* **Código:** RF-23
* **Nombre corto:** Actualizar contenido de solicitud
* **Descripción:** El sistema debe permitir al Solicitante modificar el asunto o la descripción de una solicitud únicamente cuando se encuentre en estado "BORRADOR" o "PENDIENTE_AJUSTES", registrando la fecha de actualización. El sistema debe bloquear la edición si la solicitud ya está en trámite o cerrada[cite: 2].
* **HU de origen:** HU-23[cite: 2]
* **RN que hace cumplir:** RN-19 (Bloqueo de edición en estados no permitidos)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-24 — Radicar solicitud formalmente
* **Código:** RF-24
* **Nombre corto:** Radicar solicitud formalmente
* **Descripción:** El sistema debe permitir al Solicitante radicar formalmente una solicitud que se encuentre en estado de borrador y tenga la información completa, cambiando su estado a "PENDIENTE", generando un código único de radicado institucional y asignando una fecha de radicación inalterable[cite: 2].
* **HU de origen:** HU-24[cite: 2]
* **RN que hace cumplir:** RN-14 (Validez de la fecha de radicación); RN-15 (Estado nuevo condicionado a la acción); RN-16 (Inactivación lógica de catálogos)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-25 — Cambiar estado de la solicitud
* **Código:** RF-25
* **Nombre corto:** Cambiar estado de la solicitud
* **Descripción:** El sistema debe permitir actualizar el estado de una solicitud en el flujo de trabajo y registrar automáticamente la transición en la bitácora de auditoría (incluyendo estado previo, nuevo estado y fecha). Asimismo, debe impedir transiciones no válidas desde estados terminales[cite: 2].
* **HU de origen:** HU-25[cite: 2]
* **RN que hace cumplir:** RN-15 (Estado nuevo condicionado a la acción)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-26 — Desblindar identidad de solicitud anónima
* **Código:** RF-26
* **Nombre corto:** Desblindar identidad de solicitud anónima
* **Descripción:** El sistema debe permitir aos usuarios con rol de Gerente o Administrador revelar la identidad del solicitante en peticiones marcadas como anónimas, generando de inmediato un registro inmutable en la bitácora de auditoría y bloqueando la acción a usuarios que no posean los privilegios requeridos[cite: 2].
* **HU de origen:** HU-26[cite: 2]
* **RN que hace cumplir:** RN-04 (Desblindaje de identidad anónima)[cite: 2]
* **Prioridad:** Media[cite: 2]

---

### RF-27 — Inactivar solicitud
* **Código:** RF-27
* **Nombre corto:** Inactivar solicitud
* **Descripción:** El sistema debe permitir a un Administrador realizar la baja lógica de una solicitud existente mediante su identificador, cambiando su estado a inactivo y generando un registro correspondiente en la bitácora de auditoría. El sistema debe bloquear la acción si el usuario no tiene permisos o si la solicitud no existe[cite: 2].
* **HU de origen:** HU-27[cite: 2]
* **RN que hace cumplir:** RN-20 (Control de privilegios para baja lógica)[cite: 2]
* **Prioridad:** Media[cite: 2]

---

## Entidad: aprobacion_solicitud

### RF-28 — Aprobar solicitud
* **Código:** RF-28
* **Nombre corto:** Aprobar solicitud
* **Descripción:** El sistema debe permitir a un usuario con rol Aprobador o Gerente registrar la aprobación de una solicitud pendiente, cambiando su estado a "APROBADA" y registrando el comentario del dictamen. El sistema debe validar estrictamente que el evaluador no sea el mismo usuario que radicó la solicitud para evitar conflictos de interés[cite: 2].
* **HU de origen:** HU-28[cite: 2]
* **RN que hace cumplir:** RN-05 (Impedimento de autoaprobación); RN-15 (Estado nuevo condicionado a la acción)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-29 — Rechazar solicitud
* **Código:** RF-29
* **Nombre corto:** Rechazar solicitud
* **Descripción:** El sistema debe permitir al Aprobador o Gerente rechazar una solicitud pendiente ingresando una justificación obligatoria, actualizando el estado de la solicitud a "RECHAZADA" y notificando al solicitante. El sistema debe bloquear la acción si el comentario de rechazo está vacío[cite: 2].
* **HU de origen:** HU-29[cite: 2]
* **RN que hace cumplir:** RN-05 (Impedimento de autoaprobación); RN-06 (Justificación obligatoria en fallos); RN-15 (Estado nuevo condicionado a la acción)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-30 — Devolver solicitud para ajustes
* **Código:** RF-30
* **Nombre corto:** Devolver solicitud para ajustes
* **Descripción:** El sistema debe permitir al Aprobador o Gerente devolver una solicitud pendiente adjuntando observaciones obligatorias, cambiando su estado a "PENDIENTE_AJUSTES" y habilitando nuevamente los permisos de edición para el solicitante. El sistema debe exigir el ingreso del comentario para proceder[cite: 2].
* **HU de origen:** HU-30[cite: 2]
* **RN que hace cumplir:** RN-05 (Impedimento de autoaprobación); RN-06 (Justificación obligatoria en fallos); RN-15 (Estado nuevo condicionado a la acción)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-31 — Consultar dictamen de aprobación
* **Código:** RF-31
* **Nombre corto:** Consultar dictamen de aprobación
* **Descripción:** El sistema debe permitir consultar la información completa de un dictamen de aprobación mediante su identificador único, mostrando la decisión adoptada, el comentario, la fecha y el nombre del evaluador responsable[cite: 2].
* **HU de origen:** HU-31[cite: 2]
* **RN que hace cumplir:** Ninguna (Consulta y auditoría de dictámenes)[cite: 2]
* **Prioridad:** Media[cite: 2]

---

## Entidad: gestion_solicitud

### RF-32 — Asignar gestor a la solicitud
* **Código:** RF-32
* **Nombre corto:** Asignar gestor a la solicitud
* **Descripción:** El sistema debe permitir a un Gerente asignar una solicitud aprobada a un gestor activo especificando su nivel de prioridad, creando un registro de gestión en estado "En_Proceso", registrando la fecha de vinculación y cambiando el estado de la solicitud a "EN_GESTION". El sistema debe validar mediante un disparador que la solicitud no posea otra gestión activa simultáneamente[cite: 2].
* **HU de origen:** HU-32[cite: 2]
* **RN que hace cumplir:** RN-11 (Unicidad de gestión activa); RN-15 (Estado nuevo condicionado a la acción); RN-27 (Validación de rol de gestión de personal)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-33 — Reasignar gestor a la solicitud
* **Código:** RF-33
* **Nombre corto:** Reasignar gestor a la solicitud
* **Descripción:** El sistema debe permitir al Gerente redistribuir la carga operacional reasignando una solicitud a un gestor distinto. Al hacerlo, el sistema debe cambiar el estado del registro de gestión actual a "Reasignado", registrar su fecha de cierre y crear un nuevo registro de gestión en estado "En_Proceso" para el nuevo gestor, bloqueando la reasignación si se selecciona al mismo gestor actual[cite: 2].
* **HU de origen:** HU-33[cite: 2]
* **RN que hace cumplir:** RN-11 (Unicidad de gestión activa); RN-27 (Validación de rol de gestión de personal)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-34 — Actualizar prioridad de gestión
* **Código:** RF-34
* **Nombre corto:** Actualizar prioridad de gestión
* **Descripción:** El sistema debe permitir al personal de gestión modificar el nivel de prioridad asignado a un caso activo, validando estrictamente que el valor pertenezca a la enumeración permitida (Baja, Media, Alta, Critica) y rechazando cualquier parámetro no válido[cite: 2].
* **HU de origen:** HU-34[cite: 2]
* **RN que hace cumplir:** RN-24 (Dominio de valores de prioridad de gestión)[cite: 2]
* **Prioridad:** Media[cite: 2]

---

### RF-35 — Finalizar gestión de la solicitud
* **Código:** RF-35
* **Nombre corto:** Finalizar gestión de la solicitud
* **Descripción:** El sistema debe permitir al gestor marcar la atención de un caso como finalizada, actualizando el estado de la gestión a "Finalizado", registrando la fecha de cierre y cambiando el estado de la solicitud a "SOLUCIONADO". El sistema debe verificar mediante restricciones que la fecha de cierre no sea anterior a la fecha de vinculación del gestor[cite: 2].
* **HU de origen:** HU-35[cite: 2]
* **RN que hace cumplir:** RN-12 (Coherencia del cierre de gestión); RN-15 (Estado nuevo condicionado a la acción)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-36 — Consultar registro de gestión
* **Código:** RF-36
* **Nombre corto:** Consultar registro de gestión
* **Descripción:** El sistema debe permitir al Gerente consultar la información detallada de un registro de gestión buscando por su identificador único, mostrando la prioridad, el estado de la gestión, la fecha de vinculación y la fecha de cierre[cite: 2].
* **HU de origen:** HU-36[cite: 2]
* **RN que hace cumplir:** Ninguna (Consulta y seguimiento de registros operativos)[cite: 2]
* **Prioridad:** Media[cite: 2]

---

## Entidad: evaluacion

### RF-37 — Calificar servicio recibido
* **Código:** RF-37
* **Nombre corto:** Calificar servicio recibido
* **Descripción:** El sistema debe permitir al Solicitante calificar la atención recibida mediante un puntaje entero de 1 a 5 y un comentario opcional, asociándolo a una gestión. El sistema debe validar estrictamente que la gestión esté formalmente finalizada, que no exista una evaluación previa para el mismo caso y que el puntaje se encuentre dentro del rango permitido[cite: 2].
* **HU de origen:** HU-37[cite: 2]
* **RN que hace cumplir:** RN-07 (Rango de calificación de servicio); RN-13 (Habilitación y unicidad de la evaluación)[cite: 2]
* **Prioridad:** Media[cite: 2]

---

### RF-38 — Consultar evaluación de servicio
* **Código:** RF-38
* **Nombre corto:** Consultar evaluación de servicio
* **Descripción:** El sistema debe permitir al Gerente General consultar la información detallada de una evaluación de servicio buscando por su identificador único, mostrando el puntaje obtenido, el comentario, la fecha y el código de la gestión asociada[cite: 2].
* **HU de origen:** HU-38[cite: 2]
* **RN que hace cumplir:** Ninguna (Consulta y análisis de métricas de satisfacción)[cite: 2]
* **Prioridad:** Media[cite: 2]

---

## Entidad: detalle_solicitud

### RF-39 — Crear detalle o interacción en solicitud
* **Código:** RF-39
* **Nombre corto:** Crear detalle o interacción en solicitud
* **Descripción:** El sistema debe permitir publicar mensajes o adjuntar archivos en el historial de una solicitud, registrando automáticamente la fecha y hora de la interacción. El sistema debe validar que la publicación contenga al menos un mensaje de texto o un archivo adjunto, rechazando interacciones completamente vacías[cite: 2].
* **HU de origen:** HU-39[cite: 2]
* **RN que hace cumplir:** RN-08 (Contenido mínimo de la interacción)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-40 — Consultar detalles de una solicitud
* **Código:** RF-40
* **Nombre corto:** Consultar detalles de una solicitud
* **Descripción:** El sistema debe permitir consultar todo el historial conversacional y los archivos adjuntos vinculados a una solicitud específica, mostrando el listado de interacciones ordenado de forma cronológica (de la más antigua a la más reciente)[cite: 2].
* **HU de origen:** HU-40[cite: 2]
* **RN que hace cumplir:** Ninguna (Consulta cronológica del hilo conversacional)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

## Entidad: bitacora_auditoria

### RF-41 — Registrar acción de auditoría
* **Código:** RF-41
* **Nombre corto:** Registrar acción de auditoría
* **Descripción:** El sistema debe registrar automáticamente en la bitácora de auditoría cada evento relevante de la aplicación (creación, modificación, eliminación, inicio y cierre de sesión, bloqueo de cuenta, cambio de estado, asignación de rol y desbloqueo de identidad), con la entidad y el registro afectados, el usuario que ejecuta la acción, los estados anterior y nuevo cuando la acción es un cambio de estado, y la fecha y hora del evento. Los registros son de solo lectura e inmutables (RN-09) y todo cambio de estado de una solicitud debe quedar registrado (RN-15)[cite: 2].
* **HU de origen:** HU-41[cite: 2]
* **RN que hace cumplir:** RN-09 (Trazabilidad inalterable de auditoría); RN-15 (Estado nuevo condicionado a la acción)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-42 — Consultar auditoría por entidad y registro
* **Código:** RF-42
* **Nombre corto:** Consultar auditoría por entidad y registro
* **Descripción:** El sistema debe permitir a los usuarios con rol de Gerente o Auditor consultar las trazas de auditoría filtradas por entidad e identificador de registro. El sistema restringirá el acceso a esta consulta a usuarios que no posean dichos roles[cite: 2].
* **HU de origen:** HU-42[cite: 2]
* **RN que hace cumplir:** RN-25 (Control de acceso al módulo de auditoría)[cite: 2]
* **Prioridad:** Alta[cite: 2]

---

### RF-43 — Consultar auditoría por rango de fechas
* **Código:** RF-43
* **Nombre corto:** Consultar auditoría por rango de fechas
* **Descripción:** El sistema debe permitir a los usuarios autorizados generar reportes de las trazas de auditoría ocurridas dentro de un periodo de tiempo específico, validando que la fecha inicial (desde) no sea posterior a la fecha final (hasta)[cite: 2].
* **HU de origen:** HU-43[cite: 2]
* **RN que hace cumplir:** RN-26 (Consistencia de rangos de fechas en reportes)[cite: 2]
* **Prioridad:** Alta[cite: 2]
