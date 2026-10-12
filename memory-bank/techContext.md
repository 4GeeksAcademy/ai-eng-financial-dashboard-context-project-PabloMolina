# Contexto técnico

## Lenguajes y frameworks
- Frontend: TypeScript y React. `frontend/package.json` declara `react` y `react-dom` en versión `^19.2.4`; `typescript` en `~6.0.2`.
- Herramienta de desarrollo y build del frontend: Vite `^8.0.4`, declarada en `frontend/package.json`. `frontend/vite.config.ts` configura el plugin React y el proxy API.
- Backend: Python con FastAPI. `backend/requirements.txt` declara `fastapi`, sin fijar versión; `backend/app/main.py` crea la aplicación FastAPI.
- ASGI server y herramientas backend: `backend/requirements.txt` declara `uvicorn[standard]`, `debugpy`, `pytest`, `pytest-cov` y `httpx`, todos sin versiones fijadas.
- Pruebas frontend: Vitest `^4.1.4`, declarado en `frontend/package.json`.

## Infraestructura y ejecución
- `docker-compose.yml` define los servicios `frontend` y `backend`; monta sus directorios de trabajo como volúmenes y configura `frontend` con dependencia de `backend`.
- El contenedor frontend se basa en `node:24-alpine`, expone `5173` y arranca Vite en `0.0.0.0:5173`. Evidencia: `frontend/Dockerfile`.
- El contenedor backend se basa en `python:3.13-slim`, expone `8000` y `5678`, e inicia Uvicorn en `8000` y debugpy en `5678` con `--reload`. Evidencia: `backend/Dockerfile`.
- Compose mapea `5173:5173`, `8000:8000` y `5678:5678`. Evidencia: `docker-compose.yml`.
- `frontend/vite.config.ts` reenvía las solicitudes `/api` a `http://backend:8000`. `frontend/src/App.tsx` permite anteponer `VITE_API_BASE_URL`, vacío por defecto.

## Dependencias clave
- UI y visualización (versiones declaradas en `frontend/package.json`): React y React DOM `^19.2.4`; Recharts `^3.8.1`; Lucide React `^1.8.0`; Tailwind CSS `^4.2.0`; `@tailwindcss/vite` `^4.2.2`; `clsx` `^2.1.1`; `tailwind-merge` `^3.5.0`; `class-variance-authority` `^0.7.1`.
- Herramientas frontend (versiones declaradas en `frontend/package.json`): Vite `^8.0.4`; TypeScript `~6.0.2`; Vitest `^4.1.4`; ESLint `^9.39.4`.
- Backend/API y pruebas: FastAPI, `uvicorn[standard]`, debugpy, pytest, pytest-cov y httpx están declarados sin versiones en `backend/requirements.txt`.
- Versiones exactas de paquetes Python instaladas en la imagen no están fijadas por `backend/requirements.txt`: **sin verificar**.
