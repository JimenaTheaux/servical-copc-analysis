# 📊 Análisis de Performance Operativa — Contact Center ServiCall

**Stack:** Python · Pandas · Power BI  
**Área:** Contact Center | Estándares COPC  
**Estado:** Finalizado proyecto hipótetico para contact center

---

## 🎯 Contexto del problema
ServiCall S.A. opera un contact center con 250 agentes en 3 turnos. El área de calidad detectó un incremento del 18% en ausentismo y 
deterioro en FCR, pero sin visibilidad real: todo estaba en Excel sin integración entre áreas.

**Objetivo:** construir un sistema de monitoreo basado en datos bajo estándares COPC para detectar desvíos y oportunidades de mejora.

## 📁 Estructura del repositorio
| Carpeta | Contenido |
|---|---|
| `data/` | Dataset RAW original y dataset limpio |
| `notebooks/` | Notebook de limpieza con Pandas |
| `dashboard/` | Archivo Power BI (.pbix) |
| `assets/` | Screenshots del dashboard |

## Fase 1 — Dataset
Dataset generado con Python simulando operación real de contact center.
5.015 registros · 20 columnas · 12 meses (2024)

**Problemas de calidad detectados:**
- Fechas en dos formatos distintos
- Valores imposibles en AHT (-1, 0, 9999)
- 14 variantes sucias en tipo_gestion
- 15 duplicados exactos
- 10% de nulos en NPS_score
- Encoding roto en nombres de agentes
- Columna constante sin valor analítico

## Fase 2 — Limpieza con Pandas

📓 [`notebooks/01_limpieza_datos.ipynb`](notebooks/01_limpieza_datos.ipynb)

**Decisiones tomadas:**
| Problema | Solución | Justificación |
|---|---|---|
| 15 duplicados | `drop_duplicates()` | Métricas infladas |
| Columna constante | `drop()` | Sin valor analítico |
| Fechas mixtas | `pd.to_datetime(dayfirst=True)` | Estandarización |
| AHT imposibles | Mediana por tipo de gestión | Robusta a outliers |
| NPS nulos | Mediana por agente | Preserva patrón individual |
| tipo_gestion sucio | `.str.strip().str.title()` + `.replace()` | 14 variantes → 6 |
| Encoding roto | `.str.replace()` | Corrección manual |

**Features creadas:**
- `AHT_minutos` — AHT en minutos para legibilidad
- `rango_AHT` — segmentación Corta / Normal / Larga / Muy larga
- `NPS_categoria` — Promotor / Neutro / Detractor
- `riesgo_agente` — flag combinando satisfacción y ausentismo
- `mes`, `dia_semana`, `es_fin_de_semana` — análisis temporal

## 📊 Fase 3 — Dashboard Power BI
**KPIs monitoreados bajo estándares COPC:**
- AHT promedio por agente y turno
- FCR % (First Contact Resolution)
- Tasa de rellamado a 7 días
- PEC % (Porcentaje de Errores Críticos)
- NPS por área y tipo de gestión

## 💡 Principales hallazgos
1. ...
2. ...
3. ...

---

## ▶️ Cómo reproducir el análisis

```bash
git clone https://github.com/JimenaTheaux/servical-copc-analysis
```

Abrir `notebooks/01_limpieza_datos.ipynb` en Google Colab o Jupyter.
Dataset RAW disponible en `data/servical_contactcenter_RAW.csv`


## 👩‍💻 Autora
**Jimena Theaux** — Data Analyst  
[LinkedIn](https://linkedin.com/in/jimena-theaux) · 
[GitHub](https://github.com/JimenaTheaux) · 
[deciDATA](https://decidata.com.ar)
