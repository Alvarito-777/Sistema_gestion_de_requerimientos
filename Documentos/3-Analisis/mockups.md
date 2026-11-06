
## Mockup MK-01 — Listado y búsqueda (R)

<img width="930" height="520" alt="image" src="https://github.com/user-attachments/assets/c7511507-225c-46f9-964f-f28a04a5ac97" />


### Ficha del mockup MK-01
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-01 |
| **Pantalla** | Roles — Listado y búsqueda |
| **Atiende (HU / RF / CU)** | HU-02 / RF-02 / CU-02 (y da entrada a HU-01 / CU-01, HU-03 / CU-03 y HU-04 / CU-04) |
| **Campos ↔ Diccionario** | **Filtro:** nombre_rol (lista desplegable con dominio autorizado RN-03: Solicitante, Aprobador, Gestion_Personal, Gerente, Administrador; el rol Auditor, también definido en RN-03, no aparece en la captura).<br>**Columnas de la tabla:** id_rol, nombre_rol, descripcion, permiso_administrar, fecha_creacion. |
| **Botones ↔ Eventos** | **Buscar** → consultar() (HU-02 / CU-02, RF-02).<br>**+ Nuevo Rol** → abre MK-02 en modo registrar (HU-01 / CU-01 → crear(), RF-01).<br>**Editar** → abre MK-02 con datos cargados (HU-03 / CU-03 → actualizar(), RF-03).<br>**Inactivar** → abre aviso MK-03 (HU-04 / CU-04 → inactivar(), RF-04; borrado lógico con ON DELETE RESTRICT según RN-10). |
| **RN visibles** | Ninguna directamente en la tabla; la restricción de dominio de roles (RN-03) opera en el filtro, y el mensaje "No se encontró ningún rol asociado..." corresponde al CA-3 de la HU-02. |

---

## Mockup MK-02 — Registrar / Actualizar rol (C y U)

<img width="930" height="505" alt="image" src="https://github.com/user-attachments/assets/d469c53f-b3ff-40e5-a49a-92720b977a96" />

### Ficha del mockup MK-02
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-02 |
| **Pantalla** | Roles — Formulario de Registro / Actualización |
| **Atiende (HU / RF / CU)** | HU-01 / RF-01 / CU-01 (Crear) y HU-03 / RF-03 / CU-03 (Actualizar) |
| **Campos ↔ Diccionario** | **id_rol** (Campo autoincremental de solo lectura, visible solo en modo actualización).<br>**nombre_rol** (Campo de entrada / Selector basado en la RN-03: Solicitante, Aprobador, Gestion_Personal, Gerente, Administrador; el rol Auditor, también definido en RN-03, no aparece en la captura).<br>**descripcion** (Área de texto para detallar el alcance, máx. 255 caracteres).<br>**permiso_administrar** (Casilla de verificación / Checkbox booleano para privilegios técnicos). |
| **Botones ↔ Eventos** | **Guardar Rol** → Ejecuta crear() (HU-01 / RF-01) si es un registro nuevo o actualizar(id_rol) (HU-03 / RF-03) si es edición, validando previamente restricciones de campos obligatorios y unicidad (uq_rol_nombre).<br>**Cancelar / Volver** → Aborta la operación y retorna al listado MK-01 sin guardar cambios (HU-02 / RF-02). |
| **RN visibles / Camino Triste** | **RN-03 / uq_rol_nombre:** Si el usuario intenta registrar un nombre de rol duplicado o fuera del dominio autorizado, el sistema despliega el mensaje de rechazo: "El nombre del rol ya se encuentra registrado o no pertenece al dominio autorizado." (CA-2 y CA-3 de HU-01; CA-2 de HU-03).<br>**Restricción NO NULO:** Si se intenta guardar dejando campos obligatorios vacíos, se resaltan los campos con el aviso correspondiente (CA-4 de HU-01 en modo registro; CA-3 de HU-03 en modo edición). |

---

## Mockup MK-03 — Aviso de inactivación (D lógico)

<img width="930" height="441" alt="image" src="https://github.com/user-attachments/assets/78948019-e863-434b-b7ee-8487aa754ab3" />

### Ficha del mockup MK-03
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-03 |
| **Pantalla** | Roles — Modal de Confirmación de Inactivación |
| **Atiende (HU / RF / CU)** | HU-04 / RF-04 / CU-04 (Inactivar rol) |
| **Campos / Elementos** | Ventana modal emergente de advertencia que muestra el nombre del rol seleccionado (ej. Gerente), el icono de alerta y el texto explicativo de la consecuencia. |
| **Botones ↔ Eventos** | **Confirmar Inactivación** → Ejecuta inactivar(id_rol) (HU-04 / RF-04), aplicando el borrado lógico en el sistema respetando la regla de integridad referencial RN-10 (ON DELETE RESTRICT) (CA-2 de HU-04).<br>**Cancelar** → Cierra el modal y retorna a MK-01 sin alterar el estado del rol. |
| **Texto Exacto del Aviso y Consecuencia (RN-10)** | > ¿Está seguro de que desea inactivar el rol "Gerente"? (CA-1 de HU-04)<br>> El rol dejará de estar disponible para nuevas asignaciones en la plataforma, pero mantendrá su historial en la base de datos (RN-10).<br>*(Camino triste / Rechazo por RN-10, CA-3 de HU-04):* Si el rol tiene usuarios activos asociados, el sistema bloquea la acción y muestra la advertencia: "No es posible inactivar el rol porque existen usuarios activos vinculados a este perfil." |

---

## Cobertura CRUD de la Entidad Rol

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **crear()** | HU-01 / RF-01 | C | MK-02 en modo registrar: botón Guardar Rol |
| **existeRol(nombre)** | HU-01, HU-03 / RF-01, RF-03 / RN-03 | (apoyo) | INTERNO: se dispara dentro de Guardar en ambos modos; no necesita botón y así se declara |
| **consultar(id_rol)** | HU-02 / RF-02 | R | MK-01: filtro por ID y botón Buscar / tabla de listado |
| **actualizar(id_rol)** | HU-03 / RF-03 | U | MK-02 en modo actualizar (entrada por Editar en MK-01): botón Guardar Rol |
| **inactivar(id_rol)** | HU-04 / RF-04 | D lógico | MK-03: botón "Confirmar Inactivación" (entrada por Inactivar en MK-01) |


## Mockup MK-04 — Listado y búsqueda (R)

<img width="595" height="301" alt="image" src="https://github.com/user-attachments/assets/93d702a4-8ce1-4eb1-8491-824239987d26" />

