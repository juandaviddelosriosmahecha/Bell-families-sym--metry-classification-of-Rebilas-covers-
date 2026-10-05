# Bell-families-sym--metry-classification-of-Rebilas-covers-

Código fuente, datos de órbitas y análisis del politopo para la **clasificación por
simetría de las desigualdades tipo Bell** que surgen en la construcción geométrica
de Rébilas.

El repositorio contiene un único notebook de Python que **demuestra numérica y
analíticamente** todos los resultados del artículo asociado (*Bell families — v11*):
clasifica las coberturas (*covers*) de Rébilas en familias de equivalencia bajo el
grupo de simetría, identifica cuáles son facetas del politopo local, las proyecta al
espacio de correladores (formas CHSH firmadas) y verifica sus violaciones cuánticas.

## ¿Qué es esto?

En el enfoque geométrico de Rébilas, las desigualdades tipo Bell para un escenario
bipartito de 2 ajustes y 2 resultados por parte (CHSH / Eberhard / CH) se describen
mediante una **rejilla de 16 celdas**. Cada celda cuenta un suceso conjunto
`n^{s_A s_B}(x, y)` (resultados `±` de Alice y Bob para los ajustes `a/a'`, `b/b'`).
Una **cobertura de Rébilas** elige una celda "círculo" (lado izquierdo de la
desigualdad) y un conjunto de celdas "X" (lado derecho) de modo que cada rectángulo
local que pasa por el círculo quede cubierto.

El notebook:

- Construye la rejilla, los **rectángulos locales** y la condición de cobertura.
- Genera el **grupo de simetría** `G = ⟨σ_A, σ_B, φ_A, φ_B, τ⟩` de orden 32
  (`G ≅ (ℤ₂)⁴ ⋊ ℤ₂`) que actúa sobre las 16 celdas.
- Enumera todas las coberturas válidas con `k = 3` marcas X (544 en total) y las
  clasifica en **18 familias** (órbitas) por canonicalización bajo `G`.
- Construye el **politopo local** a partir de los 16 vértices deterministas,
  prueba que su dimensión es 8 (vía `PᵀP = 16·I₈`) y determina qué familias son
  **facetas** (criterio `afdim(S) = 7`): resultan **4 facetas** (F1–F4) y 14 no-facetas.
- Proyecta las facetas al **espacio de correladores**, obteniendo las formas CHSH
  firmadas, y verifica numéricamente la **violación cuántica**
  `V_Q = (√2 − 1)/2 ≈ 0.207` para F2/F3/F4 y `V_Q = 0` para F1.
- Reproduce los lemas y teoremas del paper (bijecciones admisibles, estabilizadores,
  equivalencia Eberhard↔CHSH vía `g* = φ_A φ_B τ`, argumento de "mala estrategia",
  valores singulares de las matrices de saturación, sector `k = 4`).
- Exporta tablas, un resumen JSON y la **Figura 1** (las cuatro familias faceta).

## Contenido del repositorio

```
.
├── README.md
└── Bell_families_v11_sym_metry_classification_of_Rebilas_covers_—_source_code,_orbit_tables,_and_saturation_matrices.ipynb
```

El notebook tiene una **única celda de código** autocontenida (~1200 líneas) que
ejecuta todo el pipeline de principio a fin e imprime cada resultado con su
verificación (`✓`).

## Requisitos

- **Python 3.8+**
- Paquetes: `numpy`, `scipy`, `pandas`, `tabulate`, `matplotlib`
- Para abrir/ejecutar el notebook: `jupyter` (o Google Colab)

Instalación de dependencias:

```bash
pip install numpy scipy pandas tabulate matplotlib jupyter
```

## Cómo ejecutarlo

### Opción A — Jupyter

```bash
jupyter notebook "Bell_families_v11_sym_metry_classification_of_Rebilas_covers_—_source_code,_orbit_tables,_and_saturation_matrices.ipynb"
```

Luego ejecuta la celda (Shift+Enter). Toda la salida (tablas, verificaciones y la
Figura 1) se genera en esa única ejecución.

### Opción B — Como script

Puedes extraer y ejecutar la celda sin interfaz de notebook:

```bash
jupyter nbconvert --to script "Bell_families_v11_...ipynb" --stdout | python3 -
```

> **Nota sobre la ruta de salida.** El notebook escribe los archivos generados en
> `OUTPUT_DIR = "/content/bell_output"`, una ruta propia de **Google Colab**. Si lo
> ejecutas en local, edita esa variable al inicio de la celda (por ejemplo
> `OUTPUT_DIR = "./bell_output"`) para que los resultados se guarden en tu directorio
> de trabajo.

## Archivos que genera

En `OUTPUT_DIR` se crean:

| Archivo | Descripción |
|---------|-------------|
| `familias_bell_k3_v11.csv` | Tabla de las 18 familias: representante canónico, tamaño de órbita, estabilizador, nº de vértices saturados, `afdim`, si es faceta y violación cuántica. |
| `resultados_v11.json` | Resumen con metadatos (orden del grupo, generadores, dimensión del politopo, conteos `k=3`/`k=4`, nº de facetas, `V_Q` exacto) y la lista de familias. |
| `fig1_grillas_facetas.pdf` / `.png` | Figura 1: las rejillas de Rébilas de las cuatro familias faceta (F1–F4) con sus rectángulos locales. |

## Resultados principales que reproduce

- **Grupo de simetría**: `|G| = 32`, con `G ≅ (ℤ₂)⁴ ⋊ ℤ₂`.
- **Dimensión del politopo local**: `dim(L) = 8` (prueba vía `PᵀP = 16·I₈`).
- **Coberturas `k=3`**: 544 válidas → **18 familias** (`2×16 + 16×32 = 544`).
- **Facetas**: 4 de 18 (F1 positividad, F2 CH, F3 CHSH firmada, F4 Eberhard/CHSH).
- **Proyecciones a correladores**: F2, F3 y F4 dan tres de las cuatro formas CHSH
  firmadas.
- **Violaciones cuánticas**: `V_Q(F2) = V_Q(F3) = V_Q(F4) = (√2 − 1)/2 ≈ 0.207`
  y `V_Q(F1) = 0`.

## Cita

Si usas este código o sus datos, cita el artículo asociado a la construcción
geométrica de Rébilas y la clasificación por simetría de las familias de Bell.
