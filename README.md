# pry_Fraud_Detection
Data science project

#
El modelo en este código es un clasificador binario que predice si una transacción financiera es fraudulenta o no. Específicamente, predice la columna isFraud del dataset.

# Detalles del Modelo

## 1. Objetivo del Modelo
El objetivo del modelo es clasificar las transacciones como fraudulentas (isFraud = 1) o no fraudulentas (isFraud = 0).

## 2. Entradas del Modelo
El modelo utiliza varias características (features) de cada transacción para hacer la predicción. Estas características incluyen:

step: El paso de tiempo, posiblemente indicando la secuencia temporal de las transacciones.
type: El tipo de transacción (por ejemplo, 'CASH_OUT', 'PAYMENT', etc.).
amount: El monto de la transacción.
oldbalanceOrg: El saldo original del remitente antes de la transacción.
newbalanceOrig: El nuevo saldo del remitente después de la transacción.
oldbalanceDest: El saldo original del destinatario antes de la transacción.
newbalanceDest: El nuevo saldo del destinatario después de la transacción.

## 3. Preprocesamiento
Antes de entrenar el modelo, las características se preprocesan:

Estandarización: Las características numéricas se escalan para tener media 0 y desviación estándar 1, utilizando StandardScaler.
Codificación One-Hot: La característica categórica type se convierte en variables dummy (one-hot encoding).

## 4. Modelo Utilizado: XGBoost
XGBoost: Es un algoritmo de gradient boosting que es muy eficiente y eficaz para tareas de clasificación y regresión. En este caso, se utiliza para la clasificación binaria.
DMatrix: Los datos se convierten en una estructura optimizada para XGBoost llamada DMatrix.

## 5. Entrenamiento del Modelo
El modelo se entrena usando los datos preprocesados:

Parámetros: Incluyen el objetivo de la clasificación binaria (binary:logistic), la profundidad máxima de los árboles (max_depth), la tasa de aprendizaje (eta), y el método del árbol (tree_method).
Iteraciones: El modelo se entrena durante un número específico de iteraciones (num_boost_round).
## 6. Predicciones y Evaluación
Predicciones: El modelo predice las probabilidades de que cada transacción sea fraudulenta. Estas probabilidades se convierten en clases binarias (0 o 1) usando un umbral de 0.5.
Evaluación: Se calculan métricas de rendimiento para evaluar la precisión del modelo. Estas métricas incluyen la precisión (accuracy), la matriz de confusión (confusion matrix), y un informe de clasificación (classification report) que muestra precisión, recall, y F1-score.
## Flujo Completo del Proceso
Cargar Datos: Se cargan los datos desde un archivo CSV usando Dask para manejar datasets grandes.
Optimizar Tipos de Datos: Se optimizan los tipos de datos para reducir el uso de memoria.
Muestreo: Se toma una muestra del dataset para desarrollo y pruebas rápidas.
División de Datos: Se dividen los datos en conjuntos de entrenamiento y prueba.
Preprocesamiento: Se estandarizan las características numéricas y se codifican las características categóricas.
Entrenamiento del Modelo: Se entrena el modelo de XGBoost con los datos preprocesados.
Predicciones: Se realizan predicciones en el conjunto de prueba.
Evaluación: Se evalúa el rendimiento del modelo utilizando diversas métricas.
## Conclusión
El modelo predice si una transacción es fraudulenta o no basándose en características de la transacción. Este tipo de modelo es crucial para detectar fraudes en sistemas financieros y proteger a las organizaciones y sus clientes de actividades fraudulentas.

## Análisis de la Importancia de las Características
El gráfico de importancia de las características muestra cuáles son las variables más influyentes en la predicción de si una transacción es fraudulenta o no en el modelo de XGBoost. Vamos a detallar por qué las características oldbalanceOrg, amount, y step son tan importantes y por qué tiene sentido intuitivo que lo sean.

### 1. oldbalanceOrg (Saldo Original del Remitente)
Importancia en el Gráfico: f2 tiene la mayor importancia.
Razón: El saldo original del remitente antes de realizar la transacción puede indicar comportamientos sospechosos. Por ejemplo, una cuenta con un saldo original muy alto que de repente hace una transacción grande podría ser una señal de lavado de dinero o un intento de fraude.
Ejemplo Intuitivo: Si una cuenta generalmente mantiene un saldo bajo pero de repente tiene una gran suma y realiza una transacción grande, esto podría ser una bandera roja para fraude.
### 2. amount (Monto de la Transacción)
Importancia en el Gráfico: f1 es la segunda característica más importante.
Razón: El monto de la transacción es crucial para identificar fraudes. Las transacciones fraudulentas suelen ser de cantidades inusualmente altas o, a veces, consistentemente bajas para evitar detección.
Ejemplo Intuitivo: Transacciones de montos inusualmente grandes pueden ser sospechosas si no coinciden con el patrón normal de gasto del usuario.
### 3. step (Paso de Tiempo)
Importancia en el Gráfico: f0 es también muy importante.
Razón: La secuencia temporal de las transacciones puede ayudar a detectar patrones fraudulentos. Las transacciones fraudulentas a menudo ocurren en ráfagas rápidas para evitar la detección.
Ejemplo Intuitivo: Si varias transacciones grandes se realizan en un corto período de tiempo (por ejemplo, dentro de unos pocos minutos o horas), esto podría indicar un comportamiento fraudulento.