### Ficha del mockup MK-04
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-04 |
| **Pantalla** | Usuarios — Listado y búsqueda |
| **Atiende (HU / RF / CU)** | HU-06 / RF-06 / CU-06 (y da entrada a HU-05 / CU-05, HU-07 / CU-07 y HU-08 / CU-08) |
| **Campos ↔ Diccionario** | **Filtro:** búsqueda por identificador del usuario (id_usuario).<br>**Columnas de la tabla:** id_usuario, nombre_completo, correo_corporativo, estado_cuenta, intentos_fallidos, fecha_creacion. |
| **Botones ↔ Eventos** | **Buscar** → consultar(id_usuario) (HU-06 / CU-06, RF-06).<br>**+ Nuevo Usuario** → abre MK-05 en modo registrar (HU-05 / CU-05 → crear(), RF-05).<br>**Editar** → abre MK-05 con datos cargados (HU-07 / CU-07 → actualizar(), RF-07).<br>**Inactivar** → abre aviso MK-06 (HU-08 / CU-08 → inactivar(), RF-08; preservación lógica de datos con ON DELETE RESTRICT según RN-10). |
| **RN visibles** | Ninguna directamente en la tabla principal; la validación de dominio corporativo (RN-01) opera al registrar/actualizar, y el mensaje "El usuario con identificador no existe en el sistema" corresponde al CA-2 de la HU-06.<br>Las columnas estado_cuenta e intentos_fallidos reflejan el resultado de los procesos internos HU-09 / CU-09 (registrarIntentoFallido(), RF-09) y HU-10 / CU-10 (reiniciarIntentos(), RF-10), regidos por RN-02; no tienen botón de interfaz. |

---

## Mockup MK-05 — Registrar / Actualizar usuario (C y U)

<img width="513" height="403" alt="image" src="https://github.com/user-attachments/assets/892388ae-4f1b-4a23-a8c3-8b47c2ae542b" />


### Ficha del mockup MK-05
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-05 |
| **Pantalla** | Usuarios — Formulario de Registro / Actualización |
| **Atiende (HU / RF / CU)** | HU-05 / RF-05 / CU-05 (Crear) y HU-07 / RF-07 / CU-07 (Actualizar)<br>Complemento: el selector estado_cuenta permite el desbloqueo manual de HU-10 / RF-10 / CU-10 (CA-2). |
| **Campos ↔ Diccionario** | **id_usuario** (Identificador autoincremental de solo lectura, visible únicamente en modo edición).<br>**nombre_completo** (Campo de texto obligatorio para los nombres y apellidos del titular).<br>**correo_corporativo** (Campo de entrada para el correo institucional; valida la regla RN-01 de dominio corporativo y la unicidad uq_usuario_correo).<br>**contrasena_hash** (Campo de contraseña enmascarado; se almacena de forma encriptada mediante bcrypt o Argon2).<br>**estado_cuenta** (Selector ENUM: 'activo', 'inactivo', 'suspendido').<br>**intentos_fallidos** (Contador numérico de control de acceso). |
| **Botones ↔ Eventos** | **Guardar Usuario** → Ejecuta crear() (HU-05 / RF-05) en modo registro (inicializando con estado activo e intentos fallidos en 0) o actualizar(id_usuario) (HU-07 / RF-07) en modo edición.<br>Al cambiar estado_cuenta de 'suspendido' a 'activo', el guardado ejecuta reiniciarIntentos() (HU-10 / RF-10, CA-2): intentos_fallidos = 0 y fecha_bloqueo = NULL.<br>**Cancelar** → Aborta la operación y retorna al listado MK-04 sin persistir cambios. |
| **RN visibles** | **RN-01 (Dominio corporativo):** Si se ingresa un correo externo (ej. @gmail.com), el sistema rechaza el registro con el mensaje: "El correo debe pertenecer al dominio corporativo autorizado (@nexaservicios.com)." (CA-2 de HU-05).<br>**Unicidad uq_usuario_correo:** si el correo ya existe, el sistema rechaza el guardado (CA-3 de HU-05 y CA-3 de HU-07).<br>**RN-02 (Bloqueo y Estado):** Permite cambiar el estado de la cuenta a suspendido asociando automáticamente la fecha_bloqueo (CA-2 de HU-07).<br>**Restricción NO NULO:** Si se omiten campos obligatorios, se resalta la celda con su respectiva advertencia (CA-4 de HU-05). |

---

## Mockup MK-06 — Aviso de inactivación (D lógico)

<img width="595" height="316" alt="image" src="https://github.com/user-attachments/assets/ccdd4648-13bc-4395-840d-4558f2883a9e" />

### Ficha del mockup MK-06
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-06 |
| **Pantalla** | Usuarios — Modal de Confirmación de Inactivación |
| **Atiende (HU / RF / CU)** | HU-08 / RF-08 / CU-08 (Inactivar cuenta de usuario) |
| **Campos / Elementos** | Ventana modal emergente con icono de advertencia, título de confirmación y el detalle de la cuenta a inhabilitar. |
| **Botones ↔ Eventos** | **Confirmar Inactivación** → Ejecuta inactivar(id_usuario) (HU-08 / RF-08), modificando el atributo estado_cuenta a 'inactivo' y bloqueando el inicio de sesión bajo la política de borrado lógico (RN-10) (CA-2 de HU-08).<br>**Cancelar** → Cierra el modal y retorna al listado MK-04 manteniendo la cuenta intacta. |
| **RN visibles / Texto del Aviso** | > ¿Desea confirmar la inactivación? (CA-1 de HU-08)<br>> "La cuenta de diego.rojas@nexaservicios.com será inhabilitada. Se conservarán sus registros en el sistema (RN-10)."<br>Garantiza el cumplimiento estricto de la regla RN-10 (ON DELETE RESTRICT), evitando la eliminación física de la base de datos para preservar los vínculos históricos y de auditoría. |

---

## Cobertura CRUD de la Entidad Usuario

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **crear()** | HU-05 / RF-05 | C | MK-05 en modo registrar: botón Guardar Usuario |
| **existeCorreo(correo)** | HU-05, HU-07 / RF-05, RF-07 / RN-01 | (apoyo) | INTERNO: se dispara dentro de Guardar en ambos modos para validar dominio y unicidad; no necesita botón y así se declara |
| **consultar(id_usuario)** | HU-06 / RF-06 | R | MK-04: filtro por ID y botón Buscar / tabla de listado |
| **actualizar(id_usuario)** | HU-07 / RF-07 | U | MK-05 en modo actualizar (entrada por Editar en MK-04): botón Guardar Usuario |
| **inactivar(id_usuario)** | HU-08 / RF-08 | D lógico | MK-06: botón "Confirmar Inactivación" (entrada por Inactivar en MK-04) |
| **registrarIntentoFallido()** | HU-09 / RF-09 / RN-02 | (apoyo) | INTERNO: se ejecuta en la lógica de autenticación del sistema al fallar credenciales; no necesita botón de interfaz (su efecto se ve en MK-04) |
| **reiniciarIntentos()** | HU-10 / RF-10 / RN-02 | (apoyo) | INTERNO: se ejecuta al iniciar sesión exitosamente (CA-1) o al desbloquear la cuenta desde MK-05 cambiando estado_cuenta a activo (CA-2); no necesita botón propio |

## Mockup MK-07 — Listado y Consulta de Roles de Usuario (R)

<img width="930" height="351" alt="image" src="https://github.com/user-attachments/assets/6f7a3015-7983-4ced-b0d8-3c22a1e26bcc" />

