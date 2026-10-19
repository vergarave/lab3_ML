# Registro de uso de IA generativa — Laboratorio 3

**Integrantes:** Julian Pinto y Daniel Vergara. La versión completa de este registro está en la sección 11 del notebook.

## Herramientas y tipo de uso

| Herramienta | Tipo de uso |
|---|---|
| **Claude Code** (modelo Claude Opus 5.5, Anthropic) | Generación inicial del código repetitivo a partir de las prácticas P1, P2, P7–P10 (exploración, pipelines, grids, gráficas), consulta del cambio de API de scikit-learn 1.9 (`penalty` → `l1_ratio`), presentación de opciones para cada decisión, revisión del avance y apoyo en redacción. |
| **ChatGPT 6 Astra** (OpenAI) | Implementación de los cambios que indicó el equipo (SMOTEN), caché de transformaciones con `joblib.Memory` para reducir el tiempo de los grids, selección por CV y reajuste final, depuración, primera redacción del análisis y exportación de HTML/CSV. |

**Todas las decisiones de criterio las tomó el equipo.** La IA ayudó con lo repetitivo: trasladar el código de las prácticas del curso, implementar el pipeline y la caché, y ejecutar y depurar.

## Decisiones del equipo

| Decisión | Alternativas consideradas | Elección del equipo |
|---|---|---|
| Nulos en `frecuencia_*` | Imputar moda en pipeline / eliminar filas / categoría "Sin información" | Imputar moda dentro del pipeline |
| Columnas a eliminar | `vehiculo`, `tiempo_cupon_mayor_5min`, `direccion_opuesta`, `temperatura` | Las cuatro (más `cupon`) |
| Duplicados | Eliminar / mantener | Eliminar |
| Codificación | Ordinal + One-Hot / One-Hot para todo | Ordinal (orden del diccionario) + One-Hot |
| Métrica de búsqueda | F1 clase "Sí" / F1-macro | F1-macro |
| Partición y CV | 80/20 + 5 folds / 80/20 + 10 folds / 75/25 + 5 folds | 80/20 estratificado, 5 folds |
| Rangos de hiperparámetros | Grid amplio / grid reducido | Grid amplio |
| Técnica de balanceo | SMOTE / SMOTENC / SMOTEN | SMOTENC en el primer avance; **Daniel Vergara decidió cambiarlo a SMOTEN** y se lo indicó a ChatGPT 6 Astra para implementarlo |
| Alcance del balanceo | Los 3 algoritmos / solo el mejor | Los 3 algoritmos |
| Selección del modelo final | Por test / por F1-macro de CV | Por F1-macro de CV, con reajuste sobre todos los datos etiquetados |

## Prompts principales

**Claude Code**
1. *"Tengo que hacer el siguiente laboratorio, las instrucciones completas están en el .md, la rúbrica está en el .pdf y tenemos la data en la carpeta Data. Quiero que revises todo y empecemos a trabajar. Fíjate que el .md especifica que si voy a usar inteligencia artificial no solo la debo declarar sino también debo yo tomar las decisiones importantes, así que tú vas a hacer todo lo repetitivo y en el momento que haya que tomar una decisión es cuando vas a pedir mi input. Guíate del repo de la clase: https://github.com/ISIS-2611-AprendizajeMaquina/MaterialDeClase-ISIS-2611.git"*

2. *(Resumen)* Corregir la documentación de la decisión de SMOTEN, restaurar la exploración detallada, alinear versiones de librerías y regenerar el HTML.

**ChatGPT 6 Astra (resumen)**
1. *"Leer muy bien Laboratorio 3_Clasificación.md y la rúbrica del PDF; continuar Lab3_Clasificacion.ipynb respetando los avances del compañero; basarse obligatoriamente en las prácticas del repositorio ISIS-2611; adaptar el código para cumplir la rúbrica, redactar explicaciones buenas pero breves y correr el notebook con los datos de /Data."*
2. Reemplazar SMOTENC por SMOTEN en la sección de balanceo (decisión de Daniel).
3. Reducir el tiempo de ejecución de las búsquedas de hiperparámetros (resultó en la caché de transformaciones).

## Análisis crítico

- **Útil:** adaptación de pipelines, CV estratificada y métricas por clase de las prácticas. La caché no introduce fuga de datos, porque guarda cada transformación según sus datos y parámetros.
- **Errores corregidos:**
  - Claude escribió hallazgos exploratorios sin verificar (misma dirección en Restaurante; asociación `ocupacion`–`edad`).
  - ChatGPT 6 Astra atribuyó el cambio a SMOTEN a la IA, cuando fue decisión de Daniel, y dejó texto genérico y de relleno.
  - `penalty` está obsoleto en scikit-learn 1.9.
  - Entre Windows y macOS cambiaban algunos hiperparámetros en empates del grid (milésimas en CV), aun con las mismas versiones; las predicciones finales no cambiaron.
- **Conceptos del curso usados:** fuga de información, F1 positivo vs F1-macro, recall de la clase minoritaria, sobreajuste e interpretación no causal.
