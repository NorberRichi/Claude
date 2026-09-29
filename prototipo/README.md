# Prototipo navegable

Un solo archivo (`index.html`). La app arranca vacía: no trae datos de ejemplo y todos los cálculos salen de lo que carga el usuario.

## Flujo

1. **Onboarding obligatorio** (6 pasos, con barra de progreso): moneda → disponible → ahorros → inversiones → deudas → resumen editable.
2. **Dashboard**: patrimonio neto, disponible, ahorros, inversiones, deuda total, liquidez y ratio de endeudamiento. Sin datos, los montos muestran `0,00` y los gráficos, "Todavía no hay datos".
3. **Ajustes → Reiniciar mis datos**: pide escribir `REINICIAR`, borra todo y vuelve al onboarding.

## Cálculos

Todo se deriva de **saldo inicial + movimientos**. No se guarda ningún total a mano.

| Movimiento | Efecto |
|---|---|
| Ingreso | + disponible |
| Gasto | − disponible (o + deuda si se paga con una deuda, por ejemplo la tarjeta) |
| A ahorro | − disponible, + ahorros |
| A inversión | − disponible, + inversiones |
| Pago de deuda | − disponible, − esa deuda (no puede superar lo pendiente) |
| Actualizar valor de inversión | ± inversiones (ganancia o pérdida, no es ingreso) |

## Datos

- **Dentro de Claude** (artifact): se usa la base de datos del artifact, en la ruta privada de cada usuario (`data/users/<id>/…`). Solo ese usuario lee y escribe sus datos, el equivalente a RLS.
  - `profile`: `moneda`, `disponible_inicial`, `ahorros_inicial`, `inversiones_inicial`, `fecha_inicio`, `onboarding_completado`.
  - `profile/debts/<id>`: `nombre`, `importe_pendiente`, `cuota_mensual`, `interes_anual`, `fecha`.
  - `profile/movements/<id>`: `tipo`, `importe`, `fecha`, `categoria`, `deuda_id`, `descripcion`.
- **Abierto como archivo suelto**: guarda en `localStorage` y avisa que los datos quedan solo en ese navegador.
- **Montos**: enteros en centavos (`montos_en: "centavos"`), nunca `float`. Es el equivalente exacto de `numeric` en un almacén JSON. En Postgres/Supabase serán `numeric(14,2)`.

El nombre de la app se cambia en la constante `APP` al inicio del script.
