graph TD

%% Actores Primarios
subgraph Actores_Primarios[Actores Primarios]
    ACT01["Desarrollador de Software<br/>(Solicitante)"]
    ACT02["Revisor de Gerencia / Jefatura<br/>(Aprobador / Evaluador)"]
end

%% Actores Secundarios / Sistemas
subgraph Actores_Secundarios[Actores Secundarios y Sistemas]
    ACT03["Auxiliar de Talento Humano"]
    ACT04["Gestor Documental / Soporte<br/>(Administrador)"]
    ACT05["Sistema de Notificaciones"]
    ACT06["Servicio de Firma Digital / Estampado de Tiempo"]
end

%% Casos de Uso: Radicación y Gestión
subgraph Modulo_Radicacion[Radicación y Gestión de Solicitudes]
    CU01(("CU-01: Registrar Solicitud Formal"))
    CU02(("CU-02: Gestionar Solicitud en Borrador"))
end

%% Casos de Uso: Visualización e Historial
subgraph Modulo_Visualizacion[Visualización, Búsqueda e Historial]
    CU03(("CU-03: Consultar Historial"))
    CU04(("CU-04: Buscar Solicitudes Avanzada"))
    CU12(("CU-12: Generar y Descargar Reporte PDF"))
end

%% Casos de Uso: Evaluación y Delegaciones
subgraph Modulo_Evaluacion[Evaluación, Respuestas y Delegaciones]
    CU05(("CU-05: Evaluar y Responder Solicitud"))
    CU06(("CU-06: Priorizar Bandeja de Entrada"))
    CU07(("CU-07: Configurar Delegación Temporal"))
    CU13(("CU-13: Visualizar Métricas en Dashboard"))
    CU14(("CU-14: Revelar Identidad en Quejas Anónimas"))
end

%% Casos de Uso: Cierres, Seguridad y Auditoría
subgraph Modulo_Seguridad[Cierres, Seguridad y Auditoría]
    CU08(("CU-08: Confirmar Cierre y Calificar Servicio"))
    CU09(("CU-09: Autenticar Usuario y Controlar Sesión"))
    CU10(("CU-10: Consultar Log de Auditoría"))
    CU11(("CU-11: Recuperar Contraseña de Usuario"))
    CU15(("CU-15: Exportar Bitácora de Auditoría"))
end

%% Relaciones: ACT-01 (Solicitante)
ACT01 --> CU01
ACT01 --> CU02
ACT01 --> CU03
ACT01 --> CU04
ACT01 --> CU08
ACT01 --> CU11
ACT01 --> CU12

%% Relaciones: ACT-02 (Revisor / Gerencia)
ACT02 --> CU04
ACT02 --> CU05
ACT02 --> CU06
ACT02 --> CU07
ACT02 --> CU11
ACT02 --> CU12
ACT02 --> CU13
ACT02 --> CU14

%% Relaciones: ACT-03 (Talento Humano)
ACT03 --> CU05

%% Relaciones: ACT-04 (Administrador)
ACT04 --> CU09
ACT04 --> CU10
ACT04 --> CU15

%% Relaciones: ACT-05 (Notificaciones)
CU01 -.-> ACT05
CU05 -.-> ACT05
CU11 -.-> ACT05

%% Relaciones: ACT-06 (Firma Digital y Estampado)
CU03 -.-> ACT06
CU05 -.-> ACT06
CU08 -.-> ACT06
CU10 -.-> ACT06
CU12 -.-> ACT06
CU14 -.-> ACT06

%% Relaciones Include / Extend
CU01 ..> CU02 : <<extend>>
CU10 ..> CU15 : <<extend>>
