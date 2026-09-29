# Prompts: Baqueano · lo que falta después de la revisión (29/9/2026)

> Son dos prompts: uno para la charla de la **landing** y otro para la charla de la **app**.
> Pegá cada uno en su propia charla de VS Code. No los mezcles: son repos distintos.
>
> **Antes de pegar nada:** en la carpeta de la landing corré `git pull`. Los arreglos de la revisión
> (privacidad con cuentas, precios en pesos, sin IA, huellas, botón Entrar, dominio de Vercel, etc.)
> ya están subidos en el commit `bd5e5e1`. Si no hacés `git pull`, la charla va a trabajar sobre la versión vieja.

---

## Prompt 1 · Charla de la LANDING (repo `NorberRichi/Baqueano`)

```
Hacé `git pull` antes de empezar. El 29/9 se subió el commit bd5e5e1, que alineó la landing
con la app. Leé en contexto-landing.md la entrada del 29/9 para ver qué se hizo. No rehagas nada
de eso ni lo deshagas: privacidad, cookies y términos con cuentas; precios en pesos; sin IA en Pro;
sección Huellas; botón Entrar; ruta de ejemplo en pesos; GSAP en lib/; dominio
baqueano-ochre.vercel.app.

Quiero estos cambios, en este orden. Parate después de cada uno para que lo pruebe.

1. MENÚ EN EL CELULAR
   Hoy, debajo de 860 px, los links del menú (Cómo funciona, Terrenos, Huellas, Precios, Preguntas)
   quedan ocultos. Para llegar a Precios hay que bajar unas 20 pantallas.
   - Sumá un botón de menú en la barra de arriba, entre el símbolo y "Entrar / Probar gratis".
   - Al tocarlo se abre un panel a pantalla completa con los 5 links, "Entrar" y "Probar gratis".
   - Tiene que cerrarse al tocar un link, con Escape y con un botón de cerrar.
   - Accesible: aria-expanded, aria-controls, foco atrapado mientras está abierto, y el foco vuelve
     al botón al cerrar.
   - Tiene que funcionar aunque GSAP no cargue: la apertura es con CSS y JS simple, sin GSAP.
   - Respetá la estética actual: tipografía mono, mayúsculas, fondo oscuro.
   - Probalo a 390 px y a 768 px. No tiene que haber scroll horizontal ni textos cortados.

2. CAPTURAS REALES DE LA APP
   En "Cómo funciona" hay un teléfono dibujado en HTML (#tel, 4 pantallas .pant).
   - Te voy a pasar 4 capturas reales de la app. Guardalas en fotos/app/ en .webp y en dos tamaños,
     celular y computadora, como hace fotos/generar-movil.ps1.
   - Reemplazá las 4 pantallas dibujadas por esas capturas, con alt descriptivo, sin perder
     la animación actual de cambio de pantalla.
   - Si todavía no te pasé las capturas, preguntámelas y no hagas este paso.

3. LICENCIAS DE LAS FOTOS
   Revisá fotos/CREDITOS.md. Hacé una tabla con las 8 fotos que usa la landing (las de landing.html),
   de dónde sale cada una, su licencia y si está confirmada o no. Para las que digan "a confirmar",
   no inventes la fuente: marcalas y decime cuáles tengo que reemplazar o confirmar yo.
   No borres ninguna foto del repo sin preguntarme.

4. CHEQUEO FINAL
   - Corré `sh publicar.sh` sin errores.
   - Buscá en todo el repo "netlify", "USD", "inteligencia artificial" y "no hay cuentas":
     no tiene que quedar ninguno en lo que se publica.
   - Anotá lo hecho en contexto-landing.md (sección 10) y subí los cambios con commit y push,
     como dice CLAUDE.md.

Reglas: Baqueano no inventa. Nada de cifras, testimonios ni funciones que la app no tenga.
Si un dato no lo sabés, preguntame.
```

---

## Prompt 2 · Charla de la APP (repo `NorberRichi/baqueano-app`)

```
Tres cosas de la app que salieron de revisar la landing. Parate después de cada una para que la pruebe.

1. LA POLÍTICA DE PRIVACIDAD DE LA APP ESTÁ VIEJA
   En data.js (priv) dice "Todavía no hay un botón para borrar la cuenta entera: está pendiente".
   Ese botón ya existe desde el 26/9 (Configuración → Tu cuenta → Eliminar mi cuenta).
   - Corregí ese párrafo y explicá cómo se elimina la cuenta.
   - La sección "Cuando usás el baqueano con IA" describe el chat con IA como parte de Pro, pero la IA
     ya no se ofrece (paso 2 del plan del 29/9). Reescribila para que diga lo que pasa hoy.
   - Sumá el correo de contacto appbaqueano@gmail.com, que es el que usa la landing.
     Sacá la frase "no hay un correo de contacto publicado".
   - Actualizá la fecha.
   - Tiene que decir lo mismo que la política de la landing (privacidad.html del repo Baqueano):
     cuenta opcional, Supabase en San Pablo, fotos en un depósito privado y Vercel como alojamiento.

2. ¿LA APP ABRE SIN SEÑAL?
   cuenta.js guarda primero en el dispositivo, pero no sé si la app ABRE sin conexión.
   No encontré un service worker.
   - Primero verificalo: cargá la app, cortá la red (modo avión o DevTools → Offline) y recargá.
     Decime qué pasa.
   - Si no abre, proponeme un plan antes de programar. Por ejemplo: un service worker que guarde el
     HTML, el CSS, el JS y lib/, estrategia "red primero y, si falla, lo guardado" para el HTML, y
     aviso de versión nueva. Contame los riesgos (versiones viejas trabadas, cómo se actualiza)
     y esperá mi OK.
   - Es para usarla en la huella, donde no hay señal. Es prioridad.

3. ENLACES DESDE LA LANDING
   La landing manda a https://baqueano-app.vercel.app/#intro ("Probar gratis") y a /#entrar ("Entrar").
   Confirmá que los dos funcionan:
   - #intro abre la pantalla de inicio, aunque la persona ya haya entrado antes.
   - #entrar abre la pantalla de inicio de sesión.
   Si alguno no anda, arreglalo y agregá un test en pruebas/.

Al terminar: tests con `deno test --allow-read pruebas/`, anotá en contexto-app.md, commit y push.
Baqueano no inventa: si algo no lo sabés, preguntame.
```

---

## Lo que no es para una charla (lo tenés que hacer vos)

- **Dominio propio**, por ejemplo `baqueano.com.ar` en NIC Argentina. Hace falta para que los mails de
  confirmación no caigan en spam (Resend no deja mandar desde `vercel.app`). Cuando lo tengas, pedile a la
  charla de la landing que cambie `baqueano-ochre.vercel.app` por el nuevo en todos lados.
- **Confirmar las licencias de las fotos** que el paso 3 del prompt 1 marque como "a confirmar".
- **Sacar las 4 capturas de la app** para el paso 2 del prompt 1.
- **Decidir "Más elegido"**: la app ya usa "Ahorrás 33 %". Hoy la landing mantiene "Más elegido".
