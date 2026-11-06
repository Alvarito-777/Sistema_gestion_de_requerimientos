# Requisitos Funcionales

## Entidad: Rol

### Requisito funcional RF-01: Registrar nuevo rol de usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-01 |
| **Nombre corto** | Registrar nuevo rol de usuario |
| **Descripción** | El sistema debe permitir al Administrador registrar un nuevo rol pidiendo el nombre, la descripción y si tiene permisos de administración. Además, debe verificar que el nombre no esté repetido y que sea uno de los permitidos por el sistema. |
| **HU de origen** | HU-01 |
| **RN que hace cumplir** | RN-03 (Dominio de perfiles autorizados) |
| **Prioridad** | Alta |

### Requisito funcional RF-02: Consultar roles del sistema
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-02 |
| **Nombre corto** | Consultar roles del sistema |
| **Descripción** | El sistema debe permitir consultar la lista general de todos los roles registrados o buscar un rol específico por su código de identificación para ver su información detallada. |
| **HU de origen** | HU-02 |
| **RN que hace cumplir** | Ninguna (Consulta general del catálogo) |
| **Prioridad** | Media |

### Requisito funcional RF-03: Actualizar información de un rol
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-03 |
| **Nombre corto** | Actualizar información de un rol |
| **Descripción** | El sistema debe permitir al Administrador modificar la descripción o los permisos de un rol ya existente, asegurándose de que los campos obligatorios no queden vacíos y que no se repita con el nombre de otro rol. |
| **HU de origen** | HU-03 |
| **RN que hace cumplir** | RN-03 (Dominio de perfiles autorizados) |
| **Prioridad** | Media |

### Requisito funcional RF-04: Inactivar rol del sistema
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-04 |
| **Nombre corto** | Inactivar rol del sistema |
| **Descripción** | El sistema debe permitir desactivar un rol del catálogo de forma lógica tras una confirmación. El sistema debe bloquear la acción y avisar si el rol tiene usuarios activos asignados para proteger la integridad de los datos. |
| **HU de origen** | HU-04 |
| **RN que hace cumplir** | RN-10 (Integridad de eliminación) |
| **Prioridad** | Baja |

---

## Entidad: Usuario

### Requisito funcional RF-05: Registrar usuario en la plataforma
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-05 |
| **Nombre corto** | Registrar usuario en la plataforma |
| **Descripción** | El sistema debe permitir al Administrador registrar un nuevo usuario pidiendo su correo corporativo y contraseña, asignándole automáticamente un estado activo y cero intentos fallidos. Además, debe validar que el correo pertenezca obligatoriamente al dominio autorizado y que no se encuentre duplicado. |
| **HU de origen** | HU-05 |
| **RN que hace cumplir** | RN-01 (Dominio de correo corporativo) |
| **Prioridad** | Alta |

### Requisito funcional RF-06: Consultar expediente de usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-06 |
| **Nombre corto** | Consultar expediente de usuario |
| **Descripción** | El sistema debe permitir consultar la información completa de un usuario específico buscando por su código de identificación, mostrando su correo, estado de cuenta, intentos fallidos y fecha de bloqueo en caso de tenerla. |
| **HU de origen** | HU-06 |
| **RN que hace cumplir** | Ninguna (Control y auditoría de cuentas) |
| **Prioridad** | Media |

### Requisito funcional RF-07: Actualizar datos de usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-07 |
| **Nombre corto** | Actualizar datos de usuario |
| **Descripción** | El sistema debe permitir al Administrador modificar la contraseña o los datos de un usuario existente. Si el estado de la cuenta cambia a suspendido, el sistema debe registrar automáticamente la fecha y hora actual del bloqueo. |
| **HU de origen** | HU-07 |
| **RN que hace cumplir** | RN-01 (Dominio de correo corporativo); RN-02 (Bloqueo por intentos fallidos) |
| **Prioridad** | Alta |

