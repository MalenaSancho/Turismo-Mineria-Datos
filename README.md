# Turismo y Minería de Datos — Torrevieja

Estudio de la dinámica turística residencial de **Torrevieja** (Alicante) mediante minería de datos sobre fuentes públicas (INE, SEPE, Generalitat Valenciana, Ayuntamiento, IGN, MITECO, etc.).

El trabajo se estructura en cuatro retos independientes pero encadenados que, juntos, caracterizan el modelo turístico del municipio: cuánta gente hay realmente, cuándo viene, dónde se aloja y qué presión genera sobre el territorio.

## Estructura del repositorio

```
.
├── RETOS/                  # Notebooks de análisis (uno por reto)
│   ├── RETO_1.ipynb
│   ├── RETO_2.ipynb
│   ├── RETO_3.ipynb
│   └── RETO_4.ipynb
├── DATASETS/               # Datos crudos y procesados, separados por reto
│   ├── RETO 1/
│   │   ├── DATASETS ORIGINALES/   # Fuentes en bruto (INE, móviles, censo…)
│   │   └── DATASETS MODIFICADOS/  # CSV limpios y unificados
│   ├── RETO 2/                    # CSV/XLS de paro SEPE + JSON hoteles
│   ├── RETO 3/
│   │   ├── DATASETS ORIGINALES/   # VUT, censo viviendas, alquileres…
│   │   └── DATASETS MODIFICADOS/  # vut_limpio, plazas_limpio, porcentaje_limpio
│   └── RETO 4/
│       ├── DATASETS ORIGINALES/   # Aguas, playas, alquileres, criminalidad
│       ├── DATASETS MODIFICADOS/
│       ├── Criminalidad/          # XLSX trimestrales 2020-2025
│       └── Gastos-Ingresos PDFs/  # PDFs trimestrales del Ayto. 2022-2025
└── Informe final.docx      # Memoria escrita del proyecto
```

## Los cuatro retos

### [RETO 1 — Población real del destino](RETOS/RETO_1.ipynb)

**Pregunta**: ¿Cuánta gente hay *realmente* en Torrevieja en cada momento, más allá del padrón?

Estima la **población efectiva** (empadronada + flotante) cruzando padrón INE, censo PEGV, datos de telefonía móvil del INE (turismo emisor/receptor/interno) y consumo eléctrico residencial. Genera las series limpias [poblacion_efectiva_torrevieja.csv](DATASETS/RETO%201/DATASETS%20MODIFICADOS/poblacion_efectiva_torrevieja.csv), [poblacion_flotante_base.csv](DATASETS/RETO%201/DATASETS%20MODIFICADOS/poblacion_flotante_base.csv) y los desgloses por origen ([interno_torrevieja_limpio.csv](DATASETS/RETO%201/DATASETS%20MODIFICADOS/interno_torrevieja_limpio.csv), [emisor_torrevieja_limpio.csv](DATASETS/RETO%201/DATASETS%20MODIFICADOS/emisor_torrevieja_limpio.csv), [receptor_torrevieja_limpio.csv](DATASETS/RETO%201/DATASETS%20MODIFICADOS/receptor_torrevieja_limpio.csv)) que alimentan los retos 2, 3 y 4.

### [RETO 2 — Estacionalidad](RETOS/RETO_2.ipynb)

**Pregunta**: ¿Qué tan estacional es Torrevieja y por qué?

Análisis temporal del **paro registrado** (SEPE, 2019-2026) y del **turismo nacional/extranjero** (poblacion_efectiva_torrevieja del RETO 1). Cuantifica la estacionalidad mediante coeficiente de variación, ratio pico/valle, correlación de Pearson paro-turismo y descomposición por sectores económicos (Servicios destaca como el sector estacionalmente sensible). Cierra cruzando la demanda con la oferta de alojamiento reglada (hoteles + VUT) para mostrar el **déficit estructural de plazas** que solo puede explicarse por segunda residencia.

