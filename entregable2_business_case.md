# Entregable 2 — Business Case del Proyecto

## 2.1 Justificación

La justificación del proyecto se articula mediante objetivos formulados bajo el criterio **SMART** (*Specific, Measurable, Achievable, Relevant, Time-bound*), orientados a recuperar el tiempo de instrucción perdido y a garantizar la fiabilidad biométrica del nuevo proceso de control de asistencia.

| Objetivo SMART | Descripción |
|---|---|
| **Específico (S)** | Implementar un sistema de reconocimiento facial basado en **YOLOv8-Face** y **ArcFace R100** que automatice el registro de asistencia en aulas. |
| **Medible (M)** | Alcanzar una **precisión de reconocimiento ≥ 90 %**, con **latencia de red ≤ 2 segundos** y **throughput ≤ 30 segundos por cada 30 estudiantes**. |
| **Alcanzable (A)** | Desplegable sobre hardware estándar (CPU i5/Ryzen, 8 GB RAM, webcam 720p), sin inversión en GPU ni licenciamiento de software. |
| **Relevante (R)** | Recupera hasta **1,000 minutos anuales de instrucción por sección**, alineado con los objetivos estratégicos institucionales de calidad educativa. |
| **Tiempo definido (T)** | Despliegue completo en **16 semanas**, desde el diagnóstico hasta el piloto en producción. |

### Metas de Disponibilidad del Servicio

- **Disponibilidad del sistema ≥ 99 %**, garantizando continuidad del servicio de registro durante la jornada académica.
- **Cero interrupciones pedagógicas activas**: el proceso de asistencia se ejecuta de forma pasiva, sin requerir intervención docente.

## 2.2 Análisis de Alternativas

Se evaluaron cinco alternativas tecnológicas para la resolución del problema de control de asistencia, utilizando una matriz comparativa multicriterio.

### Matriz Comparativa de Alternativas

| Criterio | Lista Manual | Lista Web | Código QR | Huella Digital | **Visión por Computadora (Propuesta)** |
|---|---|---|---|---|---|
| **Fricción por sesión** | Alta (5–10 min) | Media (requiere login) | Media (requiere escaneo activo) | Media-Alta (fila, contacto físico) | **Cero** (pasiva, en segundo plano) |
| **Dependencia de hardware del usuario** | No (papel) | Sí (dispositivo con navegador) | Sí (smartphone propio) | Sí (lector biométrico dedicado por aula) | **No** (una sola cámara por aula) |
| **Riesgo de suplantación** | Alto (respuesta verbal) | Alto (login compartido) | Alto (QR transferible) | Bajo | **Bajo** (biometría facial 1:N) |
| **Higiene / contacto físico** | Bajo riesgo | Bajo riesgo | Bajo riesgo | Riesgo de contacto | Sin contacto |
| **Costo de licenciamiento** | Ninguno | Variable (SaaS) | Bajo | Medio-Alto (hardware propietario) | **US$ 0** (Open Source) |
| **Escalabilidad por sección** | Nula | Media | Media | Baja (cuello de botella por fila) | **Alta** (procesamiento por lotes) |
| **Trazabilidad y auditoría** | Nula/manual | Media | Media | Alta | **Alta** (timestamp + embedding cifrado) |
| **Inclusión pasiva del alumno** | No aplica | No (requiere acción) | No (requiere acción) | No (requiere acción) | **Sí** (no requiere acción del estudiante) |

### Conclusión del Análisis

La alternativa de **Visión por Computadora** es la única opción que logra **fricción estructural cero** para el docente y **no exige que el estudiante posea o manipule un dispositivo o credencial adicional** (a diferencia del código QR o la huella digital, que trasladan la carga operativa al usuario final). Esta característica la posiciona como la alternativa **estratégicamente superior**, al eliminar simultáneamente la interrupción de clase y la dependencia de hardware individual.

## 2.3 Evaluación de Beneficios

### 2.3.1 Beneficios Tangibles

