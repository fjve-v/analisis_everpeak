# 🔍 Diagnóstico Rápido de Calidad de Datos: Everpeak Retail

Este proyecto implementa un protocolo de auditoría de datos para un dataset de retail. Se enfoca en la identificación de anomalías estructurales y la toma de decisiones basada en evidencia estadística para el tratamiento de valores nulos.

## 🚀 Puntos Clave del Análisis

### 1. Auditoría de Integridad (Missingness)
Se detectaron patrones de datos faltantes en columnas críticas:
* **Geografía:** 100 registros nulos en `city` y `state`.
* **Demografía:** 150 registros sin `customer_age`.
* **Diagnóstico:** Mediante un análisis de grupos (`groupby`), se determinó que la ausencia de datos en `city` es consistente entre métodos de pago (~2%), sugiriendo un patrón **MCAR** (Missing Completely At Random).

### 2. Validación de Consistencia Temporal
El script identifica registros fuera de rango cronológico:
* **Hallazgo:** 15 registros con fecha de orden en el año **2026** (fuera del rango operativo actual).
* **Acción:** Identificación y aislamiento para corrección de captura.

### 3. Estrategias de Imputación Comparadas
No se aplicó una limpieza ciega. Se compararon métodos para minimizar el sesgo:
* **Order Value:** Se validó que la imputación por mediana mantiene la media original ($10,071.56$), confirmando que es una estrategia segura.
* **Customer Age:** Dado que la edad no sigue una distribución normal perfecta, se seleccionó la **mediana** sobre la media para evitar distorsiones por valores extremos.

## 🛠️ Tecnologías
* **Pandas:** Procesamiento de 5,008 registros y análisis de cardinalidad.
* **Python 3.12:** Lógica de diagnóstico y validación.

## 📈 Resumen de Cardinalidad
* **Clientes únicos:** 1,829
* **Métodos de pago:** 4 categorías.
* **Ciudades:** 10 sedes operativas.
