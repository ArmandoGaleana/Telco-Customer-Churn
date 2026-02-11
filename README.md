# Telco Customer Churn

# Predicción de Cancelación de Clientes (Customer Churn)

## Problema de Negocio

Una empresa de telecomunicaciones enfrenta una tasa significativa de cancelación de clientes (churn).  
El objetivo de este proyecto es **identificar clientes en riesgo de cancelar su servicio** para implementar campañas de retención (descuentos, planes especiales, soporte personalizado) antes de que abandonen la empresa.

Retener un cliente es considerablemente más barato que adquirir uno nuevo, por lo que una buena predicción puede generar un impacto financiero importante.

---

## Objetivo del Proyecto

Construir un modelo de Machine Learning que prediga la probabilidad de cancelación de un cliente.

- Variable objetivo: `Churn Value`
  - 1 = Cliente cancela
  - 0 = Cliente permanece
- Métrica principal: **AUC-ROC**
- Enfoque de negocio: **Maximizar Recall**
- Métricas secundarias: Accuracy, Precision, F1-score

---

## Dataset

Dataset de clientes de telecomunicaciones en formato Excel.

El conjunto de datos contiene información demográfica, tipo de contrato, servicios contratados, cargos mensuales y valor estimado del cliente (CLTV).

⚠ Columnas eliminadas por posible *data leakage*:
- `Churn Label`
- `Churn Score`
- `Churn Reason`

Estas variables contienen información derivada directamente de la cancelación y podrían inflar artificialmente el desempeño del modelo.

---

## Metodología

1. **Carga y limpieza de datos**
   - Eliminación de columnas irrelevantes
   - Conversión de variables numéricas
   - Limpieza de strings
   - Eliminación de duplicados

2. **Análisis Exploratorio (EDA)**
   - Tasa general de churn
   - Churn por tipo de contrato
   - Churn por antigüedad (Tenure Months)
   - Visualización de patrones clave

3. **Preparación de datos**
   - División train/test con estratificación
   - Imputación de valores faltantes
   - Escalado de variables numéricas
   - Codificación One-Hot para variables categóricas

4. **Modelado**
   - Logistic Regression (modelo base)
   - Random Forest (modelo no lineal)

5. **Optimización de umbral**
   - Ajuste del threshold para priorizar Recall
   - Evaluación con matriz de confusión

---

## Resultados

- Logistic Regression AUC-ROC: ~0.84
- Random Forest AUC-ROC: ~0.85

Al reducir el umbral de decisión:
- Recall ≈ 98%
- Se detecta casi la totalidad de clientes en riesgo
- Aumentan los falsos positivos (trade-off entre costo y cobertura)

---

## Interpretación de Negocio

Reducir el umbral permite identificar casi todos los clientes que cancelarán el servicio.

Sin embargo:
- Un umbral muy bajo incrementa el número de clientes marcados como riesgo
- Esto puede aumentar el costo de campañas de retención

El siguiente paso ideal sería optimizar el umbral considerando:
- Costo de campaña
- Tasa de retención
- Ingreso promedio por cliente

---