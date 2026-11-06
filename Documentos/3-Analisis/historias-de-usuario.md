# Historias de usuario con criterios de aceptación

## Entidad rol

### Crear nuevo rol de usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-01 |
| **Título corto** | Crear nuevo rol de usuario |
| **Historia** | Como Administrador, quiero registrar un nuevo rol especificando su nombre, descripción y permiso de administración, para definir perfiles de acceso estructurados en el sistema. |
| **Criterios de aceptación** | Antecedentes:<br>  # Se cumple antes de CADA escenario de esta historia<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Registro exitoso de un nuevo rol válido<br>  # crear() · usa datos completos de la entidad Rol<br>  Dado que no existe ningún rol registrado con el nombre "Aprobador"<br>  Cuando Carlos registra un rol con los siguientes datos:<br>    \| nombre_rol \| Aprobador \|<br>    \| descripcion \| Usuario responsable de revisar y autorizar solicitudes \|<br>    \| permiso_administrar \| false \|<br>  Entonces el sistema registra el nuevo rol en el catálogo<br>  Y muestra el mensaje "Rol registrado correctamente."<br>  Y el rol "Aprobador" aparece en la lista de roles del sistema<br>Escenario: CA-2 Rechazo por nombre de rol duplicado<br>  # Restricción de unicidad uq_rol_nombre<br>  Dado que ya existe un rol registrado con el nombre "Administrador"<br>  Cuando Carlos intenta registrar un nuevo rol con el nombre "Administrador"<br>  Entonces el sistema no registra el rol<br>  Y muestra el mensaje "El nombre del rol 'Administrador' ya se encuentra registrado."<br>Esquema del escenario: CA-3 Rechazo por nombre de rol fuera del dominio permitido<br>  # RN-03 · Valida valores autorizados en el dominio del sistema<br>  Cuando Carlos intenta registrar un rol con el nombre <nombre_ingresado><br>  Entonces el sistema no guarda el registro<br>  Y muestra el mensaje "El nombre del rol debe pertenecer al dominio autorizado."<br>  Ejemplos:<br>    \| nombre_ingresado \|<br>    \| SuperUsuario \|<br>    \| Invitado \|<br>    \| Auditing \|<br>Esquema del escenario: CA-4 Rechazo por campos obligatorios incompletos<br>  # Restricción NO NULO del diccionario de datos<br>  Cuando Carlos deja vacío el campo <campo> y presiona "Guardar"<br>  Entonces el sistema no registra el rol<br>  Y resalta el campo indicando "<mensaje>"<br>  Ejemplos:<br>    \| campo \| mensaje \|<br>    \| nombre_rol \| Debe ingresar el nombre del rol. \|<br>    \| descripcion \| La descripción del rol es obligatoria. \| |
| **Origen de la necesidad** | Pregunta 9 del formulario, Regla RN-03 y método crear() de la clase Rol. |
| **RF derivados** | RF-01 |
| **Prioridad** | Alta |

---

### Consultar roles del sistema
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-02 |
| **Título corto** | Consultar roles del sistema |
| **Historia** | Como Administrador, quiero consultar la información de un rol registrado por su identificador, para verificar sus permisos e integrantes. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Listado general de roles registrados<br>  # listarTodos() / consultar()<br>  Dado que existen los siguientes roles en el sistema:<br>    \| id_rol \| nombre_rol \| descripcion \| permiso_administrar \|fecha_creacion \|<br>    \| 1 \| Administrador \| Acceso total al sistema \| true \| 2026-01-10 \|<br>    \| 2 \| Solicitante \| Creación de peticiones \| false \| 2026-01-15 \|<br>  Cuando Carlos ingresa a la consulta del catálogo de roles<br>  Entonces el sistema muestra en pantalla la lista con el ID, Nombre, Descripción y Estado de Permisos de Administrador y Solicitante<br>Escenario: CA-2 Búsqueda exitosa de rol por ID<br>  # consultar(id_rol) · muestra el detalle completo de la entidad<br>  Dado que existe un rol con id_rol = 1, nombre "Administrador", descripción "Acceso total al sistema", permiso_administrar = true y fecha_creacion "2026-01-10"<br>  Cuando Carlos busca el rol con id_rol 1<br>  Entonces el sistema despliega el expediente con los campos:<br>    \| id_rol \| 1 \|<br>    \| nombre_rol \| Administrador \|<br>    \| descripcion \| Acceso total al sistema \|<br>    \| permiso_administrar \| true \|<br>    \| fecha_creacion \| 2026-01-10 \|<br>Escenario: CA-3 Búsqueda de rol inexistente por ID<br>  Dado que no existe ningún rol registrado con el id_rol 99<br>  Cuando Carlos busca el rol con id_rol 99<br>  Entonces el sistema no muestra ningún expediente<br>  Y emite la advertencia "No se encontró ningún rol asociado al identificador 99." |
| **Origen de la necesidad** | Pregunta 15 del formulario y método consultar(id_rol) de la clase Rol. |
| **RF derivados** | RF-02 |
| **Prioridad** | Media |

---

### Actualizar información de rol
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-03 |
| **Título corto** | Actualizar información de rol |
| **Historia** | Como Administrador, quiero modificar la descripción o los permisos de administración de un rol existente, para ajustar el alcance de sus funciones. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>  Y que existe el rol "Gestion_Personal" registrado con id_rol 3, descripción "Manejo de personal" y permiso_administrar = false<br>Escenario: CA-1 Actualización exitosa de descripción y permisos<br>  # actualizar(id_rol)<br>  Cuando Carlos modifica la descripción a "Gestión integral del talento humano" y cambia permiso_administrar a true para el id_rol 3<br>  Entonces el sistema guarda los cambios en el rol 3<br>  Y muestra el mensaje "Información del rol actualizada correctamente."<br>  Y al consultar el id_rol 3 se observa la descripción "Gestión integral del talento humano" y permiso_administrar = true<br>Escenario: CA-2 Rechazo de actualización por duplicidad de nombre de rol<br>  # Restricción de unicidad uq_rol_nombre<br>  Dado que existe otro rol con id_rol 2 y nombre_rol "Gerente"<br>  Cuando Carlos intenta editar el nombre del rol 3 de "Gestion_Personal" a "Gerente"<br>  Entonces el sistema rechaza la actualización<br>  Y muestra el mensaje "El nombre del rol 'Gerente' ya está en uso por otro registro."<br>  Y los datos del rol 3 permanecen sin modificaciones<br>Escenario: CA-3 Rechazo por vaciar campo obligatorio al editar<br>  # Restricción NO NULO<br>  Cuando Carlos borra la descripción del rol 3 dejándola en blanco y presiona "Guardar"<br>  Entonces el sistema no actualiza el registro<br>  Y muestra el mensaje "La descripción del rol no puede quedar vacía." |
| **Origen de la necesidad** | Pregunta 13 del formulario, RN-03 (Dominio y unicidad del nombre del rol) y Mantenimiento de perfiles de acceso y método actualizar(id_rol) de la clase Rol. |
| **RF derivados** | RF-03 |
| **Prioridad** | Media |

---

### Inactivar rol del sistema
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-04 |
| **Título corto** | Inactivar rol del sistema |
| **Historia** | Como Administrador, quiero inactivar un rol mediante su identificador, para suspender su disponibilidad en nuevas asignaciones. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Confirmación previa a la inactivación<br>  Dado que existe el rol "Gerente" con id_rol 4 sin usuarios asignados<br>  Cuando Carlos solicita inactivar el rol con id_rol 4<br>  Entonces el sistema muestra la advertencia "El rol 'Gerente' no estará disponible para nuevas asignaciones. ¿Desea continuar?"<br>  Y el estado del rol no cambia hasta recibir confirmación<br>Escenario: CA-2 Inactivación exitosa de un rol sin asignaciones<br>  # inactivar(id_rol)<br>  Dado que Carlos está viendo la confirmación de inactivación del rol id_rol 4 "Gerente"<br>  Cuando confirma la operación<br>  Entonces el sistema deshabilita el rol en el catálogo<br>  Y muestra el mensaje "El rol ha sido inactivado exitosamente."<br>Escenario: CA-3 Rechazo de inactivación por restricción de integridad (usuarios asociados)<br>  # Regla RN-10 / ON DELETE RESTRICT en usuario_rol<br>  Dado que el rol "Solicitante" (id_rol 2) tiene usuarios activos asignados en la tabla usuario_rol<br>  Cuando Carlos intenta inactivar el id_rol 2<br>  Entonces el sistema detiene la operación<br>  Y muestra el mensaje "No es posible inactivar el rol porque existen usuarios activos vinculados a este perfil."<br>  Y el rol 2 permanece activo en el catálogo |
| **Origen de la necesidad** | Pregunta 9 de formulario, Regla RN-10 y método inactivar(id_rol) de la clase Rol. |
| **RF derivados** | RF-04 |
| **Prioridad** | Baja |

---

## Entidad usuario

### Registrar usuario en la plataforma
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-05 |
| **Título corto** | Registrar usuario en la plataforma |
| **Historia** | Como Administrador, quiero registrar una nueva cuenta de usuario con su correo corporativo y contraseña, para otorgarle acceso al sistema. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Registro exitoso de usuario con datos válidos<br>  # crear() · establece estado_cuenta = 'activo' e intentos_fallidos = 0<br>  Dado que no existe un usuario registrado con el correo "marta.perez@nexaservicios.com"<br>  Cuando Carlos registra una cuenta con los datos:<br>    \| correo_corporativo \| marta.perez@nexaservicios.com \|<br>    \| contrasena_hash \| P@ssword2026! \|<br>  Entonces la cuenta se crea con estado_cuenta = "activo" e intentos_fallidos = 0<br>  Y el sistema muestra el mensaje "Usuario registrado exitosamente."<br>Escenario: CA-2 Rechazo por correo con dominio no corporativo<br>  # RN-01 · Validación de dominio corporativo<br>  Cuando Carlos intenta registrar un usuario con el correo "marta.perez@gmail.com"<br>  Entonces el sistema no crea la cuenta<br>  Y muestra el mensaje "El correo debe pertenecer al dominio corporativo autorizado (@nexaservicios.com)."<br>Escenario: CA-3 Rechazo por correo corporativo duplicado<br>  Dado que ya existe un usuario registrado con el correo "juan.gomez@nexaservicios.com"<br>  Cuando Carlos intenta registrar otra cuenta con el correo "juan.gomez@nexaservicios.com"<br>  Entonces el sistema bloquea el registro<br>  Y muestra el mensaje "El correo corporativo ya se encuentra registrado en la plataforma."<br>Esquema del escenario: CA-4 Rechazo por campos de cuenta incompletos<br>  When Carlos omite el campo <campo> durante el registro de usuario<br>  Then el sistema no crea el usuario<br>  And señala "<mensaje>"<br>  Ejemplos:<br>    \| campo \| mensaje \|<br>    \| correo_corporativo \| El correo corporativo es obligatorio. \|<br>    \| contrasena_hash \| Debe asignar una contraseña para la cuenta. \| |
| **Origen de la necesidad** | Pregunta 21 del formulario, Regla RN-01 y método crear() de la clase Usuario. |
| **RF derivados** | RF-05 |
| **Prioridad** | Alta |

