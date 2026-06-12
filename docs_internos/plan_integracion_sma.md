# Plan de integración: análisis intra-municipal San Miguel de Allende (COMUDE)

## 1. Por qué este análisis es distinto a los anteriores

Los notebooks 01-05 trabajan a nivel **municipio** (20 municipios de la encuesta ENSADUL, 46 del Observatorio
IPLANEG). Este nuevo componente **abre uno de esos municipios** — San Miguel de Allende (clave 11003) — para
encontrar dónde, *dentro* del municipio, conviene priorizar programas de activación física. Es una capa nueva,
no un reemplazo: el dashboard y el reporte general seguirán hablando a nivel estatal/municipal, y este análisis
se usa como **anexo focalizado** para la propuesta a COMUDE San Miguel de Allende.

## 2. Fuentes y su rol

| Fuente | Nivel | Rol en el análisis |
|---|---|---|
| `DA_EC_SIS_2023.csv` (DGIS/SIS) | 22 unidades de salud (CLUES) | Carga de enfermedad crónica "en control" (diabetes, HTA, obesidad, dislipidemia, síndrome metabólico) — proxy de necesidad de intervención |
| `iml_2020.csv` (CONAPO) | 331 localidades | Marginación + población — para identificar zonas rurales vulnerables y calcular tasas |
| `imuc_2020.csv` (CONAPO) | 121 colonias de la cabecera | Marginación urbana — para identificar colonias prioritarias dentro de la cabecera, donde no hay desagregación de salud por colonia |

## 3. Crosswalk (pieza clave)

21 de las 22 unidades de salud de SMA son UMAPS/ESI/Caravanas cuyo nombre corresponde directamente a una
localidad de `iml_2020` (ej. `ALCOCER-UMAPS` → *Alcocer*). La unidad #22 (`SAN MIGUEL DE ALLENDE-CAISES`) atiende
toda la cabecera urbana, por lo que **no se puede desagregar por colonia** — para esa zona se usa únicamente
`imuc_2020` (marginación urbana por colonia), sin cruzar con datos de salud.

Esto da dos rankings paralelos, no uno solo:

- **Ranking rural** (21 localidades): combina tasa de control de enfermedad crónica (por 100 hab.) + marginación
  CONAPO → índice de prioridad para activación física (50/50).
- **Ranking urbano** (121 colonias de la cabecera): ordenado solo por marginación urbana relativa (z-score), como
  proxy de vulnerabilidad donde la salud no se puede desagregar.

## 4. Resultado del notebook 06

- `data/processed/sma_localidades_panel.csv` — 21 localidades rurales con CLUES, marginación, carga de
  enfermedad, índice de prioridad (`prioridad_activacion`, 0-100).
- `data/processed/sma_colonias_panel.csv` — 121 colonias de la cabecera con marginación urbana e índice z.
- Gráficas en `reports/figures/`: distribución de marginación rural y urbana, y top 10 localidades rurales
  prioritarias.

## 5. Limitaciones documentadas (importantes para la propuesta a COMUDE)

1. **Desfase temporal**: salud es de 2023, población/marginación es de 2020. Las tasas son aproximadas.
2. **Cabecera sin desagregación de salud**: el CAISES atiende a toda la zona urbana como una sola unidad, así
   que el ranking urbano se basa solo en marginación, no en datos de enfermedad por colonia.
3. **Localidades muy pequeñas excluidas** (92 de 331, población < 50) del ranking rural — no representan un
   tamaño suficiente para justificar un programa dedicado, pero se mantienen en el dataset completo.
4. **Columnas auxiliares de `DA_EC_SIS_2023`** (`HBA*`, `PDM*`, `FRS*`, `PMA*`, `RUN01`) no se usaron por no tener
   diccionario de variables confirmado — quedan documentadas para uso futuro si se consigue el catálogo oficial
   del SIS.
5. **Tasas de control "imposibles" (>100 por 100 hab.)**: algunas localidades, notablemente *La Puerta*
   (160.6 por 100 hab.), muestran tasas que superan matemáticamente el 100%. Esto ocurre porque las UMAPS
   rurales suelen atender pacientes de **varias localidades vecinas**, no solo la que les da nombre — el
   numerador (pacientes en control en esa unidad) no corresponde 1:1 con el denominador (población de esa
   localidad únicamente). Por esto, para el reporte y la propuesta a COMUDE se recomienda citar el **índice de
   prioridad** (`prioridad_activacion`) en lugar de la tasa cruda como dato principal — sigue siendo válido
   como ranking relativo, aunque la tasa absoluta de algunas localidades esté inflada por este efecto de "zona
   de influencia" de la unidad de salud.

## 6. Próximos pasos sugeridos

1. **Dashboard**: agregar una sub-vista "San Miguel de Allende" con los dos rankings (localidades rurales y
   colonias urbanas) — puede ser una pestaña nueva o un modal de detalle dentro de la ficha de SMA.
2. **Propuesta COMUDE**: documento corto (1-2 páginas) con el top 5 de localidades rurales + top 5 de colonias
   urbanas, mapas/gráficas de este notebook, y una recomendación concreta (ej. "llevar el programa X a estas 5
   localidades en los próximos 6 meses").
3. **Validar crosswalk con alguien de COMUDE/jurisdicción sanitaria**: confirmar que las 21 unidades de salud
   efectivamente corresponden a esas localidades sobre el terreno (el match es por nombre, razonable pero no
   verificado institucionalmente).
4. Si se consigue el catálogo de variables del SIS, reincorporar `HBA*`/`FRS*`/`PMA*` para enriquecer el perfil
   de riesgo por unidad de salud.
