# Componente: Button (variante Primary)

> Extraído directamente del archivo de Figma (`Primary`, nodeId `15:12968`, 36 variantes) vía Figma Console MCP. Los datos de color, tipografía y spacing son reales, leídos del componente — no inventados. Las secciones marcadas **[Propuesta — revisar]** son inferencias razonables porque el archivo de Figma no trae esa información (0% de descripciones, según la auditoría de `docs/auditoria-taptap-ds.md`); confírmalas o ajústalas.

## Descripción

Botón de acción principal (relleno, color de marca). Úsalo para la acción primaria de una pantalla o formulario — máximo una por vista para no competir visualmente.

## Variantes

| Eje | Valores | Uso |
|---|---|---|
| Size | Large / Medium / Small | Large en CTAs destacados, Medium por defecto, Small en espacios compactos (tablas, toolbars) |
| Left Icon | true / false | Icono antes del texto |
| Right Icon | true / false | Icono después del texto (no se combinan ambos a la vez en este set) |

## Props / Properties

| Property | Type | Default | Descripción |
|---|---|---|---|
| `size` | `'sm' \| 'md' \| 'lg'` | `'md'` | Mapea a Small/Medium/Large de Figma |
| `label` | `string` | — | Texto del botón (nodo `Text`) |
| `leftIcon` | `ReactNode` | `undefined` | Slot de icono izquierdo |
| `rightIcon` | `ReactNode` | `undefined` | Slot de icono derecho |
| `disabled` | `boolean` | `false` | Aplica el estado Disabled |
| `onClick` | `() => void` | — | **[Propuesta — revisar]** no viene de Figma, es el contrato estándar de un botón |

## Estados y tokens reales

| Estado | Fondo (token) | Valor hex | Texto (token) | Notas |
|---|---|---|---|---|
| Default | `color/action/primary` | `#15C5CE` | `color/text/inverse` (`#FFFFFF`) | — |
| Hover | ⚠️ ninguno — usa `Primary/500` directo | `#47CFD6` | `color/text/inverse` | Transición 300ms ease-out |
| Pressed | `color/action/primary-hover` | `#00ABB6` | `color/text/inverse` | El nombre del token dice "hover" pero en Figma está aplicado al estado Pressed — mismatch de nomenclatura a corregir |
| Disabled | `color/action/disabled-bg` | `#B0EBEC` | `color/text/inverse` | — |

**Hallazgo de consistencia** (aplica la capa 2 de la skill de auditoría): el estado Hover no usa ningún token semántico, usa el primitivo `Primary/500` directo — y el token `color/action/primary-hover` en realidad está aplicado al estado *Pressed*, no a Hover. Recomendación: crear `color/action/primary-hover` (para Hover) y `color/action/primary-pressed` (para Pressed) como tokens separados, y renombrar en consecuencia.

## Tamaños (medidos en Figma)

| Size | Padding (V / H) | Alto total | Font-size | Line-height |
|---|---|---|---|---|
| Large | 8px / 8px | 40px | 16px | 24px |
| Medium | 7px / 8px | 36px | 14px | 22px |
| Small | 3px / 4px | 24px | 12px | 18px |

Tipografía: `Noto Sans SC`, peso 500 (Medium), `letter-spacing: 0`. Border-radius: `4px` en todos los tamaños.

## Accesibilidad **[Propuesta — revisar]**

- **Role**: `button` nativo (usar elemento `<button>`, no un `<div>` con onClick)
- **Teclado**: `Tab` para enfocar, `Enter` / `Space` para activar. En estado Disabled, se excluye del orden de tabulación (`tabindex="-1"` o atributo `disabled` nativo)
- **Screen reader**: se anuncia como "`{label}`, botón". Si lleva solo icono (sin `label` visible), necesita `aria-label` obligatorio — no cubierto por este componente en Figma, revisar si existe una variante icon-only
- **Foco visible**: no hay estado "Focus" definido en las 36 variantes de Figma (solo Default/Hover/Pressed/Disabled) — falta agregarlo para cumplir WCAG 2.4.7. Marcarlo como pendiente en el backlog de diseño.

## Do's and Don'ts

| ✅ Hacer | ❌ Evitar |
|---|---|
| Usar un solo botón Primary por vista/sección | Poner dos botones Primary compitiendo por atención |
| Usar `disabled` solo cuando la acción no es válida aún | Usar Primary para acciones destructivas (usar la variante Danger) |
| Mantener el label corto (1-3 palabras) | Textos largos que rompan el `Min Width` interno del componente |

## Ejemplo de código (React + tokens de este repo)

```tsx
import { tokens } from '../tokens/tokens'; // o import desde tokens.css como custom properties

type ButtonProps = {
  size?: 'sm' | 'md' | 'lg';
  label: string;
  leftIcon?: React.ReactNode;
  rightIcon?: React.ReactNode;
  disabled?: boolean;
  onClick?: () => void;
};

const sizeStyles = {
  lg: { padding: '8px', height: 40, fontSize: 16, lineHeight: '24px' },
  md: { padding: '7px 8px', height: 36, fontSize: 14, lineHeight: '22px' },
  sm: { padding: '3px 4px', height: 24, fontSize: 12, lineHeight: '18px' },
};

export function Button({ size = 'md', label, leftIcon, rightIcon, disabled, onClick }: ButtonProps) {
  return (
    <button
      className="ds-button ds-button--primary"
      style={sizeStyles[size]}
      disabled={disabled}
      onClick={onClick}
    >
      {leftIcon}
      {label}
      {rightIcon}
    </button>
  );
}
```

```css
.ds-button--primary {
  background: var(--color-action-primary);
  color: var(--color-text-inverse);
  border-radius: 4px;
  border: none;
  font-family: 'Noto Sans SC';
  font-weight: 500;
  transition: background 300ms ease-out;
}
.ds-button--primary:hover { background: var(--primary-500); } /* ver hallazgo de consistencia arriba */
.ds-button--primary:active { background: var(--color-action-primary-hover); }
.ds-button--primary:disabled { background: var(--color-action-disabled-bg); cursor: not-allowed; }
```
