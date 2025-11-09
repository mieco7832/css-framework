# CSS Base Framework

Este conjunto de hojas de estilo define una estructura modular para construir interfaces limpias y consistentes sin depender de frameworks externos.  
Está dividido en dos archivos principales:

- **root.css:** contiene todas las variables globales, escalas de espaciado, paleta de colores, tipografía, radios, sombras y transiciones.
- **index.css:** agrupa las reglas y utilidades que implementan los estilos base, incluyendo helpers de margen, padding, display, grid, tablas, listas, formularios y componentes visuales.

El objetivo es ofrecer un sistema simple, descriptivo y fácil de mantener, donde los nombres de clases reflejan su función (`bg-blue`, `text-gray`, `border-green`, etc.), y las variables se organizan por tipo (`--blue`, `--green-dark`, `--radius-2`, `--font-family-console`, etc.).

---

## Estructura General

- **Variables globales:** definidas en `:root`, sirven como tokens reutilizables en todas las reglas.
- **Helpers:** clases rápidas (`.m-1`, `.p-2`, `.d-flex`, etc.) para composición visual.
- **Componentes base:** estilos listos para elementos comunes como tablas, alertas, botones y formularios.
- **Consistencia cromática:** todos los colores siguen el patrón `color`, `dark-color`, `light-color`, `color-hover`, `deep-color`.

---

A partir de aquí se documentarán las secciones principales:  

1. Variables (`root.css`)  
2. Helpers (`index.css`)  
3. Componentes visuales  
4. Buenas prácticas de uso  
5. Ejemplos prácticos de integración

## 1. Variables Globales (`root.css`)

El archivo `root.css` define todas las variables globales dentro del selector `:root`.  
Estas variables actúan como tokens reutilizables para colores, tamaños, tipografías, sombras y animaciones.

---

### Colores Base

Los colores siguen un patrón uniforme con variantes `dark`, `light`, `hover` y `deep` para mantener consistencia tonal.

| Nombre | Descripción | Ejemplo |
|---------|--------------|---------|
| `--blue`, `--blue-dark`, `--light-blue`, `--blue-hover`, `--blue-deep` | Gama azul usada en botones, enlaces y encabezados. | `steelblue` → `#145ca8` |
| `--green`, `--green-dark`, `--light-green`, `--green-hover`, `--green-deep` | Verde para estados de éxito o confirmación. | `#82B366` → `#0b3d0b` |
| `--red`, `--red-dark`, `--light-red`, `--red-hover`, `--red-deep` | Rojo para errores, alertas o avisos críticos. | `#e09a9a` → `#b71c1c` |
| `--yellow`, `--yellow-dark`, `--light-yellow`, `--yellow-hover`, `--yellow-deep` | Amarillo para advertencias o mensajes informativos. | `#f0d38d` → `#b58900` |
| `--gray-100` ... `--gray-900` | Escala neutra utilizada en fondos, bordes y tipografía. | De `#f5f6f7` a `#263238` |
| `--white`, `--black`, `--dark` | Tonos básicos y de contraste. | `#fff`, `#000`, `#333` |
| `--muted`, `--muted-strong` | Colores de texto secundarios o desactivados. | `#666`, `#222` |

---

### Sombras y Opacidad

| Variable | Descripción |
|-----------|-------------|
| `--shadow-light` | Sombras sutiles para elementos pequeños o botones. |
| `--shadow-medium` | Sombra intermedia para tarjetas o modales. |
| `--shadow-strong` | Sombra intensa para overlays o capas principales. |
| `--shadow-1`, `--shadow-2`, `--shadow-3` | Escala uniforme de profundidad visual. |
| `--overlay` | Color semitransparente para fondos de modales (`rgba(0,0,0,0.5)`). |

---

### Tipografía

| Variable | Uso |
|-----------|-----|
| `--font-family-base` | Fuente principal del sitio (`"Segoe UI", system-ui, Arial`). |
| `--font-family-console` | Fuente monoespaciada para bloques de código (`"Cascadia Code", "Fira Code"`, etc.). |
| `--font-size-xs` a `--font-size-xl` | Escala tipográfica estándar (`.8125rem` a `1.25rem`). |
| `--line-height-base` | Altura de línea predeterminada (`1.5`). |

---

### Espaciado y Layout

| Variable | Descripción |
|-----------|-------------|
| `--space-0` a `--space-5` | Escala de espaciado base (`0` → `3rem`). |
| `--radius-1` a `--radius-4` | Radios de borde para esquinas suaves (`4px` a `20px`). |
| `--container-sm`, `--container-md`, `--container-lg`, `--container-xl` | Anchos máximos de contenedor (540px a 1140px). |

---

### Transiciones

| Variable | Descripción |
|-----------|-------------|
| `--transition-fast` | Transición rápida (120 ms). |
| `--transition-base` | Transición estándar (200 ms). |
| `--transition-slow` | Transición suave (320 ms). |

Estas variables conforman la base visual del framework y son utilizadas en todos los módulos de `index.css`.  
El uso de nombres descriptivos y la ausencia de conceptos como *primary* o *secondary* permite mantener un sistema semántico claro y predecible.

---

### Ejemplo de uso

```css
button {
  background-color: var(--blue);
  color: var(--white);
  border-radius: var(--radius-2);
  transition: background-color var(--transition-base);
}

button:hover {
  background-color: var(--blue-hover);
}
```

## 2. Helpers (`index.css`)

Los *helpers* son clases utilitarias que aplican estilos directos, evitando escribir reglas CSS adicionales.  
Usan una sintaxis clara y predecible: `[propiedad]-[valor]`.  
Ejemplo: `.m-2`, `.bg-blue`, `.text-center`.

---

### 2.1 Espaciado

Basado en la escala `--space-0` a `--space-5` definida en `root.css`.

| Clases | Descripción |
|---------|-------------|
| `.m-*`, `.mt-*`, `.mb-*`, `.ms-*`, `.me-*`, `.mx-*`, `.my-*` | Márgenes (top, bottom, start, end, eje X/Y). |
| `.p-*`, `.pt-*`, `.pb-*`, `.ps-*`, `.pe-*`, `.px-*`, `.py-*` | Paddings con la misma escala. |
| `.m-auto`, `.mx-auto`, `.my-auto` | Centra horizontal o verticalmente. |

Ejemplo:

```html
<div class="mt-3 mb-2 p-3">...</div>
```

---

### 2.2 Display y Flexbox

| Clases | Descripción |
|---------|-------------|
| `.d-none`, `.d-block`, `.d-inline`, `.d-inline-block` | Cambia el tipo de display. |
| `.d-flex`, `.d-inline-flex`, `.d-grid`, `.d-inline-grid` | Activa layouts flexibles o de cuadrícula. |
| `.flex-row`, `.flex-column`, `.flex-wrap`, `.flex-nowrap` | Dirección y envoltura de elementos. |
| `.justify-*` | Alineación horizontal (`start`, `center`, `end`, `between`, `around`). |
| `.align-*` | Alineación vertical (`start`, `center`, `end`). |
| `.flex-[1..12]` | Escala proporcional de crecimiento. |

Ejemplo:

```html
<div class="d-flex justify-between align-center">
  <span>Texto</span>
  <button>Acción</button>
</div>
```

---

### 📍 2.3 Posicionamiento

| Clases | Descripción |
|---------|-------------|
| `.position-static`, `.position-relative`, `.position-absolute`, `.position-fixed`, `.position-sticky` | Define tipo de posición. |
| `.top-0`, `.bottom-0`, `.start-0`, `.end-0` | Posiciona el elemento por borde. |
| `.center-xy`, `.top-50`, `.left-50` | Centrado absoluto. |
| `.z-0`, `.z-1`, `.z-10`, `.z-100`, `.z-max` | Control de z-index. |

Ejemplo:

```html
<div class="position-absolute top-0 end-0">...</div>
```

---

### 2.4 Colores de fondo y texto

Todos los colores provienen de las variables de `root.css`.

| Clases | Descripción |
|---------|-------------|
| `.bg-[color]` | Cambia color de fondo (`white`, `blue`, `green`, `red`, `yellow`, etc.). |
| `.text-[color]` | Cambia color del texto. |
| `.text-muted`, `.text-muted-strong` | Colores secundarios o desactivados. |

Ejemplo:

```html
<p class="text-blue bg-light-blue">Texto con fondo azul claro</p>
```

---

### 2.5 Tamaños y dimensiones

| Clases | Descripción |
|---------|-------------|
| `.w-*`, `.h-*` | Ancho o alto absoluto (`25vw`, `100vh`, etc.). |
| `.w-per-*`, `.h-per-*` | Ancho o alto relativo en porcentaje. |
| `.min-w-*`, `.max-w-*`, `.min-h-*`, `.max-h-*` | Límites de tamaño. |
| `.gap-*` | Espacio entre elementos en `flex` o `grid`. |