### Ficha del mockup MK-07
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-07 |
| **Pantalla** | UsuarioRol — Listado y búsqueda |
| **Atiende (HU / RF / CU)** | HU-12 / RF-12 / CU-12 (y da entrada a HU-11 / CU-11, HU-13 / CU-13 y HU-44 / CU-44) |
| **Campos ↔ Diccionario** | **Filtro de búsqueda:** campos de entrada para id_usuario e id_rol.<br>**Columnas de la tabla de resultados:** id_usuario, correo_corporativo, id_rol, nombre_rol, fecha_asignacion. |
| **Botones ↔ Eventos** | **Buscar** → consultar(id_usuario, id_rol) (HU-12 / CU-12, RF-12).<br>**+ Asignar Rol** → abre el formulario MK-08 (HU-11 / CU-11 → crear(), RF-11).<br>**Revocar** → abre el aviso modal MK-09 (HU-13 / CU-13 → revocar(), RF-13).<br>**Editar Rol** → abre el formulario MK-29 con la asignación cargada (HU-44 / CU-44 → actualizar(id_usuario, id_rol), RF-44). Esta acción se representa en MK-29 (la captura original de MK-07 solo muestra la acción Revocar). |
| **RN visibles** | Ninguna directamente en la tabla principal; el mensaje "No existe la asignación del rol para el usuario..." corresponde al CA-2 de la HU-12. |

---

## Mockup MK-08 — Formulario de Asignación de Rol (C)

<img width="930" height="605" alt="image" src="https://github.com/user-attachments/assets/b0de1958-8712-4a39-bd97-123956c3c198" />

### Ficha del mockup MK-08
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-08 |
| **Pantalla** | UsuarioRol — Formulario de asignación |
| **Atiende (HU / RF / CU)** | HU-11 / RF-11 / CU-11 (Asignar rol a usuario) |
| **Campos ↔ Diccionario** | **id_usuario** (Selector o campo de búsqueda del usuario activo).<br>**id_rol** (Selector desplegable con los roles activos disponibles en el catálogo).<br>**fecha_asignacion** (Sello de tiempo automático generado al registrar el vínculo). |
| **Botones ↔ Eventos** | **Guardar Asignación** → Ejecuta crear() (HU-11 / RF-11), validando la unicidad de la tupla compuesta (id_usuario, id_rol) y que la cuenta no esté inactiva.<br>**Cancelar** → Retorna al listado MK-07 sin persistir cambios. |
| **RN visibles** | **RN-17 (unicidad de la asignación):** Si el usuario ya posee el rol, el sistema impide el registro con el mensaje: "El usuario ya cuenta con el rol asignado." (CA-2 de HU-11).<br>**RN-17 (cuenta activa):** No se permite asignar roles a cuentas con estado inactivo (CA-3 de HU-11). |

---

## Mockup MK-09 — Aviso de Revocación de Rol (D)

<img width="930" height="519" alt="image" src="https://github.com/user-attachments/assets/018ecbda-ba4c-4e05-9099-885de7905f2d" />

### Ficha del mockup MK-09
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-09 |
| **Pantalla** | UsuarioRol — Modal de confirmación de revocación (sobre el MK-07) |
| **Atiende (HU / RF / CU)** | HU-13 / RF-13 / CU-13 (Revocar rol asignado a usuario) |
| **Campos / Elementos** | Ventana modal emergente con advertencia de desvinculación, mostrando el detalle de la cuenta y el rol a retirar. |
| **Botones ↔ Eventos** | **Confirmar Revocación** → Ejecuta revocar(id_usuario, id_rol) (HU-13 / RF-13), eliminando la asociación de la tabla intermedia y validando que el usuario conserve al menos un rol activo (CA-1 y CA-2 de HU-13).<br>**Cancelar** → Cierra el modal sin modificar las relaciones. |
| **RN visibles / Texto del Aviso** | > ¿Desea retirar el rol asignado?<br>> "El rol 'Aprobador' será desvinculado del usuario marta.perez@nexaservicios.com."<br>Garantiza la RN-18: toda cuenta de usuario debe mantener al menos un rol asignado en la plataforma (CA-2 de HU-13). |

---

## Mockup MK-29 — Formulario de Actualización de Asignación de Rol (U)

<img width="930" height="537" alt="image" src="https://github.com/user-attachments/assets/91b6e376-3982-4a7f-9d14-700355235273" />

### Ficha del mockup MK-29
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-29 |
| **Pantalla** | UsuarioRol — Formulario de actualización de asignación |
| **Atiende (HU / RF / CU)** | HU-44 / RF-44 / CU-44 (Actualizar asignación de rol de usuario) |
| **Campos ↔ Diccionario** | **id_usuario** (Campo de solo lectura: identifica la cuenta cuya asignación se modifica).<br>**correo_corporativo** (Campo de solo lectura con el correo de la cuenta).<br>**Rol actual (id_rol / nombre_rol)** (Campo de solo lectura con el rol asignado antes del cambio).<br>**id_rol** (Selector desplegable con los roles activos disponibles en el catálogo; define el nuevo rol).<br>**fecha_asignacion** (Sello de tiempo automático actualizado al guardar el cambio). |
| **Botones ↔ Eventos** | **Guardar Cambio** → Ejecuta actualizar(id_usuario, id_rol) (HU-44 / RF-44), validando que el nuevo rol esté activo y que no duplique un rol que el usuario ya posee (unicidad de la clave compuesta).<br>**Cancelar** → Retorna al listado MK-07 sin persistir cambios. |
| **RN visibles / Camino Triste** | **Éxito (CA-1 de HU-44):** el sistema actualiza el registro en usuario_rol, guarda la fecha y hora actual y muestra "Asignación de rol actualizada correctamente."<br>**RN-17 (unicidad de la asignación):** si el usuario ya posee el rol seleccionado, el sistema bloquea la operación y muestra "El usuario ya cuenta con el rol asignado." (CA-2 de HU-44).<br>**RN-17 (rol activo):** no se permite asignar un rol inactivo; el sistema bloquea la operación y muestra el mensaje de error correspondiente (CA-2 de HU-44). |

---

## Cobertura CRUD de la Entidad usuario_rol

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **crear()** | HU-11 / RF-11 | C | MK-08: botón "Guardar Asignación" |
| **consultar(id_usuario, id_rol)** | HU-12 / RF-12 | R | MK-07: filtros por id_usuario e id_rol junto con el botón Buscar / tabla de listado |
| **actualizar(id_usuario, id_rol)** | HU-44 / RF-44 | U | MK-29: botón "Guardar Cambio" (entrada por Editar Rol en MK-07) |
| **revocar(id_usuario, id_rol)** | HU-13 / RF-13 | D físico / lógico | MK-09: botón "Confirmar Revocación" (entrada por el enlace Revocar en MK-07) |

## Mockup MK-10 — Listado y Búsqueda de Tipos de Solicitud (R)

<img width="930" height="403" alt="image" src="https://github.com/user-attachments/assets/4df76139-416e-4a23-b32e-e27e2f5f2429" />

