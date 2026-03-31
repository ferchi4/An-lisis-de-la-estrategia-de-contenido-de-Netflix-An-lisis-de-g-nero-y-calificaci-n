# **Proyecto:  de Estrategia de Contenido de Netflix**

Este proyecto se centra en el análisis estratégico del catálogo de Netflix mediante el procesamiento de metadatos de títulos (películas y series). El análisis cubre tendencias de género, ratings, duración, países de origen y características de autorización, con un enfoque en clasificación automática (Movie vs TV Show) y recomendaciones de producto.

**Objetivo**

El proyecto se estructura en las siguientes fases principales:

1. **Carga y validación de datos:** Importar dataset local `netflix_titles.csv`, auditoría de calidad y limpieza.
2. **Exploración inicial (EDA):** Analizar distribución de géneros, ratings, países, años y duración.
3. **Ingeniería de características:** Crear variables clave (duración numérica, edad de contenido, indicadoras de género, etc.).
4. **Modelado clasificatorio:** Entrenar y comparar RandomForest, XGBoost y LightGBM para predecir tipo de contenido.
5. **Interpretabilidad:** Usar SHAP para explicar predicciones y priorizar métricas de contenido.
6. **Insights estratégicos:** Generar recomendaciones de contenido premium, focalización internacional y engagement.
7. **Reporte final:** Guardar resultados y gráficos en `results/`, además de documentar hallazgos.

** Tecnologías Utilizadas**

* **Python:** Lenguaje principal para análisis y pipeline.
* **SQL:** Opcional para procesamiento inicial, con soporte de pandas.
* **Pandas:** Manipulación y transformación de datos.
* **scikit-learn:** Modelado, preprocesado y validación.
* **XGBoost, LightGBM:** Modelos avanzados boosteados.
* **SHAP:** Interpretabilidad de machine learning.
* **Matplotlib/Seaborn/Plotly:** Visualización y dashboards.
* **Jupyter Notebook:** Entorno interactivo para la experimentación.

**Pasos Clave**

1. **Carga de datos y verificación:**
   - Cargar `data/raw/netflix_titles.csv`.
   - Validar presencia de columnas y valores faltantes.
   - Asegurar que no existan duplicados en `show_id`.

2. **Auditoría de estructuras y métricas:**
   - Describir 12 columnas clave de metadatos.
   - Detectar 66 valores NA y tratarlos con reglas de imputación.

3. **Transformaciones iniciales:**
   - Convertir `date_added` a fecha y extraer año/mes.
   - Mapear `duration` en minutos/temporadas y crear `effective_duration`.
   - Codificar ratings y variables categóricas.

4. **Consulta 1 - Contenido post-2000:**
   - Identificar títulos con `release_year >= 2000`.
   - 81.9% del catálogo es moderno (ejercicio de ejemplo similar de libros).

5. **Consulta 2 - Interacción y rating:**
   - Agregar análisis de calificaciones por título y por tipo.
   - Calcular promedio de rating y desviación estándar.

6. **Consulta 3 - Editoriales y producción:**
   - Analizar `country` y `listed_in` para detectar mercados clave.
   - Identificar contenido relevante en mercados internacionales.

7. **Consulta 4 - Autoridad de contenido:**
   - Usar modelos para estimar importancia de características.
   - Detectar features en top 5: `duration_seasons`, `duration_numeric`, `duration_mins`, `has_director`, `genre_International_Movies`.

8. **Consulta 5 - Segmentación de usuarios (estilo recomendaciones):**
   - Usar `RANDOM_STATE` para reproducibilidad.
   - Generar predicciones y evaluar en conjunto de prueba (80/20).

**Resultados**

El análisis revela que:

- **Cobertura de Datos:** 76 títulos, 43 Movies y 33 TV Shows.
- **Modernización Editorial:** Alto porcentaje de contenido post-2000.
- **Interacción de usuarios:** Métricas de rating y duration para segmentación.
- **Dominancia de contenido internacional:** Géneros internacionales líderes.
- **Modelo Destacado:** RandomForest con test accuracy 100% en dataset pequeño.

**Recomendaciones Estratégicas**

1. **Foco en contenido de alta duración y series:** Mantener la promoción en top features de duración y valores de rating.
2. **Enriquecer metadatos internacionales:** Potenciar selección, soporte y marketing para multiregiones.
3. **Optimizar referencias de rating:** Promover títulos con ratings >4.0 y variación estable.
4. **Gamificación de engagement:** Incentivar reseñas y calificaciones (modelo similar a libros con contenido de usuario activo).
5. **Curación basada en SHAP:** Publicar colecciones temáticas a partir de features de mayor impacto.

**Cómo Ejecutar el Proyecto**

1. Clona el repositorio:
   ```bash
   git clone <URL_DEL_REPOSITORIO>
   cd netflix-analysis
   ```

2. Crea y activa entorno virtual:
   ```bash
   python -m venv venv
   venv\Scripts\activate    # Windows
   source venv/bin/activate  # Linux/Mac
   ```

3. Instala dependencias:
   ```bash
   pip install -r requirements.txt
   ```

4. Ejecuta el notebook:
   ```bash
   jupyter notebook notebooks/analysis.ipynb
   ```

5. Corre celdas en orden para reproducir el análisis completo.

**Notas Importantes**

- El dataset debe estar en `data/raw/netflix_titles.csv`.
- Los resultados de `results/` pueden estar vacíos si no se guardaron explícitamente (configurar en notebook para exportar CSV/PNG).
- Asegura usar el kernel con paquetes instalados (`xgboost`, `lightgbm`, `shap`).
