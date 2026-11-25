# Handoff: Portal Inverplus+ (portal de proyectos inmobiliarios)

## Overview
Portal interno de Inverplus+ Inmobiliaria. El usuario ingresa con correo y clave de 6 dígitos, elige uno de dos proyectos (ECLAT, ESSENZIALE) y entra a los módulos de ese proyecto: Ventas (Lista de Precios, Clientes, Boletas de Venta, Vendedoras), Construcción, Proveedores, Pedidos y Perfil Económico. A nivel empresa hay un módulo de Balance. Cada proyecto maneja sus datos de forma independiente.

Estado: **borrador / modelo de diseño, versión 2 (25 nov 2026)**. Incorpora las observaciones preliminares del cliente (ver «Cambios de la versión 2») y la adaptación a celular. Todos los números, nombres de clientes, vendedoras y contratistas, y la cantidad de departamentos son datos de ejemplo generados en el prototipo.

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
- Derecha (`flex:1.25 1 440px`, fondo `#F3F0EA`): lista de 8 filas, cada una con número, (grupo "Ventas" en las cuatro primeras), nombre en Cormorant `clamp(24px,2.3vw,32px)`, descripción 13px, dato en vivo y flecha. Hover: fondo `#2E2E2E`, texto `#F3F0EA`, `padding-left:26px`.
  1. Lista de Precios · 2. Clientes · 3. Boletas de Venta · 4. Vendedoras · 5. Construcción · 6. Proveedores · 7. Pedidos · 8. Perfil Económico.

### 4. Módulos (pantalla de trabajo)
- Barra lateral fija de 224px (`#1C1B1A`): logo, bloque del proyecto con miniatura (vuelve al índice), navegación (grupo "Ventas": Lista de Precios, Clientes, Boletas de Venta, Vendedoras; grupo "Obra y resultado": Construcción, Proveedores, Pedidos, Perfil Económico), y abajo "← Proyectos", "Balance Empresa", correo y "Salir". Ítem activo: fondo `rgba(243,240,234,.12)`, borde izquierdo 2px acento, peso 700.
- Área principal (fondo `#F3F0EA`, padding `clamp(20px,3vw,44px)`): migas "+ PROYECTO · Ventas" en acento, título Cormorant `clamp(36px,3.8vw,58px)`, y franja de 4 indicadores (rejilla `auto-fit, minmax(200px,1fr)`, celdas `#FBFAF7`, valor Cormorant 32px).

**Lista de Precios** — tres pestañas con su propio inventario y precios: **Departamentos**, **Estacionamientos** y **Depósitos**.
- Los indicadores (Total / Disponibles / Separados / Vendidos) y la leyenda son **botones**: al tocarlos filtran el plano (lo demás se atenúa) y debajo aparece la lista de las unidades de ese estado con su precio. "Ver todos" quita el filtro.
- Barra de proporción y plano: departamentos por piso (de arriba hacia abajo); estacionamientos y depósitos por sótano, en filas de 6. Cada celda muestra número y precio de venta abreviado ("412k"), coloreada por estado (Vendido = acento, Separado = `#D9B36A`, Disponible = `#FBFAF7` con borde `#CFC9BD`). Clic selecciona (contorno 2px `#23221F`).
- Panel de la unidad: número, piso o nivel, área, vista, **Precio de lista**, **Descuento** (campo editable, muestra su %) y **Precio de venta** (lista − descuento), selector de estado, y si está vendida: cliente y vendedora con enlace a su ficha. Un estacionamiento o depósito vendido indica con qué departamento se vendió.

**Clientes** — tabla: Cliente (con DNI y cónyuge), Inmueble (departamento + estacionamiento/depósito), Vista, m², Vendedora, Venta (Contado/Crédito, y US$ si aplica), Precio de venta, Monto pagado, Letras por pagar. Cada fila se expande en una ficha con cinco pestañas:
- **Cronograma de pagos**: Concepto, Vencimiento, Monto, Fecha de pago, Importe pagado, N° Boleta, Detracción, Estado. Las letras pendientes tienen "Registrar pago" (fecha, importe, N° de boleta). Al escribir o elegir un N° de boleta ya registrado en Boletas de Venta, el importe y la **detracción se jalan de la boleta**.
- **Datos del cliente**: titular y DNI, cónyuge o segundo titular y su DNI (ambos en un solo inmueble), celular, correo, dirección, profesión, medio de contacto.
- **Venta e inmuebles**: forma de venta (contado/crédito), moneda (soles/dólares; en dólares pide el T.C. de la venta), promoción/descuento, regalo; lista de inmuebles de la venta, cada uno con precio de lista, descuento y precio de venta; formulario para **agregar un estacionamiento o depósito** (también meses después) con su precio, fecha de compra, cuota inicial y N° de letras, que se suman al cronograma.
- **Trámite y fechas**: fecha de separación, firma de minuta, firma de escritura, kardex, notaría, fecha de desembolso, AFP (importe) y fecha de AFP.
- **Observaciones**: observación comercial para obra (modificaciones del departamento), observación de pago, penalidad e importe de penalidad.

