# Riesgo Crediticio - Regresion Logistica vs Random Forest

**Autor:** Nestor Camilo Hernandez Campo

Modelo de clasificacion supervisada para predecir riesgo de mora en **36.457 clientes**, comparando Regresion Logistica L2 vs Random Forest con foco en impacto financiero real.

---

## Resultados

| Metrica          | Reg. Logistica | Random Forest |
|------------------|----------------|---------------|
| Accuracy         | 0.904          | **0.987**     |
| Precision        | 0.148          | **0.756**     |
| Recall           | **0.978**      | 0.351         |
| F1-Score         | 0.256          | **0.480**     |
| ROC-AUC          | 0.972          | **0.979**     |
| Falsos Negativos | **4**          | 119+          |
| Overfitting      | Gap 0.0008     | Severo        |

> Un Falso Negativo = **COP 9.000.000** de perdida de capital

---

## Decisiones clave

- Imputacion con criterio de negocio: nulos en mora = evento nunca ocurrio → variable `tiene_historial_mora`
- PCA descartado: 2 componentes = solo 12.39% de varianza
- Threshold Tuning: umbral optimo 0.95 para Regresion Logistica
- Balanceo: `class_weight='balanced'` + `StratifiedKFold` 5-fold

---

## Stack

Python · Pandas · Scikit-learn · Matplotlib · Seaborn · Power BI

---

## Como ejecutar

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
jupyter notebook actividad_final_nestor_camilo_hernandez_campo.ipynb
```

**LinkedIn:** linkedin.com/in/camilo-hernandez-data
