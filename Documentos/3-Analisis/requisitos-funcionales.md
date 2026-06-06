## RF 01 – Registro Formal de Solicitudes
**HU Relacionada:** HU 01  
**Descripción:** El sistema debe presentar un formulario digital de solicitud con los campos título, descripción, tipo de solicitud y nivel de urgencia.


## RF 02 – Asignación Automática de Radicado
**HU Relacionada:** HU 01  
**Descripción:** El sistema debe asignar automáticamente un número de radicado único con formato NEXA AAAA ##### a cada solicitud enviada exitosamente.


## RF 03 – Inmutabilidad del Historial
**HU Relacionada:** HU 03  
**Descripción:** El sistema debe bloquear cualquier opción para borrar o modificar solicitudes en estado Aprobada, Rechazada o Cerrada, y registrar usuario, fecha, hora y cambios realizados.


## RF 04 – Priorización de Solicitudes
**HU Relacionada:** HU 04  
**Descripción:** Ordenar solicitudes por urgencia y luego por marca temporal. Gerencia puede modificar urgencia con justificación registrada en el log.


## RF 05 – Notificación por Correo
**HU Relacionada:** HU 02  
**Descripción:** Enviar correo automático al solicitante cada vez que el estado cambie, en menos de 1 minuto.


## RF 06 – Notificación In‑App
**HU Relacionada:** HU 02  
**Descripción:** Disparar notificación en la campana de alertas cuando el estado cambie.


## RF 07 – Resaltado de Urgencias Críticas
**HU Relacionada:** HU 04  
**Descripción:** Resaltar visualmente solicitudes críticas en la bandeja de Gerencia.


## RF 08 – Recuperación de Contraseña
**HU Relacionada:** HU 22  
**Descripción:** Proveer opción de “Recuperar Contraseña” en el inicio de sesión.


## RF 09 – Privacidad y Auditoría
**HU Relacionada:** HU 11  
**Descripción:** Restringir visibilidad según rol y registrar accesos administrativos en el log.


## RF 10 – Edición de Solicitudes Pendientes
**HU Relacionada:** HU 05  
**Descripción:** Permitir edición solo mientras la solicitud esté en estado Pendiente.


## RF 11 – Versionamiento de Solicitudes
**HU Relacionada:** HU 05  
**Descripción:** Conservar versión original y generar versiones v1, v2, v3 visibles en historial.


## RF 12 – Notificación a Gerencia por Edición
**HU Relacionada:** HU 05  
**Descripción:** Notificar automáticamente a Gerencia cuando una solicitud en cola sea modificada.


## RF 13 – Notificaciones Críticas a Coordinadores
**HU Relacionada:** HU 06  
**Descripción:** Enviar notificaciones de alta prioridad cuando Gerencia apruebe solicitudes críticas.


## RF 14 – Mensaje Emergente de Resoluciones Críticas
**HU Relacionada:** HU 06  
**Descripción:** Forzar visualización de mensaje emergente con acuse de lectura.


## RF 15 – Reporte de Lectura de Resoluciones
**HU Relacionada:** HU 06  
**Descripción:** Registrar qué coordinadores leyeron cada resolución crítica.


## RF 16 – Configuración de Delegación
**HU Relacionada:** HU 07  
**Descripción:** Permitir configurar delegado, fechas y categorías autorizadas.


## RF 17 – Restricción de Acciones del Delegado
**HU Relacionada:** HU 07  
**Descripción:** Limitar acciones del delegado solo a categorías autorizadas.


## RF 18 – Resumen Diario al Gerente
**HU Relacionada:** HU 07  
**Descripción:** Enviar resumen diario con decisiones tomadas por el delegado.


## RF 19 – Comprobante PDF de Solicitudes Finalizadas
**HU Relacionada:** HU 08  
**Descripción:** Generar PDF con radicado, solicitante, aprobador, fechas, estado y firmas digitales.


## RF 20 – Código QR en Comprobante
**HU Relacionada:** HU 08  
**Descripción:** Incluir QR que redirija a URL pública de validación.


## RF 21 – Envío Automático del Comprobante
**HU Relacionada:** HU 08  
**Descripción:** Enviar el PDF al correo del solicitante al cerrar la solicitud.


## RF 22 – Tablero Visual del Solicitante
**HU Relacionada:** HU 09  
**Descripción:** Mostrar tablero con semáforo: rojo, amarillo, verde.


## RF 23 – Alertas por Falta de Gestión
**HU Relacionada:** HU 09  
**Descripción:** Mostrar ícono de alerta en solicitudes sin gestión por más de 3 días hábiles.


## RF 24 – Validación de Campos Obligatorios
**HU Relacionada:** HU 10  
**Descripción:** Validar en tiempo real que todos los campos obligatorios estén completos.