---

### Consultar expediente de usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-06 |
| **Título corto** | Consultar expediente de usuario |
| **Historia** | Como Administrador, quiero consultar la información de un usuario por su identificador, para validar sus datos de cuenta y estado. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Consulta exitosa de expediente de usuario activo<br>  # consultar(id_usuario)<br>  Dado que existe el usuario con id_usuario 10, correo "marta.perez@nexaservicios.com", estado_cuenta "activo", intentos_fallidos 0 y fecha_bloqueo nula<br>  Cuando Carlos consulta el expediente del usuario con id_usuario 10<br>  Entonces el sistema presenta el detalle completo del expediente:<br>    \| id_usuario \| 10 \|<br>    \| correo_corporativo \| marta.perez@nexaservicios.com \|<br>    \| estado_cuenta \| activo \|<br>    \| intentos_fallidos \| 0 \|<br>    \| fecha_bloqueo \| N/A \|<br>Escenario: CA-2 Consulta de usuario inexistente<br>  Dado que no existe ningún usuario asociado al id_usuario 999<br>  Cuando Carlos busca el expediente del id_usuario 999<br>  Entonces el sistema no muestra información<br>  Y emite la alerta "El usuario con identificador 999 no existe en el sistema." |
| **Origen de la necesidad** | Pregunta 15 del formulario, Control y auditoría de cuentas y método consultar(id_usuario) de la clase Usuario. |
| **RF derivados** | RF-06 |
| **Prioridad** | Media |

---

### Actualizar datos de usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-07 |
| **Título corto** | Actualizar datos de usuario |
| **Historia** | Como Administrador, quiero modificar la información general o la contraseña de un usuario, para mantener actualizadas sus credenciales. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>  Y que existe la cuenta activa id_usuario 10 con correo "marta.perez@nexaservicios.com"<br>Escenario: CA-1 Cambio exitoso de credenciales<br>  # actualizar(id_usuario)<br>  Cuando Carlos actualiza la contraseña del id_usuario 10<br>  Entonces el sistema encripta y guarda la nueva contraseña<br>  Y muestra el mensaje "Credenciales actualizadas correctamente."<br>Escenario: CA-2 Cambio de estado a suspendido exige fecha de bloqueo<br>  # RN-02 · chk_usuario_bloqueo<br>  Cuando Carlos cambia el estado_cuenta del id_usuario 10 a "suspendido"<br>  Entonces el sistema asigna automáticamente la fecha y hora actual en el campo fecha_bloqueo<br>  Y guarda el registro cumpliendo la restricción de bloqueo<br>Escenario: CA-3 Rechazo por asignación de correo duplicado<br>  Dado que existe otra cuenta registrada con el correo "ana.rios@nexaservicios.com"<br>  Cuando Carlos intenta modificar el correo del id_usuario 10 a "ana.rios@nexaservicios.com"<br>  Entonces el sistema rechaza el cambio<br>  Y muestra el mensaje "El correo corporativo ya pertenece a otra cuenta." |
| **Origen de la necesidad** | Pregunta 21 del formulario, Regla RN-02 y método actualizar(id_usuario) de la clase Usuario. |
| **RF derivados** | RF-07 |
| **Prioridad** | Alta |

---

### Inactivar cuenta de usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-08 |
| **Título corto** | Inactivar cuenta de usuario |
| **Historia** | Como Administrador, quiero inactivar la cuenta de un usuario por su identificador, para revocar su acceso sin eliminar sus datos del sistema. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>  Y que existe la cuenta activa id_usuario 12 perteneciente a "diego.rojas@nexaservicios.com"<br>Escenario: CA-1 Mensaje de confirmación de inactivación<br>  Cuando Carlos solicita la inactivación de la cuenta con id_usuario 12<br>  Entonces el sistema muestra el diálogo "La cuenta de diego.rojas@nexaservicios.com será inhabilitada. Se conservarán sus registros en el sistema. ¿Confirmar?"<br>  Y la cuenta permanece activa mientras no se confirme<br>Escenario: CA-2 Inactivación lógica confirmada (preservación de datos)<br>  # inactivar(id_usuario) · estado_cuenta = 'inactivo' (jamás DELETE por RN-10)<br>  Dado que Carlos confirma la inactivación del id_usuario 12<br>  Entonces el sistema actualiza el atributo estado_cuenta a "inactivo"<br>  Y bloquea el inicio de sesión para "diego.rojas@nexaservicios.com"<br>  Pero los registros históricos y claves foráneas asociadas en la base de datos se mantienen intactos |
| **Origen de la necesidad** | Pregunta 4 del formulario, Regla RN-10 y método inactivar(id_usuario) de la clase Usuario. |
| **RF derivados** | RF-08 |
| **Prioridad** | Alta |

---

### Registrar intento fallido de autenticación
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-09 |
| **Título corto** | Registrar intento fallido de autenticación |
| **Historia** | Como Administrador del sistema, quiero incrementar el contador de intentos fallidos al ingresar una contraseña incorrecta, para gestionar la seguridad de las cuentas. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que la cuenta "laura.gomez@nexaservicios.com" está en estado_cuenta "activo"<br>Escenario: CA-1 Incremento de contador por contraseña errónea<br>  # registrarIntentoFallido()<br>  Dado que el usuario tiene intentos_fallidos = 1<br>  Cuando la persona intenta ingresar con una contraseña incorrecta<br>  Entonces el sistema invoca registrarIntentoFallido() e incrementa el contador a 2<br>  Y muestra el mensaje "Credenciales inválidas. Intento 2 de 3."<br>Escenario: CA-2 Suspensión automática de la cuenta al alcanzar el límite máximo<br>  # RN-02 · estado_cuenta = 'suspendido' y asignación de fecha_bloqueo<br>  Dado que el usuario tiene intentos_fallidos = 2<br>  Cuando ingresa por tercera vez consecutiva una contraseña incorrecta<br>  Entonces el sistema incrementa intentos_fallidos a 3<br>  Y cambia el estado_cuenta a "suspendido"<br>  Y registra la fecha y hora actual en fecha_bloqueo<br>  Y muestra la alerta "Su cuenta ha sido suspendida por exceder el número máximo de intentos fallidos." |
| **Origen de la necesidad** | Pregunta 20 del formulario, Regla RN-02 y método registrarIntentoFallido() de la clase Usuario. |
| **RF derivados** | RF-09 |
| **Prioridad** | Alta |

---

### Reiniciar intentos fallidos de autenticación
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-10 |
| **Título corto** | Reiniciar intentos fallidos de autenticación |
| **Historia** | Como Administrador del sistema, quiero restablecer a cero el contador de intentos fallidos tras un inicio de sesión exitoso o un desbloqueo manual. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que la cuenta "laura.gomez@nexaservicios.com" está registrada en el sistema<br>Escenario: CA-1 Restablecimiento automático por inicio de sesión exitoso<br>  # reiniciarIntentos()<br>  Dado que la cuenta tiene intentos_fallidos = 2 y estado_cuenta = "activo"<br>  Cuando la persona ingresa correctamente su correo y contraseña<br>  Entonces el sistema ejecuta reiniciarIntentos() asignando intentos_fallidos = 0<br>  Y le permite el ingreso al panel principal<br>Escenario: CA-2 Restablecimiento manual y reactivación de cuenta por el Administrador<br>  # RN-02 · Limpieza de fecha_bloqueo y reactivación de estado<br>  Dado que la cuenta está con estado_cuenta = "suspendido", intentos_fallidos = 3 y fecha_bloqueo registrada<br>  Cuando el Administrador "Carlos Restrepo" ejecuta el desbloqueo manual de la cuenta<br>  Entonces el sistema asigna estado_cuenta = "activo"<br>  Y ejecuta reiniciarIntentos() dejando intentos_fallidos = 0<br>  Y limpia el campo fecha_bloqueo dejando valor nulo |
| **Origen de la necesidad** | Pregunta 21 del formulario, Regla RN-02 y método reiniciarIntentos() de la clase Usuario. |
| **RF derivados** | RF-10 |
| **Prioridad** | Media |

### Asignar rol a usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-11 |
| **Título corto** | Asignar rol a usuario |
| **Historia** | Como Administrador, quiero asociar un rol específico a un usuario, para concederle las atribuciones operativas del perfil. |
| **Criterios de aceptación** | Antecedentes:<br>  # Se cumple antes de CADA escenario de esta historia<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>  Y que existe el usuario activo "marta.perez@nexaservicios.com" con id_usuario 10<br>  Y que existe el rol activo "Aprobador" con id_rol 2<br>Escenario: CA-1 Asignación exitosa de rol a usuario<br>  # crear() en usuario_rol · registra (id_usuario, id_rol) y fecha_asignacion actual<br>  Dado que el usuario 10 no tiene asignado el rol 2<br>  Cuando Carlos asigna el rol "Aprobador" (id_rol 2) al usuario "marta.perez@nexaservicios.com" (id_usuario 10)<br>  Entonces el sistema registra el vínculo en la tabla usuario_rol<br>  Y guarda la fecha y hora actual en fecha_asignacion<br>  Y muestra el mensaje "Rol 'Aprobador' asignado correctamente al usuario."<br>Escenario: CA-2 Rechazo por asignación duplicada del mismo rol<br>  # Unicidad en la clave primaria compuesta (id_usuario, id_rol)<br>  Dado que el usuario 10 ya tiene asignado previamente el rol "Aprobador" (id_rol 2)<br>  Cuando Carlos intenta asignar nuevamente el id_rol 2 al id_usuario 10<br>  Entonces el sistema impide el registro<br>  Y muestra el mensaje "El usuario marta.perez@nexaservicios.com ya cuenta con el rol Aprobador."<br>Escenario: CA-3 Rechazo por asignación a usuario inactivo o inexistente<br>  Dado que el usuario "diego.rojas@nexaservicios.com" con id_usuario 12 está con estado_cuenta "inactivo"<br>  Cuando Carlos intenta asignarle el id_rol 2<br>  Entonces el sistema detiene la operación<br>  Y muestra el mensaje "No se puede asignar roles a una cuenta de usuario inactiva." |
| **Origen de la necesidad** | Pregunta 9 del formulario y método crear() de la clase usuario_rol. |
| **RF derivados** | RF-11 |
| **Prioridad** | Alta |