### Ficha del mockup MK-10
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-10 |
| **Pantalla** | Tipos de Solicitud — Listado y Búsqueda |
| **Atiende (HU / RF / CU)** | HU-15 / RF-15 / CU-15 (y da entrada a HU-14 / CU-14, HU-16 / CU-16 y HU-17 / CU-17) |
| **Campos ↔ Diccionario** | **Filtro de búsqueda:** por identificador o código de tipo (id_tipo_solicitud / codigo_tipo).<br>**Columnas de la tabla:** id_tipo_solicitud, codigo_tipo, nombre_tipo, descripcion, activo. |
| **Botones ↔ Eventos** | **Buscar** → consultar(id_tipo_solicitud) (HU-15 / CU-15, RF-15).<br>**+ Nuevo Tipo** → abre MK-11 en modo registrar (HU-14 / CU-14 → crear(), RF-14).<br>**Editar** → abre MK-11 con datos cargados (HU-16 / CU-16 → actualizar(), RF-16).<br>**Inactivar** → abre aviso MK-12 (HU-17 / CU-17 → inactivar(), RF-17 / RN-16). |
| **RN visibles** | Regla de inactivación lógica de catálogos (RN-16) y mensaje de no encontrado correspondiente al CA-2 de la HU-15. |

---

## Mockup MK-11 — Registrar / Actualizar Tipo de Solicitud (C y U)

<img width="930" height="558" alt="image" src="https://github.com/user-attachments/assets/ad521c30-b90b-4724-9139-5e110ab544b4" />

### Ficha del mockup MK-11
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-11 |
| **Pantalla** | Tipos de Solicitud — Formulario de Registro / Actualización |
| **Atiende (HU / RF / CU)** | HU-14 / RF-14 / CU-14 (Crear) y HU-16 / RF-16 / CU-16 (Actualizar) |
| **Campos ↔ Diccionario** | **id_tipo_solicitud** (solo lectura).<br>**codigo_tipo** (sujeto a unicidad uq_tipo_codigo).<br>**nombre_tipo**.<br>**descripcion**.<br>**activo**. |
| **Botones ↔ Eventos** | **Guardar Tipo** → Ejecuta crear() (HU-14 / RF-14) o actualizar(id_tipo_solicitud) (HU-16 / RF-16) validando unicidad y campos obligatorios.<br>**Cancelar** → retorna al listado MK-10 sin cambios. |
| **RN visibles** | **RN-21 (unicidad del código, uq_tipo_codigo):** CA-2 de la HU-14 y CA-2 de la HU-16.<br>**Restricción NO NULO** para campos obligatorios (CA-3 de HU-14). |

---

## Mockup MK-12 — Aviso de Inactivación de Tipo de Solicitud (D lógico)

<img width="930" height="501" alt="image" src="https://github.com/user-attachments/assets/509d4daf-fe6a-48d2-a737-1836a1112b21" />

### Ficha del mockup MK-12
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-12 |
| **Pantalla** | Aviso de inactivación (modal sobre el MK-10) |
| **Atiende (HU / RF / CU)** | HU-17 / RF-17 / CU-17 (Inactivar tipo de solicitud) |
| **Campos ↔ Diccionario** | Muestra el nombre y código del tipo de solicitud; cambia el atributo activo a FALSE bajo la regla RN-16. |
| **Botones ↔ Eventos** | **Confirmar Inactivación** → inactivar(id_tipo_solicitud) (HU-17 / RF-17).<br>**Cancelar** → cierra el aviso sin cambios. |
| **RN visibles** | **RN-16 (CA-2 de la HU-17):** las solicitudes asociadas previamente se preservan y el tipo inactivo deja de poder seleccionarse en nuevas solicitudes (ver MK-16).<br>Aplica la regla de oro de interfaz: el aviso explica la consecuencia y la preservación del historial (CA-1 de la HU-17). |

---

## Cobertura CRUD de la Entidad tipo_solicitud

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **crear()** | HU-14 / RF-14 | C | MK-11 (Formulario de Registro/Actualización): botón "Guardar Tipo" |
| **consultar(id_tipo_solicitud)** | HU-15 / RF-15 | R | MK-10 (Listado y Búsqueda): filtros de búsqueda por ID/código y tabla general del catálogo |
| **actualizar(id_tipo_solicitud)** | HU-16 / RF-16 | U | MK-11 (Formulario en modo edición, ingresando desde el botón "Editar" del MK-10): botón "Guardar Tipo" |
| **inactivar(id_tipo_solicitud)** | HU-17 / RF-17 | D lógico (activo = FALSE) | MK-12 (Modal de Confirmación): botón "Confirmar Inactivación" (accionado desde el botón "Inactivar" del MK-10) |

## Mockup MK-13 — Listado y Búsqueda de Estados de Solicitud (R)

<img width="930" height="443" alt="image" src="https://github.com/user-attachments/assets/59934fdd-209d-482b-9d53-ff199507bbb5" />

### Ficha del mockup MK-13
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-13 |
| **Pantalla** | Estados de Solicitud — Listado y Búsqueda |
| **Atiende (HU / RF / CU)** | HU-19 / RF-19 / CU-19 (y da entrada a HU-18 / CU-18 y HU-20 / CU-20) |
| **Campos ↔ Diccionario** | **Filtro de búsqueda:** por identificador o código de estado (id_estado_solicitud / codigo_estado).<br>**Columnas de la tabla:** id_estado_solicitud, codigo_estado, nombre_estado, descripcion, es_final, y columna de Acciones. |
| **Botones ↔ Eventos** | **Buscar** → consultar(id_estado_solicitud) (HU-19 / CU-19, RF-19).<br>**+ Nuevo Estado** → abre MK-14 en modo registrar (HU-18 / CU-18 → crear(), RF-18).<br>**Editar** → abre MK-14 con datos cargados (HU-20 / CU-20 → actualizar(), RF-20). |
| **RN visibles** | Mensaje de no encontrado correspondiente al CA-2 de la HU-19[cite: 11]. |

---

## Mockup MK-14 — Registrar / Actualizar Estado de Solicitud (C y U)

<img width="930" height="444" alt="image" src="https://github.com/user-attachments/assets/271e8673-7787-47ad-b0b3-a41f2e579557" />

### Ficha del mockup MK-14
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-14 |
| **Pantalla** | Estados de Solicitud — Formulario de Registro / Actualización |
| **Atiende (HU / RF / CU)** | HU-18 / RF-18 / CU-18 (Crear) y HU-20 / RF-20 / CU-20 (Actualizar) |
| **Campos ↔ Diccionario** | **id_estado_solicitud** (solo lectura en edición).<br>**codigo_estado** (sujeto a unicidad uq_estado_codigo).<br>**nombre_estado** (sujeto a unicidad uq_estado_nombre).<br>**descripcion**.<br>**es_final** (bandera booleana de estado terminal). |
| **Botones ↔ Eventos** | **Guardar Estado** → Ejecuta crear() (HU-18 / RF-18) o actualizar(id_estado_solicitud) (HU-20 / RF-20) validando unicidad y campos obligatorios.<br>**Cancelar** → retorna al listado MK-13 sin cambios. |
| **RN visibles / Camino Triste** | **RN-22 (unicidad del código y nombre, uq_estado_codigo y uq_estado_nombre):** CA-2 de la HU-18.<br>**RN-23 (restricción de alteración de la bandera es_final si existen solicitudes activas vinculadas):** CA-2 de la HU-20. |