| Beneficio | Descripción | Métrica |
|---|---|---|
| Recuperación de tiempo de instrucción | Eliminación de la interrupción activa del pase de lista | Hasta **1,000 min/año por sección** |
| Reducción de carga administrativa docente | El docente deja de ejecutar tareas de registro manual | 100 % de las sesiones automatizadas |
| Reducción de errores de registro | Eliminación de doble digitación y errores de transcripción | Disminución del margen de error humano |

### 2.3.2 Beneficios Intangibles

- **Modernización de la imagen institucional**, al posicionar a la institución como adoptante de tecnologías de inteligencia artificial aplicada.
- **Mejora del clima de aula**, al eliminar interrupciones recurrentes del flujo pedagógico.
- **Fortalecimiento de la cultura de datos**, mediante la generación de registros confiables y auditables para la gestión académica.
- **Valor reputacional en procesos de acreditación**, al demostrar innovación tecnológica con enfoque ético y de cumplimiento normativo.

## 2.4 Estimación de Costos

Uno de los pilares centrales de la viabilidad del proyecto es su **bajo costo total de propiedad (TCO)**, sustentado en dos decisiones de arquitectura:

### 2.4.1 Stack 100 % Open Source

| Componente | Tecnología | Costo de Licencia |
|---|---|---|
| Aplicación móvil | Flutter 3 | US$ 0 |
| API principal | Laravel 11 (JWT) | US$ 0 |
| Motor de IA | Python + FastAPI | US$ 0 |
| Base de datos | MySQL 8 | US$ 0 |
| Contenerización | Docker | US$ 0 |
| Sistema operativo | Ubuntu Server | US$ 0 |
| **Total en licenciamiento de software** | — | **US$ 0** |

### 2.4.2 Eficiencia de Hardware

- **No se requiere GPU**: el pipeline de inferencia (YOLOv8-Face + ArcFace R100) está optimizado para ejecución sobre **CPU estándar**, eliminando la principal barrera de costo de los sistemas de visión por computadora convencionales.
- **Hardware mínimo requerido**: CPU Intel i5 / AMD Ryzen equivalente, 8 GB de RAM y webcam de 720p — especificaciones ya presentes en la mayoría de los laboratorios y equipos institucionales existentes.
- **Costo marginal de escalamiento bajo**: replicar la solución en aulas adicionales solo requiere una webcam 720p y un equipo de gama estándar, sin inversión incremental en licenciamiento.

!!! success "Conclusión de Viabilidad Económica"
    Al eliminar tanto el costo de licenciamiento de software como la necesidad de hardware especializado (GPU), el proyecto presenta una de las relaciones **costo-beneficio más favorables** dentro de las alternativas tecnológicas evaluadas, con una inversión concentrada casi exclusivamente en horas de desarrollo e implementación.

## 2.5 Riesgos Iniciales

| Riesgo | Descripción | Estrategia de Mitigación |
|---|---|---|
| **Baja iluminación en el aula** | Condiciones lumínicas deficientes pueden degradar la precisión de detección facial. | Uso de modelos de IA avanzados (YOLOv8-Face) con robustez ante condiciones de iluminación variable, complementado con recomendaciones de ubicación de cámara. |
| **Privacidad y protección de datos biométricos** | El procesamiento de rostros constituye datos personales sensibles bajo marcos regulatorios de protección de datos. | Implementación de una **Bóveda Digital (Digital Vault)**: no se almacenan fotografías, únicamente **embeddings matemáticos cifrados de 512 dimensiones**, no reversibles a imagen original. |
| **Resistencia al cambio (docentes/estudiantes)** | Adopción de un sistema biométrico puede generar reticencia inicial. | Plan de comunicación institucional y política de transparencia sobre el tratamiento de datos, alineada a **ACM Code of Ethics**. |
| **Dependencia de conectividad** | Fallos de red podrían interrumpir el registro. | Arquitectura desplegada sobre **red LAN aislada** (*air-gapped*), sin dependencia de conectividad a internet externa. |

---

**Entregable anterior:** [Entregable 1 — Diagnóstico Organizacional](entregable1_diagnostico.md)
**Siguiente entregable:** [Entregable 3 — Plan de Gestión del Proyecto (PMBOK)](entregable3_plan_gestion.md)