---

### Consultar asignación de rol de un usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-12 |
| **Título corto** | Consultar asignación de rol de un usuario |
| **Historia** | Como Administrador, quiero verificar la asignación específica entre un usuario y un rol por sus identificadores. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Consulta exitosa de vínculo existente<br>  # consultar(id_usuario, id_rol)<br>  Dado que el usuario id_usuario 10 "marta.perez@nexaservicios.com" tiene asignado el id_rol 2 "Aprobador" desde "2026-02-15"<br>  Cuando Carlos consulta la asignación entre id_usuario 10 e id_rol 2<br>  Entonces el sistema despliega el detalle de la relación:<br>    \| id_usuario \| 10 \|<br>    \| correo_corporativo \| marta.perez@nexaservicios.com \|<br>    \| id_rol \| 2 \|<br>    \| nombre_rol \| Aprobador \|<br>    \| fecha_asignacion \| 2026-02-15 \|<br>Escenario: CA-2 Consulta de asignación inexistente<br>  Dado que el usuario id_usuario 10 no tiene asignado el id_rol 4 "Gerente"<br>  Cuando Carlos consulta la relación entre id_usuario 10 e id_rol 4<br>  Entonces el sistema no muestra detalles<br>  Y emite la notificación "No existe la asignación del rol 'Gerente' para el usuario marta.perez@nexaservicios.com." |
| **Origen de la necesidad** | Pregunta 15 del formulario y método consultar(id_usuario, id_rol) de la clase usuario_rol. |
| **RF derivados** | RF-12 |
| **Prioridad** | Media |

---

### Revocar rol asignado a usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-13 |
| **Título corto** | Revocar rol asignado a usuario |
| **Historia** | Como Administrador, quiero desvincular un rol específico de un usuario por sus identificadores, para retirar los accesos correspondientes. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>  Y que el usuario id_usuario 10 "marta.perez@nexaservicios.com" tiene asignados los roles "Solicitante" (id_rol 1) y "Aprobador" (id_rol 2)<br>Escenario: CA-1 Revocación exitosa cuando el usuario conserva otros roles<br>  # revocar(id_usuario, id_rol)<br>  Cuando Carlos desvincula el id_rol 2 ("Aprobador") del id_usuario 10<br>  Entonces el sistema elimina la asociación de la tabla usuario_rol<br>  Y muestra el mensaje "Rol 'Aprobador' retirado del usuario marta.perez@nexaservicios.com correctamente."<br>  Y el usuario conserva únicamente el id_rol 1 ("Solicitante")<br>Escenario: CA-2 Rechazo de revocación por regla de rol único mínimo<br>  # Regla de negocio: la cuenta debe conservar al menos 1 rol activo<br>  Dado que el usuario id_usuario 15 "ana.rios@nexaservicios.com" tiene asignado únicamente el id_rol 1 ("Solicitante")<br>  Cuando Carlos intenta revocar el id_rol 1 al id_usuario 15<br>  Entonces el sistema bloquea la operación<br>  Y muestra el mensaje "No se puede revocar el rol. Toda cuenta de usuario debe mantener al menos un rol asignado en la plataforma."<br>  Y la relación se mantiene intacta |
| **Origen de la necesidad** | Pregunta 9 del formulario, Control de permisos y método revocar(id_usuario, id_rol) de la clase usuario_rol. |
| **RF derivados** | RF-13 |
| **Prioridad** | Alta |

---

### Actualizar asignación de rol de usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-44 |
| **Título corto** | Actualizar asignación de rol de usuario |
| **Historia** | Como Administrador, quiero modificar el rol asignado a un usuario activo, para actualizar sus permisos operativos en la plataforma sin perder la trazabilidad. |
| **Criterios de aceptación** | Antecedentes:<br>• Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma.<br>• Y que el usuario con id_usuario 10 tiene asignado el id_rol 2 ("Aprobador").<br>Escenario: CA-1 Actualización exitosa de rol asignado<br>• Cuando Carlos actualiza la asignación cambiando el id_rol 2 por el id_rol 3 ("Gestor") para el id_usuario 10.<br>• Entonces el sistema actualiza el registro en la tabla usuario_rol.<br>• Y guarda la fecha y hora actual en la fecha de asignación.<br>• Y muestra el mensaje "Asignación de rol actualizada correctamente."<br>Escenario: CA-2 Rechazo de actualización por duplicidad o rol inactivo<br>• Cuando Carlos intenta actualizar el rol a uno que el usuario ya posee o a un rol inactivo.<br>• Entonces el sistema bloquea la operación y muestra el mensaje de error correspondiente. |
| **Origen de la necesidad** | Pregunta 9 del formulario, Mantenimiento de privilegios de usuario y gestión de perfiles de acceso y el método actualizar(id_usuario, id_rol) |
| **RF derivados** | RF-44 |
| **Prioridad** | Media |

---

## Entidad tipo_solicitud

### Crear tipo de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-14 |
| **Título corto** | Crear tipo de solicitud |
| **Historia** | Como Administrador, quiero parametrizar un nuevo tipo de solicitud con código, nombre y descripción, para habilitar nuevas categorías de trámites. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Creación exitosa de tipo de solicitud<br>  # crear() en tipo_solicitud · asigna codigo_tipo único y activo = TRUE<br>  Dado que no existe ningún tipo de solicitud con código "TS-COMP"<br>  Cuando Carlos registra un tipo de solicitud con los siguientes datos:<br>    \| codigo_tipo \| TS-COMP \|<br>    \| nombre_tipo \| Solicitud de Compra de Equipos \|<br>    \| descripcion \| Adquisición de hardware y perifericos \|<br>  Entonces el sistema guarda el tipo de solicitud habilitando activo = true<br>  Y muestra el mensaje "Tipo de solicitud registrado exitosamente."<br>Escenario: CA-2 Rechazo por código de tipo duplicado<br>  # Restricción uq_tipo_codigo<br>  Dado que ya existe un tipo de solicitud registrado con el código "TS-VAC"<br>  Cuando Carlos intenta crear otro tipo de solicitud con código "TS-VAC"<br>  Entonces el sistema cancela el registro<br>  Y muestra el mensaje "El código de tipo 'TS-VAC' ya está registrado."<br>Esquema del escenario: CA-3 Rechazo por campos obligatorios faltantes<br>  When Carlos deja en blanco el campo <campo> al registrar un tipo de solicitud<br>  Then el sistema no guarda el registro<br>  And indica "<mensaje>"<br>  Ejemplos:<br>    \| campo \| mensaje \|<br>    \| codigo_tipo \| El código del tipo de solicitud es obligatorio. \|<br>    \| nombre_tipo \| Debe especificar el nombre del tipo. \| |
| **Origen de la necesidad** | Pregunta 12 del formulario y método crear() de la clase tipo_solicitud. |
| **RF derivados** | RF-14 |
| **Prioridad** | Alta |

---

### Consultar tipo de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-15 |
| **Título corto** | Consultar tipo de solicitud |
| **Historia** | Como Administrador, quiero consultar la información de un tipo de solicitud por su identificador, para conocer sus detalles y condiciones. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que la usuaria autenticada "marta.perez@nexaservicios.com" ingresa al módulo de trámites<br>Escenario: CA-1 Consulta exitosa por ID<br>  # consultar(id_tipo_solicitud)<br>  Dado que existe el id_tipo_solicitud 1 con código "TS-VAC", nombre "Solicitud de Vacaciones", descripción "Permisos de descanso" y activo = true<br>  Cuando Marta consulta la categoría con id_tipo_solicitud 1<br>  Entonces el sistema despliega la información completa de la categoría:<br>    \| id_tipo_solicitud \| 1 \|<br>    \| codigo_tipo \| TS-VAC \|<br>    \| nombre_tipo \| Solicitud de Vacaciones \|<br>    \| descripcion \| Permisos de descanso \|<br>    \| activo \| true \|<br>Escenario: CA-2 Búsqueda de identificador no existente<br>  Dado que no existe ningún registro para id_tipo_solicitud 50<br>  Cuando Marta intenta consultar el tipo de solicitud con id_tipo_solicitud 50<br>  Entonces el sistema no arroja resultados<br>  Y emite la advertencia "No se encontró ningún tipo de solicitud asociado al identificador 50." |
| **Origen de la necesidad** | Pregunta 21 del formulario y método consultar(id_tipo_solicitud) de la clase tipo_solicitud. |
| **RF derivados** | RF-15 |
| **Prioridad** | Alta |

---

### Actualizar tipo de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-16 |
| **Título corto** | Actualizar tipo de solicitud |
| **Historia** | Como Administrador, quiero actualizar el nombre o la descripción de un tipo de solicitud, para mantener clara la información a los usuarios. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>  Y que existe el tipo de solicitud id_tipo_solicitud 1 con código "TS-VAC" y nombre "Solicitud de Vacaciones"<br>Escenario: CA-1 Modificación exitosa de nombre y descripción<br>  # actualizar(id_tipo_solicitud)<br>  Cuando Carlos actualiza el nombre a "Solicitud de Vacaciones y Descansos" y la descripción a "Trámite legal de licencias" para id_tipo_solicitud 1<br>  Entonces el sistema actualiza la entidad<br>  Y muestra "Tipo de solicitud actualizado correctamente."<br>Escenario: CA-2 Rechazo por colisión de código alfanumérico al editar<br>  # Restricción de unicidad del código uq_tipo_codigo<br>  Dado que existe otro tipo de solicitud con id_tipo_solicitud 2 y código "TS-PERM"<br>  Cuando Carlos intenta modificar el código del id_tipo_solicitud 1 a "TS-PERM"<br>  Entonces el sistema cancela la edición<br>  Y muestra el mensaje "El código 'TS-PERM' ya pertenece a otro tipo de solicitud registrado."<br>  Y el tipo de solicitud 1 conserva su código "TS-VAC" |
| **Origen de la necesidad** | Pregunta 12 del formulario, Mantenimiento de catálogos y método actualizar(id_tipo_solicitud) de la clase tipo_solicitud. |
| **RF derivados** | RF-16 |
| **Prioridad** | Baja |

