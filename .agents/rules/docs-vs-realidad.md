# docs-vs-realidad

## Nombre
`docs-vs-realidad` — mantener las instrucciones y referencias documentales alineadas con los archivos y configuración presentes.

## Alcance
- `README.md`
- `README.es.md`
- `AGENTS.md`
- `docker-compose.yml`
- `frontend/`
- `.agents/rules/`
- `.agents/skills/`
- `memory-bank/`

## Justificación
`README.md` y `README.es.md` indican copiar `frontend/.env.example`, pero ese archivo no existe actualmente en `frontend/`. `AGENTS.md` instruye revisar `.agents/rules/`, `.agents/skills/` y `memory-bank/`; de esas ubicaciones, esta tarea crea `.agents/rules/`, mientras las otras deben comprobarse antes de describirlas como presentes.

## Guía
- Antes de documentar un archivo, puerto, script o servicio, comprueba que exista en el árbol o en la configuración actual. En particular, no presentes `frontend/.env.example` como disponible mientras no se haya creado.
- Si se decide añadir ese archivo de ejemplo, asegúrate de que sus variables correspondan con `frontend/src/App.tsx` y la configuración de `frontend/vite.config.ts`; luego conserva instrucciones equivalentes en `README.md` y `README.es.md`.
- Al cambiar pasos de ejecución o puertos, contrástalos con `docker-compose.yml` y los Dockerfiles antes de actualizar ambos README.
- Mantén las versiones inglesa y española sincronizadas y conserva sus enlaces cruzados.
- Al modificar `AGENTS.md`, refleja la estructura real: `.agents/rules/` existe una vez incorporadas estas reglas; comprueba por separado `.agents/skills/` y `memory-bank/` antes de afirmar que contienen archivos. La propia guía marca `memory-bank/` como condicional.
