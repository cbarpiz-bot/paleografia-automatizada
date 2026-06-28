# Paleografía automatizada: transcripción e indexación de registros parroquiales

**TFM — Máster en Ciencia de Datos Aplicada a las Ciencias Sociales · Universidad de Granada**  
Alumna: Clara Barriuso Pizarro · Tutor: Miguel Molina Solana

---

## Descripción

Repositorio con el código reproducible del flujo de trabajo desarrollado para la transcripción automática y el análisis sociodemográfico del archivo parroquial de Losar de la Vera (Cáceres), correspondiente al periodo 1807–1874.

El proyecto combina modelos de lenguaje multimodal (GPT-4o y Gemini 2.5 Flash) con análisis estadístico histórico-demográfico. Los resultados incluyen una base de datos con 5.257 registros de bautismo y análisis de natalidad, apellidos, transmisión onomástica y movilidad geográfica.

---

## Estructura del repositorio

```
├── 01_preprocesamiento.ipynb         # Detección de duplicados y mejora de imagen
├── 02_transcripcion_openai.ipynb     # Transcripción y extracción con GPT-4o
├── 03_transcripcion_gemini.ipynb     # Transcripción y extracción con Gemini 2.5 Flash
├── 04_validador_consistencia.ipynb   # Evaluador de consistencia cruzada (ICG)
├── 05_estadisticas.ipynb             # Análisis estadístico y visualizaciones
├── requirements.txt                  # Dependencias Python
├── REPRODUCIR.txt                    # Instrucciones de ejecución paso a paso
└── .gitignore
```

### Orden de ejecución recomendado

1. `01_preprocesamiento.ipynb` *(opcional — ver nota en el notebook)*
2. `02_transcripcion_openai.ipynb`
3. `03_transcripcion_gemini.ipynb`
4. `04_validador_consistencia.ipynb`
5. `05_estadisticas.ipynb`

---

## Requisitos

- Python 3.8+
- Cuenta de Google (para ejecutar en Google Colab y acceder a Drive)
- API key de OpenAI (para el notebook 02)
- API key de Google Gemini (para los notebooks 03 y 04)

---

## Instalación

### Ejecución en Google Colab (recomendado)

Abre cada notebook directamente desde este repositorio en Colab. En la primera celda ejecutable se monta Google Drive:

```python
from google.colab import drive
drive.mount('/content/drive')
```

Las dependencias se instalan automáticamente en cada notebook con `pip install`.

### Ejecución local

```bash
git clone <URL_DEL_REPO>
cd <repo>
python -m venv .venv
source .venv/bin/activate       # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

---

## Configuración

### Rutas

En cada notebook hay una celda de configuración con la variable `DRIVE_MOUNT` y `DB_PATH`. Ajusta la ruta a la carpeta de tu Drive donde estén almacenadas las imágenes y la base de datos:

```python
DB_PATH = os.path.join(DRIVE_MOUNT, 'MyDrive', '<TU_CARPETA>', 'bautismos_losar_vera.db')
```

### Claves API

Las claves se solicitan de forma segura mediante `getpass.getpass()` y no se almacenan en el notebook. Tenlas disponibles antes de ejecutar las celdas de configuración de API.

---

## Notas de reproducibilidad

- Los nombres de las funciones principales (`transcribir_imagen`, `segmentar_actas`, `extraer_datos`, `guardar_en_bd`) son consistentes entre notebooks; no los modifiques si quieres mantener la compatibilidad.
- El notebook `01_preprocesamiento` es opcional: el corpus ya fue sometido a un tratamiento previo durante el escaneado y se decidió usar las imágenes originales directamente. Se incluye por reproducibilidad del proceso de exploración.
- Los resultados pueden variar ligeramente entre ejecuciones por la naturaleza estocástica de los modelos de lenguaje.

---

## Datos

El corpus documental consiste en 1.362 imágenes digitalizadas del archivo parroquial de Losar de la Vera, cedidas para este estudio. El fondo original pertenece al Archivo Histórico de la Diócesis de Plasencia, donde los registros son accesibles para consulta pública.

Por razones de privacidad y volumen, las imágenes y la base de datos generada **no se incluyen en este repositorio**.

---

## Licencia

Código publicado bajo licencia MIT. Los datos del archivo parroquial pertenecen al Archivo Histórico de la Diócesis de Plasencia.
