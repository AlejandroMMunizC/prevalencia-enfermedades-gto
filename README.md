# Prevalencia de Enfermedades Crónicas en Guanajuato

> Análisis longitudinal de encuestas de salud del adulto en Guanajuato · 2020–2022  
> Proyecto desarrollado para **Juventudes GTO** como parte del programa **Exportación de Talento 2024**

**[→ Ver dashboard interactivo](https://alejandrommunizc.github.io/prevalencia-enfermedades-gto/)**

---

## ¿De qué trata este proyecto?

Se procesaron tres ediciones de encuestas nacionales de salud levantadas en el estado de Guanajuato para identificar tendencias en enfermedades crónicas, salud mental y estilos de vida entre 2020 y 2022. El resultado final es un dashboard interactivo dirigido a tomadores de decisión en salud pública — funcionarios de la Secretaría de Salud, presidencias municipales y Juventudes GTO — que permite explorar la prevalencia por municipio sin necesidad de conocimientos técnicos.

---

## Dashboard

El dashboard permite:

- **Seleccionar un indicador** (Diabetes / Hipertensión / Colesterol / Depresión / Tabaquismo) y ver cómo re-rankea todos los municipios en tiempo real
- **Hacer clic en cualquier municipio** para abrir un panel lateral con su perfil completo: radar vs promedio estatal, KPIs con delta, composición demográfica
- **Seleccionar dos municipios** y compararlos lado a lado con radar, barras y tabla detallada
- Navegar entre secciones: Resumen · Municipios · Salud mental · Estilos de vida

---

## Estructura del repositorio

```
.
├── data/
│   ├── raw/
│   │   ├── 2020/   ← ENSANUT Continua COVID-19 (CSV + catálogo)
│   │   ├── 2021/   ← ENSADUL 2021 (CSV + catálogo)
│   │   └── 2022/   ← ENSADUL 2022 (CSV + catálogo)
│   └── processed/
│       ├── ensanut2020_GTO_clean.csv
│       ├── ensadul2021_GTO_clean.csv
│       ├── ensadul2022_GTO_clean.csv
│       ├── ensadul_GTO_panel_3yr.csv   ← Panel armonizado 2020–2022
│       └── ensadul_GTO_panel_2yr.csv   ← Panel 2021–2022 (incl. enf. crónicas)
│
├── notebooks/
│   ├── 01_limpieza_eda_2020.ipynb
│   ├── 02_limpieza_eda_2021.ipynb
│   ├── 03_limpieza_eda_2022.ipynb
│   └── 04_analisis_comparativo.ipynb
│
├── docs/
│   └── index.html   ← Dashboard (GitHub Pages)
│
├── outputs/
│   └── figures/
│       ├── 2020/
│       ├── 2021/
│       ├── 2022/
│       └── comparativo/
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## Fuentes de datos

| Año | Encuesta | n | Variables orig. | Dataset limpio |
|-----|----------|---|-----------------|----------------|
| 2020 | ENSANUT Continua COVID-19 | 1,035 | 114 | 1,035 × 24 |
| 2021 | ENSADUL | 1,115 | 704 | 1,115 × 74 |
| 2022 | ENSADUL | 1,227 | 572 | 1,227 × 61 |

La encuesta de 2020 fue levantada durante la pandemia y tiene un cuestionario diferente: no incluye diagnósticos de enfermedades crónicas ni escala depresiva, pero agrega preguntas sobre aceptación de vacunas y violencia doméstica durante el confinamiento.

---

## Hallazgos principales

| Indicador | 2020 | 2021 | 2022 |
|-----------|:----:|:----:|:----:|
| Tabaquismo activo | 15.5% | 17.1% | 15.1% |
| Consume alcohol (≥mensual) | 40.7% | 46.0% | 46.9% |
| Víctimas de violencia (12m) | 3.3% | 3.3% | 2.3% |
| Diabetes | — | 10.9% | 13.1% ▲ |
| Hipertensión | — | 21.3% | 20.5% ▼ |
| Colesterol alto | — | 14.8% | 16.1% ▲ |
| Score depresivo CES-D (media) | — | 10.98 | 11.02 |

Municipios con mayor índice de riesgo compuesto (2022): **Irapuato · Dolores Hidalgo · Valle de Santiago · Jaral del Progreso**

---

## Cómo reproducir el análisis

```bash
# 1. Clonar el repositorio
git clone https://github.com/alejandrommunizc/prevalencia-enfermedades-gto.git
cd prevalencia-enfermedades-gto

# 2. Crear entorno e instalar dependencias
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# 3. Ejecutar los notebooks en orden
jupyter notebook notebooks/
```

Los datos crudos deben colocarse en `data/raw/<año>/` antes de ejecutar.

---

## Stack

`Python 3.10` · `pandas` · `numpy` · `matplotlib` · `seaborn` · `scipy` · `Jupyter` · `Chart.js` · `GitHub Pages`

---

*Juventudes GTO · Programa Exportación de Talento 2024*
