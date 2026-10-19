# Guion de video — Ruta Alpes

**Julian Pinto y Daniel Vergara. Duración objetivo: 2:40–2:55.** Ensayar a ritmo natural y mantener el video por debajo de tres minutos. Mostrar las salidas indicadas. Este archivo es un guion, no el video final.

## 0:00–0:20 — Problema

Queremos ayudar a Ruta Alpes a ofrecer cupones relevantes y reducir notificaciones molestas. Construimos dos clasificadores independientes: Cafetería y Restaurante de menos de veinte. Cafetería tiene aproximadamente la mitad de aceptaciones; en Restaurante son cerca del 71%, por lo que identificar rechazos es especialmente importante.

## 0:20–0:50 — Preparación (mostrar secciones 1 y 2)

Revisamos nulos, duplicados, dominios y consistencia. Eliminamos vehículo por casi 99% de faltantes, columnas constantes y la dirección redundante; también conservamos la decisión de excluir temperatura, aunque pierde algo de información. Imputamos frecuencias con la moda y codificamos categorías dentro del pipeline. Separamos 80% para entrenamiento y 20% para test, estratificados, y buscamos hiperparámetros con cinco folds.

## 0:50–1:25 — Modelos (mostrar tabla de sección 7)

Comparamos regresión logística, árbol y Random Forest, siguiendo las prácticas del curso. Optimizamos F1-macro para dar el mismo peso a aceptar y rechazar. La selección por validación cruzada fue Random Forest para Cafetería y Random Forest + SMOTEN para Restaurante. En test obtuvimos F1-macro de 0.775 y 0.695, respectivamente. No confundimos el ajuste de entrenamiento con la capacidad de generalizar.

## 1:25–1:55 — Balanceo (mostrar tabla de sección 6)

Probamos los tres algoritmos con SMOTEN, una adaptación de SMOTE para variables categóricas, únicamente dentro de los folds de entrenamiento. Comparamos también recall y precisión de la clase No sobre el mismo test. La recomendación final es Random Forest + SMOTEN. Detectar más rechazos puede evitar molestias, pero una menor precisión de No también significa dejar de ofrecer cupones que serían aceptados.

## 1:55–2:20 — Interpretación (mostrar sección 8)

En Cafetería destacan frecuencia_cafeteria, destino; en Restaurante, ocupacion, hora. Lo medimos por la pérdida de F1 al permutar cada variable en el bosque. Las reglas del árbol permiten describir decisiones concretas, pero estas asociaciones no prueban causalidad ni explican exactamente todo el bosque.

## 2:20–2:50 — Recomendación y límites

Proponemos un piloto con límites de notificaciones, evaluación por grupos y seguimiento de aceptación y rechazo. La demografía puede reproducir sesgos de representación, y una encuesta no garantiza rendimiento en conducción real. Antes de usar probabilidades para elegir entre ofertas se debe revisar su calibración. Finalmente reajustamos los modelos elegidos con todos los datos etiquetados y exportamos las veinte predicciones, conservando las columnas y el orden originales. Declaramos el apoyo de IA en el notebook.