---

### Inactivar tipo de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-17 |
| **Título corto** | Inactivar tipo de solicitud |
| **Historia** | Como Administrador, quiero inactivar un tipo de solicitud por su identificador, para retirar la opción del formulario sin afectar el historial. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>  Y que existe el id_tipo_solicitud 1 con código "TS-VAC" en estado activo = true<br>Escenario: CA-1 Inactivación lógica exitosa<br>  # inactivar(id_tipo_solicitud) · activo = FALSE por RN-16<br>  Cuando Carlos solicita inactivar el tipo de solicitud id_tipo_solicitud 1<br>  Entonces el sistema actualiza el atributo activo a false<br>  Y muestra el mensaje "El tipo de solicitud ha sido inactivado. Ya no estará disponible para nuevos formularios."<br>Escenario: CA-2 Preservación de solicitudes asociadas previamente<br>  # Restricción ON DELETE RESTRICT (Jamás DELETE físico)<br>  Dado que el id_tipo_solicitud 1 está inactivo pero tiene 15 solicitudes históricas registradas<br>  Cuando un Solicitante intenta crear un nuevo trámite<br>  Entonces el id_tipo_solicitud 1 no aparece seleccionable en el listado<br>  Pero las 15 solicitudes previas conservan la integridad de sus datos y lecturas históricas<br>Criterio de Rechazo: Si se intenta inactivar un tipo de solicitud que actualmente se encuentra asociado a solicitudes activas en el sistema, la operación debe ser rechazada, mostrando un mensaje en pantalla que indique: "No es posible inactivar este tipo de solicitud porque existen trámites en curso asociados a él", y manteniendo el estado original sin alteraciones. |
| **Origen de la necesidad** | Pregunta 12 del formulario, Regla RN-16 y método inactivar(id_tipo_solicitud) de la clase tipo_solicitud. |
| **RF derivados** | RF-17 |
| **Prioridad** | Media |

---

## 2.1.5 Entidad estado_solicitud

### Crear estado de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-18 |
| **Título corto** | Crear estado de solicitud |
| **Historia** | Como Administrador, quiero registrar un nuevo estado definiendo su código, nombre, descripción y si es un estado terminal, para configurar la trazabilidad del proceso. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Creación exitosa de un estado de solicitud<br>  # crear() en estado_solicitud<br>  Dado que no existe ningún estado con código "EST-REV" ni nombre "En Revisión"<br>  Cuando Carlos registra un estado con los datos:<br>    \| codigo_estado \| EST-REV \|<br>    \| nombre_estado \| En Revisión \|<br>    \| descripcion \| La solicitud está en evaluación docente \|<br>    \| es_final \| false \|<br>  Entonces el sistema guarda el nuevo estado en el catálogo<br>  Y emite el mensaje "Estado de solicitud creado correctamente."<br>Escenario: CA-2 Rechazo por código o nombre duplicado<br>  # Restricciones uq_estado_codigo y uq_estado_nombre<br>  Dado que ya existe un estado con código "EST-APR" y nombre "Aprobado"<br>  Cuando Carlos intenta registrar un estado con código "EST-APR" o nombre "Aprobado"<br>  Entonces el sistema no efectúa el alta<br>  Y muestra el mensaje "Ya existe un estado registrado con ese código o nombre." |
| **Origen de la necesidad** | Pregunta 21 del formulario y método crear() de la clase estado_solicitud. |
| **RF derivados** | RF-18 |
| **Prioridad** | Media |

---

### Consultar estado de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-19 |
| **Título corto** | Consultar estado de solicitud |
| **Historia** | Como Solicitante, quiero consultar los datos descriptivos de un estado de solicitud por su identificador, para entender su significado dentro del flujo. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el usuario autenticado "marta.perez@nexaservicios.com" ingresa al seguimiento de peticiones<br>Escenario: CA-1 Consulta exitosa de la ficha del estado con bandera final<br>  # consultar(id_estado_solicitud)<br>  Dado que existe el id_estado_solicitud 3 con código "EST-FIN", nombre "Finalizado", descripción "Proceso cerrado" y es_final = true<br>  Cuando Marta consulta la información del estado con id_estado_solicitud 3<br>  Entonces el sistema presenta el detalle:<br>    \| id_estado_solicitud \| 3 \|<br>    \| codigo_estado \| EST-FIN \|<br>    \| nombre_estado \| Finalizado \|<br>    \| descripcion \| Proceso cerrado \|<br>    \| es_final \| true \|<br>Escenario: CA-2 Búsqueda de un estado no registrado<br>  Dado que no existe el id_estado_solicitud 99<br>  Cuando Marta intenta consultar el id_estado_solicitud 99<br>  Entonces el sistema muestra el error "El estado de solicitud especificado no existe." |
| **Origen de la necesidad** | Pregunta 5 del formulario y método consultar(id_estado_solicitud) de la clase estado_solicitud. |
| **RF derivados** | RF-19 |
| **Prioridad** | Alta |

---

### Actualizar estado de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-20 |
| **Título corto** | Actualizar estado de solicitud |
| **Historia** | Como Administrador, quiero modificar el nombre o descripción de un estado de solicitud por su identificador, para refinar la presentación al usuario. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Administrador "Carlos Restrepo" ha iniciado sesión en la plataforma<br>  Y que existe el id_estado_solicitud 2 con nombre "En Proceso" y es_final = false<br>Escenario: CA-1 Actualización de datos descriptivos<br>  # actualizar(id_estado_solicitud)<br>  Cuando Carlos cambia el nombre a "En Evaluación Técnica" y la descripción a "Revisión por el área encargada"<br>  Entonces el sistema guarda las modificaciones en el id_estado_solicitud 2<br>  Y muestra "Estado de solicitud actualizado correctamente."<br>Escenario: CA-2 Prohibición de alterar la bandera 'es_final' con solicitudes activas asociadas<br>  # Regla de integridad de flujo del trámite<br>  Dado que existen 8 solicitudes en tránsito asignadas al id_estado_solicitud 2 ("En Evaluación Técnica")<br>  Cuando Carlos intenta modificar la bandera es_final de false a true<br>  Entonces el sistema bloquea la actualización<br>  Y muestra el mensaje "No se puede marcar como estado final porque existen solicitudes activas vinculadas a este estado."<br>  Y el valor de es_final permanece en false |
| **Origen de la necesidad** | Pregunta 5 del formulario, Mantenimiento de catálogo de estados y método actualizar(id_estado_solicitud) de la clase estado_solicitud. |
| **RF derivados** | RF-20 |
| **Prioridad** | Baja |

## Entidad solicitud

### Crear borrador de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-21 |
| **Título corto** | Crear borrador de solicitud |
| **Historia** | Como Solicitante, quiero crear una solicitud inicial en borrador, para completar el asunto y la descripción antes de su envío formal. |
| **Criterios de aceptación** | Antecedentes:<br>  # Se cumple antes de CADA escenario de esta historia<br>  Dado que la usuaria Solicitante "Marta Pérez" con id_usuario 10 ha iniciado sesión en la plataforma<br>Escenario: CA-1 Creación exitosa de solicitud en estado borrador<br>  # crear() en Solicitud · asigna estado 'BORRADOR' y fecha_radicacion = NULL<br>  Cuando Marta crea un nuevo borrador con los siguientes datos:<br>    \| asunto \| Requerimiento de nuevo equipo portátil \|<br>    \| descripcion \| Se solicita laptop de alta gama para desarrollo \|<br>    \| id_tipo \| 1 (Solicitud de Equipos) \|<br>  Entonces el sistema registra la solicitud asignando automáticamente el id_solicitante 10<br>  Y establece el estado_solicitud en "BORRADOR"<br>  Y deja el campo fecha_radicacion en valor nulo (NULL)<br>  Y muestra el mensaje "Borrador de solicitud guardado correctamente."<br>Escenario: CA-2 Rechazo por creación de borrador con tipo de solicitud inactivo<br>  Dado que el id_tipo 4 ("Licencias de Software") está con el atributo activo = false<br>  Cuando Marta intenta guardar un borrador seleccionando el tipo de solicitud id_tipo 4<br>  Entonces el sistema impide el registro del borrador<br>  Y muestra el mensaje "El tipo de solicitud seleccionado no se encuentra activo."<br>Escenario: CA-3 Creación de borrador sin ingresar asunto ni descripción<br>  # El borrador permite campos iniciales vacíos antes del envío formal<br>  Cuando Marta crea un borrador dejando el asunto y la descripción vacíos<br>  Entonces el sistema guarda la solicitud en estado "BORRADOR"<br>  Y asigna el identificador de solicitud<br>  Y muestra el aviso "Borrador guardado sin contenido. Recuerde completarlo antes de radicar." |
| **Origen de la necesidad** | Pregunta 7 del formulario, Regla RN-16 (Restricción de selección en tipos inactivos) y método crear() de la clase Solicitud. |
| **RF derivados** | RF-21 |
| **Prioridad** | Alta |

---

### Consultar expediente de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-22 |
| **Título corto** | Consultar expediente de solicitud |
| **Historia** | Como Usuario, quiero consultar los datos de una solicitud por su identificador, para visualizar sus atributos y estado. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el usuario autenticado "Carlos Restrepo" ingresa a la consulta de expedientes<br>Escenario: CA-1 Consulta exitosa de expediente estándar<br>  # consultar(id_solicitud)<br>  Dado que existe la solicitud con id_solicitud 105, asunto "Compra de insumos", descripción "Resaltadores y carpetas", id_tipo 1, estado "PENDIENTE", fecha_radicacion "2026-03-01", anonimo_bloqueado = false y solicitante "Marta Pérez"<br>  Cuando Carlos busca la solicitud con id_solicitud 105<br>  Entonces el sistema presenta la ficha completa de la solicitud:<br>    \| id_solicitud \| 105 \|<br>    \| asunto \| Compra de insumos \|<br>    \| descripcion \| Resaltadores y carpetas\|<br>    \| tipo_solicitud \| Solicitud de Equipos \|<br>    \| estado \| PENDIENTE \|<br>    \| fecha_radicacion \| 2026-03-01 \|<br>    \| solicitante \| Marta Pérez \|<br>Escenario: CA-2 Consulta de solicitud anónima con identidad protegida<br>  # Protección de identidad por anonimo_bloqueado = TRUE<br>  Dado que existe la solicitud id_solicitud 108 con anonimo_bloqueado = true y solicitante original "Diego Rojas"<br>  Cuando Carlos consulta la solicitud id_solicitud 108<br>  Entonces el sistema despliega el asunto, descripción, tipo, estado y fechas<br>  Pero oculta la identidad del solicitante mostrando la etiqueta "SOLICITANTE ANÓNIMO"<br>Escenario: CA-3 Búsqueda de expediente inexistente<br>  Dado que no existe ninguna solicitud con id_solicitud 9999<br>  Cuando Carlos busca el id_solicitud 9999<br>  Entonces el sistema no muestra expediente<br>  Y emite la alerta "No se encontró ninguna solicitud asociada al código 9999." |
| **Origen de la necesidad** | Pregunta 14 y 21 del formulario y método consultar(id_solicitud) de la clase Solicitud. |
| **RF derivados** | RF-22 |
| **Prioridad** | Alta |

