# Cómo actualizar tu web

Hola, Andrea. Esta guía es para que cambies tu web tú misma: añadir un
proyecto, cambiar fotos o textos, cambiar las categorías… Todo se hace con
**Visual Studio Code**, un programa gratuito: cambias los archivos en tu
ordenador y, al subirlos, la web se publica sola.

> **La regla de oro**: solo tocas **dos carpetas**: `data/` (tus proyectos y
> la lista de la home) y `_portada/` (las fotos de la home). Lo demás es el
> código o lo escribe la web sola (`proyectos/`, `index.html`,
> `sitemap.xml`): mejor no tocarlo.

Cuando subes un cambio, la web se actualiza sola en **2 o 3 minutos**. Si te
equivocas en algo, lo normal es que la web se quede como estaba hasta que lo
arregles (punto 7, *Si algo va mal*).

---

## 0. Antes de empezar (solo la primera vez)

1. Instala **Visual Studio Code**: https://code.visualstudio.com
2. Ábrelo y trae la web: a la izquierda, el icono de las ramas
   (**Source Control**) → **Clone Repository** → **Clone from GitHub** → entra
   con tu cuenta → elige `carillagonzalezandrea-source/andreacarilla` → elige
   una carpeta de tu ordenador → **Open**. Si te pide instalar Git, acepta.

Desde aquí, la web es esa carpeta: cada vez que abras VS Code, se abre ahí.

Para preparar las fotos, **imgToWeb**: https://meowrhino.github.io/imgToWeb/
(las pasa al formato de la web, `.webp`, del tamaño justo, y las numera:
`1.webp`, `2.webp`…). **Ábrelo en Chrome o Firefox**, no en Safari: Safari no
sabe hacer `.webp` y imgToWeb se salta las fotos.

---

## 1. Cómo está organizado

```
data/
  home.json                  ← qué proyectos salen en la home, con qué nombre
                               y en qué categoría; y las fotos de la home
  tuttiPari/                 ← un proyecto, una carpeta
    tuttiPari.json           ← los textos del proyecto
    img/                     ← sus fotos: 1.webp, 2.webp, 3.webp…
  diario/
    diario.json
    img/
  …
_portada/                    ← las fotos de la home: 1/, 2/, 3/ (los botones 1 2 3)
formateador.html             ← un formulario que te escribe el .json de un proyecto
```

El **nombre de la carpeta** de un proyecto (el *slug*) es su dirección en la
web: `data/tuttiPari/` → `andreacarilla.work/proyectos/tuttiPari/`. Sin
espacios ni tildes. El `.json` de dentro se llama igual que la carpeta.

---

## 2. Cómo se hace un cambio con VS Code

1. **Antes de nada, baja la última versión**: en la barra de abajo del todo,
   pulsa las flechas ⟳ (**Sync**). Es importante: cada vez que subes algo, la
   web genera sus páginas y las guarda en GitHub, así que siempre hay algo
   nuevo que bajar.
2. En la columna de la izquierda, abre el archivo (por ejemplo
   `data/tuttiPari/tuttiPari.json`) y cambia lo que quieras. Guarda con
   **Cmd+S**. Si algo sale **subrayado en rojo**, hay una coma o unas comillas
   mal: arréglalo antes de seguir (punto 7).
3. A la izquierda, el icono de las ramas (**Source Control**): escribe en una
   línea qué has cambiado ("texto de tutti pari") y pulsa **Commit**.
4. Pulsa **Sync Changes** (el mismo botón azul).

Ya está: en 2-3 minutos sale en la web.

**Para añadir fotos**: arrástralas a su carpeta (por ejemplo
`data/tuttiPari/img/`) en la columna de la izquierda de VS Code, y luego los
pasos 3 y 4.

---

## 3. Lo que más vas a hacer

### Cambiar un texto de un proyecto

En su `.json`, dentro de `descripcion`. El texto (`texto`) es una **lista de
párrafos**, cada uno entre comillas y separados por comas:

