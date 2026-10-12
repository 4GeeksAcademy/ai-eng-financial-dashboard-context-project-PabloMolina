# api-frontend-sync

## Nombre
`api-frontend-sync` — mantener coordinados los endpoints de métricas del backend y su consumo en el frontend.

## Alcance
- `backend/app/routes.py`
- `frontend/src/App.tsx`
- `frontend/src/lib/financial-types.ts`
- `frontend/src/lib/financial-utils.ts`

## Justificación
`frontend/src/App.tsx` actualmente consulta `GET /api/metrics` y calcula los KPI y los datos mensuales en el cliente. `backend/app/routes.py` también define endpoints de resumen, categorías, comparación y alertas. Por tanto, añadir un endpoint no hace que aparezca automáticamente en el dashboard.

## Guía
- Al añadir o modificar un endpoint de métricas en `backend/app/routes.py`, determina explícitamente si el dashboard debe consumirlo. Si sí, actualiza la llamada a API y el estado/render correspondiente en `frontend/src/App.tsx` o extrae esa integración a `frontend/src/lib/` según su responsabilidad.
- Cuando cambie el formato de una respuesta, actualiza conjuntamente el modelo Pydantic correspondiente en `backend/app/routes.py` y el tipo consumidor en `frontend/src/lib/financial-types.ts`.
- Comprueba las transformaciones de datos del frontend en `frontend/src/lib/financial-utils.ts`; no des por hecho que usar un endpoint agregado es equivalente al cálculo actual sobre movimientos.
- No presentes endpoints existentes como funcionalidad visible del dashboard hasta confirmar que `frontend/src/App.tsx` los consulta y renderiza sus resultados.
