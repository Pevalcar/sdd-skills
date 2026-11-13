# Full Flow Example — Proyecto Web Completo

Ejemplo completo de uso del sistema SDD V2 con perfil web-frontend.

## Escenario

Crear un dashboard de métricas con React, TypeScript y Chart.js.

## Inicio

```bash
/sdd-discover
```

**Detección automática:**
```
🔍 Perfil detectado: web-frontend
📁 Stack: React 18, TypeScript 5, Vite, Tailwind CSS

📋 Estado del proyecto:
  ✓ constitution.md existe (aprobado)
  ✓ spec.md existe (aprobado)
  ✗ plan.md no existe
  ✗ tasks.md no existe
  ✗ Tests no ejecutados

💡 Skill recomendado: /sdd-plan
```

El usuario puede:
- Continuar con `/sdd-plan` directamente
- O reiniciar todo con `/sdd-flow "dashboard métricas"`

---

## Caso A: Flujo Individual

### 1. Plan técnico existente

```bash
/sdd-plan
```

Genera `specs/002-dashboard/plan.md`:
- Arquitectura: Components → Hooks → API Client
- Modelo: MetricCard interface, DashboardData type
- Algoritmo: fetch metrics → transform → render charts
- Cobertura: RF-1 → MetricCard.test.tsx, etc.

### 2. Tareas

```bash
/sdd-tasks
```

Genera `specs/002-dashboard/tasks.md`:
- T1: Setup types y interfaces
- T2: Crear hook useMetrics
- T3: Component MetricCard
- T4: Layout grid responsivo
- T5: Integration test completo

### 3. Implementar T1

```bash
/sdd-implement T1
```

Resultado:
```typescript
// src/types/metrics.ts (nuevo)
export interface MetricCard {
  id: string;
  title: string;
  value: number;
  trend: 'up' | 'down' | 'stable';
}

export interface DashboardData {
  cards: MetricCard[];
  lastUpdated: Date;
}
```

Tests creados y passing. Tasks marcada como completada.

---

## Caso B: Flujo Automático

```bash
/sdd-flow "dashboard de métricas con React"
```

Wizard interactivo ejecuta automáticamente:
1. ✅ Discover (perfil web-frontend cargado)
2. ⏭️ Skip constitution (ya existe)
3. ✅ Validate spec exists (está aprobada)
4. ▶️ Ejecutar plan
5. ▶️ Ejecutar tasks
6. ▶️ Implementar T1
7. ▶️ Validar cobertura

Checkpoint guardado en `.sdd-state.json` después de cada fase crítica.

---

## Reglas del Perfil web-frontend Aplicadas

Durante toda la ejecución se aplicaron reglas específicas:

### TypeScript Strict
```typescript
// ❌ Anti-pattern (prohibido)
const data = response.data; // implicit any

// ✅ Required pattern
const data: DashboardData = response.data as DashboardData;
```

### Bundle Size Monitoring
```bash
# Después de cada feature, verificar bundle
npm run build && npm run size-limit
# Warning si > 10KB aumentado
```

### Accessibility
```tsx
// ✅ WCAG 2.1 AA compliant
<MetricCard 
  title="Ventas Totales" 
  value={sales}
  aria-label={`Ventas totales: ${sales} dólares`}
/>
```

### Testing Patterns
```typescript
// ✅ Use Render (Testing Library), not Mount
import { render, screen } from '@testing-library/react';

// ✅ DAMP over DRY
test('shows metric title correctly', () => {
  render(<MetricCard title="Revenue" />);
  expect(screen.getByText('Revenue')).toBeInTheDocument();
});

test('formats value with currency', () => {
  render(<MetricCard value={1234.5} />);
  expect(screen.getByText('$1,234.50')).toBeInTheDocument();
});
```

---

## Verification Gates Cumplidas

Antes de marcar feature como done:

- [x] TypeScript compila sin errores ni warnings
- [x] ESLint pasa con zero errors
- [x] Prettier formatting aplicado
- [x] Unit tests pasan (Jest + Vitest)
- [x] Component tests pasan (Testing Library)
- [x] No console errors en browser
- [x] Bundle size dentro de thresholds
- [x] Accessibility audit passed (axe-core)
- [x] Lighthouse score > 90

---

## Definition of Done Verificada

### Correctness
- [x] Todos acceptance criteria cumplidos
- [x] Código runs y behaves expected (verificado runtime)
- [x] Nuevos behavior covered by tests
- [x] Existing tests still pass
- [x] Edge cases handled

### Quality
- [x] Naming reveals intent
- [x] No duplicated logic
- [x] No dead code or debug output
- [x] Scoped to task only
- [x] Linting/formatting pass

### Integration
- [x] Works with rest of system
- [x] Backward compatibility considered
- [x] Feature flag ready if needed

### Documentation
- [x] Public APIs documented
- [x] README updated con nuevo feature
- [x] Change log entry added

### Ship-readiness
- [x] Security reviewed (no user input in this case)
- [x] Observability not needed (client-only)
- [x] Rollback path: revert commit
- [x] Human approved before merge

---

## Output Final

```
Dashboard completo implementado:
✓ Types definidos
✓ Hook useMetrics creado
✓ Component MetricCard tested
✓ Grid layout responsivo
✓ 15 tests passing (100% green)
✓ Bundle: 45KB (within limit)
✓ Lighthouse: 95 performance

Próximo paso sugerido:
/sdd-implement T2  (para siguiente feature)
```
