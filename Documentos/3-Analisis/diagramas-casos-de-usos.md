```mermaid
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
    CU11(("CU-1
