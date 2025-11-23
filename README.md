 # Sprint 11 – OilyGiant: Selección óptima de ubicación para un nuevo pozo petrolero

## Descripción general
Este proyecto tiene como objetivo **determinar la región óptima para la perforación de un nuevo pozo petrolero**, combinando análisis estadístico, modelado predictivo y evaluación económica.  
El propósito principal es **maximizar la rentabilidad y minimizar el riesgo financiero**, de acuerdo con las condiciones del negocio.

---

## Objetivos del proyecto
- Desarrollar un **modelo de regresión lineal** que prediga el volumen de reservas (producción esperada) por pozo.
- Estimar el **beneficio potencial por región**, considerando ingresos y presupuesto de inversión.
- Aplicar un **análisis de riesgo con bootstrapping (1,000 simulaciones)** para evaluar la estabilidad de los resultados.
- Seleccionar la **región con mayor rentabilidad esperada y menor riesgo**.

---

## Enfoque metodológico

1. **Análisis exploratorio de datos (EDA)**
   - Verificación de tipos de datos, valores ausentes y estadísticos descriptivos.
   - Visualización de la distribución de la producción (`product`) por región.
   - Identificación de anomalías (región 1 con dispersión atípica).

2. **Preparación de datos**
   - No se requirió limpieza adicional:
     - Todas las variables son numéricas.
     - No existen valores nulos ni duplicados.
     - Las escalas son compatibles para regresión.
   - Los datos se dividieron en conjuntos de entrenamiento (75%) y validación (25%).

3. **Entrenamiento del modelo**
   - Se utilizó `LinearRegression()` de Scikit-Learn.
   - Se definió una función `train_region()` para evitar duplicación de código.
   - Se evaluó el modelo con la métrica **RMSE**.

4. **Evaluación económica**
   - Selección de los 200 mejores pozos basada en las predicciones.
   - Cálculo de beneficios esperados basado en la producción real de esos pozos.
   - Simulación de ingresos considerando:
     - `INCOME_PER_UNIT = 4,500 USD`
     - `BUDGET = 100,000,000 USD`

5. **Análisis de riesgo (bootstrapping)**
   - Se aplicó remuestreo con reemplazo (`bootstrap_profit()`).
   - Se estimaron los intervalos de confianza al 95% (`ci_low`, `ci_high`) y el riesgo de pérdida (`risk_loss`).

---

## Estructura del proyecto
sprint11_oilygiant/
│
├── data/ # Archivos CSV con los datos de las tres regiones
│ ├── geo_data_0.csv
│ ├── geo_data_1.csv
│ └── geo_data_2.csv
│
├── notebooks/ # Análisis principal (EDA, modelado y resultados)
│ └── oilygiant_analysis.ipynb
│
├── src/ # Funciones auxiliares y scripts (opcional)
│
├── reports/ # Visualizaciones y conclusiones
│
├── requirements.txt # Librerías necesarias
├── README.md # Este documento
└── .gitignore

---
## Requisitos e instalación

### 1. Crear entorno virtual
```bash
python -m venv .venv
.venv\Scripts\activate
```

### 2. Instalar dependencias
pip install -r requirements.txt

### 3. Ejecutar el notebook
Abre el archivo:
`notebooks/oilygiant_analysis.ipynb`
en VS Code o JupyterLab, y ejecuta todas las celdas en orden para reproducir el análisis completo.

---

## Resultados principales (Iteración 1 – Inicial)
| Región | Beneficio medio (USD) | IC 95 % [ci_low – ci_high] | Riesgo de pérdida |
|:--------|----------------------:|----------------------------:|------------------:|
| Región 0 | ≈ 46.9 M USD | [46.3 M – 47.6 M] | 0 % |
| Región 2 | ≈ 40.9 M USD | [40.3 M – 41.5 M] | 0 % |
| Región 1 | ≈ 25.2 M USD | [25.2 M – 25.3 M] | 0 % |

**Interpretación:**
*   **Región 0** muestra el mayor beneficio esperado y el intervalo de confianza más estrecho → alta estabilidad.
*   **Región 2** también es rentable, aunque con un margen menor.
*   **Región 1** presenta valores inferiores y comportamiento irregular.

## Conclusión final

> Con base en el análisis predictivo, financiero y de riesgo,
> la Región 0 es la candidata óptima para la perforación del nuevo pozo petrolero.

> Su combinación de alta rentabilidad media, bajo riesgo y consistencia estadística la convierten en la opción más segura y rentable para invertir el presupuesto disponible.

---

## Resultados principales (Iteración 2 – escenario real)
| Región | Beneficio medio (USD) | IC 95 % [ci_low – ci_high] | Riesgo de pérdida |
|:--------|----------------------:|----------------------------:|------------------:|
| Región 1 | ≈ 4.52 M USD | [0.62M , 8.45M] | 1.5 % |
| Región 0 | ≈ 3.99 M USD | [−1.1M , 8.97M] | 6 % |
| Región 2 | ≈ 3.75 M USD | [-1.44M , 8.88M] | 8 % |

**Interpretación:**
*   **Región 1** resulta ser la mejor alternativa para perforar un nuevo pozo.
   * Presenta el mayor beneficio medio (≈4.52 M USD).
   Su intervalo inferior es positivo, aunque pequeño (≈0.6 M), lo que indica que incluso en los escenarios más desfavorables la región aún genera ganancias.
   Tiene el riesgo más bajo de pérdidas (1.5 %).

*   **Región 0** muestra un beneficio competitivo, pero con una mayor incertidumbre:
   * Su intervalo incluye pérdidas de hasta −1.1 M USD.
   * El riesgo es aproximadamente cuatro veces mayor que en la Región 1.

*   **Región 2** presenta la menor rentabilidad y la mayor probabilidad de pérdida, siendo la opción menos favorable.

## Conclusión final
**Decisión final recomendada:**
Perforar en Región 1, ya que ofrece la mejor combinación de rentabilidad, estabilidad y mínimo riesgo financiero.

---

## Librerías principales

* `pandas`
* `numpy`
* `matplotlib`
* `seaborn`
* `plotly`
* `scikit-learn`
* `jupyter`
* `ipykernel`

---

## **Autor**
**Diana Marlene Reyes Fraire**
*Data Science Bootcamp — TripleTen*
**Proyecto Sprint 11: OilyGiant — Selección de la mejor ubicación para un pozo petrolero**



