# Cuando la app no responde la pregunta que la gente vino a hacer

Presentación web del desafío técnico de **UX Research & Strategy** para MATCH.
Evaluación heurística del flujo de autoatención de la app Entel, plan de investigación
y propuesta de mejora prototipada con IA.

Nicole Matus · nicole.matusp@gmail.com · Septiembre 2026

---

## Estructura de archivos

```
desafio-match/
├── index.html      Presentación completa: HTML, CSS y JS embebidos. Sin dependencias.
├── README.md       Este archivo.
└── img/            Capturas del flujo evaluado (12 archivos, 10 en uso).
```

`index.html` funciona abriendo el archivo directamente (doble clic) y servido desde
GitHub Pages. No usa frameworks, CDN, fuentes externas, librerías de animación ni
`localStorage`.

### Capturas

Las rutas son relativas y sin barra inicial (`img/nombre.jpg`). Las 12 capturas están
en la carpeta; la presentación usa 10:

| Archivo | Se usa en |
|---|---|
| `img/01-interstitial-copec.jpg` | 03b |
| `img/02-home-primer-viewport.jpg` | Portada y 03a |
| `img/03-home-scroll-club.jpg` | 03b |
| `img/04-home-scroll-promos.jpg` | 03b |
| `img/05-interstitial-fibra.jpg` | 04 |
| `img/06-consumo-tarjeta.jpg` | 05a y 10a |
| `img/07-consumo-detalle-llamadas.jpg` | 05b |
| `img/08-menu-que-hacemos-hoy.jpg` | 06a |
| `img/09-club-mis-cupones-vacio.jpg` | 06a y 10b |
| `img/11-ayuda-puntos-no-disponible.jpg` | 06a |
| `img/10-club-beneficios.jpg` | sin usar |
| `img/12-ayuda-sms-fraudulentos.jpg` | sin usar |

Las dos últimas quedaron fuera porque el guion de las secciones no las contemplaba.
Si se quieren incorporar, el lugar natural de `12-ayuda-sms-fraudulentos.jpg` es la
sección 06b, que cita justamente ese artículo, y el de `10-club-beneficios.jpg` es la
columna "Actual" de la sección 10b.

Si falta una captura, la página no muestra un ícono roto: dibuja un recuadro naranja
con el texto "Captura pendiente" y el nombre del archivo que falta.

---

## Sistema de diseño

Todos los colores están declarados como tokens en `:root`, dentro de `index.html`.
Para cambiar uno, se edita solo ahí.

| Token | Valor | Uso |
|---|---|---|
| `--negro` | `#101114` | Texto y fondos oscuros |
| `--gris-texto` | `#5F6470` | Texto secundario |
| `--gris-linea` | `#E2E4E9` | Bordes, divisores y lienzo de fondo |
| `--gris-fondo` | `#F4F5F7` | Secciones neutras |
| `--azul` | `#1226E8` | Acento principal |
| `--azul-palido` | `#DCEAEC` | Secciones de datos |
| `--naranja` | `#F57917` | Reglas, insignias, chips de pendiente |
| `--naranja-palido` | `#FDE7D5` | Fondo de la sección de tensión |
| `--alerta` | `#C2410C` | Filete de la cita antifraude |
| `--exito` / `--exito-palido` | `#166534` / `#DCF0E3` | Severidad 0 a 2 |
| `--aviso` | `#9A3412` | Texto de la severidad 3 |
| `--peligro` / `--peligro-palido` | `#991B1B` / `#FEE2E2` | Severidad 4 |

**Sobre el naranja.** El sitio actual de Entel ya no usa naranja: su identidad vigente
es azul (`#002EFF`). El naranja corresponde a la identidad anterior y el valor `#F57917`
viene de una ficha de marca de terceros, no del manual oficial. Si se consigue el valor
del manual, se cambia el token `--naranja` y se propaga a toda la página.

El naranja funciona como color de texto sobre blanco por debajo del mínimo (2,8:1), así
que no se usa en tipografía. Como fondo a página completa con texto negro daba 6,8:1:
pasa el mínimo, pero el texto vibraba. Por eso los campos grandes usan `--naranja-palido`
(negro sobre él: 15,8:1) y el naranja fuerte queda en reglas, insignias y chips, donde
el texto es corto, en negrita y en mayúsculas.

**Geometría.** Cada sección es una tarjeta redondeada (`--radio: 24px`) sobre un lienzo
gris. Los tokens `--gutter` y `--tope` controlan la separación entre tarjetas y el
espacio que reserva la barra de índice.

**Índice.** Barra fija a ras del borde superior, a todo el ancho, con los nombres sin
numerar, igual que en la presentación de la Ley 21.719. No lista las 19 secciones sino
11 grupos: una entrada puede cubrir varias secciones y el enlace lleva a la primera.
Los grupos se declaran con el atributo `data-grupo` en cada `<section>`; las secciones
sin ese atributo forman grupo propio con su `data-titulo`. Así la barra cabe entera en
1440 px sin desplazamiento horizontal, y el contador de la derecha sigue mostrando la
sección exacta. Para mover una sección de grupo basta cambiar su `data-grupo`.

**Impacto en el negocio (07b).** Los cuatro KPI usan cifras públicas y una medición
propia, cada una con su fuente en 11 px bajo el bloque. La medición propia va con la
cifra en `--azul` para distinguirla de las referencias externas. Cierra con el modelo de
ahorro anual como fórmula en texto, no como imagen, para que se lea en el PDF y con
lector de pantalla. Las fuentes van sin enlaces, a propósito, para que se impriman igual.

