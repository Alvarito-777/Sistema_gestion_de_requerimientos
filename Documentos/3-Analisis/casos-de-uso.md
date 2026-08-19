# CU-01 — Registrar Solicitud Formal
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-01 |
| **Nombre** | Registrar Solicitud Formal |
| **HU Relacionada** | HU-01 |
| **Actor(es)** | ACT-01 (Desarrollador de Software), ACT-05 (Sistema de Notificaciones Electrónicas) |
| **Descripción** | Permitir al empleado crear y enviar una petición formal llenando los campos necesarios y adjuntando soportes si es requerido. |
| **Precondiciones** | El usuario debe haber iniciado sesión correctamente. |
| **Postcondiciones** | Éxito: La solicitud queda en estado “Pendiente” y se envía correo con radicado.<br>Fallo: El sistema no guarda datos y mantiene el formulario editable mostrando el error. |

---

# CU-02 — Gestionar Solicitud en Borrador
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-02 |
| **Nombre** | Gestionar Solicitud en Borrador |
| **HU Relacionada** | HU-02 |
| **Actor(es)** | ACT-01 (Desarrollador de Software) |
| **Descripción** | Permitir reabrir un formulario guardado localmente para completar datos, cambiar archivos o cancelar el proceso antes del envío definitivo. |
| **Precondiciones** | Debe existir al menos una solicitud guardada como borrador. |
| **Postcondiciones** | Éxito: Se convierte en radicado oficial o se mantiene intacto si se cancela.<br>Fallo: El borrador se daña o se borra sin aprobación del usuario. |

---

# CU-03 — Consultar Historial de Solicitudes
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-03 |
| **Nombre** | Consultar Historial de Solicitudes |
| **HU Relacionada** | HU-03 |
| **Actor(es)** | ACT-01, ACT-06 |
| **Descripción** | Mostrar el listado de solicitudes enviadas y bloquear modificaciones si ya tienen respuesta. |
| **Precondiciones** | El usuario debe estar autenticado. |
| **Postcondiciones** | Éxito: Visualización segura sin alterar datos históricos.<br>Fallo: Se muestran solicitudes ajenas o se permite editar casos cerrados. |

---

# CU-04 — Buscar Solicitudes Avanzada
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-04 |
| **Nombre** | Buscar Solicitudes Avanzada |
| **HU Relacionada** | HU-18 |
| **Actor(es)** | ACT-01, ACT-02 |
| **Descripción** | Filtrar solicitudes en tiempo real por palabra clave, radicado, estado o fechas. |
| **Precondiciones** | Estar en una pantalla con listado de solicitudes. |
| **Postcondiciones** | Éxito: Se reduce el listado visible.<br>Fallo: El motor se congela o rompe filtros de seguridad. |

---

# CU-05 — Evaluar y Responder Solicitud
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-05 |
| **Nombre** | Evaluar y Responder Solicitud |
| **HU Relacionada** | HU-04, HU-05, HU-06, HU-07 |
| **Actor(es)** | ACT-02, ACT-03, ACT-05, ACT-06 |
| **Descripción** | Permitir aprobar o rechazar una solicitud, exigiendo motivo obligatorio si es negativa. |
| **Precondiciones** | El revisor debe tener permisos de aprobación. |
| **Postcondiciones** | Éxito: El caso cambia de estado con firma y notificación.<br>Fallo: Se cierra sin comentarios obligatorios. |

---

# CU-06 — Priorizar Bandeja de Entrada
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-06 |
| **Nombre** | Priorizar Bandeja de Entrada |
| **HU Relacionada** | HU-12 |
| **Actor(es)** | ACT-02 |
| **Descripción** | Organizar automáticamente la bandeja priorizando casos urgentes y antiguos. |
| **Precondiciones** | El jefe debe ingresar a su pantalla principal. |
| **Postcondiciones** | Éxito: Bandeja organizada por urgencia y orden de llegada.<br>Fallo: Solicitudes desorganizadas. |

---

# CU-07 — Configurar Delegación Temporal
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-07 |
| **Nombre** | Configurar Delegación Temporal |
| **HU Relacionada** | HU-09 |
| **Actor(es)** | ACT-02 (Gerente General) |
| **Descripción** | Delegar permisos de aprobación a un coordinador con fechas de inicio y fin. |
| **Precondiciones** | Usuario autenticado con rol de Gerente General. |
| **Postcondiciones** | Éxito: Accesos del coordinador activados por el plazo configurado.<br>Fallo: Delegación queda abierta indefinidamente. |

---

# CU-08 — Confirmar Cierre y Calificar Servicio
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-08 |
| **Nombre** | Confirmar Cierre y Calificar Servicio |
| **HU Relacionada** | HU-21 |
| **Actor(es)** | ACT-01, ACT-06 |
| **Descripción** | Recibir conformidad del empleado o aplicar cierre automático tras 5 días. |
| **Precondiciones** | La solicitud debe estar en estado “Solucionado”. |
| **Postcondiciones** | Éxito: Caso cerrado con calificación.<br>Fallo: Caso queda abierto afectando reportes. |

