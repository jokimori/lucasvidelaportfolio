# Lucas Videla — Portfolio

Sitio estático: una carpeta que se abre y pasa páginas. No necesita servidor,
ni build, ni dependencias. Son archivos sueltos que cualquier hosting sirve.

```
index.html      la página entera (estructura, estilos y código, todo adentro)
libros/         los 4 libros en EPUB y 3 de ellos también en PDF
tapas/          las tapas, recortadas de los EPUB
_headers        reglas de caché para Cloudflare Pages o Netlify (opcional)
```

Lo único que se descarga de afuera son las tipografías (Spectral e IBM Plex Mono,
de Google Fonts). Si no cargan, la página se ve igual de bien con las de respaldo.

## Publicarlo

### Opción A — Cloudflare Pages, sin GitHub (lo más rápido)
1. Entrá a dash.cloudflare.com → **Workers & Pages** → **Create** → **Pages** →
   **Upload assets**.
2. Arrastrá **el contenido de esta carpeta** (no la carpeta en sí): `index.html`,
   `libros/`, `tapas/`, `_headers`.
3. Listo: queda en `https://<nombre>.pages.dev`. Para usar un dominio propio:
   **Custom domains** → agregar el dominio (si ya está en Cloudflare, se
   configura solo).

Para actualizar, volvés a subir los archivos. Simple, pero sin historial.

### Opción B — GitHub + Cloudflare Pages (recomendada si va a cambiar)
1. Creá un repositorio en GitHub y subí **el contenido** de esta carpeta a la raíz.
2. En Cloudflare: **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
   → elegí el repo.
3. En la configuración de build, dejá todo vacío:
   - Framework preset: **None**
   - Build command: *(vacío)*
   - Build output directory: `/`
4. **Save and Deploy**.

Desde ahí, cada vez que hagas un commit se publica solo. Cada rama y cada commit
quedan con su propia vista previa, así podés ver un cambio antes de que sea el
sitio definitivo.

> GitHub Pages también sirve y es gratis, pero Cloudflare da CDN global, HTTPS y
> vistas previas por rama sin configurar nada.

## Editar el contenido

Todo el texto vive al final de `index.html`, en el bloque `<div id="contenido">`,
como HTML común. Cada `<div>` es **una cara** de la carpeta, en orden de lectura:
el primero es la tapa y el último la contratapa.

- **Agregar o sacar una página**: agregás o borrás un `<div>` en el orden que va.
  La carpeta recalcula sola cuántas hojas necesita.
- **El nombre que aparece arriba a la derecha** sale del `data-title` de cada bloque.
- **Carátulas de sección**: un bloque con `<div class="caratula">` adentro. Siempre
  caen en página izquierda; si hace falta, el código mete una página en blanco antes.
- **Los índices navegan**: un botón con `data-ir="obra"` salta al bloque que tenga
  `data-id="obra"`.
- **Un libro**: tapa en `tapas/`, archivo en `libros/`, y en `<ul class="formatos">`
  una línea por formato. Con un solo formato, la descarga es directa; con dos,
  aparece la elección.
- **El extracto** es el `<div class="extracto" hidden>` que está al lado del botón.

## Antes de publicarlo, completar

- **Contacto**: el mail y los enlaces son de ejemplo (`correo@ejemplo.com`, `#`).
- **Obra visual** y **Arqueología de cada uno**: los recuadros son marcadores de
  posición. Para poner una foto, reemplazá
  `<div class="ph">Escultura</div>` por
  `<div class="ph"><img src="obras/lo-que-sea.jpg" alt="..."></div>`
  y agregá la carpeta `obras/`. Las fichas de cada pieza (`<figcaption class="pie">`)
  todavía dicen "Título s/t · Material · año".
- **El rótulo de arriba a la izquierda** dice "Carpeta". Está en
  `<span class="mark">Carpeta</span>`, por si preferís "Lucas Videla".
