# Segmentación y Detección de Anomalías en Pacientes Crónicos

Este proyecto implementa un pipeline completo de **análisis exploratorio no supervisado** sobre un conjunto de datos clínicos de pacientes, utilizando técnicas avanzadas de reducción de dimensionalidad, clustering y detección de anomalías. El objetivo principal es identificar grupos de pacientes con características similares, detectar perfiles atípicos y analizar la coherencia entre distintos métodos de agrupamiento y outlier detection.

---

## Objetivos

- **Segmentar pacientes** en grupos homogéneos según sus características clínicas.
- **Visualizar** los resultados en espacios de baja dimensión para facilitar la interpretación.
- **Detectar pacientes atípicos** mediante algoritmos robustos de anomalía.
- **Comparar y validar** los resultados entre métodos de clustering y detección de outliers.

---

## Pipeline de Análisis

El notebook sigue cuatro etapas principales:

### 1. Preprocesamiento y Reducción de Dimensionalidad

- **Carga automática del dataset** desde Kaggle usando `kagglehub`.
- **Estandarización** de los datos con `StandardScaler` para asegurar que todas las variables tengan media cero y desviación estándar uno.
- **Reducción de dimensionalidad** aplicando tres técnicas complementarias:
  - **PCA** (Análisis de Componentes Principales): Proyección lineal que maximiza la varianza explicada.
  - **t-SNE**: Técnica no lineal que preserva relaciones locales, ideal para visualizar agrupamientos.
  - **UMAP**: Proyección moderna que preserva tanto estructura local como global, eficiente en grandes volúmenes de datos.

### 2. Segmentación mediante Clustering

- **DBSCAN**: Algoritmo basado en densidad que detecta clusters y outliers sin requerir el número de grupos.
- **HDBSCAN**: Extensión jerárquica de DBSCAN, capaz de identificar clusters con densidades variables.
- **Optimización automática** de hiperparámetros para DBSCAN usando el índice de silueta.
- **Visualización comparativa** de los resultados de ambos algoritmos.

### 3. Detección de Anomalías

- **Isolation Forest**: Algoritmo basado en árboles aleatorios que identifica puntos fácilmente aislables como anomalías.
- **One-Class SVM**: Modelo de frontera que encapsula la mayoría de los datos normales y detecta desviaciones.
- **Etiquetado directo** en el DataFrame de pacientes, mostrando cuáles son considerados atípicos por cada método.

### 4. Análisis Cruzado

- **Comparación visual y cuantitativa** entre los pacientes detectados como ruido por HDBSCAN y los considerados anómalos por Isolation Forest.
- **Visualizaciones explicativas** que resaltan los outliers y clusters en el espacio reducido.
- **Conteo de coincidencias** para validar la robustez y coherencia entre métodos.

---

## Resultados y Métricas

- **DBSCAN** mostró mejor calidad de agrupamiento que HDBSCAN según el índice de silueta y Davies-Bouldin.
- **Isolation Forest** y **One-Class SVM** detectaron diferentes cantidades de pacientes atípicos, con baja coincidencia entre ambos y el ruido de HDBSCAN.
- El análisis cruzado permite identificar casos extremos que podrían requerir atención clínica especial.

---

## Tecnologías Utilizadas

- **Python** (Jupyter Notebook)
- **pandas**, **numpy**: Manipulación y análisis de datos.
- **scikit-learn**: Preprocesamiento, reducción de dimensionalidad, clustering y anomalía.
- **umap-learn**: Reducción de dimensionalidad avanzada.
- **hdbscan**: Clustering jerárquico.
- **matplotlib**, **seaborn**: Visualización.
- **kagglehub**: Descarga automática de datasets.

---

## Ejecución

1. Instala los requisitos del archivo `requirements.txt`.
2. Ejecuta el notebook `henzo_arrue_modular6.ipynb` en Jupyter o VS Code.
3. Sigue el flujo principal del pipeline para obtener visualizaciones y métricas.

---

## Interpretación y Aplicaciones

- El pipeline es útil para **análisis exploratorio de datos médicos**, segmentación poblacional, detección de casos extremos y validación de métodos no supervisados.
- Puede adaptarse fácilmente a otros datasets clínicos o de salud pública.
- Las visualizaciones y métricas permiten justificar decisiones en contextos clínicos y científicos.

---

## Autor

**Henzo Alejandro Arrué Muñoz**

---

## Licencia

GPLv3