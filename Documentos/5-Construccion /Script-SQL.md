-- =====================================================================================
-- Proyecto  : Sistema de Gestión de Requerimientos (RMS) · NexaServicios
--             Ingeniería de Software II · Rebeca López Buelvas · Alvaro Tamayo Sierra
-- Archivo   : db/script_bd_gestion_requerimientos.sql
-- Historial : v1.0  2026-11-05  LB-1 (creación)                  -- cabecera de historial (GCS)
--             (todo cambio posterior entra por CRF y agrega una línea aquí: vX.Y fecha CRF-nnn LB-n)
-- Nace de   : Modelo Relacional (3.2 · paso 6) ← Diccionario de Datos (3.1 · paso 5)
--             Restricciones ← Matriz consolidada de Reglas de Negocio (RN-01 a RN-27)
-- Motor     : MySQL 8 · InnoDB · utf8mb4 / utf8mb4_0900_ai_ci
-- Reglas    : cada tabla es la imagen exacta del MR; cada CONSTRAINT lleva nombre propio y
--             cita su RN. Este archivo nunca elimina datos.
-- =====================================================================================
CREATE DATABASE IF NOT EXISTS gestion_requerimientos
  CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;
USE gestion_requerimientos;

-- 4.1.2 Tablas
-- =====================================================================================
-- 1. TABLAS (orden de dependencia del diccionario = orden válido de creación)
--    Norma general de FK (RN-10): ON DELETE RESTRICT, ON UPDATE CASCADE.
--    Única excepción: composición detalle_solicitud → solicitud (ON DELETE CASCADE).
-- =====================================================================================

