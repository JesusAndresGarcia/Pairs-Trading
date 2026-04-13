# 📊 Estrategia de Arbitraje Estadístico

## Pairs Trading Multiactivo con Cointegración y Filtros de Kalman

---

## 🧠 Descripción General del Proyecto

Este proyecto implementa una **estrategia de arbitraje estadístico** basada en portafolios multiactivo con reversión a la media. A diferencia del pairs trading tradicional, se trabaja con **grupos de 3 activos** que comparten una tendencia estocástica común.

La estrategia combina:

* **Test de cointegración de Johansen** → para construir el portafolio
* **Filtros de Kalman** → para estimar dinámicamente los pesos y el spread
* **Modelo VECM** → para capturar desviaciones de equilibrio
* **Z-score dinámico** → para generar señales de trading
* **Backtesting realista** → incluyendo costos de transacción

---

## 🎯 Objetivos

* Identificar grupos de activos cointegrados
* Construir un portafolio con reversión a la media
* Estimar pesos dinámicos mediante Filtros de Kalman
* Generar señales de trading sin sesgo de anticipación
* Evaluar desempeño considerando costos reales

---

## 🏗️ Estructura del Proyecto

```id="estructura1"
project/
│
├── data/                  # Ingesta, limpieza y validación de datos
├── cointegration/         # Tests Engle-Granger y Johansen
├── kalman/                # Implementación de los dos filtros de Kalman
├── strategy/              # VECM, z-score, lógica de señales
├── backtest/              # Motor de backtesting con costos
├── performance/           # Métricas de desempeño
├── dashboard/             # Aplicación en Streamlit o Dash
├── project_management/    # Planeación, bitácoras y retrospectiva
│
├── notebooks/             # Análisis exploratorio
├── README.md
└── requirements.txt
```

---

## 📈 Descripción de la Estrategia

La estrategia construye un portafolio con reversión a la media definido como:

[
S_t = \beta_t^\top P_t
]

Donde:

* (P_t): vector de precios de los activos
* (\beta_t): pesos dinámicos estimados con Kalman

---

### 🔹 Componentes Clave

### 1. Cointegración

* Se utiliza el test de Johansen para detectar relaciones de equilibrio de largo plazo
* Se extrae el **eigenvector (β)** que define el portafolio

---

### 2. Filtro de Kalman 1 (Pesos dinámicos)

* Estado: ( \beta_t )
* Permite que los pesos del portafolio cambien en el tiempo

---

### 3. Filtro de Kalman 2 (Señales)

* Estado: media y varianza del spread
* Genera un **z-score en tiempo real** sin look-ahead bias

---

### 4. Reglas de Trading

* **Entrada Long Spread**:
  ( z_t < -z_{entry} )

* **Entrada Short Spread**:
  ( z_t > +z_{entry} )

* **Salida**:
  ( |z_t| < z_{exit} )

---

## 📊 Datos

* Fuente: Yahoo Finance (`yfinance`)
* Frecuencia: diaria
* Periodo: aproximadamente 15 años
* Selección: activos del mismo sector (ej. energía, ETFs, bancos)

---

## ⚙️ Instalación

Clonar repositorio:

```bash id="instalacion1"
git clone https://github.com/tu-usuario/stat-arb-kalman.git
cd stat-arb-kalman
```

Instalar dependencias:

```bash id="instalacion2"
pip install -r requirements.txt
```

---

## 🚀 Uso

Ejecutar flujo principal:

```bash id="uso1"
python main.py
```

O usar notebooks:

```bash id="uso2"
jupyter notebook
```

---

## 💸 Supuestos de Costos

| Parámetro        | Valor                |
| ---------------- | -------------------- |
| Comisión         | 0.125% por operación |
| Tasa de préstamo | 0.25% anual          |
| Capital inicial  | $1,000,000           |
| Uso de capital   | 80%                  |

---

## 📉 Backtesting

Incluye:

* Ejecución sin look-ahead bias
* Costos de transacción
* Cambios de posición
* Retornos netos

---

## 📊 Métricas de Desempeño

* Retorno acumulado
* Sharpe ratio
* Frecuencia de operaciones
* Drawdown (extensión opcional)

---

## 📌 Hallazgos Principales

* La cointegración **no siempre está presente**, incluso con alta correlación
* Los Filtros de Kalman permiten un modelo **adaptativo y realista**
* La estrategia depende fuertemente de la estacionariedad del spread
* Los costos de transacción impactan significativamente los resultados

---

## ⚠️ Limitaciones

* Cointegración débil o inestable
* Sensibilidad a parámetros del Kalman (Q y R)
* Baja frecuencia de operaciones en algunos casos
* No se considera slippage

---

## 🔧 Mejoras Futuras

* Extender a portafolios de 4–5 activos
* Reestimar Johansen de forma rolling
* Optimizar parámetros del Kalman
* Agregar gestión de riesgo (stop-loss, volatilidad)
* Crear dashboard interactivo completo

---

## 📊 Dashboard (Opcional)

```bash id="dashboard1"
streamlit run dashboard/app.py
```

---

## 📚 Dependencias

* numpy
* pandas
* yfinance
* statsmodels
* matplotlib

---

## 👨‍💻 Autor

Jesús García

---

## 📄 Licencia

Proyecto con fines académicos.
