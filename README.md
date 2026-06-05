# Prevalencia de Enfermedades Crónicas en Guanajuato

Análisis longitudinal de encuestas de salud del adulto para el estado de Guanajuato en los años 2020, 2021 y 2022. El objetivo es identificar y comparar tendencias en enfermedades crónicas, salud mental, estilos de vida y acceso a servicios de salud, y exponer esos hallazgos en un dashboard interactivo.

> Proyecto desarrollado para **Juventudes GTO** como parte del programa **Exportación de Talento 2024**.

---

## Estructura del proyecto

```
.
├── data/
│   ├── raw/
│   │   ├── 2020/          ← ENSANUT Continua COVID-19 (CSV + catálogo)
│   │   ├── 2021/          ← ENSADUL 2021 (CSV + catálogo)
│   │   └── 2022/          ← ENSADUL 2022 (CSV + catálogo)
│   └── processed/
│       ├── ensanut2020_GTO_clean.csv       ← Dataset limpio 2020  ✅
│       ├── ensadul2021_GTO_clean.csv       ← Dataset limpio 2021  ✅
│       ├── ensadul2022_GTO_clean.csv       ← Dataset limpio 2022  ✅
│       ├── ensadul_GTO_panel_3yr.csv       ← Panel armonizado 2020–2022  ✅
│       └── ensadul_GTO_panel_2yr.csv       ← Panel 2021–2022 (incl. crónicas)  ✅
│
├── notebooks/
│   ├── 01_limpieza_eda_2020.ipynb          ← Limpieza + EDA ENSANUT 2020  ✅
│   ├── 02_limpieza_eda_2021.ipynb          ← Limpieza + EDA ENSADUL 2021  ✅
│   ├── 03_limpieza_eda_2022.ipynb          ← Limpieza + EDA ENSADUL 2022  ✅
│   └── 04_analisis_comparativo.ipynb       ← Análisis longitudinal 2020–2022  ✅
│
├── outputs/
│   └── figures/
│       ├── 2020/          ← Gráficas EDA 2020  ✅
│       ├── 2021/          ← Gráficas EDA 2021  ✅
│       ├── 2022/          ← Gráficas EDA 2022  ✅
│       └── comparativo/   ← Gráficas del análisis longitudinal  ✅
│
├── dashboard/             ← Aplicación de visualización interactiva  (pendiente)
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## Etapas del proyecto

| # | Etapa | Estado |
|---|-------|--------|
| 1 | Limpieza de datos + EDA — ENSANUT COVID-19 2020 | ✅ Completado |
| 2 | Limpieza de datos + EDA — ENSADUL 2021 | ✅ Completado |
| 3 | Limpieza de datos + EDA — ENSADUL 2022 | ✅ Completado |
| 4 | Análisis comparativo longitudinal 2020–2022 | ✅ Completado |
| 5 | Dashboard interactivo | 🔲 Pendiente |

---

## Datasets

### Nota sobre las fuentes

Las tres ediciones provienen de encuestas distintas. La de 2020 fue levantada en el contexto de la pandemia de COVID-19 y tiene un cuestionario diferente; no incluye diagnósticos de enfermedades crónicas ni escala de síntomas depresivos, pero agrega preguntas sobre aceptación de vacunas y violencia doméstica durante el confinamiento.

| Año | Encuesta | n original | Variables orig. | Dataset limpio |
|-----|----------|-----------|-----------------|----------------|
| 2020 | ENSANUT Continua COVID-19 | 1,035 | 114 | 1,035 × 24 |
| 2021 | ENSADUL | 1,115 | 704 | 1,115 × 74 |
| 2022 | ENSADUL | 1,227 | 572 | 1,227 × 61 |

### Temas cubiertos por año

| Tema | 2020 | 2021 | 2022 |
|------|:----:|:----:|:----:|
| Demografía (edad, sexo, municipio, urbanidad) | ✅ | ✅ | ✅ |
| Tabaquismo y alcohol | ✅ | ✅ | ✅ |
| Ideación suicida y violencia | ✅ | ✅ | ✅ |
| Enfermedades crónicas (diabetes, HTA, colesterol…) | — | ✅ | ✅ |
| Salud mental — escala CES-D | — | ✅ | ✅ |
| Antecedentes familiares de enfermedades | — | ✅ | ✅ |
| Discapacidades y dificultades funcionales | — | ✅ | ✅ |
| Actividad física (caminata semanal) | — | ✅ | — |
| Vacunas (influenza, COVID-19) | ✅ | — | — |
| Violencia durante el confinamiento COVID-19 | ✅ | — | — |

---

## Hallazgos principales (análisis comparativo)

| Indicador | 2020 | 2021 | 2022 | Tendencia |
|-----------|:----:|:----:|:----:|-----------|
| Tabaquismo activo | 15.5% | 17.1% | 15.1% | Estable |
| Consume alcohol (≥mensual) | 40.7% | 46.0% | 46.9% | ↑ Al alza |
| Víctimas de violencia (12m) | 3.3% | 3.3% | 2.3% | ↓ Ligera mejora |
| Diabetes | — | 10.9% | 13.1% | ↑ +2.2 pp |
| Hipertensión | — | 21.3% | 20.5% | ↓ -0.8 pp |
| Colesterol alto | — | 14.8% | 16.1% | ↑ +1.3 pp |
| Score depresivo (CES-D, media) | — | 10.98 | 11.02 | Estable |

---

## Cómo reproducir

```bash
# 1. Clonar el repositorio
git clone https://github.com/<usuario>/prevalencia-enfermedades-gto.git
cd prevalencia-enfermedades-gto

# 2. Crear entorno virtual e instalar dependencias
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# 3. Ejecutar los notebooks en orden
jupyter notebook notebooks/
```

> Los archivos de datos crudos deben colocarse en `data/raw/<año>/` antes de ejecutar.
> Los notebooks están numerados en orden de ejecución sugerido (01 → 04).

---

## Tecnologías

- **Python 3.10+** — pandas, numpy, matplotlib, seaborn, scipy
- **Jupyter Notebooks** — limpieza, análisis exploratorio y comparativo
- **Dashboard** *(pendiente)* — por definir (Streamlit / Power BI / Tableau)

---

*Proyecto realizado para Juventudes GTO · Programa Exportación de Talento 2024*