Ejemplo:

```html
<section class="h-100 w-per-75 d-flex align-center justify-center">...</section>
```

---

### 2.6 Bordes, radios y sombras

| Clases | Descripción |
|---------|-------------|
| `.border-[color]` | Color del borde (`gray`, `blue`, `green`, etc.). |
| `.border-0` a `.border-5` | Grosor del borde. |
| `.border-solid`, `.border-dashed`, `.border-dotted` | Estilo de borde. |
| `.rounded-0` a `.rounded-4`, `.rounded-circle` | Radio de borde según `--radius-*`. |

Ejemplo:

```html
<div class="border-blue border-2 rounded-2 p-3">Caja con borde azul</div>
```

---

### 2.7 Tipografía y alineación

| Clases | Descripción |
|---------|-------------|
| `.font-[400..900]` | Peso tipográfico. |
| `.font-small`, `.font-medium`, `.font-large` | Tamaños predefinidos. |
| `.text-left`, `.text-center`, `.text-right`, `.text-justify` | Alineación del texto. |
| `.lh-tight`, `.lh-normal`, `.lh-loose` | Control de `line-height`. |
| `.text-select-none` | Desactiva selección de texto. |

Ejemplo:

```html
<h2 class="font-700 text-center text-blue">Título principal</h2>
```

---

### 2.8 Overflow y cursor

| Clases | Descripción |
|---------|-------------|
| `.overflow-hidden`, `.overflow-auto`, `.overflow-visible` | Controla desbordamiento. |
| `.cursor-pointer`, `.cursor-not-allowed`, `.cursor-default` | Cambia el tipo de cursor. |

Ejemplo:

```html
<div class="overflow-auto cursor-pointer">...</div>
```

---

### 2.9 Layout y contenedor

| Clases | Descripción |
|---------|-------------|
| `.container` | Centra contenido y ajusta ancho según el viewport. |
| `.row`, `.col-*`, `.col-md-*` | Sistema de cuadrícula basado en flexbox. |
| `.d-flex-m-column` | Variante responsive para móviles. |

Ejemplo:

```html
<div class="container">
  <div class="row">
    <div class="col-6">Columna 1</div>
    <div class="col-6">Columna 2</div>
  </div>
</div>
```

---

### 2.10 Media Queries

El sistema usa dos puntos de ruptura principales:

| Breakpoint | Descripción |
|-------------|-------------|
| `@media (max-width: 900px)` | Ajustes en navegación, disposición vertical y layouts móviles. |
| `@media (max-width: 600px)` | Simplificación de componentes como modales y formularios. |

---

Los *helpers* constituyen la base del framework:  
permiten una construcción rápida, semántica y reutilizable de cualquier estructura visual sin dependencias externas.

---

## 3. Componentes visuales

Componentes listos para usar, construidos sobre variables (`root.css`) y helpers (`index.css`). Cada bloque incluye propósito, clases clave y un ejemplo breve.

### 3.1 Botones

**Clases:** `.btn`, `.btn-sm`, `.btn-lg`, `.btn-blue`, `.btn-green`, `.btn-red`  
**Uso:** acciones principales/secundarias con estados hover consistentes.

```html
<button class="btn btn-blue">Confirmar</button>
<button class="btn btn-green btn-sm">Guardar</button>
<button class="btn btn-red btn-lg">Eliminar</button>
```

Notas:

- Colores de fondo: usan variables `--blue-soft`, `--green-soft`, `--red-soft` para contraste adecuado.
- Hover: elevación mediante sombra `--shadow-2`.

---

### 3.2 Alertas (notificaciones)

**Clases:** `.alert`, `.alert.success`, `.alert.danger`, `.alert.warning`, `.alert.info`, `.hidden`

```html
<div class="alert success" role="status">
  <strong class="title">Listo</strong>
  <span class="message">Se guardó correctamente.</span>
  <button aria-label="Cerrar">×</button>
</div>
```

Notas:

- Paletas basadas en `light-*` con bordes del color medio y texto `*-dark`.
- `.hidden` para transición de salida.

---

### 3.3 Modal

**Clases:** `.modal`, `.modal.hidden`, `.modal-content`, `.modal-body`

```html
<div class="modal">
  <div class="modal-content">
    <h3 class="title">Título</h3>
    <button class="close" aria-label="Cerrar">×</button>
    <div class="modal-body">Contenido...</div>
  </div>
</div>
```

Notas:

- Fondo `--overlay`, profundidad `--shadow-3` y animación `modalFadeIn`.
- Ocultar/mostrar con `.hidden`.

---

### 3.4 Formularios

#### 3.4.1 Tarjeta de formulario

**Clases:** `form.card-form`

```html
<form class="card-form">
  <h3>Ingreso</h3>
  <!-- campos -->
  <button>Entrar</button>
</form>
```

#### 3.4.2 Label flotante

**Clases:** `.label-float > input|textarea|select + label`

```html
<div class="label-float">
  <input placeholder=" " id="user">
  <label for="user">Usuario</label>
</div>
```

#### 3.4.3 Grupo de entrada con botón

**Clases:** `.input-group`, `.input-group .btn`

```html
<div class="input-group">
  <div class="label-float">
    <input placeholder=" " id="token">
    <label for="token">Token</label>
  </div>
  <button class="btn" aria-label="Copiar"><i></i></button>
</div>
```

#### 3.4.4 Checkbox estandarizado

**Clases:** `.chex-box`

```html
<div class="chex-box">
  <input type="checkbox" id="remember">
  <label for="remember">Recordar</label>
  <span class="text-light-gray">Mantener sesión</span>
</div>
```

---

### 3.5 Tablas

**Clases:** `.table`, `.table-striped`, `.table-hover`, `.table-bordered`, `.table-rounded`, `.table-responsive`, `.caption-top`, `.table-[blue|green|red|yellow]`

```html
<div class="table-responsive">
  <table class="table table-striped table-hover table-rounded">
    <caption>Listado</caption>
    <thead class="table-blue">
      <tr><th>Nombre</th><th>Estado</th></tr>
    </thead>
    <tbody>
      <tr><td>Elemento A</td><td>OK</td></tr>
      <tr><td>Elemento B</td><td>Error</td></tr>
    </tbody>
  </table>
</div>
```

Notas:

- `table-*` de color aplica sólo en `<th>` para contraste.
- `table-responsive` agrega scroll horizontal en móviles.

---

### 3.6 Listas

#### 3.6.1 Lista tipo tabla

**Clases:** `.list-table`, `.table-striped`, `.table-hover`, `.table-rounded`

```html
<ul class="list-table table-striped table-hover table-rounded">
  <li>
    <div class="cell col-1">#1</div>
    <div class="cell col-2">Item</div>
    <div class="cell col-end">100</div>
  </li>
</ul>
```

#### 3.6.2 Bullets y diamantes

**Clases:** `.list-bullets`, `.list-diamonds`

```html
<ul class="list-bullets">
  <li>Uno</li><li>Dos</li><li>Tres</li>
</ul>
<ul class="list-diamonds">
  <li>Alpha</li><li>Beta</li>
</ul>
```

#### 3.6.3 Enumeración

**Clases:** `.list-enum`, `.list-enum-compact`

```html
<ol class="list-enum list-enum-compact">
  <li>Paso</li><li>Paso</li>
</ol>
```

---

### 3.7 Árbol de archivos

**Clases:** `ul.files-root`, `li.directory`, `li.file`

```html
<ul class="files-root">
  <li class="directory">src
    <ul>
      <li class="file">index.ts</li>
    </ul>
  </li>
</ul>
```

---

### 3.8 Navegación

**Clases:** `nav`, `nav ul`, `nav button`

```html
<nav>
  <ul>
    <li>Inicio</li>
    <li>Docs</li>
  </ul>
  <button>Salir</button>
</nav>
```

Notas:

- Sticky top, borde inferior y transiciones suaves en hover.

---

### 3.9 Tarjetas

**Clases:** `.card`, `.card-hover`, `.card-content`

```html
<article class="card card-hover">
  <h3>Título</h3>
  <div class="card-content">
    <i class="icon-JAVA" aria-hidden="true"></i>
    <p>Contenido</p>
  </div>
</article>
```

---

### 3.10 Consola / Código

**Clases sugeridas:** `code, pre, .console` con `--font-family-console`

```html
<pre class="text-console">Log de ejemplo...</pre>
```

Sugerencia de estilo mínimo:

