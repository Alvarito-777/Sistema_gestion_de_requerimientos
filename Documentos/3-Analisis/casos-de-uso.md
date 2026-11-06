# Diagrama y Especificación de Casos de Uso Críticos

<img width="1000" height="690" alt="image" src="https://github.com/user-attachments/assets/a9194526-2517-4515-8bf6-6f1c141ec77d" />


## Casos de uso críticos documentados y justificación de la selección

### Casos de uso críticos seleccionados

| Código | Caso de uso | Actor principal | HU | RF | RN que hace cumplir |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **CU-24** | Radicar solicitud formalmente | Solicitante | HU-24 | RF-24 | RN-14, RN-15, RN-16 |
| **CU-27** | Aprobar solicitud | Aprobador / Gerente | HU-28 (con HU-29 y HU-30 como alternativos) | RF-28 (RF-29, RF-30) | RN-05, RN-06, RN-15 |
| **CU-33** | Asignar gestor a la solicitud | Gerente | HU-32 | RF-32 | RN-11, RN-15, RN-27 |
| **CU-36** | Finalizar gestión de la solicitud | Gestor / Personal de Gestión | HU-35 | RF-35 | RN-12, RN-15 |

---

## CU-24: Radicar solicitud formalmente

<img width="774" height="690" alt="image" src="https://github.com/user-attachments/assets/266f4d7e-83df-472a-9eb1-1f201297a8d0" />

### Especificación del caso de uso CU-24 Radicar solicitud formalmente

| Elemento | Descripción / Valor | Procedencia |
| :--- | :--- | :--- |
| **Caso de Uso** | `CU-24` Radicar solicitud formalmente | — |
| **Actor** | Solicitante | El rol de la HU-24 |
| **Precondición** | El solicitante ha iniciado sesión y tiene una solicitud propia en estado `BORRADOR`. | Antecedentes de la HU-24 |
| **Flujo básico · Paso 1** | 1. El solicitante selecciona su solicitud en `BORRADOR` y presiona «Radicar Solicitud». / El sistema recibe la orden de radicación. | El «Cuando» del CA-1 |
| **Flujo básico · Paso 2** | 2. — / El sistema verifica que la información obligatoria (asunto y descripción) esté completa. | Prepara la validación que exige el CA-2 de rechazo |
| **Flujo básico · Paso 3** | 3. — / El sistema verifica que el tipo de solicitud elegido esté activo («include» Validar tipo de solicitud activo, RN-16). | Prepara la validación de RN-16 (catálogo de tipos) |
| **Flujo básico · Paso 4** | 4. — / El sistema asigna la fecha y hora actuales a `fecha_radicacion`, que queda inalterable (RN-14). | ES el CA-1 (RN-14) |
| **Flujo básico · Paso 5** | 5. — / El sistema cambia el estado de la solicitud a `PENDIENTE` («include» Cambiar estado de solicitud) y registra en la bitácora el estado previo, el nuevo y el usuario responsable (RN-15). | ES el CA-1 (RN-15) |
| **Flujo básico · Paso 6** | 6. — / El sistema genera un código único de radicado institucional. | ES el CA-1 |
| **Flujo básico · Paso 7** | 7. — / El sistema informa «Solicitud radicada con éxito bajo el código RAD-2026-105.» | ES el CA-1 hecho paso final (RF-24) |
| **Flujo alternativo 2a** | 2a. Falta información obligatoria (por ejemplo, la descripción está vacía): el sistema no radica, mantiene el estado `BORRADOR` y `fecha_radicacion` en `NULL`, y resalta el campo con el mensaje «La descripción es obligatoria para poder radicar la solicitud.» Vuelve al paso 1. | ES el CA-2 de la HU-24 |
| **Flujo alternativo 3a** | 3a. El tipo de solicitud está inactivo (`activo = false`): el sistema no radica, mantiene el estado `BORRADOR` y pide seleccionar un tipo activo. Vuelve al paso 1. (Valida la RN-16) | RN-16 (HU-21 CA-2) |
| **Poscondición** | La solicitud queda radicada, con fecha de radicación inalterable, estado `PENDIENTE` y código de radicado, y la transición queda registrada en la bitácora. Queda disponible para su evaluación (`CU-27`). Si la radicación se rechaza, la solicitud sigue en `BORRADOR` sin fecha de radicación. | CA-1 y CA-2 de la HU-24, RN-14 y RN-15 |

* **Justificación:** Es la puerta de entrada y reemplaza el WhatsApp y el correo, que son el problema original. Sella la fecha de radicación inalterable (RN-14). Si falla, ninguna solicitud entra al flujo formal.

---

## CU-27: Aprobar solicitud

<img width="780" height="500" alt="image" src="https://github.com/user-attachments/assets/4676cbb4-71c0-4d94-9869-cc41c845dbbb" />


### Especificación del caso de uso CU-27 Aprobar solicitud

