# 📈 Financial Transaction Analytics | Cultura Zero-Manual

## 🎯 El Desafío del Negocio
Los equipos financieros tradicionales pierden hasta un 40% de su semana revisando manualmente archivos de Excel, buscando registros duplicados o cuadrando saldos a mano. En el ecosistema FinTech, este retraso operativo cuesta dinero. Mi filosofía es clara: **si un proceso toma más de 15 minutos y es recurrente, debe programarse de forma autónoma.**

---

## 🛠️ Bitácora de Desarrollo Técnico Paso a Paso

### 🐍 Día 1: Ingesta y Limpieza de Datos Automatizada (Python & Pandas)
Desarrollé un pipeline de control que procesa registros masivos de transacciones crudas para mitigar el riesgo de error humano y duplicidad contable:
* **Control de Duplicidad:** Eliminación automática de transacciones repetidas basadas en el `transaction_id` para evitar la sobreestimación artificial de saldos contables.
* **Consistencia de Datos:** Identificación de valores nulos contables y reclasificación automática bajo la etiqueta de *'No Clasificado'* para asegurar la continuidad del flujo analítico.
* **Alertas de Auditoría:** Implementación de un control basado en desviaciones estándar para aislar transacciones atípicas (*outliers*) que superen las 3 desviaciones estándar (detección temprana de anomalías).

*El código completo de esta fase se encuentra documentado en el archivo `data_cleaning_transactions.ipynb` en este repositorio.*

---

### ☁️ Día 2: Arquitectura de Datos Relacionales (PostgreSQL en la Nube)
Migré el almacenamiento de archivos locales hacia una base de datos relacional centralizada y segura utilizando **SQLAlchemy** en Python y **Neon.tech**:
* **Inyección Automatizada:** El pipeline de Python genera la conexión directa e inyecta miles de registros en la tabla relacional `public fact_transactions` en milisegundos, eliminando las cargas manuales.
* **Queries de Auditoría Avanzada (SQL):** Escribí consultas de agregación para desglosar ingresos/gastos netos por categoría y alertas de riesgo operativo con la cláusula `HAVING` para identificar cuentas con más de 2 transacciones fallidas consecutivas.

---

### 📊 Día 3: Inteligencia de Negocio y Modelado Financiero (Power BI & DAX)
Conecté de forma nativa la base de datos PostgreSQL de la nube a Power BI Desktop, estructurando las siguientes fórmulas analíticas complejas de supervivencia financiera:

* **Ingresos Totales:**
  ```dax
  Ingresos_Totales = CALCULATE(SUM('public fact_transactions'[amount]), 'public fact_transactions'[category] = "Ingreso", 'public fact_transactions'[status] = "Completed")
  ```
* **Gastos Totales:**
  ```dax
  Gastos_Totales = CALCULATE(SUM('public fact_transactions'[amount]), 'public fact_transactions'[category] = "Gasto", 'public fact_transactions'[status] = "Completed")
  ```
* **Burn Rate (Ritmo de Gasto Mensual):**
  ```dax
  Burn_Rate = ABS([Gastos_Totales])
  ```
* **Caja Actual (Simulación de Fondos):**
  ```dax
  Caja_Actual = 1500000 + [Ingresos_Totales] + [Gastos_Totales]
  ```
* **Runway (Meses de Vida Restantes):**
  ```dax
  Runway = DIVIDE([Caja_Actual], [Burn_Rate], 0)
