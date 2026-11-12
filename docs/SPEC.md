# Especificación — FeriaCuenta

Requisitos escritos con el patrón EARS («Cuando…, el sistema deberá…»). Cada uno es verificable con una prueba (ver [PRUEBAS.md](PRUEBAS.md)).

## Alcance de la versión 1.0

Ventas, compras y ganancia del día para comerciantes de feria y mercado, con teclado grande y sin internet. Funciona en un solo dispositivo, sin cuentas de usuario y sin servidor.

## Requisitos funcionales

| ID | Requisito |
|---|---|
| R01 | Cuando el usuario toca un producto en la pantalla de venta, el sistema deberá registrar la venta con la cantidad y el precio vigentes. |
| R02 | Cuando el usuario deshace la última venta, el sistema deberá revertirla sin dejar registros huérfanos. |
| R03 | Cuando se registra una compra, el sistema deberá actualizar el último costo del producto. |
| R04 | El sistema deberá estimar la ganancia del día como ventas menos costo de lo vendido menos gastos. |
| R05 | Cuando el usuario ingresa el efectivo contado al cierre, el sistema deberá mostrar la diferencia contra el efectivo esperado. |
| R06 | El sistema deberá mostrar botones y textos legibles con luz solar directa (alto contraste y tamaño mínimo de 48 dp). |
| R07 | Si el dispositivo está sin conexión, el sistema deberá funcionar con todas sus funciones. |
| R08 | Cuando se cambia el precio de un producto, el sistema no deberá alterar el monto de ventas ya registradas. |

## Requisitos no funcionales

| ID | Requisito |
|---|---|
| N01 | La app deberá abrir en menos de 3 segundos en un teléfono Android de gama baja (2 GB de RAM). |
| N02 | Todos los datos deberán almacenarse en SQLite local y no enviarse a ningún servidor. |
| N03 | La interfaz deberá estar en español con montos en bolivianos (Bs) y fechas dd/mm/aaaa. |
| N04 | Los botones táctiles deberán medir al menos 48 dp. |
| N05 | La app deberá operar completa sin conexión a internet. |
| N06 | El costo de licencias de cualquier dependencia deberá ser cero. |

## Fuera de alcance (v1.0)

- El costo de lo vendido se estima con el último costo de compra, no con lotes.
- Sin sincronización entre teléfonos.
- No emite facturas.

## Criterios de aceptación globales

1. Un usuario nuevo registra su primer dato útil en menos de 5 minutos.
2. Ningún dato se pierde al cerrar la app de forma abrupta.
3. Los totales coinciden con un cálculo manual en los casos de prueba de [PRUEBAS.md](PRUEBAS.md).
