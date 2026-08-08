# Titanic — Análisis Exploratorio de Datos (EDA)

Workshop 1 · Unidad 1 · Machine Learning

## Integrantes

- Mariamny Del Valle Ramirez Telles
- David Alejandro Gutiérrez Leal
- Sahian Salomé Gutiérrez Ossa

## Descripción del proyecto

Este notebook desarrolla un análisis exploratorio de datos (EDA) completo sobre el dataset [Titanic - Machine Learning from Disaster](https://www.kaggle.com/competitions/titanic/data?select=train.csv) de Kaggle. El objetivo del dataset es predecir la supervivencia de los pasajeros a partir de variables demográficas y socioeconómicas (clase del ticket, sexo, edad, tarifa pagada, familiares a bordo, puerto de embarque, etc.), por lo que se trata de un problema de **clasificación binaria supervisada** (`Survived`: 0 = no sobrevivió, 1 = sobrevivió).

## Estructura del notebook

El análisis se organiza en 5 fases, siguiendo el ciclo completo de trabajo con datos:

| Fase | Contenido |
|------|-----------|
| **Fase 1 — Reconocimiento inicial** | Carga del dataset, `head()`/`tail()`, diccionario de datos, tipos de columna (`.info()`, `.dtypes`), estadísticos descriptivos (`.describe()`) y cálculo manual de media/mediana/desviación estándar con NumPy |
| **Fase 2 — Limpieza de datos** | Identificación y tratamiento de nulos (`Age`, `Cabin`, `Embarked`), detección de duplicados, corrección de inconsistencias de formato en texto, detección de outliers con el criterio IQR |
| **Fase 3 — Análisis descriptivo** | Conteo de categorías, diccionario de métricas agregadas por clase, `.groupby()` para responder preguntas de negocio, extremos del dataset con `.sort_values()` |
| **Fase 4 — Visualización** | Gráfico de barras, gráfico de pie, histograma, scatter plot, boxplots — cada uno con interpretación y recomendación |
| **Fase 5 — Conclusiones** | Síntesis general de hallazgos con un panel de 4 gráficos (subplot 2×2) |

## Principales hallazgos

- **Tasa de supervivencia global:** 38.4% (desbalance de clases relevante para un futuro modelo).
- **Clase del ticket (`Pclass`):** el factor más determinante — 1ª clase 62.96% de supervivencia, 2ª clase 47.28%, 3ª clase 24.24%.
- **Sexo:** las mujeres sobrevivieron en un 74.2% frente a un 18.9% de los hombres.
- **Tarifa (`Fare`):** distribución fuertemente sesgada a la derecha, con 116 outliers según el criterio IQR (tarifas > 65.63), concentrados en pasajeros de 1ª clase.
- **Edad vs. Tarifa:** correlación prácticamente nula (Pearson = 0.097); la edad no predice la tarifa pagada.

## Limpieza de datos aplicada

| Columna | % nulos | Estrategia | Justificación |
|---------|--------:|------------|----------------|
| `Cabin` | 77.1% | Eliminar columna | Porcentaje de nulos demasiado alto para imputar sin introducir sesgo |
| `Age` | 19.9% | Imputar con mediana | Medida robusta frente a los outliers de edad presentes en el dataset |
| `Embarked` | 0.2% | Imputar con moda | Variable categórica con una categoría (`S`) claramente dominante (~72%) |

## Herramientas y librerías

- Python 3 (Google Colab)
- `pandas`, `numpy`, `matplotlib`

## Justificación del uso de IA

Durante el desarrollo de este taller se usó **Claude (Anthropic)** como herramienta de apoyo, no como generador del análisis. El uso se limitó a:

- **Revisión de código y detección de errores técnicos:** por ejemplo, identificar que `pandas.boxplot()` ignora una figura creada previamente con `plt.figure()` si no se le pasa el parámetro `ax`, generando una figura vacía; o detectar una celda que hacía referencia a una columna (`Cabin`) ya eliminada previamente, lo que habría causado un `KeyError` al ejecutar el notebook de corrido.
- **Retroalimentación sobre la calidad de las interpretaciones:** validar si los párrafos de análisis cumplían con lo pedido en cada punto del enunciado (interpretar, no solo describir el resultado) y sugerir qué faltaba profundizar (por ejemplo, cuantificar con un coeficiente de correlación una lectura que solo era visual).

Todo el análisis, las decisiones de limpieza de datos, el código y las interpretaciones fueron elaborados y validados por el equipo. La IA se usó como un segundo revisor para pulir el trabajo antes de la entrega, no reemplazó el razonamiento ni la escritura del análisis.

## Cómo ejecutar

1. Descargar `train.csv` desde [Kaggle](https://www.kaggle.com/competitions/titanic/data?select=train.csv).
2. Colocar el archivo en la misma carpeta que el notebook.
3. Abrir `Workshop1.ipynb` en Jupyter o Google Colab y ejecutar las celdas en orden.
