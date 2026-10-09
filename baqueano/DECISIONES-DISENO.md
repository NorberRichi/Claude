# Baqueano — Decisiones de diseño

App: https://baqueano-app.vercel.app/

## 1. Pantalla Garaje: reemplazo de la foto del Jeep

**Estado:** decidido (2026-10-09). Pendiente de implementar.

**Decisión:** la foto del Jeep subiendo una colina se reemplaza por la **camioneta del usuario dibujada en líneas animadas**.

- Siluetas **por categoría**, no por modelo: pickup doble cabina, pickup cabina simple, SUV 4x4, Jeep corto, Jeep largo, utilitario y, opcionalmente, cuatriciclo o moto.
- Personalización con datos del usuario: color, nombre o patente, y accesorios como capas (snorkel, barras de techo, cubiertas grandes).
- Datos superpuestos al dibujo: km, próximo service, estado de cubiertas.
- Animación: el trazo se dibuja (`stroke-dashoffset`), las ruedas giran y la suspensión rebota una vez. Dura entre 1 y 1,5 s y no queda en loop.
- Técnica: SVG + CSS o Framer Motion (no Lottie). Respetar `prefers-reduced-motion`.
- Pantalla sin vehículo: silueta punteada con "Agregá tu vehículo".

**Condición:** esto requiere que la app guarde el tipo o modelo de vehículo de cada usuario. Si todavía no lo guarda, se usa temporalmente el fondo topográfico.

**Topografía (curvas de nivel):** se descarta para el garaje. Queda reservada como identidad de marca para inicio, login, onboarding y mapas.

## 2. Pantalla de inicio (splash / onboarding)

**Estado:** foto decidida; mapa en discusión.

- **Foto:** `paisaje-roca-cordillera`, la Toyota Hilux del autor en una huella recta hacia la cordillera, al atardecer. Reemplaza a la camioneta anterior, que no es representativa del mercado argentino.
  - Pendiente: conseguir el original en resolución completa (la copia recibida es de 1600×1200).
  - Recorte vertical: el foco va en el frontal de la camioneta y la huella al horizonte.
  - Texto arriba, sobre el cielo; botones abajo, sobre las rocas, con un degradado oscuro.
- **Texto:** se saca la mención a la Ruta del Abra del Acay. Titular propuesto: "Donde termina la ruta, empieza Baqueano."
- **Mapa de huellas:** propuesto para reemplazar el bloque del Abra del Acay.
  - Formato: SVG estático de la silueta de Argentina; cada huella se dibuja en línea animada (mismo lenguaje visual que el garaje).
  - Ubicación: segunda pantalla del onboarding, no en la portada con la foto.
  - No usar un mapa interactivo (Mapbox o Leaflet) en el inicio.
  - Mostrarlo solo cuando haya suficientes huellas cargadas.
