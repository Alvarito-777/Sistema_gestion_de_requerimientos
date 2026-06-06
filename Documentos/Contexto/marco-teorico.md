El sustento técnico de este proyecto se divide en la comprensión de la información como un activo sistémico y la aplicación de modelos de ciclo de vida que garanticen la persistencia del dato.

1. Conceptos Claves y Definiciones Formales
   
•	Gestión de Requerimientos (Requirements Management): Según el Software Engineering Body of Knowledge (SWEBOK v4, 2024), es el proceso de encontrar, documentar, organizar y rastrear los requerimientos de un sistema, así como la gestión de los cambios en dichos requerimientos. En Nexa, este concepto es la antítesis del "sticker de WhatsApp", pues exige un canal formal de entrada y salida.

•	Trazabilidad (Traceability): Definida por la ISO/IEC/IEEE 24765:2017 (ratificada en revisiones de 2022) como la capacidad de describir y seguir la vida de un requerimiento en una dirección hacia adelante y hacia atrás. Es el "hilo de Ariadna" que permitiría a la gerencia de Nexa saber quién aprobó una solicitud y qué ejecución técnica derivó de ella.

•	Integridad de Datos: Es el mantenimiento y la garantía de la exactitud y consistencia de los datos a lo largo de su ciclo de vida (Stair & Reynolds, 2022). Un archivo de Excel llamado "final_v9" es una violación directa a la integridad, pues no garantiza que el dato sea el más reciente o veraz.

•	Workflow (Flujo de Trabajo): La automatización de un proceso de negocio, en su totalidad o en partes, donde documentos o tareas pasan de un participante a otro según un conjunto de reglas procedimentales (WfMC, 2021).

3. Teorías y Modelos de Sustento
   
•	Modelo de Madurez de Capacidades (CMMI): Este modelo sugiere que para que una organización sea eficiente, debe pasar de procesos "Ad Hoc" (caóticos, como los de Nexa) a procesos "Definidos" y "Gestionados". La solución propuesta se basa en el Nivel 2 de CMMI, que se enfoca en la gestión de requisitos para establecer líneas base de control.

•	Teoría de Sistemas (Ludwig von Bertalanffy): Aplicada a las organizaciones, postula que una empresa es un sistema abierto donde la salida de un proceso (la aprobación de la Gerencia) es la entrada de otro (la ejecución de TI). Si el canal de comunicación tiene "ruido" (WhatsApp, correos perdidos), el sistema entra en un estado de entropía o desorden máximo.

•	Ciclo de Vida de Desarrollo de Software (SDLC) - Enfoque Ágil: El manifiesto ágil y sus actualizaciones (2021-2025) enfatizan que, aunque se valore la interacción humana, se requiere de "software funcionando" y "respuesta al cambio". La solución propuesta utiliza el modelo de Backlog de Producto para organizar las solicitudes de la gerencia antes de ser enviadas a Camilo (TI).

5. Relación entre Conceptos y la Problemática de Nexa
La crisis de Nexa Servicios no es una falta de trabajo, sino una falla de arquitectura de procesos. La relación se establece de la siguiente forma:

• De la Informalidad a la Trazabilidad: Al aplicar la definición de trazabilidad, se elimina la libreta de Oscar y los chats de Diana. Cada solicitud recibe un Identificador Único (UUID) que vincula la aprobación de palabra con un registro digital inmutable.
• Del Caos al Workflow: El problema de "quién autorizó esto" se resuelve implementando un Modelo de Estados. Una solicitud no puede ser ejecutada por Camilo si su estado en la base de datos no es Aprobado_Gerencia. Esto fuerza a la organización a seguir un flujo lógico, eliminando la ambigüedad operativa.
• De los Archivos Locales a la Integridad Centralizada: El reemplazo de los Excel "final_final" por un sistema de gestión permite aplicar reglas de negocio y restricciones de integridad (Foreign Keys, Triggers), asegurando que la información sea consistente para todos los actores en tiempo real.
________________________________________
Bibliografía de Respaldo (2021-2026)
•	IEEE Computer Society (2024). Guide to the Software Engineering Body of Knowledge (SWEBOK V4.0).
•	Stair, R., & Reynolds, G. (2022). Principles of Information Systems. Cengage Learning. (Conceptos de Integridad y Sistemas de Información).
•	Sommerville, I. (2021). Software Engineering. 10th Edition (Global Edition). Pearson. (Modelos de gestión de requisitos).
•	ISO/IEC (2022). Information technology — Systems and software quality requirements and evaluation (SQuaRE). Standard 25010.

