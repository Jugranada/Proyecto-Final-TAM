# 📌 Descripción del Problema

La empresa **CHEC (Central Hidroeléctrica de Caldas)** es una prestadora del servicio de energía eléctrica en Colombia. Garantizar un servicio continuo y de alta calidad es fundamental para mantener la satisfacción del usuario y asegurar el correcto funcionamiento de la red de distribución.

Este proyecto utiliza un conjunto de datos académico que contiene información **técnica, operativa, estructural y meteorológica** de puntos y equipos de la red eléctrica. El objetivo principal es desarrollar un modelo de aprendizaje automático capaz de **predecir el índice UITI (Índice Unificado de Tensión e Interrupciones)**, una métrica integral que resume la calidad del servicio eléctrico a nivel de punto de red.

---

## 🎯 Objetivo del Proyecto

El propósito del análisis es **estimar el UITI** a partir de las características disponibles en el dataset. Este índice funciona como una **variable objetivo** dentro de un modelo supervisado y permite evaluar la calidad del servicio incluso en escenarios donde no se presentan cortes perceptibles por parte del usuario.

Predecir el UITI puede ayudar a:

- Identificar zonas críticas o vulnerables de la red  
- Anticipar problemas de calidad de tensión  
- Evaluar el rendimiento de equipos instalados  
- Priorizar mantenimientos preventivos  
- Mejorar la percepción del servicio por parte del usuario  

---

## 📊 Índices de Confiabilidad

Para contextualizar el UITI, es importante comprender los índices tradicionales usados en sistemas eléctricos:

### **SAIFI** – *Índice de Frecuencia de Interrupción Promedio del Sistema*  
Número promedio de interrupciones experimentadas por cliente.  
\[
\text{SAIFI} = \frac{\text{Total customer interruptions}}{\text{Total customers served}}
\]

### **SAIDI** – *Índice de Duración Promedio de Interrupción del Sistema*  
Duración promedio total de las interrupciones por cliente.  
\[
\text{SAIDI} = \frac{\text{Total customer interruption duration}}{\text{Total customers served}}
\]

### **CAIDI** – *Índice de Duración Promedio de Interrupción por Cliente*  
Duración promedio por interrupción.  
\[
\text{CAIDI} = \frac{\text{SAIDI}}{\text{SAIFI}}
\]

### **UITI** – *Índice Unificado de Tensión e Interrupciones*  
Es una métrica compuesta que integra:
- Estabilidad de la tensión  
- Frecuencia de interrupciones  
- Duración de interrupciones  

SAIFI y SAIDI son componentes clave que influyen directamente en el valor final del UITI.

---

## 🗂️ Acerca del Conjunto de Datos

- **Formato:** PKL  
- **Filas:** Cada fila representa un punto de red o equipo  
- **Columnas:** Variables técnicas, operativas, estructurales, ambientales y la variable objetivo UITI

## 📎 Enlace al Conjunto de Datos

El conjunto de datos utilizado en este proyecto está disponible en Kaggle:

- **PowerGrid Assets ML Dataset**  
  https://www.kaggle.com/datasets/cristiancamiloo/powergrid-assets-ml-dataset/data

-## 📄 Paper de Referencia del Estado del Arte

- Mossie, M. A., Yetayew, T. T., Bitew, G. T., Yenealem, M. G., Beza, T. M. (2025). *Machine learning algorithms for voltage stability assessment in electrical distribution systems.* Scientific Reports. DOI: https://doi.org/10.1038/s41598-025-15791-2  




