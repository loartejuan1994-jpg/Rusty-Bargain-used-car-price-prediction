# 🚗 Rusty Bargain – Predicción del Valor de Mercado de Autos Usados

## 📋 Descripción del proyecto

Rusty Bargain, un servicio de venta de autos usados, está desarrollando una aplicación que permite a sus clientes averiguar rápidamente el valor de mercado de su vehículo. Este proyecto construye un modelo de Machine Learning capaz de predecir dicho valor a partir de las especificaciones técnicas, el equipamiento y el historial del vehículo.

El proyecto sigue un pipeline completo de ciencia de datos: desde la exploración y limpieza de los datos, hasta el entrenamiento, ajuste de hiperparámetros y evaluación final de distintos modelos de regresión.

## 🎯 Objetivos

A Rusty Bargain le interesan tres criterios clave al evaluar un modelo:

- **Calidad de la predicción** (RMSE)
- **Velocidad de la predicción**
- **Tiempo de entrenamiento**

El objetivo es encontrar el modelo con el mejor equilibrio entre estos tres factores, no simplemente el de menor error.

## 🗂️ Datos

El dataset contiene información histórica de autos usados con las siguientes características: tipo de vehículo, año de matriculación, tipo de caja de cambios, potencia, modelo, kilometraje, tipo de combustible, marca, estado de reparación, entre otras. La variable objetivo es `Price`.

## 🔧 Proceso realizado

1. **Preparación de datos**
   - Eliminación de columnas irrelevantes (fechas de rastreo, código postal, número de fotos, etc.)
   - Tratamiento de valores ausentes en variables categóricas
   - Detección y eliminación de valores duplicados (27,543 filas) antes de dividir los datos, evitando fuga de información
   - Filtrado de valores atípicos en precio, año de registro y potencia
   - Codificación ordinal de variables categóricas
   - Escalado de variables numéricas (para el modelo lineal)

2. **Entrenamiento de modelos**
   - Modelo base: Regresión Lineal
   - Árbol de Decisión
   - Random Forest
   - LightGBM
   - CatBoost

3. **Ajuste de hiperparámetros**
   - Se probaron múltiples configuraciones para Random Forest, LightGBM y CatBoost, midiendo RMSE, tiempo de entrenamiento y tiempo de predicción en cada caso.

4. **Evaluación final**
   - Selección del modelo con mejor equilibrio entre los tres criterios
   - Validación del desempeño sobre un conjunto de prueba no utilizado previamente

## 📊 Resultados

| Modelo | RMSE (validación) | Tiempo de entrenamiento (s) | Tiempo de predicción (s) |
|---|---|---|---|
| LightGBM – Config 3 | 1529.57 | 4.33 | 0.79 |
| **CatBoost – Config 2** | **1581.05** | **9.78** | **0.01** |
| Random Forest – Config 2 | 1586.49 | 25.08 | 0.59 |
| Modelo Dummy (referencia) | 4560.06 | – | 0.01 |

**Modelo final recomendado: CatBoost (Config 2)**
- RMSE en conjunto de prueba: **1593.05**
- Tiempo de predicción en prueba: **0.0412s**

CatBoost Config 2 no obtuvo el RMSE más bajo de todas las configuraciones evaluadas, pero ofrece el mejor balance entre calidad de predicción y velocidad de respuesta, un criterio crítico para una aplicación que debe responder en tiempo real.

## 🛠️ Tecnologías utilizadas

- Python
- Jupyter Notebook
- pandas, NumPy
- scikit-learn
- LightGBM
- CatBoost
- Matplotlib / Seaborn

## 📁 Estructura del repositorio

├── notebook_rusty_bargain.ipynb   # Notebook principal con todo el pipeline
├── README.md                       # Este archivo
└── data/                           # (no incluida por tamaño/licencia)

## 🚀 Cómo ejecutar

```bash
pip install pandas numpy scikit-learn lightgbm catboost matplotlib seaborn
jupyter notebook notebook_rusty_bargain.ipynb
```

## 📌 Conclusiones principales

- Los modelos de boosting (LightGBM, CatBoost) superan significativamente a la Regresión Lineal en calidad de predicción.
- La velocidad de predicción varía considerablemente entre modelos, siendo un factor decisivo para aplicaciones en tiempo real.
- El mejor modelo no siempre es el de menor error: el trade-off entre calidad y velocidad es clave para la decisión final.

---
## 👤 Autor

**Juan Carlos Buri** — Junior Data Scientist
