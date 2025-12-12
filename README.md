

# Predicción y Análisis de Calidad de Energía 

Por:

* Luis Fernando Castro Buchelly
* Diego Fernando Erazo Ciceri
* Juan Esteban Granada Cardona
* Daniel Mauricio Mejia Hoyos

## Motivación del Proyecto

La calidad y continuidad del servicio eléctrico es un aspecto fundamental para CHEC, tanto por el impacto directo en los usuarios como por las responsabilidades regulatorias. Las interrupciones, variaciones de tensión y el desgaste de los activos generan costos altos y afectan los indicadores de calidad. Además, muchas zonas de la red no cuentan con medición avanzada, lo que limita la capacidad de analizar su comportamiento real.

Por esta razón, es necesario contar con modelos que permitan estimar la calidad del servicio en puntos donde no hay instrumentación, aprovechando datos históricos, variables ambientales y condiciones operativas. Este proyecto responde a esa necesidad combinando técnicas de aprendizaje profundo con un agente capaz de interpretar la normativa, con el fin de apoyar la toma de decisiones y anticipar posibles fallas.

## Descripción del Problema

La empresa CHEC (Central Hidroeléctrica de Caldas) es la encargada de la distribución y comercialización de energía eléctrica en el departamento de Caldas, Colombia. La continuidad y calidad del servicio son indicadores críticos para la operación eficiente de la red y la satisfacción del usuario final.

Este proyecto aborda el desafío de estimar la calidad del servicio en puntos específicos de la red de distribución donde no se cuenta con medición directa continua. Se utiliza un conjunto de datos que integra variables técnicas, operativas, estructurales y condiciones meteorológicas. El núcleo del problema consiste en desarrollar un sistema capaz de predecir el índice UITI (Índice Unificado de Tensión e Interrupciones) y, posteriormente, explicar las causas de las fallas utilizando un agente de inteligencia artificial que cruza los hallazgos matemáticos con la normativa técnica vigente.

## Objetivo del Proyecto

El objetivo principal es implementar una arquitectura neuro-simbólica que combine el aprendizaje profundo tabular con sistemas de recuperación de información para apoyar la toma de decisiones en ingeniería de mantenimiento.

Los objetivos específicos incluyen:

* Estimar el valor del UITI utilizando un modelo de regresión basado en mecanismos de atención (TabNet).
* Optimizar los hiperparámetros del modelo mediante búsqueda bayesiana para minimizar el error de predicción.
* Identificar las variables críticas que afectan la calidad del servicio mediante análisis de importancia de características.
* Generar reportes técnicos automáticos utilizando un sistema Agentic RAG que consulte la normativa técnica y las estadísticas del sistema para recomendar acciones de mantenimiento específicas.

## Metodología y Arquitectura Técnica

El proyecto se desarrolla en cuatro bloques funcionales:

### 1. Ingeniería de Datos y Preprocesamiento
Se realiza la ingesta del archivo en formato PKL y se aplica un saneamiento profundo. Dado que la variable objetivo (UITI) presenta una distribución de cola larga con valores extremos, se aplica una transformación logarítmica (np.log1p) para estabilizar el entrenamiento de la red neuronal. Se imputan valores faltantes y se generan tensores compatibles con PyTorch.

### 2. Modelado Predictivo (TabNet + Optuna)
Se emplea TabNet, una arquitectura de aprendizaje profundo diseñada para datos tabulares que utiliza mecanismos de atención secuencial para seleccionar características relevantes en cada paso de decisión. El entrenamiento incluye:
* Búsqueda de hiperparámetros con Optuna (optimizando tasa de aprendizaje, pasos de atención y regularización).
* Entrenamiento con función de pérdida MSE y métrica de evaluación MAE.
* Visualización de curvas de convergencia y dispersión de predicciones.

### 3. Sistema de Recuperación Aumentada (RAG)
Se implementa una base de conocimientos vectorial utilizando ChromaDB y modelos de embeddings (all-MiniLM-L6-v2). El sistema ingesta el reglamento técnico de redes aéreas de media tensión, fragmentando el texto para permitir búsquedas semánticas precisas sobre distancias de seguridad, materiales y normas constructivas.

### 4. Agente Inteligente (Agentic RAG Determinista)
Se despliega un ingeniero virtual utilizando un Modelo de Lenguaje Grande (LLM) local (Zephyr-7B cuantizado) ejecutado sobre GPU T4. El agente sigue un flujo determinista para evitar alucinaciones:
* Percibe la variable crítica identificada por TabNet.
* Calcula la correlación estadística en los datos reales.
* Recupera el artículo pertinente de la norma técnica.
* Genera un reporte técnico final recomendando acciones correctivas.

## Índices de Confiabilidad

El análisis se centra en métricas estandarizadas para la evaluación de sistemas de distribución:

### SAIFI
Índice de Frecuencia de Interrupción Promedio del Sistema. Representa la cantidad promedio de veces que un cliente experimenta una interrupción en un periodo determinado.

### SAIDI
Índice de Duración Promedio de Interrupción del Sistema. Indica el tiempo total promedio que un cliente permanece sin servicio.

### UITI
Índice Unificado de Tensión e Interrupciones. Es la variable objetivo de este estudio. Funciona como una métrica integral que pondera tanto la estabilidad de la tensión (calidad de potencia) como la frecuencia y duración de las interrupciones (confiabilidad), permitiendo una evaluación holística del punto de conexión.

## Formulación Básica de SAIFI, SAIDI y UITI

SAIFI indica cuántas interrupciones en promedio experimenta un usuario:

$$
\text{SAIFI} = \frac{\sum N_i}{N_T}
$$

donde 𝑁_𝑖 es el número de usuarios afectados por cada interrupción y 𝑁_𝑇 es el total de usuarios.

SAIDI representa la duración promedio de las interrupciones:

$$
\text{SAIDI} = \frac{\sum N_i T_i}{N_T}
$$

donde 𝑇_𝑖 es la duración de cada evento.

El UITI combina calidad de tensión y confiabilidad. Aunque su fórmula exacta depende del operador, puede expresarse de forma general como:

$$
\text{UITI} = \alpha \cdot f(\text{tensión}) + \beta \cdot \text{SAIFI} + \gamma \cdot \text{SAIDI}
$$

donde las ponderaciones α,β y γ reflejan la importancia relativa de cada componente.

## Acerca del Conjunto de Datos

El conjunto de datos contiene registros históricos de activos de la red eléctrica.

* Fuente: PowerGrid Assets ML Dataset (Kaggle).
* Estructura: Datos tabulares enriquecidos.
* Contenido: Variables geoespaciales (coordenadas), físicas (materiales, tipo de estructura), ambientales (temperatura, precipitación) y operativas.

## Enlace al Conjunto de Datos

PowerGrid Assets ML Dataset:
[https://www.kaggle.com/datasets/cristiancamiloo/powergrid-assets-ml-dataset/data](https://www.kaggle.com/datasets/cristiancamiloo/powergrid-assets-ml-dataset/data)

## Documentación y Referencia Técnica

Para la construcción del sistema RAG y la validación normativa, se utilizó el siguiente reglamento técnico oficial como base de conocimiento (Ground Truth):

Reglamento de Redes Aéreas de Media Tensión:
[https://github.com/UN-GCPDS/CRITAIR/blob/main/Regulation_files/Redes_aereas_MT.pdf](https://github.com/UN-GCPDS/CRITAIR/blob/main/Regulation_files/Redes_aereas_MT.pdf)
