# Entregable 4 — Modelado de Procesos AS-IS / TO-BE

## 4.1 Proceso Actual (AS-IS)

### Narrativa del Flujo Manual

El proceso actual de control de asistencia se ejecuta de forma **manual y sincrónica** al inicio (o durante el desarrollo) de cada sesión de clase, siguiendo la siguiente secuencia:

1. El docente **interrumpe la actividad pedagógica en curso** para dar inicio al pase de lista.
2. El docente **lee en voz alta** el listado de estudiantes matriculados en la sección, o hace circular una **hoja de firmas física**.
3. Cada estudiante debe **responder verbalmente** ("presente") o **firmar manualmente** el registro, en el orden en que es nombrado o le llega la hoja.
4. El docente **anota manualmente** las inasistencias, tardanzas o incidencias observadas.
5. Al finalizar la sesión (o en un momento posterior), el docente o personal administrativo **transcribe o digitaliza** el registro físico a un sistema institucional, en muchos casos mediante **doble digitación**.

### Diagrama de Flujo AS-IS

```
[Inicio de clase]
      │
      ▼
[Docente interrumpe la clase] ── 5 a 10 min de fricción activa
      │
      ▼
[Lectura de lista / circulación de hoja de firmas]
      │
      ▼
[Respuesta verbal o firma de cada estudiante]
      │
      ▼
[Registro manual de inasistencias/tardanzas]
      │
      ▼
[Transcripción posterior al sistema institucional] ── riesgo de error humano
      │
      ▼
[Fin del proceso — clase reanudada con tiempo perdido]
```

### Características Críticas del Proceso AS-IS

| Característica | Descripción |
|---|---|
| **Naturaleza** | Activa, sincrónica, interruptora del flujo pedagógico |
| **Verificación de identidad** | Débil (respuesta verbal o firma, sin validación biométrica) |
| **Tiempo consumido** | 5 – 10 minutos por sesión |
| **Trazabilidad digital** | Nula o tardía (dependiente de digitación posterior) |
| **Escalabilidad** | Nula — el tiempo de fricción crece de forma proporcional al número de estudiantes |

## 4.2 Proceso Propuesto (TO-BE)

### Narrativa del Flujo Automatizado

El proceso propuesto reemplaza la interacción activa docente-estudiante por un **pipeline de visión por computadora pasivo**, que se ejecuta en segundo plano sin requerir la interrupción de la clase.

**Paso 1 — Captura en Red LAN**
Una cámara (webcam 720p) instalada en el aula, conectada a la **red LAN institucional aislada**, captura de forma continua o programada el video del aula durante el desarrollo de la sesión.

**Paso 2 — Detección Facial (YOLOv8-Face)**
El motor de inteligencia artificial, desplegado sobre **FastAPI**, procesa el flujo de video mediante el modelo **YOLOv8-Face**, identificando y delimitando (*bounding box*) cada rostro presente en el campo de visión de la cámara.

**Paso 3 — Vectorización Biométrica (ArcFace R100)**
Cada rostro detectado es procesado por el modelo **ArcFace R100**, que genera un **embedding matemático de 512 dimensiones** — una representación numérica única del rostro, no reversible a la imagen original.

**Paso 4 — Similitud Coseno contra Base de Datos (MySQL)**
El embedding generado se compara, mediante **similitud coseno**, contra los embeddings previamente registrados y cifrados en la base de datos **MySQL 8**. Si la similitud supera el umbral de confianza establecido (**precisión ≥ 90 %**), el estudiante es marcado automáticamente como **presente**, con sello temporal (*timestamp*) exacto, dentro del **throughput objetivo de ≤ 30 segundos por cada 30 estudiantes**.

### Diagrama de Flujo TO-BE

```
[Inicio de clase — sin interrupción]
      │
      ▼
[1. Captura de video vía cámara en Red LAN]
      │
      ▼
[2. Detección facial — YOLOv8-Face]
      │
      ▼
[3. Vectorización — ArcFace R100 → embedding 512-D]
      │
      ▼
[4. Comparación por Similitud Coseno contra MySQL 8]
      │
      ├── Similitud ≥ umbral ──► [Registro automático de asistencia + timestamp]
      │
      └── Similitud < umbral ──► [No coincidencia — sin registro / revisión]
      │
      ▼
[Fin del proceso — clase sin interrupción]
```

### Características Críticas del Proceso TO-BE

| Característica | Descripción |
|---|---|
| **Naturaleza** | Pasiva, asincrónica respecto a la actividad docente |
| **Verificación de identidad** | Fuerte — biometría facial 1:N mediante embeddings de 512 dimensiones |
| **Tiempo consumido por el docente** | 0 minutos (fricción cero) |
| **Trazabilidad digital** | Inmediata y automática, con timestamp exacto en base de datos |
| **Escalabilidad** | Alta — throughput definido (≤ 30 s por cada 30 estudiantes), independiente de la intervención humana |

## 4.3 Análisis Comparativo

### Cuantificación del Ahorro de Tiempo

| Indicador | AS-IS (Manual) | TO-BE (Reconocimiento Facial) | Mejora |
|---|---|---|---|
| Tiempo de fricción por sesión | 5 – 10 minutos | **~0 minutos** (procesamiento en segundo plano) | Reducción total de la interrupción activa |
| Pérdida anual de instrucción por sección | **1,000 minutos** | Cercana a 0 minutos | Recuperación de hasta **1,000 min/año por sección** |
| Verificación de identidad | Verbal / firma (débil) | Biométrica 1:N (fuerte) | Reducción sustancial del riesgo de suplantación |
| Disponibilidad de datos para gestión académica | Diferida (post-digitación) | Inmediata (tiempo real) | Trazabilidad en tiempo real |
| Intervención requerida del docente | Activa y obligatoria | **Ninguna** | Fricción cero para el cuerpo docente |
| Intervención requerida del estudiante | Activa (responder/firmar) | **Ninguna** | Inclusión pasiva del estudiante |

### Principios Clave del Rediseño

!!! success "Fricción Cero para el Docente"
    El proceso TO-BE **elimina por completo** la necesidad de que el docente ejecute, supervise o valide manualmente el pase de lista, devolviendo el 100 % del tiempo de clase a su propósito pedagógico original.

!!! success "Inclusión Pasiva del Alumno"
    A diferencia de soluciones basadas en QR o huella digital, el estudiante **no requiere ejecutar ninguna acción** (escanear, tocar, mostrar credencial) para ser registrado. El reconocimiento ocurre de manera **pasiva y no intrusiva**, simplemente por su presencia física en el aula dentro del campo de visión de la cámara.

### Conclusión del Análisis Comparativo

La transición del modelo AS-IS al modelo TO-BE representa un **rediseño estructural del proceso**, no una simple digitalización del formulario existente. El valor del proyecto reside precisamente en la **eliminación de la interacción humana como requisito del proceso**, sustituyéndola por un pipeline automatizado, auditable y de alta precisión, que opera de forma transparente al desarrollo normal de la clase.

---

**Entregable anterior:** [Entregable 3 — Plan de Gestión del Proyecto](entregable3_plan_gestion.md)
**Siguiente entregable:** [Entregable 5 — Propuesta de Solución TIC Integrada](entregable5_solucion_tic.md)