### Requisito funcional RF-08: Inactivar cuenta de usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-08 |
| **Nombre corto** | Inactivar cuenta de usuario |
| **Descripción** | El sistema debe permitir desactivar la cuenta de un usuario de forma lógica previa confirmación del Administrador, bloqueando su inicio de sesión pero manteniendo intactos sus registros históricos y relaciones en la base de datos. |
| **HU de origen** | HU-08 |
| **RN que hace cumplir** | RN-10 (Integridad de eliminación) |
| **Prioridad** | Alta |

### Requisito funcional RF-09: Registrar intento fallido de autenticación
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-09 |
| **Nombre corto** | Registrar intento fallido de autenticación |
| **Descripción** | El sistema debe incrementar el contador de intentos fallidos cada vez que se ingrese una contraseña incorrecta. Si se alcanza el límite máximo permitido, la cuenta debe suspenderse automáticamente registrando la fecha y hora del bloqueo. |
| **HU de origen** | HU-09 |
| **RN que hace cumplir** | RN-02 (Bloqueo por intentos fallidos) |
| **Prioridad** | Alta |

### Requisito funcional RF-10: Reiniciar intentos fallidos de autenticación
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-10 |
| **Nombre corto** | Reiniciar intentos fallidos de autenticación |
| **Descripción** | El sistema debe restablecer a cero el contador de intentos fallidos de forma automática tras un inicio de sesión exitoso, o de manera manual cuando un Administrador desbloquea y reactiva la cuenta limpiando su fecha de bloqueo. |
| **HU de origen** | HU-10 |
| **RN que hace cumplir** | RN-02 (Bloqueo por intentos fallidos) |
| **Prioridad** | Media |

---

## Entidad: usuario_rol

### Requisito funcional RF-11: Asignar rol a usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-11 |
| **Nombre corto** | Asignar rol a usuario |
| **Descripción** | El sistema debe permitir al Administrador asociar un rol específico a un usuario activo mediante sus identificadores, registrando automáticamente la fecha y hora de la asignación. Además, debe validar que el usuario no tenga el rol repetido y que la cuenta del usuario se encuentre activa. |
| **HU de origen** | HU-11 |
| **RN que hace cumplir** | RN-17 (Validación de unicidad y estado para asignación de rol) |
| **Prioridad** | Alta |

### Requisito funcional RF-12: Consultar asignación de rol de un usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-12 |
| **Nombre corto** | Consultar asignación de rol de un usuario |
| **Descripción** | El sistema debe permitir al Administrador verificar la relación específica entre un usuario y un rol utilizando sus identificadores, mostrando los detalles completos del vínculo y la fecha en que fue asignado. |
| **HU de origen** | HU-12 |
| **RN que hace cumplir** | Ninguna (Consulta y control de asignaciones) |
| **Prioridad** | Media |

### Requisito funcional RF-13: Revocar rol asignado a usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-13 |
| **Nombre corto** | Revocar rol asignado a usuario |
| **Descripción** | El sistema debe permitir al Administrador desvincular un rol específico de un usuario mediante sus identificadores para retirar sus permisos. El sistema debe validar obligatoriamente que el usuario conserve al menos un rol asignado en la plataforma antes de permitir la eliminación del vínculo. |
| **HU de origen** | HU-13 |
| **RN que hace cumplir** | RN-18 (Mantenimiento de rol mínimo por usuario) |
| **Prioridad** | Alta |

### Requisito funcional RF-44: Actualizar asignación de rol de usuario
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-44 |
| **Nombre corto** | Actualizar asignación de rol de usuario |
| **Descripción** | El sistema debe permitir al Administrador modificar el rol asociado a un usuario existente, validando que el nuevo rol se encuentre activo y que no genere duplicidad en los permisos del usuario dentro de la plataforma. |
| **HU de origen** | HU-44 |
| **RN que hace cumplir** | RN-17 (Validación de unicidad y estado para asignación de rol) |
| **Prioridad** | Media |

