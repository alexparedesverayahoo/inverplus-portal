# Handoff: Portal Inverplus+ (portal de proyectos inmobiliarios)

## Overview
Portal interno de Inverplus+ Inmobiliaria. El usuario ingresa con correo y clave de 6 dígitos, elige uno de dos proyectos (ECLAT, ESSENZIALE) y entra a los módulos de ese proyecto: Ventas (Lista de Precios, Clientes, Vendedoras), Construcción, Proveedores y Perfil Económico. A nivel empresa hay un módulo de Balance. Cada proyecto maneja sus datos de forma independiente.

Estado: **borrador / modelo de diseño**. Todos los números, nombres de clientes, vendedoras y contratistas, y la cantidad de departamentos son datos de ejemplo generados en el prototipo.

## About the Design Files
Los archivos de este paquete son **referencias de diseño hechas en HTML**: prototipos que muestran el aspecto y el comportamiento esperados, no código de producción para copiar tal cual. La tarea es **recrear estos diseños en el entorno del código destino** (React, Vue, etc.) con sus patrones y librerías; si aún no existe un entorno, elegir el framework más adecuado e implementarlos ahí. El prototipo no tiene backend, autenticación real ni persistencia.

`Portal Inverplus.dc.html` es un "Design Component": un HTML con plantilla de estilos en línea + una clase de lógica (`class Component`) al final del archivo. `support.js` es solo el runtime del prototipo; no se porta.

## Fidelity
**Alta fidelidad (hifi)** en colores, tipografía, espaciado e interacciones. Recrear la UI con precisión. Los datos son ficticios.

## Flujo
1. **Ingreso** → 2. **Selección de proyecto** → 3. **Índice de módulos** del proyecto → 4. **Módulo** (con barra lateral). Desde Selección o la barra lateral también se llega a **Balance Empresa**.

## Screens / Views

### 1. Ingreso
- Layout: fila flex con wrap, alto mínimo 100vh, fondo `#1C1B1A`.
- Izquierda (`flex:1 1 520px`, mín. 56vh): dos fotos lado a lado (`gap:2px`), cada una `object-fit:cover`. ECLAT usa `eclat-angulo.jpg` con `object-position:35% 36%; transform:scale(1.17); transform-origin:10% 42%` (recorta un árbol cortado en el borde derecho). ESSENZIALE usa `essenziale-angulo.jpg`, `object-position:50% 36%`. Degradado inferior `linear-gradient(180deg, rgba(28,27,26,0) 72%, rgba(28,27,26,.8) 100%)`. Abajo a la izquierda: etiqueta "+ Proyecto 01/02" (11px, 600, tracking .3em, mayúsculas) y nombre en Cormorant Garamond 500, `clamp(26px,3.1vw,56px)`, tracking .04em.
- Derecha (`flex:0 1 296px`, padding 28px, centrado vertical): logo blanco (alto 42px), título "Portal de proyectos" (Cormorant 500, 24px), texto "Ingrese con su correo y su clave de 6 dígitos." (13px, `#B5B0A6`), campo Correo y campo Clave, botón "Ingresar".
- Campos: alto 46px, padding 0 12px, fondo `rgba(243,240,234,.05)`, borde inferior 1px `rgba(243,240,234,.45)` (foco: `#F3F0EA`), texto 15px `#F3F0EA`. Etiquetas 10px, 600, tracking .22em, mayúsculas, `#B5B0A6`. Clave: `type=password`, `inputmode=numeric`, placeholder "6 dígitos", tracking .3em.
- Botón: alto 48px, fondo acento `#A9492A`, texto blanco 12px 600 tracking .2em mayúsculas; hover `filter:brightness(1.15)`.
- Validación: correo con formato `algo@algo.algo` y clave de exactamente 6 dígitos (solo se aceptan dígitos, máx. 6). Error: "Ingrese un correo válido y su clave de 6 dígitos." (12px, `#F0B49A`).

