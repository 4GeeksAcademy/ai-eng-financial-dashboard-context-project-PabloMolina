# dev-config-sync

## Nombre
`dev-config-sync` — mantener coherentes los servicios y la conexión API del entorno de desarrollo.

## Alcance
- `docker-compose.yml`
- `frontend/vite.config.ts`
- `frontend/src/App.tsx`
- `frontend/Dockerfile`
- `backend/Dockerfile`

## Justificación
`docker-compose.yml` define los servicios `frontend` y `backend`, con los puertos `5173:5173` y `8000:8000`, además de `5678:5678` para el backend. `frontend/vite.config.ts` reenvía `/api` a `http://backend:8000`, mientras `frontend/src/App.tsx` antepone `VITE_API_BASE_URL`, vacío por defecto.

## Guía
- Si cambias el nombre del servicio backend o su puerto interno, actualiza el destino `/api` en `frontend/vite.config.ts` y la configuración de puertos de `docker-compose.yml`.
- Si cambias el puerto de Vite, coordina el puerto expuesto en `docker-compose.yml` y el argumento `--port` de `frontend/Dockerfile`.
- Conserva el uso de `VITE_API_BASE_URL` en `frontend/src/App.tsx` si el frontend debe poder apuntar a otro origen; verifica que el caso por defecto siga funcionando con el proxy de Vite.
- El backend de desarrollo inicia debugpy en `5678` y Uvicorn en `8000` con `--reload` (`backend/Dockerfile`). Mantén sus puertos coordinados con Compose y no describas esa configuración de desarrollo como configuración de producción.
- Tras modificar cualquiera de estas conexiones, revisa en conjunto los archivos de esta regla para evitar cambios parciales entre Compose, Vite y la aplicación.
