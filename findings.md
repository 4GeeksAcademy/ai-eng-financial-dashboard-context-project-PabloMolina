# Fase 2: Hallazgos de ingeniería y reglas propuestas

Resumen de los hallazgos más relevantes. Cada regla cita al menos un hecho verificable del repositorio.

## Arquitectura

| Regla propuesta | Evidencia |
|---|---|
| Al añadir métricas, comprobar si el frontend debe consumir los nuevos endpoints; no asumir que ya lo hace. | `App.tsx` solo consulta `/api/metrics`, pero `backend/app/routes.py` también expone resumen, categorías, comparación y alertas. |
| Al cambiar los datos o su período, actualizar el rótulo del dashboard. | `App.tsx` pasa el texto fijo `2024 - Full Year` a `DashboardHeader`, mientras `generate_mock_movements` usa `date.today()`. |
| No alterar el estado global de `random` al generar datos de ejemplo. | `generate_mock_movements(seed=...)` llama a `random.seed(seed)` y usa el módulo global `random`. |

## Naming

| Regla propuesta | Evidencia |
|---|---|
| Mantener `snake_case` del API en los tipos TypeScript. | `FinancialMovement` (Pydantic) y su interfaz en `financial-types.ts` usan `create_date` y `operation_type`. |
| Componentes en `PascalCase`, archivos en `kebab-case`. | `income-outcome-chart.tsx` exporta `IncomeOutcomeChart`. |
| Seguir el formato del archivo editado; sin reformateos masivos. | `App.tsx` usa comillas dobles y `;`; `dashboard-header.tsx` usa comillas simples y sin `;`. |

## Testing

| Regla propuesta | Evidencia |
|---|---|
| Añadir o actualizar pruebas de backend en `test_routes.py` por cada endpoint o función modificada. | `test_routes.py` usa `TestClient`; `conftest.py` configura `sys.path`. |
| Si se cambia `App.tsx` o sus componentes, evaluar pruebas de interfaz. | `financial-utils.test.ts` solo cubre utilidades (KPI, agregación mensual, formateadores), no el componente `App`. |

## Documentación

| Regla propuesta | Evidencia |
|---|---|
| Mantener las instrucciones de setup alineadas con los archivos reales. | Ambos README indican copiar `.env.example`, pero ese archivo no existe. |
| Verificar que las carpetas citadas por `AGENTS.md` existan; actualizarlo si cambia la estructura. | `AGENTS.md` referencia `.agents/rules/`, `.agents/skills/` y `memory-bank/`, que aún no existían en la raíz. |
| Conservar README en inglés y español con enlaces cruzados. | `README.md` y `README.es.md` se enlazan entre sí. |

## DX

| Regla propuesta | Evidencia |
|---|---|
| Al cambiar puertos, servicios o API, sincronizar Compose, proxy de Vite y config del frontend. | Compose define `frontend` y `backend`; Vite redirige `/api` a `http://backend:8000`; `App.tsx` antepone `VITE_API_BASE_URL` (vacío por defecto). |
| No tratar el contenedor backend como configuración de producción. | `backend/Dockerfile` arranca `debugpy` y Uvicorn con `--reload`; Compose expone los puertos `8000` y `5678`. |
| Mantener el alias `@/` alineado entre TypeScript y Vite. | `tsconfig.app.json` mapea `@/*` a `./src/*`; `vite.config.ts` resuelve `@` a `./src`. |

## Prioridades para la Fase 3

Las reglas con mayor impacto, que conviene convertir primero en archivos de `.agents/rules/`, son:

1. **api-frontend-sync**: endpoints nuevos y consumo desde el frontend.
2. **dev-config-sync**: puertos, Compose, proxy de Vite y `VITE_API_BASE_URL`.
3. **testing-obligatorio**: pruebas en `test_routes.py` y `financial-utils.test.ts`.
4. **docs-vs-realidad**: README, `.env.example` y `AGENTS.md` frente a lo que existe.
5. **estilo-por-archivo**: formato local y `snake_case` del API.