---

### Actualizar contenido de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-23 |
| **Título corto** | Actualizar contenido de solicitud |
| **Historia** | Como Solicitante, quiero actualizar el asunto o descripción de una solicitud en borrador o devuelta para ajustes, para corregir la información. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que la usuaria "Marta Pérez" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Edición exitosa de solicitud en borrador o devuelta para ajustes<br>  # actualizar(id_solicitud) · registra fecha_actualizacion<br>  Dado que Marta tiene la solicitud id_solicitud 105 en estado "BORRADOR" o "PENDIENTE_AJUSTES"<br>  Cuando modifica el asunto a "Compra de 2 Laptops de Desarrollo" y la descripción a "Ajuste de especificaciones de memoria RAM"<br>  Entonces el sistema actualiza los datos de la solicitud id_solicitud 105<br>  Y asigna la fecha y hora actual en fecha_actualizacion<br>  Y muestra el mensaje "Solicitud actualizada correctamente."<br>Escenario: CA-2 Rechazo por intento de edición en estados no permitidos<br>  # Restricción de estado para edición<br>  Dado que la solicitud id_solicitud 102 de Marta se encuentra en estado "PENDIENTE", "APROBADA" o "RECHAZADA"<br>  Cuando Marta intenta modificar el asunto o la descripción de la solicitud id_solicitud 102<br>  Entonces el sistema bloquea los campos del formulario<br>  Y muestra el aviso "La solicitud no se puede modificar porque se encuentra en trámite o cerrada." |
| **Origen de la necesidad** | Pregunta 16 del formulario y método actualizar(id_solicitud) de la clase Solicitud. |
| **RF derivados** | RF-23 |
| **Prioridad** | Alta |

---

### Radicar solicitud formalmente
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-24 |
| **Título corto** | Radicar solicitud formalmente |
| **Historia** | Como Solicitante, quiero radicar formalmente una solicitud, para iniciar el flujo institucional de revisión. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que la usuaria "Marta Pérez" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Radicación formal exitosa con información completa<br>  # radicar() · fecha_radicacion inalterable (RN-14) y cambia a estado 'PENDIENTE'<br>  Dado que Marta tiene la solicitud id_solicitud 105 en estado "BORRADOR" con asunto "Compra de Laptops" y descripción "Especificación de hardware completa"<br>  Cuando Marta presiona el botón "Radicar Solicitud"<br>  Entonces el sistema asigna la fecha y hora actual inalterable a fecha_radicacion<br>  Y cambia el estado_solicitud a "PENDIENTE"<br>  Y genera un código único de radicado institucional<br>  Y muestra el mensaje "Solicitud radicada con éxito bajo el código RAD-2026-105."<br>Escenario: CA-2 Rechazo de radicación por información incompleta<br>  Dado que la solicitud id_solicitud 106 en estado "BORRADOR" tiene el asunto "Compra" pero la descripción está vacía<br>  Cuando Marta intenta radicar la solicitud id_solicitud 106<br>  Entonces el sistema no efectúa la radicación<br>  Y mantiene el estado en "BORRADOR" y fecha_radicacion en NULL<br>  Y resalta el campo indicando "La descripción es obligatoria para poder radicar la solicitud." |
| **Origen de la necesidad** | Pregunta 21 del formulario, Regla RN-14 y método radicar() de la clase Solicitud. |
| **RF derivados** | RF-24 |
| **Prioridad** | Alta |

---

### Cambiar estado de la solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-25 |
| **Título corto** | Cambiar estado de la solicitud |
| **Historia** | Como Gerente, quiero cambiar el estado de una solicitud en el flujo, para reflejar el progreso del trámite. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que existe la solicitud id_solicitud 105 radicada en el sistema en estado "PENDIENTE"<br>Escenario: CA-1 Transición exitosa de estado con registro en bitácora de auditoría<br>  # cambiarEstado(nuevoEstado) · registro obligatorio en bitácora por RN-15<br>  Cuando el sistema invoca cambiarEstado("APROBADA") para la solicitud id_solicitud 105<br>  Entonces la solicitud id_solicitud 105 actualiza su estado a "APROBADA"<br>  Y el sistema inserta automáticamente un registro en la bitácora de auditoría detallando:<br>    \| id_solicitud \| 105 \|<br>    \| estado_previo\| PENDIENTE \|<br>    \| estado_nuevo \| APROBADA \|<br>    \| fecha_cambio \| Fecha/Hora actual \|<br>Escenario: CA-2 Error por intento de transición de estado no válida<br>  Dado que la solicitud id_solicitud 110 se encuentra en estado terminal "RECHAZADA"<br>  Cuando el sistema intenta cambiar el estado a "PENDIENTE"<br>  Entonces el sistema aborta la transacción<br>  Y emite la excepción "Transición de estado no permitida desde un estado terminal."<br>  Y el estado permanece en "RECHAZADA" sin alterar la bitácora |
| **Origen de la necesidad** | Pregunta 6 del formulario, Regla RN-15 y método cambiarEstado(nuevoEstado) de la clase Solicitud. |
| **RF derivados** | RF-25 |
| **Prioridad** | Alta |

---

### Desblindar identidad de solicitud anónima
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-26 |
| **Título corto** | Desblindar identidad de solicitud anónima |
| **Historia** | Como Administrador, quiero desblindar la identidad del solicitante anónimo mediante autorización, para resolver investigaciones de auditoría. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que existe la solicitud id_solicitud 108 con anonimo_bloqueado = true perteneciente originalmente al usuario id_usuario 12 "Diego Rojas"<br>Escenario: CA-1 Desblindaje exitoso por usuario autorizado con registro de auditoría<br>  # desblindarIdentidad(id_usuario) · Auditoría por RN-04<br>  Dado que el Gerente "Álvaro Tamayo" ha iniciado sesión con permisos de seguridad<br>  Cuando Álvaro ejecuta la función desblindarIdentidad para el id_solicitud 108<br>  Entonces el sistema muestra en pantalla la identidad del solicitante: "Diego Rojas (diego.rojas@nexaservicios.com)"<br>  Y genera inmediatamente un registro no borrable en la bitácora de auditoría indicando:<br>    \| id_solicitud \| 108 \|<br>    \| usuario_ejecutor \| Álvaro Tamayo \|<br>    \| accion \| DESBLINDAJE_IDENTIDAD\|<br>    \| fecha_desblindaje \| Fecha/Hora actual \|<br>Escenario: CA-2 Rechazo de desblindaje por falta de permisos de rol<br>  Dado que el Aprobador "Rebeca López" sin rol de Gerente o Administrador intenta desblindar la solicitud id_solicitud 108<br>  Cuando Rebeca solicita la revelación de la identidad<br>  Entonces el sistema bloquea la acción<br>  Y muestra la alerta "No cuenta con los privilegios requeridos para desblindar identidades protegidas."<br>  Y la identidad del solicitante permanece oculta |
| **Origen de la necesidad** | Pregunta 14 del formulario, Regla RN-04 y método desblindarIdentidad(id_usuario) de la clase Solicitud. |
| **RF derivados** | RF-26 |
| **Prioridad** | Media |

---

### Inactivar solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-27 |
| **Título corto** | Inactivar solicitud |
| **Historia** | Como Administrador, quiero inactivar una solicitud existente mediante su identificador, para asegurar la baja lógica del registro dentro del sistema. |
| **Criterios de aceptación** | Antecedentes:<br>• Dado que existe la solicitud con id_solicitud 108 en estado activo.<br>Escenario: CA-1 Inactivación exitosa por usuario administrador<br>• Dado que el Administrador "Carlos Restrepo" ha iniciado sesión con permisos de seguridad.<br>• Cuando Carlos ejecuta la función inactivar(id_solicitud) para el id_solicitud 108.<br>• Entonces el sistema procesa la baja lógica cambiando su estado a inactivo y devuelve un valor true.<br>• Y genera inmediatamente un registro en la bitácora de auditoría indicando la acción correspondiente.<br>Escenario: CA-2 Rechazo de inactivación por falta de permisos o registro inexistente<br>• Dado que un usuario sin rol de Administrador intenta inactivar la solicitud o el id_solicitud no se encuentra registrado.<br>• Cuando se ejecuta la función inactivar(id_solicitud).<br>• Entonces el sistema bloquea la acción, retorna false y muestra la alerta "No cuenta con los privilegios requeridos o la solicitud no existe". |
| **Origen de la necesidad** | Pregunta 15 del formulario, Requerimiento operativo del sistema y método inactivar(id_solicitud: int): boolean de la clase Solicitud. |
| **RF derivados** | RF-27 |
| **Prioridad** | Media |

## Entidad aprobacion_solicitud

