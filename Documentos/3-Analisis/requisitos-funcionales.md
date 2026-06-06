Campo | Descripción
|--------|--------|
ID | RF 01
HU Relacionada | HU 01 (Registro Formal de Solicitudes)
Descripción | El sistema debe presentar un formulario digital de solicitud con los campos título, descripción, tipo de solicitud y nivel de urgencia.

Campo | Descripción
ID | RF 02
HU Relacionada | HU 01 (Registro Formal de Solicitudes)
Descripción | El sistema debe asignar automáticamente un número de radicado único con formato NEXA AAAA ##### a cada solicitud enviada exitosamente.

Campo | Descripción
ID | RF 03
HU Relacionada | HU 03 (Historial de Solicitudes Inmutables)
Descripción | El sistema debe bloquear cualquier opción para borrar o modificar solicitudes en estado Aprobada, Rechazada o Cerrada, y registrar usuario, fecha, hora y cambios realizados.

Campo | Descripción
ID | RF 04
HU Relacionada | HU 04 (Priorización de Solicitudes)
Descripción | El sistema debe ordenar las solicitudes por urgencia y luego por marca temporal. Gerencia podrá modificar la urgencia con justificación registrada en el log.

Campo | Descripción
ID | RF 05
HU Relacionada | HU 02 (Notificaciones Automáticas)
Descripción | El sistema debe enviar un correo electrónico automático al solicitante cada vez que el estado de su solicitud sea modificado en un plazo no mayor a 1 minuto.

Campo | Descripción
ID | RF 06
HU Relacionada | HU 02 (Notificaciones Automáticas)
Descripción | El sistema debe disparar una notificación in app en la campana de alertas del usuario al cambiar el estado de su solicitud.

Campo | Descripción
ID | RF 07
HU Relacionada | HU 04 (Priorización de Solicitudes)
Descripción | El sistema debe resaltar visualmente en la bandeja de Gerencia las solicitudes con urgencia crítica mediante color distintivo y posición preferente.

Campo | Descripción
ID | RF 08
HU Relacionada | HU 22 (Recuperación de contraseña)
Descripción | El sistema debe proveer una opción de "Recuperar Contraseña" en la interfaz de inicio de sesión.

Campo | Descripción
ID | RF 09
HU Relacionada | HU 11 (Privacidad de Solicitudes por Usuario)
Descripción | El sistema debe restringir la visibilidad según rol y registrar en el log cada acceso administrativo a solicitudes ajenas.

Campo | Descripción
ID | RF 10
HU Relacionada | HU 05 (Edición de Solicitudes Pendientes)
Descripción | El sistema debe permitir al solicitante editar su solicitud únicamente mientras esté en estado Pendiente.

Campo | Descripción
ID | RF 11
HU Relacionada | HU 05 (Edición de Solicitudes Pendientes)
Descripción | El sistema debe conservar la versión original y generar versiones correlativas (v1, v2, v3) visibles en el historial.

Campo | Descripción
ID | RF 12
HU Relacionada | HU 05 (Edición de Solicitudes Pendientes)
Descripción | El sistema debe notificar automáticamente a Gerencia cuando una solicitud en cola sea modificada.

Campo | Descripción
ID | RF 13
HU Relacionada | HU 06 (Notificación de Resoluciones Críticas)
Descripción | El sistema debe enviar notificaciones de alta prioridad cuando Gerencia apruebe solicitudes críticas.

Campo | Descripción
ID | RF 14
HU Relacionada | HU 06 (Notificación de Resoluciones Críticas)
Descripción | El sistema debe forzar la visualización de un mensaje emergente con acuse de lectura.

Campo | Descripción
ID | RF 15
HU Relacionada | HU 06 (Notificación de Resoluciones Críticas)
Descripción | El sistema debe registrar qué coordinadores acusaron recibido de cada resolución crítica.

Campo | Descripción
ID | RF 16
HU Relacionada | HU 07 (Delegación de Autoridad en Contingencias)
Descripción | El sistema debe permitir configurar delegado, fechas y categorías autorizadas.

Campo | Descripción
ID | RF 17
HU Relacionada | HU 07 (Delegación de Autoridad en Contingencias)
Descripción | El sistema debe restringir las acciones del delegado solo a categorías autorizadas.

Campo | Descripción
ID | RF 18
HU Relacionada | HU 07 (Delegación de Autoridad en Contingencias)
Descripción | El sistema debe enviar un resumen diario al Gerente con las decisiones del delegado.

Campo | Descripción
ID | RF 19
HU Relacionada | HU 08 (Gestión de Evidencia Digital)
Descripción | El sistema debe generar un comprobante PDF con radicado, solicitante, aprobador, fechas, estado y firmas digitales.

Campo | Descripción
ID | RF 20
HU Relacionada | HU 08 (Gestión de Evidencia Digital)
Descripción | El sistema debe incluir un código QR en el PDF que redirija a una URL pública de validación.

Campo | Descripción
ID | RF 21
HU Relacionada | HU 08 (Gestión de Evidencia Digital)
Descripción | El sistema debe enviar automáticamente el comprobante PDF al solicitante al cerrar la solicitud.

Campo | Descripción
ID | RF 22
HU Relacionada | HU 09 (Seguimiento Visual de Estados)
Descripción | El sistema debe mostrar un tablero con semáforo: rojo, amarillo y verde.

Campo | Descripción
ID | RF 23
HU Relacionada | HU 09 (Seguimiento Visual de Estados)
Descripción | El sistema debe mostrar un ícono de alerta en solicitudes sin gestión por más de 3 días hábiles.

Campo | Descripción
ID | RF 24
HU Relacionada | HU 10 (Validación de Datos Obligatorios)
Descripción | El sistema debe validar en tiempo real que todos los campos obligatorios estén completos.

