# Plan de pruebas — FeriaCuenta

## Automáticas (Jest)

La lógica de cálculo vive en `src/lib/` y se prueba sin interfaz.

- [ ] Venta rápida con 200 toques seguidos sin demora perceptible.
- [ ] Deshacer venta y verificar totales del día.
- [ ] Cierre con diferencia positiva y negativa.
- [ ] Lectura de la pantalla bajo luz intensa (prueba manual).
- [ ] Cambio de precio con ventas previas.

## Manuales en teléfono real

- [ ] Instalación del APK en Android 10 o superior.
- [ ] Uso completo en modo avión.
- [ ] Cierre abrupto de la app y reapertura sin pérdida de datos.
- [ ] Exportación y apertura del archivo en otra app.

## Comandos

```bash
npm test
npx tsc --noEmit
```
