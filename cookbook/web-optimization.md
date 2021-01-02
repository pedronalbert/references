# Web Optimization

# Teoría

## Web Vitals

### LCP (Largest Contentful Paint)

Tiempos: < 2,5s (Buena), 2,5s - 4s (Regular), > 4s (Mala)

El tiempo que tarda en pintar el mayor elemento visible en la ventana.

### FID (First Input Delay)

Tiempos: < 100ms (Buena), 100ms - 300ms (Regular), > 300ms (Mala)

El tiempo que tarda la página en responder a las acciones del usuario

> El FID se mide basado en el peor tiempo de respuesta de varias interacciones

### CLS (Cummulative Layout Shift)

Tiempos: < 0.1 (Buena), 0.1 - 0.25 (Regular), > 0.25 (Mala)

Mide todos los cambios inesperados en el layout de una página, como por ejemplo cuando cargas una imagen muy grande, y luego se reacomoda a ser mas pequeña durante el render

## Paints and Render

### To Remember
- El proceso de paint es el mas costoso que realiza un navegador, por lo cual todo elemento que no vaya a ser mostrado directamente es preferibel mantenerlo en css con display: none (ejemplo los dropdowns) y luego de la accion si mostrarlos por JS
- Todos los cambios en css generan un paint a excepción de un opacity o un transform
- Entre mas cortos y mas directos sean los selectores css mas rápido será el render
- Basandose en el critical rendering, hay que evitar usar imágenes como backgrounds de css y en su lugar usar <img>

# Codigo

## Critical Assets

### Media Link
Podemos usar media queries en los scirpts links

```html
<link rel="stylesheet" href="file.css" media="screen and (min-width: 600px)>
```

### Pre
Tenemos diferentes maneras de acelerar aciones futuras

```html
<!-- prefetch -->

<!-- preload -->

<!-- dns-prefetch: Realiza la resolucion de DNS del dominio indicado  -->
<link rel="dns-prefetch" href="https://fonts.gstatic.com">

<!-- preconnect: Realiza la conexion hacia el diminio, esto incluye el TLS handshake  -->
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigen>
```

## Fonts

- Usar el modo `swap` en las google fonts
- https://github.com/typekit/webfontloader

# Recursos

- https://bundlephobia.com/