```css
code, pre, .console {
  font-family: var(--font-family-console);
  font-size: 0.95rem;
  background: var(--bg-soft);
  color: var(--dark);
  padding: .5rem .75rem;
  border-radius: var(--radius-1);
}
```

---

## 4. Buenas prácticas de uso

Esta sección describe lineamientos generales para mantener consistencia y escalabilidad en el uso del framework CSS.  
Las reglas se enfocan en simplicidad, legibilidad y reutilización, evitando estilos redundantes o dependientes de contexto.

---

### 4.1 Convenciones de nomenclatura

- **Prefijos claros:** cada clase debe reflejar su función (`bg-`, `text-`, `border-`, `m-`, `p-`, etc.).
- **Variables semánticas:** usa los nombres de color directamente (`--blue`, `--dark-green`, `--light-yellow`, `--deep-red`).
- **Clases reutilizables:** evita combinaciones únicas. Crea helpers antes que reglas específicas.
- **Evita abreviaciones no estándar:** toda clase debe ser comprensible sin referencia externa.

Ejemplo correcto:

```html
<div class="bg-blue text-white p-3 rounded-2">Confirmado</div>
```

Ejemplo incorrecto:

```html
<div class="bg--blue text--white">Confirmado</div>
```

---

### 4.2 Jerarquía y especificidad

- Usa clases antes que selectores de tipo (`div`, `p`, etc.).
- Evita anidamientos profundos o dependencias de jerarquía.
- Prefiere clases pequeñas y combinables.

```html
<section class="container p-4">
  <article class="card card-hover text-blue">...</article>
</section>
```

---

### 4.3 Variables como punto central

- Cualquier cambio visual debe gestionarse desde `root.css`.
- No redefinas colores o tamaños directamente en reglas locales.
- Las variables permiten mantener la armonía cromática y escalar estilos sin ruptura.

Ejemplo:

```css
.badge {
  background-color: var(--green);
  color: var(--white);
  border-radius: var(--radius-1);
}
```

---

### 4.4 Uso combinado de helpers

Los helpers son acumulativos. Se pueden mezclar libremente según la necesidad del layout.

```html
<div class="d-flex align-center justify-between bg-light-blue p-3 rounded-2">
  <span>Etiqueta</span>
  <button class="btn btn-green">Acción</button>
</div>
```

---

### 4.5 Recomendaciones de componentes

| Elemento | Recomendación |
|-----------|----------------|
| Botones | Utiliza colores `light-*` para fondo y `dark-*` para texto. |
| Alertas | Mantén contraste suficiente entre texto y fondo. |
| Formularios | Usa `.label-float` y evita `placeholder` como único texto guía. |
| Tablas | Usa `.table-rounded` y `.table-hover` para accesibilidad visual. |
| Listas | Prefiere `.list-enum` o `.list-diamonds` según jerarquía. |

---

### 4.6 Responsividad

- Usa el sistema de contenedores (`.container`, `.row`, `.col-*`) para estructuras adaptables.
- Aprovecha los breakpoints integrados (`900px`, `600px`) para modificar disposición.
- Combina con helpers (`.d-flex-m-column`, `.w-per-100`) para vistas móviles.

---

### 4.7 Versionado y extensión

- Guarda personalizaciones adicionales en archivos separados (`custom.css`, `theme.css`).
- Mantén `root.css` y `index.css` sin modificaciones directas para facilitar actualización.
- Documenta nuevas variables y helpers siguiendo el formato actual.

---

## 5. Ejemplos prácticos  

Los siguientes ejemplos muestran el uso aplicado de los helpers más utilizados.   Comenzamos con los que modifican las **dimensiones** y el **espaciado** de los elementos.  ---  ## 5.1 Helpers de dimensión y espaciado  Estos helpers permiten ajustar márgenes, rellenos y tamaños sin escribir reglas CSS personalizadas.   Usan la escala de variables `--space-0` a `--space-5` y los valores porcentuales o relativos definidos en `root.css`.  

### Márgenes (`m-*`, `mt-*`, `mb-*`, `ms-*`, `me-*`, `mx-*`, `my-*`)  

```html
<div class="bg-light-blue p-3 m-3 rounded-2">   
    <p class="text-blue">Caja con margen general (.m-3)</p> 
</div>
<div class="bg-light-green p-3 mt-5 rounded-2">
    <p class="text-green">Caja con margen superior grande (.mt-5)</p> 
</div>  
<div class="bg-light-red p-3 mx-auto w-50 rounded-2">
    <p class="text-red text-center">Caja centrada horizontalmente (.mx-auto)</p> 
</div>
```

**Explicación:**

- `.m-*` aplica un margen uniforme.  
- `.mt-*`, `.mb-*`, `.ms-*`, `.me-*` controlan lados específicos.
- `.mx-auto` centra un bloque horizontalmente dentro de su contenedor.

---

### Relleno interno (`p-*`, `pt-*`, `pb-*`, `ps-*`, `pe-*`, `px-*`, `py-*`)

```html
<div class="bg-blue p-5 rounded-3 text-white">
    <p>Relleno general (.p-5)</p> 
</div>

<div class="bg-green py-2 px-4 rounded-3 text-white mt-3">
    <p>Padding vertical 2 y horizontal 4 (.py-2 .px-4)</p> 
</div>
```

**Explicación:**

- `.p-*` define relleno uniforme.
- `.py-*` y `.px-*` afectan ejes vertical y horizontal.
- Se basan en las variables de espaciado (`--space-*`).

---

### Ancho y alto (`w-*`, `h-*`, `w-per-*`, `h-per-*`)

```html
<div class="bg-light-yellow text-dark text-center p-2 w-50 rounded-2">  
    <p>Elemento con ancho del 50% (.w-50)</p> 
</div>
<div class="bg-light-blue text-dark text-center p-2 h-25 rounded-2 mt-3">  
    <p>Elemento con alto del 25vh (.h-25)</p> 
</div>

<div class="bg-gray-300 text-dark text-center p-2 w-per-75 h-per-50 rounded-2 mt-3">
    <p>Elemento proporcional al contenedor (.w-per-75 .h-per-50)</p>
</div>
```

**Explicación:**

- `.w-*`, `.h-*` usan unidades relativas al viewport (`vw`, `vh`).
- `.w-per-*`, `.h-per-*` usan porcentaje dentro del contenedor padre.

---

### Dimensiones mínimas y máximas

```html
<div class="bg-white border-blue border-2 rounded-2 p-2 min-h-100">
    <p>El contenedor ocupa siempre al menos el alto total del viewport (.min-h-100)</p>
</div>
<div class="bg-gray-200 border-gray border-1 rounded-2 p-2 max-w-100 mt-2">
    <p>La anchura máxima se limita al ancho completo (.max-w-100)</p>
</div>
```

**Explicación:**

- `.min-h-*`, `.min-w-*`, `.max-h-*`, `.max-w-*` restringen dimensiones.
- Ideales para layouts fluidos o contenedores adaptativos.

---

Estos helpers constituyen la base de todo el sistema visual, permiten definir **espaciado, proporciones y alineación** sin escribir código adicional.

## 5.2 Helpers de display, flex y posición

Estos helpers controlan cómo se muestran los elementos, su orientación y su alineación dentro del flujo del documento.  
Permiten crear layouts flexibles sin escribir CSS personalizado.

---

### Display (`d-*`)

Clases para cambiar rápidamente el tipo de visualización del elemento.

| Clase | Descripción |
|-------|-------------|
| `.d-none` | Oculta el elemento (`display: none`). |
| `.d-block` | Lo convierte en bloque (`display: block`). |
| `.d-inline` | Muestra como elemento en línea (`display: inline`). |
| `.d-inline-block` | En línea, pero con propiedades de bloque. |
| `.d-flex`, `.d-inline-flex` | Activa un contenedor flex. |
| `.d-grid`, `.d-inline-grid` | Activa un contenedor de tipo grid. |

Ejemplo:

```html
<div class="d-flex justify-between align-center bg-gray-100 p-2 rounded-2">
    <span>Etiqueta</span>
    <button class="btn btn-blue">Acción</button>
</div>
```

---

### Flexbox (dirección y envoltura)

| Clase | Descripción |
|-------|-------------|
|`.flex-row`, `.flex-column`|Define la dirección principal.|
|`.flex-wrap`, `.flex-nowrap` |Controla si los ítems se ajustan o no al ancho.|
|`.flex-row-reverse`, `.flex-column-reverse`|Invierte el orden natural.|
|`.flex-[1..12]`|Asigna proporciones de crecimiento (flex: n).|

