# Requisitos No Funcionales

### Requisito no funcional RNF-01: Disponibilidad / Rendimiento
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-01[cite: 5] |
| **Categoría** | Disponibilidad / Rendimiento[cite: 5] |
| **Enunciado con medida** | La página debe estar disponible el 99.5% del tiempo (sin caerse más de 3.6 horas al mes) para que los usuarios envíen y consulten sus solicitudes en cualquier momento. Si el servidor falla, debe volver a funcionar en máximo 2 horas y recuperar la información guardada.[cite: 5] |

### Requisito no funcional RNF-02: Seguridad
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-02[cite: 5] |
| **Categoría** | Seguridad[cite: 5] |
| **Enunciado con medida** | Toda la información que viaja por la página debe usar conexión segura (HTTPS), y el 100% de las contraseñas de los usuarios se deben guardar en la base de datos de forma encriptada (con BCrypt o Argon2) para que nadie pueda verlas en texto plano.[cite: 5] |

### Requisito no funcional RNF-03: Auditoría / Registro
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-03[cite: 5] |
| **Categoría** | Auditoría / Registro[cite: 5] |
| **Enunciado con medida** | El sistema debe guardar automáticamente en el historial el 100% de los cambios de estado, aprobaciones y rechazos en menos de 1 segundo. Estos registros no se podrán modificar ni borrar por ningún usuario.[cite: 5] |

### Requisito no funcional RNF-04: Rendimiento / Rapidez
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-04[cite: 5] |
| **Categoría** | Rendimiento / Rapidez[cite: 5] |
| **Enunciado con medida** | La carga de pantallas, consultas e inicio de sesión deben responder en máximo 2 segundos aunque haya 100 usuarios conectados al mismo tiempo. La creación de reportes completos no debe tardar más de 18 segundos.[cite: 5] |

### Requisito no funcional RNF-05: Usabilidad / Diseño
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-05[cite: 5] |
| **Categoría** | Usabilidad / Diseño[cite: 5] |
| **Enunciado con medida** | La interfaz debe adaptarse fácilmente a pantallas de computadores y celulares, usando un código de 3 colores claros (Verde, Amarillo y Rojo) e iconos sencillos para identificar rápido el estado de cada solicitud.[cite: 5] |

### Requisito no funcional RNF-06: Seguridad / Archivos
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-06[cite: 5] |
| **Categoría** | Seguridad / Archivos[cite: 5] |
| **Enunciado con medida** | Al adjuntar un documento o evidencia, el sistema solo debe permitir archivos comunes (`.pdf`, `.png`, `.jpg`, `.docx`, `.xlsx`) con un tamaño máximo de 10 MB por archivo, rechazando automáticamente archivos no permitidos o muy pesados.[cite: 5] |

### Requisito no funcional RNF-07: Notificaciones
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-07[cite: 5] |
| **Categoría** | Notificaciones[cite: 5] |
| **Enunciado con medida** | El sistema debe enviar un correo automático al usuario en menos de 30 segundos cada vez que su solicitud cambie de estado, sin congelar ni hacer lenta la pantalla del usuario mientras se envía el mensaje.[cite: 5] |

### Requisito no funcional RNF-08: Estructura / Mantenimiento
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-08[cite: 5] |
| **Categoría** | Estructura / Mantenimiento[cite: 5] |
| **Enunciado con medida** | El código fuente debe cumplir con una calificación mínima del 95% o cero errores/advertencias en las herramientas de análisis estático de código, manteniendo una indentación uniforme de espacios y una longitud máxima de 50 líneas por función o método.[cite: 5] |

### Requisito no funcional RNF-09: Seguridad / Control de Acceso
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-09[cite: 5] |
| **Categoría** | Seguridad / Control de Acceso[cite: 5] |
| **Enunciado con medida** | El sistema debe cerrar automáticamente la sesión del usuario si no detecta actividad en la pantalla durante 15 minutos continuos, exigiendo ingresar nuevamente usuario y contraseña para proteger el acceso.[cite: 5] |

### Requisito no funcional RNF-10: Portabilidad / Compatibilidad
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-10[cite: 5] |
| **Categoría** | Portabilidad / Compatibilidad[cite: 5] |
| **Enunciado con medida** | La aplicación web debe cargar correctamente y mantener el 100% de sus funciones en las versiones actuales de los navegadores más utilizados (Google Chrome, Mozilla Firefox, Microsoft Edge y Safari).[cite: 5] |