### Aprobar solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-28 |
| **Título corto** | Aprobar solicitud |
| **Historia** | Como Gerente, quiero dictaminar la aprobación de una solicitud pendiente, para permitir el paso a la fase de gestión. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que la Aprobadora "Rebeca López" con id_usuario 5 ha iniciado sesión<br>  Y que existe la solicitud id_solicitud 105 radicada por "Marta Pérez" (id_usuario 10) en estado "PENDIENTE"<br>Escenario: CA-1 Aprobación exitosa por un evaluador válido<br>  # aprobar() en aprobacion_solicitud · registra 'Aprobado' y cambia estado a 'APROBADA'<br>  Cuando Rebeca dictamina la aprobación de la solicitud id_solicitud 105 con el comentario "Aprobado según presupuesto disponible"<br>  Entonces el sistema registra la decisión 'Aprobado' en la tabla aprobacion_solicitud<br>  Y actualiza la solicitud id_solicitud 105 al estado "APROBADA"<br>  Y muestra el mensaje "La solicitud ha sido aprobada exitosamente."<br>Escenario: CA-2 Rechazo de aprobación por ser el mismo solicitante<br>  # Disparador trg_validar_aprobador bloquea por RN-05<br>  Dado que el usuario "Marta Pérez" (id_usuario 10) tiene rol de Aprobador y es la solicitante de la id_solicitud 105<br>  Cuando Marta intenta dictaminar la aprobación de su propia solicitud id_solicitud 105<br>  Entonces el disparador trg_validar_aprobador aborta la operación<br>  Y el sistema muestra el mensaje de error "Conflicto de interés: El aprobador no puede ser el mismo usuario solicitante."<br>  Y la solicitud id_solicitud 105 permanece en estado "PENDIENTE" |
| **Origen de la necesidad** | Pregunta 11 del formulario, Regla RN-05 y método aprobar() de la clase aprobacion_solicitud. |
| **RF derivados** | RF-28 |
| **Prioridad** | Alta |

---

### Rechazar solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-29 |
| **Título corto** | Rechazar solicitud |
| **Historia** | Como Gerente, quiero rechazar una solicitud ingresando una justificación obligatoria, para finalizar negativamente el trámite. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que la Aprobadora "Rebeca López" ha iniciado sesión<br>  Y que existe la solicitud id_solicitud 105 en estado "PENDIENTE"<br>Escenario: CA-1 Rechazo exitoso con justificación<br>  # rechazar(comentario) · registra 'Rechazado' y pasa a estado 'RECHAZADA'<br>  Cuando Rebeca rechaza la solicitud id_solicitud 105 ingresando el comentario "No hay disponibilidad presupuestal en el periodo actual"<br>  Entonces el sistema guarda la decisión 'Rechazado' junto con la justificación<br>  Y actualiza el estado de la solicitud id_solicitud 105 a "RECHAZADA"<br>  Y notifica la decisión al solicitante<br>Escenario: CA-2 Rechazo abortado por comentario de justificación vacío<br>  # Regla chk_aprobacion_comentario (RN-06)<br>  Cuando Rebeca intenta rechazar la solicitud id_solicitud 105 dejando el campo comentario en blanco<br>  Entonces la regla chk_aprobacion_comentario detiene la operación<br>  Y el sistema muestra la advertencia "Debe ingresar una justificación obligatoria para rechazar la solicitud."<br>  Y la solicitud mantiene su estado "PENDIENTE" |
| **Origen de la necesidad** | Pregunta 11 del formulario, Regla RN-06 y método rechazar(comentario) de la clase aprobacion_solicitud. |
| **RF derivados** | RF-29 |
| **Prioridad** | Alta |

---

### Devolver solicitud para ajustes
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-30 |
| **Título corto** | Devolver solicitud para ajustes |
| **Historia** | Como Gerente, quiero devolver una solicitud al solicitante con observaciones, para que sea corregida y reenviada.[cite: 9] |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que la Aprobadora "Rebeca López" ha iniciado sesión<br>  Y que existe la solicitud id_solicitud 105 en estado "PENDIENTE"<br>Escenario: CA-1 Devolución exitosa con observaciones registradas<br>  # devolverParaAjustes(comentario) · asigna 'Devuelto_Para_Ajustes' y estado 'PENDIENTE_AJUSTES'<br>  Cuando Rebeca devuelve la solicitud id_solicitud 105 adjuntando el comentario "Por favor adjuntar tres cotizaciones de proveedores"<br>  Entonces el sistema registra la decisión 'Devuelto_Para_Ajustes' con el comentario correspondiente<br>  Y cambia el estado de la solicitud a "PENDIENTE_AJUSTES"<br>  Y habilita nuevamente los permisos de edición para la usuaria solicitante<br>Escenario: CA-2 Rechazo de devolución por omisión de observaciones<br>  # Regla chk_aprobacion_comentario (RN-06)<br>  Cuando Rebeca intenta devolver la solicitud id_solicitud 105 sin ingresar ningún comentario<br>  Entonces el sistema no efectúa la devolución<br>  Y exige el diligenciamiento del campo señalando "Es obligatorio especificar las observaciones o ajustes requeridos."<br>  Y la solicitud continúa en estado "PENDIENTE" |
| **Origen de la necesidad** | Pregunta 11 del formulario, Regla RN-06 y método devolverParaAjustes(comentario) de la clase aprobacion_solicitud. |
| **RF derivados** | RF-30 |
| **Prioridad** | Alta. |

---

### Consultar dictamen de aprobación
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-31 |
| **Título corto** | Consultar dictamen de aprobación |
| **Historia** | Como Usuario o Auditor, quiero consultar la información de una aprobación por su identificador, para revisar la decisión adoptada. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Auditor "Carlos Restrepo" ingresa a la revisión de dictámenes de solicitudes<br>Escenario: CA-1 Consulta exitosa del dictamen de evaluación<br>  # consultar(id_aprobacion)<br>  Dado que existe el registro id_aprobacion 50 con decisión "Aprobado", comentario "Cumple con los requisitos", fecha "2026-03-02 14:30:00" y aprobador "Rebeca López"<br>  Cuando Carlos consulta el dictamen con id_aprobacion 50<br>  Entonces el sistema retorna y despliega la ficha del dictamen:<br>    \| id_aprobacion \| 50 \|<br>    \| decision \| Aprobado \|<br>    \| comentario \| Cumple con los requisitos \|<br>    \| fecha_decision \| 2026-03-02 14:30:00 \|<br>    \| evaluador \| Rebeca López \|<br>Escenario: CA-2 Búsqueda de dictamen inexistente<br>  Dado que no existe ningún dictamen registrado con el id_aprobacion 999<br>  Cuando Carlos busca el id_aprobacion 999<br>  Entonces el sistema emite el mensaje "No se encontraron registros de dictamen para el identificador 999." |
| **Origen de la necesidad** | Pregunta 15 del formulario y método consultar(id_aprobacion) de la clase aprobacion_solicitud. |
| **RF derivados** | RF-31 |
| **Prioridad** | Media |

## Entidad gestion_solicitud

### Asignar gestor a la solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-32 |
| **Título corto** | Asignar gestor a la solicitud |
| **Historia** | Como Gerente, quiero asignar una solicitud a un gestor con su nivel de prioridad, para dar inicio a la atención operativa. |
| **Criterios de aceptación** | Antecedentes:<br>  # Se cumple antes de CADA escenario de esta historia<br>  Dado que el Gerente "Álvaro Tamayo" ha iniciado sesión en la plataforma<br>  Y que la solicitud id_solicitud 105 se encuentra en estado "APROBADA"<br>  Y que el gestor "Andrés Castro" con id_gestor 8 está activo en el sistema<br>Escenario: CA-1 Asignación exitosa de gestor<br>  # asignarGestor(id_gestor) · crea gestión en 'En_Proceso' y cambia solicitud a 'EN_GESTION'<br>  Dado que la solicitud id_solicitud 105 no tiene ninguna gestión activa en proceso<br>  Cuando Álvaro asigna al id_gestor 8 la atención de la id_solicitud 105 con prioridad "Alta"<br>  Entonces el sistema crea un nuevo registro en la tabla gestion_solicitud con estado_gestion = "En_Proceso"<br>  Y guarda la fecha y hora actual en fecha_vinculacion<br>  Y actualiza el estado de la solicitud id_solicitud 105 a "EN_GESTION"<br>  Y muestra el mensaje "Gestor Andrés Castro asignado correctamente a la solicitud."<br>Escenario: CA-2 Rechazo por gestión única activa (Regla RN-11)<br>  # Disparador trg_gestion_unica_activa bloquea si ya existe gestión en proceso<br>  Dado que la solicitud id_solicitud 105 ya cuenta con una gestión activa en estado "En_Proceso" asignada al id_gestor 4<br>  Cuando Álvaro intenta asignar un nuevo gestor (id_gestor 8) a la id_solicitud 105<br>  Entonces el disparador trg_gestion_unica_activa detiene la operación<br>  Y el sistema muestra el mensaje "Error: La solicitud ya posee una gestión activa en proceso."<br>  Y el registro de gestión existente no sufre modificaciones |
| **Origen de la necesidad** | Pregunta 8 del formulario, Regla RN-11 y método asignarGestor(id_gestor) de la clase gestion_solicitud. |
| **RF derivados** | RF-32 |
| **Prioridad** | Alta |

---

### Reasignar gestor a la solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-33 |
| **Título corto** | Reasignar gestor a la solicitud |
| **Historia** | Como Gerente, quiero reasignar la atención de un caso a un gestor distinto, para redistribuir la carga operacional. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Gerente "Álvaro Tamayo" ha iniciado sesión en la plataforma<br>  Y que la solicitud id_solicitud 105 tiene una gestión activa (id_gestion 12) en estado "En_Proceso" con el gestor "Andrés Castro" (id_gestor 8)<br>Escenario: CA-1 Reasignación exitosa garantizando gestión única activa (Regla RN-11)<br>  # reasignar(id_gestor) · cambia gestión actual a 'Reasignado' e inicia nuevo registro 'En_Proceso'<br>  Cuando Álvaro reasigna la id_solicitud 105 al nuevo gestor "Beatriz Gómez" (id_gestor 15)<br>  Entonces el sistema actualiza el estado_gestion del id_gestion 12 a "Reasignado"<br>  Y asigna la fecha y hora actual en fecha_cierre para id_gestion 12<br>  Y crea un nuevo registro de gestión para id_gestor 15 con estado_gestion = "En_Proceso"<br>  Y mantiene el estado de la solicitud en "EN_GESTION"<br>  Y garantiza que exista únicamente una gestión activa en estado "En_Proceso"<br>Escenario: CA-2 Rechazo de reasignación al mismo gestor actual<br>  Cuando Álvaro intenta reasignar la id_solicitud 105 al mismo gestor actual (id_gestor 8)<br>  Entonces el sistema bloquea la transacción<br>  Y muestra la advertencia "El gestor seleccionado ya se encuentra a cargo del caso." |
| **Origen de la necesidad** | Pregunta 8 del formulario, Gestión operativa y método reasignar(id_gestor) de la clase gestion_solicitud. |
| **RF derivados** | RF-33 |
| **Prioridad** | Alta |

