# Inventario de componentes — TapTap Design System

Extraído del archivo de Figma vía Figma Console MCP (`figma_get_design_system_summary`). Todavía no hay implementación en código en este repo — este inventario es el punto de partida para portar componentes de forma incremental (ver `figma_ds_status` en el framework de auditoría para trackear qué se va portando).

**Totales:** 165 componentes — 141 en variant sets, 24 standalone.

| Categoría | Componentes sueltos | Variant sets |
|---|---|---|
| Basic | 1 | 9 |
| Content | 4 | 3 |
| Item | 0 | 4 |
| Primary | 0 | 3 |
| Outline | 0 | 3 |
| Ghost | 0 | 3 |
| Link | 1 | 2 |
| Action | 0 | 3 |
| File | 0 | 2 |
| Area Chart | 0 | 2 |
| Warning | 0 | 2 |
| Checkbox | 1 | 1 |
| Multiple | 1 | 1 |
| Line Chart | 1 | 1 |
| Tooltips | 0 | 2 |

## Gaps detectados en la auditoría

Faltan 3 de las 6 categorías "core" de un DS: **modal/dialog, navegación, alert/toast**. Antes de portar componentes existentes conviene decidir si estos se diseñan primero en Figma o se implementan directo en código y se documentan hacia atrás.

## Próximo paso

Portar componente por componente, empezando por los de mayor uso real (Button, Input, Checkbox), usando los tokens de `../tokens/` como única fuente de valores — no hardcodear colores/spacing en el código del componente.
