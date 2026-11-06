
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
