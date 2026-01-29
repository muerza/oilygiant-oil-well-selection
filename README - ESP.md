# OilyGiant — Selección de pozos petroleros con análisis de riesgo 🛢️📊

Este proyecto selecciona la **mejor región** para desarrollar **200 nuevos pozos petroleros** bajo restricciones estrictas del negocio.  
Entrenamos un modelo de **Regresión Lineal** para predecir el volumen de reservas (`product`) y luego usamos **bootstrapping** para estimar la incertidumbre del beneficio y el **riesgo de pérdida**.

---

## Objetivo 🎯

Elegir la región que:
- Mantenga la **probabilidad de pérdida < 2.5%** ✅
- Maximice el **beneficio esperado** 💰

---

## Supuestos del negocio 💵

- Presupuesto total: **$100,000,000**
- Pozos a desarrollar: **200**
- Puntos de exploración por región: **500**
- Ingreso por unidad de `product`: **$4,500**
- Umbral mínimo de producción (punto de equilibrio): **111.1 unidades** *(derivado en el notebook)*

---

## Enfoque 🧩

1) **Modelado**
- Entrenar un modelo de **Regresión Lineal** por región para predecir `product`.

2) **Selección de pozos**
- Para cada región, tomar los **200 pozos con mayor predicción** de entre 500 puntos de exploración.

3) **Cálculo de beneficio**
- Calcular el beneficio de los pozos seleccionados usando las constantes del negocio.

4) **Bootstrapping (riesgo) 🎲**
- Repetir muchas veces el proceso de selección/beneficio (remuestreo) para estimar:
  - Beneficio promedio
  - Intervalo de confianza (cuantiles 2.5% / 97.5%)
  - Probabilidad de pérdida

---

## Desempeño del modelo (validación) 🧪

| Región | RMSE | R² |
|---|---:|---:|
| geo_data_0 | 37.6834 | 0.2738 |
| geo_data_1 | 0.8923 | 0.9996 |
| geo_data_2 | 40.1525 | 0.2023 |

> La región `geo_data_1` muestra un RMSE muchísimo menor y un R² muy alto en comparación con las otras.

---

## Resultados de beneficio y riesgo (bootstrapping) 📈

| Región | Beneficio promedio (USD) | Cuantil 2.5% | Cuantil 97.5% | Prob. de pérdida | ROI | ROI efectivo |
|---|---:|---:|---:|---:|---:|---:|
| geo_data_0 | $4,089,561.93 | $-963,570.86 | $9,616,291.73 | 5.20% | 4.09% | 3.88% |
| geo_data_1 | $4,714,887.65 | $523,824.95 | $9,114,850.35 | 1.20% | 4.71% | 4.66% |
| geo_data_2 | $4,209,020.14 | $-1,403,231.64 | $9,343,215.56 | 7.40% | 4.21% | 3.90% |

✅ **Región recomendada:** `geo_data_1`  
- Beneficio promedio: **$4,714,887.65**
- Probabilidad de pérdida: **1.20%** *(cumple el requisito de <2.5%)*

---

## Tecnologías 🛠️
- Python
- pandas, NumPy
- scikit-learn
- matplotlib

---

## Cómo ejecutar ▶️

1) Instala dependencias:
```bash
pip install -r requirements.txt
