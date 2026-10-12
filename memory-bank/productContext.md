# Contexto del producto

## Qué hace
El proyecto es un dashboard de métricas financieras con frontend React + TypeScript y backend FastAPI. Evidencia: `README.es.md` y `backend/app/main.py` (título de la API: `Financial Metrics API`).

El backend genera movimientos financieros de ejemplo con fecha, monto, tipo de operación, categoría y tipo de negocio. Evidencia: modelo `FinancialMovement` y función `generate_mock_movements` en `backend/app/routes.py`.

El dashboard muestra KPI y visualizaciones mensuales de ingresos, egresos y porcentaje de beneficio. Evidencia: `frontend/src/App.tsx` renderiza `KPIRow`, `IncomeOutcomeChart` y `ProfitPercentChart`; `frontend/src/lib/financial-utils.ts` define `computeKPIs` y `computeMonthlyData`.

## Para quién
- La documentación presenta el proyecto como un dashboard de métricas financieras y parte de un proyecto educativo de 4Geeks Academy. Evidencia: `README.es.md`.
- El público usuario final del dashboard no está especificado en los archivos revisados: **sin verificar**.

## Flujo principal
1. `frontend/src/App.tsx` solicita `GET /api/metrics` al iniciar el componente.
2. `backend/app/routes.py` atiende `/api/metrics`, genera movimientos de ejemplo con semilla `42`, aplica filtros opcionales y los devuelve ordenados cronológicamente.
3. `frontend/src/App.tsx` pasa la respuesta a `computeKPIs` y `computeMonthlyData`, definidos en `frontend/src/lib/financial-utils.ts`.
4. La interfaz muestra los KPI y gráficos mediante componentes de `frontend/src/components/dashboard/`; durante la solicitud pasa estados de carga y presenta un mensaje si la carga falla.

## Límites verificados
- El frontend mostrado en `frontend/src/App.tsx` consume `/api/metrics`. Otros endpoints están implementados en `backend/app/routes.py`, pero su consumo por el dashboard no está implementado allí: **verificado en esos archivos**.
- El período presentado en `frontend/src/App.tsx` es el texto fijo `2024 - Full Year`; que coincida con el rango de datos generado no está garantizado: **sin verificar**.