```json
"descripcion": {
  "titulo": "TUTTI PARI",
  "link": "https://www.instagram.com/tuttiispace/",
  "texto": [
    "Primer párrafo.",
    "Segundo párrafo, con **negrita**, *cursiva* y un [link](https://www.instagram.com/usuario/)."
  ]
}
```

Negrita, cursiva y links se escriben así: `**negrita**`, `*cursiva*` y
`[texto del link](https://…)`. Es lo que escriben los botones del
formateador.

### Cambiar el orden de las fotos, o quitar una

En `imatges`, el orden es el de la página. Para cambiar el orden, mueve las
líneas; para quitar una, bórrala de la lista (la foto puede quedarse en `img/`,
no pasa nada):

```json
"primera_imatge": { "src": "./img/1.webp" },
"imatges": [
  "./img/2.webp",
  "./img/3.webp",
  "./img/5.webp"
]
```

`primera_imatge` es la portada: la foto grande de arriba y la que sale cuando
alguien comparte el enlace por WhatsApp o Instagram.

### Añadir fotos a un proyecto

1. Pásalas por imgToWeb. **Ojo**: imgToWeb las numera desde el 1. Si el
   proyecto ya tiene 16 fotos, cámbiales el nombre a 17, 18… antes de subirlas.
2. Arrástralas a su carpeta `img/`.
3. Añádelas a `imatges` en su `.json`: `"./img/17.webp"`, `"./img/18.webp"`…

### Cambiar el nombre en la home, la categoría o el orden; esconder un proyecto

En `data/home.json`, en `projectes_visibles`. Cada proyecto es un bloque:

```json
{
  "slug": "tuttiPari",
  "name": "tutti pari",
  "category": "eventos",
  "visible": true
},
```

- `name`: el nombre del enlace en la home.
- `category`: la categoría de los filtros. Para una **nueva**, basta con
  escribirla: sale sola en los filtros.
- Para **esconder** un proyecto sin borrarlo: `"visible": false`. Para que
  vuelva, `true`.
- El **orden** de la lista es el de la web sin JavaScript y el del mapa del
  sitio para Google; en la home los nombres se reparten al azar.

### Cambiar las fotos de la home

Son las carpetas `_portada/1/`, `_portada/2/` y `_portada/3/` (los botones
1 2 3 de la home). Para cambiar una foto por otra, sustituye el `.webp` por
otro **con el mismo nombre** (`1_1.webp`, `1_2.webp`…).

Cada foto está en `data/home.json`, en `gallerySets`, con su archivo (`src`),
el proyecto al que lleva (`url`, su *slug*) y dónde se coloca en ordenador
(`desktopStyle`) y en móvil (`mobileStyle`): `top`, `left`, `right`, `bottom`
en % de la pantalla, `scale` el tamaño e `index` cuál va encima.

### Cambiar tu bio, tu email o tu Instagram

El texto que sale al pulsar "andrea carilla" está dentro del código: escríbenos
y lo cambiamos.

---

## 4. Añadir un proyecto nuevo

1. **Las fotos**: pásalas por imgToWeb en el orden en que quieras que salgan
   y descarga el zip.
2. **La carpeta**: en VS Code, clic derecho en `data/` → **New Folder** → el
   nombre (por ejemplo `nuevoProyecto`). Dentro, otra carpeta `img`, y arrastra
   ahí las fotos del zip.
3. **Los textos**: abre `formateador.html` en Chrome (doble clic en el archivo,
   desde la carpeta de la web), rellénalo y pulsa **descargar .json**. Mueve el
   archivo a `data/nuevoProyecto/`; se tiene que llamar
   `nuevoProyecto.json`, igual que la carpeta. (O copia el `.json` de otro
   proyecto, cámbiale el nombre y los textos.)
4. **Que salga**: en `data/home.json`, copia un bloque de `projectes_visibles`
   (desde `{` hasta `},`), pégalo donde quieras que salga y cambia `slug`,
   `name` y `category`.
