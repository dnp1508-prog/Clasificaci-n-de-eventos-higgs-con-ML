# Clasificaci-n-de-eventos-higgs-con-ML
Clasificación binaria para distinguir eventos de **señal** (producción del bosón de Higgs)
de eventos de **fondo** a partir de variables cinemáticas de colisiones de partículas.
Dataset: [HIGGS (UCI)](https://archive.ics.uci.edu/dataset/280/higgs), 28 variables.

## Contenido

- `higgs.ipynb`: análisis exploratorio, entrenamiento y evaluación de los modelos.

## Datos

Se usa un subconjunto de 98.050 eventos (46.223 de fondo y 51.827 de señal, aprox. equilibrado),
dividido en 78.440 para entrenamiento y 19.610 para prueba.
El dataset no se incluye en el repositorio; descárgalo desde el enlace anterior.

## Metodología

1. Análisis exploratorio: distribución de clases, densidad de `m_jj` por clase y matriz de correlación de las variables de alto nivel.
2. Modelos: regresión logística, árbol de decisión y árbol de decisión optimizado
   (mejores hiperparámetros: `criterion=entropy`, `max_depth=5`,`min_samples_split=2`).
3. Evaluación sobre el conjunto de prueba con matriz de confusión, precision, recall, F1 y AUC-ROC.

## Resultados

| Modelo | Accuracy | F1 (señal) | Recall (señal) | AUC |
|--------|----------|------------|----------------|-------|
| Regresión logística | 0.64 | 0.68 | 0.74 | 0.681 |
| Árbol de decisión | 0.66 | 0.70 | 0.74 | 0.719 |
| Árbol optimizado | 0.66 | 0.69 | 0.73 | 0.720 |

Variables más importantes en el árbol: `m_bb` (aprox. 50 % de la importancia), `m_wwbb` y `m_wbb`.

## Conclusiones y limitaciones

- El árbol supera a la regresión logística en AUC (+0.04), lo que indica relaciones no lineales
  entre las variables y la clase.
- La optimización de hiperparámetros apenas mejora al árbol base (0.719 → 0.720): el límite
  está en la capacidad del modelo, no en el ajuste.
- El rendimiento absoluto es moderado. Todos los modelos detectan bien la señal (recall ~0.73)
  pero clasifican peor el fondo (recall 0.52-0.57).
- Solo se usó un subconjunto del dataset completo y modelos simples.

## Trabajo futuro

Random Forest, gradient boosting (XGBoost/LightGBM), redes neuronales y entrenamiento con más datos.

## Requisitos

Python 3, numpy, pandas, scikit-learn, matplotlib, seaborn.

## Uso

Abre `higgs.ipynb` en Google Colab o Jupyter y ejecuta las celdas en orden.

## Autor

David