---

## Cobertura CRUD de la Entidad estado_solicitud

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **crear()** | HU-18 / RF-18 | C | MK-14 (Formulario de Registro/Actualización): botón "Guardar Estado" |
| **consultar(id_estado_solicitud)** | HU-19 / RF-19 | R | MK-13 (Listado y Búsqueda): filtros por ID/código y tabla general del catálogo |
| **actualizar(id_estado_solicitud)** | HU-20 / RF-20 | U | MK-14 (Formulario en modo edición, ingresando desde el botón "Editar" del MK-13): botón "Guardar Estado" |

## Mockup MK-15 — Listado y Búsqueda de Solicitudes (R)

<img width="930" height="504" alt="image" src="https://github.com/user-attachments/assets/4b7cb9cb-ef76-4e18-8eda-7dc6697a24ad" />

### Ficha del mockup MK-15
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-15 |
| **Pantalla** | Solicitudes — Listado y Búsqueda |
| **Atiende (HU / RF / CU)** | HU-22 / RF-22 / CU-22 (y da entrada a HU-21 / CU-21, HU-23 / CU-23, HU-24 / CU-24, HU-26 / CU-26 y HU-27 / CU-43)<br>Complemento: la columna estado refleja el proceso interno HU-25 / RF-25 / CU-25 (cambiarEstado()), sin botón de interfaz. |
| **Campos ↔ Diccionario** | **Filtro de búsqueda:** por identificador de solicitud (id_solicitud) o código de radicado.<br>**Columnas de la tabla:** id_solicitud, asunto, tipo_solicitud, estado, fecha_radicacion, solicitante (con enmascaramiento a "SOLICITANTE ANÓNIMO" si anonimo_bloqueado = true), y columna de Acciones. |
| **Botones ↔ Eventos** | **Buscar** → consultar(id_solicitud) (HU-22 / CU-22, RF-22).<br>**+ Nueva Solicitud** → abre MK-16 en modo borrador (HU-21 / CU-21 → crear(), RF-21).<br>**Editar** → abre MK-16 si está en borrador o devuelta (HU-23 / CU-23 → actualizar(), RF-23; desde allí se radica: HU-24 / CU-24, RF-24).<br>**Desblindar** → abre el modal MK-17 para revelar la identidad anónima si posee privilegios de Gerente/Administrador (HU-26 / CU-26 → desblindarIdentidad(), RF-26).<br>**Inactivar** → abre el modal MK-28 (HU-27 / CU-43 → inactivar(), RF-27). Esta acción se representa en MK-28 (la captura original de MK-15 no la muestra). |
| **RN visibles** | Protección de identidad anónima (RN-04) y mensaje de expediente no encontrado correspondiente al CA-3 de la HU-22. |

---

## Mockup MK-16 — Crear Borrador / Actualizar Solicitud (C y U)

<img width="849" height="630" alt="image" src="https://github.com/user-attachments/assets/7df898b0-e5a2-47c9-87ab-0f96ab5d02e8" />

### Ficha del mockup MK-16
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-16 |
| **Pantalla** | Solicitudes — Formulario de Borrador y Edición |
| **Atiende (HU / RF / CU)** | HU-21 / RF-21 / CU-21 (Crear borrador), HU-23 / RF-23 / CU-23 (Actualizar contenido) y HU-24 / RF-24 / CU-24 (Radicar formalmente) |
| **Campos ↔ Diccionario** | **id_solicitud** (solo lectura).<br>**id_tipo_solicitud** (Selector de tipo de solicitud activo, validando RN-16).<br>**asunto** (texto descriptivo corto).<br>**descripcion** (área de texto detallada).<br>**anonimo_bloqueado** (casilla de verificación booleana para protección de identidad). |
| **Botones ↔ Eventos** | **Guardar Borrador** → Ejecuta crear() (HU-21 / RF-21) asignando estado "BORRADOR".<br>**Actualizar Solicitud** → Ejecuta actualizar(id_solicitud) (HU-23 / RF-23) registrando fecha_actualizacion.<br>**Radicar Formalmente** → Cambia el estado a "PENDIENTE" y fija la fecha inalterable (radicar(), HU-24 / RF-24, RN-14).<br>**Cancelar** → Retorna al listado MK-15. |
| **RN visibles** | Validación de tipo de solicitud activo (RN-16, CA-2 de HU-21).<br>RN-19 (bloqueo de edición en estados no permitidos): CA-2 de HU-23.<br>Obligatoriedad de descripción para la radicación formal (CA-2 de HU-24). |

---

## Mockup MK-17 — Modal de Desblindaje de Identidad (Auditoría)

<img width="930" height="455" alt="image" src="https://github.com/user-attachments/assets/06875485-27c8-45bb-9d39-6537495ed90d" />

### Ficha del mockup MK-17
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-17 |
| **Pantalla** | Solicitudes — Modal de Confirmación de Desblindaje de Identidad Anónima |
| **Atiende (HU / RF / CU)** | HU-26 / RF-26 / CU-26 (Desblindar identidad anónima) |
| **Campos / Elementos** | Ventana modal de seguridad que advierte sobre la revelación de datos personales protegidos bajo una solicitud anónima (anonimo_bloqueado = true). |
| **Botones ↔ Eventos** | **Confirmar Desblindaje** → Ejecuta desblindarIdentidad(id_usuario) (HU-26 / RF-26) revelando los datos del autor y generando un registro inmutable en la bitácora de auditoría (RN-04) (CA-1 de HU-26).<br>**Cancelar** → Cierra el modal sin alterar la privacidad del caso. |
| **RN visibles / Restricción** | Validación estricta del rol de Gerente o Administrador (RN-04); en caso contrario, el sistema bloquea la acción emitiendo la alerta de privilegios insuficientes (CA-2 de HU-26). |

---

## Mockup MK-28 — Modal de Inactivación de Solicitud (D lógico)

<img width="930" height="434" alt="image" src="https://github.com/user-attachments/assets/facab9f2-e3bf-45cb-be6a-64f77f98a581" />

### Ficha del mockup MK-28
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-28 |
| **Pantalla** | Solicitudes — Modal de Confirmación de Inactivación de Solicitud |
| **Atiende (HU / RF / CU)** | HU-27 / RF-27 / CU-43 (Inactivar solicitud) |
| **Campos / Elementos** | Ventana modal emergente de advertencia (sobre el listado MK-15) que muestra el identificador de la solicitud (id_solicitud) y su asunto, el icono de alerta y el texto explicativo de la consecuencia de la baja lógica. |
| **Botones ↔ Eventos** | **Confirmar Inactivación** → Ejecuta inactivar(id_solicitud) (HU-27 / RF-27): cambia el estado a inactivo, retorna true y genera el registro de la acción en la bitácora de auditoría (CA-1 de HU-27).<br>**Cancelar** → Cierra el modal y retorna al listado MK-15 sin alterar la solicitud. |
| **RN visibles / Texto del Aviso** | > ¿Desea inactivar la solicitud SOL-108?<br>> La solicitud pasará a estado inactivo (baja lógica). Su registro y su historial se conservarán en el sistema y la acción quedará registrada en la bitácora de auditoría.<br>(Camino triste, RN-20 / CA-2 de HU-27): si el usuario no posee rol de Administrador o la solicitud no existe, el sistema bloquea la acción, retorna false y muestra la alerta "No cuenta con los privilegios requeridos o la solicitud no existe". |

