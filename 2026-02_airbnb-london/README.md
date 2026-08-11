[<img width="5400" height="1350" alt="Diseño sin título (2)" src="https://github.com/user-attachments/assets/816d8241-36ae-4241-bbeb-223bfd8fa741" />](https://malcolmdpc.github.io)

# Airbnb en Londres con datos abiertos de Inside Airbnb (2025-SEPT)

> Proyecto desarrollado dentro de **@PatronesLab** — análisis de datos abiertos con foco en entender patrones reales y comunicarlos de forma clara.

## Qué es este proyecto

Este repositorio reúne un caso de estudio **reproducible** a partir de datos abiertos de **Inside Airbnb** para analizar la oferta de alojamientos en **Londres** a partir del snapshot de **listings** del **14 de septiembre de 2025**.

La intención es doble:
- **Entender** cómo se distribuyen los precios según tipo de alojamiento, barrio, estancia mínima, disponibilidad y contexto espacial.
- **Comunicarlo** con visualizaciones claras.

**Fuente principal:** Inside Airbnb – London listings  
https://insideairbnb.com/get-the-data/

---

## Cómo leer los resultados

Para evitar interpretaciones erróneas, este proyecto toma como unidad de análisis **cada anuncio publicado** (*listing*), no una reserva ni una transacción efectivamente realizada.

- **`price`**: precio publicado por noche del anuncio. No debe interpretarse como ingreso real ni como tarifa final pagada.
- **`room_type`**: tipo de alojamiento publicado en la plataforma (por ejemplo, vivienda completa, habitación privada, habitación de hotel o habitación compartida).
- **Comparación relativa de precios**: cuando se clasifica un anuncio como **barato**, **estable** o **caro**, la comparación se hace **dentro de su propio `room_type`**.
- **`dist_centro_km`**: distancia al centro calculada con referencia operativa en **Charing Cross**, usada como lugar geográfico para comparar centralidad.
- **KNN (*k-nearest neighbours*, vecinos más cercanos)**: en el análisis espacial se construyen variables de entorno a partir de anuncios geográficamente cercanos para aproximar contexto local comparable.

### Limitación clave de estos datos

Este dataset representa una **foto de la oferta publicada** en una fecha determinada.  
Por tanto, el análisis debe leerse como estructura del mercado visible en la plataforma, no como demanda real, ocupación efectiva ni rentabilidad observada.

Además:
- `availability_365` refleja disponibilidad declarada en la plataforma, no noches efectivamente vendidas.
- `last_review` funciona como señal de actividad reciente, pero no garantiza volumen de reservas ni frecuencia exacta de uso.

---

## Decisiones metodológicas

- **Base analítica principal:** todo el análisis parte de `df_london_core`, construido a partir del archivo de listings depurado.
- **Filtros “duros” aplicados de forma conjunta:**  
  - `price > 0`  
  - `last_review > 2023-09-14` (para trabajar con histórico de los últimos dos años)
  - `minimum_nights < 90` (por restricción legal de alquiler en Londres)
  - `availability_365 > 0` (quedando así aquellos que tienen disponibilidad a la fecha de análisis)
- **Sin filtrados selectivos por tipología o barrio:** no se eliminan registros por `room_type` ni por `neighbourhood`.  
  Esto evita sesgos arbitrarios y mantiene el mercado completo dentro de la base analítica filtrada.
- **Limpieza mínima necesaria:** se eliminan columnas no esenciales para el análisis principal, como identificadores o campos textuales que no aportan al objetivo analítico inmediato.
- **Tiempo:** el campo `last_review` se convierte a fecha para permitir filtros, chequeos de recencia y construcción de variables derivadas como `days_since_last_review`.
- **Geografía:** las coordenadas se usan para mapas, distancia al centro y variables de vecindad.  
  El archivo `greater-london.geo.json` se utiliza para enmarcar visualmente el territorio de Greater London.
- **Segmentación relativa de precio:** en el análisis descriptivo, la clasificación de precios se define por percentiles dentro de cada `room_type`.  
  En el notebook de modelado, el clasificador trabaja sobre los extremos relativos del precio dentro de cada tipo de alojamiento y luego traduce probabilidades a zonas interpretables.

---

## Qué contiene el repo

### Notebooks principales

1. **`01_airbnb_london_prep_analisis.ipynb`**  
   Notebook base de **preparación, limpieza y análisis descriptivo inicial**. Incluye:
   - lectura del archivo de listings
   - depuración de columnas y revisión rápida de métricas
   - construcción de `df_london_core`
   - indicadores principales del mercado
   - boxplots e histogramas de precio por tipo de alojamiento
   - comparación de precios por barrio
   - mapa de calor `neighbourhood × room_type`
   - análisis de precio según estancia mínima y disponibilidad anual
   - guardado opcional de salidas en `Parquet` y `CSV` (*comma-separated values*, valores separados por comas)

2. **`02_airbnb_london_analysis.ipynb`**  
   Notebook de **análisis descriptivo avanzado, contexto espacial y mapas**. Incluye:
   - segmentación relativa de precio por `room_type`
   - frecuencia de categorías de precio
   - distancia al centro de Londres
   - precios medianos por barrio y por tipo
   - composición de anuncios caros / estables / baratos por barrio
   - mapas de precio por ubicación y por tramos de distancia
   - variables de entorno con **KNN (*k-nearest neighbours*, vecinos más cercanos)**
   - tablas resumen por barrio y por distancia al centro

3. **`03_airbnb_london_model.ipynb`**  
   Notebook de **modelado de precios relativos**. Incluye:
   - construcción de variables derivadas
   - bandas de estancia mínima y tamaño del host
   - definición del target binario de anuncios relativamente caros
   - partición train / test
   - preprocesado de variables numéricas y categóricas
   - entrenamiento de un modelo base de clasificación
   - evaluación de probabilidades y zonas predichas
   - mapas de acierto / error y scoring sobre todo Londres

### Visualizaciones

Las visualizaciones se han construido principalmente con **Plotly**, priorizando:
- gráficos claros y comparables
- mapas interpretables sin sobrecarga visual
- análisis segmentado por tipo de alojamiento
- reutilización posterior para piezas visuales y comunicación pública

---

## Estructura de datos

El proyecto sigue una estructura simple y explícita:

- **`data/raw/`**  
  Archivos originales descargados o insumos geográficos sin transformar.  
  Ejemplos:
  - `london-airbnb-listings-2025_09_14.csv`
  - `greater-london.geo.json`

- **`data/staging/`**  
  Archivos intermedios corregidos manualmente para dejar el insumo listo para análisis.  
  Ejemplo:
  - `london-airbnb-listings-2025_09_14.xlsx`

- **`data/processed/`**  
  Salidas generadas a partir del notebook de preparación.  
  Ejemplos:
  - `df_london_core.parquet`
  - `df_london_core.csv`

> Nota: los notebooks asumen rutas relativas coherentes con la carpeta del proyecto.

---

## Cómo ejecutarlo

### Requisitos
- Python 3.12 (recomendado)
- Jupyter Notebook o JupyterLab

### Instalación rápida
```bash
pip install pandas numpy plotly matplotlib openpyxl pyarrow scikit-learn shapely
```
---

## Créditos y licencia

**Fuente de datos:** Inside Airbnb – London listings (datos abiertos).  
Este proyecto utiliza datos abiertos de oferta publicados por Inside Airbnb y los transforma en una base analítica reproducible para fines de exploración, visualización y modelado.

**Autoría del análisis:** Malcolm Di Pietro Cagliari (@PatronesLab).  
Los gráficos, el código y las conclusiones son elaboración propia a partir de datos abiertos.

**Licencia del repositorio:** el código y contenidos de este repositorio se publican bajo la licencia indicada en el archivo `LICENSE` del proyecto.