---

### Actualizar prioridad de gestión
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-34 |
| **Título corto** | Actualizar prioridad de gestión |
| **Historia** | Como Personal de Gestión, quiero modificar la prioridad asignada a un caso ('Baja', 'Media', 'Alta', 'Critica'), para ajustar la urgencia de atención. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Gestor "Andrés Castro" ha iniciado sesión en la plataforma<br>  Y que existe un registro id_gestion 12 en estado "En_Proceso" con prioridad "Media"<br>Escenario: CA-1 Actualización exitosa a una prioridad válida<br>  # actualizarPrioridad(nuevaPrioridad)<br>  Cuando Andrés cambia la prioridad del id_gestion 12 a "Critica"<br>  Entonces el sistema actualiza el campo prioridad a "Critica" en la tabla gestion_solicitud<br>  Y muestra la confirmación "Prioridad de la gestión actualizada a Critica."<br>Escenario: CA-2 Rechazo por valor no perteneciente a la enumeración PrioridadGestion<br>  # Los valores permitidos son estrictamente: 'Baja', 'Media', 'Alta', 'Critica'<br>  Cuando Andrés intenta asignar el valor de prioridad "Urgente" al id_gestion 12<br>  Entonces el sistema rechaza el parámetro<br>  Y emite un error de validación: "La prioridad 'Urgente' no es válida. Debe seleccionar: Baja, Media, Alta o Critica."<br>  Y el campo prioridad conserva el valor "Media" |
| **Origen de la necesidad** | Pregunta 8 del formulario y método actualizarPrioridad(nuevaPrioridad: PrioridadGestion) de la clase gestion_solicitud. |
| **RF derivados** | RF-34 |
| **Prioridad** | Media |

---

### Finalizar gestión de la solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-35 |
| **Título corto** | Finalizar gestión de la solicitud |
| **Historia** | Como Personal de Gestión, quiero marcar la atención como finalizada, para concluir el trabajo operativo sobre la solicitud. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Gestor "Andrés Castro" ha iniciado sesión en la plataforma<br>  Y que la id_solicitud 105 está en "EN_GESTION" con id_gestion 12 activo en "En_Proceso" desde fecha_vinculacion "2026-03-01 08:00:00"<br>Escenario: CA-1 Cierre exitoso de gestión con cumplimiento de coherencia de fechas (Regla RN-12)<br>  # finalizar() · estado_gestion = 'Finalizado', asigna fecha_cierre y solicitud = 'SOLUCIONADO'<br>  Cuando Andrés ejecuta la acción finalizar sobre el id_gestion 12 con la fecha y hora actual ("2026-03-01 16:30:00")<br>  Entonces las restricciones chk_gestion_cierre y chk_gestion_fechas validan que fecha_cierre >= fecha_vinculacion<br>  Y el sistema actualiza el estado_gestion a "Finalizado"<br>  Y registra fecha_cierre = "2026-03-01 16:30:00"<br>  Y cambia el estado de la id_solicitud 105 a "SOLUCIONADO"<br>  Y muestra el mensaje "Gestión de la solicitud finalizada correctamente."<br>Escenario: CA-2 Rechazo por inconsistencia temporal en fecha de cierre (Regla RN-12)<br>  # Restricción chk_gestion_fechas<br>  Cuando el sistema detecta que se intenta registrar una fecha_cierre anterior a fecha_vinculacion (ej: "2026-02-28")<br>  Entonces el sistema aborta la transacción por violar chk_gestion_fechas<br>  Y muestra el error "La fecha de cierre no puede ser anterior a la fecha de vinculación del gestor."<br>  Y la gestión se mantiene en estado "En_Proceso" |
| **Origen de la necesidad** | Pregunta 18 del formulario, Regla RN-12 y método finalizar() de la clase gestion_solicitud. |
| **RF derivados** | RF-35 |
| **Prioridad** | Alta |

---

### Consultar registro de gestión
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-36 |
| **Título corto** | Consultar registro de gestión |
| **Historia** | Como Gerente, quiero consultar la información de un registro de gestión por su identificador, para revisar su asignación y tiempos. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Gerente "Álvaro Tamayo" ingresa al módulo de seguimiento de trámites<br>Escenario: CA-1 Consulta exitosa de ficha de gestión<br>  # consultar(id_gestion)<br>  Dado que existe el id_gestion 12 con prioridad "Alta", estado_gestion "Finalizado", fecha_vinculacion "2026-03-01 08:00:00" y fecha_cierre "2026-03-01 16:30:00"<br>  Cuando Álvaro consulta el registro con id_gestion 12<br>  Entonces el sistema despliega la información del registro:<br>    \| id_gestion \| 12 \|<br>    \| prioridad \| Alta \|<br>    \| estado_gestion \| Finalizado \|<br>    \| fecha_vinculacion \| 2026-03-01 08:00:00 \|<br>    \| fecha_cierre \| 2026-03-01 16:30:00 \|<br>Escenario: CA-2 Consulta de id_gestion inexistente<br>  Dado que no existe ningún registro con id_gestion 888<br>  Cuando Álvaro consulta el id_gestion 888<br>  Entonces el sistema emite el mensaje "No se encontraron registros de gestión asociadas al código 888." |
| **Origen de la necesidad** | Pregunta 8 del formulario y método consultar(id_gestion) de la clase gestion_solicitud. |
| **RF derivados** | RF-36 |
| **Prioridad** | Media |

---

## Entidad evaluacion

### Calificar servicio recibido
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-37 |
| **Título corto** | Calificar servicio recibido |
| **Historia** | Como Solicitante, quiero calificar de 1 a 5 la atención recibida e ingresar un comentario opcional, para evaluar el servicio prestado. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que la Solicitante "Marta Pérez" (id_usuario 10) ha iniciado sesión en la plataforma<br>  Y que la solicitud id_solicitud 105 de Marta finalizó su atención operativa con id_gestion 12 (estado_gestion = "Finalizado")<br>Escenario: CA-1 Evaluación exitosa por el solicitante (Reglas RN-07 y RN-13)<br>  # calificar(puntaje, comentario) en Evaluacion<br>  Dado que no existe ninguna evaluación previa para el id_gestion 12<br>  Cuando Marta asigna un puntaje de 5 y el comentario "Excelente atención y rapidez" para el id_gestion 12<br>  Entonces las reglas RN-07 (puntaje entre 1 y 5) y RN-13 (gestión finalizada) se validan como correctas<br>  Y el sistema registra la evaluación vinculada al id_gestion 12 con la fecha actual<br>  Y muestra el mensaje "Gracias por evaluar nuestro servicio."<br>Escenario: CA-2 Rechazo por intento de calificar una gestión NO finalizada (Regla RN-13)<br>  Dado que el id_gestion 14 se encuentra en estado_gestion = "En_Proceso"<br>  Cuando Marta intenta registrar una calificación para el id_gestion 14<br>  Entonces el sistema bloquea el registro por regla RN-13<br>  Y muestra la advertencia "No es posible evaluar la solicitud hasta que la gestión haya sido finalizada."<br>Escenario: CA-3 Rechazo por evaluación duplicada<br>  # Unicidad en id_gestion<br>  Dado que la gestión id_gestion 12 ya cuenta con una evaluación registrada<br>  Cuando Marta intenta enviar una segunda calificación para id_gestion 12<br>  Entonces el sistema rechaza la nueva evaluación<br>  Y muestra el mensaje "Ya se ha registrado una evaluación previa para este servicio."<br>Escenario: CA-4 Rechazo por puntaje fuera del rango permitido (Regla RN-07)<br>  Cuando Marta intenta enviar un puntaje de 6 o 0 para id_gestion 12<br>  Entonces la regla de validación RN-07 rechaza la transacción<br>  Y indica "El puntaje debe ser un número entero entre 1 y 5." |
| **Origen de la necesidad** | Pregunta 19 del formulario, Reglas RN-07 y RN-13 y método calificar(puntaje, comentario) de la clase Evaluacion. |
| **RF derivados** | RF-37 |
| **Prioridad** | Media |

---

### Consultar evaluación de servicio
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-38 |
| **Título corto** | Consultar evaluación de servicio |
| **Historia** | Como Gerente General, quiero consultar una evaluación por su identificador, para analizar la satisfacción expresada por el usuario. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Gerente General "Álvaro Tamayo" ha iniciado sesión<br>Escenario: CA-1 Consulta exitosa de evaluación registrada<br>  # consultar(id_evaluacion)<br>  Dado que existe el id_evaluacion 40 con puntaje 5, comentario "Excelente atención", fecha "2026-03-02" y id_gestion 12<br>  Cuando Álvaro consulta la evaluación con id_evaluacion 40<br>  Entonces el sistema presenta el detalle:<br>    \| id_evaluacion \| 40 \|<br>    \| puntaje \| 5 estrellas \|<br>    \| comentario \| Excelente atención \|<br>    \| fecha \| 2026-03-02 \|<br>    \| id_gestion \| 12 \|<br>Escenario: CA-2 Búsqueda de evaluación inexistente<br>  Dado que no existe el id_evaluacion 999<br>  Cuando Álvaro busca el id_evaluacion 999<br>  Entonces el sistema notifica "No se encontró ningún registro de evaluación con el identificador 999." |
| **Origen de la necesidad** | Pregunta 15 del formulario, Análisis de métricas y método consultar(id_evaluacion) de la clase Evaluacion. |
| **RF derivados** | RF-38 |
| **Prioridad** | Media |

---

## Entidad detalle_solicitud

