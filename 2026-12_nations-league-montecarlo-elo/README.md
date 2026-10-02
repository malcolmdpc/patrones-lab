# Simulación de Montecarlo · Nations League 2026/27

**Modelo probabilístico para estimar el desarrollo de la UEFA Nations League 2026/27 a partir de ratings Elo, un modelo Davidson, un modelo Poisson y simulación Montecarlo.**

El proyecto se concentra en la **Liga A** y estima la probabilidad de que cada selección avance desde la fase de grupos hasta cuartos de final, semifinales, final y campeonato.

<p align="center">
  <a href="https://github.com/malcolmdpc/patrones-lab/tree/main/2026-12_nations-league-montecarlo-elo">
    <img src="https://img.shields.io/badge/GitHub-Repositorio-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repositorio GitHub">
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Estado-%E2%9A%A0%EF%B8%8F%20en%20desarrollo-FFF3BF?style=flat-square" alt="Estado: en desarrollo">
  <img src="https://img.shields.io/badge/Datos-2018%2F19--2026%2F27-E9D5FF?style=flat-square" alt="Datos: 2018/19–2026/27">
</p>

---

## Objetivo

El objetivo es modelar la **Liga A de la UEFA Nations League 2026/27** y transformar el torneo en una distribución de escenarios posibles.

La simulación permite estimar para cada selección:

- probabilidad de terminar primera o segunda de grupo;
- probabilidad de clasificar a cuartos de final;
- probabilidad de llegar a semifinales;
- probabilidad de alcanzar la final;
- probabilidad de salir campeona.

El modelo también permite seguir cómo cambian esas probabilidades a medida que se cargan nuevos resultados y se actualizan los ratings Elo.

---

## Datos

El proyecto combina tres fuentes principales de información:

- resultados históricos de la Nations League;
- ratings Elo de selecciones;
- calendario y resultados oficiales de la edición 2026/27.

Para calibrar el modelo se utiliza el histórico de la **Liga A** desde la edición 2018/19 hasta 2024/25.

La edición 2026/27 se modela con sus **16 selecciones**, distribuidas en cuatro grupos:

| Grupo | Selecciones |
|---|---|
| **A1** | Francia · Italia · Bélgica · Turquía |
| **A2** | Alemania · Países Bajos · Serbia · Grecia |
| **A3** | España · Croacia · Inglaterra · Chequia |
| **A4** | Portugal · Dinamarca · Noruega · Gales |

Los partidos ya jugados se mantienen con su resultado real y la simulación se aplica sobre los encuentros pendientes.

---

## Modelo Elo + Davidson + Poisson

El proyecto combina tres componentes.

### Ratings Elo

Los ratings Elo representan la fortaleza relativa de cada selección y se utilizan como base para comparar el nivel de los equipos antes de cada partido.

### Modelo Davidson

A partir de la diferencia de Elo, el modelo Davidson estima tres probabilidades:

- victoria local;
- empate;
- victoria visitante.

Esto permite trabajar con un resultado 1X2 y contemplar de forma explícita la posibilidad de empate.

### Modelo Poisson

El modelo Poisson se utiliza para generar marcadores compatibles con las probabilidades estimadas.

Los marcadores permiten resolver situaciones en las que el resultado exacto es necesario, como:

- diferencia de goles;
- desempates de grupo;
- resultados acumulados en cuartos de final;
- prórroga y penales en la fase final.

---

## Simulación Montecarlo

El torneo se simula **1.000.000 de veces**.

Cada simulación recorre todas las etapas de la Liga A:

1. fase de grupos;
2. clasificación de los dos primeros de cada grupo;
3. cuartos de final a ida y vuelta;
4. semifinales;
5. final.

En la fase de grupos se aplican los criterios de desempate correspondientes, incluyendo los enfrentamientos directos cuando son necesarios.

Los resultados ya observados permanecen fijos, mientras que los partidos pendientes se resuelven a partir de las probabilidades generadas por el modelo.

---

## Resultados

Las principales salidas del proyecto son:

| Resultado | Lectura |
|---|---|
| **Probabilidad de ganar el grupo** | Frecuencia con la que una selección termina primera |
| **Probabilidad de cuartos** | Frecuencia con la que clasifica entre las dos primeras |
| **Probabilidad de semifinales** | Frecuencia con la que supera los cuartos de final |
| **Probabilidad de final** | Frecuencia con la que gana su semifinal |
| **Probabilidad de campeón** | Frecuencia con la que gana el torneo |

Además, la simulación permite analizar:

- puntos esperados por selección;
- posición probable dentro del grupo;
- posibles cruces de cuartos;
- recorridos hasta la final;
- evolución de las probabilidades a medida que avanza el torneo.

---

## Visualizaciones

El proyecto transforma los resultados de la simulación en gráficos orientados a seguir la competencia desde distintos ángulos.

Entre las visualizaciones desarrolladas se incluyen:

- ranking de probabilidad de campeón;
- probabilidades de clasificación por selección;
- probabilidades por etapa del torneo;
- distribución de posiciones dentro de cada grupo;
- posibles cruces de cuartos de final;
- caminos más probables hacia la final;
- comparación entre ratings Elo y probabilidades simuladas;
- evolución de probabilidades a medida que se incorporan resultados.

Las visualizaciones mantienen la estética de Patrones Lab, con una composición oscura y una línea gráfica consistente con los demás proyectos de analítica deportiva.

---

## Flujo de trabajo

El desarrollo se organiza en las siguientes etapas:

### 1. Preparación histórica

Selección de los partidos de Liga A utilizados para calibrar el modelo.

### 2. Estimación

Ajuste del modelo Davidson sobre resultados históricos y preparación del componente Poisson para generar marcadores.

### 3. Preparación de la edición 2026/27

Carga del calendario, resultados disponibles y ratings Elo actuales.

### 4. Modelo de partido

Estimación de probabilidades 1X2 y generación de marcadores para cada encuentro.

### 5. Fase de grupos

Simulación de los grupos y aplicación de los criterios de clasificación y desempate.

### 6. Fase eliminatoria

Simulación de cuartos de final, semifinales y final hasta obtener un campeón.

### 7. Resultados y visualización

Cálculo de probabilidades acumuladas y construcción de gráficos para comunicar los escenarios del torneo.

---

## Fuentes de datos

El proyecto utiliza información pública proveniente de:

- **UEFA** · calendario, grupos y resultados oficiales de la Nations League  
  https://www.uefa.com/uefanationsleague/

- **World Football Elo Ratings** · ratings Elo de selecciones  
  https://www.eloratings.net/

- **Mart Jürisoo · International football results** · resultados históricos de selecciones  
  https://github.com/martj42/international_results

---

## Tecnologías

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/SciPy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white" alt="SciPy">
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge" alt="Matplotlib">
  <img src="https://img.shields.io/badge/Elo-8D7130?style=for-the-badge" alt="Ratings Elo">
  <img src="https://img.shields.io/badge/Davidson-5B6F8A?style=for-the-badge" alt="Modelo Davidson">
  <img src="https://img.shields.io/badge/Poisson-6E7F6B?style=for-the-badge" alt="Modelo Poisson">
  <img src="https://img.shields.io/badge/Montecarlo-334155?style=for-the-badge" alt="Simulación Montecarlo">
</p>

---

## Enlaces

- [Repositorio del proyecto](https://github.com/malcolmdpc/patrones-lab/tree/main/2026-12_nations-league-montecarlo-elo)
- [UEFA Nations League](https://www.uefa.com/uefanationsleague/)
- [World Football Elo Ratings](https://www.eloratings.net/)
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
