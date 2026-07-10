# Sistema Inteligente de Control de Asistencia mediante Reconocimiento Facial

## Documentación del Área de Gestión de Tecnologías de Información (GTI)

Este sitio documenta, bajo los lineamientos de la guía **PMBOK** y los estándares **CDIO**, **ACM** e **ISO/IEC 27001**, el conjunto de entregables correspondientes a la iniciativa de automatización del control de asistencia mediante **visión por computadora** y **reconocimiento facial biométrico**.

---

## Resumen Ejecutivo

| Dimensión | Descripción |
|---|---|
| **Problema** | Pérdida estructural de **1,000 minutos anuales de instrucción por sección** debido a la fricción del pase de lista manual (5–10 min/clase). |
| **Solución** | Pipeline de visión por computadora basado en **YOLOv8-Face** (detección) y **ArcFace R100** (vectorización biométrica de 512 dimensiones). |
| **Stack Tecnológico** | Flutter 3 · Laravel 11 (JWT) · Python FastAPI · MySQL 8 · Ubuntu Server + Docker — **100 % Open Source**. |
| **Costo de Licencias** | **US$ 0**, sobre hardware estándar (CPU i5/Ryzen, 8 GB RAM, webcam 720p), **sin dependencia de GPU**. |
| **Plazo de Despliegue** | **16 semanas**, en 4 fases incrementales. |
| **Marco de Seguridad** | Red LAN aislada (*air-gapped*), cifrado de embeddings, cumplimiento **ISO 27001** y código de ética **ACM**. |

---

## Índice de Entregables

1. **[Entregable 1 — Diagnóstico Organizacional y Alineamiento Estratégico](entregable1_diagnostico.md)**
   Contexto institucional, análisis estratégico, diagnóstico digital y cuantificación del problema.

2. **[Entregable 2 — Business Case del Proyecto](entregable2_business_case.md)**
   Justificación SMART, análisis de alternativas, beneficios, costos y riesgos iniciales.

3. **[Entregable 3 — Plan de Gestión del Proyecto (PMBOK)](entregable3_plan_gestion.md)**
   Acta de constitución, alcance, cronograma, costos y gestión de riesgos.

4. **[Entregable 4 — Modelado de Procesos AS-IS / TO-BE](entregable4_procesos.md)**
   Flujo actual vs. flujo propuesto y análisis comparativo de eficiencia.

5. **[Entregable 5 — Propuesta de Solución TIC Integrada](entregable5_solucion_tic.md)**
   Arquitectura, ecosistema de información, gobernanza de seguridad y escalabilidad.

---

!!! info "Alcance de la documentación"
    Esta documentación se enfoca **estrictamente** en el área de **Gestión de Tecnologías de Información (GTI)**, cubriendo la planificación, arquitectura, seguridad y viabilidad técnico-económica de la solución, conforme a los criterios de evaluación académica basados en PMBOK, CDIO, ACM e ISO 27001.
