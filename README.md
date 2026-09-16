# Proyecto 1 - Bodega de Datos, ETL y Análisis Descriptivo

## 👥 Integrantes
* Juan Camilo Velez Ospina 2510206-3743
* Andrés Felipe Salcedo Buitrago 2359304-3743
* [Estudiante 3]
* [Estudiante 4]

---

## 🚀 Instrucciones de Configuración y Ejecución

Por buenas prácticas de almacenamiento y peso masivo, **los archivos de datos crudos no están incluidos en este repositorio**.

### 1. Preparación de los Datos
1. Descargue los microdatos mensuales desde el enlace oficial del DANE:  
   🔗 [Descargar Microdatos GEIH 2026](https://microdatos.dane.gov.co/index.php/catalog/900/get-microdata)
2. Descomprima el archivo descargado. **Conserve únicamente la carpeta con archivos `.csv`** (puede eliminar las carpetas `.dta` y `.sav`).
3. Mueva los archivos CSV directamente a la raíz del proyecto.

### 2. Variables de Entorno
Cree un archivo local `.env` en la raíz del proyecto configurando sus credenciales de PostgreSQL:
```text
DATABASE_URL=postgresql://usuario:contraseña@localhost:5432/nombre_base_datos
```

### 3. Entorno Virtual e Instalación
Ejecute en su terminal desde la raíz del proyecto para aislar las dependencias:

```bash
# Crear y activar entorno virtual
python -m venv env

# Activar en Windows:
.\env\Scripts\activate
# Activar en Linux/macOS:
source env/bin/activate

# Instalar librerías
pip install -r requirements.txt
```

### 4. Ejecución del Pipeline
Abra su editor de código, **seleccione el kernel de Jupyter apuntando al entorno virtual (`env`)** recién creado y ejecute en orden mediante *Restart & Run All*:
1. `entrega/fase_b_etl.ipynb` (Carga los CSV en PostgreSQL).
2. `entrega/fase_c_sql.ipynb` (Ejecuta las consultas analíticas).
3. `entrega/fase_d_visualizaciones.ipynb` (Genera los reportes gráficos).

---

## 📂 Estructura del Entregable
* **`entrega/fase_a_diseño.pdf`** (Diagrama estrella y justificación).
* **`entrega/fase_b_etl.ipynb`** (Pipeline de extracción, limpieza y carga).
* **`entrega/fase_c_sql.ipynb`** (6 consultas analíticas avanzadas).
* **`entrega/fase_d_visualizaciones.ipynb`** (8 gráficos con insights).
* **`entrega/informe.pdf`** (Informe final de resultados).
* **`.env.example`** y **`requirements.txt`**.
