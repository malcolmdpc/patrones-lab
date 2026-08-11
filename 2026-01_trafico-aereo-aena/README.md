[<img width="5400" height="1350" alt="banner para README de GitHub" src="https://github.com/user-attachments/assets/1560e595-2864-4380-a85e-a461e4f4c807" />](https://malcolmdpc.github.io)


# Tráfico aéreo en Baleares con datos abiertos de AENA (2024–2025)

> Proyecto desarrollado dentro de **@PatronesLab** — análisis de datos abiertos con foco en entender patrones reales y comunicarlos de forma clara.

## Qué es este proyecto

Este repositorio reúne un caso de estudio **reproducible** a partir de estadísticas abiertas de **AENA (Aeropuertos Españoles y Navegación Aérea)** para analizar la actividad aérea en **Illes Balears** (Palma de Mallorca, Ibiza y Menorca) durante **2024–2025**.

La intención es doble:
- **Entender** cómo se distribuye y evoluciona el tráfico (pasajeros, mercancías y correo) en Baleares.
- **Comunicarlo** con visualizaciones claras.

**Fuente oficial:** AENA – Estadísticas de tráfico aeroportuario (datos abiertos)  
https://www.aena.es/es/estadisticas/inicio.html

---

## Cómo leer los resultados

Para evitar interpretaciones erróneas, este proyecto respeta las definiciones oficiales de AENA:

- **Aeropuerto base**: aeropuerto de referencia estadística (Palma, Ibiza, Menorca).
- **Aeropuerto escala**: aeropuerto en el que el pasajero embarca o desembarca.
- **Movimiento**:
  - `LLEGADA`: el vuelo llega al aeropuerto base desde una escala.
  - `SALIDA`: el vuelo sale del aeropuerto base hacia una escala.
- **Pasajeros_totales**: suma de pasajeros y tránsitos.

### Limitación clave de estos datos
Estos datasets no permiten identificar el origen o destino final del pasajero cuando existen escalas.  
Por tanto, el análisis debe entenderse como tráfico observado en los aeropuertos base (Baleares), no como “viajes completos” del pasajero.

---

## Decisiones metodológicas

- **Métrica de pasajeros:** todos los cálculos se realizan con `pasajeros_totales` (no con `pasajeros`).
- **Sin filtrados “selectivos”:** no se eliminan registros por servicio ni por tipo_tráfico (incluyendo “OTRAS CLASES DE TRÁFICO”).  
  Esto evita sesgos y mantiene la integridad estadística.
- **Limpieza mínima necesaria:** se eliminan únicamente filas sin actividad real (valores 0 simultáneamente en las métricas operativas).
- **Tiempo:** el campo `Mes` se normaliza a fecha mensual (`YYYY-MM-01`) para comparaciones temporales consistentes.
- **Geografía:** para mapas se usa un *lookup* de aeropuertos (`lkp_aeropuertos.xlsx`) con país y coordenadas (más códigos IATA/ICAO), basado en fuentes open data y con correcciones puntuales documentadas cuando fue necesario.  
  Las coordenadas se usan solo con fines de visualización.

---

## Qué contiene el repo

### Notebooks principales

1. **`01_pasajeros_por_escala.ipynb`**  
   Análisis de **pasajeros en escala** para Baleares (2024–2025). Incluye:
   - exploración inicial y validaciones
   - comparativas **llegadas vs salidas**
   - rankings (Top 10) por aeropuerto de escala / país
   - series temporales y visualizaciones interactivas (Plotly)
   - análisis de mercancías y correo cuando aplica

2. **`02_pasajeros_por_compania.ipynb`**  
   Análisis de **pasajeros por grupo de compañía** para Baleares (2024–2025). Incluye:
   - limpieza y preparación
   - métricas y rankings por grupo de compañía
   - comparación 2024 vs 2025 con visuales comparables
   - distribución por aeropuerto base
   - evolución mensual
   - estacionalidad: temporada alta (mayo–septiembre) vs baja (octubre–abril) y un indicador de estacionalidad

### Visualizaciones
Las visualizaciones se han construido con Plotly, priorizando:
- gráficos interactivos
- comparativas interanuales consistentes
- exportabilidad a HTML cuando conviene compartir

---

## Datos

Los ficheros de AENA se descargan del portal oficial y se trabajan localmente.  
Por tamaño y buenas prácticas, en el repositorio se incluyen notebooks y *lookups*, pero los ficheros de datos “pesados” pueden mantenerse fuera o en `data/` según tu preferencia.

**Lookup geográfico:** `../data/lkp_aeropuertos.xlsx`  
(Contiene `aeropuerto_escala`, país, coordenadas, IATA e ICAO)

> Nota: los notebooks asumen rutas relativas coherentes con la carpeta del proyecto.

---

## Cómo ejecutarlo

### Requisitos
- Python 3.10+ (recomendado)
- Jupyter Notebook o JupyterLab

### Instalación rápida
```bash
pip install pandas numpy plotly openpyxl
```
---

## Créditos y licencia

**Fuente de datos:** AENA – Estadísticas de tráfico aeroportuario (datos abiertos).  
Este proyecto utiliza ficheros descargados desde el portal oficial de AENA y, por transparencia, en cada notebook se describe cómo se procesan y qué significan sus campos.

**Autoría del análisis:** Malcolm Di Pietro Cagliari (@PatronesLab).  
Los gráficos, el código y las conclusiones son elaboración propia a partir de datos abiertos.

**Licencia del repositorio:** el código y contenidos de este repositorio se publican bajo la licencia indicada en el archivo `LICENSE` del proyecto (si aún no existe, se recomienda añadir una licencia simple como MIT para el código).

