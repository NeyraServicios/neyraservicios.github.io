# Neyra Servicios — Sitio Web

Sitio web estático de **Neyra Servicios**, empresa de tecnología con más de 40 años de experiencia y sede en La Rioja 361, Córdoba, Argentina.

🌐 **Sitio oficial:** [neyraservicios.com.ar](https://neyraservicios.com.ar)

---

## Stack

| Capa | Tecnología |
|------|-----------|
| Markup | HTML5 semántico |
| Estilos | CSS puro — Custom Properties, Grid, Flexbox |
| Scripts | Vanilla JS ES2020+, zero dependencias |
| Fuentes | Google Fonts (carga no-bloqueante) |
| Analytics | No configurado |
| Formulario | [FormSubmit.co](https://formsubmit.co), destino de Ventas |
| Iconos de servicios | Font Awesome Free 7.0.1 ([CC BY 4.0](https://fontawesome.com/license/free)) |
| Tienda y panel | PowerShell `HttpListener`, sin dependencias externas |
| PWA | `manifest.json` + theme-color |

> Bootstrap fue **completamente eliminado** en el rewrite 2025. El CSS resultante pesa ~30 KB menos y no tiene dependencias de terceros en runtime.

---

## Estructura del proyecto

```
NeyraServicios/
├── index.html          # Inicio — hero, stats, servicios, CTA
├── nosotros.html       # Historia, galería, valores
├── marcas.html         # Servicios: hardware, soporte, ciberseguridad y soluciones digitales
├── ubicacion.html      # Mapa, horarios, contacto directo
├── contacto.html       # Formulario + WhatsApp
├── store/              # Catálogo y carrito de compra
├── admin/              # Panel privado de productos y textos de portada
├── server.ps1          # API y servidor local de tienda
├── data/               # Catálogo, textos y hash del administrador
│
├── css/
│   └── main.css        # Estilos compilados (CSS puro, sin Bootstrap)
├── js/
│   └── main.js         # Lógica del sitio (menú, lightbox, contadores, formulario)
├── sass/               # Fuente SCSS (referencia histórica)
│   ├── main.scss
│   ├── _variables.scss
│   ├── _mixins.scss
│   ├── _reset.scss
│   └── layout/
├── media/              # Imágenes, logo, íconos
│
├── manifest.json       # PWA manifest
├── sitemap.xml         # Sitemap para Google Search Console
├── robots.txt          # Directivas para crawlers
└── docs/               # Documentación técnica
    ├── arquitectura.md
    ├── seo.md
    └── accesibilidad.md
```

---

## Páginas

| Página | URL | Descripción |
|--------|-----|-------------|
| Inicio | `/` | Hero animado, contadores, servicios |
| Nosotros | `/nosotros.html` | Historia, galería lightbox, valores |
| Servicios | `/marcas.html` | Soluciones tecnológicas para empresas y personas |
| Ubicación | `/ubicacion.html` | Mapa Google Maps + horarios |
| Contacto | `/contacto.html` | Formulario FormSubmit + WhatsApp directo |
| Tienda | `/store/` | Catálogo, filtros, carrito persistente y pedido por WhatsApp |
| Administración | `/admin/` | Productos, precios, ventas, gastos, pedidos y textos de portada |

---

## Funcionalidades JS

- **Menú móvil** — overlay con gestión de foco (WCAG 2.4.3)
- **Contadores animados** — `IntersectionObserver` + easing cúbico
- **Fade-in por scroll** — `IntersectionObserver`, sin GSAP ni librerías
- **Galería / Lightbox** — foco guardado y restaurado, cierre con Escape
- **Formulario async** — `fetch` + FormSubmit.co, sin recarga de página
- **Contacto directo** — WhatsApp, correo de ventas y soporte técnico
- **Header shadow** — clase `scrolled` en scroll >20px

---

## SEO & Performance

- `<link rel="canonical">` en todas las páginas
- Open Graph + Twitter Card con URLs absolutas e imágenes dimensionadas
- Schema.org: `LocalBusiness`, `BreadcrumbList`, `FAQPage`
- Preload del hero image (`fetchpriority="high"`)
- Fuentes con `media="print" onload="this.media='all'"` (no bloquean render)
- `width`/`height` en todas las imágenes (previene CLS)
- `sitemap.xml` registrado en Google Search Console

---

## Accesibilidad (WCAG 2.1 AA)

- Skip link `#main` en todas las páginas
- `aria-current="page"` en nav activo
- `aria-label` en links externos con "(abre en nueva ventana)"
- Botones de galería (`<button>`) con soporte teclado nativo (Enter/Space)
- `:focus-visible` en todos los elementos interactivos
- Contraste AA verificado en textos sobre fondos oscuros
- `prefers-reduced-motion` respetado en animaciones

---

## Desarrollo local

```powershell
# Iniciar API, tienda y panel en http://127.0.0.1:8080
.\server.ps1
```

Al entrar por primera vez a `/admin/`, creá una contraseña de al menos 12 caracteres. Los controles **Mostrar contraseña** y **Ocultar contraseña** permiten verla mientras la escribís; el servidor sigue guardando únicamente el hash en `data/admin.json`. Para restablecer el acceso local, eliminá `data/admin.json` y reiniciá `.\server.ps1`; al abrir `/admin/` podrás crear una contraseña nueva. Los productos se guardan en `data/products.json` y las fotos en `media/store/`.

La tienda envía un solo mensaje de WhatsApp por pedido, agrupando las unidades del mismo producto (por ejemplo, 2 unidades); si se incluyen productos distintos, los lista juntos en ese mismo mensaje. Los pedidos rápidos también guardan una sola entrada con la cantidad total y el botón de WhatsApp usa esa cantidad. La plantilla admite `{nombre}`, `{cantidad}`, `{unidades}` (unidad/unidades) y `{producto}`. El sitio no procesa pagos ni controla existencias: los productos se ofrecen por encargo y la disponibilidad se confirma al coordinar la entrega. El precio de los cuatro Epson T544 cargados inicialmente es ilustrativo y aparece marcado como muestra. Para publicar el backend fuera de la PC hace falta un servidor HTTPS que pueda ejecutar PowerShell y escribir en `data/` y `media/store/`; el sitio estático actual por sí solo no alcanza.

La copia completa previa a la eliminación del control de stock está en `backup_antes_de_quitar_stock_2026-10-23/`. No publiques esa carpeta: contiene una copia íntegra de los datos y archivos del proyecto.

---

## Contacto del negocio

- 📍 La Rioja 361, Córdoba, Argentina · C.P. 5003
- 📧 Ventas: ventas@neyraservicios.com.ar · Servicio técnico: st@neyraservicios.com.ar · Info: info@neyraservicios.com.ar
- ☎ Ventas: (0351) 15 260-0101 · Servicio técnico: (0351) 15 368-6439 · Fijo: (0351) 422-3214
- 🕐 Lunes a viernes, 9:00–17:00

---

*Desarrollado por [@davidwebgt](https://www.instagram.com/davidwebgt/)*