### Requisito no funcional RNF-11: Copias de Seguridad
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-11[cite: 5] |
| **Categoría** | Copias de Seguridad[cite: 5] |
| **Enunciado con medida** | El sistema debe realizar una copia de seguridad (`backup`) automática de la base de datos todos los días a la medianoche, guardando las copias durante un mínimo de 30 días en un almacenamiento seguro.[cite: 5] |

### Requisito no funcional RNF-12: Usabilidad / Mensajes de Error
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-12[cite: 5] |
| **Categoría** | Usabilidad / Mensajes de Error[cite: 5] |
| **Enunciado con medida** | Ante cualquier fallo en la carga de datos o al llenar mal un formulario, el sistema debe mostrar un mensaje en pantalla en menos de 1 segundo, explicando claramente qué campo falló y cómo corregirlo en un lenguaje sencillo.[cite: 5] |

### Requisito no funcional RNF-13: Seguridad / Intentos de Acceso
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-13[cite: 5] |
| **Categoría** | Seguridad / Intentos de Acceso[cite: 5] |
| **Enunciado con medida** | El sistema debe bloquear temporalmente por 15 minutos la cuenta de cualquier usuario que intente iniciar sesión sin éxito 3 veces consecutivas, registrando el evento para evitar ataques de fuerza bruta.[cite: 5] |

### Requisito no funcional RNF-14: Escalabilidad / Almacenamiento
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-14[cite: 5] |
| **Categoría** | Escalabilidad / Almacenamiento[cite: 5] |
| **Enunciado con medida** | La base de datos debe estar diseñada para soportar un crecimiento de hasta 100,000 registros de solicitudes al año sin degradar el tiempo de consulta general en más de un 10%.[cite: 5] |

### Requisito no funcional RNF-15: Mantenibilidad / Registros del Sistema (Logs)
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-15[cite: 5] |
| **Categoría** | Mantenibilidad / Registros del Sistema (Logs)[cite: 5] |
| **Enunciado con medida** | El sistema debe generar archivos de registro (`logs`) diarios de errores técnicos e interacciones del backend, conservándolos organizados durante 90 días para facilitar el diagnóstico de fallos por parte del equipo informático.[cite: 5] |

### Requisito no funcional RNF-16: Concurrencia / Control de Cambios
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-16[cite: 5] |
| **Categoría** | Concurrencia / Control de Cambios[cite: 5] |
| **Enunciado con medida** | Si dos o más usuarios intentan actualizar o cambiar el estado de la misma solicitud al mismo tiempo, el sistema debe procesar las peticiones en orden de llegada sin permitir sobreescrituras conflictivas o pérdida de datos.[cite: 5] |

### Requisito no funcional RNF-17: Portabilidad / Visualización e Impresión
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-17[cite: 5] |
| **Categoría** | Portabilidad / Visualización e Impresión[cite: 5] |
| **Enunciado con medida** | Los documentos y reportes exportados en formato PDF por el sistema deben mantener un diseño estandarizado y legible, ajustándose automáticamente al tamaño de hoja Carta/A4 sin cortes de texto o imágenes.[cite: 5] |

### Requisito no funcional RNF-18: Usabilidad / Facilidad de Aprendizaje
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-18[cite: 5] |
| **Categoría** | Usabilidad / Facilidad de Aprendizaje[cite: 5] |
| **Enunciado con medida** | Un usuario nuevo con conocimientos básicos de oficina debe ser capaz de radicar una solicitud completa en menos de 3 minutos durante su primer uso del sistema sin requerir asistencia técnica.[cite: 5] |

### Requisito no funcional RNF-19: Seguridad / Privacidad de Sesión
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-19[cite: 5] |
| **Categoría** | Seguridad / Privacidad de Sesión[cite: 5] |
| **Enunciado con medida** | El sistema no debe permitir la apertura de múltiples sesiones simultáneas con el mismo usuario en diferentes navegadores o dispositivos, cerrando automáticamente la sesión anterior si se detecta un nuevo inicio.[cite: 5] |

### Requisito no funcional RNF-20: Despliegue / Eficiencia de Peso Web
| Campo | Contenido |
| :--- | :--- |
| **Código** | RNF-20[cite: 5] |
| **Categoría** | Despliegue / Eficiencia de Peso Web[cite: 5] |
| **Enunciado con medida** | La carga inicial de la página principal (HTML, CSS y scripts) no debe superar un tamaño total de 7 MB para garantizar un acceso ágil incluso desde conexiones de red lentas.[cite: 5] |
