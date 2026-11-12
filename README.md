# Bolo Bros

**▶ Jugar ahora: https://bolobros.netlify.app/**

Plataformero web de estilo clásico con personaje, niveles, gráficos y música originales. Se juega en el navegador, en computadora o celular, sin instalar nada.

Bolo es un bichito turquesa con bufanda roja y una **B** en el pecho. Corre, salta, nada, junta monedas, baja por tuberías secretas y se enfrenta a tres jefes para salvar el reino.

## Cómo se juega

| Acción | Teclado | Celular |
|---|---|---|
| Moverse | ← → o A / D | ◀ ▶ |
| Saltar / nadar (brazada) | Espacio, ↑, W o Z | A |
| Correr | Shift o X | B |
| Entrar a una tubería | ↓ o S | ▼ |
| Pausa | P | — |
| Empezar / confirmar | Enter | Tocar la pantalla |

En el mapa de mundos se elige nivel con ← → y Enter, o tocando el nivel.

## Contenido

**16 niveles: 12 normales y 4 mundos secretos.**

| Mundo | Niveles | Ambiente | Enemigos | Jefe |
|---|---|---|---|---|
| 1 · Pradera | 1‑1, 1‑2, 1‑3 | Día, atardecer, noche | Slimes, bebés dragón que lanzan bolas de fuego | Dragón Mayor |
| 2 · Desierto | 2‑1, 2‑2, 2‑3 | Día, atardecer, noche | Escorpiones, cactus andantes, buitres | Rey Escorpión |
| 3 · Océano | 3‑1, 3‑2, 3‑3 | Bajo el agua, corrientes, profundidades | Peces, medusas, erizos, tiburones | Pulpo Gigante |
| 4 · Nieve | 4‑1, 4‑2, 4‑3 | Día, atardecer, noche; el hielo resbala | Pingüinos, erizos de hielo, búhos, muñecos de nieve que lanzan bolas | Yeti de las Nieves |
| Secretos | 0‑1, 0‑2, 0‑3, 0‑4 | Sin enemigos, monedas dobles, vidas extra | — | — |

### Objetos

- **Monedas:** 100 monedas dan una vida.
- **Baya roja:** Bolo crece, rompe ladrillos y aguanta un golpe.
- **Estrella:** 14 segundos de invencibilidad, con música propia.
- **Baya verde 1UP:** una vida extra (solo en los mundos secretos).

### Medallas, combos y puntos de control

- **Medallas:** cada nivel normal tiene 3 (36 en total): terminar el nivel, juntar las 3 monedas grandes con la letra B y encontrar los 3 cuartos secretos. Se ven como estrellas en el mapa.
- **Combos:** pisar enemigos seguidos sin tocar el suelo duplica los puntos cada vez (100, 200, 400…) con un sonido que sube de tono; el sexto da una vida.
- **Punto de control:** una bandera a mitad de nivel; si pierdes una vida reapareces ahí.
- **Compartir:** al terminar la partida aparecen botones para copiar el resultado o enviarlo por WhatsApp.

### Enemigos con reglas especiales

- **Cactus, medusas y erizos** tienen espinas: no se pueden pisar, solo se vencen con la estrella.
- **Tiburón:** no se puede vencer pisándolo. Gruñe, embiste en línea recta y se pasa de largo; al tocarle la cola se encoge, se pone gris y se va dormido.
- **Jefes:** se vencen con 3 pisotones y se vuelven más agresivos con cada golpe.

### Secretos

- **Tuberías secretas:** en cada nivel normal, 3 tuberías elegidas al azar en cada partida tienen un brillo intermitente. Con ↓ llevan a cuartos donde las monedas forman frases misteriosas.
- **Cofre del tesoro:** aparece en el tercer cuarto secreto de un nivel y da +5 vidas.
- **Warp zones:** hay rutas ocultas con un bloque invisible o una cámara escondida cerca del final de los niveles 1‑3, 2‑2, 3‑2 y 4‑2. Llevan a los mundos secretos 0‑1, 0‑2, 0‑3 y 0‑4.
- **Código secreto:** escribir `BOLO` en la portada o en el mapa (o tocar 5 veces el título "MAPA DE MUNDOS" en el celular) desbloquea todos los niveles.

El avance (niveles desbloqueados y secretos encontrados) se guarda en el navegador con `localStorage`.

## En qué lenguaje está hecho

Todo el juego vive en **un solo archivo, `index.html`** (unas 1,200 líneas, 80 KB), sin motor de juegos, sin bibliotecas y sin paso de compilación.

| Parte | Tecnología |
|---|---|
| Lógica del juego | **JavaScript** puro (ES6+) |
| Gráficos | **Canvas 2D** de HTML5: todo se dibuja con código (formas vectoriales), no hay imágenes |
| Música y sonidos | **Web Audio API**: osciladores y ruido generados en tiempo real, no hay archivos de audio |
| Estructura y estilos | **HTML5** y **CSS** |
| Guardado | `localStorage` del navegador |
| Tipografía | "Press Start 2P" de Google Fonts (lo único que se carga de internet; si falla, usa una fuente monoespaciada) |

### Cómo está organizado el código

- **Entrada:** teclado y botones táctiles.
- **Audio:** efectos (`sfx`) y un secuenciador de pistas (`TRACKS`) con un tema por mundo, jefe, estrella, cuartos secretos y victoria.
- **Niveles:** `buildLevel()` arma cada nivel sobre una cuadrícula de 200 × 15 bloques de 32 px; `ENEMIES` define los enemigos de cada nivel.
- **Física:** colisiones por cuadrícula (`collideX`, `collideY`) y nado en los niveles de agua.
- **Bucle principal:** `step()` actualiza la lógica a 60 pasos por segundo fijos y `draw()` dibuja con `requestAnimationFrame`.

## Cómo implementarlo en la web

Es un sitio estático: basta con servir `index.html`. No necesita servidor de aplicaciones, base de datos ni instalar dependencias.

### Probarlo en tu computadora

Abre `index.html` con doble clic, o sirve la carpeta:

```bash
git clone https://github.com/vixbee/bolobros.git
cd bolobros
python3 -m http.server 8000
# abre http://localhost:8000
```

### Netlify (como está publicado este proyecto)

1. En [app.netlify.com](https://app.netlify.com): **Add new site → Import an existing project → GitHub** y elige este repositorio.
2. Configuración: rama `main`, **Build command** vacío, **Publish directory** vacío o `.`.
3. Cada `git push` a `main` publica la nueva versión automáticamente.

### GitHub Pages

1. En el repositorio: **Settings → Pages**.
2. En *Source* elige **Deploy from a branch**, rama `main`, carpeta `/ (root)`.
3. El juego queda en `https://vixbee.github.io/bolobros/`.

### Otras opciones

- **Cloudflare Pages o Vercel:** importar el repositorio sin comando de build.
- **itch.io:** crear un proyecto tipo *HTML*, subir `index.html` en un .zip y marcar "This file will be played in the browser".
- **Hosting propio (Apache, Nginx, IIS):** copiar `index.html` a la carpeta pública.

### Requisitos

- Un navegador moderno (Chrome, Edge, Firefox o Safari recientes).
- El sonido empieza después de la primera tecla o toque, porque los navegadores bloquean el audio automático.

## Créditos

Diseño y dirección: Vix. Programación, gráficos y música generados con Claude (Anthropic). Los personajes, niveles y melodías son originales de este proyecto.
