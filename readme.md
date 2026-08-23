# 📊 Análisis de Ventas Online e Indicadores Económicos

Proyecto Final — Análisis de Datos & Dashboard

**Autor:** José Antonio Gálvez Beneroso

---

## 📌 Descripción del proyecto

Este proyecto consiste en un **análisis exploratorio de datos (EDA)** completo y un **dashboard operativo** construido a partir de la combinación de dos fuentes de datos distintas:

- Transacciones reales de una tienda online del Reino Unido (2009–2011)
- Indicadores económicos por país y año (Banco Mundial)

El objetivo es analizar el comportamiento de compra de los clientes, identificar patrones de negocio (estacionalidad, productos más rentables, diferencias entre mercados) y comprobar si existe relación entre la situación económica de un país y el comportamiento de compra de sus clientes.

---

## 🎯 Objetivos

- Limpiar y transformar en profundidad dos conjuntos de datos en bruto y unirlos en un dataset final coherente.
- Realizar un análisis descriptivo y estadístico riguroso (correlaciones, prueba de hipótesis).
- Visualizar los hallazgos más relevantes.
- Construir un dashboard interactivo que aporte valor real de negocio.
- Documentar todo el proceso de forma clara y reproducible.

---

## 🗂️ Fuentes de datos

| Fuente | Descripción | Origen |
|---|---|---|
| `online_retail_II.csv` | Transacciones de una tienda online del Reino Unido, dic. 2009 – dic. 2011 | [Kaggle / UCI](https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci) |
| `world_bank_data_2025.csv` | Indicadores económicos por país y año (PIB, inflación, desempleo, etc.) | [Kaggle / World Bank](https://www.kaggle.com/datasets/tanishksharma9905/global-economic-indicators-20102025) |

Ambos archivos en bruto se encuentran en `data/raw/`, sin modificar.

El dataset final, resultado de la limpieza y unión de ambas fuentes, se encuentra en `data/processed/retail_final.csv`.

**Dimensiones del dataset final:** ~1.003.000 filas × 27 columnas.

---

## 🛠️ Herramientas utilizadas

- **Python** (Pandas, NumPy, Matplotlib, Seaborn, SciPy) — limpieza, transformación y análisis exploratorio
- **Visual Studio Code** + Jupyter Notebooks — entorno de desarrollo
- **Power BI Desktop** — dashboard interactivo
- **Git / GitHub** — control de versiones y publicación del proyecto

---

## 📁 Estructura del repositorio

```
proyecto-final-data-analytics/
│
├── data/
│   ├── raw/                     # Datasets originales, sin modificar
│   │   ├── online_retail_II.csv
│   │   └── world_bank_data_2025.csv
│   └── processed/               # Dataset final limpio y unido
│       └── retail_final.csv
│
├── notebooks/                   # Notebooks de Python con todo el análisis
│   ├── 01_carga_exploracion.ipynb    # Carga, limpieza, transformación y unión
│   └── 02_analisis_descriptivo.ipynb # Análisis descriptivo, estadístico y visualización
│
├── dashboard/                   # Dashboard de Power BI
│   └── dashboard_retail.pbix
│
│
└── README.md
```

---

## 🔄 Proceso seguido

### 1. Carga y limpieza de datos
- Eliminación de **34.335 filas duplicadas**.
- Separación de **19.104 facturas canceladas** en un dataset independiente.
- Eliminación de cantidades y precios inválidos (≤ 0).
- Tratamiento de valores nulos (`Description`, `Customer ID`).
- Corrección de tipos de datos (fechas, identificadores).
- Corrección de **6 nombres de país inconsistentes** entre ambas fuentes para maximizar coincidencias.
- Eliminación de **4.699 registros administrativos** (ajustes contables, gastos de envío, comisiones) que no representaban ventas reales de producto.
- Eliminación de la columna `Public Debt (% of GDP)` por tener un 75% de valores nulos.

### 2. Unión de las fuentes
- Combinación (`merge`) de ambos datasets por `Country` + `Year`.
- El 4,4% de las filas (diciembre de 2009 y 3 registros que no son países reales) quedaron sin datos económicos, ya que el Banco Mundial solo cubre desde 2010. Se decidió **no imputar** estos valores para preservar la integridad de los datos.

### 3. Análisis descriptivo y estadístico
- Estadísticas generales, distribución de variables y detección de outliers.
- Análisis por país, producto y tiempo.
- Matriz de correlación entre variables de compra e indicadores económicos.
- Prueba de hipótesis (t de Student) comparando el gasto medio en Reino Unido frente al resto del mundo.

### 4. Visualización y dashboard
- Gráficos exploratorios en Python (distribución, evolución temporal, comparativas).
- Dashboard interactivo en Power BI con 3 páginas y filtros dinámicos.

---

## 📈 Principales hallazgos

- **Concentración geográfica:** el Reino Unido representa el **85,53%** de los ingresos totales del negocio.
- **Paradoja del ticket medio:** a pesar de generar menos ingresos totales, los clientes internacionales gastan de media **casi el doble** por línea de compra que los del Reino Unido (35,64 frente a 18,19). La diferencia es estadísticamente significativa (prueba t de Student, p ≈ 0,0).
- **Sin relación con la macroeconomía:** no existe correlación relevante entre los indicadores económicos del país del cliente (PIB per cápita, inflación, desempleo) y su comportamiento de compra.
- **Estacionalidad marcada:** las ventas alcanzan su punto máximo en **noviembre**, coincidiendo con la campaña previa a Navidad, con tendencia de crecimiento interanual.
- **Patrón semanal:** los **sábados** presentan ventas prácticamente nulas, mientras que **jueves** es el día de mayor facturación.
- **El ranking de productos depende de la métrica:** *World War 2 Gliders Asstd Designs* es el producto más vendido en unidades, pero *Regency Cakestand 3 Tier* es el que más ingresos genera — dos historias distintas según cómo se mida el éxito de un producto.

---

## 📊 Dashboard

El dashboard (`dashboard/dashboard_retail.pbix`) está organizado en 3 páginas:

1. **Visión General** — KPIs generales, evolución mensual de ingresos, top países y top productos.
2. **Análisis Geográfico** — comparativa Reino Unido vs. resto del mundo, ticket medio, relación entre PIB per cápita e ingresos.
3. **Productos y Estacionalidad** — mapa de calor de estacionalidad, ranking de productos por unidades e ingresos, ventas por día de la semana.

Incluye filtros interactivos por **Año**, **Mes** y **País**.

---

## ✍️ Autor

**José Antonio Gálvez Beneroso**

Proyecto realizado como trabajo final del curso de Análisis de Datos.
