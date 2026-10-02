# Taxi Trips Chicago con datos abiertos (ENE 2024 - MAR 2026)

> Proyecto desarrollado dentro de **@PatronesLab** — análisis de datos abiertos con foco en entender patrones reales y comunicarlos de forma clara.


<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/analisis-viajes-taxi-chicago.html">
    <img src="https://img.shields.io/badge/Web-Taxi%20Trips%20Chicago-FF9F1C?style=for-the-badge" alt="Web · Taxi Trips Chicago">
  </a>
  <a href="https://github.com/malcolmdpc/patrones-lab/tree/main/2026-03_taxi-trip-chicago">
    <img src="https://img.shields.io/badge/GitHub-Repositorio-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repositorio GitHub">
  </a>
  <a href="https://data.cityofchicago.org/Transportation/Taxi-Trips-2024-/ajtu-isnz">
    <img src="https://img.shields.io/badge/Datos-City%20of%20Chicago-334155?style=for-the-badge" alt="Datos · City of Chicago">
  </a>
</p>

---

## Proyectos publicados

A partir de esta misma línea de trabajo sobre viajes reportados de taxi en Chicago se desarrollaron tres proyectos publicados en **Patrones Lab**.

<table>
  <tr>
    <td width="33.33%" valign="top">
      <a href="https://malcolmdpc.github.io/proyectos/analisis-viajes-taxi-chicago.html">
        <img width="100%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p03-taxi-chicago-cover.webp" alt="Análisis de Viajes en Taxi en Chicago">
      </a>
      <br><br>
      <strong>03 · Análisis de Viajes en Taxi en Chicago</strong><br><br>
      <img src="https://img.shields.io/badge/Estado-%E2%9C%85%20publicado-CFF7D3?style=flat-square" alt="Estado: publicado"><br>
      <img src="https://img.shields.io/badge/Datos-2026-E9D5FF?style=flat-square" alt="Datos: 2026"><br><br>
      Análisis de viajes reportados de taxi en Chicago para estudiar duración, demanda, distribución geoespacial y patrones operativos.<br><br>
      <kbd>Python</kbd> <kbd>Data Analysis</kbd> <kbd>Taxi</kbd> <kbd>BI</kbd><br><br>
      <a href="https://malcolmdpc.github.io/proyectos/analisis-viajes-taxi-chicago.html">Ver proyecto</a>
    </td>
    <td width="33.33%" valign="top">
      <a href="https://malcolmdpc.github.io/proyectos/dashboard-looker-taxi-trips-chicago.html">
        <img width="100%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p05-looker-taxi-chicago-cover.webp" alt="Dashboard Looker · Taxi Trips Chicago">
      </a>
      <br><br>
      <strong>05 · Dashboard Looker · Taxi Trips Chicago</strong><br><br>
      <img src="https://img.shields.io/badge/Estado-%E2%9C%85%20publicado-CFF7D3?style=flat-square" alt="Estado: publicado"><br>
      <img src="https://img.shields.io/badge/Datos-2026-E9D5FF?style=flat-square" alt="Datos: 2026"><br><br>
      Dashboard interactivo en Looker Studio para explorar indicadores operativos, patrones horarios y recorridos pickup-dropoff.<br><br>
      <kbd>Looker Studio</kbd> <kbd>Dashboard</kbd> <kbd>Taxi</kbd> <kbd>BI</kbd><br><br>
      <a href="https://malcolmdpc.github.io/proyectos/dashboard-looker-taxi-trips-chicago.html">Ver proyecto</a>
    </td>
    <td width="33.33%" valign="top">
      <a href="https://malcolmdpc.github.io/proyectos/analisis-geoespacial-viajes-taxi.html">
        <img width="100%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p12-taxi-geoespacial-cover.webp" alt="Análisis Geoespacial de los Viajes en Taxi">
      </a>
      <br><br>
      <strong>12 · Análisis Geoespacial de los Viajes en Taxi</strong><br><br>
      <img src="https://img.shields.io/badge/Estado-%E2%9C%85%20publicado-CFF7D3?style=flat-square" alt="Estado: publicado"><br>
      <img src="https://img.shields.io/badge/Datos-2026-E9D5FF?style=flat-square" alt="Datos: 2026"><br><br>
      Análisis geoespacial orientado a detectar zonas de mayor actividad, recorridos urbanos y concentración territorial de la demanda.<br><br>
      <kbd>Python</kbd> <kbd>GeoPandas</kbd> <kbd>Geoespacial</kbd> <kbd>Taxi</kbd><br><br>
      <a href="https://malcolmdpc.github.io/proyectos/analisis-geoespacial-viajes-taxi.html">Ver proyecto</a>
    </td>
  </tr>
