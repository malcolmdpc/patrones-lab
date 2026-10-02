# Redes Neuronales · Daños en Eventos Meteorológicos

**Modelo de clasificación para estimar la probabilidad de daño económico en eventos meteorológicos, comparando una regresión logística con una red neuronal.**

El proyecto utiliza datos públicos de **NOAA / NCEI Storm Events** para analizar si un evento meteorológico registra daños económicos y evaluar cuánto mejora un modelo no lineal frente a una referencia más simple e interpretable.

<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/red-neuronal-danos-eventos-meteorologicos.html">
    <img src="https://img.shields.io/badge/Web-Ver%20proyecto-FF9F1C?style=for-the-badge" alt="Ver proyecto en Patrones Lab">
  </a>
  <a href="https://github.com/malcolmdpc/patrones-lab/tree/main/2026-08_storm-events-neural-network">
    <img src="https://img.shields.io/badge/GitHub-Repositorio-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repositorio GitHub">
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Estado-%E2%9A%A0%EF%B8%8F%20en%20desarrollo-FFF3BF?style=flat-square" alt="Estado: en desarrollo">
  <img src="https://img.shields.io/badge/Datos-2010--2025-E9D5FF?style=flat-square" alt="Datos: 2010–2025">
</p>

<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/red-neuronal-danos-eventos-meteorologicos.html">
    <img width="36%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p16-storm-events-neural-network-cover.webp" alt="Redes Neuronales · Daños en Eventos Meteorológicos">
  </a>
</p>

---

## Objetivo

Construir un modelo de **clasificación binaria** que estime la probabilidad de que un evento meteorológico registre daño económico.

El análisis compara dos enfoques:

- **Regresión logística**, utilizada como modelo de referencia.
- **Red neuronal**, orientada a capturar relaciones no lineales entre las variables.

La comparación busca medir si la red neuronal mejora la detección de eventos con daños sin perder una referencia clara para interpretar el desempeño.

---

## Datos

La fuente utilizada es **NOAA / NCEI Storm Events**, a partir de los archivos `Details`.

La base analizada reúne:

- **1.037.691 eventos meteorológicos**;
- período **2010–2025**;
- **19 variables** temporales, geográficas y meteorológicas;
- una variable objetivo binaria que identifica si el evento registra daño económico.

La unidad de análisis es cada evento meteorológico individual registrado en Storm Events.

---

## División temporal

La evaluación respeta el orden cronológico de los datos:

| Período | Uso |
|---|---|
| **2010–2021** | Entrenamiento |
| **2022–2023** | Validación |
| **2024–2025** | Test final |

Esta separación permite evaluar los modelos sobre eventos posteriores a los utilizados durante el entrenamiento.

---

## Preparación de datos

El flujo de preparación incluye:

- construcción de la variable objetivo;
- selección de variables explicativas;
- tratamiento de variables numéricas y categóricas;
- preprocesamiento consistente entre entrenamiento, validación y test;
- preparación de los datos para los dos modelos comparados.

La misma base temporal y el mismo criterio de evaluación se utilizan para la regresión logística y la red neuronal.

---

## Modelos

### Regresión logística

Funciona como **baseline** del proyecto.

Permite establecer una referencia de desempeño mediante un modelo supervisado más simple antes de evaluar la red neuronal.

### Red neuronal

La red neuronal se desarrolla con **Keras / TensorFlow** sobre el mismo conjunto de variables.

El objetivo es capturar relaciones no lineales que la regresión logística no puede representar de la misma manera y comparar su capacidad para identificar eventos con daño económico.

---

## Resultados

La comparación final se realiza sobre el período **2024–2025**.

| Métrica | Regresión logística | Red neuronal |
|---|---:|---:|
| **ROC AUC** | 0,8961 | **0,9324** |
| **PR AUC** | 0,6691 | **0,8004** |
| **F1 · clase positiva** | 0,6042 | **0,6991** |

La red neuronal obtiene mejores resultados en las tres métricas principales utilizadas para comparar los modelos.

La diferencia más marcada aparece en **PR AUC**, donde el valor pasa de **0,6691** a **0,8004**, acompañada también por una mejora del F1 de la clase positiva.

---

## Lectura del modelo

El proyecto está orientado a responder una pregunta concreta:

> **Dadas las características de un evento meteorológico, ¿qué probabilidad tiene de registrar daño económico?**

La regresión logística permite construir una referencia sólida y la red neuronal amplía esa capacidad al modelar relaciones más complejas entre las variables.

La comparación entre ambos enfoques permite evaluar la ganancia real obtenida al incorporar una arquitectura no lineal.

---

## Flujo de trabajo

El proyecto se organiza en cinco notebooks que cubren las principales etapas del desarrollo:

1. **Obtención y preparación de los datos**
2. **Análisis y construcción de variables**
3. **Preprocesamiento**
4. **Regresión logística y red neuronal**
5. **Validación y comparación de resultados**

Además del modelado, el proyecto genera predicciones y métricas para comparar ambos enfoques sobre el mismo conjunto de test.

---

## Tecnologías

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white" alt="Scikit-learn">
  <img src="https://img.shields.io/badge/Keras-D00000?style=for-the-badge&logo=keras&logoColor=white" alt="Keras">
  <img src="https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white" alt="TensorFlow">
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge" alt="Matplotlib">
  <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub">
</p>

---

## Fuente de datos

Los datos provienen de **NOAA / National Centers for Environmental Information (NCEI)**:

**Storm Events Database · Bulk CSV Files**  
https://www.ncei.noaa.gov/pub/data/swdi/stormevents/csvfiles/

El proyecto utiliza los archivos de detalle de eventos meteorológicos correspondientes al período analizado.

---

## Enlaces

- [Ver proyecto en Patrones Lab](https://malcolmdpc.github.io/proyectos/red-neuronal-danos-eventos-meteorologicos.html)
- [Repositorio del proyecto](https://github.com/malcolmdpc/patrones-lab/tree/main/2026-08_storm-events-neural-network)
- [NOAA / NCEI Storm Events](https://www.ncei.noaa.gov/pub/data/swdi/stormevents/csvfiles/)
- [LinkedIn](https://www.linkedin.com/in/malcolmdpc/)

---

<p align="center">
  <strong>Patrones Lab</strong> · Generando conocimiento a partir de los datos
  <br>
  <a href="https://malcolmdpc.github.io/">Web</a>
  ·
  <a href="https://github.com/malcolmdpc/patrones-lab">Repositorio</a>
  ·
  <a href="https://www.linkedin.com/in/malcolmdpc/">LinkedIn</a>
</p>
