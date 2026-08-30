# 🧠 Automatización de Codificación Temática en Entrevistas mediante LLMs

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)]()
[![NLP](https://img.shields.io/badge/NLP-HuggingFace-yellow.svg)]()
[![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Transformers-orange.svg)]()

## 📖 Descripción del Proyecto
Este proyecto de Ciencia de Datos y Neurociencia Social automatiza el proceso cualitativo de codificación temática de entrevistas mediante técnicas de Procesamiento de Lenguaje Natural (PLN). 

Originalmente enmarcado en la investigación de la orientación y participación política de jóvenes universitarios, el objetivo principal es reducir drásticamente el tiempo y esfuerzo humano requerido para analizar manualmente transcripciones complejas. Mediante el uso de Modelos de Lenguaje de Gran Escala (LLMs) enfocados en *embeddings*, el sistema extrae fragmentos relevantes, comprende el contexto semántico y predice etiquetas para múltiples variables sociodemográficas e ideológicas.

## 🎯 Objetivos
* **Automatización:** Sugerir automáticamente posibles etiquetas para nuevas entrevistas basándose en una matriz de codificación previa.
* **Aplicación de LLMs:** Evaluar y utilizar redes neuronales preentrenadas (arquitectura Transformer) para identificar patrones complejos en el lenguaje natural.
* **Análisis Semántico:** Implementar métricas como la similitud del coseno para emparejar consultas estructuradas (*queries*) con respuestas abiertas de los entrevistados.

## ⚙️ Metodología y Tecnologías

El flujo de trabajo se divide en dos fases principales, documentadas en cuadernos interactivos:

### 1. Limpieza y Exploración (`limpieza_fragmentos.ipynb`)
* **Limpieza de datos:** Uso de expresiones regulares (regex) y la librería `spaCy` para normalizar el texto, eliminar muletillas típicas del habla colombiana (ej. "emmm", "este") y corregir repeticiones.
* **Procesamiento de edades:** Extracción y categorización dinámica de variables numéricas complejas (como edad de inicio en redes sociales) desde texto libre.
* **Modelado de Temas:** Aplicación de TF-IDF y LDA para la extracción exploratoria de palabras clave y tópicos recurrentes.

### 2. Predicción de Categorías (`prediccion_fragmentos.ipynb`)
* **Generación de Embeddings:** Se evaluaron 4 modelos Transformer. Se seleccionó **`intfloat/e5-large`** (335 millones de parámetros, 1024 dimensiones) por su capacidad superior para capturar sutilezas del "español colombiano", regionalismos y jerga universitaria frente a modelos más pequeños.
* **Clasificación por Similitud:** El modelo vectoriza tanto las respuestas de los participantes como los *queries* de las categorías objetivo. Mediante **Similitud del Coseno**, identifica los fragmentos más pertinentes (Top-k) y asigna la categoría dominante.

## 📊 Resultados y Desempeño
El modelo fue evaluado utilizando métricas de recuperación de información: **Top-k Accuracy**, **MRR** (Mean Reciprocal Rank) y **MAP** (Mean Average Precision).

El rendimiento varió significativamente dependiendo de la naturaleza de la variable:
* **Alta Precisión (Estructuradas):** Variables como *Ideología Política (Presencia/Ausencia)* alcanzaron un **Top-5 Accuracy de 0.968**, demostrando la eficacia del modelo para clasificar conceptos expresados de forma directa.
* **Precisión Moderada/Baja (Subjetivas):** Variables altamente abstractas como el *Tipo de Discurso* (Reactivo, Propositivo, Desinterés) presentaron mayores retos (**Top-5 Accuracy: 0.643**). Esto subraya la dificultad algorítmica de interpretar la ironía, el contexto y la intención comunicativa subyacente.
* **Sesgos Identificados:** Se observaron desafíos al procesar categorías con fronteras difusas (ej. *Urbano vs. Rural*, niveles de *Cohesión Familiar*) o cuando los datos de entrenamiento presentaban desbalances de clases.

## 💡 Conclusiones
La automatización de la codificación cualitativa con LLMs es altamente viable y acelera el trabajo hermenéutico. El modelo `intfloat/e5-large` demostró ser una herramienta robusta para el análisis semántico de entrevistas. Sin embargo, el proyecto revela que el éxito del algoritmo depende críticamente de la calidad del diseño de los *queries* (consultas) y que la supervisión humana sigue siendo indispensable para validar variables de alta carga subjetiva.

---
*Desarrollado en el contexto del Laboratorio Interdisciplinar de Ciencias y Procesos Humanos (LINCIPH) - Universidad Externado de Colombia, 2025.*
