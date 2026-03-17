# Taller_B3_T1 - Machine Learning para series financieras

## Descripción del proyecto
Este repositorio contiene el notebook `Taller_B3_T1.ipynb`, donde se trabaja un pipeline de analisis cuantitativo sobre datos de mercado de criptomonedas.

El flujo principal incluye:
- Carga automática de datos CSV en `data/`.
- Construcción y comparación de barras `tick`, `volume` y `dollar`.
- Análisis de retornos y volatilidad por tipo de barra.
- Diferenciación fraccional para aproximar estacionariedad.
- Etiquetado de eventos con método de triple barrera.
- Visualizaciones para inspección y validación.

## Estructura del repositorio
- `Taller_B3_T1.ipynb`: notebook principal.
- `data/`: archivos CSV de entrada (`*-1m-YYYY-MM.csv` y `BTCUSDT-aggTrades-YYYY-MM-DD.csv`).
- `Taller_B3_T1.pdf`: exportado del taller.
- `requirements.txt`: dependencias para reproducibilidad.

## Requisitos
Se recomienda Python 3.10 o 3.11.

Instalación en entorno virtual:

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux/macOS
source .venv/bin/activate

pip install --upgrade pip
pip install -r requirements.txt
```

## Cómo ejecutar
1. Coloca los CSV en la carpeta `data/` con los nombres esperados.
2. Abre `Taller_B3_T1.ipynb` en Jupyter Lab o VS Code.
3. Ejecuta las celdas en orden, desde el inicio.
4. Revisa tablas y gráficos finales para validar resultados.

## Convenciones de datos
- Velas 1m: `<SYMBOL>-1m-YYYY-MM.csv`
  - Ejemplo: `BTCUSDT-1m-2026-02.csv`
- Trades agregados BTC: `BTCUSDT-aggTrades-YYYY-MM-DD.csv`
  - Ejemplo: `BTCUSDT-aggTrades-2026-03-16.csv`

## Notas de uso
- El notebook detecta automáticamente todos los meses disponibles de cada activo 1m.
- También detecta automáticamente los archivos `aggTrades` disponibles.
- En triple barrera, la clase `0` puede ser muy baja o nula si:
  - la volatilidad es alta,
  - el horizonte es amplio,
  - y/o los umbrales son estrechos.

## Resumen de conclusiones
- Las barras por actividad (tick/volume/dollar) estabilizan mejor la información que una simple frecuencia temporal fija en escenarios de intensidad variable.
- Las distribuciones de retornos entre tipos de barra son similares en forma, con diferencias en dispersión y microestructura.
- La diferenciación fraccional permite reducir dependencia temporal manteniendo parte de la memoria de la serie (trade-off entre estacionariedad y correlación con la original).
- En triple barrera, la distribución de etiquetas depende fuertemente de `threshold` y `horizon`; no es raro observar `pct_0` cercano a 0 en mercados muy activos.
- Es recomendable calibrar parámetros por muestra y régimen de volatilidad antes de entrenar modelos supervisados.

## Reproducibilidad
Para resultados comparables entre equipos:
- Usa las versiones fijadas en `requirements.txt`.
- Ejecuta el notebook de principio a fin sin saltar celdas.
- Mantiene la misma carpeta `data/` y convenciones de nombre de archivo.
