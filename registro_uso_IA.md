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
