Campo | Descripción
--------|-------------
ID | RNF 01
Categoría | Rendimiento
Descripción | El sistema debe procesar y mostrar la actualización del estado de una solicitud tras la acción de Gerencia. La interfaz debe soportar hasta 150 usuarios concurrentes realizando consultas en tiempo real sin degradar la velocidad del servidor.
Métrica | Las consultas generales e informes administrativos deben cargar en menos de 2 segundos.

Campo | Descripción
--------|-------------
ID | RNF 02
Categoría | Disponibilidad
Descripción | El sistema debe estar operativo, estable y accesible durante la jornada laboral oficial (lunes a viernes 7:00 a.m. – 6:00 p.m., sábados 8:00 a.m. – 12:00 m). Los mantenimientos programados se realizarán los domingos por la noche con aviso previo de 48 horas.
Métrica | 99.5% de disponibilidad durante el horario laboral.

Campo | Descripción
--------|-------------
ID | RNF 03
Categoría | Seguridad
Descripción | El sistema debe garantizar que los registros de solicitudes finalizadas permanezcan protegidos contra eliminación o modificación. Se aplicará cifrado AES 256 para datos en reposo y HTTPS (TLS 1.3) para datos en tránsito, cumpliendo la Ley 1581 de 2012.
Métrica | 100% de inmutabilidad en datos históricos.

Campo | Descripción
--------|-------------
ID | RNF 04
Categoría | Usabilidad
Descripción | El sistema debe permitir que un empleado nuevo complete y radique su primera solicitud sin asistencia técnica. La interfaz debe cumplir con WCAG 2.1 nivel AA para accesibilidad.
Métrica | Tiempo de aprendizaje menor a 5 minutos.

Campo | Descripción
--------|-------------
ID | RNF 05
Categoría | Compatibilidad
Descripción | El sistema debe adaptar su interfaz para funcionar correctamente en navegadores móviles, con diseño responsivo desde 360px de ancho en Chrome, Firefox, Edge y Safari.
Métrica | 100% de compatibilidad con vistas responsivas.

Campo | Descripción
--------|-------------
ID | RNF 06
Categoría | Rendimiento
Descripción | El sistema debe generar y permitir la descarga del comprobante PDF inmediatamente después de hacer clic en el botón de descarga. Cada archivo PDF no debe superar los 2 MB.
Métrica | Generación y descarga en menos de 3 segundos.

Campo | Descripción
--------|-------------
ID | RNF 07
Categoría | Seguridad
Descripción | El sistema debe garantizar que la información confidencial de cada solicitud solo sea accesible para su autor y los roles autorizados según la matriz de permisos. Cualquier intento de acceso no autorizado debe ser bloqueado y registrado en el log de auditoría.
Métrica | 0 accesos no autorizados registrados en auditoría durante la operación normal.

Campo | Descripción
--------|-------------
ID | RNF 08
Categoría | Auditoría / Legal
Descripción | Todos los logs de eventos, ingresos, intentos fallidos y modificaciones críticas deben almacenarse íntegros para cumplir normativas de auditoría en Colombia.
Métrica | Conservación del 100% de los logs por mínimo 5 años.

Campo | Descripción
--------|-------------
ID | RNF 09
Categoría | Respaldos
Descripción | El sistema debe realizar copias de seguridad automáticas diariamente a las 11:00 p.m., almacenándolas en un servidor en la nube independiente durante 6 meses.
Métrica | Margen de pérdida de datos máximo de 24 horas.

Campo | Descripción
--------|-------------
ID | RNF 10
Categoría | Escalabilidad
Descripción | La arquitectura del backend debe ser modular y permitir crecimiento sin modificar el código base, soportando aumento de empleados, áreas y solicitudes.
Métrica | Soportar incremento del 200% en volumen de datos sin degradar tiempos de respuesta.

Campo | Descripción
--------|-------------
ID | RNF 11
Categoría | Idioma
Descripción | El sistema debe utilizar un idioma base unificado para toda la interfaz y estar preparado para traducciones futuras.
Métrica | 100% de la interfaz inicial en español latinoamericano.

Campo | Descripción
--------|-------------
ID | RNF 12
Categoría | Respaldos / Recuperación ante desastres
Descripción | En caso de caída total del entorno de producción, el sistema debe activar automáticamente una instancia espejo en la nube y restaurar la última copia útil.
Métrica | RTO < 4 horas, RPO < 24 horas.