### 2. Selección de proyecto
- Fondo `#1C1B1A`, texto `#F3F0EA`. Cabecera: logo (32px) a la izquierda; correo del usuario y botón "Salir" (borde 1px, 36px de alto) a la derecha. Debajo: título "Seleccione un proyecto" (Cormorant 500, `clamp(32px,3.8vw,56px)`) y "2 proyectos".
- Variante por defecto **Tarjetas verticales**: fila flex centrada, `gap:clamp(56px,18vw,300px)`, con scroll horizontal y `scroll-snap` en pantallas angostas (móvil). Cada tarjeta: ancho `clamp(240px, min(32vw,46vh), 460px)`; foto con `aspect-ratio:4/5`; debajo "+ Proyecto 01", nombre (Cormorant, `clamp(28px,4.4vh,46px)`) con flecha "→" a la derecha, y una fila de 3 cifras separada por línea fina: **Dptos / Vendidos / Separados** (número Cormorant `clamp(26px,3.6vh,36px)`, etiqueta 10px 600 mayúsculas `#D8D3C9`). Hover: `translateY(-6px)`, .35s.
  - Encuadre de foto: ECLAT `object-position:50% 0%; transform:scale(1.15); transform-origin:8% 0%`; ESSENZIALE `object-position:50% 5%`.
- Variante alternativa **Paneles a pantalla completa**: dos paneles `flex:1 1 320px`, alto mín. `max(440px,60vh)`, foto a sangre con nombre sobre la foto; hover `flex-grow:1.6` (.7s).
- Franja inferior **Balance Empresa**: fondo arena `#D9B36A`, texto `#23221F`; hover fondo acento y texto blanco (.25s). Contenido: "+ Empresa", "Balance Empresa" (Cormorant 30px), descripción y flecha.

### 3. Índice de módulos (por proyecto)
- Dos columnas con wrap. Izquierda (`flex:1 1 360px`): foto frontal del proyecto a sangre, logo y botón "← Proyectos" arriba, y abajo "+ Proyecto NN", nombre (Cormorant `clamp(52px,6.6vw,108px)`) y 4 cifras: Departamentos, Vendidos, Separados, Disponibles.
- Derecha (`flex:1.25 1 440px`, fondo `#F3F0EA`): lista de 6 filas, cada una con número, (grupo "Ventas" en las tres primeras), nombre en Cormorant `clamp(24px,2.4vw,34px)`, descripción 13px, dato en vivo y flecha. Hover: fondo `#2E2E2E`, texto `#F3F0EA`, `padding-left:26px`.
  1. Lista de Precios · 2. Clientes · 3. Vendedoras · 4. Construcción · 5. Proveedores · 6. Perfil Económico.

### 4. Módulos (pantalla de trabajo)
- Barra lateral fija de 224px (`#1C1B1A`): logo, bloque del proyecto con miniatura (vuelve al índice), navegación (grupo "Ventas": Lista de Precios, Clientes, Vendedoras; grupo "Obra y resultado": Construcción, Proveedores, Perfil Económico), y abajo "← Proyectos", "Balance Empresa", correo y "Salir". Ítem activo: fondo `rgba(243,240,234,.12)`, borde izquierdo 2px acento, peso 700.
- Área principal (fondo `#F3F0EA`, padding `clamp(20px,3vw,44px)`): migas "+ PROYECTO · Ventas" en acento, título Cormorant `clamp(36px,3.8vw,58px)`, y franja de 4 indicadores (rejilla `auto-fit, minmax(200px,1fr)`, celdas `#FBFAF7`, valor Cormorant 32px).

**Lista de Precios** — debe mostrar el total de departamentos y marcar vendidos y separados.
- Barra de proporción y leyenda (Vendido = acento, Separado = `#D9B36A`, Disponible = `#FBFAF7` con borde `#CFC9BD`).
- Plano por pisos (de arriba hacia abajo): una fila por piso con una celda por departamento (número + precio abreviado "412k"), coloreada por estado. Clic selecciona (contorno 2px `#23221F`).
- Panel lateral del departamento: número, piso, área, vista, precio de lista y selector de estado (Disponible / Separado / Vendido). Si está vendido muestra cliente y vendedora.

**Clientes** — tabla: Cliente, Inmueble, Vista (Interna/Externa), Vendedora, Precio de venta, m², Monto pagado, Letras por pagar. Cada fila se expande para ver el cronograma: Concepto (cuota inicial / letra N de M), Vencimiento, Monto, N° Boleta, Estado (Pagada / Por pagar).

**Vendedoras** — una tarjeta por vendedora: nombre, departamentos vendidos y ventas; campo **% Comisión** editable; **Comisión a pagar** calculada (ventas × %); lista de sus departamentos vendidos con precio y comisión. Los departamentos se toman de los marcados como Vendidos.