---

# CU-09 — Autenticar Usuario y Controlar Sesión
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-09 |
| **Nombre** | Autenticar Usuario y Controlar Sesión |
| **HU Relacionada** | HU-17 |
| **Actor(es)** | ACT-04 |
| **Descripción** | Validar acceso, bloquear intentos fallidos y cerrar sesión por inactividad. |
| **Precondiciones** | El usuario debe cargar la URL de la plataforma. |
| **Postcondiciones** | Éxito: Acceso seguro con expiración automática.<br>Fallo: Intentos infinitos permiten vulnerabilidades. |

---

# CU-10 — Consultar Log de Auditoría
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-10 |
| **Nombre** | Consultar Log de Auditoría |
| **HU Relacionada** | HU-20 |
| **Actor(es)** | ACT-04, ACT-06 |
| **Descripción** | Dar acceso exclusivo al Administrador para revisar la bitácora técnica. |
| **Precondiciones** | Usuario con rol exclusivo de Administrador. |
| **Postcondiciones** | Éxito: Inspección completa del historial técnico.<br>Fallo: Exposición de datos sensibles. |

---

# CU-11 — Recuperar Contraseña de Usuario
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-11 |
| **Nombre** | Recuperar Contraseña de Usuario |
| **HU Relacionada** | HU-22 |
| **Actor(es)** | ACT-01, ACT-02, ACT-05 |
| **Descripción** | Restablecer la clave mediante enlace temporal enviado al correo corporativo. |
| **Precondiciones** | Estar en la pantalla de Login y no recordar la clave. |
| **Postcondiciones** | Éxito: Usuario recibe enlace seguro.<br>Fallo: Envío inseguro o a correos externos. |

---

# CU-12 — Generar y Descargar Reporte PDF
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-12 |
| **Nombre** | Generar y Descargar Reporte PDF |
| **HU Relacionada** | HU-15 |
| **Actor(es)** | ACT-01, ACT-02, ACT-06 |
| **Descripción** | Descargar un PDF con código QR como evidencia física e inalterable. |
| **Precondiciones** | Solicitud en estado final aprobado. |
| **Postcondiciones** | Éxito: PDF validable con QR.<br>Fallo: PDF incompleto o sin QR. |

---

# CU-13 — Visualizar Métricas en Dashboard Directivo
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-13 |
| **Nombre** | Visualizar Métricas en Dashboard Directivo |
| **HU Relacionada** | HU-19 |
| **Actor(es)** | ACT-02 |
| **Descripción** | Mostrar panel de gráficas con métricas en tiempo real. |
| **Precondiciones** | Autenticación con rol directivo. |
| **Postcondiciones** | Éxito: Información clara para decisiones.<br>Fallo: Datos mezclados o expuestos a roles no autorizados. |

---

# CU-14 — Revelar Identidad en Quejas Anónimas
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-14 |
| **Nombre** | Revelar Identidad en Quejas Anónimas |
| **HU Relacionada** | HU-10 |
| **Actor(es)** | ACT-02 (Gerente General), ACT-06 |
| **Descripción** | Permitir levantar el anonimato bajo causa mayor con registro obligatorio. |
| **Precondiciones** | Solicitud clasificada como “Queja Anónima”. |
| **Postcondiciones** | Éxito: Identidad revelada con traza imborrable.<br>Fallo: Acceso indebido sin justificación. |

---

# CU-15 — Exportar Bitácora de Auditoría
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-15 |
| **Nombre** | Exportar Bitácora de Auditoría |
| **HU Relacionada** | HU-20 |
| **Actor(es)** | ACT-04 |
| **Descripción** | Descargar registros técnicos del sistema para auditorías externas. |
| **Precondiciones** | Estar en pantalla del Log con rol de Administrador. |
| **Postcondiciones** | Éxito: Copia física legal del rastro técnico.<br>Fallo: Alteración o edición del log antes de exportar. |

---

# CU-16 — Gestionar Cuentas de Usuario
| **Campo** | **Descripción** |
|-----------|------------------|
| **ID** | CU-16 |
| **Nombre** | Gestionar Cuentas de Usuario |
| **HU Relacionada** | HU-23, HU-24, HU-25 |
| **Actor(es)** | ACT-04 (Gestor Documental / Soporte) |
| **Descripción** | Permitir al ACT-04 gestionar las cuentas de usuario mediante las operaciones de creación, edición e inactivación (relaciones «extend»), incluyendo la validación de datos y el registro en el log de auditoría (relaciones «include»). |
| **Precondiciones** | La cuenta de usuario debe existir en el sistema y los datos deben estar previamente validados antes de ser creados, editados o inactivados. |
| **Postcondiciones** | La cuenta de usuario es creada, editada o inactivada correctamente, quedando los cambios registrados en el Log de Auditoría y los datos validados. |

