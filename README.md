# financial-transaction-analytics
Procesamiento, limpieza y estructuración analítica de más de 1 millón de transacciones financieras crudas utilizando Python, Pandas y SQL. Aplicación de la Cultura Zero-Manual.
## 📊 Día 3: Inteligencia de Negocio y Modelado DAX

Conecté de forma nativa la base de datos PostgreSQL de la nube a Power BI Desktop, estructurando las siguientes métricas clave de supervivencia financiera (FinTech):

* **Ingresos Totales:**
  `Ingresos_Totales = CALCULATE(SUM('public fact_transactions'[amount]), 'public fact_transactions'[category] = "Ingreso", 'public fact_transactions'[status] = "Completed")`

* **Gastos Totales:**
  `Gastos_Totales = CALCULATE(SUM('public fact_transactions'[amount]), 'public fact_transactions'[category] = "Gasto", 'public fact_transactions'[status] = "Completed")`

* **Burn Rate (Ritmo de Gasto Mensual):**
  `Burn_Rate = ABS([Gastos_Totales])`

* **Caja Actual (Simulación de Fondos):**
  `Caja_Actual = 1500000 + [Ingresos_Totales] + [Gastos_Totales]`

* **Runway (Meses de Vida Restantes):**
  `Runway = DIVIDE([Caja_Actual], [Burn_Rate], 0)`
