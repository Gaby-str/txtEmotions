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
