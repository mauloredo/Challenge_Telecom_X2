# Proyecto de Predicción de Cancelación (Churn) en Telecom X

## Descripción del Desafío

Este proyecto tuvo como objetivo desarrollar modelos predictivos para prever qué clientes de Telecom X tienen una alta probabilidad de cancelar sus servicios. El desafío consistió en construir un pipeline de Machine Learning robusto, desde la preparación de datos hasta la evaluación e interpretación del modelo, para permitir que la empresa anticipe y gestione proactivamente el problema de la cancelación de clientes.

**Objetivos clave:**

- Preparar y preprocesar datos para el modelado.
- Realizar análisis exploratorio y de correlación para entender los factores que influyen en la cancelación.
- Entrenar y evaluar múltiples modelos de clasificación.
- Optimizar el modelo con mejor rendimiento.
- Interpretar el modelo para identificar las variables más importantes.
- Generar conclusiones estratégicas basadas en los hallazgos.

---

## Control de Versiones de Datos y Objetos

Durante el proyecto se generaron y utilizaron los siguientes archivos clave:

### DataFrames:

- `datos_x2.csv`: DataFrame importado del proyecto anterior.
- `datos.csv`: DataFrame con columnas 'object' convertidas a 'category'.
- `datos_v1.csv`: DataFrame después de eliminar las columnas 'TotalCharges', 'Cuentas_Diarias' y 'PhoneService'.
- `datos_v2.csv`: DataFrame con columnas 'object' convertidas nuevamente a 'category' después de la eliminación de columnas.
- `data.csv`: DataFrame después de la codificación (**One-Hot Encoding** y **LabelEncoder**).
- `data_2.csv`: DataFrame después de la estandarización (**StandardScaler**) de variables numéricas.
- `model_x.csv`: DataFrame final de características (`features`) limpio y listo para modelado (sin variables redundantes).

### Objetos Guardados:

- `champion_44.pkl`: El modelo final entrenado (**XGBoost** con hiperparámetros optimizados y `scale_pos_weight`), guardado para su posterior implementación.

### Visualizaciones (Archivos .png):

- `hist_tenure_churn.png`
- `hist_monthlycharges_churn.png`
- `hist_totalcharges_churn.png`
- `boxplot_tenure_churn.png`
- `boxplot_monthlycharges_churn.png`
- `boxplot_totalcharges_churn.png`
- `catplot_gender_churn.png`
- `catplot_seniorcitizen_churn.png`
- `catplot_partner_churn.png`
- `catplot_dependents_churn.png`
- `catplot_contract_churn.png`
- `catplot_paymentmethod_churn.png`
- `catplot_internetservice_churn.png`
- `catplot_phoneservice_churn.png`
- `catplot_multiplelines_churn.png`
- `catplot_onlinesecurity_churn.png`
- `catplot_onlinebackup_churn.png`
- `catplot_deviceprotection_churn.png`
- `catplot_techsupport_churn.png`
- `catplot_streamingtv_churn.png`
- `catplot_streamingmovies_churn.png`
- `catplot_paperlessbilling_churn.png`
- `heatmap_correlation_X.png`
- `hist_tenure_churn_cleaned.png`
- `hist_monthlycharges_churn_cleaned.png`
- `catplot_InternetService_Fiber optic_churn_cleaned.png`
- `catplot_PaymentMethod_Electronic check_churn_cleaned.png`
- `catplot_Contract_Two year_churn_cleaned.png`
- `catplot_SeniorCitizen_churn_cleaned.png`
- `catplot_OnlineSecurity_Yes_churn_cleaned.png`
- `catplot_TechSupport_Yes_churn_cleaned.png`
- `cv_results_comparison.png`
- `roc_curve_final_model.png`
- `precision_recall_curve.png`
- `feature_importance.png`

---

## Fases del Proyecto

El proyecto se estructuró en las siguientes fases:

### FASE 0: Análisis Exploratorio Básico (Antes de la Limpieza)

Se realizó una exploración inicial de los datos para comprender distribuciones, identificar tipos de datos, valores nulos y evaluar la necesidad de limpieza y transformación. Se identificaron variables redundantes y aquellas con baja variabilidad.

### FASE 1: Preparación de los Datos (Limpieza y Codificación)

En esta fase, se llevó a cabo la limpieza eliminando columnas irrelevantes y se prepararon los datos para el modelado. Esto incluyó la verificación de tipos de datos, manejo de nulos (confirmando su ausencia) y la codificación de variables categóricas utilizando **Label Encoding** para variables binarias y **One-Hot Encoding** para variables con más de dos categorías. Las variables numéricas `tenure` y `MonthlyCharges` fueron estandarizadas utilizando `StandardScaler`.