**Boletas de Venta** — registro de boletas: N° Boleta, Fecha, Cliente, Inmueble, Concepto, Importe, **Detracción** (importe × tasa; la tasa es un campo editable, 4% por defecto como valor de ejemplo, a confirmar con contabilidad) y Constancia. Buscador, y formulario "+ Registrar boleta". Una boleta registrada sin asignar aparece como "Sin asignar a un pago" y se ofrece al registrar el pago de una letra de ese cliente.

**Vendedoras · Comisiones** — bloque "% de comisión pactado" con cuatro tasas editables: vista externa/interna × contado/crédito (valores de ejemplo). Una sección por vendedora (plegable): comisión total, pagado y por pagar; por cada venta: Dpto, Vista · Venta, Precio de venta, **% Comisión** (toma la tasa pactada y se puede cambiar por venta), Comisión, y el pago en dos partes — **60% a la firma de minuta** y **40% al desembolso** — cada una con su fecha de pago.

**Construcción** — el **terreno va aparte** (franja oscura propia) y no se suma a la construcción. Bloque "por tipo de gasto" (Obra / Comercial / Administrativo, con barra apilada). Tabla mes a mes desde el **Mes 1**: Mes, barra apilada por tipo, Gastos del mes, Acumulado (solo construcción). Al elegir un mes se ven sus gastos diarios y un formulario (Día, Concepto, **Tipo**, Monto); el tipo también se cambia en cada gasto. Los tres tipos suman al total de construcción del Perfil Económico.

**Proveedores** — tabla por contratista: Contratista · Partida, Presupuesto aprobado, Última valorización, Factura, Acumulado pagado (con barra y aviso de lo valorizado por pagar), Saldo. Cada fila se expande con sus valorizaciones (N°, fecha, factura, **PDF de la factura** adjuntable, **fecha de pago**, monto) y un formulario para registrar una valorización con su fecha de pago y su PDF. Botón "+ Nuevo contratista" (Contratista, Partida, Presupuesto aprobado).

**Pedidos** — compras de materiales y servicios contratados.
- "Acumulado por material": una celda por material y unidad con la suma de cantidades de todos sus pedidos (bolsas, kg, m, m², m³, und…), más los servicios contratados.
- Tabla: Fecha, Proveedor · RUC, Pedido (compra o servicio), Cantidad, Importe, Forma de pago (con lo pagado y el saldo), Garantía · Protocolos. Cada fila se expande con sus pagos (adelanto 10/20/50% y cancelación a la entrega, contado o crédito a 30 días), cada uno con fecha editable y estado Pagado/Pendiente, y los interruptores "¿Envió carta de garantía?" y "¿Envió protocolos?".
- "+ Nuevo pedido o servicio": fecha, RUC, proveedor, tipo, pedido, cantidad, unidad, importe, forma de pago, fecha de entrega, carta de garantía, protocolos.

**Perfil Económico** — bloque oscuro con la ecuación en tipografía grande: Ventas − Compra de terreno − Construcción = **Utilidad** (Cormorant `clamp(48px,8.4vw,136px)`, con borde superior 3px acento) y margen %. Debajo, barra de proporción terreno / construcción / utilidad y el desglose de construcción por tipo. Las ventas consideran el precio de venta (con descuentos) de departamentos, estacionamientos y depósitos. En ESSENZIALE el primer término se rotula "Ingresos" (así viene en el requerimiento).

**Balance Empresa** — rejilla de 4 bloques: Ingresos por Proyecto, Gastos por Proyecto, Saldo Ctas Ordinarias, Saldo Ctas Garantias. Cada bloque: total grande y una fila por proyecto con barra. Los dos primeros en fondo oscuro, los dos últimos en claro.