### Crear detalle o interacción en solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-39 |
| **Título corto** | Crear detalle o interacción en solicitud |
| **Historia** | Como Solicitante, quiero publicar un mensaje o adjuntar un archivo en el historial de la solicitud, para aportar información al expediente. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Gestor "Andrés Castro" ha iniciado sesión en la solicitud id_solicitud 105<br>Escenario: CA-1 Registro exitoso de mensaje con adjunto<br>  # crear() en detalle_solicitud · registra mensaje, ruta_adjunto y fecha_registro<br>  Cuando Andrés publica el mensaje "Se adjunta cotización del proveedor B" e incluye el archivo "/adjuntos/cotizacion_b.pdf"<br>  Entonces el sistema registra el detalle asociado al id_solicitud 105<br>  Y guarda la fecha y hora actual en fecha_registro<br>  Y muestra "Interacción agregada al expediente."<br>Escenario: CA-2 Registro exitoso de mensaje sin adjunto (o solo adjunto)<br>  Cuando Andrés publica un mensaje con contenido de texto pero sin archivo adjunto (ruta_adjunto = NULL)<br>  Entonces el sistema acepta y guarda la publicación correctamente<br>Escenario: CA-3 Rechazo por interacción totalmente vacía (Regla RN-08)<br>  # Restricción chk_detalle_contenido<br>  Cuando Andrés intenta publicar una interacción dejando el mensaje en blanco Y sin adjuntar ningún archivo<br>  Entonces la regla chk_detalle_contenido detiene el envío<br>  Y el sistema muestra el error "Debe ingresar al menos un mensaje de texto o un archivo adjunto para registrar la interacción." |
| **Origen de la necesidad** | Pregunta 17 y 18 del formulario, Regla RN-08 y método crear() de la clase detalle_solicitud. |
| **RF derivados** | RF-39 |
| **Prioridad** | Alta |

---

### Consultar detalles de una solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-40 |
| **Título corto** | Consultar detalles de una solicitud |
| **Historia** | Como Solicitante, quiero consultar todos los mensajes y archivos adjuntos asociados a una solicitud por su identificador, para revisar el hilo conversacional. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que la Solicitante "Marta Pérez" ingresa a ver la bitácora conversacional de la id_solicitud 105<br>Escenario: CA-1 Consulta cronológica de interacciones existentes<br>  # consultarPorSolicitud(id_solicitud)<br>  Dado que la id_solicitud 105 tiene 2 interacciones registradas el "2026-03-01 09:00:00" y el "2026-03-01 10:15:00"<br>  Cuando Marta consulta los detalles de la id_solicitud 105<br>  Entonces el sistema despliega el listado de interacciones ordenado cronológicamente (de la más antigua a la más reciente):<br>    \| Fecha / Hora \| Usuario \| Mensaje \| Adjunto \|<br>    \| 2026-03-01 09:00:00 \| Marta Pérez \| Adjunto solicitud original \| /adjuntos/solicitud.pdf \|<br>    \| 2026-03-01 10:15:00 \| Andrés Castro \| Se adjunta cotización del proveedor B \| /adjuntos/cotizacion_b.pdf \|<br>Escenario: CA-2 Consulta de solicitud sin interacciones registradas<br>  Dado que la id_solicitud 109 es de reciente radicación y no posee notas ni adjuntos<br>  Cuando Marta consulta los detalles de la id_solicitud 109<br>  Entonces el sistema retorna una lista vacía<br>  Y presenta la leyenda "No existen mensajes o adjuntos adicionales para esta solicitud." |
| **Origen de la necesidad** | Pregunta 21 del formulario y método consultarPorSolicitud(id_solicitud) de la clase detalle_solicitud. |
| **RF derivados** | RF-40 |
| **Prioridad** | Alta |

---

## Entidad bitacora_auditoria

### Registrar acción de auditoría
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-41 |
| **Título corto** | Registrar acción de auditoría |
| **Historia** | Como Gerente, quiero registrar automáticamente cada evento relevante de la aplicación en la bitácora, para garantizar la trazabilidad inalterable. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el sistema ejecuta operaciones transaccionales sobre la base de datos<br>Escenario: CA-1 Registro exitoso de evento de cambio de estado (Regla RN-15)<br>  # registrarAccion(accion) · requiere obligatoriamente estado_nuevo si la acción es 'Cambio_Estado'<br>  Cuando se ejecuta el evento 'Cambio_Estado' sobre la entidad "Solicitud" con id_registro 105<br>  Entonces el sistema exige e inserta en Bitacora_Auditoria el campo estado_nuevo = "APROBADA"<br>  Y registra la entidad, el ID afectado, el usuario responsable y la marca de tiempo<br>Escenario: CA-2 Garantía de inalterabilidad y no eliminación de la bitácora (Regla RN-09)<br>  # Disparadores trg_bitacora_no_update y trg_bitacora_no_delete<br>  Dado que existen 500 registros almacenados en Bitacora_Auditoria<br>  Cuando un usuario o script intenta ejecutar sentencias UPDATE o DELETE sobre la tabla Bitacora_Auditoria<br>  Entonces los disparadores trg_bitacora_no_update y trg_bitacora_no_delete bloquean la sentencia<br>  Y la base de datos emite la excepción "Operación prohibida: La bitácora de auditoría es de solo lectura e inalterable (RN-09)." |
| **Origen de la necesidad** | Pregunta 4 del formulario, Reglas RN-09 y RN-15 y método registrarAccion(acción: accionAuditoria) de la clase Bitacora_Auditoria. |
| **RF derivados** | RF-41 |
| **Prioridad** | Alta |

---

### Consultar auditoría por entidad y registro
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-42 |
| **Título corto** | Consultar auditoría por entidad y registro |
| **Historia** | Como Gerente, quiero consultar las trazas de auditoría filtradas por entidad e ID de registro, para auditar el historial de una entidad específica. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Auditor "Carlos Restrepo" con privilegios de seguridad ha iniciado sesión<br>Escenario: CA-1 Consulta trazable por entidad e ID con soporte de índice<br>  # consultarPorEntidad(entidad, id_registro) · uso del índice idx_bitacora_entidad_registro<br>  Cuando Carlos consulta la bitácora filtrando por entidad = "Solicitud" e id_registro = 105<br>  Entonces el sistema utiliza el índice idx_bitacora_entidad_registro y retorna la lista cronológica de eventos de esa solicitud:<br>    \| Fecha / Hora \| Usuario \| Accion \| Estado Nuevo \|<br>    \| 2026-03-01 08:00:00 \| Marta Pérez \| Creacion \| BORRADOR \|<br>    \| 2026-03-01 08:30:00 \| Marta Pérez \| Radicacion \| PENDIENTE \|<br>    \| 2026-03-01 14:00:00 \| Rebeca López \| Aprobacion \| APROBADA \|<br>Escenario: CA-2 Denegación de acceso a usuarios sin rol Gerente o Auditor<br>  Dado que el usuario "Marta Pérez" (rol Solicitante) intenta consultar la función consultarPorEntidad<br>  Cuando Marta intenta ejecutar la consulta de auditoría<br>  entonces el sistema restringe el acceso<br>  y emite la alerta "Acceso denegado: Solo el personal de Gerencia o Auditoría puede consultar la bitácora."<br>Criterio de Rechazo: Si se produce un fallo de conexión con la base de datos o un error crítico de escritura al intentar almacenar el evento de auditoría, el sistema debe registrar el incidente en el archivo de logs del servidor y rechazar o bloquear preventivamente la transacción principal asociada para garantizar que no existan acciones del sistema sin trazabilidad. |
| **Origen de la necesidad** | Pregunta 15 del formulario y método consultarPorEntidad(entidad, id_registro) de la clase Bitacora_Auditoria. |
| **RF derivados** | RF-42 |
| **Prioridad** | Alta |

---

### Consultar auditoría por rango de fechas
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-43 |
| **Título corto** | Consultar auditoría por rango de fechas |
| **Historia** | Como Gerente, quiero consultar las trazas de auditoría ocurridas dentro de un rango de fechas, para supervisar las operaciones del sistema en un periodo. |
| **Criterios de aceptación** | Antecedentes:<br>  Dado que el Gerente "Álvaro Tamayo" ha iniciado sesión en la plataforma<br>Escenario: CA-1 Consulta exitosa por rango de fechas válido<br>  # consultarPorRango(desde, hasta)<br>  Cuando Álvaro ejecuta la consulta de auditoría especificando fecha 'desde' = "2026-03-01 00:00:00" y fecha 'hasta' = "2026-03-01 23:59:59"<br>  Entonces el sistema genera el reporte con todas las trazas de auditoría ocurridas dentro de ese rango de tiempo<br>Escenario: CA-2 Rechazo por rango de fechas invertido o inconsistente<br>  Cuando Álvaro ingresa una fecha 'desde' ("2026-03-05") que es posterior a la fecha 'hasta' ("2026-03-01")<br>  Entonces el sistema invalida el rango enviado<br>  Y muestra el mensaje de error "La fecha inicial ('desde') no puede ser posterior a la fecha final ('hasta')."<br>  Y no ejecuta la consulta en la base de datos |
| **Origen de la necesidad** | Pregunta 15 del formulario y método consultarPorRango(desde, hasta) de la clase Bitacora_Auditoria. |
| **RF derivados** | RF-43 |
| **Prioridad** | Alta |


## Exportar informe de auditoría
| Campo | Contenido |
| :--- | :--- |
| **Código** | HU-45 |
| **Título corto** | Exportar informe de auditoría |
| **Historia** | Como Gerente o Auditor, quiero exportar los registros filtrados de la bitácora de auditoría en formato CSV o PDF, para realizar análisis de seguridad y auditorías externas sin alterar los datos del sistema. |
| **Criterios de aceptación** | **Antecedentes:**<br># Se cumple antes de CADA escenario de esta historia · equivale a la precondición del CU<br>**Dado** que el auditor "Carlos Fernández" ha iniciado sesión con rol de Auditor o Gerente<br><br>**Escenario: CA-1 Exportación exitosa de informe en formato CSV o PDF**<br># `exportarInforme(formato)`<br>**Dado** que existen registros de auditoría filtrados en la interfaz de consulta<br>**Cuando** Carlos selecciona el formato "CSV" (o PDF) y hace clic en el botón "Exportar Informe"<br>**Entonces** el sistema genera y descarga el archivo comprimido o documento con los datos correspondientes, registrando la acción en la bitácora (RN-09, RN-25)<br><br>**Escenario: CA-2 Intento de exportación por usuario sin privilegios**<br>**Dado** que el usuario "Andrés Mejía" tiene el rol de Auxiliar Administrativo (sin privilegios de auditoría)<br>**Cuando** Andrés intenta acceder o ejecutar la exportación del informe de auditoría<br>**Entonces** el sistema restringe el acceso y muestra la alerta de seguridad correspondiente ("No cuenta con los privilegios requeridos para exportar informes de auditoría", RN-25) |
| **Origen de la necesidad** | Requerimiento de control y seguridad institucional para la trazabilidad y rendición de cuentas ante entes de control externos. |
| **RF derivados** | RF-45 (exportar informe de auditoría) — propuesto; se formaliza en la sección 2.2 |
| **Prioridad** | Media |
