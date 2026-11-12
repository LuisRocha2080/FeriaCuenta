<div align="center">

<img src="docs/assets/logo.svg" alt="Logo de FeriaCuenta" width="120" />

# 🥬 FeriaCuenta

**Ventas, compras y ganancia del día para comerciantes de feria y mercado, con teclado grande y sin internet.**

[![Licencia: MIT](https://img.shields.io/badge/licencia-MIT-blue.svg)](LICENSE)
[![CI](https://github.com/LuisRocha2080/FeriaCuenta/actions/workflows/ci.yml/badge.svg)](https://github.com/LuisRocha2080/FeriaCuenta/actions/workflows/ci.yml)
![Estado](https://img.shields.io/badge/estado-fase%20inicial-orange)
![React Native](https://img.shields.io/badge/React%20Native-Expo-0a7ea4)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178c6)
![SQLite](https://img.shields.io/badge/SQLite-local-003b57)
![Offline](https://img.shields.io/badge/offline-first-2ea44f)
![Costo de licencias](https://img.shields.io/badge/licencias-%240-success)

[Inicio rápido](#-inicio-rápido) · [Características](#-características) · [Arquitectura](#️-arquitectura) · [Roadmap](#️-roadmap) · [Pruebas](#-pruebas) · [Limitaciones](#-lo-que-todavía-no-existe) · [Contribuir](#-contribuir)

</div>

El comerciante compra en la madrugada, vende todo el día y cierra sin saber si ganó: el dinero se mezcla con el del hogar y no distingue costo de ganancia. **FeriaCuenta** es una app móvil (Android) hecha con React Native + Expo y SQLite local, pensada para comerciantes de feria, puestos de mercado y vendedores de frutas, verduras y abarrotes. Funciona sin internet, sin servidores y sin licencias de pago. **Todavía no es una app lista para usar:** hoy el repositorio contiene la especificación, el plan, el modelo de datos, el diseño de pantallas y la base de configuración; el código de la app llega por fases (ver [Roadmap](#️-roadmap) y [Lo que todavía no existe](#-lo-que-todavía-no-existe)).

## 🎬 Vista rápida

> Aún no hay capturas: la app no está implementada. Las pantallas planificadas están descritas en [docs/PANTALLAS.md](docs/PANTALLAS.md) y se agregarán capturas reales al cerrar la primera fase.

Flujo principal:

```
Vender → Comprar → Gastos → Cierre del día → Productos → Historial
```

| Pantalla | Qué muestra |
|---|---|
| Vender | Cuadrícula de productos con precio y cantidad rápida. |
| Comprar | Compras del día con costo total y unidad. |
| Gastos | Gastos del puesto por categoría. |
| Cierre del día | Resumen con ganancia estimada y diferencia contra el efectivo contado. |
| Productos | Catálogo con precio de venta y último costo. |
| Historial | Totales por semana y mes. |

## ✨ Características

| Característica | Detalle |
|---|---|
| Venta rápida con | Venta rápida con botones grandes por producto, por peso o por unidad. |
| Registro de compras | Registro de compras de mercadería con costo por unidad. |
| Gastos del puesto | Gastos del puesto (alquiler, transporte, bolsas, ayudante). |
| Cierre del día | Cierre del día: ventas, compras, gastos y ganancia estimada. |
| Margen por producto | Margen por producto para saber qué conviene vender. |
| Historial semanal y | Historial semanal y mensual en gráfico simple. |

Todos los datos viven en el dispositivo (SQLite): sin cuentas, sin suscripciones y sin servicios de pago.

## 🏗️ Arquitectura

```mermaid
flowchart LR
    U[Usuario] --> UI[Pantallas Expo Router]
    UI --> L[Lógica y validaciones]
    L --> DB[(SQLite local)]
    L --> X[Exportar CSV / PDF]
    L --> W[Enlaces wa.me y mapas]
```

| Capa | Tecnología |
|---|---|
| App | React Native + Expo (TypeScript) |
| Datos | SQLite local (`expo-sqlite`) |
| Navegación | Expo Router |
| Pruebas | Jest + `tsc --noEmit` |
| Distribución | APK directo / EAS Build local |

**Modelo de datos**

| Tabla | Campos |
|---|---|
| `productos` | id, nombre, unidad (kg / unidad / atado / caja), precio_venta, costo_ultimo, activo |
| `compras` | id, fecha, producto_id, cantidad, costo_total |
| `ventas` | id, fecha, producto_id, cantidad, monto |
| `gastos` | id, fecha, categoria, monto, nota |
| `cierres` | id, fecha, ventas, compras, gastos, efectivo_contado |

<details>
<summary>Estructura de carpetas</summary>

```
FeriaCuenta/
├── app/                 # pantallas (Expo Router)
├── src/
│   ├── components/      # componentes de interfaz
│   ├── db/              # esquema y consultas SQLite
│   └── lib/             # lógica y validaciones
├── docs/                # especificación, roadmap, planificación, datos, pantallas, pruebas, backlog y negocio
├── .github/             # CI, CodeQL, Dependabot, plantillas de issues y PR
├── app.json · package.json · tsconfig.json
└── LICENSE · CHANGELOG.md · CONTRIBUTING.md · SECURITY.md · SUPPORT.md
```

</details>

## 🗺️ Roadmap

1. **Base y navegación:** Proyecto Expo + TypeScript, Esquema SQLite, Tema de alto contraste
2. **Productos y venta rápida:** Catálogo de productos, Pantalla de venta con deshacer
3. **Compras y gastos:** Compras con costo, Gastos del puesto
4. **Cierre y margen:** Cierre del día, Margen por producto
5. **Historial y piloto:** Gráficos semanales, Exportación CSV, APK de prueba con 5 puestos piloto

Detalle fase por fase en [docs/ROADMAP.md](docs/ROADMAP.md). Documentación completa: [SPEC](docs/SPEC.md) · [PLANNING](docs/PLANNING.md) · [DATOS](docs/DATOS.md) · [PANTALLAS](docs/PANTALLAS.md) · [PRUEBAS](docs/PRUEBAS.md) · [BACKLOG](docs/BACKLOG.md) · [NEGOCIO](docs/NEGOCIO.md).

## 💼 Modelo comercial

| Aspecto | Detalle |
|---|---|
| Cómo se vende | Pago único muy bajo con difusión boca a boca, o plan mensual simbólico. |
| Precio de partida | Hipótesis a validar: Bs 60–100 pago único. |
| Canal | Visita a ferias barriales y capacitación presencial de 15 minutos por puesto. |
| Piloto | 5 puestos por 30 días, midiendo cuántos cierran el día con la app y cuántos dicen conocer su ganancia. |

Los precios son hipótesis para validar con clientes reales, no resultados medidos.

## 🚀 Inicio rápido

| Requisito | Versión |
|---|---|
| Node.js | 18+ |
| npm | 9+ |
| Android | Expo Go o emulador |

Clona el repositorio y entra a la carpeta.

```bash
git clone https://github.com/LuisRocha2080/FeriaCuenta.git
cd FeriaCuenta
```

Cuando exista el código de la app (fase 1 del roadmap), se instalará y arrancará así:

```bash
npm install
npm start        # Expo; escanea el QR con Expo Go
npm run android  # o en el emulador
```

> **No verificado:** `package.json` todavía no declara dependencias, así que `npm install` y `npm start` aún no levantan una app. Los scripts `npm test` y `npm run typecheck` sí están definidos y pasan sin pruebas todavía.

<details>
<summary>Variables de entorno</summary>

FeriaCuenta no usa variables de entorno ni claves de API: todo funciona en el dispositivo. `.env.example` queda como plantilla vacía por si se agrega una integración (declarala sin valores reales).

</details>

## 🧪 Pruebas

Casos que la suite debe cubrir (definidos en [docs/PRUEBAS.md](docs/PRUEBAS.md)):

- Venta rápida con 200 toques seguidos sin demora perceptible.
- Deshacer venta y verificar totales del día.
- Cierre con diferencia positiva y negativa.
- Lectura de la pantalla bajo luz intensa (prueba manual).
- Cambio de precio con ventas previas.

Hoy `npm test` corre Jest sin pruebas (`--passWithNoTests`) y `npm run typecheck` ejecuta `tsc --noEmit`. El pipeline de CI y el análisis CodeQL corren en GitHub Actions en cada push y PR a `main`.

## 🔒 Seguridad

**Implementado:** no hay cuentas, contraseñas ni servidores; no se envían datos a terceros. El repositorio tiene activados el reporte privado de vulnerabilidades, Dependabot y la protección de secretos, y hay un workflow de CodeQL.

**Avisos importantes:**

- La base SQLite local no está cifrada: quien tenga acceso al dispositivo desbloqueado puede ver los datos.
- No hay copia de respaldo en la nube; si se pierde el teléfono se pierden los datos (la exportación a CSV/PDF está prevista en el diseño, ver [docs/SPEC.md](docs/SPEC.md)).
- Los problemas de seguridad se reportan según [SECURITY.md](SECURITY.md).

## 🚧 Lo que todavía no existe

- **La app en sí:** el repositorio es la base documental y de configuración; las pantallas, la base de datos y la lógica se construyen fase por fase (ver Roadmap).
- El costo de lo vendido se estima con el último costo de compra, no con lotes.
- Sin sincronización entre teléfonos.
- No emite facturas.
- Sin capturas de pantalla, sin pruebas automáticas reales y sin APK publicado.
- Los precios y el piloto del modelo comercial son hipótesis sin validar.

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Leé la [guía de contribución](CONTRIBUTING.md) y el [código de conducta](CODE_OF_CONDUCT.md) antes de abrir un PR. Para bugs o ideas usá las plantillas de issues; los problemas de seguridad se reportan según la [política de seguridad](SECURITY.md). ¿Dudas? Mirá [SUPPORT.md](SUPPORT.md). Los cambios por versión están en el [CHANGELOG](CHANGELOG.md).

## 📄 Licencia

Distribuido bajo la licencia MIT. Ver [LICENSE](LICENSE).

---

<div align="center">Hecho por <a href="https://github.com/LuisRocha2080">LuisRocha2080</a> · ventas, compras y ganancia del día para comerciantes de feria y mercado, con teclado grande y sin internet. con React Native, Expo y SQLite</div>
