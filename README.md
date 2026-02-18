# Detección de fraudes con uso de tarjeta de credito
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1DH962JbLDAhDVHQmECVNqXOQ8j-j6T-4?usp=sharing)
![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-Gradient_Boosting-orange.svg)
![SHAP](https://img.shields.io/badge/SHAP-Explainable_AI-green.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit_Learn-Machine_Learning-yellow.svg)

## Visión General
Este proyecto en base a un dasaset, esta diseñado para detectar transacciones fraudulentas con tarjetas de credito. El principal desafio abordado a lo largo del proyecto fue el desbalaceo extremo de la clase 'Class', donde los datos de fraudes solo representaban un **0.17%** del total de transacciones.

El enfoque no solamente se centro en entrenar un modelo algoritmico para predecir resultados, tambien en construir una solución con calidad para producción que pueda evaluar el impacto financiero, que sea interpretable y que tenga una simulación aleatoria para mas realismo.

## Impacto de Negocio
Al aplicar el modelo XGBoost optimizado en un set de prueba, el sistema logró lo siguiente:
* **Recuperar un 75.8% del capital expuesto a fraude** (Mas detalles en el archivo .ipynb).
* Generar el ahorro neto correspondiente en la sesión de prueba.
* Mantener falsos positivos bajos, asegurando una experiencia a clientes de manera acertiva.

<img width="768" height="489" alt="image" src="https://github.com/user-attachments/assets/436e4c32-9c40-4b4b-834d-d29175e0cb01" />

## Arquitectura Técnica y Pipeline

1. **Preprocesamiento y Limpieza:**
   * Manejo de variables altamente sesgadas (Time, Amount) utilizando `RobustScaler` para mitigar el impacto de valores atípicos.
   * Análisis de Componentes Principales (PCA) provenientes del dataset original (Como v14, v2, v12, etc).

2. **Estrategia contra el Desbalanceo:**
   * Implementación de **SMOTE** (Synthetic Minority Over-sampling Technique) exclusivo en el set de entrenamiento para equilibrar las clases 50/50 sin generar fuga de datos (*Data Leakage*).

3. **Modelado y Benchmark:**
   * Se evaluaron tres algoritmos: *Regresión Logística*, *Random Forest* y *XGBoost*.
   * **Ganador:** **XGBoost**. Se ajustó la profundidad (`max_depth=10`) para controlar el *overfitting*. A diferencia del Random Forest, la naturaleza secuencial de XGBoost permitió aprender de los errores pasados, logrando un **F1-Score de 0.76** y un **Recall de 0.86** en la detección de fraudes.
     
<img width="352" height="343" alt="image" src="https://github.com/user-attachments/assets/8095abfd-ef48-4060-a8b2-9a43aa8a5d61" />

## Inteligencia Artificial Explicable (XAI) con SHAP
Para evitar que el modelo sea una "caja negra" inoperable por los equipos de seguridad, se integró la librería **SHAP**:
* **Visualización de variables:** Identificamos que anomalías negativas en variables como `V14` y positivas en `V4` son los principales detonantes matemáticos del fraude.
* **Auditoría de fraude exacta:** Capacidad de aislar una sola transacción y explicar visualmente qué variables empujaron al modelo a bloquear la tarjeta.
  
<img width="1248" height="330" alt="image" src="https://github.com/user-attachments/assets/6876d98f-daa9-44d8-8169-7051f5c53d42" />

## Simulador en Tiempo Real
Se desarrolló un Dashboard integrado usando HTML/CSS dentro del entorno Python para simular el flujo de procesos. El sistema procesa transacciones aleatorias y calcula probabilidades para determinar si la transacción es fraude o es una transacción normal, incluye contadores.

<img width="862" height="480" alt="image" src="https://github.com/user-attachments/assets/e79d9337-ea15-436e-ade9-2e8b7baadd61" />

## Conclusión
El desarrollo de este detector de fraudes se centró en resolver uno de los problemas más críticos del sector financiero. Partiendo de un escenario con un desbalanceo extremo, el objetivo no era solamente predecir, sino equilibrar las condiciones para no sesgar el aprendizaje del algoritmo. 

Técnicas clave como `RobustScaler` y `SMOTE` fueron esenciales para el avance. En cuanto al modelado, **XGBoost** fue la opción ganadora por su capacidad de construir árboles secuencialmente y aprender de errores pasados, logrando un rendimiento superior sin caer en *overfitting*. Las pruebas se dividieron en tres frentes: **impacto financiero** (dinero tangible), **explicabilidad de impacto a partir de variables** (SHAP) y **despliegue realista aleatorio** (dashboard). Esta solución demuestra que el modelo no solo es matemáticamente robusto, sino que está listo para generar valor operativo.

---
* **Herramientas:** Python, Pandas, Scikit-Learn, XGBoost, SHAP, Matplotlib.