| Elemento | Descripción / Valor | Procedencia |
| :--- | :--- | :--- |
| **Caso de Uso** | `CU-27` Aprobar solicitud | — |
| **Actor** | Gerente (el Gerente hereda las funciones del Aprobador) | El rol de la HU-28 |
| **Precondición** | El aprobador ha iniciado sesión con rol Aprobador o Gerente y existe una solicitud en estado `PENDIENTE` radicada por otro usuario. | Antecedentes de la HU-28 y RN-05 |
| **Flujo básico · Paso 1** | 1. El aprobador consulta las solicitudes `PENDIENTES` y selecciona una. / El sistema presenta la información de la solicitud. | Antecedentes de la HU-28 |
| **Flujo básico · Paso 2** | 2. El aprobador selecciona la opción Aprobar e ingresa un comentario. / El sistema recibe el dictamen. | El «Cuando» del CA-1 |
| **Flujo básico · Paso 3** | 3. — / El sistema verifica que el aprobador no sea el mismo usuario que radicó la solicitud («include» Validar conflicto de interés, RN-05). | Prepara la validación que exige el CA-2 de rechazo |
| **Flujo básico · Paso 4** | 4. — / El sistema registra la decisión «Aprobado» con su comentario y fecha en `aprobacion_solicitud`. | ES el CA-1 |
| **Flujo básico · Paso 5** | 5. — / El sistema cambia el estado de la solicitud a `APROBADA` y registra la transición en la bitácora (RN-15). | ES el CA-1 (RN-15) |
| **Flujo básico · Paso 6** | 6. — / El sistema informa «La solicitud ha sido aprobada exitosamente.» | ES el CA-1 hecho paso final (RF-28) |
| **Flujo alternativo 2a** | 2a. El aprobador elige Rechazar en lugar de Aprobar e ingresa una justificación: tras validar el paso 3, el sistema registra la decisión «Rechazado» con la justificación, cambia el estado a `RECHAZADA` y notifica al solicitante. Fin del caso de uso. | CA-1 de la HU-29 (RF-29) |
| **Flujo alternativo 2b** | 2b. El aprobador elige Devolver para ajustes e ingresa observaciones: tras validar el paso 3, el sistema registra la decisión «Devuelto_Para_Ajustes», cambia el estado a `PENDIENTE_AJUSTES` y habilita de nuevo la edición para el solicitante. Fin del caso de uso. | CA-1 de la HU-30 (RF-30) |
| **Flujo alternativo 2c** | 2c. El aprobador intenta rechazar o devolver sin comentario: el sistema no registra la decisión, exige la justificación u observaciones y la solicitud permanece `PENDIENTE`. Vuelve al paso 2. (Valida la RN-06) | ES el CA-2 de la HU-29 y el CA-2 de la HU-30 (RN-06) |
| **Flujo alternativo 3a** | 3a. El aprobador es el mismo usuario solicitante: el disparador `trg_validar_aprobador` aborta la operación, el sistema muestra «Conflicto de interés: El aprobador no puede ser el mismo usuario solicitante.» y la solicitud permanece `PENDIENTE`. Fin del caso de uso. (Valida la RN-05) | ES el CA-2 de la HU-28 (RN-05) |
| **Poscondición** | La decisión queda registrada. En el flujo básico, la solicitud pasa a `APROBADA` y queda disponible para asignarle un gestor (`CU-33`). En los flujos alternativos, la solicitud queda `RECHAZADA` o `PENDIENTE_AJUSTES`, o sigue `PENDIENTE` si el dictamen se bloquea. | CA-1 de la HU-28, HU-29 y HU-30, RN-05, RN-06 y RN-15 |

* **Justificación:** Es el punto de control. Protege contra la autoaprobación (RN-05) y exige justificación al rechazar o devolver (RN-06). Sin eso, cualquiera podría aprobar sus propias solicitudes.

---

## CU-33: Asignar gestor a la solicitud

<img width="683" height="690" alt="image" src="https://github.com/user-attachments/assets/e9854d21-f82e-4fa5-8de7-0e946ae83ea3" />


### Especificación del caso de uso CU-33 Asignar gestor a la solicitud