Campo | Descripción
ID | RF 25
HU Relacionada | HU 10 (Validación de Datos Obligatorios)
Descripción | El sistema debe impedir caracteres inválidos como <, >, {, }.

Campo | Descripción
ID | RF 26
HU Relacionada | HU 10 (Validación de Datos Obligatorios)
Descripción | El sistema debe validar coherencia lógica de fechas.

Campo | Descripción
ID | RF 27
HU Relacionada | HU 11 (Privacidad de Solicitudes por Usuario)
Descripción | El sistema debe ocultar el nombre del solicitante en solicitudes tipo Queja Anónima.

Campo | Descripción
ID | RF 28
HU Relacionada | HU 12 (Comentario de Rechazo o Ajuste)
Descripción | El sistema debe exigir comentario mínimo de 50 caracteres al rechazar.

Campo | Descripción
ID | RF 29
HU Relacionada | HU 12 (Comentario de Rechazo o Ajuste)
Descripción | El sistema debe permitir adjuntar un documento guía al rechazar.

Campo | Descripción
ID | RF 30
HU Relacionada | HU 12 (Comentario de Rechazo o Ajuste)
Descripción | El sistema debe habilitar un botón de Apelación para el solicitante.

Campo | Descripción
ID | RF 31
HU Relacionada | HU 13 (Filtro de Solicitudes por Área)
Descripción | El sistema debe permitir filtrar solicitudes por departamentos.

Campo | Descripción
ID | RF 32
HU Relacionada | HU 13 (Filtro de Solicitudes por Área)
Descripción | El sistema debe permitir guardar filtros favoritos.

Campo | Descripción
ID | RF 33
HU Relacionada | HU 13 (Filtro de Solicitudes por Área)
Descripción | El sistema debe permitir exportar datos filtrados a CSV o XLSX.

Campo | Descripción
ID | RF 34
HU Relacionada | HU 14 (Confirmación de Lectura)
Descripción | Registrar fecha y hora exactas en que Gerencia abre una solicitud.

Campo | Descripción
ID | RF 35
HU Relacionada | HU 14 (Confirmación de Lectura)
Descripción | Cambiar ícono de Nuevo a Visto al abrir la solicitud.

Campo | Descripción
ID | RF 36
HU Relacionada | HU 14 (Confirmación de Lectura)
Descripción | Notificar al solicitante cuando Gerencia visualice su solicitud.

Campo | Descripción
ID | RF 37
HU Relacionada | HU 14 (Escalamiento por Inactividad)
Descripción | Marcar como Gestión en Retraso si no se abre en 24 horas hábiles.

Campo | Descripción
ID | RF 38
HU Relacionada | HU 15 (Cierre con Confirmación)
Descripción | Requerir confirmación explícita del solicitante para cerrar.

Campo | Descripción
ID | RF 39
HU Relacionada | HU 15 (Cierre con Confirmación)
Descripción | Permitir calificar la atención con 1 a 5 estrellas.

Campo | Descripción
ID | RF 40
HU Relacionada | HU 15 (Cierre con Confirmación)
Descripción | Habilitar campo de observaciones finales.

Campo | Descripción
ID | RF 41
HU Relacionada | HU 16 (Alerta de Solicitudes Estancadas)
Descripción | Notificar al Gerente cuando una solicitud urgente lleve más de 3 días sin atención.

Campo | Descripción
ID | RF 42
HU Relacionada | HU 16 (Alerta de Solicitudes Estancadas)
Descripción | Mostrar semáforo de solicitudes estancadas.

Campo | Descripción
ID | RF 43
HU Relacionada | HU 16 (Alerta de Solicitudes Estancadas)
Descripción | Enviar reporte semanal de cuellos de botella cada lunes a las 8 a.m.

Campo | Descripción
ID | RF 44
HU Relacionada | HU 22 (Recuperación de Contraseña)
Descripción | Enviar enlace de restablecimiento con vigencia de 15 minutos.

Campo | Descripción
ID | RF 45
HU Relacionada | HU 17 (Autenticación de Usuarios)
Descripción | Validar usuario y contraseña corporativa.

Campo | Descripción
ID | RF 46
HU Relacionada | HU 17 (Autenticación de Usuarios)
Descripción | Bloquear cuenta por 15 minutos tras 3 intentos fallidos.

Campo | Descripción
ID | RF 47
HU Relacionada | HU 17 (Autenticación de Usuarios)
Descripción | Expirar sesión tras 20 minutos sin actividad.

Campo | Descripción
ID | RF 48
HU Relacionada | HU 17 (Autenticación de Usuarios)
Descripción | Redirigir al usuario según su rol al iniciar sesión.

Campo | Descripción
ID | RF 49
HU Relacionada | HU 17 (Autenticación de Usuarios)
Descripción | Restringir acceso a menús y botones según permisos.

Campo | Descripción
ID | RF 50
HU Relacionada | HU 18 (Búsqueda de Solicitudes)
Descripción | Incluir barra de búsqueda avanzada por palabra clave, radicado, fecha o estado.

Campo | Descripción
ID | RF 51
HU Relacionada | HU 19 (Dashboard Principal)
Descripción | Mostrar panel gráfico con métricas en tiempo real.

Campo | Descripción
ID | RF 52
HU Relacionada | HU 20 (Consulta del Log de Auditoría)
Descripción | Permitir solo al Administrador ver el log técnico con fecha, hora, IP y acción.

Campo | Descripción
ID | RF 53
HU Relacionada | HU 21 (Proceso de Cierre Automático)
Descripción | El sistema debe cerrar automáticamente y calificar con 3 estrellas los casos que cumplan 5 días hábiles sin confirmación del empleado.

