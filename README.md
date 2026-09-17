# Vinilo Andino — Práctica Semana 05

**Curso:** Desarrollo de Aplicaciones Web (ISO93A)  
**Universidad Nacional del Centro del Perú — Facultad de Ingeniería de Sistemas**  
**Programa:** Ingeniería de Sistemas

## Integrante
- ROBERTO CAMARGO ALVARADO — rama `Camargo`

## Tema elegido
E-commerce de vinilos, tornamesas y audio — **"Vinilo Andino"** (Opción 2: E-commerce de Productos).

## Tecnologías utilizadas
- HTML5 semántico
- Bootstrap 5.3.3 (vía CDN oficial jsDelivr)
- Tailwind CSS (Play CDN — solo para desarrollo)
- Google Fonts: Fraunces (display) + Inter (texto)
- JavaScript nativo (validación de formulario)

## Estructura del proyecto

## Estrategia de combinación Bootstrap + Tailwind

### Bootstrap 5 — estructura y componentes
- **Navbar:** `navbar-expand-lg`, `collapse`, `toggler`, `dropdown` (sin JS adicional, aprovechando el bundle de Bootstrap).
- **Sistema de grillas:** `container`, `row`, `col-md-4` para el grid de tarjetas.
- **Formulario:** `form-control`, `form-select`, `is-invalid`, `valid-feedback`, `needs-validation`.
- **Utilidades de layout:** `d-flex`, `gap-3`, `justify-content-between`.

### Tailwind CSS — utilidades visuales y estados
- **Navbar:** `py-3`, `shadow-lg`, `backdrop-blur`.
- **Hero:** `text-balance`, `max-w-3xl`, `bg-gradient-to-r from-[#14120f] via-[#1a1712] to-[#14120f]`.
- **Tarjetas:** `rounded-xl`, `shadow-lg`, `hover:scale-105`, `transition-transform duration-300`, `overflow-hidden`.
- **Formulario:** validación avanzada solo con CSS usando la clase `peer` y la variante arbitraria `peer-[&:not(:placeholder-shown):invalid]:visible`.

### Conflictos de especificidad y cómo se resolvieron
1. **Preflight de Tailwind vs Bootstrap.**  
   Tailwind Play CDN inyecta su *preflight* después del CSS de Bootstrap, lo que altera algunos estilos base (por ejemplo, márgenes de `h1`–`h3` y el estilo por defecto de `button`).  
   **Solución:** se declararon variables de diseño propias en `:root` (`--bg`, `--surface`, `--accent`, etc.) y se aplicaron en clases específicas del proyecto (`.navbar-vinilo`, `.hero-section`, `.btn-accent`), evitando depender de los estilos base de ninguno de los dos frameworks.

2. **Especificidad en los enlaces de la navbar.**  
   Bootstrap aplica `.navbar-nav .nav-link { color: … }` con una especificidad relativamente alta.  
   **Solución:** se usó `!important` **solo** en `.navbar-vinilo .nav-link` para los estados `hover` y `active`, ya que era el único punto donde se requería sobreescribir el color de Bootstrap sin romper el layout.

3. **Orden de carga de las hojas de estilo.**  
   El `<link>` de Bootstrap se colocó **antes** del `<script>` de Tailwind Play CDN, de modo que las utilidades de Tailwind tengan prioridad en la cascada cuando se usan clases como `shadow-lg`, `rounded-xl` o `bg-gradient-to-r` sobre componentes de Bootstrap.

4. **Regla interna adoptada.**  
   Bootstrap se reservó para **estructura y componentes** (grillas, navbar, formularios). Tailwind se reservó para **utilidades visuales** (sombras, gradientes, transiciones, tipografía). Cuando un mismo elemento necesitaba ambos, primero se aplicaban las clases de Bootstrap y luego las de Tailwind, aprovechando la posición en la cascada.
   5. **Conflicto de clase `.collapse` entre Tailwind y Bootstrap.**  
   Tailwind Play CDN genera automáticamente la utilidad `.collapse { visibility: collapse; }` al detectarla en el HTML, lo que colisionaba con la clase `.collapse` de Bootstrap usada para el menú móvil del navbar.  
   **Síntoma observado:** al pulsar el botón hamburguesa, el menú aparecía brevemente, se ocultaba y dejaba un "fantasma" visible al hacer scroll.  
   **Solución:** se declaró un override explícito en el CSS propio:  
   ```css
   .collapse,
   .collapsing,
   .navbar-collapse { visibility: visible !important; }

## Accesibilidad
- `lang="es"` en el `<html>`.
- Skip-link al contenido principal (`Saltar al contenido principal`).
- Todas las etiquetas `<label>` vinculadas con `for`/`id`.
- `aria-describedby` en campos con mensajes de ayuda o error (`#nombre`, `#email`, `#telefono`, `#cantidad`, `#mensaje`, `#terminos`).
- Grupo de radios envuelto en `<fieldset>` con `<legend>`.
- Contraste de texto verificado ≥ 4.5:1 (texto claro `#f2ede4` sobre fondo oscuro `#14120f`).
- `aria-label` en el botón hamburguesa (`Abrir menú de navegación`).

## SEO
- `<title>` descriptivo y único.
- Meta tags: `description`, `keywords`, `author`, `robots`.
- Open Graph: `og:title`, `og:description`, `og:type`.
- Estructura semántica: `<nav>`, `<header>`, `<section>`, `<footer>`.
- Jerarquía correcta de encabezados: un solo `<h1>` en el hero, `<h2>` por sección, `<h3>` por tarjeta.

## Auditorías
- **Lighthouse Desktop:** Performance __ / Accessibility __ / Best Practices __ / SEO __
- **Lighthouse Mobile:** Performance __ / Accessibility __ / Best Practices __ / SEO __
- **WAVE:** __ errores, __ alertas.

*(Completar con los puntajes reales tras ejecutar las auditorías del Paso 6.)*

## Nota sobre Tailwind Play CDN
Se utilizó el Play CDN de Tailwind por indicación de la guía (solo para desarrollo).  
En un entorno de producción se recomienda compilar Tailwind a un archivo CSS estático para eliminar el coste de compilación en el navegador y mejorar el puntaje de Performance en Lighthouse.

## Enlace del repositorio
https://github.com/THEDEMONS101/DAW_P_03_parte02