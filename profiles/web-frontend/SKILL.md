---
name: profile-web-frontend
description: "Reglas específicas para desarrollo web/frontend (React, Vue, Angular, Next.js, Svelte, etc.)"
---

# Perfil: Web/Frontend Development

Reglas específicas para proyectos web y frontend. Se carga automáticamente cuando se detecta `package.json`, `tsconfig.json`, o frameworks JavaScript/TypeScript.

## Cuándo Cargar

Detectar automáticamente al analizar el proyecto:

| Indicadores | Acciona este perfil |
|-------------|---------------------|
| `package.json` presente | Principal o adicional |
| `tsconfig.json` presente | Configuración TypeScript estricta |
| `next.config.js` / `nuxt.config.ts` | Framework SSR/SSG |
| `vite.config.*`, `webpack.config.*` | Build tools específicos |
| `jest.config.*`, `vitest.config.*` | Testing configuration |
| `eslint.*`, `prettier.*` | Linting/formatting rules |

## Reglas Específicas

### TypeScript
- Strict mode obligatorio
- No `any` sin justificación documentada
- Interfaces vs types: usar `interface` para objetos, `type` para unions/intersecciones
- Generics con constraints cuando posible

### Componentes
- Un componente, una responsabilidad
- Props tipadas explícitamente
- Hooks personalizados para lógica reutilizable
- Naming: PascalCase para componentes, camelCase para hooks/functions

### Testing
- Unit tests: Jest/Vitest para lógica pura
- Component tests: Testing Library (no mount/shallow, prefer render)
- Integration tests: API mocking con MSW o similar
- E2E: Playwright/Cypress para flows críticos

### Performance
- Code splitting obrigatório
- Lazy loading de routes/components pesados
- Bundle analysis antes de agregar dependencies
- Memoization estratégica (useMemo, useCallback)

### Accessibility
- Semantic HTML where possible
- ARIA labels for interactive elements
- Keyboard navigation support
- Color contrast WCAG 2.1 AA minimum

## Anti-Patterns Específicos

| Anti-pattern | Problema | Alternativa |
|-------------|----------|-------------|
| Prop drilling excesivo | Hard to maintain, rigid components | Context/State management |
| useEffect como data fetching | Race conditions, memory leaks | React Query/SWR/TanStack Query |
| Inline functions en JSX | Re-renders innecesarios | useMemo/memo |
| CSS-in-JS para estilos estáticos | Runtime overhead | CSS modules/Tailwind/styled-components |
| Global state para datos locales | Over-engineering, debugging hard | Local state/component state |

## Commands Comunes

| Task | Command |
|------|---------|
| Type check | `tsc --noEmit` |
| Lint | `eslint src/` |
| Format | `prettier --check src/` |
| Unit tests | `vitest run` / `jest` |
| Full test suite | `npm test` |
| Build | `npm run build` |
| Dev server | `npm run dev` |

## Integration Points

- `sdd-spec`: Especificar API contracts y component interfaces
- `sdd-implement`: Tests first, component-driven development
- `sdd-validate`: Coverage report, bundle size checks

## Verification Checklist

- [ ] TypeScript compiles without errors or warnings
- [ ] ESLint passes with zero errors
- [ ] Prettier formatting applied
- [ ] Unit tests pass
- [ ] Component tests pass
- [ ] No console errors in browser
- [ ] Accessibility basics checked (semantic HTML, ARIA)
- [ ] Bundle size reasonable (check before/after)
