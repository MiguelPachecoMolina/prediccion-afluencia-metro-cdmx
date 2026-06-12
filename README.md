# 🚇 Predicción de Afluencia del Metro CDMX

## 📝 Descripción del Proyecto
Este proyecto se centra en el desarrollo de un modelo predictivo para estimar la cantidad de usuarios en la red de transporte del Metro de la Ciudad de México. El objetivo es analizar los patrones de movilidad, identificar tendencias, detectar estacionalidad y anomalías, y realizar pronósticos de afluencia futura para optimizar la toma de decisiones en políticas de movilidad urbana.

## 👥 Equipo de Trabajo
Este proyecto de investigación y modelado estadístico fue desarrollado por:
* **Miguel Alejandro Pacheco Molina**
* **Jesús Armando Soria Martínez**

## 📊 Conjunto de Datos
* **Fuente:** Datos Abiertos de la Ciudad de México.
* **Periodo Analizado:** Se segmentó la serie temporal exclusivamente al año 2023 para obtener un comportamiento estable y representativo de la operación normal del Metro, eliminando el ruido y las anomalías de los años de pandemia.
* **Variable Objetivo:** Afluencia total diaria (suma de las entradas registradas por día en todas las estaciones y líneas).

## ⚙️ Metodología y Tecnologías Aplicadas
* **Análisis Exploratorio (EDA):** Descomposición de la serie temporal y evaluación de estacionariedad mediante la prueba Augmented Dickey-Fuller (ADF) y gráficos ACF/PACF.
* **Transformaciones:** Aplicación de diferenciación estacional de 7 días (D=1, s=7) para aislar el fuerte patrón semanal del transporte urbano.
* **Modelado SARIMA:** Configuración de un modelo inicial mediante inspección visual `SARIMA(1,0,1)(0,1,1)_7` y optimización mediante Grid Search para definir el mejor modelo base `SARIMA(1,0,2)(0,1,1)_7`.
* **Modelo SARIMAX (Variables Exógenas):** Al diagnosticar heterocedasticidad en días festivos, se incorporó la variable binaria `es_festivo` para capturar las caídas abruptas de demanda, resultando en el modelo final `SARIMAX(1,0,1)(0,1,1)_7 + es_festivo`.
* **Tecnologías:** Python, Pandas, Statsmodels, Scikit-learn, Matplotlib.

## 🏆 Resultados Destacados
Se evaluó la capacidad predictiva de los modelos mediante validación cruzada con ventanas deslizantes:

* **Modelo SARIMA Base:** Alcanzó un RMSE de 314,446 y un MAPE de 7.54%.
* **Modelo Final SARIMAX (+ Festivos):** Logró reducir el RMSE significativamente a 282,017, manteniendo un MAPE de 7.82%.
* **Conclusión:** La inclusión de la variable exógena permitió al modelo capturar de manera realista los cambios abruptos asociados a días festivos. Al reducir el RMSE (que penaliza los errores grandes), el modelo SARIMAX demostró ser mucho más robusto para escenarios atípicos.

## 🚀 Trabajo Futuro
Para perfeccionar la capacidad predictiva, se proyecta la incorporación de variables exógenas adicionales que modelen periodos vacacionales prolongados (calendario SEP/Universidades), factores climáticos y eventos masivos en la ciudad.
