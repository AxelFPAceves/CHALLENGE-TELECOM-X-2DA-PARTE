# Telecom X - Predicción de Evasión de Clientes (Churn)

## Introducción

Este repositorio contiene la segunda fase del proyecto de Churn para la empresa Telecom X. El objetivo de este proyecto es desarrollar un pipeline de Machine Learning para construir y evaluar modelos predictivos capaces de identificar qué clientes tienen una mayor probabilidad de cancelar sus servicios. 

El análisis se basa en un conjunto de datos previamente limpiado y preparado, y se enfoca en el preprocesamiento, entrenamiento, evaluación e interpretación de modelos de clasificación.

## Pipeline de Machine Learning

El proceso para desarrollar el modelo predictivo siguió los siguientes pasos:

### 1. Preparación de Datos para Modelado

*   **Carga de Datos:** Se utilizó un archivo CSV (`telecom_churn_cleaned.csv`) que contiene los datos de clientes ya procesados.
*   **Eliminación de Columnas:** Se descartaron identificadores únicos (`customerID`) y columnas redundantes que no aportan valor predictivo.
*   **Encoding de Variables Categóricas:** Se transformaron las variables categóricas a formato numérico mediante la técnica de *one-hot encoding* para hacerlas compatibles con los algoritmos.
*   **Balanceo de Clases:** Dado que solo el 27% de los clientes habían cancelado, se aplicaron dos técnicas para evitar que el modelo se sesgara hacia la clase mayoritaria:
    *   **SMOTE (Oversampling):** Creación de muestras sintéticas de la clase minoritaria.
    *   **RandomUnderSampler (Undersampling):** Reducción de muestras de la clase mayoritaria.
*   **Estandarización de Datos:** Se estandarizaron las variables numéricas con `StandardScaler` para asegurar que todas tuvieran una escala comparable, un paso crucial para los modelos basados en distancia.

### 2. Creación y Evaluación de Modelos

Se entrenaron tres algoritmos de clasificación (Regresión Logística, Random Forest y K-Nearest Neighbors) en tres conjuntos de datos diferentes (original, SMOTE y undersampling) para encontrar la mejor combinación. 

El modelo con el mejor rendimiento fue el **Random Forest entrenado con datos balanceados por SMOTE**, el cual obtuvo un **F1-score de 0.8416**, demostrando un excelente equilibrio para identificar correctamente a los clientes que cancelan y a los que no.

### 3. Análisis de Importancia de Variables

La interpretación de los modelos más relevantes (Random Forest y Regresión Logística) nos permitió identificar los factores clave que impulsan la cancelación:

1.  **Tipo de Contrato:** Ser cliente con un **contrato mes a mes** es el predictor más fuerte de una posible cancelación.
2.  **Antigüedad (Tenure):** Los clientes con **pocos meses** en la compañía son mucho más propensos a irse.
3.  **Servicio de Internet de Fibra Óptica:** Este servicio, a pesar de ser premium, está fuertemente asociado a la cancelación, posiblemente por una mala relación precio-calidad o expectativas no cumplidas.
4.  **Gasto Mensual:** A mayor el gasto mensual, mayor la probabilidad de churn.

## Conclusiones y Estrategias de Retención

El análisis predictivo confirma que los clientes nuevos, con contratos flexibles y gastos mensuales altos (especialmente en fibra óptica), son los que tienen mayor riesgo. Se proponen las siguientes estrategias:

1.  **Fidelización Temprana:** Crear programas de lealtad y seguimiento para clientes durante sus primeros 6 meses.
2.  **Incentivar Contratos a Largo Plazo:** Ofrecer descuentos o beneficios exclusivos para clientes que migren de planes mes a mes a contratos anuales.
3.  **Revisar Oferta de Fibra Óptica:** Analizar la competitividad y la calidad del servicio de fibra óptica para ajustar la relación precio-valor.
4.  **Gestión Proactiva de Cuentas:** Utilizar el modelo para identificar clientes de alto riesgo y contactarlos proactivamente con ofertas personalizadas o soporte técnico.

## Cómo ejecutar el proyecto

### Requisitos

*   Python 3.x
*   Jupyter Notebook o Google Colab
*   Bibliotecas de Python:
    *   pandas
    *   matplotlib
    *   seaborn
    *   scikit-learn
    *   imblearn

### Instrucciones

1.  Clonar el repositorio.
2.  Asegurarse de tener las bibliotecas necesarias instaladas:
    ```bash
    pip install pandas matplotlib seaborn scikit-learn imblearn
    ```
3.  Abrir el notebook `TelecomX_LATAM.ipynb` en Jupyter Notebook o Google Colab y ejecutar las celdas en orden.