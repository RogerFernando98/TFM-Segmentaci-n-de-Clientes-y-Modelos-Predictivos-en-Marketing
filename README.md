# TFM: Segmentación de Clientes y Modelos Predictivos para Marketing Personalizado

Este proyecto forma parte de mi Trabajo Final de Máster en Ciencia de Datos en [Nuclio Digital School](https://nuclio.school). El objetivo es maximizar la rentabilidad de la empresa ficticia EasyMoney a través de una estrategia data-driven que combina limpieza de datos, segmentación de clientes y modelos de clasificación predictiva, permitiendo diseñar una campaña de marketing personalizada para 10.000 clientes.

---

## 🔍 Objetivo del Proyecto

Diseñar e implementar un sistema de segmentación de clientes y clasificación predictiva que permita:

* Identificar patrones de comportamiento en los clientes.
* Predecir qué grupo de productos financieros (Accounts, Financing o Investment) es más probable que adquieran.
* Personalizar los envíos de email marketing para cada uno de los 4 segmentos finales.

---

## 📈 Problema que resuelve

EasyMoney tenía una gran base de clientes adquiridos, pero no sabía cómo aprovecharla para aumentar ingresos. Este proyecto responde a la necesidad de:

* Rentabilizar la base de clientes con estrategias de upselling y cross-selling.
* Personalizar la comunicación a los distintos perfiles de cliente.
* Maximizar el ROI de las campañas de marketing.

---

## 📅 Contexto

EasyMoney es una plataforma financiera multicanal que ofrece productos de ahorro, inversión y financiación. Con el objetivo de mejorar su EBITDA, la dirección decide implementar un enfoque data-driven para optimizar la propuesta de valor y aumentar la fidelización de sus clientes mediante campañas personalizadas basadas en datos.

---

## 📊 Datos Utilizados

Se trabajó con tres datasets originales, cada uno con más de 6 millones de filas:

* `df_commercial_activity`: información sobre la actividad comercial de los clientes.
* `df_products`: detalle de productos financieros contratados.
* `df_sociodemographic`: variables demográficas y de segmentación.

### Preprocesamiento

* Eliminación de duplicados (hasta 17 por cliente), conservando la fila más reciente.
* Unificación por `PK_CID` y `PK_PARTITION`.
* Manejo de nulos: imputación de `salary` por edad usando backfill/frontfill.
* Agrupación de variables categóricas poco frecuentes.
* Conversión de fechas a features numéricas (año, mes, día, día de semana).
* OneHotEncoding y OrdinalEncoding para categorías.

---

## 🪡 Metodología

### 1. Agrupación de productos

* Se redujo la dimensionalidad agrupando los productos en tres categorías:

  * **Accounts**: cuentas, tarjetas de débito, nómina.
  * **Financing**: préstamos, hipotecas, tarjetas de crédito.
  * **Investment**: fondos, planes de pensiones, valores.

### 2. Segmentación inicial (7 clusters)

* Se usó K-Means para descubrir patrones.
* Se crearon variables como `product_engagement_score` y `debt_to_income_ratio`.
* Se interpretaron los clusters a partir de medias de variables clave.

### 3. Modelos de Clasificación (1 por grupo de producto)

* Modelos usados: LogisticRegression, RandomForest, CatBoost, XGBoost, entre otros.
* Selección del mejor modelo según `accuracy`, `roc_auc` y capacidad predictiva.
* Se filtraron los clientes con probabilidad de compra > 70% (o >96% en Accounts).
* Resultados:

  * 933 clientes para Financing
  * 4991 clientes para Investment
  * 4076 clientes para Accounts

### 4. Merge de predicciones

* Se combinan las predicciones por cliente, rellenando nulos con 0.
* Se estima el ingreso por cliente según:

  * Probabilidad de compra
  * Ingreso por producto
  * Precisión del modelo

### 5. Segmentación final (4 clusters)

* Se agrupan los 10.000 clientes seleccionados usando K-Means.
* Cada cluster representa un perfil específico.
* Se definen mensajes y productos clave para cada grupo.

---

## 🎓 Tecnologías y Librerías

* **Lenguaje**: Python
* **Entorno**: Jupyter Notebook
* **Librerías principales**:

  * `pandas`, `numpy`: manipulación de datos
  * `matplotlib`, `seaborn`: visualización
  * `scikit-learn`, `xgboost`, `catboost`: modelado
  * `tensorflow/keras`: pruebas con modelos de deep learning

---

## 📁 Estructura del repositorio

```bash
TFM_EasyMoney/
│
├── data/
│   ├── raw/                      # Datos originales (no subidos por tamaño)
│   └── processed/                # Datos procesados
│
├── notebooks/                   # Notebooks por etapa del proyecto
│   ├── 1.-preprocesing.ipynb
│   ├── 2.-encoding.ipynb
│   ├── 3.-Segmentacion.ipynb
│   ├── 4.-agrupacion.ipynb
│   ├── 5.-balancear.ipynb
│   ├── 6.-Modelo_investment.ipynb
│   ├── 6.1.-Modelo_financing.ipynb
│   ├── 6.2.-Modelo_account.ipynb
│   ├── 7.-Unir_predicciones.ipynb
│   └── 8.-Segmentacion_10K_Clientes.ipynb
│
├── documentos_complementarios/ # PDFs de interpretaciones, presentaciones y KPIs
├── src/                         # (opcional) funciones comunes y helpers
├── README.md                    # Este documento
├── requirements.txt             # Dependencias del proyecto
└── .gitignore                   # Archivos ignorados por Git
```

---

## 🌍 Resultados

* **Segmentación clara** de 10.000 clientes en 4 perfiles distintos.
* **Modelos predictivos** con alta precisión para recomendar productos.
* **Campañas de marketing personalizadas** según perfil, producto y comportamiento.
* **Estimación de ingresos y ROI positivo** basado en la probabilidad de compra.

---

## ⚡ Posibles mejoras

* Incluir métricas como F1-score y matriz de confusión para evaluar mejor los modelos.
* Automatizar el pipeline en `src/` para producción.
* Probar clustering con métodos jerárquicos o DBSCAN.
* Desarrollar dashboard de visualización con Streamlit o Power BI.

---

## 📖 Autor

**Fernando Arroyo Herrera**
Data Scientist con background en Finanzas y especialización en segmentación, modelado predictivo y estrategias de marketing basadas en datos.

* [LinkedIn](https://www.linkedin.com/in/f-arroyo-herrera/)
* [GitHub](https://github.com/RogerFernando98)