## RF 25 – Máscaras de Entrada
**HU Relacionada:** HU 10  
**Descripción:** Impedir caracteres inválidos como <, >, {, }.


## RF 26 – Validación de Fechas
**HU Relacionada:** HU 10  
**Descripción:** Validar coherencia lógica de fechas ingresadas.


## RF 27 – Anonimato en Quejas
**HU Relacionada:** HU 11  
**Descripción:** Ocultar nombre del solicitante en solicitudes tipo Queja Anónima.


## RF 28 – Comentario Obligatorio en Rechazo
**HU Relacionada:** HU 12  
**Descripción:** Exigir comentario mínimo de 50 caracteres al rechazar.


## RF 29 – Adjuntar Guía en Rechazo
**HU Relacionada:** HU 12  
**Descripción:** Permitir adjuntar documento guía al rechazar.


## RF 30 – Botón de Apelación
**HU Relacionada:** HU 12  
**Descripción:** Habilitar apelación textual tras un rechazo.


## RF 31 – Filtro por Área
**HU Relacionada:** HU 13  
**Descripción:** Filtrar solicitudes por departamentos.


## RF 32 – Filtros Favoritos
**HU Relacionada:** HU 13  
**Descripción:** Guardar combinaciones de filtros como favoritos.


## RF 33 – Exportación de Datos
**HU Relacionada:** HU 13  
**Descripción:** Exportar datos filtrados a CSV o XLSX.


## RF 34 – Registro de Primera Lectura
**HU Relacionada:** HU 14  
**Descripción:** Registrar fecha y hora exacta en que Gerencia abre una solicitud.


## RF 35 – Cambio de Ícono a “Visto”
**HU Relacionada:** HU 14  
**Descripción:** Cambiar ícono de Nuevo a Visto al abrir la solicitud.


## RF 36 – Notificación de Visualización
**HU Relacionada:** HU 14  
**Descripción:** Notificar al solicitante cuando Gerencia visualice su solicitud.


## RF 37 – Escalamiento por Inactividad
**HU Relacionada:** HU 14  
**Descripción:** Marcar como Gestión en Retraso si no se abre en 24 horas hábiles.


## RF 38 – Confirmación del Solicitante para Cierre
**HU Relacionada:** HU 15  
**Descripción:** Requerir confirmación explícita del solicitante para cerrar.


## RF 39 – Calificación del Servicio
**HU Relacionada:** HU 15  
**Descripción:** Permitir calificar atención con 1 a 5 estrellas.


## RF 40 – Observaciones Finales
**HU Relacionada:** HU 15  
**Descripción:** Habilitar campo de observaciones cuando indique que no fue resuelto.


## RF 41 – Alerta por Solicitudes Urgentes Estancadas
**HU Relacionada:** HU 16  
**Descripción:** Notificar al Gerente cuando una solicitud urgente lleve más de 3 días sin atención.


## RF 42 – Semáforo de Vencimiento
**HU Relacionada:** HU 16  
**Descripción:** Mostrar semáforo de solicitudes estancadas en tablero de Gerencia.


## RF 43 – Reporte Semanal de Cuellos de Botella
**HU Relacionada:** HU 16  
**Descripción:** Enviar reporte semanal cada lunes a las 8 a.m.


## RF 44 – Enlace de Restablecimiento de Contraseña
**HU Relacionada:** HU 22  
**Descripción:** Enviar enlace con vigencia de 15 minutos.


## RF 45 – Validación de Credenciales
**HU Relacionada:** HU 17  
**Descripción:** Validar usuario y contraseña corporativa.


## RF 46 – Bloqueo por Intentos Fallidos
**HU Relacionada:** HU 17  
**Descripción:** Bloquear cuenta por 15 minutos tras 3 intentos fallidos.


## RF 47 – Expiración Automática de Sesión
**HU Relacionada:** HU 17  
**Descripción:** Cerrar sesión tras 20 minutos sin actividad.


## RF 48 – Redirección por Rol
**HU Relacionada:** HU 17  
**Descripción:** Redirigir al usuario según su rol al iniciar sesión.


## RF 49 – Restricción de Accesos
**HU Relacionada:** HU 17  
**Descripción:** Restringir acceso a menús y botones según permisos.


## RF 50 – Búsqueda Avanzada
**HU Relacionada:** HU 18  
**Descripción:** Barra de búsqueda por palabra clave, radicado, fecha o estado.


## RF 51 – Dashboard de Indicadores
**HU Relacionada:** HU 19  
**Descripción:** Panel gráfico con métricas en tiempo real.


## RF 52 – Consulta del Log de Auditoría
**HU Relacionada:** HU 20  
**Descripción:** Solo el Administrador puede ver el log técnico.


## RF 53 – Cierre Automático por Silencio Administrativo
**HU Relacionada:** HU 21  
**Descripción:** Cerrar automáticamente y calificar con 3 estrellas tras 5 días sin confirmación.
