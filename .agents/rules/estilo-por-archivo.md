# estilo-por-archivo

## Nombre
`estilo-por-archivo` — respetar el formato existente en cada archivo y preservar el casing del contrato API.

## Alcance
- `frontend/src/App.tsx`
- `frontend/src/components/dashboard/`
- `frontend/src/lib/financial-types.ts`
- `backend/app/routes.py`

## Justificación
`frontend/src/App.tsx` usa comillas dobles y punto y coma, mientras `frontend/src/components/dashboard/dashboard-header.tsx` usa comillas simples y omite los puntos y coma. Además, el modelo `FinancialMovement` de `backend/app/routes.py` y la interfaz del mismo nombre en `frontend/src/lib/financial-types.ts` comparten campos API en `snake_case`, como `create_date` y `operation_type`.

## Guía
- Al editar un archivo, conserva su formato local —comillas, punto y coma e indentación— y limita el diff a los cambios necesarios; no reformatees carpetas completas por una modificación funcional.
- En nuevos componentes de React, usa nombre de componente en `PascalCase` y nombre de archivo en `kebab-case`, siguiendo ejemplos como `IncomeOutcomeChart` en `income-outcome-chart.tsx`.
- Conserva en los tipos TypeScript los nombres `snake_case` que forman parte de respuestas del API. Si cambia un campo, coordina el cambio con el modelo Pydantic en `backend/app/routes.py`; no conviertas el nombre solo para ajustarlo a `camelCase`.
- Para propiedades internas del frontend que no representan el contrato del API, sigue el estilo ya usado en ese módulo; no mezcles una conversión de casing con un cambio de formato sin necesidad.
