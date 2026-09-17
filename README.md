# Vinilo Andino — Práctica Semana 05

**Curso:** Desarrollo de Aplicaciones Web (ISO93A)  
**Universidad Nacional del Centro del Perú — Facultad de Ingeniería de Sistemas**

## Integrante
- ROBERTO CAMARGO ALVARADO — rama `Camargo`

## Tema elegido
E-commerce de vinilos, tornamesas y audio — "Vinilo Andino".

## Tecnologías
- HTML5 semántico
- Bootstrap 5.3.3 (vía CDN)
- Tailwind CSS (Play CDN)
- Google Fonts: Fraunces + Inter

## Estrategia de combinación Bootstrap + Tailwind

**Bootstrap** se usó para:
- Estructura y componentes: navbar-expand-lg, collapse, dropdown, toggler.
- Sistema de grillas (container/row/col-md-4).
- Estados de formulario (form-control, is-invalid, valid-feedback).

**Tailwind** se usó para:
- Utilidades de espaciado y sombras: py-3, shadow-lg, backdrop-blur.
- Composición tipográfica del hero: text-balance, max-w-3xl, bg-gradient-to-r.
- Efectos interactivos en tarjetas: rounded-xl, hover:scale-105, transition-transform.
- Validación CSS avanzada con `peer` en el campo teléfono.

### Conflictos de especificidad y cómo se resolvieron
El único conflicto real fue que Tailwind (Play CDN) inyecta su preflight
después del CSS de Bootstrap, alterando algunos estilos base (por ejemplo
`button` y `h1`). Se resolvió:
1. Declarando variables de diseño propias en `:root` y aplicándolas en
   estilos específicos del proyecto (`.navbar-vinilo`, `.hero-section`, etc.).
2. Usando `!important` solo donde Bootstrap lo exige (`.nav-link` activo/hover).
3. Evitando mezclar en el mismo elemento clases de color de ambos frameworks:
   Bootstrap se usó para layout/estructura y Tailwind para utilidades visuales.
4. Colocando el `<link>` de Bootstrap **antes** del `<script>` de Tailwind,
   para que las utilidades de Tailwind tengan mayor prioridad en la cascada.

## Auditorías
- Lighthouse Desktop: Performance XX / Accessibility XX / Best Practices XX / SEO XX
- Lighthouse Mobile: Performance XX / Accessibility XX / Best Practices XX / SEO XX
- WAVE: 0 errores, X alertas.

## Nota sobre Tailwind Play CDN
Se usó el Play CDN de Tailwind por indicación de la guía (solo para desarrollo).
En producción se recomienda compilar Tailwind a un archivo CSS local para
evitar el overhead de compilación en el navegador.

## Enlace
https://github.com/THEDEMONS101/DAW_P_03_parte02