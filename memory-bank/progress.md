# Estado del proyecto

## Qué funciona según el código y las pruebas existentes
- El backend crea la API FastAPI y registra las rutas. Evidencia: `backend/app/main.py`.
- `backend/app/routes.py` implementa `/health` y endpoints de métricas para movimientos, facets, resúmenes, categorías principales, comparación, alertas y subconjuntos B2B/B2C.
- El endpoint `/api/metrics` genera movimientos de ejemplo con semilla `42`, acepta filtros por fecha, categoría y tipo de operación, y devuelve los movimientos en orden cronológico. Evidencia: `backend/app/routes.py`.
- El frontend solicita `/api/metrics`, calcula KPI y resúmenes mensuales, y renderiza tarjetas y gráficos. Evidencia: `frontend/src/App.tsx` y `frontend/src/lib/financial-utils.ts`.
- Hay pruebas de backend para endpoints y funciones de rutas en `backend/tests/test_routes.py`, y pruebas de utilidades financieras frontend en `frontend/src/lib/financial-utils.test.ts`.
- Los scripts frontend disponibles son `dev`, `build`, `lint`, `test`, `test:watch` y `test:coverage`. Evidencia: `frontend/package.json`.

## Gaps conocidos
- `frontend/src/App.tsx` consume solo `/api/metrics`; la interfaz no consume allí los endpoints adicionales implementados por el backend. Evidencia: `frontend/src/App.tsx` y `backend/app/routes.py`.
- Las pruebas visibles del frontend cubren utilidades, no el componente `App` ni los componentes del dashboard. Evidencia: `frontend/src/lib/financial-utils.test.ts` y ausencia de pruebas de componentes en `frontend/src/components/dashboard/`.
- `frontend/src/App.tsx` muestra el período fijo `2024 - Full Year`, mientras `backend/app/routes.py` deriva años de generación usando `date.today()`. La correspondencia entre ese rótulo y los datos no está garantizada: **gap verificable en el código**.
- Los README mencionan `frontend/.env.example`, pero ese archivo no existe en el árbol revisado. Evidencia: `README.md`, `README.es.md` y búsqueda del árbol `frontend/`.
- Las comprobaciones de ejecución con Docker, `/health`, `/docs` y el puerto `5678` constan como pendientes en `verification.md`; su estado actual en ejecución queda **sin verificar**.

## Siguientes prioridades documentadas
- `findings.md` enumera cinco reglas propuestas para la siguiente fase: sincronización API-frontend, configuración de desarrollo, testing, documentación frente a realidad y estilo por archivo.
- Los archivos `.agents/rules/api-frontend-sync.md`, `.agents/rules/dev-config-sync.md`, `.agents/rules/testing-obligatorio.md`, `.agents/rules/docs-vs-realidad.md` y `.agents/rules/estilo-por-archivo.md` ya documentan esas reglas.
- No se encontró en los archivos revisados un roadmap adicional ni prioridades posteriores a esas reglas: **sin verificar**.
