# TapTap Design System — Repositorio

Versionado en GitHub del Design System de Figma **"TapTap Design System | Developers (Community)"**, generado como caso práctico de la skill de auditoría de sistemas de diseño con IA.

Archivo de Figma: https://www.figma.com/design/iV8dKjWaq6ZmKxoiDREKBr/

## Estructura

```
tokens/       Design tokens exportados de Figma Variables (colores, tipografía, tamaños)
  tokens.json   Formato DTCG (fuente canónica)
  tokens.css    Custom properties CSS (:root)
  tokens.ts     Módulo TypeScript tipado
components/   Inventario de componentes del archivo de Figma
docs/         Auditoría del sistema + framework/skill usado para generarla
```

## Tokens

**`tokens/tokens.json` es la fuente viva**, sincronizada directamente desde Figma con el plugin **Tokens Studio**. El flujo es: editas un token en Figma → le das a Push (⬆) en el plugin → este archivo se actualiza solo en GitHub. No se edita a mano.

131 variables de Figma, en 2 colecciones:

- **Primitives** (109): la paleta base — Neutral, Primary, Auxiliary, Danger, Warning, Success, Info, Chart Colors, tipografía (tamaños, line-height, letter-spacing), `font-family`.
- **Semantic** (22): capa semántica que debería aliasear a Primitives (`color/text/primary`, `color/bg/surface`, `color/action/primary`, `color/feedback/error`, etc.) — es la capa que consume el código.

`tokens/tokens.css` y `tokens/tokens.ts` son una **foto fija del día 1** (generados a mano antes de conectar Tokens Studio) y ya están desactualizados frente a `tokens.json`. Pendiente: automatizar su regeneración a partir de `tokens.json` (por ejemplo con Style Dictionary) cada vez que este cambie — por ahora, si necesitas CSS/TS al día, regenéralos manualmente desde `tokens.json`.

## Componentes

Ver `components/README.md` para el inventario completo (165 componentes / 141 variant sets, por categoría). Todavía no hay implementación en código — esta primera versión del repo prioriza tokens + gobernanza; los componentes se portan de forma incremental.

## Auditoría (IA-Readiness)

Ver `docs/auditoria-taptap-ds.md` — resultado real de correr las 5 capas de la skill sobre este archivo: **Salud general 76/100**. El hallazgo principal: 0% de los componentes y solo 2% de los tokens tienen descripción, lo cual es la principal fuente de alucinaciones si un agente de IA intenta generar código desde este archivo sin pasar por este repo.

## Gobernanza

Este repo es la fuente de verdad versionada para tokens y decisiones del DS (capa "Documentación & Gobernanza" de la skill). Cambios de tokens → PR en este repo → review → merge. El historial de commits/PRs sustituye al changelog manual.