```html
<div class="d-flex flex-row-wrap gap-2 bg-light-blue p-3 rounded-2">
    <div class="bg-blue text-white p-2 flex-1">1</div>
    <div class="bg-green text-white p-2 flex-2">2</div>
    <div class="bg-red text-white p-2 flex-3">3</div>
</div>
```

---

### 🎯 Justificación y alineación

|Clase|Propiedad|Valor aplicado|
|---|---|---|
|`.justify-start`|`justify-content`|`flex-start`|
|`.justify-center`|`justify-content`|`center`|
|`.justify-end`|`justify-content`|`flex-end`|
|`.justify-between`|`justify-content`|`space-between`|
|`.justify-around`|`justify-content`|`space-around`|
|`.align-start`|`align-items`|`flex-start`|
|`.align-center`|`align-items`|`center`|
|`.align-end`|`align-items`|`flex-end`|

Ejemplo:

```html
<div class="d-flex justify-around align-center bg-light-green p-3 rounded-2">
    <div class="bg-green text-white p-2 rounded-1">A</div>
    <div class="bg-green text-white p-2 rounded-1">B</div>
    <div class="bg-green text-white p-2 rounded-1">C</div>
</div>
```

---

### Posicionamiento (`position-*`, `top-*`, `z-*`)

|Clase|Descripción|
|---|---|
|`.position-static`, `.position-relative`, `.position-absolute`, `.position-fixed`, `.position-sticky`|Define el modelo de posicionamiento.|
|`.top-0`, `.bottom-0`, `.start-0`, `.end-0`|Ancla el elemento a un borde.|
|`.top-50`, `.left-50`|Centra el elemento en un eje con `transform: translate`.|
|`.center-xy`|Centra completamente el elemento (`x` y `y`).|
|`.z-0`, `.z-1`, `.z-10`, `.z-100`, `.z-max`|Controla el nivel de apilamiento.|

Ejemplo:

```html
<div class="position-relative bg-gray-200 h-100">
    <div class="position-absolute center-xy bg-blue text-white p-3 rounded-2">Centrado con .center-xy</div>
</div>
```

---

### 🔢 Capas y orden visual (`z-*`)

Los valores de `z-index` predefinidos facilitan el control de superposición entre componentes.

|Clase|Valor|
|---|---|
|`.z-0`|0|
|`.z-1`|1|
|`.z-10`|10|
|`.z-100`|100|
|`.z-max`|9999|

Ejemplo:

```html
<div class="position-relative h-50">
    <div class="position-absolute top-0 start-0 bg-red text-white p-2 z-1">Nivel 1</div>
    <div class="position-absolute top-2 start-2 bg-blue text-white p-2 z-10">Nivel 10</div>
    <div class="position-absolute top-4 start-4 bg-green text-white p-2 z-max">Nivel máximo</div>
</div>
```

Estos helpers proporcionan control total sobre la disposición visual de los elementos.  
Son la base para construir layouts flexibles, responsivos y estructurados sin escribir reglas adicionales.

## 5.3 Helpers de texto y color

Estos helpers controlan el color, alineación, peso tipográfico y tamaño de la fuente.  
Permiten mantener una jerarquía visual clara y uniforme en cualquier parte de la interfaz.

---

### 🎨 Colores de texto (`text-[color]`)

Los colores se basan en las variables definidas en `root.css` y mantienen el mismo patrón cromático que los fondos.

| Clase | Color asociado | Descripción |
|--------|----------------|-------------|
| `.text-black` | `--black` | Texto negro absoluto. |
| `.text-white` | `--white` | Texto blanco, para fondos oscuros. |
| `.text-dark` | `--dark` | Texto gris oscuro estándar. |
| `.text-gray` | `--gray-400` | Texto neutro. |
| `.text-light-gray` | `--gray-300` | Texto atenuado. |
| `.text-blue`, `.text-green`, `.text-red`, `.text-yellow` | `--blue`, `--green`, `--red`, `--yellow` | Tonos temáticos principales. |
| `.text-deep-red` | `--deep-red` | Tono más fuerte, ideal para alertas críticas. |
| `.text-light-blue`, `.text-light-yellow` | `--light-blue`, `--light-yellow` | Versiones suaves para fondos claros. |
| `.text-muted`, `.text-muted-strong` | `--muted`, `--muted-strong`| Texto desactivado o secundario. |

Ejemplo:

```html
<p class="text-blue">Texto azul principal</p>
<p class="text-green">Texto verde (éxito)</p>
<p class="text-muted">Texto desactivado o descriptivo</p>
```

---

### Alineación del texto

| Clase           | Descripción             |
| --------------- | ----------------------- |
| `.text-left`    | Alinea a la izquierda.  |
| `.text-center`  | Centra horizontalmente. |
| `.text-right`   | Alinea a la derecha.    |
| `.text-justify` | Justifica el contenido. |

Ejemplo:

```html
<p class="text-center text-blue">Texto centrado y azul</p>
<p class="text-justify text-dark">Lorem ipsum dolor sit amet...</p>
```

### Tamaño y peso tipográfico

| Clase                     | Descripción                                   |
| ------------------------- | --------------------------------------------- |
| `.font-400` a `.font-900` | Controla el grosor del texto (`font-weight`). |
| `.font-small`             | Tamaño reducido (`0.9rem`).                   |
| `.font-medium`            | Tamaño base (`1rem`).                         |
| `.font-large`             | Tamaño destacado (`1.2rem`).                  |

Ejemplo:

```html
<h2 class="font-700 text-dark">Encabezado con peso 700</h2>
<p class="font-small text-gray">Texto descriptivo en tamaño pequeño</p>
```

### Selección y comportamiento

| Clase               | Descripción                             |
| ------------------- | --------------------------------------- |
| `.text-select-none` | Evita que el texto pueda seleccionarse. |

Ejemplo:

```html
<p class="text-select-none text-gray">
  Este texto no puede seleccionarse con el cursor.
</p>
```

Estos helpers permiten mantener una coherencia visual y tipográfica en toda la aplicación,
facilitando la personalización de títulos, subtítulos y descripciones sin alterar el CSS base.

## 5.4 Helpers de borde, radios y sombras

Estos helpers controlan el estilo, color, grosor y radio de los bordes, además de aplicar sombras predefinidas para aportar profundidad visual.

---

### Bordes (`border-[color]`)

| Clase                                                                          | Descripción                                              |
| ------------------------------------------------------------------------------ | -------------------------------------------------------- |
| `.border-solid`                                                                | Borde continuo (`solid`).                                |
| `.border-dashed`                                                               | Borde discontinuo (`dashed`).                            |
| `.border-dotted`                                                               | Borde punteado (`dotted`).                               |
| `.border-none`                                                                 | Elimina cualquier borde.                                 |
| `.border-all`, `.border-top`, `.border-bottom`, `.border-start`, `.border-end` | Aplica borde en todo el elemento o en lados específicos. |

Ejemplo:

```html
<div class="border-solid border-2 border-blue p-3 rounded-1">
  <p>Borde azul sólido</p>
</div>
<div class="border-dashed border-3 border-green p-3 rounded-2 mt-2">
  <p>Borde verde discontinuo</p>
</div>
```

---

### Colores de borde (border-[color])

| Clase                                                                                  | Color asociado     |
| -------------------------------------------------------------------------------------- | ------------------ |
| `.border-white`, `.border-black`, `.border-dark`                                       | Tonos neutros.     |
| `.border-gray`, `.border-light-gray`                                                   | Escala de grises.  |
| `.border-blue`, `.border-green`, `.border-red`, `.border-yellow`, `.border-light-blue` | Colores temáticos. |

Ejemplo:

```html
<div class="border-3 border-red border-solid rounded-2 p-2 text-red">
  Borde rojo con radio medio
</div>
```

---

Grosor del borde (border-[0..5])

| Clase       | Valor aplicado |
| ----------- | -------------- |
| `.border-0` | 0 px           |
| `.border-1` | 1 px           |
| `.border-2` | 2 px           |
| `.border-3` | 3 px           |
| `.border-4` | 4 px           |
| `.border-5` | 5 px           |

Ejemplo:

```html
<div class="border-1 border-gray rounded-1 p-2">Borde fino</div>
<div class="border-5 border-blue rounded-3 p-2 mt-2">Borde grueso</div>
```

---

### Radios de borde (rounded-*)

Basados en las variables `--radius-*` definidas en root.css.

| Clase             | Valor aplicado            |
| ----------------- | ------------------------- |
| `.rounded-0`      | `0`                       |
| `.rounded-1`      | `var(--radius-1)` (4 px)  |
| `.rounded-2`      | `var(--radius-2)` (8 px)  |
| `.rounded-3`      | `var(--radius-3)` (12 px) |
| `.rounded-4`      | `var(--radius-4)` (20 px) |
| `.rounded-circle` | `50%` (forma circular)    |

