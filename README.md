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

## MiniReto 5 - Layout de la landing

### Grid o flex
- **Encabezado y pie: flex.** Son una sola fila de elementos de tamaños distintos (logo,
  enlaces, botón). Flex reparte el espacio en una dirección, con `justify-between` y
  `items-center`.
- **Rutas: grid de 3 columnas.** Las tres cards deben medir lo mismo y alinearse en
  columnas, así que `grid grid-cols-3 gap-6` me da el ancho igual sin calcular nada.
- **Pasos de "¿Cómo funciona?": grid de 4 columnas.** Los cuatro pasos tienen la misma
  estructura (número, título y texto) y deben verse parejos. Con `grid-cols-4` cada paso
  recibe exactamente un cuarto del ancho. Con flex, el ancho de cada paso dependería de su
  contenido y quedarían desiguales.

### Contenedor
Encabezado, secciones y pie usan `max-w-6xl mx-auto px-6`, por eso todo queda alineado.

## MiniReto 6 - Landing responsive

### Qué se rompía a 360 px (versión de escritorio)
(Escribe aquí lo que viste tú. Por ejemplo: el encabezado se salía del ancho y
aparecía scroll horizontal; las rutas quedaban en tres columnas muy angostas; los pasos
quedaban en cuatro columnas con el texto cortado; el pie quedaba apretado.)

### Enfoque mobile-first
Las clases sin prefijo son las del celular. Con `sm:` (640 px), `md:` (768 px) y
`lg:` (1024 px) se agregan los cambios para pantallas más grandes. El celular no usa prefijo.

### Resultados por ancho
| Ancho | Encabezado | Enlaces del encabezado | Rutas | Pasos | Pie | Scroll horizontal |
|---|---|---|---|---|---|---|
| 360 px | Apilado | Ocultos, solo el botón | 1 columna | 1 columna | Apilado | No |
| 768 px | En fila | Visibles | 2 columnas | 2 columnas | En fila | No |
| 1024 px | En fila | Visibles | 3 columnas | 4 columnas | En fila | No |
| 1280 px | En fila | Visibles | 3 columnas | 4 columnas | En fila | No |

### Ajustes por breakpoint
- Título principal: `text-4xl` en celular y `lg:text-6xl` desde 1024 px.
- Títulos de sección: `text-2xl` y `lg:text-3xl`.
- Relleno de las secciones: `py-12` y `lg:py-20`.

### Cambios en las cards
Quité `max-w-sm` para que llenen su columna y agregué `gap-4` en las filas de datos
para que no se peguen cuando la card es angosta.

## MiniReto 7 - Tema de marca y modo oscuro

### Tema
En `src/input.css` definí con `@theme` los seis colores de la marca (Verde Ruta,
Naranja Pedal, Azul Noche, Crema, Gris Asfalto y Amarillo Farol) y las fuentes
Montserrat (`font-titulos`) y Open Sans (`font-cuerpo`), cargadas desde Google Fonts.
Con `--color-*: initial` eliminé la paleta genérica de Tailwind.

### Modo oscuro
Estrategia por defecto (`prefers-color-scheme`). Sin prefijo es el modo claro; `dark:`
cambia fondos, textos, cards, bordes, campos y foco.

### Contraste (WCAG, mínimo 4.5:1)
| Texto | Fondo | Proporción | ¿Cumple? | Qué hice |
|---|---|---|---|---|
| (llena con los resultados que obtuviste en WebAIM) | | | | |

Verde Ruta sobre Azul Noche dio aproximadamente 3.0, no cumple. En modo oscuro no uso
verde como texto: los acentos y el botón principal pasan a Amarillo Farol.
Gris Asfalto sobre Azul Noche dio aproximadamente 2.7: en modo oscuro uso Crema al 70 %.

### Pruebas
Emulé `prefers-color-scheme: dark` en DevTools. Todas las secciones cambian y el modo
claro sigue funcionando.