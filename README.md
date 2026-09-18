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
| `img/02-home-primer-viewport.jpg` | 03a |
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

Si falta una captura, la página no muestra un ícono roto: dibuja un recuadro amarillo
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
| `--alerta` | `#C2410C` | Severidad alta |

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

**Índice.** Barra fija a ras del borde superior, a todo el ancho, con los nombres de
sección sin numerar, igual que en la presentación de la Ley 21.719. Los 19 nombres no
caben en 1440 px, así que la lista se desplaza en horizontal y la sección activa se
centra sola. Si se prefiere verlos todos de una vez, hay que acortar los nombres
compuestos (por ejemplo, "Hallazgo 01, evidencia" a "Evidencia") en el atributo
`data-titulo` de cada sección.

**Iconos.** Doce iconos de línea en SVG embebido (secciones 01, 08, 09 y 12), sin
archivos externos. Heredan el color del bloque con `currentColor` y están marcados
`aria-hidden` porque acompañan a un título que ya dice lo mismo.

**Capturas.** Van sin marco de dispositivo. Se midieron los bordes de las 12 imágenes:
casi todas terminan en blanco o casi blanco (luminancia 0,86 a 0,94), así que llevan una
línea de 1 px solo sobre los fondos claros, donde se confundirían con la tarjeta. Sobre
el fondo negro y el azul van sin borde.

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

Todo lo que falta está marcado en la página con un recuadro amarillo `[  ]`
(`<span class="pendiente">`). Ningún dato de negocio fue inventado.

**Contenido**

- [ ] **01 · Método:** modelo de equipo, versión de iOS y versión de la app.
- [ ] **07b · Impacto en el negocio:** los cuatro KPIs (autoatención digital, costo por
      contacto, uso de beneficios del Club y riesgo de fraude), con la data interna de
      la compañía.
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
