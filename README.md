# Plantilla NoExpertise · Gimnasio y deporte

Web enérgica en tema oscuro para gimnasios y centros deportivos, con clases, horario y tarifas.

- Sectores: gimnasio, deporte, yoga, crossfit, club deportivo, pilates. Estilo: enérgico. Plan mínimo: presencia.
- Secciones: hero, clases, horario-clases, tarifas, entrenadores, instalaciones, opiniones, preguntas, contacto (+ `texto` para apartados nuevos).
- Campos propios: `clases.items[].intensidad`, `clases_horario[]` (dia, hora, clase, monitor), `planes[]` (nombre, precio, periodo, incluye con «;», destacado, cta_texto).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos en `template.yaml`; reglas para el agente en `CLAUDE.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.
