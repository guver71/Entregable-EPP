# Entregable 5 — Propuesta de Solución TIC Integrada

## 5.1 Arquitectura de la Solución

La solución se estructura mediante una **arquitectura en capas**, que garantiza separación de responsabilidades, escalabilidad y aislamiento de seguridad entre los componentes de presentación, negocio, inteligencia artificial y datos.

### 5.1.1 Diagrama General de Arquitectura

```
┌───────────────────────────────────────────────────────────────┐
│                    CAPA DE PRESENTACIÓN                       │
│                  Aplicación Móvil — Flutter 3                 │
│   (Docentes / Administradores — consulta y gestión de datos)  │
└───────────────────────────┬───────────────────────────────────┘
                             │ HTTPS / JWT (Red LAN)
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                     CAPA DE NEGOCIO (Core API)                │
│                       Laravel 11 + JWT                        │
│   Autenticación · Autorización · Reglas de Negocio Académicas │
└───────────────────────────┬───────────────────────────────────┘
                             │ API interna (REST)
                             ▼
┌───────────────────────────────────────────────────────────────┐
│              CAPA DE INTELIGENCIA ARTIFICIAL                  │
│                     Python + FastAPI                          │
│     Detección (YOLOv8-Face) · Vectorización (ArcFace R100)    │
│              Comparación por Similitud Coseno                 │
└───────────────────────────┬───────────────────────────────────┘
                             │ Consultas cifradas
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                CENTRO DE DATOS LOCAL (On-Premise)              │
│         Ubuntu Server + Docker · MySQL 8 (Embeddings 512-D)   │
│              Red LAN Aislada (Air-Gapped) — ISO 27001         │
└───────────────────────────────────────────────────────────────┘
```

### 5.1.2 Descripción de Capas

| Capa | Componente Tecnológico | Responsabilidad |
|---|---|---|
| **Presentación** | Flutter 3 (móvil, multiplataforma) | Interfaz para docentes/administradores: visualización de asistencia, reportes, gestión de secciones. |
| **Negocio (Core API)** | Laravel 11 + JWT | Gestión de identidad, autenticación de usuarios, reglas académicas (secciones, horarios, roles). |
| **Inteligencia Artificial** | Python + FastAPI, YOLOv8-Face, ArcFace R100 | Detección facial, vectorización biométrica y comparación de identidad. |
| **Centro de Datos Local** | Ubuntu Server + Docker + MySQL 8 | Persistencia de embeddings cifrados, orquestación de contenedores, aislamiento de red. |

## 5.2 Ecosistema de Sistemas de Información

La solución se concibe como un **ecosistema de microservicios contenedorizados**, donde cada componente se comunica mediante interfaces API bien definidas, permitiendo la interoperabilidad con los sistemas de información institucionales existentes sin comprometer su integridad.

### 5.2.1 Flujo de Interacción entre Componentes

1. La **aplicación Flutter** consume exclusivamente el **Core API (Laravel 11)**, autenticándose mediante tokens **JWT**, sin acceso directo a la capa de inteligencia artificial ni a la base de datos.
2. El **Core API (Laravel 11)** actúa como orquestador: gestiona la lógica académica (secciones, docentes, horarios) y delega el procesamiento biométrico al **servicio de IA (FastAPI)** mediante llamadas internas a la red LAN.
3. El **servicio de IA (FastAPI)** procesa el reconocimiento facial y persiste/consulta los **embeddings** directamente en **MySQL 8**, devolviendo únicamente el resultado de la coincidencia (identidad + score de similitud) al Core API.
4. El **Core API** traduce el resultado del reconocimiento en un **registro de asistencia** dentro del modelo de datos académico institucional, disponible para consulta desde la aplicación móvil.

### 5.2.2 Principio de Integración con Sistemas Institucionales

- El **Core API (Laravel 11)** funciona como la **capa de integración** hacia futuros sistemas de información institucionales (por ejemplo, sistemas de gestión académica), exponiendo endpoints REST versionados y documentados.
- La **capa de IA permanece desacoplada** de la lógica académica: solo resuelve el problema de identidad biométrica, lo cual permite actualizar o reemplazar el modelo de reconocimiento (YOLOv8-Face / ArcFace R100) sin afectar al resto del ecosistema.
- Toda comunicación entre capas ocurre **dentro de la red LAN institucional**, sin exposición de endpoints a redes públicas.

## 5.3 Seguridad y Gobernanza (Digital Vault)

### 5.3.1 Principio de No Almacenamiento de Fotografías

La solución adopta como principio de diseño irrenunciable la **NO retención de fotografías o imágenes faciales**. En su lugar, el sistema procesa cada rostro capturado en el momento (*in-memory*), lo transforma en un **embedding matemático de 512 dimensiones** mediante ArcFace R100, y **descarta la imagen original inmediatamente después del procesamiento**.

