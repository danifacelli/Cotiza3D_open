# Technical Overview

Este documento complementa al README con detalles para quienes van a mantener o extender Cotiza3D.

## Stack principal
- **Framework:** [Next.js 15](https://nextjs.org/) con App Router y turbopack (script `npm run dev`).
- **Lenguaje:** TypeScript con soporte estricto.
- **UI:** React 18, Tailwind CSS, componentes basados en shadcn/ui.
- **Estado y persistencia:** `localStorage` + hook `useLocalStorage` para hidratar datos por pantalla.
- **Iconografía:** `lucide-react`.
- **Utilidades adicionales:** `date-fns`, `zod`, `react-hook-form`, `nanoid`, `html2canvas`, `jspdf`, `embla-carousel-react`, entre otros.

## Scripts de npm
- `npm run dev`: arranca Next.js en modo desarrollo (puerto 9002, turbopack).
- `npm run build`: build de producción.
- `npm run start`: servidor Next.js productivo.
- `npm run lint`: validación ESLint.
- `npm run typecheck`: verificación TypeScript sin emitir archivos.
- `npm run genkit:*`: arranca herramientas de IA Genkit (si se usan flujos de IA).

## Estructura de carpetas relevante
```
src/
  app/
    (main)/           # Rutas protegidas por el layout principal
      dashboard/
      designs/
      quotes/
      clients/
      materials/
      machines/
      investments/
      future-purchases/
      links/
      settings/
    layout.tsx        # Layout raíz
    page.tsx          # Redirige al dashboard
  components/
    dashboard/
    designs/
    quotes/
    materials/
    machines/
    clients/
    future-purchases/
    investments/
    links/
    settings/
    ui/               # Base shadcn/ui
  hooks/
    use-local-storage.ts
    use-toast.ts
  lib/
    calculations.ts
    constants.ts
    defaults.ts
    types.ts
  services/
    exchange-rate-service.ts
```

## Flujo de datos
- `src/hooks/use-local-storage.ts` carga valores por clave (`LOCAL_STORAGE_KEYS`) e hidrata cada pantalla. Retorna `[valor, setter, isHydrated]` para evitar renderizados incompletos.
- Datos iniciales (mock) están en `src/lib/defaults.ts`. Sirven como “semillas” cuando no existe almacenamiento previo.
- El cálculo de costos está centralizado en `src/lib/calculations.ts`, reutilizado por diseños, presupuestos, dashboard, inversiones y clientes.
- Tipos compartidos en `src/lib/types.ts`. Al extender modelos conviene actualizar aquí primero.

## Intercambio de moneda
- `src/services/exchange-rate-service.ts` consulta tasas (fuente externa definida en el servicio). Las pantallas que muestran montos locales llaman a `getExchangeRate` después de hidratar configuración.
- El manejo de decimales depende de `settings.currencyDecimalPlaces`, con casos especiales para monedas sin centavos (`CLP`, `PYG`).

## Estados de presupuestos
Estos valores están tipados en `Quote['status']` y se usan tanto en tablas como en el dashboard:
`draft`, `accepted`, `in_preparation`, `ready_to_deliver`, `delivered`, `canceled`.

## Copia de seguridad
`BackupRestore` exporta todos los datos serializados en un único JSON con esta estructura aproximada:
```
{
  "cotiza3d_materials": [...],
  "cotiza3d_machines": [...],
  "cotiza3d_settings": {...},
  "cotiza3d_quotes": [...],
  "cotiza3d_designs": [...],
  "cotiza3d_investments": [...],
  "cotiza3d_future_purchases": [...],
  "cotiza3d_clients": [...],
  "cotiza3d_links": [...]
}
```
Al importar se validan las claves y se sobreescribe `localStorage`. Cualquier clave faltante se rellena con `{}` o `[]` según corresponda.

## Guías para contribuir
1. **Instalación:** `npm install`.
2. **Convenciones:**
   - Componentes bajo `src/components/<dominio>/`.
   - Las rutas del App Router viven en `src/app/(main)/<feature>/` con archivos `page.tsx`.
   - Usa `useLocalStorage` para leer/escribir datos persistentes.
3. **Estilos:** Tailwind + componentes shadcn. Evitar estilos inline complejos para mantener consistencia.
4. **Cálculos:** Si agregas métricas, reutiliza `calculateCosts` o añade helpers en `lib/`.
5. **Internacionalización:** Actualmente solo en español. Si se expande, considerar `next-intl` u otra solución.
6. **Testing:** No hay suite formal incluida. Se recomienda añadir pruebas unitarias (Vitest/Jest) para `lib/` y tests de integración ligeros para componentes críticos.

## Próximos pasos sugeridos
- Integrar autenticación opcional y sincronización en la nube.
- Agregar reportes descargables (CSV/PDF) para clientes o inversiones.
- Automatizar tareas repetitivas con cron (ej. refrescar tipo de cambio).

Para un contexto más conceptual, consulta también `docs/blueprint.md`.
