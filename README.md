# INF3862 - Food & Activity Insights

Proyecto individual del curso **Plataformas Big Data para Data Science**,
Pontificia Universidad Católica de Chile (2026).

## Caso de uso

**Food & Activity Insights** es una propuesta de plataforma de datos orientada a
analizar la relación entre la actividad física registrada por dispositivos
wearable y las características nutricionales estimadas de las recetas de
Food.com que los usuarios declaran haber preparado.

El producto final contempla un dashboard que permita visualizar tendencias de
actividad física, hábitos alimenticios y métricas agregadas por usuario y
período.

**Alcance:** herramienta de análisis exploratorio, no destinada a
recomendaciones médicas ni evaluaciones clínicas.

## Entregas

| Entrega | Descripción                                                                   | Estado     |
| ------- | ----------------------------------------------------------------------------- | ---------- |
| **E1**  | Diseño de datos, fuentes, modelos OLTP/OLAP, consultas y arquitectura inicial | Completada |
| **E2**  | Ingesta, procesamiento, calidad de datos y pipeline reproducible              | Pendiente  |
| **E3**  | Producto analítico final, arquitectura y operación                            | Pendiente  |

### Entrega 1 — Diseño de datos

[Ver informe E1](entregas/E1/informe.pdf)

El informe contiene tres páginas de desarrollo y siete páginas de anexos,
incluyendo los modelos de datos y la arquitectura propuesta.

## Datos del proyecto

Los datasets utilizados corresponden a Food.com y a datos sintéticos de
dispositivos wearable proporcionados por el equipo docente.

### Estructura local

```text
datos_proyecto_INF3862/
├── foodcom/
│   ├── recipes.parquet
│   └── reviews.parquet
└── wearable/
    ├── LEEME.md
    ├── dispositivos.csv
    ├── comidas.csv
    ├── sesiones.jsonl
    └── mediciones/
        └── AAAA-MM-DD/
            └── HH.jsonl.gz
```

### Fuentes de información

**Food.com**

- `recipes.parquet`: catálogo de 522.517 recetas.
- `reviews.parquet`: 1.401.982 reseñas de usuarios.

**Wearable**

- `dispositivos.csv`: vinculación de relojes y usuarios.
- `mediciones/`: mediciones de actividad y frecuencia cardíaca, almacenadas por
  fecha y hora de recepción.
- `sesiones.jsonl`: actividades físicas registradas.
- `comidas.csv`: recetas que los usuarios declaran haber preparado.
- `LEEME.md`: diccionario de datos y descripción de formatos.

Los datos wearable se relacionan con Food.com mediante `AuthorId` y `RecipeId`,
según corresponda.

### Disponibilidad de los datasets

Los archivos de datos se encuentran disponibles localmente en
`datos_proyecto_INF3862/`.

Esta carpeta está excluida del repositorio público mediante `.gitignore`, por lo
que los datasets **no se distribuyen directamente en GitHub**.

Para reproducir el proyecto:

1. Obtener los datasets desde Canvas del curso.
2. Crear la carpeta `datos_proyecto_INF3862/` en la raíz del repositorio.
3. Ubicar los archivos respetando la estructura indicada anteriormente.
4. Ejecutar los procedimientos de preparación y análisis que se incorporarán en
   E2 y E3.

Fuente original:
[Food.com Recipes and Reviews — Kaggle](https://www.kaggle.com/datasets/irkaal/foodcom-recipes-and-reviews),
licencia CC0.

## Limitaciones de E1

La primera entrega corresponde a un diseño conceptual y no requiere ejecutar
código.

Aunque los datasets completos ya se encuentran disponibles, los conteos y
tamaños específicos de las fuentes wearable aún deben verificarse mediante un
análisis exploratorio.

Las proyecciones de crecimiento, frecuencias de actualización y requisitos de
latencia presentados en E1 corresponden a supuestos de diseño y no a resultados
experimentales.

Adicionalmente, la interpretación de las métricas nutricionales dependerá de la
validación de unidades, porciones y características de los datos originales.

## Próximas etapas

### E2 — Ingesta y procesamiento

- Inspeccionar y perfilar los datasets originales.
- Implementar un pipeline reproducible de extracción, transformación y carga.
- Normalizar los formatos de mediciones de ambos modelos de reloj.
- Identificar duplicados, valores faltantes y registros tardíos.
- Integrar actividad física, comidas y recetas.
- Ejecutar consultas analíticas y evaluar el procesamiento.

### E3 — Producto analítico y arquitectura final

- Construir el producto analítico definido para el caso de uso.
- Evaluar y justificar las plataformas tecnológicas.
- Documentar la arquitectura definitiva.
- Definir mecanismos de calidad, actualización y operación.

## Registro de decisiones

Las decisiones arquitectónicas, sus justificaciones y los cambios realizados
durante el proyecto se documentan en [`decisiones.md`](decisiones.md).

Este registro se actualizará a medida que evolucionen las entregas.
