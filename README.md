# Riesgo Crediticio — Regresión Logística vs Random Forest

**Autor:** Néstor Camilo Hernández Campo

Modelo de clasificación supervisada para predecir riesgo de mora en un portafolio de **36.457 clientes**, comparando Regresión Logística L2 vs Random Forest con foco en impacto financiero real.

---

## Problema de negocio

Las entidades financieras enfrentan pérdidas significativas por aprobar créditos a clientes que no pagarán (Falsos Negativos). Este proyecto construye un sistema de scoring crediticio que permite identificar clientes de alto riesgo antes de aprobar un crédito, reduciendo la exposición al impago y optimizando las decisiones de colocación.

> Un solo Falso Negativo representa **COP $9.000.000** de pérdida de capital.

---

## Resultados

| Métrica | Reg. Logística | Random Forest |
|---|---|---|
| Accuracy | 0.904 | **0.987** |
| Precision | 0.148 | **0.756** |
| Recall | **0.978** | 0.351 |
| F1-Score | 0.256 | **0.480** |
| ROC-AUC | 0.972 | **0.979** |
| Falsos Negativos | **4** | 119+ |
| Gap Train-Val | **0.0008** | 0.6497 |

### Impacto financiero

| Modelo | Costo oportunidad (FP) | Pérdida capital (FN) | Total |
|---|---|---|---|
| Regresión Logística | $1.255.200.000 | **$36.000.000** | $1.291.200.000 |
| Random Forest | **$25.200.000** | $1.080.000.000 | $1.105.200.000 |

### Modelo recomendado por escenario

**Regresión Logística** → cuando el objetivo es **minimizar pérdidas por impago**. Con un Recall del 97.8% y solo 4 Falsos Negativos, actúa como filtro de riesgo máximo. Ideal para entidades con alta aversión al riesgo crediticio.

**Random Forest** → cuando el objetivo es **reducir rechazos innecesarios** de buenos clientes. Con una Precisión del 75.6% y menor costo de oportunidad ($25.2M COP en FP), es adecuado para estrategias de crecimiento comercial agresivo.

---

## Hallazgos del análisis exploratorio

- **Desbalance severo:** 35.841 buenos pagadores (98.31%) vs 616 en mora (1.69%)
- **Diferenciador principal:** los clientes en mora tienen en promedio **1.2 años menos de antigüedad laboral** que los buenos pagadores
- **Ingreso promedio similar entre grupos:** buenos pagadores $186.700 vs en mora $185.865 — el ingreso solo no predice el riesgo
- **Edad promedio similar:** 43.7 años buenos pagadores vs 43.6 años en mora
- **Conclusión EDA:** la estabilidad laboral es el factor más relevante para predecir el comportamiento de pago

---

## Decisiones técnicas clave

- **Imputación con criterio de negocio:** valores nulos en variables de mora se interpretaron como ausencia del evento, no como dato faltante → variable binaria `tiene_historial_mora`
- **PCA descartado:** varianza explicada insuficiente (12.39% en 2 componentes) — se trabajó con las variables originales transformadas
- **Threshold Tuning:** umbral ajustado a 0.95 para maximizar Recall y reducir Falsos Negativos en contexto crediticio, donde el costo del error tipo II es crítico
- **Desbalance tratado con:** `class_weight='balanced'` + validación cruzada estratificada `StratifiedKFold` 5-fold
- **Winsorización:** aplicada en 10 variables numéricas con outliers, con mayor presencia en `meses_sin_deuda` (15.42%)
- **Codificación:** Label Encoding jerárquico para `name_education_type`, One-Hot Encoding para el resto de variables categóricas

---

## Estabilidad de los modelos

La Regresión Logística demostró ser el modelo más robusto con un Gap Train-Validación de apenas 0.0008, lo que indica que no sufre sobreajuste y generaliza bien a datos nuevos. El Random Forest, aunque superior en accuracy, presenta un Gap de 0.6497 — señal clara de sobreajuste que limita su confiabilidad en producción.

---

## Limitaciones conocidas

- Dataset con desbalance severo (98% / 2%) que condiciona el comportamiento de todos los modelos
- Sin variables macroeconómicas externas (tasa de interés, índice de desempleo, ciclo económico)
- Sin información de bureau de crédito externo (centrales de riesgo)
- Modelos entrenados y evaluados en el mismo dataset histórico — no validados en producción con datos nuevos
- El análisis de impacto financiero usa un monto promedio fijo por crédito, no montos individuales reales

---

## Próximos pasos

- Probar **XGBoost** y **LightGBM** como modelos de ensamble alternativos con mejor manejo del desbalance
- Aplicar **SMOTE** (Synthetic Minority Oversampling Technique) para sobremuestreo de la clase minoritaria
- Desarrollar una **API de scoring en tiempo real** con FastAPI para integración con sistemas de originación
- Incorporar **variables externas** de bureaus de crédito para enriquecer el perfil del cliente
- Implementar **monitoreo de data drift** para detectar degradación del modelo en producción
- Explorar modelos de **detección de anomalías** como complemento al clasificador supervisado

---

## Stack tecnológico

`Python` · `Pandas` · `Scikit-learn` · `Matplotlib` · `Seaborn` · `Power BI`

---

## Estructura del proyecto

```
├── actividad_final_nestor_camilo_hernandez_campo.ipynb  # Notebook principal con todo el análisis
├── dataset_credito_unificado.csv                        # Dataset original (36.457 clientes, 23 variables)
├── riesgo_financiero.pbix                               # Dashboard interactivo Power BI
├── dashboard_credito.png                                # Captura del dashboard
└── README.md                                            # Documentación del proyecto
```

---

## Cómo ejecutar

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
jupyter notebook actividad_final_nestor_camilo_hernandez_campo.ipynb
```

---

## Contacto

**Néstor Camilo Hernández Campo**
Proyecto de análisis de riesgo crediticio — Machine Learning 
