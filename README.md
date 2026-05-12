# 💥 Diseño de Malla de Perforación y Voladura
### Método de Langefors-Kihlström · Análisis Determinista + Monte Carlo

Aplicación web interactiva construida con **Streamlit** para el diseño y análisis probabilístico de mallas de perforación y voladura en minería superficial, siguiendo la metodología de **Langefors-Kihlström**.

---

## 🚀 Instalación y Ejecución

### 1. Clonar el repositorio
```bash
git clone https://github.com/tu-usuario/tu-repositorio.git
cd tu-repositorio
```

### 2. Crear entorno virtual (opcional pero recomendado)
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# Linux / macOS
source venv/bin/activate
```

### 3. Instalar dependencias
```bash
pip install -r requirements.txt
```

### 4. Ejecutar la aplicación
```bash
streamlit run app.py
```

La aplicación se abrirá automáticamente en tu navegador en `http://localhost:8501`.

---

## 📋 Parámetros de Entrada

| Símbolo | Descripción | Unidad |
|---------|-------------|--------|
| H | Altura del banco | m |
| d | Diámetro del barreno | mm |
| ρ_F | Densidad del explosivo de fondo | kg/dm³ |
| S_F | Potencia relativa del explosivo de fondo | - |
| ρ_C | Densidad del explosivo de columna | kg/dm³ |
| E/V | Relación espaciamiento / burden | - |
| f | Factor de inclinación | - |
| c | Factor de roca | kg/m³ |
| α | Ángulo de inclinación del barreno | grados |
| N | Número de simulaciones Monte Carlo | - |

---

## 📊 Resultados que genera la app

### Análisis Determinista
- **Geometría del barreno**: Piedra práctica (Vp), espaciamiento (E), sobreperforación (U), longitud de perforación (L).
- **Carga explosiva**: Carga total (Q), carga de fondo (qf), carga de columna (qc), longitud de columna (hc).
- **Indicadores de rendimiento**: Consumo específico (Qe) y rendimiento de perforación (Rp), con interpretación ingenieril y nivel de riesgo.
- **Secuencia de cálculo** paso a paso con fórmulas aplicadas.

### Análisis Probabilístico (Monte Carlo)
- Tabla de estadísticas: Media, Desv. Est., P5, P50, P90, P95 para todas las variables de salida.
- **Fig. 1** – PDF y CDF del Consumo Específico (Qe).
- **Fig. 2** – PDF y CDF del Rendimiento de Perforación (Rp).
- **Fig. 3** – Diagrama de Tornado (correlación de Pearson de cada variable de entrada con Qe).
- **Fig. 4** – Scatter del Factor de Roca (c) vs Consumo Específico (Qe).

### Exportación
- Archivo **Excel** (.xlsx) con 5 hojas detalladas, descargable directamente desde la app.

---

## 🏗️ Estructura del Proyecto

```
├── app.py              # Aplicación principal Streamlit
├── requirements.txt    # Dependencias Python
└── README.md           # Este archivo
```

---

## 📦 Dependencias

| Librería | Versión mínima | Uso |
|----------|---------------|-----|
| streamlit | 1.35.0 | Framework web |
| numpy | 1.26.0 | Cálculo numérico vectorizado |
| matplotlib | 3.8.0 | Generación de gráficas |
| scipy | 1.13.0 | Distribuciones estadísticas (Monte Carlo) |
| openpyxl | 3.1.2 | Exportación a Excel (.xlsx) |

---

## 🧮 Metodología

El método de **Langefors-Kihlström** calcula la geometría de la malla de voladura a partir de:

1. **Piedra máxima teórica (V):**  
   `V = (d/33) · √( (ρF · SF) / (c · f · (E/V)) )`

2. **Piedra práctica:** `Vp = 0.9 · V`
3. **Espaciamiento:** `E = (E/V) · Vp`
4. **Sobreperforación:** `U = 0.3 · Vp`
5. **Longitud de perforación:** `L = U + H / cos(α)`
6. **Carga de fondo:** `hf = 1.3 · Vp`
7. **Retacado:** `hr = Vp`
8. **Carga de columna:** `hc = L − hf − hr`
9. **Consumo específico:** `Qe = Q / (Vp · E · H)`
10. **Rendimiento:** `Rp = (Vp · E · H) / L`

El análisis de Monte Carlo propaga la incertidumbre de cada parámetro usando distribuciones normales truncadas con coeficientes de variación (CoV) definidos por variable.

---

## 📄 Licencia

Uso académico y profesional libre. Se agradece la atribución.
