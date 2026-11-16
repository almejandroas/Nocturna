## MiniReto 1 - Botón "Inscríbete": Bootstrap vs Tailwind

**Semana 2 (Bootstrap):** Con boostrap crear botones solo se compone de una clase que es btn, que contiene ya predeterminadas formas e interacciones propias, lo unico que se le puede cambiar es su color de relleno asignandosele.

**Hoy (Tailwind):** construir un boton con tailwind es un poco más complejo, pero entrega autonomia de como quieres que se vea tu boton, esta autonomia es a cambio de más clases y conocer las funciones de estas clases.

**Diferencia clave:** un framework de componentes (Bootstrap) entrega piezas ya diseñadas
(`btn`) que se ven iguales por defecto y se personalizan sobrescribiendo estilos.
Uno utility-first (Tailwind) entrega pequeñas clases de una sola función y el diseño se
compone en el HTML, sin CSS propio y con más control, a cambio de escribir más clases.

## MiniReto 2 - clase usada vs. no usada

Busqué `bg-amber-400` en `src/output.css` y la encontré con su regla CSS, porque la uso en
`index.html`. Busqué `bg-pink-500` y no apareció.

Pasa porque Tailwind CLI escanea mis archivos buscando nombres de clases y genera solo el CSS
de las que encuentra.

## MiniReto 4 - Kit de componentes

### Reglas del kit
- **Radios:** `rounded-xl` en cards, `rounded-lg` en botones, alertas e inputs, `rounded-full` en etiquetas de nivel.
- **Espaciado:** `p-6` dentro de la card, `px-6 py-3` en botones, `px-4 py-3` en alertas e inputs, `space-y-2/4/6` entre elementos, `gap-4/6` entre componentes.
- **Colores:** marca `amber-400` (hover `amber-300`, foco `amber-200`); fondos `slate-900`, `slate-800` y `slate-700`; texto `white`, `slate-300` y `slate-400`; estados `sky` (info), `emerald` (éxito), `amber` (advertencia).
- **Foco:** todo elemento interactivo usa `focus:outline-hidden focus:ring-4` con un color de anillo visible.
- **Accesibilidad:** cada input tiene `<label for>` con su `id`, la alerta de éxito lleva `role="status"` y cada ayuda se conecta con `aria-describedby`.

### Verificación
Los botones, la card, las alertas y los inputs de `componentes.html` comparten estos radios, espaciados y colores, y se pueden recorrer completos con `Tab`.