---

## Entidad: tipo_solicitud

### Requisito funcional RF-14: Crear tipo de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-14 |
| **Nombre corto** | Crear tipo de solicitud |
| **Descripción** | El sistema debe permitir al Administrador registrar una nueva categoría o tipo de solicitud ingresando su código único, nombre y descripción, habilitándolo de forma automática con un estado activo. Además, debe validar que el código no se encuentre duplicado y que no falten campos obligatorios. |
| **HU de origen** | HU-14 |
| **RN que hace cumplir** | RN-21 (Unicidad del código de tipo de solicitud) |
| **Prioridad** | Alta |

### Requisito funcional RF-15: Consultar tipo de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-15 |
| **Nombre corto** | Consultar tipo de solicitud |
| **Descripción** | El sistema debe permitir consultar la información completa de un tipo de solicitud específico buscando por su identificador único, mostrando su código, nombre, descripción y estado actual (activo o inactivo). |
| **HU de origen** | HU-15 |
| **RN que hace cumplir** | Ninguna (Consulta general de catálogo) |
| **Prioridad** | Alta |

### Requisito funcional RF-16: Actualizar tipo de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-16 |
| **Nombre corto** | Actualizar tipo de solicitud |
| **Descripción** | El sistema debe permitir al Administrador modificar el nombre o la descripción de un tipo de solicitud existente. Asimismo, debe validar que si se modifica el código alfanumérico, este no colisione ni se duplique con otro registro previo. |
| **HU de origen** | HU-16 |
| **RN que hace cumplir** | RN-21 (Unicidad del código de tipo de solicitud) |
| **Prioridad** | Baja |

### Requisito funcional RF-17: Inactivar tipo de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-17 |
| **Nombre corto** | Inactivar tipo de solicitud |
| **Descripción** | El sistema debe permitir al Administrador inactivar de forma lógica un tipo de solicitud cambiando su atributo a falso, retirándolo de los formularios disponibles para nuevos trámites sin afectar ni eliminar los registros históricos previos. |
| **HU de origen** | HU-17 |
| **RN que hace cumplir** | RN-16 (Inactivación lógica de catálogos) |
| **Prioridad** | Media |

---

## Entidad: estado_solicitud

### Requisito funcional RF-18: Crear estado de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-18 |
| **Nombre corto** | Crear estado de solicitud |
| **Descripción** | El sistema debe permitir al Administrador registrar un nuevo estado de solicitud especificando su código único, nombre, descripción y si corresponde a un estado final, validando que no existan duplicados en el código o en el nombre. |
| **HU de origen** | HU-18 |
| **RN que hace cumplir** | RN-22 (Unicidad de código y nombre de estados) |
| **Prioridad** | Media |

### Requisito funcional RF-19: Consultar estado de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-19 |
| **Nombre corto** | Consultar estado de solicitud |
| **Descripción** | El sistema debe permitir a los usuarios consultar los datos descriptivos y la ficha de un estado de solicitud específico mediante su identificador único, mostrando su código, nombre, descripción y si es un estado final. |
| **HU de origen** | HU-19 |
| **RN que hace cumplir** | Ninguna (Consulta general de catálogo) |
| **Prioridad** | Alta |

### Requisito funcional RF-20: Actualizar estado de solicitud
| Campo | Contenido |
| :--- | :--- |
| **Código** | RF-20 |
| **Nombre corto** | Actualizar estado de solicitud |
| **Descripción** | El sistema debe permitir al Administrador modificar el nombre o la descripción de un estado de solicitud existente. Además, debe bloquear la alteración de la bandera de estado final (es_final) si existen solicitudes activas vinculadas a dicho estado. |
| **HU de origen** | HU-20 |
| **RN que hace cumplir** | RN-23 (Restricción de alteración de estado final) |
| **Prioridad** | Baja |

