## Matriz de Trazabilidad HU → RF → Entidad → Clase.método → CU → Mensaje (secuencia) → Pantalla → RN

| HU | RF | Entidad | Clase.método | CU | Mensaje (secuencia) | Pantalla (MK) | RN |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **HU-01** Crear nuevo rol | RF-01 | rol | Rol.crear() | CU-01 | RolService.crear() | MK-02 Guardar Rol | RN-03 |
| **HU-02** Consultar roles | RF-02 | rol | Rol.consultar(id_rol) | CU-02 | RolService.consultar(id_rol) | MK-01 Buscar | — |
| **HU-03** Actualizar rol | RF-03 | rol | Rol.actualizar(id_rol) | CU-03 | RolService.actualizar(id_rol) | MK-02 Guardar Rol | RN-03 |
| **HU-04** Inactivar rol | RF-04 | rol | Rol.inactivar(id_rol) | CU-04 | RolService.inactivar(id_rol) | MK-03 Confirmar Inactivación | RN-10 |
| **HU-05** Registrar usuario | RF-05 | usuario | Usuario.crear() | CU-05 | UsuarioService.crear() | MK-05 Guardar Usuario | RN-01 |
| **HU-06** Consultar usuario | RF-06 | usuario | Usuario.consultar(id_usuario) | CU-06 | UsuarioService.consultar(id_usuario) | MK-04 Buscar | — |
| **HU-07** Actualizar usuario | RF-07 | usuario | Usuario.actualizar(id_usuario) | CU-07 | UsuarioService.actualizar(id_usuario) | MK-05 Guardar Usuario | RN-01<br>RN-02 |
| **HU-08** Inactivar cuenta de usuario | RF-08 | usuario | Usuario.inactivar(id_usuario) | CU-08 | UsuarioService.inactivar(id_usuario) | MK-06 Confirmar Inactivación | RN-10 |
| **HU-09** Registrar intento fallido | RF-09 | usuario | Usuario.registrarIntentoFallido() | CU-09 | UsuarioService.registrarIntentoFallido() | Interno (refleja MK-04) | RN-02 |
| **HU-10** Reiniciar intentos fallidos | RF-10 | usuario | Usuario.reiniciarIntentos() | CU-10 | UsuarioService.reiniciarIntentos() | Interno / MK-05 desbloqueo | RN-02 |
| **HU-11** Asignar rol a usuario | RF-11 | usuario_rol | usuario_rol.crear() | CU-11 | UsuarioRolService.crear() | MK-08 Guardar Asignación | RN-17 |
| **HU-12** Consultar asignación de rol | RF-12 | usuario_rol | usuario_rol.consultar(id_usuario, id_rol) | CU-12 | UsuarioRolService.consultar(id_usuario, id_rol) | MK-07 Buscar | — |
| **HU-13** Revocar rol asignado | RF-13 | usuario_rol | usuario_rol.revocar(id_usuario, id_rol) | CU-13 | UsuarioRolService.revocar(id_usuario, id_rol) | MK-09 Confirmar Revocación | RN-18 |
| **HU-44** Actualizar asignación de rol | RF-44 | usuario_rol | usuario_rol.actualizar(id_usuario, id_rol) | CU-44 | UsuarioRolService.actualizar(id_usuario, id_rol) | MK-29 Guardar Cambio | RN-17 |
| **HU-14** Crear tipo de solicitud | RF-14 | tipo_solicitud | tipo_solicitud.crear() | CU-14 | TipoSolicitudService.crear() | MK-11 Guardar Tipo | RN-21 |
| **HU-15** Consultar tipo de solicitud | RF-15 | tipo_solicitud | tipo_solicitud.consultar(id_tipo_solicitud) | CU-15 | TipoSolicitudService.consultar(id_tipo_solicitud) | MK-10 tabla | — |
| **HU-16** Actualizar tipo de solicitud | RF-16 | tipo_solicitud | tipo_solicitud.actualizar(id_tipo_solicitud) | CU-16 | TipoSolicitudService.actualizar(id_tipo_solicitud) | MK-11 Guardar Tipo | RN-21 |
| **HU-17** Inactivar tipo de solicitud | RF-17 | tipo_solicitud | tipo_solicitud.inactivar(id_tipo_solicitud) | CU-17 | TipoSolicitudService.inactivar(id_tipo_solicitud) | MK-12 Confirmar Inactivación | RN-16 |
| **HU-18** Crear estado de solicitud | RF-18 | estado_solicitud | estado_solicitud.crear() | CU-18 | EstadoSolicitudService.crear() | MK-14 Guardar Estado | RN-22 |
| **HU-19** Consultar estado de solicitud | RF-19 | estado_solicitud | estado_solicitud.consultar(id_estado_solicitud) | CU-19 | EstadoSolicitudService.consultar(id_estado_solicitud) | MK-13 tabla | — |
| **HU-20** Actualizar estado de solicitud | RF-20 | estado_solicitud | estado_solicitud.actualizar(id_estado_solicitud) | CU-20 | EstadoSolicitudService.actualizar(id_estado_solicitud) | MK-14 Guardar Estado | RN-23 |
| **HU-21** Crear borrador de solicitud | RF-21 | solicitud | Solicitud.crear() | CU-21 | SolicitudService.crear() | MK-16 Guardar Borrador | RN-16 |
| **HU-22** Consultar expediente de solicitud | RF-22 | solicitud | Solicitud.consultar(id_solicitud) | CU-22 | SolicitudService.consultar(id_solicitud) | MK-15 Buscar | RN-04 |
| **HU-23** Actualizar contenido de solicitud | RF-23 | solicitud | Solicitud.actualizar(id_solicitud) | CU-23 | SolicitudService.actualizar(id_solicitud) | MK-16 Actualizar Solicitud | RN-19 |
| **HU-24** Radicar solicitud formalmente | RF-24 | solicitud | Solicitud.radicar() | CU-24 | SolicitudService.radicar(id_solicitud)<br>DS-01 m.3 | MK-16 Radicar Formalmente | RN-14<br>RN-15<br>RN-16 |
| **HU-25** Cambiar estado de la solicitud | RF-25 | solicitud | Solicitud.cambiarEstado(nuevoEstado) | CU-25 | Solicitud.cambiarEstado(nuevoEstado)<br>DS-01 m.19 · DS-02A m.22 · DS-03 m.28 · DS-04 m.23 | Interno (refleja MK-15) | RN-15 |
| **HU-26** Desblindar identidad anónima | RF-26 | solicitud | Solicitud.desblindarIdentidad(id_usuario) | CU-26 | SolicitudService.desblindarIdentidad(id_usuario) | MK-17 Confirmar Desblindaje | RN-04 |
| **HU-27** Inactivar solicitud | RF-27 | solicitud | Solicitud.inactivar(id_solicitud) | CU-43 | SolicitudService.inactivar(id_solicitud) | MK-28 Confirmar Inactivación | RN-20 |
| **HU-28** Aprobar solicitud | RF-28 | aprobacion_solicitud | aprobacion_solicitud.aprobar() | CU-27 | AprobacionService.aprobar(id_solicitud, comentario)<br>DS-02A m.12 | MK-19 Aprobar Solicitud | RN-05<br>RN-15 |
| **HU-29** Rechazar solicitud | RF-29 | aprobacion_solicitud | aprobacion_solicitud.rechazar(comentario) | CU-28<br>*(alt. 2a de CU-27)* | AprobacionService.rechazar(id_solicitud, comentario)<br>DS-02B m.3 | MK-19 Rechazar Solicitud | RN-05<br>RN-06<br>RN-15 |
| **HU-30** Devolver solicitud para ajustes | RF-30 | aprobacion_solicitud | aprobacion_solicitud.devolverParaAjustes(comentario) | CU-29<br>*(alt. 2b de CU-27)* | AprobacionService.devolverParaAjustes(id_solicitud, comentario)<br>DS-02B m.8 | MK-19 Devolver para Ajustes | RN-05<br>RN-06<br>RN-15 |
| **HU-31** Consultar dictamen de aprobación | RF-31 | aprobacion_solicitud | aprobacion_solicitud.consultar(id_aprobacion) | CU-30 | AprobacionService.consultar(id_aprobacion) | MK-18 Buscar | — |
| **HU-32** Asignar gestor a la solicitud | RF-32 | gestion_solicitud | gestion_solicitud.asignarGestor(id_gestor) | CU-33 | GestionService.asignarGestor(id_solicitud, id_gestor, prioridad)<br>DS-03 m.14 | MK-21 Guardar Asignación | RN-11<br>RN-15<br>RN-27 |
| **HU-33** Reasignar gestor | RF-33 | gestion_solicitud | gestion_solicitud.reasignar(id_gestor) | CU-34 | GestionService.reasignar(id_gestor) | MK-21 Guardar Asignación (desde Reasignar) | RN-11<br>RN-27 |
| **HU-34** Actualizar prioridad de gestión | RF-34 | gestion_solicitud | gestion_solicitud.actualizarPrioridad(nuevaPrioridad) | CU-35 | GestionService.actualizarPrioridad(nuevaPrioridad) | MK-21 selector de prioridad | RN-24 |
| **HU-35** Finalizar gestión de la solicitud | RF-35 | gestion_solicitud | gestion_solicitud.finalizar() | CU-36 | GestionService.finalizar(id_gestion)<br>DS-04 m.12 | MK-22 Confirmar Finalización | RN-12<br>RN-15 |
| **HU-36** Consultar registro de gestión | RF-36 | gestion_solicitud | gestion_solicitud.consultar(id_gestion) | CU-37 | GestionService.consultar(id_gestion)<br>DS-04 m.3 | MK-20 Buscar | — |
| **HU-37** Calificar servicio recibido | RF-37 | evaluacion | Evaluacion.calificar(puntaje, comentario) | CU-38 | EvaluacionService.calificar(puntaje, comentario) | MK-24 Enviar Calificación | RN-07<br>RN-13 |
| **HU-38** Consultar evaluación de servicio | RF-38 | evaluacion | Evaluacion.consultar(id_evaluacion) | CU-39 | EvaluacionService.consultar(id_evaluacion) | MK-23 tabla | — |
| **HU-39** Crear interacción en solicitud | RF-39 | detalle_solicitud | detalle_solicitud.crear() | CU-31 | DetalleSolicitudService.crear() | MK-26 Publicar Interacción | RN-08 |
| **HU-40** Consultar detalles de una solicitud | RF-40 | detalle_solicitud | detalle_solicitud.consultarPorSolicitud(id_solicitud) | CU-32 | DetalleSolicitudService.consultarPorSolicitud(id_solicitud) | MK-25 tabla | — |
| **HU-41** Registrar acción de auditoría | RF-41 | bitacora_auditoria | Bitacora_Auditoria.registrarAccion(accionAuditoria) | CU-40 | Solicitud → BitacoraAuditoria.registrarAccion(Cambio_Estado)<br>DS-01 m.21 · DS-02A m.24 · DS-03 m.30 · DS-04 m.25 | Interno (refleja MK-27) | RN-09<br>RN-15 |
| **HU-42** Consultar auditoría por entidad | RF-42 | bitacora_auditoria | Bitacora_Auditoria.consultarPorEntidad(entidad, id_registro) | CU-41 | BitacoraService.consultarPorEntidad(entidad, id_registro) | MK-27 Buscar | RN-25 |
| **HU-43** Consultar auditoría por fechas | RF-43 | bitacora_auditoria | Bitacora_Auditoria.consultarPorRango(desde, hasta) | CU-42 | BitacoraService.consultarPorRango(desde, hasta) | MK-27 filtros desde / hasta | RN-26 |
| **HU-45** Exportar informe de auditoría | RF-45 | bitacora_auditoria | Bitacora_Auditoria.exportarInforme(formato) | CU-45 | BitacoraService.exportarInforme(formato) | MK-27 Exportar Informe | RN-09<br>RN-25 |

> **Nota.** La columna *Clase.método* usa los nombres del diagrama de clases (3.3) y del script (4.1). En la columna *Mensaje (secuencia)* se conservan los nombres de las líneas de vida de los diagramas de secuencia (convención Java; observación OA-06).
