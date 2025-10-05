# Segmentación y Detección de Anomalías en Pacientes Crónicos

Este proyecto implementa un pipeline completo de **análisis exploratorio no supervisado** sobre un dataset clínico de pacientes, combinando técnicas avanzadas de reducción de dimensionalidad, clustering y detección de anomalías. El objetivo es identificar grupos de pacientes con características similares, detectar perfiles atípicos y analizar la coherencia entre distintos métodos de agrupamiento y outlier detection, todo con justificación clínica y visualización detallada.

---

## Tabla de Contenidos

- [Segmentación y Detección de Anomalías en Pacientes Crónicos](#segmentación-y-detección-de-anomalías-en-pacientes-crónicos)
  - [Tabla de Contenidos](#tabla-de-contenidos)
  - [Objetivo](#objetivo)
  - [Tecnologías y Librerías](#tecnologías-y-librerías)
  - [Pipeline de Análisis](#pipeline-de-análisis)
    - [Importación y Preprocesamiento](#importación-y-preprocesamiento)
    - [Reducción de Dimensionalidad](#reducción-de-dimensionalidad)
    - [Clustering No Supervisado](#clustering-no-supervisado)
      - [Métricas de Evaluación](#métricas-de-evaluación)
    - [Detección de Anomalías](#detección-de-anomalías)
    - [Análisis Cruzado](#análisis-cruzado)
  - [Resultados y Métricas](#resultados-y-métricas)
    - [Clustering](#clustering)
    - [Detección de Anomalías](#detección-de-anomalías-1)
  - [Visualizaciones](#visualizaciones)
      - [Gráficos de dispersión en 2D para PCA, t-SNE y UMAP](#gráficos-de-dispersión-en-2d-para-pca-t-sne-y-umap)
      - [Comparación visual de clusters generados por DBSCAN y HDBSCAN](#comparación-visual-de-clusters-generados-por-dbscan-y-hdbscan)
      - [Visualización de pacientes atípicos detectados por Isolation Forest y One-Class SVM](#visualización-de-pacientes-atípicos-detectados-por-isolation-forest-y-one-class-svm)
  - [Interpretación y Aplicaciones](#interpretación-y-aplicaciones)
  - [CI/CD: Integración y Despliegue Continuos](#cicd-integración-y-despliegue-continuos)
    - [Proceso CI/CD recomendado](#proceso-cicd-recomendado)
    - [Ejemplo de flujo CI/CD](#ejemplo-de-flujo-cicd)
  - [Ejecutar el Notebook](#ejecutar-el-notebook)

---

## Objetivo

Aplicar técnicas avanzadas de aprendizaje no supervisado para:

- Identificar grupos de pacientes con condiciones clínicas similares.
- Visualizar segmentos en espacios de baja dimensión.
- Detectar perfiles atípicos.
- Analizar comparativamente distintos métodos de agrupamiento y anomalía.
- Justificar las decisiones en función del contexto clínico y los resultados obtenidos.

---

## Tecnologías y Librerías

El entorno está construido sobre Python y Jupyter Notebook, utilizando:

- **pandas** y **numpy**: Manipulación y análisis de datos.
- **scikit-learn**: Preprocesamiento, reducción de dimensionalidad, clustering y anomalía.
- **umap-learn**: Reducción de dimensionalidad avanzada.
- **hdbscan**: Clustering jerárquico.
- **matplotlib** y **seaborn**: Visualización.
- **kagglehub**: Descarga automática de datasets.
- **warnings**: Gestión de advertencias para una experiencia limpia.

---

## Pipeline de Análisis

### Importación y Preprocesamiento

- Descarga automática del dataset de diabetes desde Kaggle con `kagglehub`.
- Estandarización de los datos clínicos usando `StandardScaler` para asegurar comparabilidad entre variables.

### Reducción de Dimensionalidad

Se aplican tres técnicas para visualizar y analizar la estructura interna de los datos:

- **PCA**: Proyección lineal que maximiza la varianza explicada.
- **t-SNE**: Técnica no lineal que preserva relaciones locales, ideal para visualizar agrupamientos.
- **UMAP**: Proyección moderna que preserva tanto estructura local como global, eficiente en grandes volúmenes de datos.

Cada técnica genera un gráfico de dispersión en 2D, permitiendo comparar visualmente la agrupación y separación de los pacientes.

### Clustering No Supervisado

- **DBSCAN**: Algoritmo basado en densidad que detecta clusters y outliers sin requerir el número de grupos.
- **HDBSCAN**: Extensión jerárquica de DBSCAN, capaz de identificar clusters con densidades variables.
- **Optimización automática** de hiperparámetros para DBSCAN usando el índice de silueta.
- **Visualización comparativa** de los resultados de ambos algoritmos en el espacio t-SNE.

#### Métricas de Evaluación

- **Índice de Silueta**: Mide la cohesión y separación de los clusters (valores cercanos a 1 son mejores).
- **Davies-Bouldin**: Evalúa la compacidad y separación de los clusters (valores bajos son mejores).

### Detección de Anomalías

- **Isolation Forest**: Algoritmo basado en árboles aleatorios que identifica puntos fácilmente aislables como anomalías.
- **One-Class SVM**: Modelo de frontera que encapsula la mayoría de los datos normales y detecta desviaciones.
- Los resultados se etiquetan directamente en el DataFrame, mostrando cuáles son considerados atípicos por cada método.

### Análisis Cruzado

- **Comparación visual y cuantitativa** entre los pacientes detectados como ruido por HDBSCAN y los considerados anómalos por Isolation Forest.
- **Visualizaciones explicativas** que resaltan los outliers y clusters en el espacio reducido.
- **Conteo de coincidencias** para validar la robustez y coherencia entre métodos.

---

## Resultados y Métricas

### Clustering

| Método  | Índice de Silueta | Davies-Bouldin |
|---------|-------------------|----------------|
| DBSCAN  | 0.48              | 0.59           |
| HDBSCAN | 0.33              | 0.90           |

- **DBSCAN** mostró mejor calidad de agrupamiento que HDBSCAN según ambas métricas.
- Los gráficos muestran clusters más definidos y separados con DBSCAN.

### Detección de Anomalías

- **Isolation Forest:** Detecta **140** pacientes atípicos.
- **One-Class SVM:** Detecta **383** pacientes atípicos.
- **Coincidencias entre One-Class SVM (ruido) e Isolation Forest:** Solo **2** pacientes son detectados como atípicos por ambos métodos.

---

## Visualizaciones

El notebook incluye:

- Gráficos de dispersión en 2D para PCA, t-SNE y UMAP.
- Comparación visual de clusters generados por DBSCAN y HDBSCAN.
- Visualización de pacientes atípicos detectados por One-Class SVM e Isolation Forest.

Estas visualizaciones permiten interpretar fácilmente la estructura interna de los datos y la ubicación de los outliers.

#### Gráficos de dispersión en 2D para PCA, t-SNE y UMAP

![Gráficos de dispersión en 2D para PCA, t-SNE y UMAP](/images/pca_tsne_unam.png)

#### Comparación visual de clusters generados por DBSCAN y HDBSCAN

![Comparación visual de clusters generados por DBSCAN y HDBSCAN](/images/clusteres_hdbscan_dbscan.png)

#### Visualización de pacientes atípicos detectados por Isolation Forest y One-Class SVM

![Visualización de pacientes atípicos detectados por Isolation Forest y One-Class SVM](/images/cross_iso_svm.png)

---

## Interpretación y Aplicaciones

- **DBSCAN** es preferible para segmentar pacientes por su mejor desempeño en cohesión y separación.
- **Isolation Forest** es más interpretable y útil para identificar casos extremos clínicamente relevantes.
- **One-Class SVM** detecta más atípicos, pero su baja interpretabilidad requiere validación adicional.
- La baja coincidencia entre métodos sugiere que cada uno identifica diferentes tipos de casos atípicos.
- El pipeline es útil para análisis exploratorio de datos médicos, segmentación poblacional, detección temprana de casos de riesgo y validación de métodos no supervisados.

---

## CI/CD: Integración y Despliegue Continuos

El proyecto está preparado para integrarse en flujos de CI/CD (Integración y Despliegue Continuos), permitiendo automatizar la validación, pruebas y despliegue de los análisis y modelos.

### Proceso CI/CD recomendado

1. **Control de versiones**: El código y los notebooks se gestionan en un repositorio Git, permitiendo trazabilidad y colaboración.
2. **Pruebas automáticas**: Se pueden agregar pruebas unitarias para funciones clave (por ejemplo, validación de escalado, clustering y detección de anomalías).
3. **Validación de dependencias**: El archivo `requirements.txt` asegura que el entorno sea reproducible en cualquier máquina o servidor.
4. **Ejecución automatizada**: Mediante herramientas como GitHub Actions, Jenkins o GitLab CI, se puede configurar la ejecución automática del notebook en cada push o pull request, verificando que el pipeline se ejecuta correctamente y genera los resultados esperados.
5. **Generación de artefactos**: Los resultados, gráficos y métricas pueden guardarse automáticamente como artefactos (imágenes, CSV, reportes) en cada ejecución.
6. **Despliegue**: El notebook y los resultados pueden desplegarse en servidores de documentación, dashboards interactivos (por ejemplo, con Voila o Streamlit), o integrarse en sistemas de reporte clínico.
7. **Notificaciones**: El sistema puede enviar alertas automáticas si alguna etapa falla, si se detectan anomalías relevantes o si los resultados cambian significativamente.

### Ejemplo de flujo CI/CD

- **Push al repositorio** → **Ejecución automática del notebook** → **Validación de resultados y métricas** → **Generación de gráficos y reportes** → **Despliegue en dashboard o servidor** → **Notificación a los responsables**

Este enfoque asegura que el análisis sea **reproducible, escalable y confiable**, facilitando su integración en entornos clínicos, educativos o de investigación.

---

## Ejecutar el Notebook

1. Instala los requisitos del archivo `requirements.txt`.
2. Ejecuta el notebook `henzo_arrue_modular6.ipynb` en Jupyter o VS Code.
3. Sigue el flujo principal del pipeline para obtener visualizaciones y métricas.
4. Analiza los gráficos y resultados impresos para interpretar la segmentación y detección de anomalías.

---

**Autor**: Henzo Alejandro Arrué Muñoz

**Licencia**: GPLv3

---