verificacion:
  repositorio: ai-eng-financial-dashboard-context-project
  fase: 1
  leyenda:
    "✅": verificada en el código
    "❌": incorrecta
    "❓": sin verificar

  afirmaciones:
    - afirmacion: "Propósito: dashboard financiero con React + TypeScript y FastAPI"
      resultado: "✅"
      documentacion: [README.md, frontend/package.json, backend/app/main.py]
      evidencia: "React 19 y Vite en package.json; FastAPI(title='Financial Metrics API') en main.py"

    - afirmacion: "Datos y API: el backend genera movimientos de ejemplo y ofrece endpoints de métricas, resúmenes, categorías, comparaciones y alertas"
      resultado: "✅ (incompleta)"
      documentacion: [backend/app/routes.py]
      evidencia: "generate_mock_movements() usa random. Endpoints: /health, /api/metrics, /facets, /summary, /categories/top, /comparison, /alerts, /b2b, /b2c"
      correccion: "La IA omitió /health, /api/metrics/facets, /api/metrics/b2b y /api/metrics/b2c"

    - afirmacion: "Visualización: el frontend consulta /api/metrics, calcula KPI y datos mensuales y muestra el dashboard"
      resultado: "✅"
      documentacion: [frontend/src/App.tsx, frontend/src/lib/financial-utils.ts]
      evidencia: "fetch(`${API_BASE_URL}/api/metrics`); usa computeKPIs y computeMonthlyData. Solo consume ese endpoint"

    - afirmacion: "Conexión: Vite reenvía /api a http://backend:8000"
      resultado: "✅"
      documentacion: [frontend/vite.config.ts]
      evidencia: "proxy: {'/api': {target: 'http://backend:8000'}}"
      correccion: "API_BASE_URL queda vacío por defecto y puede cambiarse con VITE_API_BASE_URL"

    - afirmacion: "Servicios: Compose define frontend y backend; el frontend depende del backend"
      resultado: "✅"
      documentacion: [docker-compose.yml]
      evidencia: "depends_on: [backend] en el servicio frontend"

    - afirmacion: "Cómo se ejecuta: docker compose up --build"
      resultado: "✅"
      documentacion: [README.md, README.es.md]
      evidencia: "Sección 'How to run locally'"

    - afirmacion: "URLs locales: frontend 5173, backend 8000, API docs en /docs"
      resultado: "✅"
      documentacion: [README.md, docker-compose.yml]
      evidencia: "ports 5173:5173 y 8000:8000; /docs es el Swagger por defecto de FastAPI"
      correccion: "En Codespaces la URL real sale en la pestaña Ports, no es localhost literal"

    - afirmacion: "Puertos de desarrollo: Vite 5173, Uvicorn 8000"
      resultado: "✅ (incompleta)"
      documentacion: [frontend/Dockerfile, backend/Dockerfile]
      evidencia: "--port 5173 en el frontend; --port 8000 en el backend"
      correccion: "El backend también expone 5678 (debugpy) en docker-compose.yml y en el Dockerfile; la IA no lo mencionó"

  verificacion_propia:
    - comprobacion: "docker compose ps muestra frontend y backend en running"
      resultado: "pendiente"
    - comprobacion: "curl http://localhost:8000/health responde"
      resultado: "pendiente"
    - comprobacion: "http://localhost:8000/docs devuelve 200"
      resultado: "pendiente"
    - comprobacion: "Puerto 5678 visible en docker compose ps"
      resultado: "pendiente"