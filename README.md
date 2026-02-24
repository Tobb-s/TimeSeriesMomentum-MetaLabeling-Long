# Time-Series Momentum with Meta-Labeling (Long-Only)

Este proyecto implementa una estrategia de trading algorítmico cuantitativo enfocada en **Time-Series Momentum** para el mercado de criptomonedas, optimizada mediante técnicas avanzadas de **Machine Learning (Meta-labeling)**.

## 🎯 Objetivo del Proyecto
El objetivo es capturar tendencias alcistas en criptomonedas utilizando un modelo primario de reglas transparentes, filtrando las señales mediante un modelo secundario de clasificación para mejorar el Sharpe Ratio y reducir el Max Drawdown.

### ¿Por qué este enfoque?
* **Evidencia Empírica:** El momentum de serie temporal es robusto en activos digitales, especialmente concentrado en los "ganadores".
* **Gestión de Riesgo Asimétrico:** El enfoque *Long-Only* protege contra los "jumps" violentos y liquidaciones comunes en posiciones cortas de cripto.
* **Control de Overfitting:** Al separar la dirección (modelo primario) del tamaño/confianza (meta-labeling), se limita el sobreajuste estadístico.

## 🛠 Workflow Técnico

### 1. Modelo Primario (Generación de Señal)
Se utiliza un cruce de Medias Móviles Exponenciales (**EWMAC**) o el cálculo del rendimiento pasado en ventanas de observación específicas. 
* **Ventana de Look-back sugerida:** 7 a 28 días.
* **Ventana de Holding sugerida:** 5 a 7 días.

### 2. Etiquetado de Triple Barrera
Implementación del método de **Marcos López de Prado** para definir el éxito de las operaciones:
* **Barrera Superior (Take-Profit):** Dinámica, basada en la volatilidad reciente.
* **Barrera Inferior (Stop-Loss):** Dinámica, basada en la volatilidad reciente.
* **Barrera Temporal:** Cierre forzoso tras un límite máximo de velas.

### 3. Meta-Etiquetado (Filtro ML)
Un clasificador (Random Forest o SVC) actúa como "gerente de riesgo".
* **Features:** Volatilidad, volumen, autocorrelación y microestructura de mercado.
* **Output:** Probabilidad binaria para decidir si se ejecuta la señal del modelo primario.

### 4. Backtesting Realista
Simulación de alta fidelidad que considera:
* **Fluctuaciones intra-vela:** Para evitar subestimar riesgos de liquidación intradía.
* **Costos de Transacción:** Asunción de 15 bps (0.15%) por operación para validar la rentabilidad neta.

## 🚀 Stack Tecnológico
* **Lenguaje:** Python
* **Análisis de Datos:** Pandas, NumPy
* **Machine Learning:** Scikit-learn
* **Backtesting:** VectorBT / MlFinLab
* **Datos:** API de CCXT

---
**Desarrollado por:** [Tobías Baziti](https://github.com/Tobb-s) | [@toobaziti](https://x.com/toobaziti)
