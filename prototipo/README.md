# Prototipo navegable

Un solo archivo (`index.html`) con datos de ejemplo. Sirve para validar el concepto, el diseño y los flujos antes de construir la app real.

- **Ver:** abrilo en cualquier navegador o desde el artifact publicado en Claude.
- **Datos:** 6 meses simulados (abril–septiembre 2026) en ARS/USD, generados con semilla fija. Lo que cargues se pierde al recargar.
- **Modelo:** usa las mismas entidades y reglas que [`docs/ARQUITECTURA.md`](../docs/ARQUITECTURA.md): el pago de la tarjeta es una transferencia, las cuotas se generan una por mes y el ahorro y la inversión son transferencias a cuentas con ese propósito.
- **Nombre:** se cambia en la constante `APP` al inicio del script.

No es código de producción: es la referencia visual y funcional para la versión web (GitHub + Vercel).
