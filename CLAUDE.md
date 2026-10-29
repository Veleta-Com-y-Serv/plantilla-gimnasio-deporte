# Plantilla «Gimnasio y deporte» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **enérgico**
(tema oscuro por defecto, verde neón de acento, titulares condensados en mayúsculas, franjas diagonales, botones inclinados).
Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`, `bg-primario/10`…
  - El tema oscuro sale de `fondo` oscuro + `texto` claro. Si el cliente pide fondo claro, cambia esos dos y todo se adapta (los componentes solo usan variables; el velo del hero usa el color de fondo).
  - `acento` = verde neón de botones, franjas y resaltados. La letra encima se calcula sola (`--sobre-acento`).
  - `primario` = fondo de la banda del horario (la letra encima también se calcula sola: `--sobre-primario`).
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-titulos` condensada: "Bahnschrift", "Arial Narrow"…; botones `.btn`/`.btn-sec` inclinados; `.franjas`; `.etiqueta`; cabecera fija `.cabecera--gym` con alto `--alto-cabecera`; pie negro `.pie--gym` con el horario en grande). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (lista y descripción en `fotos.json`); las de relleno, en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Fotos de personas: `/placeholders/persona.svg` (no se generan caras).
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en bloque de acento + nombre.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie`. El pie muestra `contacto.horario` en grande.

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`.
- `hero` → `hero.astro`: pantalla completa, foto con velo, `titulo` enorme (mejor 2-4 palabras), `texto`, `cta`, `cta_secundario` e `items: [{titulo, icono}]` (3 etiquetas).
- `clases` → `clases.astro`: `items: [{titulo, texto, icono, imagen, intensidad}]`; `intensidad` = "Suave" | "Media" | "Alta" (o vacía: no se pinta).
- `horario-clases` → `horario-clases.astro`: `clases_horario: [{dia, hora, clase, monitor}]`, agrupado por `dia` en orden de aparición (una columna por día en escritorio, lista en móvil). `nota` y `cta` opcionales. Lista vacía = solo titular y texto.
- `tarifas` → `tarifas.astro`: `planes: [{nombre, precio, periodo, incluye, destacado, cta_texto}]`. `incluye` es **una cadena** separada por «;». `precio` siempre texto (`"44,90 €"`); vacío = no se pinta. `destacado: true` = bloque con resplandor. El botón de cada plan va a `cta.url` (o a `#contacto`). `planes: []` = titular, texto, `nota` y botón `cta`. No inventes precios.
- `entrenadores` → `entrenadores.astro`: `personas: [{nombre, cargo, foto, texto}]`.
- `instalaciones` → `instalaciones.astro`: `galeria: [ruta…]` en mosaico (la 1.ª grande, la 4.ª ancha) + `items: [{titulo, icono}]` opcionales.
- `opiniones` → `opiniones.astro`: `testimonios: [{texto, autor, nota}]`. No inventes opiniones.
- `preguntas` → `preguntas.astro` (preguntas frecuentes en acordeón `details/summary`; sin preguntas no se pinta)
- `contacto` → `contacto.astro`: teléfono en grande y datos de `contacto`; formulario (nombre, teléfono, email, «Me interesa» con las clases y los planes, mensaje). `boton_formulario` opcional.
- `texto` → `texto.astro`: apartado genérico (párrafos, `imagen`, `items`, `cta`). Para apartados nuevos: `tipo: texto`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas (las horas, siempre: `hora: "18:30"`).
4. **Listas planas**: nunca una lista dentro de un elemento de lista (el horario es una lista de clases con su `dia`, no días con clases dentro). Precios siempre como texto entre comillas. Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: mejor un apartado con `tipo:` (`tipo: texto`, `tipo: clases`, `tipo: tarifas`…) y su propio id. Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)`, `Seccion`, `Titular`. `src/pages/index.astro` la recoge sola: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` son obligatorios. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en las 16 plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral (`.contenedor`), sin scroll horizontal en móvil. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`, o el `titulo`/`nombre` de la ficha); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Iconos disponibles: ver `src/components/ui/Icono.astro` (de deporte: `pesa, fuego, bici, guante, loto, pulso, cronometro, taquilla, trofeo, corazon, reloj, regalo`…).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.