| Elemento | Descripción / Valor | Procedencia |
| :--- | :--- | :--- |
| **Caso de Uso** | `CU-33` Asignar gestor a la solicitud | — |
| **Actor** | Gerente | El rol de la HU-32 |
| **Precondición** | El gerente ha iniciado sesión, la solicitud está en estado `APROBADA` y existe al menos un gestor activo en el sistema. | Antecedentes de la HU-32 |
| **Flujo básico · Paso 1** | 1. El gerente consulta las solicitudes `APROBADAS` y selecciona una. / El sistema presenta la solicitud y los gestores activos disponibles. | Antecedentes de la HU-32 |
| **Flujo básico · Paso 2** | 2. El gerente selecciona un gestor y define el nivel de prioridad (Baja, Media, Alta o Crítica). / El sistema recibe la asignación. | El «Cuando» del CA-1 |
| **Flujo básico · Paso 3** | 3. — / El sistema verifica que la solicitud no tenga una gestión activa en estado `En_Proceso` («include» Validar gestión única activa, RN-11). | Prepara la validación que exige el CA-2 de rechazo |
| **Flujo básico · Paso 4** | 4. — / El sistema crea el registro en `gestion_solicitud` con `estado_gestion` `En_Proceso` y guarda la fecha y hora actuales en `fecha_vinculacion`. | ES el CA-1 |
| **Flujo básico · Paso 5** | 5. — / El sistema cambia el estado de la solicitud a `EN_GESTION` y registra la transición en la bitácora (RN-15). | ES el CA-1 (RN-15) |
| **Flujo básico · Paso 6** | 6. — / El sistema informa «Gestor [nombre] asignado correctamente a la solicitud.» | ES el CA-1 hecho paso final (RF-32) |
| **Flujo alternativo 3a** | 3a. La solicitud ya tiene una gestión `En_Proceso`: el disparador `trg_gestion_unica_activa` detiene la operación, el sistema muestra «Error: La solicitud ya posee una gestión activa en proceso.» y la gestión existente no se modifica. Para cambiar de gestor debe usarse la reasignación (`HU-33`). Fin del caso de uso. (Valida la RN-11) | ES el CA-2 de la HU-32 (RN-11) |
| **Poscondición** | La solicitud queda asignada a un gestor, con su prioridad, una única gestión activa en estado `En_Proceso`, fecha de vinculación y estado `EN_GESTION`. | CA-1 de la HU-32, RN-11 y RN-15 |

* **Justificación:** Es el puente entre aprobar y ejecutar. Garantiza una sola gestión activa por solicitud (RN-11), así no hay doble atención ni responsabilidad difusa.

---

## CU-36: Finalizar gestión de la solicitud

<img width="703" height="690" alt="image" src="https://github.com/user-attachments/assets/3a3fecda-b6ee-4417-8fc7-fe08d9c818f8" />


### Especificación del caso de uso CU-36 Finalizar gestión de la solicitud

| Elemento | Descripción / Valor | Procedencia |
| :--- | :--- | :--- |
| **Caso de Uso** | `CU-36` Finalizar gestión de la solicitud | — |
| **Actor** | Gestor / Personal de Gestión | El rol de la HU-35 |
| **Precondición** | El gestor ha iniciado sesión, la solicitud está en estado `EN_GESTION` y existe una gestión a su cargo en estado `En_Proceso`. | Antecedentes de la HU-35 |
| **Flujo básico · Paso 1** | 1. El gestor consulta sus solicitudes asignadas y selecciona la gestión que desea cerrar. / El sistema presenta la información de la gestión. | Antecedentes de la HU-35 |
| **Flujo básico · Paso 2** | 2. El gestor ejecuta la acción Finalizar. / El sistema recibe la orden y toma la fecha y hora actuales como fecha de cierre. | El «Cuando» del CA-1 |
| **Flujo básico · Paso 3** | 3. — / El sistema verifica que `fecha_cierre` sea igual o posterior a `fecha_vinculacion` («include» Validar fecha de cierre, RN-12; restricciones `chk_gestion_cierre` y `chk_gestion_fechas`). | Prepara la validación que exige el CA-2 de rechazo |
| **Flujo básico · Paso 4** | 4. — / El sistema cambia el estado de la gestión a `Finalizado` y registra la `fecha_cierre`. | ES el CA-1 |
| **Flujo básico · Paso 5** | 5. — / El sistema cambia el estado de la solicitud a `SOLUCIONADO` y registra la transición en la bitácora (RN-15). | ES el CA-1 (RN-15) |
| **Flujo básico · Paso 6** | 6. — / El sistema informa «Gestión de la solicitud finalizada correctamente.» | ES el CA-1 hecho paso final (RF-35) |
| **Flujo alternativo 3a** | 3a. La fecha de cierre es anterior a la fecha de vinculación: la restricción `chk_gestion_fechas` aborta la transacción, el sistema muestra «La fecha de cierre no puede ser anterior a la fecha de vinculación del gestor.» y la gestión se mantiene `En_Proceso`. (Valida la RN-12) | ES el CA-2 de la HU-35 (RN-12) |
| **Poscondición** | La gestión queda en estado `Finalizado` con `fecha_cierre` registrada, la solicitud pasa a `SOLUCIONADO` (estado terminal) y la transición queda registrada en la bitácora. Queda habilitada la evaluación del servicio (RN-13). Si el cierre se rechaza, la gestión sigue `En_Proceso`. | CA-1 y CA-2 de la HU-35, RN-12, RN-13 y RN-15 |

* **Justificación:** Cierra el ciclo y habilita la calificación del servicio (RN-13). Valida que la fecha de cierre no sea anterior a la de vinculación (RN-12), lo que mantiene confiables los tiempos de atención y los reportes.
