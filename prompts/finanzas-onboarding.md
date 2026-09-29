# Prompt: Reset + Onboarding de capital inicial (app de finanzas)

> Copiar y pegar tal cual en el constructor de la app (Lovable u otro).

---

## Objetivo

Quiero que la app parta de cero y que todos los cálculos se basen **únicamente** en los datos que cargue el usuario. Hazlo en dos partes: (1) reset de datos, (2) onboarding inicial obligatorio.

## 1. Reset de datos

- Elimina todos los datos de ejemplo, mock o seed de la app (transacciones, saldos, gráficos, metas, etc.).
- Todos los indicadores deben mostrar `0,00` (con el formato de moneda del usuario) mientras no haya datos cargados. Nada de valores inventados ni placeholders numéricos.
- Los gráficos sin datos deben mostrar un estado vacío ("Todavía no hay datos") en lugar de ejes con valores falsos.
- Añade en Ajustes una opción **"Reiniciar mis datos"** que borre todos los datos del usuario y lo devuelva al onboarding. Debe pedir confirmación explícita (escribir "REINICIAR") porque es irreversible.

## 2. Onboarding inicial (primera pantalla tras registrarse)

Si el usuario no tiene un perfil financiero inicial, **lo primero que ve** es un asistente paso a paso (una pregunta por pantalla, con barra de progreso, botones Atrás/Siguiente). No se puede acceder al dashboard hasta completarlo.

**Paso 0 – Moneda:** selector de moneda principal (por defecto la del navegador).

**Paso 1 – Dinero disponible:** "¿Cuánto dinero tienes disponible hoy? (cuentas corrientes + efectivo)"

**Paso 2 – Ahorros:** "¿Cuánto tienes ahorrado?" (cuentas de ahorro, plazos fijos, fondo de emergencia)

**Paso 3 – Inversiones:** "¿Cuánto tienes invertido?" (valor actual de acciones, fondos, cripto, etc.)

**Paso 4 – Deudas:** "¿Tienes deudas?" Sí / No.
- Si responde Sí: lista donde puede añadir una o varias deudas con: nombre (ej. "Tarjeta Visa", "Préstamo coche"), importe pendiente, cuota mensual (opcional) y tasa de interés anual (opcional).
- Si responde No: deudas = 0.

**Paso 5 – Resumen:** muestra todo lo cargado con opción de editar cualquier paso antes de confirmar.

### Validaciones

- Todos los importes: numéricos, `>= 0`, máximo 2 decimales. Aceptar tanto `1.234,56` como `1234.56`.
- Campo vacío = 0 (no bloquear), pero avisar "¿Seguro que es 0?".
- No permitir negativos: las deudas se cargan como positivas en su propio paso.

## 3. Cálculos (derivados, nunca preguntados)

- **Activos totales** = disponible + ahorros + inversiones
- **Deuda total** = suma de las deudas
- **Patrimonio neto** = activos totales − deuda total (puede ser negativo; mostrarlo en rojo si lo es)
- **Liquidez** = disponible + ahorros
- **Ratio de endeudamiento** = deuda total / activos totales (mostrar "—" si activos = 0, no dividir por cero)

Estos valores son el punto de partida. A partir de aquí, cada ingreso, gasto, aporte a ahorro/inversión o pago de deuda que el usuario registre debe **actualizar automáticamente** los saldos correspondientes:

| Movimiento | Efecto |
|---|---|
| Ingreso | + disponible |
| Gasto | − disponible |
| Transferencia a ahorro | − disponible, + ahorros |
| Aporte a inversión | − disponible, + inversiones |
| Pago de deuda | − disponible, − deuda correspondiente |
| Actualizar valor de inversión | ajusta inversiones (ganancia/pérdida, no es ingreso) |

Los totales se calculan siempre a partir del saldo inicial + movimientos (no guardar totales "a mano" que puedan desincronizarse).

## 4. Datos

- Guardar el perfil inicial por usuario (tabla `financial_profile`: user_id, moneda, disponible_inicial, ahorros_inicial, inversiones_inicial, fecha_inicio, onboarding_completado).
- Tabla `debts` separada (user_id, nombre, importe_pendiente, cuota_mensual, interes_anual).
- Usar tipo decimal/numeric para dinero, nunca float.
- Seguridad: cada usuario solo puede leer/escribir sus propios datos (RLS).

## 5. Criterios de aceptación

- [ ] Usuario nuevo → ve el onboarding, no el dashboard.
- [ ] Sin datos, todo el dashboard muestra 0,00 y estados vacíos.
- [ ] Tras cargar disponible 1.000, ahorros 2.000, inversiones 3.000 y una deuda de 1.500 → activos 6.000, deuda 1.500, patrimonio neto 4.500.
- [ ] Registrar un gasto de 100 → disponible 900, patrimonio neto 4.400.
- [ ] "Reiniciar mis datos" devuelve todo a 0 y vuelve al onboarding.