### [RETO 3 — Viviendas de Uso Turístico (VUT)](RETOS/RETO_3.ipynb)

**Pregunta**: ¿Qué peso tienen las VUT en el modelo de alojamiento de Torrevieja?

Caracteriza el **parque de VUT** del municipio: dimensión, evolución temporal, distribución espacial y comparación con la oferta hotelera. Trabaja con [vut_limpio.csv](DATASETS/RETO%203/DATASETS%20MODIFICADOS/vut_limpio.csv) (registro de inscripciones VUT con dirección, plazas y referencia catastral), [plazas_limpio.csv](DATASETS/RETO%203/DATASETS%20MODIFICADOS/plazas_limpio.csv) (plazas y viviendas turísticas por mes) y [porcentaje_limpio.csv](DATASETS/RETO%203/DATASETS%20MODIFICADOS/porcentaje_limpio.csv) (% de VUT sobre viviendas censadas). Confirma que el alojamiento dominante en Torrevieja es residencial, no hotelero.

### [RETO 4 — Sostenibilidad ambiental y cohesión social](RETOS/RETO_4.ipynb)

**Pregunta**: ¿Hay evidencia de presión ambiental o social asociada al turismo?

Construye **indicadores indirectos** de presión turística a partir de variables ambientales (calidad de aguas subterráneas y de baño, lagunas), económicas (precios de alquiler y vivienda, gastos e ingresos municipales) y sociales (criminalidad trimestral 2020-2025). Incluye una sección crítica sobre los **datos no disponibles** (registros históricos SINAC de tratamientos de agua potable, residuos urbanos a nivel municipal) que limitan el análisis.

## Datasets principales

| Reto | Dataset                                     | Fuente           | Granularidad          |
| ---- | ------------------------------------------- | ---------------- | --------------------- |
| 1    | Censo INE/PEGV                              | INE, GVA         | Anual                 |
| 1    | Telefonía móvil receptora/emisora/interna | INE              | Mensual               |
| 1    | Viviendas por consumo eléctrico            | INE 2021         | Anual                 |
| 2    | Paro registrado                             | SEPE             | Mensual               |
| 2    | Histórico de hoteles (altas/bajas)         | GVA              | Diario                |
| 3    | Registro VUT                                | GVA              | Diario (inscripción) |
| 3    | Plazas y viviendas turísticas              | GVA              | Mensual               |
| 3    | Precios vivienda y alquiler                 | INE / Idealista  | Mensual               |
| 4    | Aguas subterráneas                         | MITECO           | Variable              |
| 4    | Calidad aguas de playa                      | MSCBS            | Por temporada         |
| 4    | Criminalidad                                | Min. Interior    | Trimestral            |
| 4    | Gastos-Ingresos municipales                 | Ayto. Torrevieja | Trimestral (PDF)      |

Los datasets en `DATASETS ORIGINALES/` son los descargados sin modificar; los de `DATASETS MODIFICADOS/` son las versiones tratadas que cargan los notebooks.

## Cómo ejecutar

Requisitos: Python 3.10+ y Jupyter.

```bash
pip install pandas matplotlib seaborn xlrd openpyxl scipy
jupyter notebook RETOS/
```

Cada notebook se ejecuta de forma independiente y carga los datasets con rutas relativas desde la raíz del repositorio. Si abres un notebook, asegúrate de que el directorio de trabajo de Jupyter es la raíz del proyecto, no la carpeta `RETOS/`.

Orden recomendado de lectura: **1 → 2 → 3 → 4**. El RETO 2 reutiliza salidas del RETO 1 (`poblacion_flotante_base.csv`, `interno_torrevieja_limpio.csv`) y del RETO 3 (`plazas_limpio.csv`).

## Documento final

[Informe final.docx](Informe%20final.docx) recoge la memoria escrita con metodología, resultados consolidados y conclusiones de los cuatro retos.

## AUTORES

* Juan Francisco Correas Díaz
* Magdalena Sancho Docón
* Itsaso Ariztimuño Cenoz
* Jimena Milla Moreno
