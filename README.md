# Predicción de Precios de Vivienda en Bogotá | Machine Learning

Modelo de regresión para estimar el precio de apartamentos en Bogotá a partir de características físicas, socioeconómicas y de ubicación. El proyecto implementa un pipeline completo de Machine Learning, desde el preprocesamiento de datos hasta el despliegue de una aplicación interactiva con Streamlit.

---

## Demo

**Aplicación interactiva (Streamlit):**

🔗 https://fw2z7ovawqtfw6gwnytndv.streamlit.app

---

## Descripción del problema

El mercado inmobiliario en Colombia presenta una característica única a nivel mundial: el **estrato socioeconómico** (escala 1–6), que influye en el acceso a servicios públicos, infraestructura, seguridad y valorización del sector.

Este proyecto incorpora el estrato como variable predictora para analizar su impacto sobre el precio de la vivienda en Bogotá mediante modelos de regresión.

**Pregunta de investigación**

> ¿Qué variables determinan el precio de un apartamento en Bogotá y con qué precisión puede estimarse mediante Machine Learning?

---

## Dataset

| Característica | Detalle |
|----------------|---------|
| Fuente | Mercado inmobiliario de Bogotá, Colombia |
| Observaciones | 585 apartamentos |
| Variables originales | 21 |
| Variables finales | 16 |
| Variable objetivo | Precio de venta (COP) |

**Variables principales**

- Área
- Estrato
- Habitaciones
- Baños
- Garajes
- Administración
- Antigüedad
- Barrio

---

## Pipeline del proyecto

```text
Carga de datos
      ↓
Limpieza y preprocesamiento
      ↓
Imputación de valores faltantes
      ↓
Detección y eliminación de outliers
      ↓
Análisis Exploratorio de Datos (EDA)
      ↓
Selección de variables (Árbol de Clasificación)
      ↓
Ingeniería de características
      ↓
Transformación logarítmica del precio (log1p)
      ↓
Codificación de variables categóricas
      ↓
Estandarización
      ↓
División entrenamiento / prueba (75/25)
      ↓
Validación Cruzada (K-Fold, 10 splits)
      ↓
Entrenamiento y comparación de modelos
      ↓
Análisis de residuos
      ↓
Interpretación de coeficientes

```

---

## Modelos evaluados

- DummyRegressor (Baseline)
- Regresión Lineal
- Regresión Lineal Estandarizada
- HuberRegressor sin estandarizar
- HuberRegressor Estandarizado (modelo final)

---

## Resultados

| Modelo | MAE (M COP) | RMSE (M COP) |
|---------|------------:|-------------:|
| Baseline (Mediana) | 105.2 | 140.5 |
| Regresión Lineal | 33.0 | 58.1 |
| HuberRegressor sin estandarizar | Diverge | Diverge |
| Regresión Lineal estandarizada | 33.0 | 58.1 |
| **HuberRegressor estandarizado** | **34.2** | **62.7** |

El modelo final reduce el error de predicción en **67.5%** respecto al baseline.

Con un precio mediano de **$218 millones COP**, el error promedio de **$34.2 millones COP** representa aproximadamente una precisión del **84%**.

---

## Variables más influyentes

| Variable | Coeficiente | Interpretación |
|-----------|------------:|---------------|
| Área | +0.1688 | Mayor área incrementa el precio esperado |
| Estrato | +0.1600 | Segundo predictor más importante del modelo |
| Garajes | +0.0783 | Asociado a viviendas de mayor categoría |
| Administración | +0.0702 | Refleja tamaño y amenidades del conjunto |
| Antigüedad | -0.0230 | Reduce el precio esperado |
| Barrio (Ciudad Usme) | -0.0533 | Zona con menor valorización relativa |

El **área** y el **estrato socioeconómico** constituyen las variables con mayor capacidad predictiva del modelo.

---

## Decisiones metodológicas

### Transformación logarítmica del objetivo

El precio presenta una distribución altamente asimétrica. Se aplicó la transformación `log1p()` durante el entrenamiento y posteriormente `expm1()` para recuperar la escala original de las predicciones.

### Selección de variables

Se utilizó un Árbol de Decisión con profundidad máxima de 4 niveles para identificar las variables numéricas con mayor capacidad predictiva antes del modelado.

### Modelo final

Aunque la Regresión Lineal obtuvo un desempeño ligeramente superior en MAE, el **HuberRegressor** fue seleccionado como modelo final por su mayor robustez frente a valores atípicos, frecuentes en el mercado inmobiliario.

### Estandarización

El uso de `StandardScaler` resultó indispensable para garantizar la convergencia del algoritmo HuberRegressor. Sin estandarización, el modelo presentó errores extremadamente altos debido a problemas numéricos durante la optimización.

---

## Tecnologías utilizadas

- Python
- pandas
- NumPy
- scikit-learn
- Matplotlib
- Seaborn
- Streamlit
- Jupyter Notebook

---

## Estructura del proyecto

```text
prediccion-precios-vivienda-bogota-ml/
│
├── data/
├── notebooks/
├── app.py
├── requirements.txt
└── README.md
```

---



---

## Limitaciones y trabajo futuro

- Incorporar más propiedades de estrato 5 y 6 para mejorar el desempeño del modelo en el segmento premium.
- Incluir variables espaciales como distancia a estaciones de TransMilenio, parques e instituciones educativas.
  

---

## Habilidades demostradas

- Limpieza y preprocesamiento de datos.
- Imputación de valores faltantes.
- Detección y tratamiento de outliers.
- Análisis Exploratorio de Datos (EDA).
- Ingeniería de características.
- Selección de variables mediante Árbol de Clasificación.
- Codificación de variables categóricas.
- Transformación logarítmica del target.
- Estandarización de variables.
- Validación Cruzada (K-Fold).
- Modelos de regresión robusta.
- Evaluación mediante MAE, RMSE.
- Análisis de residuos.
- Interpretación de coeficientes.
- Desarrollo y despliegue de aplicaciones con Streamlit.

---

## Autor

**Franklin Manuel Manjarres**

Matemático | Data Science | Machine Learning

- **GitHub:** https://github.com/franklinmanjarres
- **LinkedIn:** https://www.linkedin.com/in/franklinmanjarres
- **Demo (Streamlit):** https://fw2z7ovawqtfw6gwnytndv.streamlit.app
