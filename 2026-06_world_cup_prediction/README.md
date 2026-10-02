# Simulación de Montecarlo · Predicciones para el Mundial 2026

**Modelo probabilístico aplicado al Mundial de Fútbol 2026 mediante ratings Elo y simulación Montecarlo.**

El proyecto estima la probabilidad de que cada selección avance por la fase de eliminación directa y salga campeona, combinando la fortaleza relativa de los equipos con el armado de las llaves del torneo.

<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/simulacion-montecarlo-mundial-2026.html">
    <img src="https://img.shields.io/badge/Web-Ver%20proyecto-FF9F1C?style=for-the-badge" alt="Ver proyecto en Patrones Lab">
  </a>
  <a href="https://github.com/malcolmdpc/patrones-lab/tree/main/2026-06_world_cup_prediction">
    <img src="https://img.shields.io/badge/GitHub-Repositorio-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repositorio GitHub">
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Estado-%E2%9C%85%20publicado-CFF7D3?style=flat-square" alt="Estado: publicado">
  <img src="https://img.shields.io/badge/Datos-2026-E9D5FF?style=flat-square" alt="Datos: 2026">
</p>

<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/simulacion-montecarlo-mundial-2026.html">
    <img width="36%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p15-montecarlo-mundial-2026-cover.webp" alt="Simulación de Montecarlo · Predicciones para el Mundial 2026">
  </a>
</p>

---

## Objetivo

El objetivo es transformar la fase de eliminación directa del Mundial 2026 en una lectura probabilística.

En lugar de representar una única trayectoria posible, el modelo simula **1.000.000 de torneos** y calcula con qué frecuencia cada selección alcanza las distintas instancias del torneo.

La salida principal permite comparar:

- probabilidad de pasar de ronda;
- probabilidad de llegar a la final;
- probabilidad de salir campeón;
- posibles cruces entre selecciones;
- finales más probables;
- concentración de la probabilidad de título.

---

## Enfoque

El modelo combina dos elementos principales:

### Ratings Elo

Cada selección cuenta con un rating Elo que representa su fortaleza relativa.

Para cada partido, la diferencia de Elo entre ambos equipos se transforma en una probabilidad de victoria:

```text
P(A) = 1 / (1 + 10 ^ (-(Elo_A - Elo_B) / 400))
```

Una mayor diferencia de rating aumenta la probabilidad de avanzar, manteniendo siempre la posibilidad de un resultado contrario.

### Llaves de eliminación directa

Las llaves de eliminación directa definen el recorrido del torneo y determinan cómo se conectan los partidos entre rondas.

Cada simulación recorre esa estructura, resuelve los partidos pendientes y registra qué selecciones continúan avanzando.

Cuando ya hay resultados confirmados, se incorporan al modelo y las probabilidades se recalculan sobre los partidos que faltan.

---

## Simulación Montecarlo

La simulación repite el torneo **1.000.000 de veces**.

En cada recorrido:

1. se identifican los equipos de cada cruce;
2. se calcula la probabilidad de victoria según Elo;
3. se determina qué selección avanza;
4. el ganador pasa al siguiente partido de la llave correspondiente;
5. se registra la instancia alcanzada por cada equipo.

Al terminar todas las simulaciones, las frecuencias observadas se convierten en probabilidades estimadas.

Este enfoque permite analizar el torneo como un conjunto de escenarios posibles, en lugar de mirar una única secuencia de resultados.

---

## Resultados del modelo

El resultado principal es una tabla de probabilidades por selección y ronda.

A partir de esa base se pueden responder preguntas como:

- ¿qué selecciones concentran una mayor probabilidad de salir campeonas?;
- ¿qué equipos tienen más posibilidades de llegar a la final?;
- ¿qué finales aparecen con mayor frecuencia?;
- ¿qué posibles rivales puede encontrar una selección en las rondas siguientes?;
- ¿cómo cambia la probabilidad de título a medida que avanza el torneo?;
- ¿qué relación existe entre el rating Elo y la probabilidad de salir campeón?

El proyecto también permite actualizar estas probabilidades a medida que se cargan nuevos resultados.

---

## Visualizaciones

La capa visual del proyecto fue construida para mostrar tanto el resultado general como distintos escenarios del torneo.

Entre las visualizaciones desarrolladas se encuentran:

- ranking de probabilidad de título;
- probabilidades por ronda;
- matriz de finales posibles;
- finales con mayor probabilidad;
- posibles rivales por selección;
- caminos más frecuentes dentro del cuadro;
- supervivencia por ronda;
- concentración acumulada de la probabilidad de título;
- riesgo de sorpresa;
- relación entre rating Elo y probabilidad de título;
- comparaciones directas entre selecciones.

Las piezas siguen la estética visual de Patrones Lab, con fondo oscuro, marco claro y una paleta basada en azul, dorado y amarillo.

---

## Flujo de trabajo

El proyecto se organiza en tres bloques:

### 1. Preparación

Carga y organización de:

- ratings Elo;
- equipos participantes;
- armado de las llaves;
- resultados ya definidos.

### 2. Simulación

Cálculo de probabilidades por partido y ejecución del modelo Montecarlo sobre las llaves del torneo.

### 3. Visualización

Transformación de los resultados de la simulación en tablas, rankings y gráficos para analizar los distintos escenarios del torneo.

---

## Fuente de datos

Los ratings de las selecciones provienen de:

**World Football Elo Ratings**  
https://www.eloratings.net/

Las llaves del torneo se utilizan como segundo insumo para construir los cruces y actualizar los resultados de la fase de eliminación directa.

---

## Tecnologías

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge" alt="Matplotlib">
  <img src="https://img.shields.io/badge/Montecarlo-334155?style=for-the-badge" alt="Simulación Montecarlo">
  <img src="https://img.shields.io/badge/Elo-8D7130?style=for-the-badge" alt="Ratings Elo">
</p>

---

## Enlaces

- [Ver proyecto en Patrones Lab](https://malcolmdpc.github.io/proyectos/simulacion-montecarlo-mundial-2026.html)
- [Repositorio del proyecto](https://github.com/malcolmdpc/patrones-lab/tree/main/2026-06_world_cup_prediction)
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
