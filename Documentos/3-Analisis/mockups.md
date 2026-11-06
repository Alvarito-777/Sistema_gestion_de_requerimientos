
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

<img width="930" height="470" alt="image" src="https://github.com/user-attachments/assets/43bb7c20-e33e-434b-81a4-c56093ca0798" />

### Ficha del mockup MK-04
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-04[cite: 13] |
| **Pantalla** | Usuarios — Listado y búsqueda[cite: 13] |
| **Atiende (HU / RF / CU)** | HU-06 / RF-06 / CU-06 (y da entrada a HU-05 / CU-05, HU-07 / CU-07 y HU-08 / CU-08)[cite: 13] |
| **Campos ↔ Diccionario** | **Filtro:** búsqueda por identificador del usuario (id_usuario)[cite: 13].<br>**Columnas de la tabla:** id_usuario, nombre_completo, correo_corporativo, estado_cuenta, intentos_fallidos, fecha_creacion[cite: 13]. |
| **Botones ↔ Eventos** | **Buscar** → consultar(id_usuario) (HU-06 / CU-06, RF-06)[cite: 13].<br>**+ Nuevo Usuario** → abre MK-05 en modo registrar (HU-05 / CU-05 → crear(), RF-05)[cite: 13].<br>**Editar** → abre MK-05 con datos cargados (HU-07 / CU-07 → actualizar(), RF-07)[cite: 13].<br>**Inactivar** → abre aviso MK-06 (HU-08 / CU-08 → inactivar(), RF-08; preservación lógica de datos con ON DELETE RESTRICT según RN-10)[cite: 13]. |
| **RN visibles** | Ninguna directamente en la tabla principal; la validación de dominio corporativo (RN-01) opera al registrar/actualizar, y el mensaje "El usuario con identificador no existe en el sistema" corresponde al CA-2 de la HU-06[cite: 13].<br>Las columnas estado_cuenta e intentos_fallidos reflejan el resultado de los procesos internos HU-09 / CU-09 (registrarIntentoFallido(), RF-09) y HU-10 / CU-10 (reiniciarIntentos(), RF-10), regidos por RN-02; no tienen botón de interfaz[cite: 13]. |

---

## Mockup MK-05 — Registrar / Actualizar usuario (C y U)

<img width="801" height="630" alt="image" src="https://github.com/user-attachments/assets/896d2e80-116e-4ae7-8794-d890bd41aa16" />

### Ficha del mockup MK-05
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-05[cite: 13] |
| **Pantalla** | Usuarios — Formulario de Registro / Actualización[cite: 13] |
| **Atiende (HU / RF / CU)** | HU-05 / RF-05 / CU-05 (Crear) y HU-07 / RF-07 / CU-07 (Actualizar)<br>Complemento: el selector estado_cuenta permite el desbloqueo manual de HU-10 / RF-10 / CU-10 (CA-2)[cite: 13]. |
| **Campos ↔ Diccionario** | **id_usuario** (Identificador autoincremental de solo lectura, visible únicamente en modo edición)[cite: 13].<br>**nombre_completo** (Campo de texto obligatorio para los nombres y apellidos del titular)[cite: 13].<br>**correo_corporativo** (Campo de entrada para el correo institucional; valida la regla RN-01 de dominio corporativo y la unicidad uq_usuario_correo)[cite: 13].<br>**contrasena_hash** (Campo de contraseña enmascarado; se almacena de forma encriptada mediante bcrypt o Argon2)[cite: 13].<br>**estado_cuenta** (Selector ENUM: 'activo', 'inactivo', 'suspendido')[cite: 13].<br>**intentos_fallidos** (Contador numérico de control de acceso)[cite: 13]. |
| **Botones ↔ Eventos** | **Guardar Usuario** → Ejecuta crear() (HU-05 / RF-05) en modo registro (inicializando con estado activo e intentos fallidos en 0) o actualizar(id_usuario) (HU-07 / RF-07) en modo edición[cite: 13].<br>Al cambiar estado_cuenta de 'suspendido' a 'activo', el guardado ejecuta reiniciarIntentos() (HU-10 / RF-10, CA-2): intentos_fallidos = 0 y fecha_bloqueo = NULL[cite: 13].<br>**Cancelar** → Aborta la operación y retorna al listado MK-04 sin persistir cambios[cite: 13]. |
| **RN visibles** | **RN-01 (Dominio corporativo):** Si se ingresa un correo externo (ej. @gmail.com), el sistema rechaza el registro con el mensaje: "El correo debe pertenecer al dominio corporativo autorizado (@nexaservicios.com)." (CA-2 de HU-05)[cite: 13].<br>**Unicidad uq_usuario_correo:** si el correo ya existe, el sistema rechaza el guardado (CA-3 de HU-05 y CA-3 de HU-07)[cite: 13].<br>**RN-02 (Bloqueo y Estado):** Permite cambiar el estado de la cuenta a suspendido asociando automáticamente la fecha_bloqueo (CA-2 de HU-07)[cite: 13].<br>**Restricción NO NULO:** Si se omiten campos obligatorios, se resalta la celda con su respectiva advertencia (CA-4 de HU-05)[cite: 13]. |