### FASE 2: Análisis Exploratorio y Correlación

Se profundizó en el análisis de datos transformados, examinando la distribución de variables clave en relación con la cancelación y calculando la matriz de correlación. Se identificaron variables con alta correlación con la variable objetivo (`Churn`) y se detectaron casos de multicolinealidad perfecta, lo que llevó a la eliminación de variables redundantes.

### FASE 3: Modelado y Evaluación

Se dividieron los datos en conjuntos de entrenamiento y prueba (estratificados). Se entrenaron y evaluaron tres modelos de clasificación (**Random Forest**, **XGBoost**, **SVM**) utilizando validación cruzada estratificada. XGBoost fue seleccionado como el modelo con mejor rendimiento inicial basado en métricas como **Recall**, **F1-Score** y **ROC-AUC**. Se optimizaron los hiperparámetros de XGBoost utilizando **RandomizedSearchCV**, priorizando el Recall.

### FASE 4: Ajustes para el Mejoramiento del Modelo

Esta fase se centró en mejorar el modelo XGBoost, principalmente abordando el desbalance de clases. Se exploraron:
- Ajuste del umbral de clasificación.
- Uso del parámetro `scale_pos_weight` en XGBoost.
- Aplicación de técnicas de sobremuestreo (SMOTE).
- Ajuste fino de hiperparámetros combinado con la mejor estrategia de desbalance.
- **Feature Engineering** para crear nuevas variables.
- **Feature Selection** para reducir la dimensionalidad.

La combinación más efectiva resultó ser el uso de `scale_pos_weight` en XGBoost junto con la optimización de hiperparámetros, logrando un balance mejorado entre **Recall** y **Precision** en el conjunto de prueba.

### FASE 5: Cierre del Proyecto

Se finalizó el proyecto obteniendo la importancia de las características del modelo final, interpretando los resultados para derivar conclusiones estratégicas y guardando el modelo entrenado para su implementación futura.

---

## Resultados Clave y Conclusiones Estratégicas

**Métricas del Modelo Final (XGBoost con scale_pos_weight y Hiperparámetros Optimizados en el conjunto de prueba):**

- **Precision:** 0.4936
- **Recall (Exhaustividad):** 0.8209
- **F1-Score:** 0.6165
- **ROC-AUC Score (Modelo Base):** 0.8397

El modelo final demostró una **alta capacidad para identificar a los clientes con riesgo de cancelación (Recall de 0.8209)**, lo cual es crucial para la detección temprana de `churners`. Si bien esto se logró a expensas de una menor **Precisión** (más falsos positivos), el enfoque está alineado con el objetivo de no perder la oportunidad de intervenir con clientes en riesgo.

**Características Más Importantes (Impulsores de Churn):**

Las variables con mayor impacto en la predicción de cancelación fueron:

1.  **InternetService_Fiber optic:** Clientes con servicio de fibra óptica son significativamente más propensos a cancelar.
2.  **Contract_Two year / Contract_One year:** Clientes con contratos a largo plazo son mucho menos propensos a cancelar.
3.  **InternetService_No:** Clientes sin servicio de internet son menos propensos a cancelar.
4.  **tenure:** La antigüedad del cliente; menor antigüedad se asocia con mayor `churn`.
5.  **PaymentMethod_Electronic check:** Clientes que pagan con cheque electrónico tienen mayor propensión a cancelar.

**Recomendaciones Estratégicas para Reducir el Churn:**

-   **Investigar y abordar problemas específicos del servicio de Fibra Óptica:** Dada su alta correlación con el `churn`, se deben examinar posibles problemas técnicos, de calidad o de precio.
-   **Promover activamente contratos a largo plazo:** Ofrecer incentivos y programas de fidelización para migrar clientes a contratos de 1 o 2 años.
-   **Implementar programas de retención para clientes nuevos:** Priorizar el _engagement_ y la satisfacción en los primeros meses de servicio para reducir el `churn` temprano.
-   **Educación sobre servicios de valor añadido (Seguridad y Soporte Técnico):** Resaltar la importancia de estos servicios para mejorar la retención.
-   **Utilizar el modelo predictivo para campañas de retención dirigidas:** Identificar a los clientes con alta probabilidad de `churn` (según el modelo) para ofrecerles atención personalizada, ofertas especiales o soluciones a sus posibles problemas.

---

## Cómo Replicar el Proyecto

Para ejecutar este proyecto, siga los siguientes pasos:

1.  Clone este repositorio.
