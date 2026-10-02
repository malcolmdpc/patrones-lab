# Analítica de Fútbol · StatsBomb Open Data

**Analítica deportiva con datos públicos de StatsBomb: xG, Peligro Esperado y radares de percentiles.**

Esta carpeta reúne una línea de trabajo sobre fútbol desarrollada dentro de **Patrones Lab**. A partir del mismo ecosistema de datos se construyeron tres proyectos distintos: un modelo de **Goles Esperados (xG)**, una métrica propia de **Peligro Esperado a 5 acciones (PE5)** inspirada en xT y un análisis de jugadores del Mundial Qatar 2022 mediante **radares de percentiles**.

<p align="center">
  <a href="https://malcolmdpc.github.io/areas/analitica-deportiva.html">
    <img src="https://img.shields.io/badge/Web-Analítica%20Deportiva-5B6F8A?style=for-the-badge" alt="Web · Analítica Deportiva">
  </a>
  <a href="https://github.com/malcolmdpc/patrones-lab">
    <img src="https://img.shields.io/badge/GitHub-Patrones%20Lab-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub · Patrones Lab">
  </a>
  <a href="https://github.com/statsbomb/open-data">
    <img src="https://img.shields.io/badge/Datos-StatsBomb%20Open%20Data-0F172A?style=for-the-badge" alt="StatsBomb Open Data">
  </a>
</p>

---

## Proyectos publicados

<table>
  <tr>
    <td width="33.33%" valign="top">
      <a href="https://malcolmdpc.github.io/proyectos/modelo-ml-goles-esperados-xg.html">
        <img width="100%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p06-xg-futbol-statsbomb-cover.webp" alt="Modelo Machine Learning · Goles Esperados xG">
      </a>
      <br><br>
      <strong>06 · Modelo Machine Learning · Goles Esperados (xG)</strong><br><br>
      <img src="https://img.shields.io/badge/Estado-%E2%9C%85%20publicado-CFF7D3?style=flat-square" alt="Estado: publicado"><br>
      <img src="https://img.shields.io/badge/Aplicación-Qatar%202022-E9D5FF?style=flat-square" alt="Aplicación: Qatar 2022"><br><br>
      Regresión logística para estimar la probabilidad de gol de cada tiro, con validación por partido y aplicación externa al Mundial Qatar 2022.<br><br>
      <kbd>Python</kbd> <kbd>Machine Learning</kbd> <kbd>Regresión logística</kbd> <kbd>xG</kbd><br><br>
      <a href="https://malcolmdpc.github.io/proyectos/modelo-ml-goles-esperados-xg.html">Ver proyecto</a>
    </td>
    <td width="33.33%" valign="top">
      <a href="https://malcolmdpc.github.io/proyectos/probabilidades-futbol-peligro-esperado-xt.html">
        <img width="100%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p07-xt-futbol-statsbomb-cover.webp" alt="Probabilidades en el Fútbol · Peligro Esperado xT y PE5">
      </a>
      <br><br>
      <strong>07 · Probabilidades en el Fútbol · Peligro Esperado</strong><br><br>
      <img src="https://img.shields.io/badge/Estado-%E2%9C%85%20publicado-CFF7D3?style=flat-square" alt="Estado: publicado"><br>
      <img src="https://img.shields.io/badge/Datos-2018%20%2B%202022-E9D5FF?style=flat-square" alt="Datos: Mundiales 2018 y 2022"><br><br>
      PE5 mide cuánto cambia el peligro de una posesión según el movimiento entre zonas y la probabilidad de gol en una ventana de cinco acciones.<br><br>
      <kbd>Python</kbd> <kbd>Football Analytics</kbd> <kbd>xT</kbd> <kbd>PE5</kbd><br><br>
      <a href="https://malcolmdpc.github.io/proyectos/probabilidades-futbol-peligro-esperado-xt.html">Ver proyecto</a>
    </td>
    <td width="33.33%" valign="top">
      <a href="https://malcolmdpc.github.io/proyectos/estadisticas-mundial-futbol-qatar-2022.html">
        <img width="100%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p11-mundial-2022-radar-percentiles-cover.webp" alt="Estadísticas del Mundial 2022 · Radar de Percentiles">
      </a>
      <br><br>
      <strong>11 · Estadísticas del Mundial 2022 · Radar de Percentiles</strong><br><br>
      <img src="https://img.shields.io/badge/Estado-%E2%9C%85%20publicado-CFF7D3?style=flat-square" alt="Estado: publicado"><br>
      <img src="https://img.shields.io/badge/Datos-Qatar%202022-E9D5FF?style=flat-square" alt="Datos: Qatar 2022"><br><br>
      Comparación de jugadores mediante métricas por 90 minutos y percentiles calculados dentro de grupos de posición equivalentes.<br><br>
      <kbd>Python</kbd> <kbd>StatsBomb</kbd> <kbd>Percentiles</kbd> <kbd>Data Visualization</kbd><br><br>
      <a href="https://malcolmdpc.github.io/proyectos/estadisticas-mundial-futbol-qatar-2022.html">Ver proyecto</a>
    </td>
  </tr>