---

## Mockup MK-06 — Aviso de inactivación (D lógico)

<img width="930" height="494" alt="image" src="https://github.com/user-attachments/assets/a7fdbce0-c1f7-4540-81e7-8563a996b20c" />

### Ficha del mockup MK-06
| Campo | Contenido |
| :--- | :--- |
| **Código** | MK-06[cite: 13] |
| **Pantalla** | Usuarios — Modal de Confirmación de Inactivación[cite: 13] |
| **Atiende (HU / RF / CU)** | HU-08 / RF-08 / CU-08 (Inactivar cuenta de usuario)[cite: 13] |
| **Campos / Elementos** | Ventana modal emergente con icono de advertencia, título de confirmación y el detalle de la cuenta a inhabilitar[cite: 13]. |
| **Botones ↔ Eventos** | **Confirmar Inactivación** → Ejecuta inactivar(id_usuario) (HU-08 / RF-08), modificando el atributo estado_cuenta a 'inactivo' y bloqueando el inicio de sesión bajo la política de borrado lógico (RN-10) (CA-2 de HU-08)[cite: 13].<br>**Cancelar** → Cierra el modal y retorna al listado MK-04 manteniendo la cuenta intacta[cite: 13]. |
| **RN visibles / Texto del Aviso** | > ¿Desea confirmar la inactivación? (CA-1 de HU-08)[cite: 13]<br>> "La cuenta de diego.rojas@nexaservicios.com será inhabilitada. Se conservarán sus registros en el sistema (RN-10)."[cite: 13]<br>Garantiza el cumplimiento estricto de la regla RN-10 (ON DELETE RESTRICT), evitando la eliminación física de la base de datos para preservar los vínculos históricos y de auditoría[cite: 13]. |

---

## Cobertura CRUD de la Entidad Usuario

| Método del diagrama de clases | Padre (HU / RF) | CRUD | Dónde aterriza |
| :--- | :--- | :--- | :--- |
| **crear()** | HU-05 / RF-05[cite: 13] | C[cite: 13] | MK-05 en modo registrar: botón Guardar Usuario[cite: 13] |
| **existeCorreo(correo)** | HU-05, HU-07 / RF-05, RF-07 / RN-01[cite: 13] | (apoyo)[cite: 13] | INTERNO: se dispara dentro de Guardar en ambos modos para validar dominio y unicidad; no necesita botón y así se declara[cite: 13] |
| **consultar(id_usuario)** | HU-06 / RF-06[cite: 13] | R[cite: 13] | MK-04: filtro por ID y botón Buscar / tabla de listado[cite: 13] |
| **actualizar(id_usuario)** | HU-07 / RF-07[cite: 13] | U[cite: 13] | MK-05 en modo actualizar (entrada por Editar en MK-04): botón Guardar Usuario[cite: 13] |
| **inactivar(id_usuario)** | HU-08 / RF-08[cite: 13] | D lógico[cite: 13] | MK-06: botón "Confirmar Inactivación" (entrada por Inactivar en MK-04)[cite: 13] |
| **registrarIntentoFallido()** | HU-09 / RF-09 / RN-02[cite: 13] | (apoyo)[cite: 13] | INTERNO: se ejecuta en la lógica de autenticación del sistema al fallar credenciales; no necesita botón de interfaz (su efecto se ve en MK-04)[cite: 13] |
| **reiniciarIntentos()** | HU-10 / RF-10 / RN-02[cite: 13] | (apoyo)[cite: 13] | INTERNO: se ejecuta al iniciar sesión exitosamente (CA-1) o al desbloquear la cuenta desde MK-05 cambiando estado_cuenta a activo (CA-2); no necesita botón propio[cite: 13] |
