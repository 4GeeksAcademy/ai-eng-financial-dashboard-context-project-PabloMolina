# testing-obligatorio

## Nombre
`testing-obligatorio` — cubrir con pruebas los cambios de lógica y endpoints usando las herramientas existentes.

## Alcance
- `backend/app/routes.py`
- `backend/tests/test_routes.py`
- `backend/tests/conftest.py`
- `frontend/src/lib/financial-utils.ts`
- `frontend/src/lib/financial-utils.test.ts`
- `frontend/src/App.tsx`
- `frontend/src/components/`
- `frontend/package.json`

## Justificación
`backend/tests/test_routes.py` ya prueba endpoints con `TestClient` y funciones como la generación y filtrado de movimientos. `frontend/src/lib/financial-utils.test.ts` cubre cálculos de KPI, agregación mensual y formateadores con Vitest. No hay en el repositorio una prueba visible del componente `App` ni de los componentes del dashboard.

## Guía
- Si modificas un endpoint o una función de apoyo en `backend/app/routes.py`, añade o ajusta el caso correspondiente en `backend/tests/test_routes.py`; reutiliza `TestClient` y datos deterministas como `seed=42` cuando corresponda.
- Si modificas cálculos o formateadores de `frontend/src/lib/financial-utils.ts`, añade o ajusta pruebas en `frontend/src/lib/financial-utils.test.ts`.
- Si modificas el manejo de carga, error o render de `frontend/src/App.tsx`, o el comportamiento de un componente en `frontend/src/components/`, evalúa cobertura de interfaz. El repo no contiene actualmente pruebas de esos componentes; no afirmes que quedan cubiertos por los tests de utilidades.
- Usa los comandos ya declarados en `frontend/package.json` (`npm test`, `npm run lint` y `npm run build`) para validar cambios del frontend. Ejecuta las pruebas de backend con pytest desde el contexto del backend, donde están `requirements.txt` y `backend/tests/`.
- Informa qué validaciones se ejecutaron y cuáles no; no marques como probada una capa que carece de cobertura ejecutada.
