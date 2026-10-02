# Dashboard en Power BI · Análisis de Gastos

**Informe ejecutivo en Power BI orientado al análisis de gastos con proveedores, evolución mensual, descuentos y ahorro.**

El proyecto transforma información de facturas, líneas de factura, proveedores, artículos, centros, monedas y fechas en un modelo analítico para seguir el gasto, detectar concentraciones y analizar oportunidades de ahorro desde una mirada de **Compras y Cuentas a Pagar**.

<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/dashboard-power-bi-prov-gastos-desc.html">
    <img src="https://img.shields.io/badge/Web-Ver%20proyecto-FF9F1C?style=for-the-badge" alt="Ver proyecto en Patrones Lab">
  </a>
  <a href="https://github.com/malcolmdpc/patrones-lab/tree/main/2026-07_supplier-spend-discounts-powerbi">
    <img src="https://img.shields.io/badge/GitHub-Repositorio-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repositorio GitHub">
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Estado-%E2%9C%85%20publicado-CFF7D3?style=flat-square" alt="Estado: publicado">
</p>

<p align="center">
  <a href="https://malcolmdpc.github.io/proyectos/dashboard-power-bi-prov-gastos-desc.html">
    <img width="36%" src="https://malcolmdpc.github.io/images/patrones/projects/home-covers/p14-proveedores-powerbi-cover.webp" alt="Dashboard en Power BI · Análisis de Gastos y Proveedores">
  </a>
</p>

---

## Objetivo

Construir un dashboard que permita analizar el gasto con proveedores desde una vista ejecutiva y, al mismo tiempo, bajar al detalle cuando sea necesario.

El informe busca responder preguntas como:

- ¿cómo evoluciona el gasto a lo largo del tiempo?;
- ¿qué proveedores concentran mayor volumen de compras?;
- ¿cómo se distribuye el gasto por país, ciudad, categoría y subcategoría?;
- ¿qué parte del gasto está asociada a descuentos?;
- ¿cuánto ahorro generan esos descuentos?;
- ¿cómo se comportan los proveedores según su nivel y condiciones de pago?

La navegación separa la lectura general del gasto del análisis específico de descuentos y proveedores.

---

## Modelo de datos

El modelo integra información de distintas entidades vinculadas al proceso de compras y facturación:

- facturas;
- líneas de factura;
- proveedores;
- artículos;
- centros;
- monedas;
- tipos de cambio;
- fechas;
- calendario.

La estructura relacional permite analizar importes y cantidades desde distintas dimensiones sin perder el nivel de detalle de las operaciones.

Power BI se utiliza tanto para el modelado como para la construcción de medidas DAX, filtros y visualizaciones interactivas.

---

## Indicadores principales

El dashboard reúne indicadores orientados al seguimiento del gasto y al análisis de descuentos:

| Indicador | Lectura |
|---|---|
| **Gasto total** | Importe acumulado dentro de la selección aplicada |
| **Cantidad de facturas** | Volumen de documentos incluidos en el análisis |
| **Gasto con descuento** | Importe asociado a operaciones con descuento |
| **Ahorro** | Valor económico obtenido mediante descuentos |
| **Descuento promedio** | Nivel medio de descuento aplicado |
| **Días disponibles para descuento** | Ventana disponible para aprovechar condiciones de descuento |
| **Plazo promedio de pago** | Tiempo medio asociado a las condiciones de pago |
| **Evolución mensual** | Comportamiento del gasto a lo largo del tiempo |

Estas medidas pueden analizarse en conjunto con las distintas dimensiones del modelo.

---

## Estructura del dashboard

El informe se organiza alrededor de una página inicial y dos vistas analíticas principales.

### Evolución y distribución del gasto

Vista orientada a entender cómo se comporta el gasto y dónde se concentra.

Incluye análisis por:

- período;
- país;
- ciudad;
- proveedor;
- nivel de proveedor;
- categoría;
- subcategoría.

La evolución mensual permite observar cambios en el tiempo mientras que las distribuciones ayudan a identificar proveedores, zonas o categorías con mayor participación.

### Descuentos por proveedor

Vista enfocada en las condiciones comerciales y el ahorro asociado a los descuentos.

Permite analizar:

- gasto con descuento;
- ahorro generado;
- descuento promedio;
- días disponibles para aplicar el descuento;
- condiciones y plazos de pago;
- comportamiento por proveedor.

El objetivo es complementar la lectura del gasto con una mirada sobre las oportunidades de ahorro disponibles dentro de las condiciones comerciales.

---

## Filtros e interacción

El dashboard permite modificar el contexto de análisis mediante filtros por:

- fecha;
- proveedor;
- categoría;
- nivel de proveedor.

Las visualizaciones responden al mismo contexto de filtro, permitiendo pasar de una lectura general a análisis más específicos sin cambiar de modelo.

Esta estructura facilita comparar proveedores, categorías y períodos manteniendo consistentes los indicadores principales.

---

## Flujo de trabajo

El desarrollo se organiza en cuatro bloques:

### 1. Preparación

Revisión de las tablas de origen, tipos de datos, claves y campos necesarios para el análisis.

### 2. Modelado

Construcción de relaciones entre las tablas operativas y las dimensiones utilizadas para segmentar el gasto.

### 3. Medidas

Definición de indicadores mediante **DAX**, concentrando la lógica de cálculo en medidas reutilizables dentro del informe.

### 4. Visualización

Diseño de las páginas del dashboard, filtros, KPIs y gráficos orientados a una lectura ejecutiva y al análisis por proveedor.

---

## Ejes de análisis

El proyecto trabaja principalmente sobre cuatro dimensiones:

### Gasto

Seguimiento del importe total y su evolución temporal.

### Proveedores

Comparación del gasto y las condiciones comerciales entre proveedores y niveles.

### Categorías

Distribución del gasto entre categorías y subcategorías de compra.

### Descuentos y ahorro

Análisis de las operaciones con descuento y del ahorro generado a partir de esas condiciones.

---

## Tecnologías

<p>
  <img src="https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" alt="Power BI">
  <img src="https://img.shields.io/badge/DAX-334155?style=for-the-badge" alt="DAX">
  <img src="https://img.shields.io/badge/Data_Modeling-5B6F8A?style=for-the-badge" alt="Modelado de datos">
  <img src="https://img.shields.io/badge/Business_Intelligence-7B6F8A?style=for-the-badge" alt="Business Intelligence">
  <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub">
</p>

---

## Enlaces

- [Ver proyecto en Patrones Lab](https://malcolmdpc.github.io/proyectos/dashboard-power-bi-prov-gastos-desc.html)
- [Repositorio del proyecto](https://github.com/malcolmdpc/patrones-lab/tree/main/2026-07_supplier-spend-discounts-powerbi)
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
