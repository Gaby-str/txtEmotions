# Clasificación de emociones en comunidades chilenas de Reddit

## 1. Definición del problema

Reddit es una plataforma de red social donde el contenido y la interacción entre usuarios se basa principalmente en la narrativa escrita. A pesar de no ser tan popular como otras redes, cuenta con una comunidad activa de usuarios chilenos, destacando principalmente dos subreddits: **r/Chile** y **r/RepublicadeChile**.

Ambas comunidades poseen políticas de moderación y dinámicas ideológicas muy distintas, lo cual genera contrastes significativos. Este proyecto busca **analizar el contenido emocional** presente en estas comunidades para **identificar patrones y características relevantes**, tanto individuales como comparativas.

---

## 2. Plan de acción

Para cumplir con el objetivo, se entrenará un modelo de clasificación de textos capaz de **determinar la emoción predominante** en los posts evaluados.

### 2.1 Dataset

Se utilizará el dataset **"Emotions in Text"** de Ishant (Kaggle), que contiene aproximadamente **21.000 ejemplos únicos**, con las columnas:

- `Text`: contenido textual
- `Emotion`: etiqueta emocional (6 clases)

Este dataset fue seleccionado por su variedad textual y multiclase, lo que lo hace superior a otros que solo contemplan clasificaciones binarias como "positivo" / "negativo".

### 2.2 Modelo

El modelo seleccionado es el **clasificador Naive Bayes**, conocido por su eficiencia y efectividad en tareas de clasificación de texto multiclase.

### El plan contempla las siguientes etapas:

### 2.3 Entrenamiento del modelo

1. **Exploración y limpieza del dataset**: se evaluarán sus características, balance de clases y se realizará una limpieza (eliminación de palabras irrelevantes o sin carga emocional) y transformación del texto.
2. **Entrenamiento y evaluación**: se entrenará el modelo y se validará su rendimiento utilizando técnicas estándar de evaluación.

### 2.4 Preparación del contenido objetivo (Reddit)

1. **Extracción de posts**: se recopilarán publicaciones desde los subreddits objetivo utilizando las herramientas de Reddit o técnicas de Web Scraping.
2. **Traducción del contenido**: como el dataset está en inglés, los textos de Reddit deben traducirse. Se utilizará el modelo de traducción automática **MADLAD-3B**, ideal para mantener el contexto en múltiples idiomas.
MADLAD-3B es útil para traducciones de baja complejidad y es soportable por la máquina virtual de Google Colab utilizando la GPU-T4.
3. **Procesamiento del contenido**: se aplicará la misma limpieza y transformación usada en el dataset de entrenamiento para asegurar compatibilidad con el modelo.

### 2.5 Clasificación y análisis

1. **Clasificación de los posts**: se utilizará el modelo entrenado para predecir la emoción de cada publicación.
2. **Evaluación y conclusiones**: se analizarán los resultados para identificar tendencias emocionales y diferencias entre las comunidades.

---

## 3. Justificación del modelo

Se elige **Naive Bayes** debido a:

- Su **eficacia en problemas de alta dimensionalidad**, como el texto.
- Su capacidad **natural para clasificación multiclase**.
- Su **rapidez y bajo costo computacional**, ideal para procesamiento de grandes volúmenes de datos. especialmente considerando los actuales 21K de datos.
- Su **interpretabilidad**, útil para análisis exploratorio.

Aunque no capta matices complejos o contextos narrativos como lo haría una red neuronal, es suficientemente potente para el propósito del proyecto y representa un excelente punto de partida.

---
---
---

# Metodología

Para la metodología se realizan la siguiente serie de pasos.

---

### Instalar e importar librerías

Para el trabajo se requiere el uso de variadas librerías, entre ellas las más notables:

- **`sklearn`**: para todo lo relacionado a clasificadores y herramientas de vectorización.  
- **`imblearn`**: para sobremuestreo con SMOTE.  
- **`numpy`** y **`pandas`**: para la manipulación del set de datos.  
- **`re`**: para el procesamiento de texto.

---

### Importar, explorar y procesar el dataset

El contenido del dataset es texto en bruto, por lo que requiere de limpieza y transformación para poder ser utilizado en cualquier modelo de clasificación, como lo es **Multinomial Naive Bayes**.

El dataset, con un total de **21.459 filas**, contiene dos columnas:

- `Text`: El texto en bruto.  
- `Emotion`: La emoción predominante (`sadness`, `anger`, `love`, `surprise`, `fear`, `happy`).  

Ninguna de las columnas contiene valores nulos o vacíos.

Posteriormente, se realiza un **countplot** para visualizar el balance de las categorías del dataset.

---

### Procesamiento del dataset

Es necesario simplificar el texto, mantener solamente las palabras más **expresivas**, eliminando aquellas que sean irrelevantes: caracteres, signos, menciones, links/URLs y otro tipo de contenido basura, para mejorar el rendimiento final.

Se aplican los siguientes pasos:

1. Eliminar enlaces, menciones, hashtags (en caso de existir) y caracteres especiales.  
2. Eliminar las *stopwords* determinadas y aplicar *stemming* para convertir las restantes a su forma raíz.  
3. Reensamblar y guardar el texto procesado.  
4. Añadir una nueva columna llamada `"Target"` para almacenar el valor numérico correspondiente a cada categoría en `"Emotion"`.

Con este preprocesamiento, el dataset resultante es más limpio y óptimo para su posterior vectorización.

---

### División del dataset y vectorización

Ahora que se posee un dataset limpio, se procede a **vectorizar** con el fin de generar una entrada válida para el clasificador Naive Bayes.

Se utiliza el vectorizador **`TfidfVectorizer`**, ya que este considera el contexto estadístico de las palabras dentro del corpus, en lugar de simplemente contar las apariciones como lo hace `CountVectorizer`.

El dataset es dividido, y los sets de entrenamiento y prueba son vectorizados.

---

### Sobremuestreo

A fin de equilibrar el conjunto de datos, se **sobremuestrean las clases minoritarias** mediante la creación de muestras sintéticas a partir de las existentes, utilizando **SMOTE (Synthetic Minority Oversampling Technique)**.

> Fuente: [Handling Imbalanced Datasets in Scikit-learn](https://datasciencehorizons.com/handling-imbalanced-datasets-in-scikit-learn-techniques-and-best-practices/)

Para aplicar SMOTE, el set de entrenamiento se convierte a un array, ya que es el formato requerido.

- Tamaño original del set de entrenamiento: **17.167** muestras (80%)  
- Tamaño posterior al sobremuestreo: **33.888** muestras

**[Gráfico del balance de clases]**

---

### Evaluar rendimiento con Cross Validation

Con el set de datos ya procesado, vectorizado y reequilibrado, se procede a evaluar el rendimiento del clasificador **Multinomial Naive Bayes** utilizando validación cruzada (**Cross Validation**).

---

### Predicciones finales

Se realizan las predicciones finales del modelo **Multinomial Naive Bayes** sobre el set de prueba.

---

### Reducción de dimensionalidad

Se aplica la técnica de **mutual information** para reducir la dimensionalidad del espacio de características, pasando de **10.000 features** a **5.000** más relevantes.

Luego, se realiza nuevamente la vectorización del set de entrenamiento usando únicamente estas features, y se evalúa el nuevo rendimiento del modelo.

---

### Evaluación con Bagging Classifier

Finalmente, se evalúa un modelo clasificador basado en **Bagging** con `MultinomialNB`, con el objetivo de observar posibles mejoras en el rendimiento general.
