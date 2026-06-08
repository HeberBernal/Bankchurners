# 📊 Modelo Analítico de Retención y Comportamiento Transaccional (Bank Churn)

Este proyecto despliega un ciclo completo de Ciencia de Datos aplicado al sector financiero y de gestión de carteras. Utilizando un conjunto de **10,127 registros de clientes bancarios** (`BankChurners.xlsx`), el análisis abarca desde la ingesta de datos y el tratamiento avanzado de registros faltantes, hasta el modelado predictivo de transacciones y la analítica prescriptiva de fuga de clientes (*churn rate*).

---

## 🚀 Estructura del Proyecto

El análisis se encuentra estructurado en 5 tópicos secuenciales alineados con los estándares de la industria tecnológica y de negocio:

1. **Carga, Limpieza y Preparación del Dataset**
2. **Análisis Descriptivo de las Variables**
3. **Análisis Inferencial (Correlaciones Críticas y Sesgo)**
4. **Análisis Predictivo (Modelado de Regresión)**
5. **Analítica Prescriptiva (Estrategia de Retención Rentable)**

---

## 🛠️ Tecnologías y Librerías Utilizadas

* **Python 3** como lenguaje principal.
* **Pandas & NumPy:** Ingesta de datos, pipelines de transformación ETL y manipulación matricial.
* **Scikit-Learn:** División de datos (*Train/Test Split*) y entrenamiento del modelo de Regresión Lineal Múltiple.
* **Seaborn & Matplotlib:** Generación de visualizaciones avanzadas (Mapas de calor estructurados y diagramas de caja distributivos).

---

## 🎯 Hallazgos Clave y Resultados Técnicos

### 1. Tratamiento de Datos Faltantes Estructurales
Al ejecutar el diagnóstico de celdas vacías (`df.isnull().sum()`), el dataset no arrojó nulos tradicionales. Sin embargo, se detectó ruido crítico bajo la etiqueta de **'Unknown'** en variables clave:
* **Education_Level:** 1,519 registros (14.99% de la muestra)
* **Income_Category:** 1,112 registros (10.98% de la muestra)
* **Marital_Status:** 749 registros (7.40% de la muestra)

**Decisión de Arquitectura de Datos:** Dado que la afectación acumulada superaba ampliamente el umbral del 5% (rozando el 15% en educación), **se determinó mantener estos registros** en el análisis descriptivo para garantizar la representatividad estadística de la muestra y evitar sesgos de selección.

### 2. Análisis Inferencial y Matriz de Correlación
A través de un mapa de calor con máscara triangular (para reducir el ruido visual), se aislaron correlaciones críticas de comportamiento:
* **Monto vs. Cantidad de Transacciones ($r = 0.81$):** Valida de forma lineal que el motor principal del gasto es la frecuencia transaccional.
* **Índice de Utilización vs. Saldo Revolvente ($r = 0.62$):** Confirma un perfil de cliente que utiliza el crédito como financiamiento a largo plazo y no solo como medio de pago diario.

### 3. Evaluación de Disparidad (Sesgo de Género)
El análisis numérico y distributivo a través de *Boxplots* reveló una brecha inicial en las líneas de crédito promedio:
* **Hombres:** \$12,685.67 (Mediana superior y mayor dispersión).
* **Mujeres:** \$5,023.85 (Distribución acotada y menor variabilidad).

**Conclusión del Analista:** Aunque existe una disparidad, no es posible afirmar un sesgo discriminatorio. Al cruzar los datos con ingresos, se demuestra que los límites se ajustan a los niveles de ingresos reportados por el segmento masculino y a sus necesidades transaccionales.

---

## 🤖 Desempeño del Modelo Predictivo

Tras el entrenamiento de la Regresión Lineal Múltiple para predecir el Monto Total de Transacciones (`Total_Trans_Amt`), el modelo arrojó las siguientes métricas de control:

| Métrica | Resultado | Interpretación |
| :--- | :--- | :--- |
| **$R^2$** | **0.6801** | El 68.01% de la variabilidad del gasto es explicada por la actividad del cliente. |
| **$R^2$ Ajustada** | **0.6801** | Ajuste óptimo del modelo considerando el número de variables predictoras utilizadas. |
| **Caso de Prueba** | **\$4,102.39** | Gasto estimado para un cliente con 60 transacciones, 3 productos y \$7,500 de crédito. |

> **Diagnóstico Pro: El alto $R^2$ (0.68)** valida sólidamente que el volumen transaccional, la cantidad de productos y la línea de crédito asignada son potentes predictores del comportamiento de consumo del usuario.

---

## 🤖 Análisis Prescriptivo y Retención de Cartera

Al evaluar el clasificador de abandono (*Naive Bayes*), se identificó que la inactividad acumulada es el principal precursor de fuga en el último año:

| Segmento de Cliente | Churn Rate Esperado | Diagnóstico de Riesgo |
| :--- | :--- | :--- |
| **Clientes Activos** (< 3 meses inactivos) | **11.11%** | Comportamiento transaccional saludable dentro de los parámetros normales. |
| **Clientes Inactivos** ($\geq$ 3 meses inactivos) | **21.91%** | Zona de alerta crítica por abandono de cuenta o desuso del plástico. |
| **Métrica de Impacto** | **1.97 veces** | Un cliente inactivo tiene casi el doble de probabilidad de fuga que uno activo. |

> **Diagnóstico Pro: La inactividad trimestral es el detonante de fuga.** La probabilidad de abandono incrementa exponencialmente al cruzar el umbral de los 3 meses, exigiendo campañas de reactivación inmediatas.

---

---

## 📈 Propuesta de Negocio y Medición de Rentabilidad

Para mitigar el *churn* en el segmento crítico ($\geq$ 3 meses de inactividad), se prescribe una **Estrategia de Domiciliación Automatizada de Servicios**. Esto genera una barrera de salida operativa que incrementa el costo de esfuerzo de cancelación para el usuario.

La rentabilidad (ROI) de la estrategia se indexa bajo 3 KPIs financieros:
1. **Incremental Lift (Prueba A/B):** Monitoreo del diferencial de facturación mensual en un grupo piloto frente a un grupo de control, asegurando el retorno del incentivo en < 4 meses.
2. **Extensión del Lifetime Value (LTV):** Proyección de meses adicionales de permanencia (un promedio de 2.5 años extra por cliente retenido con pagos recurrentes).
3. **Eficiencia frente al CAC:** Contraste del costo de retención de la campaña (aprox. \$200 MXN) contra el costo de adquisición de un cliente nuevo en el sector bancario (\$1,500 - \$3,000 MXN), demostrando que retener es entre 5 y 10 veces más económico.

---

## 🛠️ Cómo Ejecutar el Notebook
1. Clona este repositorio o descarga el archivo `Bankchurners.ipynb`.
2. Sube el archivo a tu entorno de **Google Colab**.
3. Asegúrate de cargar el archivo fuente `BankChurners (1).xlsx` en la ruta correspondiente o modifica la variable `ruta`.
4. Ejecuta las celdas de forma secuencial para visualizar las tablas descriptivas y las gráficas interactivas de Seaborn.

---

### Heber Bernal | Data Analyst & Analytics Specialist
*Conectando ciencia de datos con el valor estratégico de negocio.*
