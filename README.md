# Proyecto TFM - Segmentación de Clientes y Modelos Predictivos

Este repositorio contiene el código y la documentación del Trabajo Final de Máster (TFM) realizado como parte del Máster en Ciencia de Datos e Inteligencia Artificial en Nucleus Digital School. El proyecto se centra en la segmentación de clientes y la creación de modelos predictivos para campañas de marketing, aprovechando técnicas avanzadas de ciencia de datos.

## Objetivo del Proyecto

El objetivo principal es realizar una segmentación de 10 mil clientes en cuatro grupos o clusters, y posteriormente construir modelos predictivos para identificar aquellos clientes con mayor probabilidad de compra en tres grupos de productos: **Financing**, **Investment**, y **Accounts**. A partir de los resultados, se busca optimizar una campaña de marketing personalizada para maximizar las probabilidades de conversión en ventas.

## Estructura del Proyecto

El proyecto está dividido en varios notebooks, cada uno de ellos con una función específica dentro del flujo de trabajo:

### 1. **Limpieza de Datos y Preprocesamiento**
   En este notebook, se realiza una limpieza exhaustiva de los datos, eliminando duplicados, manejando valores nulos, y transformando variables categóricas en variables numéricas para su posterior análisis. Este proceso es fundamental para garantizar que los datos sean de alta calidad antes de la aplicación de cualquier técnica de modelado.

   **Conocimientos aplicados:**
   - Manejo de librerías como `pandas` y `numpy` para la manipulación de datos.
   - Técnicas de imputación y tratamiento de valores nulos.
   - Transformaciones de variables categóricas y numéricas.
   - Normalización y escalado de datos.

### 2. **Segmentación de Clientes con K-Means**
   Se utiliza el algoritmo K-Means para segmentar a los clientes en cuatro clusters. El análisis de clusters permite identificar patrones en el comportamiento de los clientes, agrupándolos según características similares.

   **Pasos importantes:**
   - Aplicación de la técnica de Elbow y la métrica de silhouette para determinar el número óptimo de clusters.
   - Interpretación de los clusters, utilizando medidas estadísticas (cálculo de medias) para entender qué características definen a cada grupo.
   - Generación de visualizaciones que permiten interpretar visualmente los resultados de la segmentación.

   **Conocimientos aplicados:**
   - Algoritmos de clustering no supervisados (K-Means).
   - Cálculo e interpretación de métricas como Silhouette y Elbow.
   - Técnicas de visualización para representar los clusters.

### 3. **Modelos Predictivos**
   Se desarrollan tres notebooks independientes para construir modelos predictivos en tres grupos de productos: **Financing**, **Investment**, y **Accounts**. Para cada uno, se sigue el mismo flujo de trabajo, que incluye:

   - **Selección de características**: Se eliminan variables irrelevantes para cada grupo de productos.
   - **División de los datos**: Se dividen los datos en conjuntos de entrenamiento y prueba.
   - **Torneo de modelos**: Se prueban diferentes algoritmos (Regresión Logística, Random Forest, XGBoost, etc.) para seleccionar el mejor modelo basado en su precisión, F1-score y AUC-ROC.
   - **Predicción y selección de clientes**: Se seleccionan los clientes con una probabilidad de compra superior al 70% (96% en el caso de **Accounts**) y se exportan en archivos CSV.

   **Conocimientos aplicados:**
   - Creación y evaluación de modelos supervisados (clasificación).
   - Optimización de hiperparámetros utilizando técnicas como `GridSearchCV`.
   - Validación cruzada y evaluación de modelos mediante métricas como F1-Score, Precisión y AUC-ROC.
   - Librerías usadas: `scikit-learn`, `XGBoost`.

### 4. **Unión de Predicciones y Cálculo de Ingresos**
   En este notebook final, se integran los resultados de los tres modelos predictivos. Se crea un dataframe unificado con las probabilidades de compra de cada cliente para los tres productos. Los valores nulos en las probabilidades se imputan con 0. A partir de estos datos, se calcula el ingreso aproximado por cliente en función del grupo de productos que probablemente compren, considerando tanto las probabilidades de compra como los ingresos generados por cada producto.

   **Conocimientos aplicados:**
   - Manipulación avanzada de dataframes.
   - Imputación de valores faltantes.
   - Cálculo de ingresos utilizando funciones basadas en probabilidades y precios de productos.

## Resultados Obtenidos

- **Segmentación exitosa de clientes en 4 clusters**: Se identificaron grupos de clientes con características similares, lo que permite una personalización de campañas de marketing.
- **Modelos predictivos efectivos**: Se seleccionaron 10 mil clientes con alta probabilidad de compra para tres grupos de productos, con una precisión superior al 70% en cada uno de los modelos.
- **Cálculo estimado de ingresos**: Se calculó el ingreso potencial por cliente basado en las probabilidades de compra y los productos más relevantes para cada segmento.
