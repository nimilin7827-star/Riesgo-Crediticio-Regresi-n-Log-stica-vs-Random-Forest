# Riesgo-Crediticio-Regresi-n-Log-stica-vs-Random-Forest
Autor: Néstor Camilo Hernández Campo Modelo de clasificación supervisada para predecir riesgo de mora en un portafolio de 36.457 clientes, comparando Regresión Logística L2 vs Random Forest con foco en impacto financiero real.

Resultados
MétricaReg. LogísticaRandom ForestAccuracy0.9040.987Precision0.1480.756Recall0.9780.351F1-Score0.2560.480ROC-AUC0.9720.979Falsos Negativos4 ★119+Overfitting✅ Gap 0.0008⚠️ Severo

Un Falso Negativo = COP 9.000.000 de pérdida de capital (LGD 60% · crédito promedio $15M)


🧠 Decisiones clave

Imputación con criterio de negocio: nulos en mora = el evento nunca ocurrió → variable binaria tiene_historial_mora
PCA descartado: 2 componentes explicaban solo el 12.39% de varianza
Threshold Tuning: umbral óptimo en 0.95 para Regresión Logística
Balanceo: class_weight='balanced' + StratifiedKFold 5-fold


🛠️ Stack
Python · Pandas · Scikit-learn · Matplotlib · Seaborn · Power BI