---

## Cobertura CRUD de la Entidad Solicitud

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **crear()** | HU-21 / RF-21 | C | MK-16 (Formulario de Borrador): botón "Guardar Borrador" |
| **consultar(id_solicitud)** | HU-22 / RF-22 | R | MK-15 (Listado y Búsqueda): filtros de ID y tabla general de expedientes |
| **actualizar(id_solicitud)** | HU-23 / RF-23 | U | MK-16 (Formulario en modo edición de borrador/ajustes): botón "Actualizar Solicitud" |
| **radicar()** | HU-24 / RF-24 | U (Transición) | MK-16: botón "Radicar Formalmente" (pasa a estado PENDIENTE) |
| **cambiarEstado(nuevoEstado)** | HU-25 / RF-25 / RN-15 | U (Workflow) | INTERNO: acciones automáticas del sistema / transiciones del flujo con bitácora obligatoria (RN-15); su efecto se ve en la columna estado de MK-15 |
| **desblindarIdentidad(id_usuario)** | HU-26 / RF-26 | R (Especial) | MK-17 (Modal de Seguridad): botón "Confirmar Desblindaje" (accionado desde MK-15) |
| **inactivar(id_solicitud)** | HU-27 / RF-27 | D lógico | MK-28 (Modal de Confirmación): botón "Confirmar Inactivación" (accionado desde el botón "Inactivar" del MK-15) |

## Mockup MK-18 — Listado y Consulta de Dictámenes de Aprobación (R)

<img width="930" height="390" alt="image" src="https://github.com/user-attachments/assets/6d006e8f-46d3-40de-8ba3-162ee125cb21" />

### Ficha del mockup MK-18
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-18 |
| **Pantalla** | Aprobaciones — Listado y Búsqueda de Dictámenes |
| **Atiende (HU / RF / CU)** | HU-31 / RF-31 / CU-30 (y da entrada a HU-28 / CU-27, HU-29 / CU-28 y HU-30 / CU-29) |
| **Campos ↔ Diccionario** | **Filtro de búsqueda:** por id_aprobacion o id_solicitud.<br>**Columnas de la tabla:** id_aprobacion, id_solicitud, decision (Aprobado, Rechazado, Devuelto_Para_Ajustes), comentario, fecha_decision y aprobador (id_aprobador). |
| **Botones ↔ Eventos** | **Buscar** → consultar(id_aprobacion) (HU-31 / CU-30, RF-31).<br>**+ Evaluar Solicitud** → abre MK-19 para registrar dictamen mediante aprobar(), rechazar() o devolverParaAjustes() (HU-28, HU-29, HU-30 / RF-28, RF-29, RF-30). |
| **RN visibles** | Mensaje de dictamen no encontrado correspondiente al CA-2 de la HU-31. |

---

## Mockup MK-19 — Formulario de Evaluación de Solicitud (C / Workflow de Aprobación)

<img width="930" height="416" alt="image" src="https://github.com/user-attachments/assets/26117835-35d3-427d-ad52-f0673c08747c" />

### Ficha del mockup MK-19
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-19 |
| **Pantalla** | Aprobaciones — Formulario de Evaluación y Resolución de Solicitud |
| **Atiende (HU / RF / CU)** | HU-28 / RF-28 / CU-27 (Aprobar), HU-29 / RF-29 / CU-28 (Rechazar) y HU-30 / RF-30 / CU-29 (Devolver para Ajustes) |
| **Campos ↔ Diccionario** | **id_aprobacion** (solo lectura).<br>**id_solicitud**.<br>**decision** (Aprobar, Rechazar, Devolver para Ajustes).<br>**comentario** (obligatorio, validado según RN-06). |
| **Botones ↔ Eventos** | **Aprobar Solicitud** → aprobar() (HU-28 / RF-28), valida RN-05 y cambia estado a APROBADA.<br>**Rechazar Solicitud** → rechazar(comentario) (HU-29 / RF-29), valida RN-06 y cambia estado a RECHAZADA.<br>**Devolver para Ajustes** → devolverParaAjustes(comentario) (HU-30 / RF-30), valida RN-06 y cambia estado a PENDIENTE_AJUSTES.<br>**Cancelar** → retorna a MK-18. |
| **RN visibles** | Restricción de autoaprobación (RN-05 / trg_validar_aprobador): CA-2 de HU-28.<br>Obligatoriedad de justificación para rechazo o devolución (RN-06 / chk_aprobacion_comentario): CA-2 de HU-29 y CA-2 de HU-30. |

---

## Cobertura CRUD de la Entidad aprobacion_solicitud

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **aprobar()** | HU-28 / RF-28 | C (Transición) | MK-19, botón "Aprobar Solicitud" |
| **rechazar(comentario)** | HU-29 / RF-29 | C (Transición) | MK-19, botón "Rechazar Solicitud" |
| **devolverParaAjustes(comentario)** | HU-30 / RF-30 | C (Transición) | MK-19, botón "Devolver para Ajustes" |
| **consultar(id_aprobacion)** | HU-31 / RF-31 | R | MK-18, filtros de búsqueda y listado de resoluciones |

## Mockup MK-20 — Listado y Búsqueda de Gestiones Operativas (R)

<img width="930" height="386" alt="image" src="https://github.com/user-attachments/assets/f0a68776-345c-44ae-a7d3-7ac2d1c2906a" />

### Ficha del mockup MK-20
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-20 |
| **Pantalla** | Gestión Operativa — Listado y Búsqueda de Casos en Curso |
| **Atiende (HU / RF / CU)** | HU-36 / RF-36 / CU-37 (y da entrada a HU-32 / CU-33, HU-33 / CU-34, HU-34 / CU-35 y HU-35 / CU-36) |
| **Campos ↔ Diccionario** | **Filtro de búsqueda:** por identificador de la gestión (id_gestion) o de la solicitud asociada (id_solicitud).<br>**Columnas de la tabla:** id_gestion, id_solicitud, prioridad ('Baja', 'Media', 'Alta', 'Critica'), estado_gestion ('En_Proceso', 'Reasignado', 'Finalizado'), fecha_vinculacion y fecha_cierre. |
| **Botones ↔ Eventos** | **Buscar** → consultar(id_gestion) (HU-36 / CU-37, RF-36).<br>**+ Asignar Gestor** → abre MK-21 para vincular un caso (HU-32 / CU-33 → asignarGestor(), RF-32).<br>**Reasignar** → abre MK-21 para cambiar de responsable (HU-33 / CU-34 → reasignar(), RF-33).<br>**Actualizar Prioridad** → abre MK-21 en modo edición (HU-34 / CU-35 → actualizarPrioridad(), RF-34).<br>**Finalizar** → abre el modal MK-22 para el cierre operativo (HU-35 / CU-36 → finalizar(), RF-35). |
| **RN visibles** | Mensaje de registro de gestión no encontrado correspondiente al CA-2 de la HU-36. |

