# Entregable 1 — Diagnóstico Organizacional y Alineamiento Estratégico

## 1.1 Contexto Organizacional

La institución educativa objeto del presente estudio opera bajo un modelo de gestión académica tradicional, en el cual el **control de asistencia** constituye un proceso administrativo transversal a todas las secciones, niveles y jornadas. Este proceso, aparentemente menor en la superficie operativa, representa en la práctica un **punto de fricción estructural** que se repite de manera sistemática en cada sesión de clase, multiplicado por el número de secciones, docentes y periodos lectivos del calendario académico.

El entorno educativo actual se caracteriza por:

- **Alta carga administrativa docente**, donde el profesorado debe compatibilizar funciones pedagógicas con tareas de registro y control.
- **Procesos manuales no digitalizados** en la gestión de asistencia, heredados de esquemas de gestión académica pre-digitales.
- **Ausencia de trazabilidad automática** de los datos de asistencia, lo que limita la capacidad de análisis institucional en tiempo real.
- **Presión creciente** por parte de organismos reguladores y de acreditación para demostrar el aprovechamiento efectivo del tiempo de instrucción.

En este contexto, el **Área de Gestión de Tecnologías de Información (GTI)** ha sido convocada para diagnosticar la raíz tecnológica del problema y proponer una solución fundamentada en **visión por computadora** e **inteligencia artificial aplicada**.

## 1.2 Análisis Estratégico

La optimización del tiempo de instrucción se encuentra **directamente alineada** con los objetivos estratégicos institucionales en materia de calidad educativa, eficiencia operativa y modernización tecnológica. El análisis estratégico identifica las siguientes líneas de conexión:

| Objetivo Institucional | Aporte del Proyecto |
|---|---|
| **Maximizar el tiempo efectivo de instrucción** | Elimina la fricción del pase de lista manual, devolviendo minutos de clase al proceso de enseñanza-aprendizaje. |
| **Modernización tecnológica institucional** | Introduce un ecosistema de IA aplicada (visión por computadora, biometría) como estándar de gestión académica. |
| **Fortalecimiento de la gobernanza de datos** | Genera trazabilidad automática y auditable de la asistencia, insumo para la toma de decisiones basada en evidencia. |
| **Sostenibilidad financiera de la innovación** | Adopta un stack **100 % Open Source**, sin costos de licenciamiento, compatible con hardware ya disponible en la institución. |
| **Cumplimiento normativo y ético** | Incorpora desde el diseño principios de protección de datos personales conforme a **ISO 27001** y al código de ética de **ACM**. |

Desde la perspectiva del **Balanced Scorecard institucional**, el proyecto impacta simultáneamente la perspectiva de **procesos internos** (automatización), la perspectiva de **aprendizaje y crecimiento** (adopción tecnológica) y, de forma indirecta, la perspectiva **financiera** (uso más eficiente del tiempo docente, un recurso de costo de oportunidad elevado).

## 1.3 Diagnóstico Digital / TI

El diagnóstico técnico del proceso actual de control de asistencia revela deficiencias estructurales que trascienden la simple incomodidad operativa:

### 1.3.1 Vulnerabilidad Verbal del Registro Manual

El pase de lista tradicional, ejecutado mediante la lectura en voz alta de nombres o el paso físico de una hoja de firmas, presenta las siguientes vulnerabilidades:

- **Suplantación de identidad simple**: la respuesta verbal ("presente") no garantiza la identidad real del estudiante, permitiendo que un compañero responda por otro (*proxy attendance*).
- **Falsificación de firmas** en listados físicos, sin mecanismo de verificación biométrica.
- **Ausencia de sello temporal (timestamp) confiable**, lo que dificulta auditar tardanzas reales frente a registros ajustados manualmente.

### 1.3.2 Interrupción del Proceso Pedagógico

- Cada sesión de clase sufre una **interrupción activa de 5 a 10 minutos**, tiempo durante el cual el proceso de enseñanza se detiene por completo.
- La interrupción no es un evento aislado: se repite en **cada sesión**, para **cada sección**, durante **todo el periodo lectivo**, generando un efecto acumulativo significativo.
- El proceso manual **no escala**: a mayor número de estudiantes por sección, mayor es el tiempo de fricción, sin que exista un mecanismo tecnológico que lo compense.

### 1.3.3 Ausencia de Infraestructura de Datos

- No existe una fuente única de verdad (*single source of truth*) digital para los registros de asistencia.
- La información, cuando se digitaliza, se realiza de forma posterior y manual (doble digitación), incrementando el riesgo de error humano y el costo administrativo oculto.

## 1.4 Identificación del Problema

### 1.4.1 Cuantificación del Impacto

El diagnóstico cuantitativo del **Área de GTI** establece la siguiente línea base:

| Variable | Valor |
|---|---|
| Tiempo de fricción por sesión de clase | 5 – 10 minutos |
| Pérdida estimada de instrucción anual por sección | **1,000 minutos** |
| Equivalente en horas de instrucción perdidas por sección/año | ≈ 16.6 horas |
| Naturaleza de la pérdida | **Estructural y recurrente**, no un evento excepcional |

### 1.4.2 Justificación de la Cifra

La pérdida de **1,000 minutos anuales por sección** se deriva de la repetición sistemática de la fricción de 5 a 10 minutos en cada sesión de clase, multiplicada por el número de sesiones que conforman un periodo lectivo completo. Al tratarse de un fenómeno **estructural** —es decir, inherente al diseño del proceso actual y no a fallas puntuales de ejecución— la pérdida **no es mitigable mediante capacitación o disciplina docente**, sino únicamente mediante un **rediseño tecnológico del proceso**.

### 1.4.3 Impacto Institucional

- **Impacto pedagógico**: reducción directa del tiempo disponible para el desarrollo curricular, con efecto acumulativo sobre el logro de los aprendizajes esperados.
- **Impacto en el clima de aula**: las interrupciones recurrentes fragmentan la continuidad didáctica y afectan la gestión del tiempo docente.
- **Impacto en la calidad del dato institucional**: los registros de asistencia, al depender de un proceso manual vulnerable, presentan baja confiabilidad para la toma de decisiones (por ejemplo, identificación temprana de riesgo de deserción).
- **Impacto en la percepción de modernización institucional**: la persistencia de procesos análogos en un entorno educativo contemporáneo constituye una brecha digital frente a instituciones comparables.

!!! warning "Conclusión del Diagnóstico"
    El problema identificado no es un déficit de disciplina o de gestión docente, sino un **déficit tecnológico estructural**. La solución, por tanto, debe originarse desde el **Área de Gestión de Tecnologías de Información**, mediante la introducción de un sistema automatizado, biométrico y de fricción cero, que se desarrolla en los entregables subsiguientes.

---

**Siguiente entregable:** [Entregable 2 — Business Case del Proyecto](entregable2_business_case.md)