Ejemplo:

```html
<div class="border-blue border-2 rounded-4 p-3 text-center">
  Borde con esquinas amplias (.rounded-4)
</div>
<div class="border-green border-2 rounded-circle p-3 text-center w-25 h-25">
  Circular
</div>
```

---

### Sombras predefinidas (shadow-*)

Los helpers de sombra utilizan las variables globales `--shadow-1`, `--shadow-2`, `--shadow-3`.

| Clase            | Descripción         |
| ---------------- | ------------------- |
| `.shadow-light`  | Sombra sutil.       |
| `.shadow-medium` | Sombra intermedia.  |
| `.shadow-strong` | Sombra pronunciada. |

Estos helpers permiten generar cajas, botones o tarjetas con bordes y profundidad visual de forma coherente y uniforme, manteniendo el diseño limpio y jerárquico.

## 5.5 Helpers de contenedor y cuadrícula

Estos helpers definen la estructura base de layout del sistema, usando un modelo de contenedor–fila–columna inspirado en flexbox.
Permiten construir distribuciones responsivas sin necesidad de escribir reglas personalizadas.

---

### Contenedor (.container)

El contenedor centraliza el contenido y define un ancho máximo variable según el tamaño de pantalla.
Utiliza las variables `--container-sm` a `--container-xl` para cada punto de ruptura.

| Breakpoint          | Ancho máximo aplicado     |
| ------------------- | ------------------------- |
| `min-width: 576px`  | `--container-sm` (540px)  |
| `min-width: 768px`  | `--container-md` (720px)  |
| `min-width: 992px`  | `--container-lg` (960px)  |
| `min-width: 1200px` | `--container-xl` (1140px) |

Ejemplo:

```html
<div class="container bg-light-blue p-3 rounded-2">
  <h3 class="text-blue">Contenedor centrado y adaptable</h3>
</div>
```

El contenedor se centra automáticamente (`margin-left/right: auto`) y tiene relleno lateral para evitar que el contenido toque los bordes del viewport.

---

### Filas (`.row`)

La clase `.row` crea un contenedor flexible horizontal para las columnas.
Utiliza `display: flex; flex-wrap: wrap;` y aplica un margen negativo para compensar el padding de las columnas internas.

```html
<div class="row bg-gray-100 rounded-2 p-2">
  <div class="col-6 bg-light-blue p-2 text-center">Columna 1</div>
  <div class="col-6 bg-light-green p-2 text-center">Columna 2</div>
</div>
```

Características:

- Las filas pueden contener una o más columnas.
- Por defecto, las columnas se ajustan a la siguiente línea si exceden el ancho disponible.
- Permiten mezclar proporciones personalizadas (`col-3`, `col-9`, etc.).

---

### Columnas (`.col-*`)

Las columnas usan flexbox (`flex: 0 0 X%; max-width: X%;`) para establecer su ancho fijo dentro de una fila.
El sistema está basado en una grilla de 12 columnas.

| Clase     | Ancho asignado |
| --------- | -------------- |
| `.col-1`  | 8.333%         |
| `.col-2`  | 16.666%        |
| `.col-3`  | 25%            |
| `.col-4`  | 33.333%        |
| `.col-5`  | 41.666%        |
| `.col-6`  | 50%            |
| `.col-7`  | 58.333%        |
| `.col-8`  | 66.666%        |
| `.col-9`  | 75%            |
| `.col-10` | 83.333%        |
| `.col-11` | 91.666%        |
| `.col-12` | 100%           |

Ejemplo:

```html
<div class="row">
  <div class="col-4 bg-light-blue p-2 text-center">.col-4</div>
  <div class="col-8 bg-light-green p-2 text-center">.col-8</div>
</div>
```

**Notas:**

- `.col` sin número se comporta como una columna flexible (`flex: 1 1 0`), ocupando el espacio restante.
- Todas las columnas incluyen un padding horizontal de `0.5rem` para separación uniforme.

### Columnas responsivas (.col-md-*)

Estas variantes se activan a partir de 768px de ancho, permitiendo ajustar la distribución en pantallas medianas y grandes.

```html
<div class="row">
  <div class="col-12 col-md-6 bg-light-blue p-2 text-center">50% en desktop</div>
  <div class="col-12 col-md-6 bg-light-green p-2 text-center">50% en desktop</div>
</div>
```

**Explicación:**

- En móviles (`<768px`), ambas columnas ocupan el 100% (`.col-12`).
- En pantallas medianas o mayores, cada una ocupa la mitad del ancho (`.col-md-6`).

### Ejemplo completo de layout

```html
<section class="container">
  <div class="row">
    <div class="col-12 text-center p-3 bg-light-blue rounded-2 mb-3">
      <h2 class="text-blue font-700">Encabezado principal</h2>
    </div>

    <div class="col-3 bg-light-green p-2 rounded-2 text-center">.col-3</div>
    <div class="col-6 bg-light-yellow p-2 rounded-2 text-center">.col-6</div>
    <div class="col-3 bg-light-red p-2 rounded-2 text-center">.col-3</div>
  </div>
</section>
```

**Resultado:**

- Encabezado centrado arriba.
- Tres columnas distribuidas proporcionalmente.
- Total de 12 unidades de ancho por fila (3 + 6 + 3).

### Helpers complementarios

| Clase                  | Descripción                                                                 |
| ---------------------- | --------------------------------------------------------------------------- |
| `.d-flex-m-column`     | Convierte un layout horizontal a vertical en pantallas pequeñas (`<900px`). |
| `.mx-auto`, `.my-auto` | Centran elementos dentro del contenedor.                                    |
| `.gap-*`               | Espaciado entre columnas o elementos flex.                                  |

Este sistema de cuadrícula es fluido, flexible y sin dependencias externas, ideal para crear layouts responsivos y ordenados en proyectos personalizados.

---

## 5.6 Componente de navegación (`nav`)

El componente **`nav`** define una barra de navegación horizontal simple, adaptable y visualmente limpia.
Está diseñado para mantenerse fijo en la parte superior del viewport y ofrecer distribución flexible de elementos (logo, menús, botones de acción, etc.).

---

### 🧭 Estructura base

```html
<nav>
  <ul>
    <li>Inicio</li>
    <li>Documentación</li>
    <li>Contacto</li>
  </ul>
  <button>Salir</button>
</nav>
```

**Resultado:**

- Menú alineado a la izquierda (`ul > li`)
- Botón alineado a la derecha
- Fondo blanco y borde inferior gris

---

### 🎨 Estilo general

El contenedor `nav` utiliza flexbox para alinear los elementos de forma horizontal y centrada verticalmente.

| Propiedad          | Valor                                          |
| ------------------ | ---------------------------------------------- |
| `display`          | `flex`                                         |
| `justify-content`  | `space-between`                                |
| `align-items`      | `center`                                       |
| `background-color` | `var(--white)`                                 |
| `border-bottom`    | `1px solid var(--gray-300)`                    |
| `padding`          | `.6rem 1.2rem`                                 |
| `position`         | `sticky` (se mantiene visible al hacer scroll) |
| `top`              | `0`                                            |
| `z-index`          | `100` (prioridad visual sobre el contenido)    |

---

### 🔗 Elementos internos (`ul` y `li`)

```css
nav ul {
  list-style: none;
  display: flex;
  gap: 1.5rem;
}

nav ul li {
  cursor: pointer;
  color: var(--dark);
  font-weight: 500;
  transition: color var(--transition-base), transform var(--transition-base);
}

nav ul li:hover {
  color: var(--dark-blue);
  transform: translateY(-2px);
}
```

**Comportamiento:**

- Los enlaces se muestran en línea con separación (`gap: 1.5rem`).
- Transición suave de color y leve desplazamiento hacia arriba al pasar el cursor.
- Colores gestionados por variables (`--dark`, `--dark-blue`).

Ejemplo:

```html
<nav>
  <ul>
    <li>Inicio</li>
    <li>Proyectos</li>
    <li>Contacto</li>
  </ul>
  <button>Acceder</button>
</nav>
```

---

### 🔘 Botones dentro del `nav`

Los botones están diseñados para acciones destacadas (como “Salir”, “Login” o “Guardar cambios”).

```css
nav button {
  background-color: var(--deep-red);
  color: var(--white);
  border: none;
  padding: .5rem 1rem;
  border-radius: 6px;
  cursor: pointer;
  font-size: .9rem;
  font-weight: 500;
  transition: background-color var(--transition-base), transform var(--transition-base);
}

nav button:hover {
  background-color: var(--red-hover);
  transform: scale(1.05);
}
```

**Ejemplo:**