---

## Mockup MK-21 — Formulario de Asignación y Reasignación de Gestor (C / U)

<img width="930" height="486" alt="image" src="https://github.com/user-attachments/assets/99c3634c-ac34-4a78-ab50-44d55d053cc4" />

### Ficha del mockup MK-21
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-21 |
| **Pantalla** | Gestión Operativa — Formulario de Asignación de Recursos y Prioridades |
| **Atiende (HU / RF / CU)** | HU-32 / RF-32 / CU-33 (Asignar gestor), HU-33 / RF-33 / CU-34 (Reasignar gestor) y HU-34 / RF-34 / CU-35 (Actualizar prioridad) |
| **Campos ↔ Diccionario** | **id_gestion** (solo lectura).<br>**id_solicitud** (identificador del trámite aprobado en curso).<br>**id_gestor** (selector desplegable con los gestores activos disponibles).<br>**prioridad** (selector ENUM obligatorio: 'Baja', 'Media', 'Alta', 'Critica' según HU-34). |
| **Botones ↔ Eventos** | **Guardar Asignación** → Ejecuta asignarGestor(id_gestor) (HU-32 / RF-32) o reasignar(id_gestor) (HU-33 / RF-33), validando la regla de gestión única activa (RN-11 / trg_gestion_unica_activa); en modo edición de prioridad ejecuta actualizarPrioridad() (HU-34 / RF-34).<br>**Cancelar** → Retorna al listado MK-20 sin guardar cambios. |
| **RN visibles / Camino Triste** | Restricción de gestión única activa por solicitud (RN-11 / disparador trg_gestion_unica_activa): CA-2 de HU-32.<br>Validación de selección de gestor distinto al actual en reasignaciones: CA-2 de HU-33.<br>RN-24 (valor de prioridad dentro de la enumeración PrioridadGestion): CA-2 de HU-34. |

---

## Mockup MK-22 — Modal de Cierre y Finalización de Gestión (U / Transición)

<img width="930" height="528" alt="image" src="https://github.com/user-attachments/assets/99f0deec-3ff3-4312-a2ee-53d7d3e1b64b" />

### Ficha del mockup MK-22
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-22 |
| **Pantalla** | Gestión Operativa — Modal de Confirmación de Cierre y Finalización |
| **Atiende (HU / RF / CU)** | HU-35 / RF-35 / CU-36 (Finalizar gestión de la solicitud) |
| **Campos / Elementos** | Ventana modal emergente que detalla el identificador de la gestión (id_gestion), la fecha y hora de vinculación inicial, y un campo editable u automático para la fecha_cierre. |
| **Botones ↔ Eventos** | **Confirmar Finalización** → Ejecuta finalizar() (HU-35 / RF-35), validando estrictamente que la fecha de cierre sea coherente con la fecha de vinculación (RN-12 / chk_gestion_fechas) y pasando la solicitud a estado "SOLUCIONADO".<br>**Cancelar** → Cierra el modal y mantiene la gestión en curso. |
| **RN visibles / Camino Triste** | Validación temporal de coherencia de fechas (chk_gestion_fechas / RN-12): si se intenta registrar una fecha de cierre anterior a la vinculación, se bloquea la transacción (CA-2 de HU-35). |

---

## Cobertura CRUD de la Entidad gestion_solicitud

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **asignarGestor(id_gestor)** | HU-32 / RF-32 | C (Transición) | MK-21 (Formulario de Asignación): botón "Guardar Asignación" |
| **reasignar(id_gestor)** | HU-33 / RF-33 | U (Transición) | MK-21 (Formulario de Asignación/Reasignación): botón de actualización de recurso (entrada por Reasignar en MK-20) |
| **actualizarPrioridad(nuevaPrioridad)** | HU-34 / RF-34 | U | MK-20 (Listado) / MK-21: selector de niveles ('Baja', 'Media', 'Alta', 'Critica') |
| **finalizar()** | HU-35 / RF-35 | U (Transición) | MK-22 (Modal de Cierre): botón "Confirmar Finalización" |
| **consultar(id_gestion)** | HU-36 / RF-36 | R | MK-20 (Listado y Búsqueda): filtros de ID y tabla general de seguimiento operativo |

## Mockup MK-23 — Listado y Consulta de Evaluaciones de Servicio (R)

<img width="930" height="487" alt="image" src="https://github.com/user-attachments/assets/dd4d49fc-6580-48ad-a526-37260528dc13" />

### Ficha del mockup MK-23
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-23 |
| **Pantalla** | Evaluaciones — Listado y Consulta de Satisfacción del Servicio |
| **Atiende (HU / RF / CU)** | HU-38 / RF-38 / CU-39 (y da entrada a HU-37 / CU-38) |
| **Campos ↔ Diccionario** | **Filtro de búsqueda:** por identificador de la evaluación (id_evaluacion) o del servicio asociado (id_gestion).<br>**Columnas de la tabla:** id_evaluacion, id_gestion, calificacion (escala de 1 a 5 estrellas), comentario y fecha de registro. |
| **Botones ↔ Eventos** | **Buscar** → consultar(id_evaluacion) (HU-38 / CU-39, RF-38).<br>**+ Evaluar Servicio** → abre MK-24 para registrar la calificación del trámite solucionado (HU-37 / CU-38 → calificar(), RF-37).<br>**Ver Detalle** → despliega la ficha completa de la calificación seleccionada (HU-38 / CU-39, RF-38). |
| **RN visibles** | Mensaje de registro de evaluación no encontrado correspondiente al CA-2 de la HU-38. |

---

## Mockup MK-24 — Formulario de Calificación y Evaluación de Servicio (C)

<img width="930" height="612" alt="image" src="https://github.com/user-attachments/assets/e4d8a58b-385c-42b1-9975-76fd961d727f" />

### Ficha del mockup MK-24
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-24 |
| **Pantalla** | Evaluaciones — Formulario de Calificación de la Atención Recibida |
| **Atiende (HU / RF / CU)** | HU-37 / RF-37 / CU-38 (Calificar servicio recibido) |
| **Campos ↔ Diccionario** | **id_evaluacion** (solo lectura).<br>**id_gestion** (identificador del trámite finalizado).<br>**calificacion** (selector interactivo de 1 a 5 estrellas obligatorio según RN-07).<br>**comentario** (área de texto opcional para observaciones del usuario). |
| **Botones ↔ Eventos** | **Enviar Calificación** → Ejecuta calificar(puntaje, comentario) (HU-37 / RF-37), validando estrictamente que la gestión esté finalizada (RN-13 / trg_validar_evaluacion), que no exista duplicidad por gestión (uq_evaluacion_gestion) y que el puntaje esté en el rango permitido de 1 a 5 (RN-07).<br>**Cancelar** → Retorna al listado MK-23 sin guardar cambios. |
| **RN visibles / Camino Triste** | Validación de estado finalizado de la gestión (RN-13): CA-2 de HU-37.<br>Restricción de evaluación única por servicio (uq_evaluacion_gestion): CA-3 de HU-37.<br>Control de rango numérico entero entre 1 y 5 (RN-07): CA-4 de HU-37. |

