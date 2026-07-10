# Entregable 3 — Plan de Gestión del Proyecto (PMBOK)

## 3.1 Acta de Constitución del Proyecto (Project Charter)

| Campo | Detalle |
|---|---|
| **Nombre del proyecto** | Sistema Inteligente de Control de Asistencia mediante Reconocimiento Facial |
| **Sponsor** | Área de Gestión de Tecnologías de Información (GTI) — Dirección Académica |
| **Gerente de Proyecto** | Designado por el Área de GTI |
| **Fecha de inicio** | Semana 1 del cronograma de despliegue |
| **Duración estimada** | 16 semanas |

### Alcance del Proyecto

**Incluye:**

- Diagnóstico del proceso actual (AS-IS) y diseño del proceso propuesto (TO-BE).
- Desarrollo del motor de inteligencia artificial (detección y reconocimiento facial).
- Desarrollo de API central (Laravel 11) y aplicación móvil (Flutter 3).
- Despliegue en infraestructura local (Ubuntu Server + Docker) sobre red LAN aislada.
- Implementación de mecanismos de seguridad y cifrado de datos biométricos.
- Ejecución de un piloto controlado en al menos una sección académica.

**Excluye:**

- Integración con sistemas de nómina o gestión de recursos humanos.
- Reconocimiento facial con fines distintos al registro de asistencia académica.
- Despliegue en infraestructura en la nube pública (arquitectura restringida a entorno local/LAN).

### Supuestos

- Las aulas piloto cuentan con conexión a la red LAN institucional.
- Se dispone de hardware mínimo (CPU i5/Ryzen, 8 GB RAM, webcam 720p) en las secciones seleccionadas para el piloto.
- La institución autoriza la captura y procesamiento de datos biométricos bajo consentimiento informado, conforme a normativa de protección de datos aplicable.
- El equipo de desarrollo cuenta con conocimientos previos en Python, PHP (Laravel) y Dart (Flutter).

### Restricciones

- El proyecto debe ejecutarse **sin costos de licenciamiento de software**.
- El procesamiento de IA debe ser viable **sin GPU dedicada**.
- Los datos biométricos **no pueden salir de la red LAN institucional**.

## 3.2 Gestión del Alcance — Entregables Principales

| # | Entregable | Descripción |
|---|---|---|
| 1 | **Diagnóstico Organizacional** | Análisis AS-IS del proceso de asistencia y alineamiento estratégico. |
| 2 | **Business Case** | Justificación económica, análisis de alternativas y evaluación de riesgos iniciales. |
| 3 | **Plan de Gestión del Proyecto** | Planificación PMBOK: alcance, cronograma, costos y riesgos. |
| 4 | **Modelado de Procesos TO-BE** | Diseño del flujo automatizado de reconocimiento facial. |
| 5 | **Arquitectura de Solución TIC** | Documento técnico de arquitectura, seguridad y escalabilidad. |
| 6 | **Sistema en producción (piloto)** | Sistema desplegado y validado en al menos una sección académica. |

### Estructura de Descomposición del Trabajo (EDT / WBS — Nivel 1)

```
1.0 Sistema de Control de Asistencia por Reconocimiento Facial
├── 1.1 Diagnóstico y Análisis Estratégico
├── 1.2 Diseño de Arquitectura y Base de Datos
├── 1.3 Desarrollo del Motor de IA (YOLOv8-Face + ArcFace R100)
├── 1.4 Desarrollo de Backend (Laravel 11 + FastAPI)
├── 1.5 Desarrollo de Aplicación Móvil (Flutter 3)
├── 1.6 Infraestructura y Despliegue (Docker + Ubuntu Server)
├── 1.7 Seguridad, Cifrado y Cumplimiento (ISO 27001 / ACM)
└── 1.8 Piloto, CI/CD y Cierre
```

## 3.3 Gestión del Cronograma — Despliegue en 16 Semanas

El cronograma se estructura en **4 fases secuenciales**, cada una de 4 semanas de duración, siguiendo un enfoque incremental de entrega de valor.

| Fase | Semanas | Foco Principal | Entregables Clave |
|---|---|---|---|
| **Fase 1 — Fundación** | 1 – 4 | Análisis **AS-IS / TO-BE** y preparación de infraestructura de **red LAN** | Diagnóstico validado, diseño de procesos, topología de red definida |
| **Fase 2 — Núcleo de Servicios** | 5 – 8 | Contenerización con **Docker** y desarrollo de **FastAPI** (IA) / **Laravel** (Core API) | Servicios backend funcionales en contenedores, endpoints de autenticación (JWT) |
| **Fase 3 — Integración de Red y Cliente** | 9 – 12 | Configuración de **red** de aulas y desarrollo de la aplicación **Flutter** | App móvil funcional conectada a la API, pruebas de latencia en red LAN |
| **Fase 4 — Automatización y Piloto** | 13 – 16 | Implementación de **CI/CD** y ejecución del **piloto** en producción controlada | Pipeline de integración/despliegue continuo, piloto validado con métricas de precisión y latencia |

