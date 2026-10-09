# Predicciones Champions League 2026/27 · Poisson + Montecarlo

**Modelo probabilístico de goles para estimar resultados de la UEFA Champions League 2026/27 y simular la clasificación de la fase liga.**

El proyecto combina un modelo **Poisson de ataque, defensa y localía** con **1.000.000 de simulaciones Montecarlo** para transformar el calendario de la competición en probabilidades de partido, distribuciones de puntos y escenarios de clasificación.

<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/predicciones-champions-league-2026-27.html">
    <img src="https://img.shields.io/badge/Web-Ver%20proyecto-FF9F1C?style=for-the-badge" alt="Ver proyecto en Patrones Lab">
  </a>
  <a href="https://github.com/malcolmdpc/patrones-lab/tree/main/2026-11_champions-goals-poisson">
    <img src="https://img.shields.io/badge/GitHub-Repositorio-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repositorio GitHub">
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Estado-%E2%9C%85%20publicado-CFF7D3?style=flat-square" alt="Estado: publicado">
  <img src="https://img.shields.io/badge/Datos-2021%2F22--2026%2F27-E9D5FF?style=flat-square" alt="Datos: 2021/22–2026/27">
</p>

<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/predicciones-champions-league-2026-27.html">
    <img width="36%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p19-champions-league-2026-27-poisson-cover.webp" alt="Predicciones Champions League 2026/27">
  </a>
</p>

---

## Objetivo

Construir un sistema reproducible para estimar cómo puede desarrollarse la **fase liga de la UEFA Champions League 2026/27**.

El modelo permite calcular:

- probabilidades de victoria local, empate y victoria visitante;
- goles esperados para cada equipo;
- marcador exacto más probable;
- puntos y posición esperados;
- probabilidad de terminar entre los puestos **1–8** y clasificar directamente a octavos;
- probabilidad de terminar entre los puestos **9–24** y disputar el playoff;
- probabilidad de terminar entre los puestos **25–36** y quedar eliminado.

La idea no es producir una única tabla final, sino medir la incertidumbre mediante una distribución de escenarios posibles.

---

## Datos

El proyecto combina información histórica y datos de la edición actual.

### Histórico UEFA

El modelo se construye con partidos de competiciones UEFA entre las temporadas **2021/22 y 2025/26**:

- Champions League;
- Europa League;
- Conference League.

La base histórica procesada reúne **3.134 partidos**.

### Champions League 2026/27

La fase liga contiene:

- **36 equipos**;
- **144 partidos**;
- **8 encuentros por equipo**;
- **4 partidos como local y 4 como visitante**.

Los resultados ya disputados se incorporan al análisis y permanecen fijos dentro de las simulaciones. Los encuentros pendientes se proyectan mediante el modelo.

---

## Modelo Poisson

El modelo estima la cantidad de goles esperados de cada equipo a partir de tres componentes principales:

- **fuerza de ataque** del equipo;
- **fuerza defensiva** del rival;
- **ventaja de localía**.

Los partidos históricos tienen ponderación temporal para dar mayor importancia a los encuentros recientes, y el modelo utiliza regularización para estabilizar las estimaciones de ataque y defensa.

El resultado son dos parámetros por partido:

- `lambda_home`: goles esperados del equipo local;
- `lambda_away`: goles esperados del equipo visitante.

A partir de esas intensidades se construye la distribución de marcadores posibles.

---

## Probabilidades por partido

Para cada encuentro pendiente se calculan:

| Métrica | Interpretación |
|---|---|
| **Victoria local** | Probabilidad de que gane el equipo local |
| **Empate** | Probabilidad de igualdad |
| **Victoria visitante** | Probabilidad de que gane el visitante |
| **Marcador más probable** | Resultado exacto con mayor probabilidad |
| **Over 2.5** | Probabilidad de más de 2,5 goles |
| **Ambos marcan** | Probabilidad de que los dos equipos conviertan |

Estas probabilidades funcionan como entrada de la simulación de la fase liga.

---

## Simulación Montecarlo

La clasificación completa se simula **1.000.000 de veces**.

En cada simulación:

1. los partidos ya disputados conservan su marcador real;
2. los encuentros pendientes se simulan con las distribuciones Poisson del modelo;
3. se asignan puntos, goles a favor y goles en contra;
4. se ordenan los 36 equipos;
5. se registra la posición y el total de puntos de cada club.

Al repetir este proceso se obtiene una distribución completa de posiciones y puntos para cada equipo.

---

## Resultados

Las principales salidas del modelo son:

| Resultado | Lectura |
|---|---|
| **Probabilidad Top 8** | Clasificación directa a octavos |
| **Probabilidad playoff** | Finalización entre los puestos 9 y 24 |
| **Probabilidad de eliminación** | Finalización entre los puestos 25 y 36 |
| **Puntos esperados** | Promedio de puntos de todas las simulaciones |
| **Posición esperada** | Posición media dentro de las tablas simuladas |
| **Distribución de posiciones** | Probabilidad de terminar en cada puesto |
| **Distribución de puntos** | Probabilidad de alcanzar cada total de puntos |

