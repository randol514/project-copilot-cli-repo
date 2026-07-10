# Instrucciones permanentes para Copilot en este repositorio

Resumen corto
- Proyecto: plantilla React + TypeScript + Vite. Usa pnpm (hay pnpm-lock.yaml). Objetivo: app mínima con HMR y ESLint.

1) Comandos útiles (build, test, lint)
- Desarrollo (dev server): pnpm install && pnpm dev
- Build (producción): pnpm build  (ejecuta `tsc -b && vite build` según package.json)
- Preview de build: pnpm preview
- Lint: pnpm lint  (ejecuta `eslint .`)
- Tests: no hay script de test en package.json ni configuración de test runner en el repositorio. Por tanto no hay comando para ejecutar tests locales. Si se añaden tests, seguir la convención de añadir un script `test` y permitir ejecutar tests individuales vía el runner elegido (p. ej. `pnpm vitest -- test/name` si se usa Vitest).

2) Arquitectura de alto nivel (qué hay y dónde mirar)
- Entrada de la app: src/main.tsx — inicializa React StrictMode y monta <App />.
- UI principal: src/App.tsx — componente de ejemplo con estado local, imágenes en src/assets y referencias a archivos estáticos en public/.
- Recursos estáticos: public/ (icons.svg, etc.) y src/assets para imágenes empaquetadas.
- Configuración de bundler: vite.config.ts (usa @vitejs/plugin-react).
- TypeScript: tsconfig.json, tsconfig.app.json, tsconfig.node.json — revisar para paths y proyecto dividido.
- Linter: eslint.config.js — utiliza `typescript-eslint`, `eslint-plugin-react-hooks` y `eslint-plugin-react-refresh`.
- Scripts: definidos en package.json (dev/build/lint/preview). No hay tests ni CI workflows en el repo por defecto.

3) Convenciones y patrones clave del repositorio
- TypeScript estricto / .tsx: Las fuentes principales son .ts/.tsx; seguir la tipificación y colocar lógica de componentes en src/. Evitar crear código fuera de src para la app.
- Assets: imágenes usadas por React se colocan en src/assets y se importan en componentes (p. ej. import heroImg from './assets/hero.png'). Archivos públicos (icons.svg) están en public/ y referenciados por rutas absolutas (/icons.svg).
- Paquete privado: package.json declara "private": true — este repo no publica un paquete npm por defecto.
- Gestor de paquetes: pnpm es el candidato primario (pnpm-lock.yaml presente). Los comandos en README usan pnpm; usar pnpm para consistencia.
- ESLint: la configuración usa comprobación de TypeScript (typescript-eslint). Evitar reglas contradictoras; usar `pnpm lint` antes de commits.
- Badges/CI: README sugiere un badge de build que apunta a `.github/workflows/ci.yml`. Si se quiere badge activo, crear un workflow con ese nombre o actualizar el badge.
- Pull requests: guide.txt recomienda usar GitHub CLI (gh) para crear PRs; no es obligatorio, pero es la convención documentada.

4) Archivos relevantes a revisar/actualizar
- README.md: ya actualizado con badges placeholder y guía mínima (ver cambios recientes).
- guide.txt: contiene instrucciones de uso del Copilot CLI, instalación de gh, y recomendaciones para workflows locales — incluye sugerencias que el agente debe respetar (abrir copilot desde la raíz, verificar rama antes de empezar).
- eslint.config.js, vite.config.ts, tsconfig.*.json: revisar si se cambian dependencias o estructura del proyecto.

5) Qué esperar del agente Copilot en futuras sesiones (concrete rules)
- Usar pnpm para comandos por defecto; preferir `pnpm dev` y `pnpm build` cuando se pida ejecutar la app.
- No asumir tests existentes: antes de ejecutar tests, buscar un script `test` en package.json y confirmar runner. Si no existe, preguntar al usuario antes de instalar o configurar un test runner.
- Para badges de CI o cobertura, verificar la existencia de workflows en `.github/workflows`. No crear badges apuntando a workflows inexistentes sin confirmación del usuario.
- Mantener lenguaje de documentación en español por defecto (README y guide.txt están en español), pero aceptar PRs/commits en inglés si el contribuyente lo prefiere.
- Antes de abrir PRs automáticamente, verificar que la CLI `gh` esté disponible; si no lo está, crear la rama, commitear y notificar la URL para crear el PR manualmente.

6) Integraciones y comprobaciones recomendadas (breve)
- Si se quiere testing o E2E, proponer Vitest + Playwright. Preguntar antes de crear CI/servers.
- Si se desea badge de build, crear `.github/workflows/ci.yml` con job `build` y `name: ci` (o actualizar badge para apuntar al nombre real).

---

Referencias internas: README.md (cabecera y sección de instalación), guide.txt (instrucciones de Copilot CLI y uso de gh), package.json (scripts y deps), eslint.config.js y vite.config.ts.

¿Deseas que cree el archivo en el repo ahora y haga un commit + push en una rama para abrir PR automáticamente? También: ¿quieres que configure algún MCP server (por ejemplo Playwright para pruebas E2E)?