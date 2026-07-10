# project-copilot-cli-test

[![build](https://img.shields.io/github/actions/workflow/status/OWNER/REPO/ci.yml?branch=main&label=build)](https://github.com/OWNER/REPO/actions)
[![version](https://img.shields.io/badge/version-0.0.0-blue.svg)]
[![license](https://img.shields.io/github/license/OWNER/REPO)](https://github.com/OWNER/REPO)

Plantilla mínima para una aplicación React + TypeScript usando Vite. Incluye configuración básica de ESLint y scripts comunes para desarrollo y build.

## Estado actual
- Paquete: `project-copilot-cli-test` (private)
- Versión: 0.0.0

## Instalación

Instalar dependencias y arrancar el servidor de desarrollo:

```bash
pnpm install
pnpm dev
```

Para construir la versión de producción:

```bash
pnpm build
pnpm preview
```

## Guía rápida
- La guía de uso extendida está en `guide.txt` (verla para pasos adicionales y notas del autor).

## Notas para badges
- Reemplaza OWNER/REPO en los badges por el propietario y el repositorio reales para que muestren información dinámica.
- El badge de build asume que existe un workflow `ci.yml` en `.github/workflows/`. Si no existe, crea un workflow o actualiza la URL del badge.

## React Compiler

El React Compiler no está habilitado en esta plantilla por su impacto en rendimiento. Para activarlo, ver: https://react.dev/learn/react-compiler/installation

## Expansión de ESLint

Si desarrollas una aplicación de producción, considera habilitar reglas de ESLint con comprobación de tipos (type-checked). Un ejemplo de configuración se muestra abajo.

```js
export default defineConfig([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      // Otras configuraciones...

      // Reemplazar configuración por defecto de tseslint por una con comprobación de tipos
      tseslint.configs.recommendedTypeChecked,
      // Alternativa más estricta
      tseslint.configs.strictTypeChecked,
      // Opcional: reglas estilísticas
      tseslint.configs.stylisticTypeChecked,

      // Otras configuraciones...
    ],
    languageOptions: {
      parserOptions: {
        project: ['./tsconfig.node.json', './tsconfig.app.json'],
        tsconfigRootDir: import.meta.dirname,
      },
      // otras opciones...
    },
  },
])

```

También puedes instalar `eslint-plugin-react-x` y `eslint-plugin-react-dom` para reglas específicas de React:

```js
// eslint.config.js
import reactX from 'eslint-plugin-react-x'
import reactDom from 'eslint-plugin-react-dom'

export default defineConfig([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      // Otras configuraciones...
      reactX.configs['recommended-typescript'],
      reactDom.configs.recommended,
    ],
    languageOptions: {
      parserOptions: {
        project: ['./tsconfig.node.json', './tsconfig.app.json'],
        tsconfigRootDir: import.meta.dirname,
      },
      // otras opciones...
    },
  },
])

```