```html
<nav>
  <ul>
    <li>Dashboard</li>
    <li>Configuración</li>
  </ul>
  <button>Cerrar sesión</button>
</nav>
```

---

### 📱 Responsividad (`@media`)

En pantallas menores de **900px**, la barra de navegación se adapta automáticamente al formato vertical.

```css
@media (max-width:900px) {
  nav {
    flex-direction: column;
    align-items: stretch;
    gap: .5rem;
  }
  nav ul {
    justify-content: center;
    flex-wrap: wrap;
    gap: .8rem;
  }
  nav button {
    align-self: flex-end;
    margin-right: .5rem;
  }
}
```

**Resultado:**

- El menú y el botón se apilan verticalmente.
- Los ítems del menú se centran y distribuyen con salto de línea si es necesario.
- El botón se mantiene alineado al borde derecho.

---

### 🧩 Ejemplo completo

```html
<nav>
  <ul>
    <li>Inicio</li>
    <li>Servicios</li>
    <li>Soporte</li>
  </ul>
  <button>Salir</button>
</nav>
```

**En escritorio:** distribución horizontal con borde inferior.
**En móvil:** disposición vertical, menú centrado y botón alineado a la derecha.

---

Este componente ofrece una base sólida para una barra de navegación **minimalista, flexible y coherente con el resto del framework**, manteniendo la armonía cromática y el comportamiento responsivo del sistema.

---

Perfecto. Aquí tienes la versión **completa del componente de alertas**, lista para tu `.MD`, con ejemplos incluidos pero **seguros para Markdown** (el HTML está escapado para que no se renderice, solo se vea como ejemplo).

---

## 5.7 Componente de alertas (`.alert`)

El componente **alert** muestra mensajes temporales o persistentes para informar al usuario sobre distintos estados del sistema: éxito, error, advertencia o información.
Cada tipo de alerta combina colores, sombras y transiciones coherentes con la paleta general del framework.

---

### 🧩 Estructura base

Una alerta se compone de:

- **Contenedor principal:** `.alert`
- **Título:** `.title`
- **Mensaje:** `.message`
- **Botón de cierre:** elemento `button`

Ejemplo estructural:

```html
<div class="alert success" role="status">
  <strong class="title">Listo</strong>
  <span class="message">La operación se completó correctamente.</span>
  <button aria-label="Cerrar">×</button>
</div>
```

---

### 🎨 Estilos principales

```css
.alert{
  display:flex;
  align-items:center;
  justify-content:space-between;
  gap:12px;
  min-width:280px;
  max-width:450px;
  padding:12px 16px;
  border-radius:8px;
  font-size:15px;
  box-shadow:var(--shadow-1);
  opacity:1;
  transform:translateY(0);
  transition:all .35s ease;
  z-index:9999;
  position:fixed;
}
.alert.hidden{
  opacity:0;
  pointer-events:none;
  transform:translateY(-10px);
}
.alert .title{font-weight:600;flex-grow:1}
.alert .message{flex-grow:2;color:inherit}
.alert button{
  border:none;
  background:transparent;
  font-size:18px;
  font-weight:bold;
  color:inherit;
  cursor:pointer;
  transition:transform .2s;
}
.alert button:hover{transform:scale(1.2)}
```

---

### 🟩 Variantes de color

| Clase            | Fondo            | Borde        | Texto           |
| ---------------- | ---------------- | ------------ | --------------- |
| `.alert.success` | `--light-green`  | `--green`    | `--dark-green`  |
| `.alert.danger`  | `--light-red`    | `--red`      | `--dark-red`    |
| `.alert.warning` | `--light-yellow` | `--yellow`   | `--dark-yellow` |
| `.alert.info`    | `--gray-100`     | `--gray-400` | `--dark`        |

Cada tipo mantiene contraste y legibilidad adecuados para su propósito.

---

### 💡 Ejemplos prácticos

#### 1️ Éxito

```html
<div class="alert success">
  <strong class="title">Éxito</strong>
  <span class="message">Los datos fueron guardados correctamente.</span>
  <button>×</button>
</div>
```

#### 2️ Error

```html
<div class="alert danger">
  <strong class="title">Error</strong>
  <span class="message">No fue posible conectar con el servidor.</span>
  <button>×</button>
</div>
```

#### 3️ Advertencia

```html
<div class="alert warning">
  <strong class="title">Advertencia</strong>
  <span class="message">Revisa los campos obligatorios antes de continuar.</span>
  <button>×</button>
</div>
```

#### 4️ Información

```html
<div class="alert info">
  <strong class="title">Información</strong>
  <span class="message">Los cambios se guardan automáticamente.</span>
  <button>×</button>
</div>
```

---

### Comportamiento dinámico

- La clase `.hidden` oculta la alerta con una animación suave.
- Puede combinarse con posiciones (`top-*`, `end-*`, etc.) para definir ubicación.
- Idealmente deben mostrarse sobre el contenido principal y desaparecer tras unos segundos o al presionar el botón.

---

### 🧭 Recomendaciones

- Usa `success` para operaciones completadas.
- Usa `danger` para errores críticos.
- Usa `warning` para validaciones o avisos preventivos.
- Usa `info` para mensajes neutros o recordatorios.

---

**Ejemplo lógico de uso en interfaz:**

```.
alert success → "Operación realizada con éxito."
alert danger  → "Error al guardar los cambios."
alert warning → "Campo obligatorio faltante."
alert info    → "Los datos se actualizarán automáticamente."
```

Estas alertas mantienen la coherencia visual del framework,
aportando claridad y jerarquía en los mensajes del sistema.

---

## 5.8 Componente modal (`.modal`)

El componente **modal** permite mostrar ventanas emergentes centradas sobre el contenido principal,
bloqueando la interacción con el fondo mediante una capa semitransparente.
Se utiliza para confirmaciones, formularios o mensajes importantes.

---

### Estructura base

Un modal contiene tres elementos principales:

```.
modal (contenedor y fondo semitransparente)
 └─ modal-content (caja visible)
     ├─ title (título principal)
     ├─ button.close (botón de cierre)
     └─ modal-body (contenido interior)
```

Ejemplo estructural:

```html
<div class="modal">
  <div class="modal-content">
    <h3 class="title">Título del modal</h3>
    <button class="close" aria-label="Cerrar">×</button>
    <div class="modal-body">
      Contenido o formulario aquí.
    </div>
  </div>
</div>
```

---

### Estilos principales

```css
.modal{
  position:fixed;
  inset:0;
  display:flex;
  justify-content:center;
  align-items:center;
  background-color:var(--overlay);
  z-index:999;
  transition:opacity .25s ease,visibility .25s ease;
}
.modal.hidden{
  opacity:0;
  visibility:hidden;
  pointer-events:none;
}
.modal-content{
  background-color:var(--white);
  border-radius:8px;
  width:90%;
  max-width:480px;
  padding:1.5rem;
  box-shadow:var(--shadow-3);
  position:relative;
  animation:modalFadeIn .3s ease;
}
.modal-content .title{
  margin:0;
  font-size:1.3rem;
  font-weight:600;
  color:var(--dark);
}
.modal-content button.close{
  position:absolute;
  top:1rem;
  right:1rem;
  background:none;
  border:none;
  font-size:1.2rem;
  font-weight:bold;
  color:var(--dark);
  cursor:pointer;
  transition:color .2s;
}
.modal-content button.close:hover{
  color:var(--dark-red);
}
.modal-body{
  margin-top:1rem;
  font-size:.95rem;
  color:var(--dark);
}
@keyframes modalFadeIn{
  from{transform:translateY(-20px);opacity:0}
  to{transform:translateY(0);opacity:1}
}
```

---

### Ejemplos prácticos

#### 1️ Modal de información

```html
<div class="modal">
  <div class="modal-content">
    <h3 class="title">Información</h3>
    <button class="close">×</button>
    <div class="modal-body">
      Este es un modal informativo con contenido breve.
    </div>
  </div>
</div>
```

#### 2️ Modal de confirmación

```html
<div class="modal">
  <div class="modal-content">
    <h3 class="title">Confirmar acción</h3>
    <button class="close">×</button>
    <div class="modal-body">
      ¿Estás seguro de que deseas eliminar este elemento?<br><br>
      <button class="btn btn-red">Eliminar</button>
      <button class="btn btn-green">Cancelar</button>
    </div>
  </div>
</div>
```

#### 3️ Modal oculto (cerrado por defecto)

```html
<div class="modal hidden">
  <div class="modal-content">
    <h3 class="title">Modal oculto</h3>
    <button class="close">×</button>
    <div class="modal-body">
      Este modal se muestra al quitar la clase <code>.hidden</code>.
    </div>
  </div>
</div>
```

