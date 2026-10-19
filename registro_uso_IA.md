# Registro de uso de IA generativa — Laboratorio 3

**Herramienta:** Claude Code (modelo Claude Opus 5.5, Anthropic), extensión de VS Code.

**Tipo de uso:** generación de código repetitivo (exploración, pipelines, grids, gráficas), revisión de documentación de librerías (cambios de API en scikit-learn 1.9) y apoyo en redacción. Las decisiones metodológicas las tomó el equipo; la IA presentó opciones con sus ventajas y desventajas.

## Prompts principales

1. *"Tengo que hacer el siguiente laboratorio, las instrucciones completas están en el .md, la rúbrica está en el .pdf y tenemos la data en la carpeta Data. Quiero que revises todo y empecemos a trabajar. Fíjate que el .md especifica que si voy a usar inteligencia artificial no solo la debo declarar sino también debo yo tomar las decisiones importantes, así que tú vas a hacer todo lo repetitivo y en el momento que haya que tomar una decisión es cuando vas a pedir mi input. Guíate del repo de la clase: https://github.com/ISIS-2611-AprendizajeMaquina/MaterialDeClase-ISIS-2611.git"*

## Decisiones tomadas por el equipo (la IA propuso opciones; el equipo eligió)

| Momento | Pregunta planteada | Opciones presentadas | Decisión del equipo |
|---|---|---|---|
| Limpieza | Tratamiento de nulos en `frecuencia_*` (1–2%) | Imputar moda en pipeline / eliminar filas / categoría "Sin información" | Imputar con la moda dentro del pipeline |
| Limpieza | Columnas a eliminar | `vehiculo`, `tiempo_cupon_mayor_5min`, `direccion_opuesta`, `temperatura` | Las cuatro (más `cupon`, que es constante por subconjunto) |
| Preparación | Codificación de categóricas | Ordinal + One-Hot / One-Hot para todo | Ordinal (orden del diccionario) + One-Hot nominales |
| Modelado | Métrica de la búsqueda de hiperparámetros | F1 clase "Sí" / F1-macro | F1-macro |
| Limpieza | Duplicados (7 por subconjunto) | Eliminar / mantener | Eliminar |
| Modelado | Partición y folds | 80/20 + 5 folds / 80/20 + 10 folds / 75/25 + 5 folds | 80/20 estratificado, 5 folds |
| Modelado | Rangos de hiperparámetros | Grid amplio / grid reducido (como en las prácticas) | Grid amplio |
| Balanceo | Técnica de balanceo | SMOTENC / SMOTE clásico / ambas | SMOTENC (las variables son categóricas) |
| Balanceo | Alcance del balanceo | Los 3 algoritmos / solo el mejor | Los 3 algoritmos |

## Continuación con Codex (OpenAI), 19 de octubre de 2026

**Tipo de uso:** revisión del enunciado, rúbrica y prácticas P1, P2, P7, P8, P9 y P10 de `202620/Prácticas`; adecuación del notebook existente, ejecución, depuración, redacción del análisis y exportación de entregables.

**Prompt principal (resumen):** «Leer muy bien Laboratorio 3_Clasificación.md y la rúbrica del PDF; continuar Lab3_Clasificacion.ipynb respetando los avances del compañero; basarse obligatoriamente en las prácticas del repositorio ISIS-2611; adaptar el código para cumplir la rúbrica, redactar explicaciones buenas pero breves y correr el notebook con los datos de /Data». El estudiante indicó además que su nombre es Daniel Vergara.

**Análisis crítico de la asistencia:**

- Resultó útil reutilizar el patrón de `ColumnTransformer`, pipelines, partición estratificada, `GridSearchCV` y métricas de las prácticas. Se conservaron la partición 80/20, los cinco folds, F1-macro y los grids amplios del avance.
- Se corrigió el tratamiento del balanceo: el avance usaba SMOTENC interpolando categorías ordinales como continuas. Al quedar únicamente variables categóricas, Codex propuso SMOTEN antes de codificarlas. Conserva categorías válidas, pero no garantiza todas las restricciones conjuntas ni explota su orden. Esta es una adaptación propuesta por IA, no una nueva decisión que se atribuya al equipo.
- Se matizó la interpretación de los coeficientes: un indicador One-Hot y una ordinal estandarizada no tienen la misma unidad. La importancia predictiva tampoco demuestra causalidad. Estos límites se explicitan en el notebook.
- La selección se realiza con validación cruzada de entrenamiento; test se usa para reportar resultados. El reajuste final con todos los datos etiquetados se hace después de evaluar. Las predicciones externas no tienen etiquetas disponibles y no se les atribuye un F1 observado.

**Aportes humanos y revisión pendiente:** el notebook y las decisiones de la tabla anterior fueron aportados por el equipo, según el registro preexistente. Daniel solicitó la continuación y definió las fuentes obligatorias y el estilo de redacción. El código añadido y la primera versión de las conclusiones de esta continuación fueron elaborados con Codex. Antes de entregar, los integrantes deben revisar que comprenden las decisiones y completar con sus propias palabras qué modificaron y qué aprendieron; esa revisión y esos aprendizajes no pueden darse por realizados automáticamente.

**Conceptos para esa revisión:** fuga de información, validación cruzada estratificada, diferencia entre F1 positivo y macro, precisión/recall de la clase minoritaria, regularización, sobreajuste e interpretación no causal.