```
Imagen del rostro (temporal, en memoria)
          │
          ▼  ArcFace R100
Embedding matemático [512 dimensiones]
          │
          ▼  Cifrado
Almacenamiento en Bóveda Digital (MySQL 8)
          │
          ▼
Imagen original ── DESCARTADA (no persistida)
```

### 5.3.2 Bóveda Digital (Digital Vault)

| Control de Seguridad | Implementación |
|---|---|
| **Cifrado en reposo** | Los embeddings de 512 dimensiones se almacenan cifrados dentro de MySQL 8, no como datos planos. |
| **Aislamiento de red** | Infraestructura desplegada sobre **red LAN air-gapped**, sin conectividad a internet pública. |
| **No reversibilidad** | Un embedding matemático **no puede reconstruirse** en una fotografía; constituye una representación vectorial abstracta, no una imagen. |
| **Control de acceso** | Autenticación **JWT** con control de roles (docente, administrador, IA) para el acceso a los servicios que interactúan con la Bóveda Digital. |
| **Contenerización** | Cada servicio (API, IA, base de datos) se ejecuta en **contenedores Docker** aislados, limitando la superficie de ataque entre componentes. |

### 5.3.3 Cumplimiento Normativo

- **ISO/IEC 27001**: la arquitectura incorpora controles de seguridad de la información alineados a los dominios de gestión de activos, control de acceso, criptografía y seguridad de las comunicaciones.
- **Código de Ética de ACM (Association for Computing Machinery)**: el diseño del sistema observa los principios de **minimización de datos**, **transparencia con los usuarios** (consentimiento informado) y **uso exclusivo de los datos para el propósito declarado** (control de asistencia académica), evitando cualquier uso secundario no autorizado de la información biométrica.
- **Principio de propósito limitado**: los embeddings almacenados en la Bóveda Digital **no pueden ser utilizados** para fines de vigilancia, análisis conductual u otros propósitos ajenos al registro de asistencia.

!!! danger "Política de Datos Sensibles"
    El sistema está diseñado bajo el principio de que **la ausencia de dato es la mejor protección del dato**. Al no almacenar fotografías, se elimina de raíz el riesgo de fuga de imágenes reales de estudiantes, incluyendo menores de edad, ante cualquier eventual incidente de seguridad.

## 5.4 Escalabilidad y Sostenibilidad

### 5.4.1 Entorno Dockerizado y Predecible

La totalidad de los servicios de la solución (Core API, servicio de IA, base de datos) se despliega mediante **contenedores Docker**, lo que garantiza:

- **Portabilidad**: el mismo conjunto de contenedores puede replicarse en aulas o sedes adicionales sin reconfiguración manual extensa.
- **Reproducibilidad**: el entorno de ejecución es idéntico entre desarrollo, pruebas y producción, eliminando incidencias del tipo *"funciona en mi máquina"*.
- **Aislamiento de fallos**: un error en un contenedor (por ejemplo, el servicio de IA) no compromete la disponibilidad del Core API ni de la base de datos.
- **Facilidad de actualización**: los modelos de IA (YOLOv8-Face, ArcFace R100) pueden actualizarse mediante el reemplazo de la imagen del contenedor correspondiente, sin afectar el resto del ecosistema.

### 5.4.2 Escalabilidad Horizontal

| Dimensión | Estrategia de Escalabilidad |
|---|---|
| **Por aula** | Replicación del contenedor de captura/cámara, apuntando al mismo servicio central de IA sobre la red LAN. |
| **Por sección** | El throughput objetivo (≤ 30 s por cada 30 estudiantes) permite el procesamiento secuencial de múltiples secciones sin degradación significativa. |
| **Por sede** | La arquitectura on-premise permite replicar el **Centro de Datos Local** completo en cada sede, manteniendo el aislamiento de red por ubicación física. |

### 5.4.3 Sostenibilidad del Proyecto

- **Sostenibilidad económica**: al sustentarse en un stack 100 % Open Source y hardware sin GPU, el costo marginal de mantener y escalar la solución es significativamente menor al de alternativas comerciales licenciadas.
- **Sostenibilidad técnica**: el uso de **Docker** garantiza que la solución no quede atada a versiones específicas del sistema operativo o dependencias del entorno, facilitando su mantenimiento a largo plazo por parte del Área de GTI.
- **Sostenibilidad operativa**: al integrarse un pipeline de **CI/CD** (Fase 4 del cronograma, Entregable 3), las actualizaciones del sistema pueden desplegarse de manera controlada y predecible, reduciendo el riesgo operativo de futuras mejoras.

---

**Entregable anterior:** [Entregable 4 — Modelado de Procesos AS-IS / TO-BE](entregable4_procesos.md)
**Volver al inicio:** [Página principal](index.md)