</table>

---

## 1 · Goles Esperados (xG)

El objetivo es estimar la **probabilidad de que un tiro termine en gol** a partir de información disponible antes de conocer el resultado de la acción.

### Datos y preparación

- Se parte de competiciones masculinas disponibles en StatsBomb Open Data desde **2015 en adelante**.
- La extracción reúne **63.740 tiros de 2.526 partidos**.
- Luego de excluir tandas de penales, la base utilizada para modelado contiene **63.482 tiros**.
- Se derivan variables espaciales como **distancia al arco** y **ángulo de tiro**.
- También se incorporan parte del cuerpo, tipo de tiro, técnica, presión y posición del jugador.
- La separación entre entrenamiento y test se hace **por partido** mediante `GroupShuffleSplit`, evitando que tiros del mismo encuentro queden repartidos entre ambos conjuntos.
- Argentina, Francia, Marruecos y Croacia en Qatar 2022 se reservan como conjunto externo de aplicación.

### Modelo

El modelo final es una **regresión logística regularizada con L1**. Después de la selección quedan **12 variables**, con especial peso de la distancia al arco, el ángulo, la parte del cuerpo y el contexto del tiro.

La validación no se limita a una métrica de clasificación: también se revisan ROC AUC, Precision-Recall, Brier Score, Log Loss, calibración por deciles, KS, lift y cumulative gains.

### Resultado

| Dataset | Tiros | Goles reales | xG estimado | ROC AUC | Brier |
|---|---:|---:|---:|---:|---:|
| Train | 47.082 | 4.943 | 4.992,7 | 0,793 | 0,078 |
| Test | 15.890 | 1.688 | 1.674,0 | 0,795 | 0,079 |
| Aplicación Qatar 2022 | 510 | 57 | 58,2 | 0,765 | 0,084 |

En el conjunto de test, el modelo estima **1.674 xG frente a 1.688 goles reales**. En la aplicación externa a Qatar 2022 estima **58,2 xG frente a 57 goles observados**.

---

## 2 · Peligro Esperado a 5 acciones (PE5)

PE5 es una métrica propia inspirada en el enfoque de **Expected Threat (xT)**. En lugar de limitarse al tiro, busca medir el peligro que se construye **antes del gol**.

### Metodología

- Se analizan los Mundiales de **Rusia 2018 y Qatar 2022**.
- La base reúne **128 partidos y 462.501 eventos**.
- Se seleccionan pases, conducciones, regates y tiros con ubicación disponible.
- La cancha se divide en una grilla de **12 × 8 = 96 zonas**.
- Cada acción se marca según si la posesión termina en gol en la acción actual o dentro de las **cuatro acciones siguientes**.
- Se obtienen **230.739 acciones ofensivas** para estimar el valor zonal y **1.227 acciones** dentro de una ventana de gol.
- Los penales se excluyen del cálculo zonal.
- Los pases completados y las conducciones se valoran como:

`PE5 de la zona destino − PE5 de la zona origen`

Una acción suma valor cuando mueve la pelota hacia una zona con mayor probabilidad de gol y resta valor cuando ocurre lo contrario.

Las dos zonas de mayor peligro alcanzan valores aproximados de **0,202 y 0,198**.

### Aplicación · Final Argentina vs Francia

PE5 permite leer la final del Mundial 2022 desde la construcción de peligro y no solamente desde los goles.

Entre los jugadores argentinos, los mayores valores netos fueron:

| Jugador | PE5 |
|---|---:|
| Lionel Messi | 0,455 |
| Alexis Mac Allister | 0,265 |
| Gonzalo Montiel | 0,227 |
| Ángel Di María | 0,181 |
| Rodrigo De Paul | 0,156 |

