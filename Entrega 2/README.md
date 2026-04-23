# Bank Customer Churn Analysis


---
## Cómo correr el proyecto
Para replicar el proceso ETL y generar el dataset limpio:

1. **Abrir la terminal** y navegar hasta la carpeta `Entrega 2`.
2. **Crear el entorno virtual** (si no existe):
   - python -m venv venv

3. **Activar el entorno virtual**:
   - En Windows: `.\venv\Scripts\activate`
   - En Mac/Linux: `source venv/bin/activate`

4. **Instalar las dependencias**:
   - pip install -r requirements.txt

5. **Ejecutar el Notebook**:
   Abre Jupyter Notebook ejecutando `jupyter notebook`, navega hasta `ETL_Fase3.ipynb` y ejecuta todas las celdas para generar el archivo resultante `Churn_Modelling_Cleaned.csv`.

## Transformaciones realizadas
Durante la Fase 3 de Preparación y Modelado de Datos (ETL) se realizaron las siguientes operaciones:
- **Limpieza**: Se eliminaron las columnas `RowNumber`, `CustomerId` y `Surname` por no aportar valor analítico y generar ruido.
- **Outliers y Tipos de Datos**: Se aplicó la técnica de Rango Intercuartílico (IQR) para atenuar valores extremos en `CreditScore` y se aseguró que su tipo de dato fuera entero (`int`).
- **Formateo para BI**: Se convirtieron variables binarias a texto (`HasCrCard` -> Yes/No, `IsActiveMember` -> Yes/No, `Exited` -> Churn/Retained) para mejorar su legibilidad en Power BI.
- **Preservación de Variables Numéricas**: Se conservaron las columnas originales `HasCrCard_num`, `IsActiveMember_num` y `Exited_num` (con valores 0 y 1) estrictamente para facilitar las futuras pruebas de hipótesis estadísticas.
- **Categorización**: Se crearon tres nuevas dimensiones (`AgeGroup`, `CreditScoreGroup` y `BalanceGroup`) para simplificar filtros y visualizaciones.

## Variables Derivadas (Justificación de Rangos)
Se crearon nuevas variables categóricas para agrupar variables continuas, facilitando su análisis visual en Power BI:

- **AgeGroup (Grupos de Edad)**:
  - `Young` (< 30 años): Clientes jóvenes que recién inician su vida financiera.
  - `Adult` (30 - 50 años): Segmento principal con mayor estabilidad económica e ingresos medios.
  - `Senior` (> 50 años): Clientes en etapa de pre-retiro o retiro, con comportamientos financieros conservadores y diferentes necesidades bancarias.

- **CreditScoreGroup (Puntaje Crediticio)**:
  - `Poor` (< 500): Clientes con alto riesgo crediticio.
  - `Fair` (500 - 649): Riesgo moderado.
  - `Good` (650 - 749): Clientes confiables estándar.
  - `Excellent` (>= 750): Clientes prime con el menor riesgo, objetivo principal para ofrecer productos premium.

- **BalanceGroup (Saldo en Cuenta)**:
  - `No Balance` (0): Identifica rápidamente a los clientes que mantienen sus cuentas vacías, un indicador muy fuerte de inactividad o posible churn inminente.
  - `Medium` (<= 100k): Clientes transaccionales o ahorradores promedio.
  - `High` (> 100k): Clientes de alto valor (High Net Worth) cuyo abandono representa una pérdida económica significativa para el banco.

## Estructura del proyecto
```text
Entrega 2/
│
├── Churn_Modelling.csv          # Dataset original
├── Churn_Modelling_Cleaned.csv  # Dataset procesado por el ETL (listo para Power BI y Análisis)
├── ETL_Fase3.ipynb              # Jupyter Notebook con el paso a paso del proceso ETL
├── requirements.txt             # Dependencias de Python (pandas, numpy, jupyter, etc.)
└── venv/                        # Entorno virtual (no versionado)
```
---