### 5. Celular (ancho ≤ 860px)
- La barra lateral se oculta. Arriba queda una **barra fija** (56px) con el botón de menú, el proyecto y el logo; abajo, una **barra de accesos** (58px): Precios, Clientes, Obra, Perfil y Menú. El menú abre la barra lateral como panel deslizante (86vw, máx. 320px) sobre un velo oscuro.
- Indicadores en rejilla de 2 columnas. Las tablas dejan de desplazarse hacia los lados: cada fila pasa a ser una **ficha** con sus datos rotulados (atributo `data-l`), en 2 columnas (3 en el cronograma de letras).
- Lista de Precios: el plano ocupa todo el ancho; al tocar una unidad aparece una franja fija con su precio, y "Ver ficha" abre el panel de la unidad a pantalla completa.
- Formularios en una columna (≤ 520px), campos de 44px con texto de 16px (evita el zoom de iOS), teclado numérico en montos y selector de fecha nativo.
- Ingreso: fotos arriba (40% del alto) y formulario a todo el ancho. Selección: los dos proyectos lado a lado. Índice de módulos: foto arriba y lista debajo con el dato en vivo bajo cada módulo.

## Cambios de la versión 2
Responden al documento «Observaciones preliminar sistema» del cliente:
1. Lista de Precios: estados cliqueables como filtro; Descuento y Precio de venta bajo el Precio de lista; listas de estacionamientos y depósitos con su propio precio.
2. Clientes: ficha completa (contado/crédito, moneda y T.C., medio de contacto, estacionamiento y depósito con su precio y sus letras, DNI de ambos esposos, celular, dirección, correo, profesión, promoción, regalo, observaciones, penalidad, fechas de separación/minuta/escritura, kardex, notaría, desembolso, AFP) y cronograma con fecha de pago, importe pagado y detracción jalada de la boleta. Apartado propio de Boletas de Venta.
3. Comisiones: % variable por venta según vista y forma de venta; pago 60% minuta / 40% desembolso con fecha en cada parte.
4. Construcción: terreno aparte; gastos desde el mes 1 con acumulado; tipo de gasto obra/comercial/administrativo.
5. Módulo de Pedidos, debajo de Proveedores.
6. Proveedores: PDF de la factura y fecha de pago por valorización.
7. Celular: rediseño completo de la vista angosta (antes la barra lateral tapaba el contenido).

## Interactions & Behavior
- Navegación por estado: `login → select → hub → work` (módulo) y `work/balance`. "Salir" vuelve al ingreso. Al cargar siempre abre en el ingreso; solo recuerda el correo.
- Enlaces directos del prototipo (para demostraciones): `#/proyectos`, `#/eclat`, `#/essenziale/clientes`, `#/empresa`, etc. abren esa pantalla sin pasar por el ingreso. No portar a producción.
- Cambiar el estado o el descuento de una unidad actualiza indicadores, Clientes (reparte el saldo entre las letras pendientes), Vendedoras, Perfil Económico y Balance.
- Registrar gasto / valorización / contratista / pedido / boleta / pago de letra actualiza totales al instante (en memoria; no persiste). El PDF adjunto se abre desde el navegador y tampoco se guarda.
- Transiciones: aparición de pantalla con fundido .5–.6s; hovers .2–.35s.
- Responsivo: flex con wrap y `clamp()`; las tablas anchas tienen scroll horizontal hasta 860px y por debajo pasan a fichas (ver «5. Celular»).

## State Management
- Sesión: `screen`, `proj` (eclat | essenziale), `mod`, `email`.
- Por proyecto: departamentos, estacionamientos y depósitos (id, piso/nivel, m², vista, precio de lista, descuento, estado, dueño); clientes (ficha, inmuebles de la venta, letras con fecha de pago, importe y boleta); boletas (número, fecha, importe, constancia, asignada o no); tasas de comisión pactadas, % por venta y fechas de pago 60/40; compra de terreno; gastos por mes con tipo; contratistas y valorizaciones (factura, PDF, fecha de pago); pedidos (proveedor, RUC, cantidad, unidad, importe, forma de pago, pagos, garantía, protocolos); saldos de cuentas.
- En producción estos datos deben venir de una API/base de datos; el prototipo los genera con una semilla fija dentro de `db()` y `client()`.
- Reglas de cálculo: Precio de venta = precio de lista − descuento; Comisión = precio de venta del departamento × % (60% a la minuta, 40% al desembolso); Detracción = importe de la boleta × tasa; Acumulado de construcción = suma de gastos mensuales desde el mes 1 (sin terreno); Acumulado pagado a proveedor = valorizaciones con fecha de pago; Saldo proveedor = presupuesto − suma de valorizaciones; Utilidad = ventas − terreno − construcción (obra + comercial + administrativo).

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
- `Portal Inverplus-print.dc.html` — documento de 21 hojas A4 horizontal con todas las pantallas (requiere `doc-page.js`).
- `../movil.html` — página de presentación de la vista en celular: ocho teléfonos con el prototipo funcionando a 375px de ancho.
- `support.js`, `doc-page.js` — runtime del prototipo; no portar.
- `Requerimiento Sr. Alex.docx` — requerimiento original con la lista de módulos.