En la evolución completa del partido, Argentina termina con **1,670 PE5 acumulado** y Francia con **1,042**. El análisis también incluye momentum por tramos de cinco minutos, acciones de mayor incremento de peligro y evolución individual de los jugadores.

[Leer el análisis publicado en LinkedIn](https://es.linkedin.com/pulse/f%C3%BAtbol-y-probabilidades-c%C3%A1lculo-del-peligro-esperado-malcolm-acide)

---

## 3 · Radar de Percentiles · Qatar 2022

Este análisis transforma los eventos del Mundial Qatar 2022 en perfiles comparables de rendimiento individual.

La comparación se hace **dentro de cada grupo posicional**, para evitar enfrentar con las mismas métricas a jugadores con funciones distintas.

### Grupos utilizados

- Arqueros
- Centrales
- Laterales
- Mediocampistas
- Ofensivos / delanteros

Las métricas de volumen se normalizan **por 90 minutos** y se filtran jugadores con al menos **180 minutos disputados**.

Cada perfil utiliza variables diferentes según la posición. Entre ellas aparecen:

- goles, xG, tiros y tiros al arco;
- asistencias y pases clave;
- pases y conducciones progresivas;
- acciones en el último tercio y dentro del área;
- recuperaciones, presiones e intercepciones;
- duelos y duelos aéreos;
- centros;
- atajadas y acciones específicas de arquero.

Finalmente, cada métrica se transforma en un **percentil dentro del grupo comparable** y se representa mediante radares `PyPizza` de `mplsoccer`.

El resultado permite leer perfiles distintos aun dentro de una misma selección: volumen y progresión, precisión de pase, creación ofensiva, presión, juego aéreo o participación en situaciones de gol.

---

## Flujo de trabajo

La carpeta reúne tres líneas de análisis construidas sobre datos de eventos de StatsBomb:

1. **Peligro Esperado (PE5)**  
   Construcción de una métrica zonal para medir cómo cambia el peligro de una posesión antes del gol y aplicación a partidos del Mundial.

2. **Radares de percentiles**  
   Preparación de métricas por posición, normalización por 90 minutos y comparación de jugadores del Mundial Qatar 2022.

3. **Goles Esperados (xG)**  
   Extracción y preparación de tiros, construcción de variables, entrenamiento del modelo, validación y aplicación sobre partidos del Mundial Qatar 2022.

El flujo general pasa de la preparación de eventos y variables al modelado, la validación y la construcción de visualizaciones para comunicar los resultados.

---

## Visualizaciones

La carpeta `visuals/` reúne salidas utilizadas en las publicaciones de Patrones Lab, entre ellas:

- mapa de probabilidad PE5 por zona;
- mapa de cantidad de acciones por zona;
- ranking de PE5 por jugador;
- generación y reducción de peligro;
- momentum por tramos de cinco minutos;
- evolución acumulada de PE5;
- radares de percentiles de jugadores de Qatar 2022.


---

## Tecnologías

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white" alt="Scikit-learn">
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge" alt="Matplotlib">
  <img src="https://img.shields.io/badge/StatsBombPy-0F172A?style=for-the-badge" alt="StatsBombPy">
  <img src="https://img.shields.io/badge/mplsoccer-1E88E5?style=for-the-badge" alt="mplsoccer">
  <img src="https://img.shields.io/badge/Plotly-3F4F75?style=for-the-badge&logo=plotly&logoColor=white" alt="Plotly">
</p>

---

## Fuente de datos

Los proyectos utilizan **StatsBomb Open Data**, disponible públicamente para investigación y análisis de fútbol.

- [StatsBomb Open Data](https://github.com/statsbomb/open-data)
- [StatsBombPy](https://github.com/statsbomb/statsbombpy)

StatsBomb es la fuente de los datos de competiciones, partidos, eventos y alineaciones utilizados en estos análisis.

---

## Alcance

Los tres trabajos responden preguntas distintas sobre el mismo deporte:

**xG** mide la calidad de una ocasión de tiro.  
**PE5** busca medir cómo se construye el peligro antes del gol.  
**Los radares de percentiles** comparan el perfil de rendimiento de los jugadores dentro de su posición.

En conjunto, la carpeta funciona como una línea de trabajo de **analítica deportiva aplicada al fútbol**, desde eventos crudos hasta modelos probabilísticos, métricas derivadas y visualizaciones orientadas a interpretar el juego.

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
