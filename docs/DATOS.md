# Modelo de datos — FeriaCuenta

Base SQLite local (`expo-sqlite`). Fechas en formato ISO `AAAA-MM-DD`; montos en bolivianos con dos decimales (guardados como enteros en centavos).

## `productos`

Columnas: id, nombre, unidad (kg / unidad / atado / caja), precio_venta, costo_ultimo, activo

## `compras`

Columnas: id, fecha, producto_id, cantidad, costo_total

## `ventas`

Columnas: id, fecha, producto_id, cantidad, monto

## `gastos`

Columnas: id, fecha, categoria, monto, nota

## `cierres`

Columnas: id, fecha, ventas, compras, gastos, efectivo_contado

## Reglas generales

- Cada tabla tiene `id` entero autoincremental.
- Los borrados con historial son **lógicos** (campo `activo`) para no romper reportes.
- Cambios de esquema mediante migraciones numeradas en `src/db/migraciones/`.
