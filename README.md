# Prevalencia de Enfermedades Crónicas en Guanajuato

> Análisis longitudinal de encuestas de salud del adulto en Guanajuato · 2020–2022  
> Proyecto desarrollado para **Juventudes GTO** como parte del programa **Exportación de Talento 2024**

**[→ Ver dashboard interactivo](https://alejandrommunizc.github.io/prevalencia-enfermedades-gto/)**

---

## ¿De qué trata este proyecto?

Se procesaron tres ediciones de encuestas nacionales de salud levantadas en el estado de Guanajuato, enriquecidas con indicadores contextuales del **Observatorio Guanajuato 2.0 (IPLANEG)**, para identificar tendencias en enfermedades crónicas, salud mental y estilos de vida entre 2020 y 2022. El resultado final es un dashboard interactivo dirigido a tomadores de decisión en salud pública — funcionarios de la Secretaría de Salud, presidencias municipales y Juventudes GTO — que permite explorar la prevalencia, la mortalidad y la prioridad de intervención por municipio sin necesidad de conocimientos técnicos.

---

## Dashboard

El dashboard integra datos de encuesta con mortalidad, pobreza y capacidad hospitalaria por municipio. Permite:

- **Seleccionar un indicador** (Diabetes / Hipertensión / Colesterol / Depresión / Tabaquismo) para re-rankear todos los municipios en tiempo real
- **Hacer clic en cualquier municipio** para abrir un panel lateral con su perfil completo: radar vs promedio estatal, KPIs con delta, mortalidad, pobreza e índice de prioridad
- **Seleccionar dos municipios** y compararlos lado a lado con radar, barras y tabla detallada
- Navegar entre secciones: Resumen · Municipios · **Priorización** · Salud mental · Estilos de vida

La pestaña **Priorización** es el corazón del dashboard para tomadores de decisión: muestra el índice compuesto de intervención por municipio, la brecha de detección (alta mortalidad vs baja prevalencia encuestada), y la relación entre pobreza y carga de enfermedad.

---

## Estructura del repositorio

```
.
├── data/
│   ├── raw/
│   │   ├── 2020/          ← ENSANUT Continua COVID-19 (CSV + catálogo)
│   │   ├── 2021/          ← ENSADUL 2021 (CSV + catálogo)
│   │   ├── 2022/          ← ENSADUL 2022 (CSV + catálogo)
│   │   └── Observatorio/  ← Observatorio GTO / IPLANEG (CSV)
│   └── processed/
│       ├── ensanut2020_GTO_clean.csv
│       ├── ensadul2021_GTO_clean.csv
│       ├── ensadul2022_GTO_clean.csv
│       ├── observatorio_GTO_clean.csv      ← Indicadores IPLANEG limpios
│       ├── municipios_GTO_panel.csv        ← Panel municipal ENSADUL + IPLANEG
│       ├── ensadul_GTO_panel_3yr.csv       ← Panel armonizado 2020–2022
│       └── ensadul_GTO_panel_2yr.csv       ← Panel 2021–2022 (incl. enf. crónicas)
│
├── notebooks/
│   ├── 01_limpieza_eda_2020.ipynb          ← Limpieza + EDA ENSANUT 2020
│   ├── 02_limpieza_eda_2021.ipynb          ← Limpieza + EDA ENSADUL 2021
│   ├── 03_limpieza_eda_2022.ipynb          ← Limpieza + EDA ENSADUL 2022
│   ├── 04_analisis_comparativo.ipynb       ← Análisis longitudinal 2020–2022
│   └── 05_analisis_observatorio.ipynb      ← Contexto municipal IPLANEG
│
├── docs/
│   └── index.html   ← Dashboard (GitHub Pages)
│
├── outputs/
│   └── figures/
│       ├── 2020/
│       ├── 2021/
│       ├── 2022/
│       └── comparativo/   ← Incluye brecha de detección y matriz de priorización
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## Fuentes de datos

| Fuente | Año(s) | n / Cobertura | Contenido principal |
|--------|--------|---------------|---------------------|
| ENSANUT Continua COVID-19 | 2020 | 1,035 adultos | Vacunas, tabaco, alcohol, violencia |
| ENSADUL | 2021 | 1,115 adultos | Enf. crónicas, salud mental, estilos de vida |
| ENSADUL | 2022 | 1,227 adultos | Enf. crónicas, salud mental, estilos de vida |
| Observatorio GTO / IPLANEG | 2020–2022 | 46 municipios | Mortalidad, marginación, pobreza, capacidad hospitalaria |

La encuesta de 2020 fue levantada durante la pandemia con un cuestionario diferente (sin diagnósticos de enfermedades crónicas ni escala depresiva, pero con preguntas sobre vacunas y violencia en el confinamiento).

---

## Hallazgos principales

### Tendencias 2020–2022 (ENSADUL / ENSANUT)

| Indicador | 2020 | 2021 | 2022 |
|-----------|:----:|:----:|:----:|
| Tabaquismo activo | 15.5% | 17.1% | 15.1% |
| Consume alcohol (≥mensual) | 40.7% | 46.0% | 46.9% |
| Víctimas de violencia (12m) | 3.3% | 3.3% | 2.3% |
| Diabetes | — | 10.9% | 13.1% ▲ |
| Hipertensión | — | 21.3% | 20.5% ▼ |
| Colesterol alto | — | 14.8% | 16.1% ▲ |
| Score depresivo CES-D (media) | — | 10.98 | 11.02 |

### Priorización municipal (ENSADUL 2022 + IPLANEG)

Índice compuesto: 30% carga de enfermedad · 30% mortalidad · 25% pobreza · 15% capacidad hospitalaria

| Municipio | Prioridad | Diabetes | HTA | Mortalidad | Pobreza |
|-----------|:---------:|:--------:|:---:|:----------:|:-------:|
| Jaral del Progreso | 78/100 🔴 | 19.4% | 29.0% | Alta | 55.0% |
| Pénjamo | 74/100 🔴 | 18.2% | 20.5% | Alta | 51.1% |
| Valle de Santiago | 73/100 🔴 | 5.6% | 36.1% | Alta | 47.0% |
| Comonfort | 72/100 🔴 | 12.9% | 19.4% | Muy alta | 52.1% |
| Dolores Hidalgo | 72/100 🔴 | 17.3% | 28.4% | Media | 53.1% |

> **Brecha de detección:** Huanímaro y Valle de Santiago muestran baja prevalencia encuestada pero alta mortalidad registrada — indicador de casos sin diagnóstico que requieren programas activos de detección.

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

Los datos crudos deben colocarse en `data/raw/<año>/` y `data/raw/Observatorio/` antes de ejecutar.

---

## Stack

`Python 3.10` · `pandas` · `numpy` · `matplotlib` · `seaborn` · `scipy` · `Jupyter` · `Chart.js` · `GitHub Pages`

---

*Juventudes GTO · Programa Exportación de Talento 2024*