**Construcción** — parte de la compra del terreno. Tabla mes a mes: Mes, barra, Gastos del mes, Acumulado (terreno + construcción). Al elegir un mes se ven sus gastos diarios y un formulario (Día, Concepto, Monto) para registrar un gasto.

**Proveedores** — tabla por contratista: Contratista · Partida, Presupuesto aprobado, Última valorización, Factura, Acumulado pagado (con barra de avance), Saldo. Cada fila se expande con sus valorizaciones (N°, fecha, factura, monto) y un formulario para registrar una valorización. Botón "+ Nuevo contratista" (Contratista, Partida, Presupuesto aprobado).

**Perfil Económico** — bloque oscuro con la ecuación en tipografía grande: Ventas − Compra de terreno − Construcción = **Utilidad** (Cormorant `clamp(56px,8.4vw,136px)`, con borde superior 3px acento) y margen %. Debajo, barra de proporción terreno / construcción / utilidad. En ESSENZIALE el primer término se rotula "Ingresos" (así viene en el requerimiento).

**Balance Empresa** — rejilla de 4 bloques: Ingresos por Proyecto, Gastos por Proyecto, Saldo Ctas Ordinarias, Saldo Ctas Garantias. Cada bloque: total grande y una fila por proyecto con barra. Los dos primeros en fondo oscuro, los dos últimos en claro.

## Interactions & Behavior
- Navegación por estado: `login → select → hub → work` (módulo) y `work/balance`. "Salir" vuelve al ingreso. Al cargar siempre abre en el ingreso; solo recuerda el correo.
- Cambiar el estado de un departamento actualiza indicadores, Clientes, Vendedoras, Perfil Económico y Balance.
- Registrar gasto / valorización / contratista actualiza totales al instante (en memoria; no persiste).
- Transiciones: aparición de pantalla con fundido .5–.6s; hovers .2–.35s.
- Responsivo: las pantallas usan flex con wrap y `clamp()`; las tablas anchas tienen scroll horizontal.

## State Management
- Sesión: `screen`, `proj` (eclat | essenziale), `mod`, `email`.
- Por proyecto: departamentos (id, piso, m², vista, precio, estado), clientes y letras, % de comisión por vendedora, compra de terreno, gastos por mes, contratistas y valorizaciones, saldos de cuentas.
- En producción estos datos deben venir de una API/base de datos; el prototipo los genera con una semilla fija dentro de `db()` y `client()`.
- Reglas de cálculo: Comisión = precio de venta × %; Acumulado = terreno + suma de gastos mensuales; Saldo proveedor = presupuesto − suma de valorizaciones; Utilidad = ventas − terreno − construcción.

## Design Tokens
- Carbón profundo `#1C1B1A` · Carbón `#2E2E2E` (color del logo) · Tinta `#23221F`
- Papel `#F3F0EA` · Tarjeta `#FBFAF7` · Líneas `#D9D4CA`, `#E6E1D8`, `#CFC9BD`
- Texto secundario `#6A665F` (sobre claro), `#B5B0A6` / `#D8D3C9` (sobre oscuro)
- Acento terracota `#A9492A` (variable `--ac`, configurable) · Arena `#D9B36A` · Error `#F0B49A`
- Tipografía: **Montserrat** 400/500/600/700 (interfaz, base 14px/1.5) y **Cormorant Garamond** 400/500/600 (títulos, nombres y cifras, con `lining-nums`). Etiquetas en mayúsculas 10–11px, 600, tracking .12–.3em.
- Radios: 0 (esquinas rectas). Sin sombras; separación con líneas de 1px.
- Moneda configurable: `S/` (por defecto) o `US$`.

## Assets
En `assets/` (provistos por el cliente, reducidos a 1800px de alto):
- `eclat-angulo.jpg`, `eclat-frente.jpg` — renders del proyecto ECLAT
- `essenziale-angulo.jpg`, `essenziale-frente.jpg` — renders del proyecto ESSENZIALE
- `logo-blanco.png`, `logo-carbon.png` — logo Inverplus+ Inmobiliaria

## Files
- `Portal Inverplus.dc.html` — prototipo interactivo completo (plantilla + lógica).
- `Portal Inverplus-print.dc.html` — documento de 17 hojas A4 horizontal con todas las pantallas (requiere `doc-page.js`).
- `support.js`, `doc-page.js` — runtime del prototipo; no portar.
- `Requerimiento Sr. Alex.docx` — requerimiento original con la lista de módulos.
