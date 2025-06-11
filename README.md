Eduardo Alfaro

Introducción
El objetivo de este análisis es explorar y comprender los factores que contribuyen a la evasión de clientes (Churn) en una empresa de telecomunicaciones, identificando patrones y características de los clientes que tienden a abandonar el servicio. La evasión de clientes representa una pérdida significativa de ingresos y una oportunidad de mejora para la retención. Utilizando un conjunto de datos que contiene información demográfica, de servicios y de cuenta de los clientes, buscamos descubrir insights accionables para reducir la tasa de Churn.

Limpieza y Tratamiento de Datos
Los datos se extrajeron de un archivo JSON alojado en un repositorio de GitHub. El proceso de limpieza y tratamiento incluyó los siguientes pasos:
1.  **Extracción:** Los datos se cargaron directamente desde la URL utilizando la librería `requests` y se parsearon como JSON.
2.  **Conversión a DataFrame:** Los datos JSON se transformaron en un DataFrame de pandas para facilitar su manipulación.
3.  **Inspección Inicial:** Se realizaron inspecciones de las primeras filas, nombres de columnas, tipos de datos, resumen estadístico y detección de valores nulos. Se identificaron columnas anidadas que contenían diccionarios ('customer', 'phone', 'internet', 'account').
4.  **Desanidamiento:** Las columnas anidadas se expandieron en nuevas columnas planas, combinando el nombre original de la columna con la subcolumna (ej: 'customer.gender' -> 'customer_gender'). Las columnas originales anidadas fueron eliminadas.
5.  **Renombre de Columnas:** Los puntos '.' en los nombres de las nuevas columnas fueron reemplazados por guiones bajos '_' para una nomenclatura más consistente.
6.  **Manejo de Nulos en Columnas Anidadas:** Se eliminaron las filas que contenían valores nulos en alguna de las columnas que provenían de las estructuras anidadas, ya que estos indicaban registros incompletos o con errores en la estructura original.
7.  **Conversión de Tipos:** Las columnas numéricas 'account_Charges_Monthly' y 'account_Charges_Total' se convirtieron a tipo numérico, manejando posibles errores con `errors='coerce'`.
8.  **Creación de Variable Derivada:** Se creó la columna 'Cuentas_Diarias' calculando el cargo diario promedio (`account_Charges_Monthly / 30`).
9.  **Limpieza de Variable Objetivo:** Se limpió la columna 'Churn', reemplazando valores vacíos o erróneos ('', ' ', 'None') por NaN, y luego se eliminaron las filas donde 'Churn' era NaN, ya que la variable objetivo es crucial para el análisis.
10. **Eliminación de Duplicados:** Se verificó y eliminó cualquier fila duplicada presente en el DataFrame.
11. **Transformación de Variables Binarias:** Las columnas categóricas con valores 'Yes'/'No', incluida la variable objetivo 'Churn', se transformaron a valores numéricos 1/0 ('Yes'/'No' -> 1/0) para facilitar análisis y modelado futuros.
12. **Diagnóstico Final:** Se compararon las dimensiones del DataFrame original con el transformado para cuantificar los registros eliminados y se inspeccionaron los registros eliminados para entender las razones de su exclusión (principalmente por tener el valor de 'Churn' vacío).
El DataFrame resultante (`df_limpio` y `df_binario`) está limpio, estructurado y listo para el análisis exploratorio.
