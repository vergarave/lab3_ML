# Laboratorio 3 — Clasificación de cupones

**Integrantes:** Julian Pinto y Daniel Vergara.

## Entregables

- `Lab3_Clasificacion.ipynb`: notebook con código, gráficas, resultados y análisis.
- `Lab3_Clasificacion.html`: versión HTML con las salidas de ejecución.
- `Lab3_datos_Prueba.csv`: archivo original de prueba con la columna `acepta_cupon` añadida.
- `registro_uso_IA.md`: resumen del uso de IA (Claude Code y ChatGPT 6 Astra); la versión completa está en la sección 11 del notebook.
- `guion_video.md`: guion para grabar el video de máximo tres minutos; no sustituye el video.

## Reproducir

Se verificó con Python 3.12. Instalar `python -m pip install -r requirements.txt`, abrir el notebook desde esta carpeta y ejecutar todas las celdas en orden. Los archivos de entrada se conservan en `Data/`.

La validación cruzada tiene cinco folds y explora grids amplios. La carpeta `tmp/cache_pipeline/` se crea automáticamente para reutilizar transformaciones dentro de cada búsqueda. Puede borrarse sin afectar los entregables; al volver a ejecutar se reconstruye.

Para exportar nuevamente el HTML después de ejecutar:

```powershell
python -m nbconvert --to html --embed-images Lab3_Clasificacion.ipynb
```

Las referencias exactas a las prácticas de `202620/Prácticas` y las adaptaciones se encuentran al inicio del notebook. La selección usa F1-macro de validación cruzada; el test interno se reserva para evaluación y se reajusta el modelo final con todos los datos etiquetados para predecir el archivo externo.

Antes de la entrega, los integrantes deben revisar el análisis y el registro de aportes/aprendizajes propios, grabar el video y subir los archivos a Bloque Neón.
