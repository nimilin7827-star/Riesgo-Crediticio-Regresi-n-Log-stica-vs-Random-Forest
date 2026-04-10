Riesgo Crediticio — Regresion Logistica vs Random Forest
Mostrar imagen
Mostrar imagen
Mostrar imagen
Autor: Nestor Camilo Hernandez Campo
Modelo de clasificacion supervisada para predecir riesgo de mora en un portafolio de 36.457 clientes, comparando Regresion Logistica L2 vs Random Forest con foco en impacto financiero real.

Archivos
actividad_final_nestor_camilo_hernandez_campo.ipynb
riesgo_financiero.pbix
dataset_credito_unificado.csv
README.md

Resultados
MetricaReg. LogisticaRandom ForestAccuracy0.9040.987Precision0.1480.756Recall0.9780.351F1-Score0.2560.480ROC-AUC0.9720.979Falsos Negativos4119+OverfittingGap 0.0008Severo

Un Falso Negativo = COP 9.000.000 de perdida de capital (LGD 60% sobre credito promedio de $15M)


Decisiones clave

Imputacion con criterio de negocio: nulos en mora = el evento nunca ocurrio. Se creo la variable binaria tiene_historial_mora
PCA descartado: 2 componentes explicaban solo el 12.39% de varianza acumulada
Threshold Tuning: umbral optimo en 0.95 para Regresion Logistica
Balanceo de clases: class_weight='balanced' + StratifiedKFold 5-fold


Stack
Python · Pandas · Scikit-learn · Matplotlib · Seaborn · Power BI

Como ejecutar
bashpip install pandas numpy scikit-learn matplotlib seaborn
jupyter notebook actividad_final_nestor_camilo_hernandez_campo.ipynb