</table>

---

## Características del Proyecto

Aquí se trabaja con aproximadamente **12,5 millones de registros** a partir de datos abiertos de **City of Chicago** para analizar viajes reportados de taxi en **Chicago** entre **enero de 2024 y marzo de 2026**. Se combina análisis temporal, económico, operativo y geoespacial de la red urbana de viajes.

**Fuente principal:** City of Chicago Data Portal – Taxi Trips (2024-) --> https://data.cityofchicago.org/Transportation/Taxi-Trips-2024-/ajtu-isnz

---

## Diccionario de datos

Para evitar interpretaciones erróneas, este proyecto toma como unidad de análisis **cada viaje reportado** en la base pública, no la totalidad real de los viajes de taxi ocurridos en Chicago.

- **`trip_seconds`**: duración del viaje en segundos.
- **`trip_miles`**: distancia del viaje en millas.
- **`fare`**: tarifa base del viaje.
- **`trip_total`**: costo total incluyendo tarifa base, propina, peajes y extras.
- **`tips`**: propina.
- **`payment_type`**: medio de pago.
- **`company`**: compañía de taxi asociada al viaje.
- **`pickup_community_area`** y **`dropoff_community_area`**: zonas de origen y destino del viaje a nivel de *community area*.
- **`speed_mph`**: velocidad estimada en millas por hora, calculada a partir de distancia y duración.
- **`time_band`**: franja horaria derivada para agrupar los viajes en mañana, tarde, tarde/noche y noche.

En los análisis descriptivos se priorizan **medianas y percentiles**, porque duración, distancia, tarifa, costo total, velocidad y ratios derivados presentan asimetría, dispersión y cola larga.

### Limitación de datos

Este dataset representa viajes **reportados** a City of Chicago.  
Por tanto, el análisis debe leerse como una aproximación a la movilidad registrada en la base pública, no como una medición completa.

Además:
- Algunas coordenadas se encuentran agregadas o protegidas por criterios de privacidad.
- Las zonas geográficas se analizan a nivel de *community area*, no a nivel de dirección exacta.
- Los viajes con valores extremos o inconsistentes se filtran para construir una base analítica estable.
- Las métricas de velocidad son derivadas y dependen de la consistencia entre duración y distancia.

---

## Decisiones metodológicas

- **Base analítica principal:** todo el análisis parte de una base procesada a partir del dataset público de Taxi Trips.
- **Tipado de variables:** se convierten fechas, variables numéricas, variables categóricas y campos geográficos para permitir análisis temporal, monetario y espacial.
- **Variables derivadas principales:** se construyen `trip_minutes`, `trip_hours`, `speed_mph`, `fare_per_mile`, `trip_total_per_mile`, `fare_per_minute`, `trip_total_per_minute`, `tip_pct`, `is_weekend` y `time_band`.
- **Filtros “duros” aplicados de forma conjunta:**  
  - `trip_seconds` entre **90** y **5400**
  - `trip_miles` entre **0.30** y **50**
  - `speed_mph` entre **1** y **70**
  - `fare` entre **USD 3.25** y **USD 150**
  - `fare_per_mile` entre **USD 2** y **USD 50**
  - `fare_per_minute` entre **USD 0.3** y **USD 5**
  - `tolls` hasta **USD 5**
  - `tips` hasta **USD 30**
  - `extras` hasta **USD 50**
  - `tip_pct` hasta **100**
  - `trip_total` hasta **USD 190**
  - `trip_total_per_mile` hasta **USD 60**
  - `trip_total_per_minute` hasta **USD 6**
