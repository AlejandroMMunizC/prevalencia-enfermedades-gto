# Prevalencia de Enfermedades Crónicas en Guanajuato

Análisis longitudinal de la **Encuesta de Salud del Adulto (ENSADUL)** para el estado de Guanajuato en los años 2020, 2021 y 2022. El objetivo es identificar y comparar tendencias en enfermedades crónicas, salud mental, estilos de vida y acceso a servicios de salud, y exponer esos hallazgos en un dashboard interactivo.

> Proyecto desarrollado para **Juventudes GTO** como parte del programa **Exportación de Talento 2024**.

---

## Estructura del proyecto

```
.
├── data/
│   ├── raw/
│   │   ├── 2020/          ← Archivos originales ENSADUL 2020 (CSV + catálogo)
│   │   ├── 2021/          ← Archivos originales ENSADUL 2021 (CSV + catálogo)
│   │   └── 2022/          ← Archivos originales ENSADUL 2022 (CSV + catálogo)
│   └── processed/
│       ├── ensadul2020_GTO_clean.csv     ← Dataset limpio 2020  (pendiente)
│       ├── ensadul2021_GTO_clean.csv     ← Dataset limpio 2021  (pendiente)
│       ├── ensadul2022_GTO_clean.csv     ← Dataset limpio 2022  ✅
│       └── ensadul_GTO_panel.csv         ← Dataset combinado multi-año  (pendiente)
│
├── notebooks/
│   ├── 01_limpieza_eda_2020.ipynb        ← Limpieza + EDA ENSADUL 2020  (pendiente)
│   ├── 02_limpieza_eda_2021.ipynb        ← Limpieza + EDA ENSADUL 2021  (pendiente)
│   ├── 03_limpieza_eda_2022.ipynb        ← Limpieza + EDA ENSADUL 2022  ✅
│   └── 04_analisis_comparativo.ipynb     ← Análisis longitudinal 2020–2022  (pendiente)
│
├── outputs/
│   └── figures/
│       ├── 2020/          ← Gráficas EDA 2020  (pendiente)
│       ├── 2021/          ← Gráficas EDA 2021  (pendiente)
│       ├── 2022/          ← Gráficas EDA 2022  ✅
│       └── comparativo/   ← Gráficas del análisis longitudinal  (pendiente)
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
| 1 | Limpieza de datos + EDA — ENSADUL 2022 | ✅ Completado |
| 2 | Limpieza de datos + EDA — ENSADUL 2021 | 🔲 Pendiente |
| 3 | Limpieza de datos + EDA — ENSADUL 2020 | 🔲 Pendiente |
| 4 | Análisis comparativo longitudinal 2020–2022 | 🔲 Pendiente |
| 5 | Dashboard interactivo | 🔲 Pendiente |

---

## Dataset: ENSADUL 2022 — Guanajuato

- **Fuente:** Encuesta de Salud del Adulto, edición 2022
- **Cobertura:** Estado de Guanajuato (20 municipios)
- **Muestra original:** 1,227 personas entrevistadas, 572 variables
- **Dataset limpio:** 1,227 filas × 61 columnas, 0 valores nulos

### Temas cubiertos

- Demografía y características del hogar (edad, sexo, municipio, urbanidad)
- Enfermedades crónicas (diabetes, hipertensión, enfermedades cardiovasculares, renales)
- Salud mental (escala CES-D de síntomas depresivos, ideación suicida)
- Estilos de vida (tabaquismo, consumo de alcohol)
- Antecedentes familiares de enfermedades crónicas
- Discapacidades y dificultades funcionales
- Acceso y detección en servicios de salud
- Percepción de imagen corporal y cambio de peso

### Decisiones de imputación de nulos

| Variable | Nulos | Estrategia |
|----------|-------|------------|
| A1305 — Tabaco en el pasado | 187 (15.2%) | Cat. 0 = "Actualmente fuma" (skip logic) |
| A1001G — Detección de diabetes | 161 (13.1%) | Moda = 2 (No) |
| Antecedentes hermano(a) ×3 | 134 c/u (10.9%) | 2 = No (sin hermanos, skip logic) |
| Unidad primaria de muestreo | 76 (6.2%) | Eliminada (variable administrativa) |
| A1404B — Dificultad para oír | 15 (1.2%) | Moda = 1 (Sin dificultad) |

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

# 3. Ejecutar el notebook
jupyter notebook notebooks/03_limpieza_eda_2022.ipynb
```

> Los archivos de datos crudos deben colocarse en su carpeta `data/raw/<año>/` antes de ejecutar.

---

## Tecnologías

- **Python 3.10+** — pandas, numpy, matplotlib, seaborn
- **Jupyter Notebooks** — análisis exploratorio y documentación
- **Dashboard** *(pendiente)* — por definir (Streamlit / Power BI / Tableau)

---

*Proyecto realizado para Juventudes GTO · Programa Exportación de Talento 2024*
