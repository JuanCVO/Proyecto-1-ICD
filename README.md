# Proyecto GEIH: bodega de datos, análisis y modelado

Trabajo de Introducción a la Ciencia de Datos (Universidad del Valle) sobre la Gran Encuesta Integrada de Hogares (GEIH) del DANE, periodo junio de 2026.

* **Proyecto 1** (`entrega 1/`): bodega de datos en PostgreSQL (esquema estrella), ETL, consultas SQL y visualizaciones.
* **Proyecto 2 y 3** (`entrega 2/`): análisis exploratorio, limpieza y normalización, modelos predictivos y segmentación. Lee la bodega del Proyecto 1 y predice el ingreso laboral de los ocupados.

## Integrantes
* Juan Camilo Velez Ospina 2510206-3743
* Andrés Felipe Salcedo Buitrago 2359304-3743
* Geraldine Florez Rico 2269476-3743
* Daniela Orrego Alfonso 2510208-3743

---

## Cómo correr el proyecto

### 1. Entorno virtual e instalación
Desde la raíz del proyecto:

```powershell
# Windows (PowerShell)
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

```bash
# Linux / macOS
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Si PowerShell no deja activar el entorno, ejecute una vez `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned`.

### 2. Variables de entorno (`.env`)
Copie `.env.example` como `.env` en la raíz y escriba la cadena de conexión de la base de datos (Neon o PostgreSQL local):

```text
DATABASE_URL=postgresql://usuario:contraseña@host/nombre_base_datos?sslmode=require
```

Los notebooks aceptan el prefijo `postgresql://` y lo convierten solos a `postgresql+psycopg2://`.

### 3. Proyecto 2 y 3 (`entrega 2/`)
La bodega ya debe estar cargada (paso del Proyecto 1). No hacen falta los CSV. En VS Code abra cada notebook, elija el kernel del `.venv` y use *Restart & Run All*, en este orden:

1. `fase_a_eda.ipynb`: análisis exploratorio (independiente de las demás).
2. `fase_b_limpieza.ipynb`: limpieza y normalización. Genera `datos_limpios.parquet` junto al notebook.
3. `fase_c_modelos.ipynb`: modelos de regresión y segmentación con K-Means. Lee `datos_limpios.parquet`.

### 4. Proyecto 1 (`entrega 1/`), solo si hay que volver a cargar la bodega
Este paso necesita los datos crudos, que no están en el repositorio:

1. Descargue los microdatos mensuales del DANE: [Microdatos GEIH](https://microdatos.dane.gov.co/index.php/catalog/900/get-microdata).
2. Descomprima y conserve solo los archivos `.csv` (puede borrar las carpetas `.dta` y `.sav`).
3. Muévalos a la raíz del proyecto, o ajuste `DATA_DIR` en `fase_b_etl.ipynb`.
4. Ejecute en orden `fase_b_etl.ipynb` (carga la bodega), `fase_c_sql.ipynb` (consultas) y `fase_d_visualizaciones.ipynb` (gráficos).

---

## Qué NO se sube al repositorio
El `.gitignore` deja fuera estos archivos, y no deben forzarse con `git add -f`:

| Archivo | Por qué |
|---|---|
| `.env` | Tiene la contraseña de la base de datos. Solo se comparte `.env.example`, sin credenciales. |
| `*.csv` / `*.CSV` | Microdatos crudos de la GEIH: pesan mucho y pueden ser sensibles. |
| `*.parquet` | Los genera la Fase B; se regeneran al ejecutarla. |
| `*.png`, `*.jpg` y `geih_2026_*.csv` | Figuras y tablas que generan los notebooks; se regeneran al ejecutarlos. |
| `.venv/`, `__pycache__/`, `.ipynb_checkpoints/` | Entorno y archivos temporales. |

Los PDF de los informes sí se versionan. El zip de entrega del Proyecto 2 y 3 se arma desde la carpeta local, que sí tiene el parquet y las figuras.

---

## Estructura

```text
entrega 1/                      Proyecto 1
  fase_a_diseño.pdf             Diseño de la bodega (esquema estrella)
  fase_b_etl.ipynb              ETL: carga de los CSV a PostgreSQL
  fase_c_sql.ipynb              Consultas analíticas
  fase_d_visualizaciones.ipynb  Gráficos con insights
  Informe.pdf                   Informe del Proyecto 1
entrega 2/                      Proyecto 2 y 3
  fase_a_eda.ipynb              Análisis exploratorio
  fase_b_limpieza.ipynb         Limpieza y normalización
  fase_c_modelos.ipynb          Modelos predictivos y segmentación
  Fase_A_Hallazgos.pdf          Los 3 hallazgos más importantes del EDA
  Fase B ... .pdf               Pasos y decisiones de la limpieza
  Fase C ... .pdf               Análisis y justificación del modelo elegido
  informe_p2p3.pdf              Informe final
  presentacion.pdf              Presentación oral
.env.example                    Plantilla de variables de entorno
requirements.txt                Dependencias
```