- **Sin filtrados selectivos por compañía o zona:** no se eliminan registros por `company`, `pickup_community_area` ni `dropoff_community_area`.  
  Esto evita sesgos arbitrarios y mantiene la estructura completa de la red reportada dentro de la base analítica filtrada.
- **Tiempo:** los viajes se analizan por mes, día de la semana, hora y franja horaria.
- **Costo:** se comparan `fare`, `trip_total`, ratios por milla, ratios por minuto y propina.
- **Distancia y duración:** se estudia la distribución de `trip_miles` y `trip_seconds`, junto con sus relaciones bivariadas.
- **Velocidad:** se usa `speed_mph` como métrica derivada para aproximar fluidez o fricción urbana.
- **Geografía:** las zonas de pickup y dropoff se usan para mapas de concentración, balances zonales, perfiles por área y flujos origen-destino.
- **Flujos OD (origen-destino):** se agrupan viajes por pares de zona de origen y zona de destino para identificar corredores principales.

---

## Contenido

### Notebooks principales

1. **`01_taxi_trip_chicago_analysis.ipynb`**  
   Notebook base de **preparación, limpieza, tipado y construcción de variables derivadas**. Incluye:
   - normalización de nombres de columnas
   - conversión de fechas y variables numéricas
   - revisión inicial de nulos y distribuciones
   - construcción de variables derivadas
   - creación de indicadores temporales
   - aplicación de filtros duros
   - generación de una base analítica para los notebooks posteriores

2. **`02_taxi_trip_chicago_eda.ipynb`**  
   Notebook de **EDA (análisis exploratorio de datos)** y visualización descriptiva. Incluye:
   - KPIs (indicadores clave de desempeño) principales del dataset
   - KPIs operativos y de monetización
   - viajes reportados por mes
   - distribución diaria por día de la semana
   - promedio diario de viajes por hora
   - distribuciones de duración, distancia, tarifa y costo total
   - heatmaps por hora, día de semana y compañía
   - análisis bivariado entre duración, distancia y tarifa
   - análisis de velocidad media y mediana por hora y día

3. **`03_taxi_trip_chicago_maps.ipynb`**  
   Notebook de **análisis geoespacial y flujos urbanos**. Incluye:
   - concentración de pickups
   - concentración de dropoffs
   - balance absoluto y relativo entre pickups y dropoffs
   - dominancia horaria por zona
   - tarifa mediana según origen
   - ingreso total por milla según origen
   - velocidad mediana según origen
   - medio de pago dominante por zona
   - principales rutas OD (origen-destino)
   - vector medio de salida por zona
   - flujos principales por franja horaria
   - comparación de flujos entre días hábiles y fin de semana
   - recorridos principales dentro del segmento de viajes largos

### Visualizaciones

Las visualizaciones se organizan en dos carpetas principales:

- **`visuals/eda/`**  
  Gráficos descriptivos, distribuciones, KPIs, heatmaps temporales y análisis bivariado.

- **`visuals/maps/`**  
  Mapas de concentración, mapas por zona, balances espaciales y visualizaciones de rutas o flujos.

Las visualizaciones se han construido principalmente con **Matplotlib**, **Plotly**, **GeoPandas**.

---

## Ejecución

### Requisitos
- Python 3.12 (recomendado)
- Jupyter Notebook o JupyterLab

### Instalación rápida
```bash
pip install pandas numpy matplotlib plotly geopandas shapely pyarrow openpyxl contextily
```

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