5. Sube el cambio (punto 2, pasos 3 y 4). La web le hace su página y su enlace
   en la home sola.

Un proyecto:

```json
{
  "slug": "nuevoProyecto",
  "titulo": "nuevo proyecto",
  "primera_imatge": { "src": "./img/1.webp" },
  "descripcion": {
    "titulo": "NUEVO PROYECTO",
    "link": "https://www.instagram.com/usuario/",
    "texto": [
      "Primer párrafo.",
      "Segundo párrafo."
    ]
  },
  "tipo_proyecto": "eventos",
  "ubicacion": "Barcelona",
  "fecha": "Octubre 2026",
  "creditos": [
    { "nombre": "Andrea Carilla", "rol": "FOTOGRAFÍA", "link": "" },
    { "nombre": "Nombre Apellido", "rol": "MODELO", "link": "https://www.instagram.com/usuario/" }
  ],
  "imatges": [
    "./img/2.webp",
    "./img/3.webp"
  ]
}
```

---

## 5. Qué va en cada campo de un proyecto

| campo | qué es | ejemplo |
|---|---|---|
| `slug` | el nombre de la carpeta (no se cambia) | `"tuttiPari"` |
| `titulo` | el nombre en la pestaña del navegador y al compartir | `"tutti pari"` |
| `primera_imatge` | la portada | `{ "src": "./img/1.webp" }` |
| `descripcion.titulo` | el título grande de la página | `"TUTTI PARI"` |
| `descripcion.link` | *(opcional)* adónde lleva el título al pulsarlo | `"https://…"` |
| `descripcion.texto` | *(opcional)* el texto, lista de párrafos | `["Uno.", "Dos."]` |
| `tipo_proyecto` | la categoría que sale en la página (la de los filtros va en `home.json`) | `"eventos"` |
| `ubicacion` | *(opcional)* el lugar; admite links | `"[Hangar](https://…) Barcelona"` |
| `fecha` | *(opcional)* la fecha, como quieras escribirla | `"Marzo 2026"` |
| `creditos` | quién hizo qué: `nombre`, `rol` y `link` (vacío si no hay) | ver arriba |
| `imatges` | las fotos de la página, en orden | `["./img/2.webp"]` |

---

## 6. Ver los cambios antes de subirlos *(opcional)*

Con la extensión **Live Server** de VS Code (búscala en Extensions, el icono de
los cuadraditos, e instálala): abajo a la derecha pulsa **Go Live** y se abre
la web en el navegador, leyendo tus archivos. Cada vez que guardas, se
actualiza. Los proyectos nuevos se abren igual, aunque aún no tengan página.

---

## 7. Si algo va mal

**Casi siempre es una coma o unas comillas.** En un `.json`:

- cada texto va entre comillas dobles: `"así"`;
- entre dos cosas de una lista va una coma: `["./img/1.webp", "./img/2.webp"]`;
- **después de la última, no**: `["./img/1.webp", "./img/2.webp",]` ✗.

**Cómo saber si ha ido bien**: en tu repositorio en github.com, pestaña
**Actions**. Lo último que has subido sale con un círculo:

- 🟢 verde: publicado.
- 🟡 amarillo: publicándose (2-3 minutos).
- 🔴 rojo: algo no cuadra. Entra en **generar paginas de proyecto** →
  **generar** → **Generar** y verás una línea que dice qué archivo es. Por
  ejemplo:

  ```
  [build] tuttiPari.json no se puede leer (¿falta una coma?): … (line 12 column 5)
  ```

  Si es el `.json` de un proyecto, su página se queda como estaba. Si es
  `data/home.json`, las fotos de la home pueden desaparecer hasta que lo
  arregles. Arréglalo (el número de línea te dice dónde mirar), sube otra vez,
  y listo.

Si no ves qué es, escríbeme con el mensaje en rojo y lo miramos.