**Líneas.** Cada bloque se marca con un icono o con una marca corta de 32 px, nunca
con una regla a todo el ancho. Solo quedan dos líneas largas por lámina: la del rótulo
de sección y la de la nota al pie. La lámina 12 pasó de nueve reglas a dos.

**Pendientes.** Los huecos `[  ]` usan relleno naranja pálido con filete naranja, y
filete discontinuo cuando ocupan el lugar de una cifra grande. Antes eran naranja
sólido y pesaban como botones.

**Heurísticas.** Cada referencia `#N` abre una explicación breve del criterio al pasar
el cursor. Un tooltip solo de hover deja fuera a quien navega con teclado, así que
también aparece al enfocar la referencia con Tab, se cierra con Esc y la referencia
lleva `aria-describedby` mientras está abierta. Las definiciones viven en el objeto
`HEURISTICAS` del script. Al imprimir, el tooltip no existe: el nombre del criterio ya
está escrito junto al número.

**Severidad.** Las insignias usan colores de estado según el número, tanto en los
hallazgos como en la columna de la tabla de síntesis: verde para 0 a 2, naranja para 3
y rojo para 4. El relleno es pastel y el color de estado va en el texto y el filete, lo
que da entre 6,1 y 6,8 de contraste sin el peso de un bloque saturado. En la evaluación
solo aparecen severidades 3 y 4; el verde queda definido para completar la escala.

**Iconos.** Veinte iconos de línea en SVG embebido (secciones 01, 08, 09, 11 y 12), sin
archivos externos. Heredan el color del bloque con `currentColor` y están marcados
`aria-hidden` porque acompañan a un título que ya dice lo mismo.

**Capturas.** Van sin marco de dispositivo y sin recuadro: la caja del `img` se ajusta
a la imagen en vez de ocupar la columna entera. Se midieron los bordes de las 12
imágenes y casi todas terminan en blanco o casi blanco (luminancia 0,86 a 0,94), así
que el contraste con el fondo lo da un filete de 1 px al 7 % y una sombra corta al 9 %,
aplicados sobre la propia imagen. Sobre el negro y el azul, el filete es blanco al 16 %.
Al imprimir queda solo el filete, sin desenfoque.

---

## Publicar en GitHub Pages

1. Crear el repositorio y subir los archivos:

```bash
git init && git add . && git commit -m "Presentación desafío MATCH"
```

2. Conectarlo con el repositorio remoto y empujar la rama principal:

```bash
git branch -M main && git remote add origin https://github.com/USUARIO/REPO.git && git push -u origin main
```

3. En GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   rama `main`, carpeta `/ (root)`, y guardar.

4. A los pocos minutos queda disponible en
   `https://USUARIO.github.io/REPO/` (toma `index.html` automáticamente).

---

## Exportar el PDF

Desde Chrome, sobre la página publicada o el archivo local:

1. `Cmd + P` (Mac) o `Ctrl + P` (Windows).
2. **Destino:** Guardar como PDF.
3. **Diseño:** Horizontal.
4. **Tamaño de papel:** A4.
5. **Márgenes:** Predeterminados (la hoja de estilos ya fija 12 mm).
6. **Más opciones → activar "Gráficos de fondo"**. Sin esto se pierden los fondos de
   color y la presentación queda en blanco y negro.
7. **Escala:** Predeterminada.

Resultado: **19 páginas, una por sección**, en A4 horizontal y con los fondos de color.

---

## Navegación

| Acción | Tecla |
|---|---|
| Avanzar | ↓, barra espaciadora, AvPág |
| Retroceder | ↑, RePág, Shift + espacio |
| Primera sección | Inicio |
| Última sección | Fin |
| Cerrar el índice móvil | Esc |

El índice superior se genera solo desde los atributos `data-titulo` de cada sección y
marca la sección activa. Bajo 760 px de ancho se colapsa en el botón "Índice".

---

## Pendientes por completar

Todo lo que falta está marcado en la página con un recuadro naranja `[  ]`
(`<span class="pendiente">`). Ningún dato de negocio fue inventado.

**Contenido**

- [ ] **10a y 10b:** reemplazar los dos marcos punteados por la salida del prototipo.
- [ ] **11 · Proceso con IA:** pegar el prompt de contexto, el de generación y el de
      refinamiento, anotando qué cambió en cada iteración; indicar la herramienta
      utilizada y el número de iteraciones.

**Prototipo**

- [ ] Reemplazar el `href="#"` de los tres botones `data-prototipo` (portada, 11 y 13)
      por la URL real. Mientras el `href` sea `#`, el botón se muestra como
      "Prototipo: URL pendiente" y no navega.
- [ ] Escribir la URL en las tres líneas `.print-only` para que aparezca en el PDF.
- [ ] Opcional: descomentar el `<iframe>` de la sección 11 y pegar la URL para embeber
      el prototipo en la página.

---

## Verificaciones realizadas

- 19 secciones, un solo `h1`, un `h2` por sección.
- Sin desborde vertical a 1440×900 ni scroll horizontal a 390 px.
- Sin errores en la consola. Las 12 capturas cargan; las 10 referenciadas se resuelven.
- Contraste: 0 elementos bajo el mínimo AA en la auditoría automática, incluidos los fondos naranja, azul y negro.
- PDF de prueba: 19 páginas, una por sección, A4 horizontal, con fondos de color.
- Lectura en voz alta: ~1.950 palabras, entre 13 y 15 minutos.
