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