---

### Responsividad

```css
@media (max-width:600px){
  .modal-content{
    width:95%;
    padding:1rem;
  }
}
```

**Efecto:**
El modal se adapta al ancho del dispositivo y reduce márgenes en pantallas pequeñas.

**Comportamiento dinámico:**

- Se muestra al remover la clase `.hidden`.
- Se oculta al volver a aplicarla o al presionar el botón de cierre.
- Bloquea la interacción con el resto del contenido mientras está activo.
- Puede acompañarse de una animación de entrada o salida con `@keyframes modalFadeIn`.

---

### Recomendaciones

| Caso de uso           | Tipo de contenido recomendado             |
| --------------------- | ----------------------------------------- |
| Confirmaciones        | Botones de acción (`Aceptar`, `Cancelar`) |
| Formularios           | Campos y botones dentro de `.modal-body`  |
| Mensajes informativos | Texto breve o detalles de sistema         |

---

### Ejemplo lógico de interacción

```.
.modal.hidden → oculto y sin interacción.
.modal (visible) → se muestra con fondo oscuro.
.close → cierra el modal.
.modal-body → contiene el contenido principal.
```

El componente **modal** ofrece una experiencia visual centrada,
limpia y coherente con los colores, transiciones y tipografía del resto del framework.

## 5.9 Formularios: `form`, `label`, `input` y `button`

Con este bloque se cubre la base de formularios usando las utilidades ya definidas en tu CSS:
`form.card-form`, `.label-float`, `.input-group`, `.btn` y variantes.

---

### Estructura base (tarjeta de formulario)

```html
<form class="card-form">
  <h3>Acceso</h3>

  <div class="label-float">
    <input id="email" type="email" placeholder=" " required>
    <label for="email">Correo electrónico</label>
  </div>

  <div class="label-float">
    <input id="password" type="password" placeholder=" " required minlength="6">
    <label for="password">Contraseña</label>
  </div>

  <button type="submit" class="btn btn-blue">Ingresar</button>
</form>
```

**Notas:**

- `placeholder=" "` (espacio) activa el estado flotante al enfocar/llenar.
- `required` y `minlength` aprovechan validaciones del navegador.
- El estilo de `form.card-form` ya está definido en `index.css`.

---

### tiquetas flotantes (`.label-float`)

```html
<div class="label-float">
  <input id="user" type="text" placeholder=" ">
  <label for="user">Usuario</label>
</div>

<div class="label-float">
  <textarea id="notes" placeholder=" " rows="3"></textarea>
  <label for="notes">Notas</label>
</div>

<div class="label-float">
  <select id="role" value="">
    <option value="" disabled selected>Seleccione un rol</option>
    <option value="admin">Administrador</option>
    <option value="user">Usuario</option>
  </select>
  <label for="role">Rol</label>
</div>
```

**Comportamiento:**

- Borde y sombra en `:focus` usando variables (`--dark-blue`, etc.).
- La etiqueta “flota” al enfocar o cuando hay contenido (reglas ya incluidas).

---

### Grupo de entrada con botón (`.input-group`)

Ideal para acciones como “copiar”, “buscar” o “enviar código”.

```html
<div class="input-group">
  <div class="label-float">
    <input id="token" type="text" placeholder=" ">
    <label for="token">Token</label>
  </div>
  <button class="btn" type="button" aria-label="Copiar">
    <i></i>
  </button>
</div>
```

**Detalles:**

- El `input` pierde el radio en el borde derecho y el botón lo complementa (reglas CSS ya incluidas).
- El `<i>` usa el ícono `copy.svg` configurado en `index.css`.

---

### Estados de los campos

```html
<!-- Deshabilitado -->
<div class="label-float">
  <input id="disabledField" type="text" placeholder=" " disabled value="Solo lectura">
  <label for="disabledField">Campo deshabilitado</label>
</div>

<!-- Requerido / patrón simple -->
<div class="label-float">
  <input id="phone" type="tel" placeholder=" " required pattern="[0-9+\-\s]{7,}">
  <label for="phone">Teléfono</label>
</div>
```

**Sugerencias:**

- Usa `disabled`/`readonly` según el caso.
- Valida con `pattern` cuando aplique; los estilos de foco siguen funcionando.

---

### Botones (`.btn` + variantes)

```html
<button class="btn btn-blue" type="button">Primario</button>
<button class="btn btn-green btn-sm" type="button">Confirmar</button>
<button class="btn btn-red btn-lg" type="button">Eliminar</button>
```

**Variantes y tamaños:**

- Color: `btn-blue`, `btn-green`, `btn-red`.
- Tamaño: `btn-sm`, `btn-lg`.
- Efectos de hover y sombra incluidos.

---

### Ejemplo completo (login + acción secundaria)

```html
<section class="container">
  <div class="row">
    <div class="col-12 col-md-6 mx-auto">
      <form class="card-form">
        <h3>Iniciar sesión</h3>

        <div class="label-float">
          <input id="login-email" type="email" placeholder=" " required>
          <label for="login-email">Correo</label>
        </div>

        <div class="label-float">
          <input id="login-pass" type="password" placeholder=" " required minlength="6">
          <label for="login-pass">Contraseña</label>
        </div>

        <button type="submit" class="btn btn-blue">Entrar</button>
        <button type="button" class="btn btn-green btn-sm mt-2">Crear cuenta</button>
      </form>
    </div>
  </div>
</section>
```

---

### Accesibilidad mínima

- Cada `input`/`textarea`/`select` debe tener `id` y `label[for]` coincidentes.
- Usa `aria-label` o `aria-describedby` cuando no haya texto visible suficiente.
- Mantén `role="status"` solo para mensajes dinámicos (p. ej., alertas), no para el formulario.

---

## 5.10 Componente de tarjetas (`.card`)

El componente **card** representa un contenedor flexible y reutilizable que agrupa contenido visual o informativo.
Puede incluir títulos, íconos, descripciones y acciones.
Las tarjetas se adaptan fácilmente a layouts en cuadrícula y a cualquier tamaño de pantalla.

**Estructura base:**

Una tarjeta típica contiene:

```.
.card (contenedor principal)
 ├─ h3 (título)
 └─ .card-content (cuerpo o disposición de contenido)
```

Ejemplo básico:

```html
<article class="card">
  <h3>Título de la tarjeta</h3>
  <div class="card-content">
    <p>Contenido o descripción principal.</p>
  </div>
</article>
```

---

**Estilos principales:**

```css
.card{
  background-color:var(--white);
  border:1px solid var(--gray-400);
  border-radius:8px;
  padding:1rem;
  box-shadow:var(--shadow-1);
  display:flex;
  flex-direction:column;
  align-items:self-start;
  gap:.6rem;
  transition:transform var(--transition-base),box-shadow var(--transition-base);
}
.card-hover:hover{
  transform:translateY(-4px);
  box-shadow:0 3px 10px var(--shadow-2);
}
.card h3{
  font-size:1.1rem;
  font-weight:600;
  text-align:center;
  margin-bottom:.2rem;
}
.card-content{
  flex:1;
  display:flex;
  flex-direction:row;
  justify-content:space-around;
  align-items:center;
  flex-wrap:nowrap;
  width:100%;
}
.card-content i{
  width:32px;
  height:32px;
  border:1px solid var(--dark);
  border-radius:50%;
  display:flex;
  align-items:center;
  justify-content:center;
  font-style:normal;
  font-weight:600;
  color:var(--dark);
}
```

---

**Ejemplos prácticos:**

1. **Tarjeta informativa**

```html
<article class="card">
  <h3>Servidor en línea</h3>
  <div class="card-content">
    <i class="icon-JAVA"></i>
    <p class="text-dark">Instancia activa en puerto 8090</p>
  </div>
</article>
```

2️. **Tarjeta con efecto hover**

```html
<article class="card card-hover">
  <h3>Proceso completado</h3>
  <div class="card-content">
    <i class="icon-PYTHON"></i>
    <p class="text-green font-600">Sin errores detectados</p>
  </div>
</article>
```

3️. **Tarjeta con varios elementos**

```html
<article class="card card-hover">
  <h3>Estado del sistema</h3>
  <div class="card-content">
    <div>
      <p class="text-muted">Usuarios activos</p>
      <p class="font-700 text-blue">124</p>
    </div>
    <div>
      <p class="text-muted">Tareas pendientes</p>
      <p class="font-700 text-red">6</p>
    </div>
  </div>
</article>
```

---

### Variantes recomendadas