-- Creación de la tabla rol
-- -------------------------------------------------------------------------------------
-- 1.1 rol · entidad MAESTRA (catálogo de perfiles)
--     HU-01..HU-04 · RF-01..RF-04 · CU-01..CU-04 · MK-01..MK-03 · Clase: Rol
-- -------------------------------------------------------------------------------------
CREATE TABLE rol (
  id_rol               INT UNSIGNED NOT NULL AUTO_INCREMENT,           -- PK sin setter
  nombre_rol           VARCHAR(50)  NOT NULL,                          -- RN-03
  descripcion          VARCHAR(255) NOT NULL,
  permiso_administrar  BOOLEAN      NOT NULL DEFAULT FALSE,            -- superusuario técnico (RN-04)
  fecha_creacion       DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT pk_rol        PRIMARY KEY (id_rol),
  CONSTRAINT uq_rol_nombre UNIQUE (nombre_rol)                         -- RN-03 dominio y unicidad
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creación de la tabla usuario
-- -------------------------------------------------------------------------------------
-- 1.2 usuario · entidad MAESTRA (se inactiva, no se elimina: RN-10)
--     HU-05..HU-10 · RF-05..RF-10 · CU-05..CU-10 · MK-04..MK-06 · Clase: Usuario
-- -------------------------------------------------------------------------------------
CREATE TABLE usuario (
  id_usuario           INT UNSIGNED     NOT NULL AUTO_INCREMENT,       -- PK sin setter
  nombre_completo      VARCHAR(150)     NOT NULL,
  correo_corporativo   VARCHAR(150)     NOT NULL,                      -- RN-01
  contrasena_hash      VARCHAR(255)     NOT NULL,                      -- RNF-02 (bcrypt / Argon2)
  estado_cuenta        ENUM('activo','inactivo','suspendido') NOT NULL DEFAULT 'activo',  -- ENUM EstadoCuenta
  intentos_fallidos    TINYINT UNSIGNED NOT NULL DEFAULT 0,            -- RN-02
  fecha_bloqueo        DATETIME         NULL DEFAULT NULL,             -- RN-02
  fecha_creacion       DATETIME         NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT pk_usuario         PRIMARY KEY (id_usuario),
  CONSTRAINT uq_usuario_correo  UNIQUE (correo_corporativo),           -- RN-01 credencial única
  CONSTRAINT chk_usuario_bloqueo
    CHECK (estado_cuenta <> 'suspendido' OR fecha_bloqueo IS NOT NULL) -- RN-02
  -- RN-01 (dominio @nexaservicios.com) se valida en la capa de aplicación (UsuarioService);
  -- el diccionario deja como opcional: CHECK (correo_corporativo LIKE '%@nexaservicios.com').
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE INDEX idx_usuario_estado ON usuario (estado_cuenta);

-- Creación de la tabla usuario_rol
-- -------------------------------------------------------------------------------------
-- 1.3 usuario_rol · entidad ASOCIATIVA (N:M usuario–rol)
--     HU-11..HU-13, HU-44 · RF-11..RF-13, RF-44 · CU-11..CU-13, CU-44 · MK-07..MK-09, MK-29
-- -------------------------------------------------------------------------------------
CREATE TABLE usuario_rol (
  id_usuario           INT UNSIGNED NOT NULL,                          -- FK → asociación Usuario 1—0..*
  id_rol               INT UNSIGNED NOT NULL,                          -- FK → asociación Rol 1—0..*
  fecha_asignacion     DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT pk_usuario_rol PRIMARY KEY (id_usuario, id_rol),          -- RN-17 no se repite el rol
  CONSTRAINT fk_usuario_rol_usuario FOREIGN KEY (id_usuario) REFERENCES usuario (id_usuario)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT fk_usuario_rol_rol     FOREIGN KEY (id_rol)     REFERENCES rol (id_rol)
    ON DELETE RESTRICT ON UPDATE CASCADE                               -- RN-10
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE INDEX idx_usuario_rol_rol ON usuario_rol (id_rol);

-- Creación de la tabla tipo_solicitud
-- -------------------------------------------------------------------------------------
-- 1.4 tipo_solicitud · entidad MAESTRA (catálogo; se inactiva: RN-16)
--     HU-14..HU-17 · RF-14..RF-17 · CU-14..CU-17 · MK-10..MK-12 · Clase: tipo_solicitud
-- -------------------------------------------------------------------------------------
CREATE TABLE tipo_solicitud (
  id_tipo_solicitud    INT UNSIGNED NOT NULL AUTO_INCREMENT,           -- PK sin setter
  codigo_tipo          VARCHAR(20)  NOT NULL,                          -- RN-21
  nombre_tipo          VARCHAR(50)  NOT NULL,
  descripcion          VARCHAR(255) NOT NULL,
  activo               BOOLEAN      NOT NULL DEFAULT TRUE,             -- RN-16 eliminación lógica
  CONSTRAINT pk_tipo_solicitud PRIMARY KEY (id_tipo_solicitud),
  CONSTRAINT uq_tipo_codigo    UNIQUE (codigo_tipo)                    -- RN-21
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creación de la tabla estado_solicitud
-- -------------------------------------------------------------------------------------
-- 1.5 estado_solicitud · entidad MAESTRA (catálogo centralizado de estados)
--     HU-18..HU-20 · RF-18..RF-20 · CU-18..CU-20 · MK-13, MK-14 · Clase: estado_solicitud
-- -------------------------------------------------------------------------------------
CREATE TABLE estado_solicitud (
  id_estado_solicitud  INT UNSIGNED NOT NULL AUTO_INCREMENT,           -- PK sin setter
  codigo_estado        VARCHAR(30)  NOT NULL,                          -- RN-22 (lo consulta el código)
  nombre_estado        VARCHAR(50)  NOT NULL,                          -- RN-22 (nombre visible)
  descripcion          VARCHAR(255) NULL DEFAULT NULL,
  es_final             BOOLEAN      NOT NULL DEFAULT FALSE,            -- RN-23 estados terminales
  CONSTRAINT pk_estado_solicitud PRIMARY KEY (id_estado_solicitud),
  CONSTRAINT uq_estado_codigo    UNIQUE (codigo_estado),               -- RN-22
  CONSTRAINT uq_estado_nombre    UNIQUE (nombre_estado)                -- RN-22
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creación de la tabla solicitud
-- -------------------------------------------------------------------------------------
-- 1.6 solicitud · entidad TRANSACCIONAL (cambia de estado; no se elimina)
--     HU-21..HU-27 · RF-21..RF-27 · CU-21..CU-26, CU-43 · MK-15..MK-17, MK-28 · Clase: Solicitud
--     CU crítico: CU-24 Radicar (DS-01 · DE-CU24)
-- -------------------------------------------------------------------------------------
CREATE TABLE solicitud (
  id_solicitud         INT UNSIGNED NOT NULL AUTO_INCREMENT,           -- PK = número de radicado
  id_solicitante       INT UNSIGNED NOT NULL,                          -- FK → asociación Usuario 1—0..* (radica)
  id_tipo_solicitud    INT UNSIGNED NOT NULL,                          -- FK → asociación tipo 1—0..* (clasifica)
  id_estado_solicitud  INT UNSIGNED NOT NULL,                          -- FK → asociación estado 1—0..*
  asunto               VARCHAR(200) NOT NULL,
  descripcion          TEXT         NOT NULL,
  anonimo_bloqueado    BOOLEAN      NOT NULL DEFAULT FALSE,            -- RN-04
  fecha_radicacion     DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP, -- RN-14 (disparadores 2.1)
  fecha_actualizacion  DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  CONSTRAINT pk_solicitud PRIMARY KEY (id_solicitud),
  CONSTRAINT fk_solicitud_solicitante FOREIGN KEY (id_solicitante)      REFERENCES usuario (id_usuario)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT fk_solicitud_tipo        FOREIGN KEY (id_tipo_solicitud)   REFERENCES tipo_solicitud (id_tipo_solicitud)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10, RN-16
  CONSTRAINT fk_solicitud_estado      FOREIGN KEY (id_estado_solicitud) REFERENCES estado_solicitud (id_estado_solicitud)
    ON DELETE RESTRICT ON UPDATE CASCADE                               -- RN-10
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE INDEX idx_solicitud_solicitante  ON solicitud (id_solicitante);
CREATE INDEX idx_solicitud_tipo         ON solicitud (id_tipo_solicitud);
CREATE INDEX idx_solicitud_estado_fecha ON solicitud (id_estado_solicitud, fecha_radicacion);

-- Creación de la tabla aprobacion_solicitud
-- -------------------------------------------------------------------------------------
-- 1.7 aprobacion_solicitud · entidad TRANSACCIONAL (un dictamen por evaluación)
--     HU-28..HU-31 · RF-28..RF-31 · CU-27..CU-30 · MK-18, MK-19 · Clase: aprobacion_solicitud
--     CU crítico: CU-27 Aprobar (DS-02A, DS-02B · DE-CU27)
-- -------------------------------------------------------------------------------------
CREATE TABLE aprobacion_solicitud (
  id_aprobacion        INT UNSIGNED NOT NULL AUTO_INCREMENT,           -- PK sin setter
  id_solicitud         INT UNSIGNED NOT NULL,                          -- FK → asociación Solicitud 1—0..* (evalúa)
  id_aprobador         INT UNSIGNED NOT NULL,                          -- FK → asociación Usuario 1—0..* (aprueba) · RN-05
  decision             ENUM('Aprobado','Rechazado','Devuelto_Para_Ajustes') NOT NULL,     -- ENUM DecisionAprobacion
  comentario           TEXT         NULL DEFAULT NULL,                 -- RN-06
  fecha_decision       DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT pk_aprobacion PRIMARY KEY (id_aprobacion),
  CONSTRAINT fk_aprobacion_solicitud FOREIGN KEY (id_solicitud) REFERENCES solicitud (id_solicitud)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT fk_aprobacion_aprobador FOREIGN KEY (id_aprobador) REFERENCES usuario (id_usuario)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT chk_aprobacion_comentario
    CHECK (decision = 'Aprobado' OR (comentario IS NOT NULL AND TRIM(comentario) <> ''))  -- RN-06
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE INDEX idx_aprobacion_solicitud ON aprobacion_solicitud (id_solicitud);
CREATE INDEX idx_aprobacion_aprobador ON aprobacion_solicitud (id_aprobador);

-- Creación de la tabla gestion_solicitud
-- -------------------------------------------------------------------------------------
-- 1.8 gestion_solicitud · entidad TRANSACCIONAL (historial de asignaciones)
--     HU-32..HU-36 · RF-32..RF-36 · CU-33..CU-37 · MK-20..MK-22 · Clase: gestion_solicitud
--     CU críticos: CU-33 Asignar gestor (DS-03 · DE-CU33) y CU-36 Finalizar (DS-04 · DE-CU36)
-- -------------------------------------------------------------------------------------
CREATE TABLE gestion_solicitud (
  id_gestion           INT UNSIGNED NOT NULL AUTO_INCREMENT,           -- PK sin setter
  id_solicitud         INT UNSIGNED NOT NULL,                          -- FK → asociación Solicitud 1—0..* (recibe) · RN-11
  id_gestor            INT UNSIGNED NOT NULL,                          -- FK → asociación Usuario 1—0..* (gestiona) · RN-27
  prioridad            ENUM('Baja','Media','Alta','Critica') NOT NULL DEFAULT 'Media',     -- ENUM PrioridadGestion · RN-24
  estado_gestion       ENUM('En_Proceso','Reasignado','Finalizado') NOT NULL DEFAULT 'En_Proceso',  -- ENUM EstadoGestion
  fecha_vinculacion    DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP,
  fecha_cierre         DATETIME     NULL DEFAULT NULL,                 -- RN-12
  CONSTRAINT pk_gestion PRIMARY KEY (id_gestion),
  CONSTRAINT fk_gestion_solicitud FOREIGN KEY (id_solicitud) REFERENCES solicitud (id_solicitud)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT fk_gestion_gestor    FOREIGN KEY (id_gestor)    REFERENCES usuario (id_usuario)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT chk_gestion_fechas
    CHECK (fecha_cierre IS NULL OR fecha_cierre >= fecha_vinculacion),  -- RN-12 coherencia temporal
  CONSTRAINT chk_gestion_cierre
    CHECK (estado_gestion <> 'Finalizado' OR fecha_cierre IS NOT NULL)  -- RN-12 cierre obligatorio
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE INDEX idx_gestion_solicitud ON gestion_solicitud (id_solicitud);
CREATE INDEX idx_gestion_gestor    ON gestion_solicitud (id_gestor);
CREATE INDEX idx_gestion_prioridad ON gestion_solicitud (prioridad);
CREATE INDEX idx_gestion_estado    ON gestion_solicitud (estado_gestion);

-- Creación de la tabla evaluacion
-- -------------------------------------------------------------------------------------
-- 1.9 evaluacion · entidad TRANSACCIONAL (encuesta de satisfacción, 1:0..1 con gestión)
--     HU-37, HU-38 · RF-37, RF-38 · CU-38, CU-39 · MK-23, MK-24 · Clase: Evaluacion
-- -------------------------------------------------------------------------------------
CREATE TABLE evaluacion (
  id_evaluacion        INT UNSIGNED     NOT NULL AUTO_INCREMENT,       -- PK sin setter
  id_gestion           INT UNSIGNED     NOT NULL,                      -- FK → asociación gestion 1—0..1 (registra) · RN-13
  id_evaluador         INT UNSIGNED     NOT NULL,                      -- FK → asociación Usuario 1—0..* (realiza) · RN-13
  calificacion         TINYINT UNSIGNED NOT NULL,                      -- RN-07
  comentario           TEXT             NULL DEFAULT NULL,
  fecha_evaluacion     DATETIME         NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT pk_evaluacion PRIMARY KEY (id_evaluacion),
  CONSTRAINT uq_evaluacion_gestion UNIQUE (id_gestion),                -- RN-13 una sola evaluación
  CONSTRAINT fk_evaluacion_gestion   FOREIGN KEY (id_gestion)   REFERENCES gestion_solicitud (id_gestion)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT fk_evaluacion_evaluador FOREIGN KEY (id_evaluador) REFERENCES usuario (id_usuario)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT chk_evaluacion_calificacion
    CHECK (calificacion BETWEEN 1 AND 5)                               -- RN-07
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE INDEX idx_evaluacion_evaluador ON evaluacion (id_evaluador);

-- Creación de la tabla detalle_solicitud
-- -------------------------------------------------------------------------------------
-- 1.10 detalle_solicitud · entidad TRANSACCIONAL (composición: historial conversacional)
--      HU-39, HU-40 · RF-39, RF-40 · CU-31, CU-32 · MK-25, MK-26 · Clase: detalle_solicitud
-- -------------------------------------------------------------------------------------
CREATE TABLE detalle_solicitud (
  id_detalle           INT UNSIGNED NOT NULL AUTO_INCREMENT,           -- PK sin setter
  id_solicitud         INT UNSIGNED NOT NULL,                          -- FK → composición Solicitud 1 ◆— 0..*
  id_usuario           INT UNSIGNED NOT NULL,                          -- FK → asociación Usuario 1—0..* (publica)
  mensaje              TEXT         NULL DEFAULT NULL,                 -- RN-08
  ruta_adjunto         VARCHAR(512) NULL DEFAULT NULL,                 -- RN-08 · RNF-06
  fecha_registro       DATETIME     NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT pk_detalle PRIMARY KEY (id_detalle),
  CONSTRAINT fk_detalle_solicitud FOREIGN KEY (id_solicitud) REFERENCES solicitud (id_solicitud)
    ON DELETE CASCADE ON UPDATE CASCADE,                               -- RN-10 excepción: composición
  CONSTRAINT fk_detalle_usuario   FOREIGN KEY (id_usuario)   REFERENCES usuario (id_usuario)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT chk_detalle_contenido
    CHECK (mensaje IS NOT NULL OR ruta_adjunto IS NOT NULL)            -- RN-08 sin registros vacíos
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE INDEX idx_detalle_solicitud ON detalle_solicitud (id_solicitud, fecha_registro);
CREATE INDEX idx_detalle_usuario   ON detalle_solicitud (id_usuario);

-- Creación de la tabla bitacora_auditoria
-- -------------------------------------------------------------------------------------
-- 1.11 bitacora_auditoria · entidad de AUDITORÍA (solo lectura e inmutable: RN-09)
--      HU-41..HU-43, HU-45 · RF-41..RF-43, RF-45 · CU-40..CU-42, CU-45 · MK-27 · Clase: Bitacora_Auditoria
--      Recibe registrarAccion(Cambio_Estado) en DS-01 m.21, DS-02A m.24, DS-02B m.25, DS-03 m.30, DS-04 m.25
-- -------------------------------------------------------------------------------------
CREATE TABLE bitacora_auditoria (
  id_bitacora          BIGINT UNSIGNED NOT NULL AUTO_INCREMENT,        -- PK sin setter (alto volumen)
  id_solicitud         INT UNSIGNED    NULL DEFAULT NULL,              -- FK → asociación Solicitud 0..1—0..* (audita)
  entidad_afectada     VARCHAR(50)     NOT NULL,
  id_registro_afectado INT UNSIGNED    NOT NULL,
  id_usuario_accion    INT UNSIGNED    NOT NULL,                       -- FK → asociación Usuario 1—0..* (ejecuta)
  accion_realizada     ENUM('Creacion','Modificacion','Eliminacion','Inicio_Sesion','Cierre_Sesion',
                            'Bloqueo_Cuenta','Cambio_Estado','Asignacion_Rol','Desbloqueo_Identidad')
                       NOT NULL,                                       -- ENUM AccionAuditoria (9 valores)
  estado_anterior      INT UNSIGNED    NULL DEFAULT NULL,              -- FK → estado_solicitud (rol estado_anterior)
  estado_nuevo         INT UNSIGNED    NULL DEFAULT NULL,              -- FK → estado_solicitud (rol estado_nuevo) · RN-15
  observaciones        TEXT            NULL DEFAULT NULL,
  fecha_registro       DATETIME        NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT pk_bitacora PRIMARY KEY (id_bitacora),
  CONSTRAINT fk_bitacora_solicitud      FOREIGN KEY (id_solicitud)      REFERENCES solicitud (id_solicitud)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT fk_bitacora_usuario        FOREIGN KEY (id_usuario_accion) REFERENCES usuario (id_usuario)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT fk_bitacora_estado_anterior FOREIGN KEY (estado_anterior)  REFERENCES estado_solicitud (id_estado_solicitud)
    ON DELETE RESTRICT ON UPDATE CASCADE,                              -- RN-10
  CONSTRAINT fk_bitacora_estado_nuevo   FOREIGN KEY (estado_nuevo)      REFERENCES estado_solicitud (id_estado_solicitud)
    ON DELETE RESTRICT ON UPDATE CASCADE                               -- RN-10
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creación de índices optimizados para bitacora_auditoria
CREATE INDEX idx_bitacora_solicitud        ON bitacora_auditoria (id_solicitud);
CREATE INDEX idx_bitacora_entidad_registro ON bitacora_auditoria (entidad_afectada, id_registro_afectado);
CREATE INDEX idx_bitacora_usuario          ON bitacora_auditoria (id_usuario_accion);
CREATE INDEX idx_bitacora_accion           ON bitacora_auditoria (accion_realizada);
CREATE INDEX idx_bitacora_est_ant          ON bitacora_auditoria (estado_anterior);
CREATE INDEX idx_bitacora_est_nuev         ON bitacora_auditoria (estado_nuevo);
CREATE INDEX idx_bitacora_fecha            ON bitacora_auditoria (fecha_registro);