El análisis también permite estudiar los puntos de corte asociados al **8.º** y **24.º puesto** y seguir cómo cambia el escenario a medida que se incorporan resultados reales.

---

## Visualizaciones

Las salidas del modelo se utilizan para construir una lectura visual de la competición.

Entre las principales visualizaciones se incluyen:

- **Mapa de rendimiento** según fuerza de ataque y defensa;
- probabilidades de Top 8, playoff y eliminación;
- distribución de posiciones para los 36 equipos;
- puntos y posiciones esperadas;
- intervalos de posiciones simuladas;
- distribución de puntos;
- análisis de los puntos de corte del 8.º y 24.º puesto;
- comparación de probabilidades entre distintos momentos de la competición;
- probabilidades y goles esperados de partidos pendientes.

Las visualizaciones forman parte del seguimiento del torneo y permiten comparar el escenario inicial con las actualizaciones posteriores.

---

## Flujo de trabajo

El proyecto sigue un flujo secuencial:

### 1. Preparación histórica

Integración, limpieza y normalización de resultados de competiciones UEFA.

### 2. Calendario 2026/27

Preparación del fixture oficial de la fase liga y normalización de los 36 equipos.

### 3. Modelo base

Estimación del modelo Poisson de ataque, defensa y localía utilizando el histórico disponible antes del comienzo de la competición.

### 4. Actualización de resultados

Incorporación de los partidos ya disputados sin modificar la base histórica original.

### 5. Probabilidades de partido

Cálculo de goles esperados, probabilidades 1X2 y métricas derivadas para los encuentros pendientes.

### 6. Simulación

Ejecución de **1.000.000 de escenarios** de la fase liga.

### 7. Análisis y visualización

Cálculo de probabilidades de clasificación, distribuciones de puntos y posiciones, puntos de corte y gráficos de seguimiento.

---

## Fuentes de datos

El proyecto utiliza información pública proveniente de distintas fuentes:

- **OpenFootball** · resultados históricos de competiciones europeas  
  https://github.com/openfootball

- **FixtureDownload** · calendario de la Champions League 2026/27  
  https://fixturedownload.com/

- **ESPN** · actualización de resultados de la competición  
  https://site.api.espn.com/apis/site/v2/sports/soccer/uefa.champions/scoreboard

- **UEFA** · referencia oficial de la competición  
  https://www.uefa.com/uefachampionsleague/

---

## Tecnologías

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/statsmodels-4051B5?style=for-the-badge" alt="statsmodels">
  <img src="https://img.shields.io/badge/SciPy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white" alt="SciPy">
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge" alt="Matplotlib">
  <img src="https://img.shields.io/badge/Poisson-6E7F6B?style=for-the-badge" alt="Modelo Poisson">
  <img src="https://img.shields.io/badge/Montecarlo-334155?style=for-the-badge" alt="Simulación Montecarlo">
</p>

---


## Proyectos relacionados

<table>
  <tr>
    <td width="50%" valign="top">
      <a href="https://malcolmdpc.github.io/proyectos/simulacion-montecarlo-laliga-2026-27.html">
        <img width="100%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p18-laliga-2026-27-montecarlo-cover.webp" alt="Simulación de Montecarlo · Predicciones para LaLiga 2026/27">
      </a>
      <br><br>
      <strong>PROYECTO 18 · ANALÍTICA DEPORTIVA</strong><br>
      <strong>Simulación de Montecarlo · Predicciones para LaLiga 2026/27</strong><br><br>
      Simulación de un millón de escenarios con ratings Elo para estimar probabilidades de campeón, Top 4, descenso, posiciones y puntos.<br><br>
      <a href="https://malcolmdpc.github.io/proyectos/simulacion-montecarlo-laliga-2026-27.html">Ver proyecto</a>
    </td>
    <td width="50%" valign="top">
      <a href="https://malcolmdpc.github.io/proyectos/simulacion-montecarlo-mundial-2026.html">
        <img width="100%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p15-montecarlo-mundial-2026-cover.webp" alt="Simulación de Montecarlo · Predicciones para el Mundial 2026">
      </a>
      <br><br>
      <strong>PROYECTO 15 · ANALÍTICA DEPORTIVA</strong><br>
      <strong>Simulación de Montecarlo · Predicciones para el Mundial 2026</strong><br><br>
      Modelo probabilístico con ratings Elo y simulación Montecarlo para estimar probabilidades de avance y campeonato en el Mundial 2026.<br><br>
      <a href="https://malcolmdpc.github.io/proyectos/simulacion-montecarlo-mundial-2026.html">Ver proyecto</a>
    </td>
  </tr>
</table>

---

## Enlaces

- [Ver proyecto en Patrones Lab](https://malcolmdpc.github.io/proyectos/predicciones-champions-league-2026-27.html)
- [Repositorio del proyecto](https://github.com/malcolmdpc/patrones-lab/tree/main/2026-11_champions-goals-poisson)
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