| Clase adicional    | Descripción                                          |
| ------------------ | ---------------------------------------------------- |
| `.card-hover`      | Añade elevación y desplazamiento al pasar el cursor. |
| `.text-*`, `.bg-*` | Permiten personalizar texto y fondo.                 |
| `.rounded-*`       | Ajusta los bordes usando las variables de radio.     |
| `.border-*`        | Añade borde temático.                                |

Ejemplo:

```html
<article class="card card-hover border-blue rounded-3">
  <h3 class="text-blue">Tarjeta personalizada</h3>
  <div class="card-content">
    <i class="icon-NODEJS"></i>
    <p>Aplicación Node.js corriendo sin interrupciones.</p>
  </div>
</article>
```

---

### Organización en cuadrícula

Las tarjetas pueden combinarse fácilmente con las clases de layout (`.row`, `.col-*`):

```html
<section class="container">
  <div class="row">
    <div class="col-4">
      <article class="card card-hover">
        <h3>Java</h3>
        <div class="card-content">
          <i class="icon-JAVA"></i>
          <p>Servicio activo</p>
        </div>
      </article>
    </div>
    <div class="col-4">
      <article class="card card-hover">
        <h3>Python</h3>
        <div class="card-content">
          <i class="icon-PYTHON"></i>
          <p>Última ejecución exitosa</p>
        </div>
      </article>
    </div>
    <div class="col-4">
      <article class="card card-hover">
        <h3>NodeJS</h3>
        <div class="card-content">
          <i class="icon-NODEJS"></i>
          <p>Sincronización completa</p>
        </div>
      </article>
    </div>
  </div>
</section>
```

---

### Buenas prácticas

- Usa `.card-hover` en elementos interactivos (paneles, botones, etc.).
- Mantén un solo propósito por tarjeta (ejemplo: estado, resumen o acción).
- Evita anidar tarjetas dentro de otras.
- Usa `gap`, `text-*`, `bg-*` y `border-*` para personalización ligera.

---

**Resultado esperado:**
Tarjetas limpias, con sombra ligera, bordes suaves, tipografía clara y color controlado por variables del sistema (`--gray-*`, `--blue`, `--green`, `--red`, etc.).
Perfectas para dashboards, resúmenes y componentes visuales reutilizables.

---

## 5.11 Tablas (`.table`) y listas (`.list-*`)

Las tablas y listas ofrecen estructuras visuales limpias para mostrar datos ordenados o colecciones de elementos.
Ambas siguen el mismo esquema cromático y tipográfico del framework, asegurando consistencia visual.

---

### 🧮 Tablas (`.table`)

El componente `.table` define un formato flexible, legible y adaptable a cualquier diseño.
Se puede combinar con clases adicionales para crear variaciones como rayadas, con borde, responsivas o con encabezados temáticos.

---

#### 🎨 Estilos base

```css
.table{
  width:100%;
  border-collapse:collapse;
  border-spacing:0;
  font-size:.95rem;
  color:var(--dark);
  background-color:var(--white);
}
.table th,
.table td{
  padding:.75rem 1rem;
  text-align:left;
  border-bottom:1px solid var(--gray-300);
}
.table th{
  background-color:var(--gray-100);
  font-weight:600;
}
.table tr:last-child td{border-bottom:none}
```

---

#### 💡 Variaciones disponibles

| Clase adicional     | Descripción                                             |     |          |                                          |
| ------------------- | ------------------------------------------------------- | --- | -------- | ---------------------------------------- |
| `.table-striped`    | Alterna el color de las filas impares.                  |     |          |                                          |
| `.table-hover`      | Agrega color de fondo al pasar el cursor.               |     |          |                                          |
| `.table-bordered`   | Aplica borde a todas las celdas.                        |     |          |                                          |
| `.table-rounded`    | Bordes redondeados.                                     |     |          |                                          |
| `.table-responsive` | Agrega desplazamiento horizontal en pantallas pequeñas. |     |          |                                          |
| `.caption-top`      | Muestra el `caption` encima de la tabla.                |     |          |                                          |
| `.table-[blue       | green                                                   | red | yellow]` | Colorea la cabecera con tonos temáticos. |

---

#### 🧩 Ejemplo básico

```html
<div class="table-responsive">
  <table class="table table-striped table-hover table-rounded caption-top">
    <caption>Listado de usuarios</caption>
    <thead class="table-blue">
      <tr>
        <th>Nombre</th>
        <th>Correo</th>
        <th>Estado</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>María López</td>
        <td>maria@example.com</td>
        <td>Activo</td>
      </tr>
      <tr>
        <td>Carlos Ruiz</td>
        <td>carlos@example.com</td>
        <td>Inactivo</td>
      </tr>
    </tbody>
  </table>
</div>
```

**Notas:**

- `.table-blue` aplica fondo azul claro y texto azul oscuro en encabezados.
- `.table-responsive` añade scroll horizontal en móviles.
- `.caption-top` coloca el título de la tabla sobre el contenido.

---

#### 🧱 Ejemplo con borde y color temático

```html
<table class="table table-bordered table-green">
  <thead>
    <tr><th>Producto</th><th>Stock</th><th>Precio</th></tr>
  </thead>
  <tbody>
    <tr><td>Laptop</td><td>25</td><td>$800</td></tr>
    <tr><td>Mouse</td><td>40</td><td>$25</td></tr>
  </tbody>
</table>
```

---

### 📜 Listas (`.list-*`)

El sistema de listas incluye distintos estilos: en formato tabla, con viñetas, con diamantes o numeradas.
Todas las listas comparten tipografía, espaciado y colores definidos en `index.css`.

---

#### 🧾 Lista tipo tabla (`.list-table`)

```html
<ul class="list-table table-striped table-hover table-rounded">
  <li>
    <div class="cell col-1">#1</div>
    <div class="cell col-2">Elemento</div>
    <div class="cell col-end text-right">100</div>
  </li>
  <li>
    <div class="cell col-1">#2</div>
    <div class="cell col-2">Elemento</div>
    <div class="cell col-end text-right">250</div>
  </li>
</ul>
```

**Clases compatibles:**

- `.table-striped` → filas alternadas.
- `.table-hover` → fondo al pasar el cursor.
- `.table-rounded` → esquinas redondeadas y sombra ligera.

---

#### 🔹 Lista con viñetas (`.list-bullets`)

```html
<ul class="list-bullets">
  <li>Iniciar servidor</li>
  <li>Verificar conexión</li>
  <li>Aplicar actualización</li>
</ul>
```

**Detalles:**

- Usa puntos estándar (`disc`) como marcadores.
- Hereda color `var(--blue)` en los marcadores (`::marker`).

---

#### 🔸 Lista con diamantes (`.list-diamonds`)

```html
<ul class="list-diamonds">
  <li>Inicio</li>
  <li>Panel de control</li>
  <li>Configuración</li>
</ul>
```

**Características:**

- Cada ítem incluye un símbolo “◆” verde a la izquierda.
- Ideal para pasos secundarios o listas estéticas.

---

#### 🔢 Lista enumerada (`.list-enum`)

```html
<ol class="list-enum">
  <li>Instalar dependencias</li>
  <li>Configurar variables</li>
  <li>Ejecutar servicio</li>
</ol>
```

**Variantes:**

- `.list-enum-compact` → reduce el espacio vertical (`margin: .25rem 0`).

```html
<ol class="list-enum list-enum-compact">
  <li>Verificar entorno</li>
  <li>Compilar</li>
  <li>Probar</li>
</ol>
```

**Estilo:**

- Los números son generados con `counter-increment` y se muestran en fuente monoespaciada.

---

### ⚙️ Buenas prácticas

| Tipo de lista / tabla | Recomendación                                          |
| --------------------- | ------------------------------------------------------ |
| `.table`              | Datos estructurados, encabezados claros, filas cortas. |
| `.list-table`         | Ideal para listas de registros o resúmenes breves.     |
| `.list-bullets`       | Instrucciones simples o listas de tareas.              |
| `.list-diamonds`      | Contenido jerárquico o decorativo.                     |
| `.list-enum`          | Procesos secuenciales o pasos numerados.               |

---

### 📘 Resumen visual

**Tablas:**

- `.table-striped` → alterna color de filas.
- `.table-hover` → resalta fila al pasar el mouse.
- `.table-responsive` → scroll horizontal.

**Listas:**

- `.list-bullets` → usa puntos.
- `.list-diamonds` → usa ◆ verde.
- `.list-enum` → numera automáticamente.
- `.list-table` → formato tipo tabla.

---

**Resultado esperado:**
Tablas limpias, listas legibles y coherentes con el resto del sistema visual,
usando únicamente variables (`--gray-*`, `--blue`, `--green`, `--light-*`) y helpers (`.rounded-*`, `.border-*`, `.p-*`) para mantener consistencia en toda la interfaz.
