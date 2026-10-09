Vamos a hacer cambios visuales en dos pantallas de Baqueano: la de inicio (splash / onboarding) y la del Garaje. Antes de escribir código, investigá el proyecto y presentame un plan.

## Paso 0 — Investigación (no modifiques nada todavía)

Revisá el código y respondeme:
1. Qué stack usa la app (framework, estilos, librería de animación si hay) y dónde están los componentes de la pantalla de inicio y del Garaje.
2. Dónde está la foto actual del inicio (la camioneta con la montaña de fondo) y la foto del Jeep subiendo una colina del Garaje.
3. Si la app guarda el tipo o modelo de vehículo de cada usuario. Si lo guarda, en qué campo y con qué valores posibles.
4. Cómo están guardadas las huellas: cuántas hay, en qué provincias y si tienen coordenadas (puntos o trazados).
5. Dónde aparece el texto sobre la Ruta del Abra del Acay.

Con eso, proponeme un plan de cambios por archivo y esperá mi aprobación.

## Cambio 1 — Pantalla de inicio: foto nueva

- Reemplazá la foto actual por `paisaje-roca-cordillera`, que te paso aparte. Es mi Toyota Hilux en una huella recta hacia la cordillera, al atardecer. Si no está en el proyecto, avisame dónde ponerla.
- Convertila a WebP: menos de 300 KB, con al menos 1080 px en el lado menor si el original lo permite. Si la resolución no alcanza para pantalla completa en celular, avisame en lugar de agrandarla.
- La foto es horizontal (4:3) y la pantalla es vertical. Ajustá el recorte (`object-position`) para que en celular se vea el frontal completo de la camioneta y, si es posible, parte de la huella hacia el horizonte. Mostrame cómo queda en 375×812 y en 390×844 antes de darlo por cerrado.
- El titular va arriba, sobre el cielo. Los botones van abajo, sobre las rocas, con un degradado oscuro de abajo hacia arriba para que se lean bien.
- Verificá que el contraste del texto sobre la foto sea legible (WCAG AA).

## Cambio 2 — Pantalla de inicio: texto

- Eliminá la mención a la Ruta del Abra del Acay.
- Titular nuevo: **"Donde termina la ruta, empieza Baqueano."**
- La pantalla con la foto queda solo con el titular y los botones. No le agregues nada más.

## Cambio 3 — Mapa de huellas (segunda pantalla del onboarding)

- Creá una segunda pantalla de onboarding, después de la foto, con la silueta de Argentina y las huellas de la app dibujadas en línea.
- Usá un SVG generado a partir de los datos reales de las huellas. No uses un mapa interactivo (Mapbox, Leaflet ni Google Maps): tiene que cargar rápido y funcionar sin conexión.
- Animación: cada huella se dibuja con `stroke-dashoffset`, de forma escalonada. Todo dura menos de 2 s y después queda quieto.
- Si hay menos de unas 20 huellas, o están concentradas en una sola zona, no lo implementes: avisame primero, porque un mapa casi vacío juega en contra.
- No inventes huellas ni coordenadas. Usá solo lo que exista en el proyecto.

## Cambio 4 — Garaje: la camioneta del usuario en líneas animadas

Reemplazá la foto del Jeep por un dibujo en líneas (SVG) de la camioneta del usuario.

- Siluetas por categoría, no por modelo: pickup doble cabina, pickup cabina simple, SUV 4x4, Jeep corto, Jeep largo y utilitario. Mapeá cada modelo guardado a su categoría.
- Personalización:
  - El trazo toma el color del vehículo si existe ese dato; si no, el color de acento del tema.
  - Nombre o patente visible.
  - Si en el futuro se cargan accesorios (snorkel, barras de techo, cubiertas grandes), que sean capas del SVG que se prenden o apagan. Dejá preparada la estructura; no hace falta dibujarlos ahora.
- Animación al entrar o al cambiar de vehículo: se dibuja el trazo, giran las ruedas y la suspensión rebota una vez. Dura entre 1 y 1,5 s, sin loop.
- Si hay datos disponibles (km, próximo service, estado de cubiertas), mostralos superpuestos al dibujo. Si no existen, no los inventes.
- Sin vehículo cargado: silueta punteada con el texto "Agregá tu vehículo", que lleve al alta de vehículo.
- Si la app NO guarda el tipo de vehículo: no implementes este cambio. Usá temporalmente un fondo de curvas de nivel topográficas (SVG, tenue) y proponeme cómo agregar el campo de tipo de vehículo.

## Reglas generales

- Todas las animaciones respetan `prefers-reduced-motion`. En ese caso se muestra el estado final, sin animar.
- Usá SVG y CSS, o la librería de animación que ya use el proyecto. No agregues Lottie ni dependencias pesadas.
- Los colores salen de los tokens o variables del tema existente, y todo tiene que verse bien en modo claro y oscuro.
- Mobile first: probá en 375 px de ancho, sin scroll horizontal.
- Mantené el estilo de código del proyecto.
- Al terminar cada cambio, corré el lint, el typecheck y el build. Mostrame capturas o una descripción del resultado. Hacé un commit por cambio, con un mensaje claro.

Implementá en este orden: 1 y 2 (lo más simple y visible), luego 4, y el 3 al final, ya que depende de cuántas huellas haya.
