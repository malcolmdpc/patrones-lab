# Simulación de Montecarlo · Predicciones para LaLiga 2026/27

**Modelo probabilístico para estimar resultados de LaLiga 2026/27 a partir de ratings Elo, un modelo Davidson y simulación Montecarlo.**

El proyecto analiza la temporada completa de LaLiga y estima la probabilidad de que cada equipo termine campeón, clasifique al Top 4 o descienda, además de proyectar puntos y posiciones finales.

<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/simulacion-montecarlo-laliga-2026-27.html">
    <img src="https://img.shields.io/badge/Web-Ver%20proyecto-FF9F1C?style=for-the-badge" alt="Ver proyecto en Patrones Lab">
  </a>
  <a href="https://github.com/malcolmdpc/patrones-lab/tree/main/2026-10_laliga-montecarlo-elo">
    <img src="https://img.shields.io/badge/GitHub-Repositorio-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repositorio GitHub">
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Estado-%E2%9A%A0%EF%B8%8F%20en%20desarrollo-FFF3BF?style=flat-square" alt="Estado: en desarrollo">
  <img src="https://img.shields.io/badge/Datos-2026-E9D5FF?style=flat-square" alt="Datos: 2026">
</p>

<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/simulacion-montecarlo-laliga-2026-27.html">
    <img width="36%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p18-laliga-2026-27-montecarlo-cover.webp" alt="Simulación de Montecarlo · Predicciones para LaLiga 2026/27">
  </a>
</p>

---

## Objetivo

El objetivo es estimar cómo puede terminar LaLiga 2026/27 a partir de la fortaleza relativa de los equipos y del calendario real de la temporada.

El modelo simula **1.000.000 de temporadas** y calcula la frecuencia con la que cada club alcanza distintos resultados:

- campeonato;
- Top 4;
- descenso;
- posición final;
- puntos acumulados.

La idea es pasar de una única predicción de tabla a una distribución de escenarios posibles para los 20 equipos.

---

## Datos

El proyecto combina tres tipos de información:

- resultados históricos recientes de LaLiga;
- ratings Elo de los equipos;
- calendario y resultados de LaLiga 2026/27.

La temporada se modela con sus **20 equipos**, **38 partidos por club** y **380 partidos** en total.

A medida que avanza el campeonato, los partidos ya jugados se mantienen con su resultado real y la simulación se concentra en los encuentros pendientes.

---

## Modelo Elo + Davidson

Los ratings Elo representan la fortaleza relativa de cada equipo.

Sobre esa diferencia de nivel se aplica un **modelo Davidson**, que estima tres probabilidades para cada partido:

- victoria local;
- empate;
- victoria visitante.

El modelo incorpora dos elementos importantes del fútbol de liga:

- **ventaja de local**;
- **propensión al empate**.

Los parámetros se estiman con partidos históricos de LaLiga y luego se aplican a la temporada 2026/27.

Los ratings Elo se utilizan como referencia fija dentro de cada simulación, por lo que el foco está puesto en cómo la combinación entre nivel relativo, localía y calendario puede modificar la tabla final.

---

## Simulación Montecarlo

Cada simulación reproduce todos los partidos pendientes de la temporada.

Para cada encuentro:

1. se identifican local y visitante;
2. se obtiene la diferencia de rating Elo;
3. el modelo Davidson calcula las probabilidades de victoria, empate y derrota;
4. se simula uno de los tres resultados;
5. se asignan los puntos correspondientes;
6. al terminar la temporada se construye la tabla final.

Este proceso se repite **1.000.000 de veces**.

A partir de todas las tablas simuladas se obtiene una distribución de resultados para cada club.

---

## Resultados

Las principales salidas del modelo son:

| Resultado | Lectura |
|---|---|
| **Probabilidad de campeón** | Frecuencia con la que cada equipo termina 1.º |
| **Probabilidad de Top 4** | Frecuencia con la que termina entre los cuatro primeros |
| **Probabilidad de descenso** | Frecuencia con la que termina en zona de descenso |
| **Puntos esperados** | Promedio de puntos obtenidos en las simulaciones |
| **Posición esperada** | Posición media dentro de las tablas simuladas |
| **Distribución de posiciones** | Probabilidad de finalizar en cada puesto |

Estas salidas permiten comparar tanto la parte alta como la zona media y baja de la tabla.

---

## Visualizaciones

El proyecto transforma las simulaciones en visualizaciones orientadas a distintas preguntas sobre la temporada.

Entre las principales se incluyen:

- ranking de probabilidad de campeón;
- ranking de probabilidad de Top 4;
- ranking de probabilidad de descenso;
- puntos esperados por equipo;
- posición final esperada;
- heatmap de probabilidades por posición;
- relación entre rating Elo y puntos promedio;
- probabilidades de próximos partidos.

Las visualizaciones siguen la línea gráfica de Patrones Lab y permiten actualizar la lectura del campeonato a medida que se incorporan nuevos resultados.

---

## Flujo de trabajo

El desarrollo se organiza en seis etapas:

### 1. Ingesta y calidad

Carga de resultados históricos, ratings Elo, calendario y resultados de la temporada.

### 2. Preparación

Normalización de equipos, fechas y variables necesarias para construir una base consistente.

### 3. Modelado

Estimación del modelo Davidson y de los parámetros asociados a localía y empate.

### 4. Validación

Evaluación temporal del modelo sobre partidos posteriores a los utilizados para estimar los parámetros.

### 5. Simulación

Aplicación del modelo a LaLiga 2026/27 y ejecución de las simulaciones Montecarlo.

### 6. Visualización

Construcción de rankings, distribuciones y gráficos de probabilidades para comunicar los resultados.

---

## Fuentes de datos

El proyecto utiliza información proveniente de distintas fuentes públicas:

- **Football-Data.co.uk** · resultados históricos de LaLiga  
  https://www.football-data.co.uk/spainm.php

- **ClubElo** · ratings Elo de clubes  
  http://clubelo.com/

- **LaLiga** · calendario y resultados de la temporada  
  https://www.laliga.com/

---

## Tecnologías

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/SciPy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white" alt="SciPy">
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge" alt="Matplotlib">
  <img src="https://img.shields.io/badge/Elo-8D7130?style=for-the-badge" alt="Ratings Elo">
  <img src="https://img.shields.io/badge/Montecarlo-334155?style=for-the-badge" alt="Simulación Montecarlo">
</p>


---

## Enlaces

- [Ver proyecto en Patrones Lab](https://malcolmdpc.github.io/proyectos/simulacion-montecarlo-laliga-2026-27.html)
- [Repositorio del proyecto](https://github.com/malcolmdpc/patrones-lab/tree/main/2026-10_laliga-montecarlo-elo)
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