### Diagrama de Fases (Gantt Simplificado)

```
Semana:        1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16
Fase 1 AS-IS   ██ ██ ██ ██
Fase 2 Docker              ██ ██ ██ ██
Fase 3 Red/App                         ██ ██ ██ ██
Fase 4 CI/CD                                       ██ ██ ██ ██
```

### Hitos del Proyecto

| Hito | Semana | Criterio de Aceptación |
|---|---|---|
| Cierre de diagnóstico AS-IS/TO-BE | 4 | Documento validado por el Área de GTI |
| Servicios backend en contenedores operativos | 8 | Endpoints de FastAPI y Laravel responden en entorno Docker |
| App móvil conectada en red LAN | 12 | Flutter consume API con latencia ≤ 2s |
| Piloto en producción | 16 | Precisión ≥ 90 %, disponibilidad ≥ 99 % sostenida durante el piloto |

## 3.4 Gestión de Costos

### Estructura de Costos del Proyecto

| Categoría | Componente | Costo de Licenciamiento | Observaciones |
|---|---|---|---|
| Software | Flutter 3, Laravel 11, FastAPI, MySQL 8, Docker, Ubuntu Server | **US$ 0** | Stack 100 % Open Source |
| Hardware — Servidor local | CPU i5/Ryzen, 8 GB RAM | Costo estándar de mercado | Sin necesidad de GPU dedicada |
| Hardware — Captura | Webcam 720p por aula | Costo estándar de mercado | Componente de menor costo del ecosistema |
| Infraestructura de red | Red LAN institucional existente | Sin costo incremental relevante | Reutiliza infraestructura ya disponible |
| Recurso humano | Equipo de desarrollo (16 semanas) | Principal componente del presupuesto | Estimado según tarifas internas/institucionales |

### Principio de Eficiencia Presupuestaria

La **ausencia de licenciamiento de software** y la **no dependencia de GPU** constituyen las dos palancas centrales de eficiencia del presupuesto del proyecto. En comparación con soluciones comerciales de reconocimiento facial —que habitualmente requieren licencias por usuario/dispositivo y hardware acelerado por GPU— la presente propuesta concentra el presupuesto casi en su totalidad en **horas de desarrollo**, un costo controlable y no recurrente, en lugar de costos de licenciamiento recurrentes (OPEX de software).

## 3.5 Gestión de Riesgos

### Matriz de Riesgos del Proyecto

| ID | Riesgo | Categoría | Probabilidad | Impacto | Estrategia de Respuesta |
|---|---|---|---|---|---|
| R-01 | Exposición o filtración de datos biométricos de estudiantes menores de edad | Seguridad / Legal | Baja | Muy Alto | **Mitigar**: cifrado de embeddings 512-D, red air-gapped, cumplimiento ISO 27001 |
| R-02 | Indisponibilidad del servicio durante horario lectivo | Operacional | Media | Alto | **Mitigar**: arquitectura contenedorizada con reinicio automático, meta de disponibilidad ≥ 99 % |
| R-03 | Degradación de precisión por condiciones de iluminación | Técnico | Media | Medio | **Mitigar**: selección de modelos robustos (YOLOv8-Face) y guías de instalación de cámara |
| R-04 | Incumplimiento de latencia (> 2s) por saturación de red | Técnico | Baja | Medio | **Mitigar**: pruebas de carga en Fase 3, red LAN dedicada |
| R-05 | Resistencia de la comunidad educativa al uso de biometría | Organizacional | Media | Medio | **Transferir/Mitigar**: comunicación institucional, consentimiento informado, transparencia normativa |
| R-06 | Uso indebido de los datos fuera del propósito de asistencia | Ético / Legal | Baja | Muy Alto | **Mitigar**: gobernanza de datos conforme a Código de Ética ACM, política de uso exclusivo académico |

### Enfoque de Protección de Datos de Menores de Edad

Dado que la población estudiantil puede incluir **menores de edad**, la gestión de riesgos del proyecto prioriza:

- **Minimización de datos**: no se almacenan fotografías, solo representaciones vectoriales (embeddings) no reversibles.
- **Aislamiento de red**: los datos biométricos permanecen exclusivamente dentro de la **red LAN institucional**, sin exposición a redes externas o servicios en la nube.
- **Cifrado en reposo** de la base de datos de embeddings, conforme a controles de la familia **ISO/IEC 27001**.
- **Consentimiento informado** de los representantes legales de los estudiantes, como condición previa a la activación del sistema para cada sección piloto.

---

**Entregable anterior:** [Entregable 2 — Business Case del Proyecto](entregable2_business_case.md)
**Siguiente entregable:** [Entregable 4 — Modelado de Procesos AS-IS / TO-BE](entregable4_procesos.md)
