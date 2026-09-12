# 🎯 Skill: Auditoría de Sistemas de Diseño con IA

## Por qué esta skill importa ahora

Auditar un Design System dejó de ser "revisar si los colores coinciden". Hoy es diagnosticar si el sistema está listo para ser **consumido, extendido y mantenido por IA** (agentes que generan código, plugins que auto-corrigen tokens, Cursor sugiriendo componentes). Un DS mal auditado hoy no solo genera inconsistencia visual: genera alucinaciones de IA cuando un agente intenta usarlo.

---

## El Framework: 5 Capas

Cada capa tiene objetivo, preguntas clave y output. Auditas de arriba a abajo — si una capa falla, condiciona a las siguientes.

### 1. Inventario
**Objetivo:** saber qué existe realmente (no lo que dice la documentación).
- ¿Cuántas variantes de un mismo componente circulan en el archivo de Figma?
- ¿Hay componentes huérfanos (sin instancias) o instancias detached?
- ¿Los tokens declarados en Figma coinciden con los tokens implementados en código?
**Output:** mapa de componentes vs. uso real + lista de duplicados/huérfanos.

### 2. Consistencia
**Objetivo:** detectar drift entre diseño e implementación.
- ¿El mismo componente tiene distinto radius/spacing en Figma vs. producción?
- ¿Los estados (hover, disabled, error) están cubiertos en ambos lados?
**Output:** tabla de discrepancias diseño↔código, priorizada por impacto visual.

### 3. Accesibilidad
**Objetivo:** que el sistema no rompa WCAG por diseño.
- Contraste de color en variantes secundarias/terciarias (no solo la primaria).
- Foco visible, tamaños táctiles mínimos, semántica de componentes interactivos.
**Output:** checklist WCAG por componente, no por pantalla.

### 4. Documentación & Gobernanza
**Objetivo:** que el sistema sea navegable sin depender de una persona.
- ¿Existe un changelog de decisiones? ¿Quién aprueba una nueva variante?
- ¿La nomenclatura sigue una convención (BEM, atómica, semántica) de forma consistente?
**Output:** documento de governance + historial de decisiones versionado.

### 5. IA-Readiness (la capa nueva)
**Objetivo:** verificar si un agente de IA puede usar el sistema sin inventar cosas.
- ¿Los nombres de capas/componentes en Figma son descriptivos o genéricos ("Frame 482")?
- ¿Los tokens tienen metadata semántica (ej. `color/error/text`) o solo valores crudos (`#FF0000`)?
- ¿El sistema tiene una fuente única de verdad (Figma Variables o Tokens Studio) sincronizada con código?
**Output:** score de "legibilidad para IA" — esto es lo que diferencia tu perfil como diseñador AI-native.

---

## Mapeo de herramientas por capa

| Capa | Herramienta | Uso concreto |
|---|---|---|
| Inventario | Figma (MCP: `figma_audit_design_system`) | Escaneo automático de componentes, variantes y huérfanos sin revisar página por página |
| Consistencia | Cursor + MCP (`figma_check_design_parity`) | Compara specs de Figma contra el código del repo y marca discrepancias |
| Accesibilidad | Figma (`figma_lint_design`, `figma_audit_component_accessibility`) | Lint WCAG 2.2 automático sobre el archivo activo |
| Documentación | Obsidian | Vault con un nota por componente, linkeada a decisiones — tu "memoria" del sistema a lo largo del tiempo |
| Gobernanza | GitHub | Versionado de tokens (JSON/DTCG), PRs para cambios de sistema, changelog automático |
| IA-Readiness | Antigravity / agentes | Automatizar tareas repetitivas del audit (renombrar capas, generar reporte) a escala, sin hacerlo componente por componente a mano |

---

## Caso práctico aplicado: TapTap Design System

Este mismo repo (`docs/auditoria-taptap-ds.md`) es el resultado real de correr las 5 capas sobre un DS de verdad (no ficticio): el archivo comunitario de Figma "TapTap Design System | Developers". Salud general: 76/100. El hallazgo más valioso no fue visual — fue que 0% de los componentes tienen descripción, así que cualquier IA que lo use directamente va a alucinar nombres de props.

---

## Ejercicio aplicable esta semana

1. Elegí un solo componente (ej. `Button` o `Input`) de un sistema real que uses.
2. Corré las 5 capas solo sobre ese componente (no el sistema completo — así no te frena el tamaño).
3. Anotá en Obsidian 1 hallazgo por capa, aunque sea menor.
4. Puntuá del 1 al 5 su "IA-Readiness": ¿un agente podría generar el componente en código solo leyendo Figma?
5. Armá un reporte de 1 página con los 5 hallazgos + 1 recomendación priorizada.
6. Repetilo la semana siguiente con otro componente — la skill se construye por repetición, no por lectura.
