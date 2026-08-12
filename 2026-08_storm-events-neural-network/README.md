[<img width="2508" height="627" alt="PatronesLab Website" src="https://github.com/user-attachments/assets/f26af2c2-5cf7-4480-8c3d-1e162c86673a" />](https://malcolmdpc.github.io)

# Red Neuronal · Daños Económicos en Eventos Meteorológicos

Proyecto desarrollado dentro de **Patrones Lab** para analizar si las características de un evento meteorológico permiten identificar aquellos casos que terminan registrando daños económicos.

La pregunta principal es:

> **¿Podemos anticipar qué eventos tienen mayor probabilidad de registrar daños monetarios?**

Para responderla comparé una **regresión logística** como modelo de referencia con una **red neuronal**, utilizando en ambos casos la misma información de entrada.

---

## Datos

La información proviene de **NOAA Storm Events**, publicada por el *National Centers for Environmental Information (NCEI)* de Estados Unidos.

Fuente oficial:  [NOAA / NCEI · Storm Events](https://www.ncei.noaa.gov/pub/data/swdi/stormevents/csvfiles/)

El proyecto utiliza registros de **2010 a 2025**.

En total se integraron más de **1 millón de eventos meteorológicos**, correspondientes a 16 años de información.

NOAA registra, entre otras variables, el tipo de evento, ubicación, magnitud, fecha, oficina meteorológica responsable y daños económicos asociados a propiedades y cultivos.

---

## Definición del objetivo

Los campos de daños aparecen en distintos formatos, por lo que primero los convertí a valores monetarios comparables.

Luego sumé los daños de propiedades y cultivos y construí una variable binaria:

- **1**: existe un importe de daños registrado mayor que cero;
- **0**: no existe un importe positivo registrado.

Por lo tanto, el modelo no intenta estimar cuánto dinero se pierde, sino **clasificar si un evento registra o no daños económicos positivos**.

---

## Preparación de los datos

Antes del modelado:

- integré los archivos anuales de 2010 a 2025;
- revisé duplicados, valores faltantes y formatos;
- transformé los campos monetarios de daños;
- generé variables temporales;
- normalicé variables categóricas;
- creé indicadores para determinados valores faltantes;
- excluí variables que podían revelar directamente el resultado.

Finalmente trabajé con **19 variables predictoras**.

Las variables numéricas fueron imputadas y estandarizadas, mientras que las categóricas se transformaron mediante *one-hot encoding*. El resultado fue una matriz de **311 variables de entrada** utilizada por ambos modelos.

---

## Separación temporal

La división de los datos respetó el orden cronológico:

| Muestra | Período | Uso |
|---|---|---|
| Train | 2010–2021 | Entrenamiento |
| Validation | 2022–2023 | Control y selección del modelo |
| Test | 2024–2025 | Comparación final |

La idea fue entrenar con años anteriores y comprobar el comportamiento sobre períodos posteriores.

---

## Modelos

### Regresión logística

La regresión logística se utilizó como modelo de referencia.

Permite establecer un punto de comparación simple y comprobar cuánto puede explicarse mediante relaciones principalmente lineales entre las variables y la probabilidad de registrar daños.

### Red neuronal

La red neuronal utiliza exactamente las mismas 311 entradas transformadas que la regresión logística.

La arquitectura final fue deliberadamente simple:

- una primera capa oculta de **64 neuronas**;
- activación **ReLU**;
- **Dropout del 20 %** para reducir el riesgo de sobreajuste;
- una segunda capa de **32 neuronas** con activación ReLU;
- una salida **sigmoid**, que devuelve una probabilidad entre 0 y 1.

El entrenamiento se realizó con **Adam** como optimizador y entropía cruzada binaria como función de pérdida.

Para evitar entrenar durante más épocas de las necesarias, utilicé:

- **Early Stopping**, controlando el PR AUC sobre validation;
- reducción automática del *learning rate* cuando la pérdida de validation dejaba de mejorar;
- restauración de los pesos correspondientes a la mejor época observada.

La red alcanzó su mejor resultado de validation alrededor de la **época 23**.

La intención no fue construir una arquitectura excesivamente compleja, sino comprobar si una red relativamente pequeña podía capturar relaciones e interacciones que la regresión logística no lograba representar.

---

## Resultados

La comparación final se realizó sobre los datos de **2024–2025**.

| Métrica | Regresión logística | Red neuronal |
|---|---:|---:|
| Accuracy | 0,8634 | **0,8885** |
| ROC AUC | 0,8961 | **0,9324** |
| PR AUC | 0,6691 | **0,8004** |
| Precision · eventos con daño | 0,7580 | **0,7942** |
| Recall · eventos con daño | 0,5023 | **0,6243** |
| F1 · eventos con daño | 0,6042 | **0,6991** |

La mejora más relevante aparece en la detección de eventos con daños.

La regresión logística identificó correctamente **14.818** eventos positivos, mientras que la red neuronal detectó **18.417**.

Eso representa **3.599 eventos adicionales con daños correctamente identificados**.

Los falsos positivos, en cambio, pasaron de **4.732 a 4.772**, una diferencia de solo 40 casos.

El principal avance se observa en el **recall**, que aumenta de aproximadamente **50 % a 62 %**, y en el **PR AUC**, que pasa de **0,669 a 0,800**.

---

## Conclusión

La regresión logística ofrece un benchmark sólido, pero la red neuronal consigue una mejor separación entre eventos con y sin daños registrados.

La mejora no proviene de utilizar más variables, sino de aplicar un modelo con mayor capacidad para aprender relaciones no lineales sobre exactamente la misma información.

El resultado muestra que una red neuronal relativamente sencilla puede aportar una mejora clara frente a un modelo lineal, especialmente en la capacidad de detectar eventos que efectivamente registraron daños económicos.

---

## Limitaciones

- El target representa **daño monetario registrado**, no la existencia absoluta de daño.
- Los criterios de reporte pueden variar entre años, regiones y tipos de evento.
- El modelo clasifica la presencia de daños, pero no estima su importe.
- Los resultados deben interpretarse como capacidad predictiva y no como causalidad.

---

## Herramientas

Python · Pandas · Scikit-learn · Keras · TensorFlow · Matplotlib · Joblib

---

**Patrones Lab**  
*Generando conocimiento a través de los datos.*