---

## Cobertura CRUD de la Entidad evaluacion

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **calificar(puntaje, comentario)** | HU-37 / RF-37 | C | MK-24 (Formulario de Calificación): botón "Enviar Calificación" |
| **consultar(id_evaluacion)** | HU-38 / RF-38 | R | MK-23 (Listado y Búsqueda): filtros de ID y tabla general de seguimiento de satisfacción |

## Mockup MK-25 — Listado y Consulta del Historial Conversacional (R)

<img width="930" height="619" alt="image" src="https://github.com/user-attachments/assets/4faf0e90-9f33-4217-a197-aed87fa4351c" />

### Ficha del mockup MK-25
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-25 |
| **Pantalla** | Detalle de Solicitud — Hilo Conversacional y Bitácora de Interacciones |
| **Atiende (HU / RF / CU)** | HU-40 / RF-40 / CU-32 (y da entrada a HU-39 / CU-31) |
| **Campos ↔ Diccionario** | **Filtro o parámetro de entrada:** por identificador de la solicitud (id_solicitud).<br>**Columnas del listado cronológico:** fecha_registro (marca de tiempo), usuario (remitente), mensaje (texto descriptivo) y ruta_adjunto (enlace al archivo vinculado). |
| **Botones ↔ Eventos** | **Buscar / Consultar** → consultarPorSolicitud(id_solicitud) (HU-40 / CU-32, RF-40).<br>**+ Agregar Interacción** → abre el formulario MK-26 para publicar un nuevo mensaje o adjunto (HU-39 / CU-31 → crear(), RF-39). |
| **RN visibles** | Leyenda de bitácora vacía correspondiente al CA-2 de la HU-40 ("No existen mensajes o adjuntos adicionales para esta solicitud"). |

---

## Mockup MK-26 — Formulario de Registro de Interacción y Adjuntos (C)

<img width="854" height="630" alt="image" src="https://github.com/user-attachments/assets/50ac1335-10fc-49a4-9e3d-238f17b2256f" />

### Ficha del mockup MK-26
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-26 |
| **Pantalla** | Detalle de Solicitud — Formulario de Publicación de Mensajes y Soportes |
| **Atiende (HU / RF / CU)** | HU-39 / RF-39 / CU-31 (Crear detalle o interacción en solicitud) |
| **Campos ↔ Diccionario** | **id_detalle** (solo lectura).<br>**id_solicitud** (identificador del expediente asociado).<br>**mensaje** (área de texto para observaciones o notas).<br>**ruta_adjunto** (selector de archivos de soporte para cargar documentos). |
| **Botones ↔ Eventos** | **Publicar Interacción** → Ejecuta crear() (HU-39 / RF-39), validando estrictamente bajo la regla RN-08 (chk_detalle_contenido) que se ingrese al menos un mensaje de texto o un archivo adjunto válido (prohibición de registros totalmente vacíos).<br>**Cancelar** → Retorna al listado MK-25 sin guardar cambios. |
| **RN visibles / Camino Triste** | Restricción de contenido obligatorio RN-08 (chk_detalle_contenido): si el usuario intenta enviar el formulario dejando el mensaje en blanco y sin adjuntar ningún archivo, el sistema bloquea la transacción y muestra el error correspondiente (CA-3 de HU-39). |

---

## Cobertura CRUD de la Entidad detalle_solicitud

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **crear()** | HU-39 / RF-39 | C | MK-26 (Formulario de Interacción): botón "Publicar Interacción" |
| **consultarPorSolicitud(id_solicitud)** | HU-40 / RF-40 | R | MK-25 (Listado y Búsqueda): consulta cronológica del hilo conversacional por ID de solicitud |


## Mockup MK-27 — Listado, Búsqueda y Filtrado de Trazas de Auditoría (R)

<img width="891" height="630" alt="image" src="https://github.com/user-attachments/assets/0dbe439f-52ec-4d7f-baae-2dee94ec33a1" />

### Ficha del mockup MK-27
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-27 |
| **Pantalla** | Bitácora de Auditoría — Consulta de Eventos del Sistema |
| **Atiende (HU / RF / CU)** | HU-42 / RF-42 / CU-41 (Consultar auditoría por entidad), HU-43 / RF-43 / CU-42 (Consultar auditoría por rango de fechas) y HU-45 / RF-45 / CU-45 (Exportar informe de auditoría)<br>Complemento: visualiza lo que registra automáticamente el proceso interno HU-41 / RF-41 / CU-40 (registrarAccion()), sin botón de interfaz. |
| **Campos ↔ Diccionario** | **Filtros de búsqueda avanzada:** campos para seleccionar la entidad (ej. "Solicitud"), el identificador del registro (id_registro) y el rango de fechas (desde, hasta).<br>**Columnas de la tabla de resultados:** id_bitacora, fecha_registro, usuario_responsable, entidad, id_registro, accion, estado_previo y estado_nuevo. |
| **Botones ↔ Eventos** | **Buscar / Filtrar** → Ejecuta consultarPorEntidad(entidad, id_registro) (HU-42 / RF-42) o consultarPorRango(desde, hasta) (HU-43 / RF-43) utilizando los índices optimizados del sistema.<br>**Exportar Informe** → Ejecuta exportarInforme(formato) (HU-45 / RF-45 / CU-45): descarga los registros filtrados en formato CSV o PDF para análisis de seguridad, sin alterarlos (RN-09, RN-25). |
| **RN visibles / Restricciones** | **RN-25 (control de acceso por rol):** si un usuario sin rol de Gerente o Auditor intenta acceder a la consulta, el sistema restringe el acceso y emite la alerta de seguridad correspondiente (CA-2 de la HU-42).<br>**RN-09:** la interfaz refleja explícitamente que la bitácora es de solo lectura e inalterable, careciendo de botones de edición o eliminación física (UPDATE / DELETE prohibidos por RN-09, CA-2 de HU-41).<br>**RN-26 (rango de fechas inconsistente):** el sistema rechaza la consulta cuando desde es posterior a hasta (CA-2 de la HU-43). |

---

## Cobertura CRUD de la Entidad bitacora_auditoria

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **registrarAccion(...)** | HU-41 / RF-41 / RN-09 / RN-15 | C (Automático) | Proceso interno del sistema: se ejecuta automáticamente ante cualquier cambio de estado (RN-15) u operación sensible, alimentando la tabla de forma inalterable (trg_bitacora_no_update y trg_bitacora_no_delete); su resultado se consulta en MK-27. |
| **consultarPorEntidad(entidad, id_registro)** | HU-42 / RF-42 | R | MK-27: filtros de entidad e ID de registro junto con el botón de búsqueda y el índice optimizado idx_bitacora_entidad_registro. |
| **consultarPorRango(desde, hasta)** | HU-43 / RF-43 | R | MK-27: filtros de fecha inicial (desde) y fecha final (hasta) para la generación de reportes de auditoría por períodos. |
| **exportarInforme(formato)** | HU-45 / RF-45 | R (Exportación) | MK-27: botón "Exportar Informe" (CSV o PDF) sobre los resultados filtrados. |
