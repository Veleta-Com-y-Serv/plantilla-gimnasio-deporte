# Plantilla NoExpertise · Gimnasio y deporte

Web enérgica en tema oscuro para gimnasios y centros deportivos, con clases, horario y tarifas.

- Sectores: gimnasio, deporte, yoga, crossfit, club deportivo, pilates. Estilo: enérgico. Plan mínimo: presencia.
- Secciones: hero, clases, horario-clases, tarifas, entrenadores, instalaciones, opiniones, preguntas, contacto (+ `texto` para apartados nuevos).
- Campos propios: `clases.items[].intensidad`, `clases_horario[]` (dia, hora, clase, monitor), `planes[]` (nombre, precio, periodo, incluye con «;», destacado, cta_texto).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas`. Sin la clave, una sola página larga.
- Contenido editable en `site.yaml`; metadatos en `template.yaml`; reglas para el agente en `CLAUDE.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.clases.items` con `detalle` tiene su página en `/clases/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
