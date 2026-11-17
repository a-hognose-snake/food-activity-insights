# Registro de decisiones - Food & Activity Insights

**Curso:** INF3862 · Plataformas Big Data para Data Science  
**Proyecto:** Food & Activity Insights  
**Última actualización:** 16 de noviembre de 2026  
**Etapa actual:** E1 - Diseño de datos

---

## 1. Propósito

Este documento registra las principales decisiones funcionales y arquitectónicas
del proyecto **Food & Activity Insights**, junto con las alternativas evaluadas,
sus justificaciones y las instancias previstas de revisión.

El objetivo es mantener la trazabilidad de las decisiones tomadas durante las
tres entregas del curso, permitiendo justificar cambios a partir de los
resultados obtenidos en las etapas de implementación y evaluación.

### Estados de las decisiones

| Estado          | Significado                                         |
| --------------- | --------------------------------------------------- |
| **Adoptada**    | Decisión incorporada al diseño actual.              |
| **Por validar** | Decisión propuesta que requiere evidencia empírica. |
| **Revisada**    | Decisión modificada a partir de nueva evidencia.    |
| **Descartada**  | Alternativa que deja de formar parte del diseño.    |

---

## 2. Registro de decisiones

### 2.1. Producto y alcance

| ID  | Fecha      | Decisión                                                                                         | Alternativa considerada                                 | Justificación                                                                                                                                              | Estado   | Revisión |
| --- | ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
| D01 | 2026-11-16 | Desarrollar un dashboard descriptivo de actividad física y recetas preparadas.                   | Sistema de recomendación o predicción personalizada.    | Permite entregar valor utilizando los datos disponibles, sin requerir etiquetas adicionales ni asumir el desempeño de un modelo predictivo.                | Adoptada | E3       |
| D02 | 2026-11-16 | Presentar las métricas nutricionales y de actividad como estimaciones descriptivas, no clínicas. | Calcular un balance energético como indicador de salud. | Las comidas pueden estar registradas parcialmente y el wearable estima el gasto energético. Es necesario validar porciones, unidades y cobertura temporal. | Adoptada | E2       |

### 2.2. Almacenamiento y modelamiento

| ID  | Fecha      | Decisión                                                             | Alternativa considerada                                       | Justificación                                                                                                                             | Estado   | Revisión |
| --- | ---------- | -------------------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
| D03 | 2026-11-16 | Utilizar un modelo relacional para el sistema operacional (OLTP).    | Base documental para todas las fuentes.                       | Las vinculaciones de dispositivos, usuarios y comidas requieren integridad referencial, consultas puntuales y transacciones consistentes. | Adoptada | E2       |
| D04 | 2026-11-16 | Conservar las mediciones originales en JSONL comprimido.             | Almacenar únicamente los registros transformados.             | Permite reprocesar información, auditar sincronizaciones y corregir cambios de esquema o problemas de calidad sin perder el origen.       | Adoptada | E2       |
| D05 | 2026-11-16 | Diseñar dos tablas de hechos: actividad diaria y eventos de comidas. | Una única tabla que combine actividad y comidas directamente. | Mantiene granularidades independientes y evita duplicaciones de métricas cuando existen varias comidas o actividades por usuario y día.   | Adoptada | E2       |
| D06 | 2026-11-16 | Utilizar Parquet como formato principal de almacenamiento analítico. | CSV como formato principal.                                   | Su representación columnar favorece la compresión, la lectura selectiva de atributos y las consultas históricas con agregaciones.         | Adoptada | E2       |

### 2.3. Procesamiento y arquitectura

| ID  | Fecha      | Decisión                                                           | Alternativa considerada                                | Justificación                                                                                                                                                | Estado      | Revisión |
| --- | ---------- | ------------------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------- | -------- |
| D07 | 2026-11-16 | Comenzar con procesamiento local, sin infraestructura distribuida. | Implementar Hadoop o Spark desde el inicio.            | Todavía no existe evidencia de que los datos superen la capacidad de una máquina o de que el procesamiento distribuido aporte beneficios suficientes.        | Por validar | E2       |
| D08 | 2026-11-16 | Actualizar los indicadores analíticos diariamente.                 | Procesamiento y actualización integral en tiempo real. | Las tendencias históricas no requieren latencias de segundos. Un procesamiento batch simplifica la arquitectura inicial y reduce la complejidad operacional. | Por validar | E2       |

---

## 3. Principios de diseño

Las decisiones anteriores siguen cuatro principios que orientarán la evolución
del proyecto.

**Simplicidad justificada.** Priorizar soluciones que respondan directamente a
los requisitos del caso de uso, evitando incorporar tecnologías sin una
necesidad demostrada.

**Separación operacional y analítica.** Distinguir entre operaciones
transaccionales que requieren consistencia y baja latencia, y consultas
históricas que necesitan procesamiento eficiente de grandes conjuntos de datos.

**Calidad y trazabilidad.** Conservar los registros originales, identificar
problemas de ingesta y permitir el reprocesamiento de datos cuando sea
necesario.

**Evolución basada en evidencia.** Revisar las decisiones iniciales utilizando
mediciones de volumen, rendimiento, calidad y complejidad obtenidas durante las
entregas posteriores.

---

## 4. Plan de revisión

| Entrega                                | Decisiones por revisar           | Evidencia esperada                                                                                             |
| -------------------------------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **E1 — Diseño de datos**               | D01–D08                          | Objetivo, modelo de datos, consultas y arquitectura conceptual.                                                |
| **E2 — Ingesta y procesamiento**       | D02–D08                          | Perfilamiento de datos reales, pipeline, validaciones de calidad, tiempos de ejecución y análisis de formatos. |
| **E3 — Producto y arquitectura final** | D01 y decisiones revisadas en E2 | Producto analítico, evaluación de plataformas y propuesta de operación.                                        |

Las decisiones pueden mantenerse, modificarse o descartarse según los resultados
obtenidos. Cualquier cambio deberá conservar su justificación original y
registrar la nueva evidencia.

---

## 5. Historial de cambios

| Fecha      | Entrega | Cambio                                                                           |
| ---------- | ------- | -------------------------------------------------------------------------------- |
| 2026-11-16 | E1      | Creación del registro inicial con ocho decisiones funcionales y arquitectónicas. |

---

_Este documento forma parte del repositorio público del proyecto y se
actualizará durante E2 y E3._
