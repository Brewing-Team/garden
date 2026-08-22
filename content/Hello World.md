Hola que tal!

<div id="kepos-container" style="text-align: center; margin: 2rem 0;">
  <!-- El estilo usa una fuente monoespaciada para que el ASCII no se deforme -->
  <pre id="kepos-ascii" style="font-family: 'Courier New', Courier, monospace; font-size: 16px; font-weight: bold; color: #4ade80; background: transparent; border: none; overflow: hidden; line-height: 1.2;">
  </pre>
</div>

<script>
// Array con los "fotogramas" de la animación
const keposFrames = [
`



  
░░░░░░░░░░░░░░░░░░░░░░░░░░░░░`,
`



      |           |
░░░░░░░░░░░░░░░░░░░░░░░░░░░░░`,
`


     \\|/         \\|/
      |           |
░░░░░░░░░░░░░░░░░░░░░░░░░░░░░`,
`

     _|_         _|_
     \\|/   _|_   \\|/
      |    \\|/    |
░░░░░░░░░░░░|░░░░░░░░░░░░░░░░`,
`
      ✿           ✿
     _|_    ✿    _|_
     \\|/   _|_   \\|/
      |    \\|/    |
░░░░░░░░░░░░|░░░░░░░░░░░░░░░░
       Bienvenido al Kêpos`
];

let frame = 0;

function growGarden() {
  const display = document.getElementById('kepos-ascii');
  if (!display) return; // Seguridad en caso de que el elemento no cargue
  
  // Actualizar el texto con el frame actual
  display.textContent = keposFrames[frame];
  frame++;
  
  // Si no hemos llegado al final, programamos el siguiente frame
  if (frame < keposFrames.length) {
    setTimeout(growGarden, 600); // 600 milisegundos entre cada fase
  }
}

// Iniciar la animación
// setTimeout le da un pequeño respiro de medio segundo al abrir la página antes de crecer
setTimeout(growGarden, 500);
</script>







<div style="text-align: center; margin: 2rem 0;">
  <!-- El canvas es de 128x128 píxeles reales, pero lo mostramos a 300px para que los píxeles se vean grandes y cuadrados -->
  <canvas id="micelio-pixel-art" width="128" height="128" style="width: 300px; height: 300px; background-color: #111; border-radius: 8px; image-rendering: pixelated; box-shadow: 0 4px 6px rgba(0,0,0,0.3); cursor: pointer;" onclick="iniciarMicelio()" title="Haz clic para cultivar otro micelio"></canvas>
  <div style="color: #a855f7; font-family: monospace; font-size: 1.2rem; margin-top: 1rem; font-weight: bold; letter-spacing: 2px;">MICELIO</div>
</div>

<script>
let animacionMicelio;
let nodos = [];
let conexiones = [];

function iniciarMicelio() {
  const canvas = document.getElementById('micelio-pixel-art');
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  
  // Limpiar animaciones previas si se hace clic otra vez
  if (animacionMicelio) clearTimeout(animacionMicelio);
  
  // Limpiar el lienzo
  ctx.fillStyle = '#111';
  ctx.fillRect(0, 0, 128, 128);
  
  // Nodo inicial en el centro
  nodos = [{x: 64, y: 64, activo: true}];
  conexiones = [];
  
  crecerMicelioProcedural(ctx);
}

function crecerMicelioProcedural(ctx) {
  let nuevosNodos = [];
  
  // Lógica de crecimiento orgánico
  nodos.filter(n => n.activo).forEach(n => {
      // Posibilidad de que una rama deje de crecer
      if (Math.random() < 0.08) n.activo = false; 
      if (!n.activo) return;
      
      // Posibilidad de ramificarse
      if (Math.random() < 0.35) {
          let angulo = Math.random() * Math.PI * 2;
          let distancia = 4 + Math.random() * 8; // Saltos de 4 a 12 píxeles
          let nx = n.x + Math.cos(angulo) * distancia;
          let ny = n.y + Math.sin(angulo) * distancia;
          
          // Mantener el crecimiento dentro de los bordes del canvas
          if (nx > 10 && nx < 118 && ny > 10 && ny < 118) {
              let nuevoNodo = {x: nx, y: ny, activo: true};
              nuevosNodos.push(nuevoNodo);
              conexiones.push({a: n, b: nuevoNodo});
              
              // **El secreto de las redes**: buscar nodos cercanos y fusionarse
              nodos.forEach(otro => {
                 if (otro !== n) {
                     let d = Math.hypot(otro.x - nx, otro.y - ny);
                     // Si hay otro nodo cerca, crear una conexión de red
                     if (d < 15 && Math.random() < 0.6) {
                         conexiones.push({a: nuevoNodo, b: otro});
                     }
                 }
              });
          }
      }
  });
  
  nodos = nodos.concat(nuevosNodos);
  dibujarRed(ctx);
  
  // Continuar la animación si aún hay nodos activos
  if (nodos.filter(n => n.activo).length > 0) {
      animacionMicelio = setTimeout(() => crecerMicelioProcedural(ctx), 100);
  }
}

function dibujarRed(ctx) {
  // Redibujar el fondo oscuro suavemente
  ctx.fillStyle = '#111';
  ctx.fillRect(0, 0, 128, 128);
  
  // Dibujar las conexiones (hifas)
  ctx.strokeStyle = '#9333ea'; // Morado oscuro
  ctx.lineWidth = 1;
  ctx.beginPath();
  conexiones.forEach(c => {
      ctx.moveTo(Math.round(c.a.x), Math.round(c.a.y));
      ctx.lineTo(Math.round(c.b.x), Math.round(c.b.y));
  });
  ctx.stroke();
  
  // Dibujar los nodos como cuadrados de 2x2 (estilo pixel art)
  ctx.fillStyle = '#d8b4fe'; // Morado claro/brillante
  nodos.forEach(n => {
      // Math.round asegura que los bloques encajen en una cuadrícula estricta de píxeles
      ctx.fillRect(Math.round(n.x) - 1, Math.round(n.y) - 1, 2, 2);
  });
}

// Iniciar al cargar la página
setTimeout(iniciarMicelio, 500);
</script>



<div style="text-align: center; margin: 2rem 0; cursor: pointer;" title="Click to replant">
  <!-- Small canvas, pixelated scaling -->
  <canvas id="enoki-dither-pixel" width="128" height="128" style="width: 300px; height: 300px; background-color: #111; border-radius: 8px; image-rendering: pixelated; box-shadow: 0 4px 6px rgba(0,0,0,0.3); border: 4px solid #444;" onclick="initEnokiDither()"></canvas>
  <div style="color: #fef3c7; font-family: monospace; font-size: 1.2rem; margin-top: 1rem; font-weight: bold; letter-spacing: 2px;">DITHERED ENOKI</div>
</div>

<style>
  #enoki-dither-pixel {
    cursor: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAAPklEQVQYV2NkQAL/GEgA5B8D+f8ZGJ4wMDxhYAj4z8Ag8A+IYWF4wMC4iYGB4REDAwMWAZBFv0H0PwhgxAAH+B8E+e8fGAAAAABJRU5ErkJggg=='), auto;
  }
</style>

<script>
let enokiDitherTimer;
let enokiCluster;
const palette = [
  '#000000', // 0 Black
  '#111111', // 1 Dark Gray
  '#444444', // 2 Med Gray
  '#fef3c7', // 3 Enoki Cream
  '#e2d2a4', // 4 Enoki Stem Shading
  '#fff8e1', // 5 Enoki Cap Light
  '#d1a361', // 6 Substrate Light
  '#8c6e3b', // 7 Substrate Shadow
  '#3d567c', // 8 Background Blue
  '#1d2d46', // 9 Deep Bkg Blue
  '#b1d8e1', // 10 Frosty Blue (Highlights)
  '#ffeb3b', // 11 Gold (Subtle Highlight)
];

function getDitherPattern(value, x, y) {
  // Ordered dithering pattern for classic pixel shading
  const dither8x8 = [
    [ 0, 48, 12, 60,  3, 51, 15, 63],
    [32, 16, 44, 28, 35, 19, 47, 31],
    [ 8, 56,  4, 52, 11, 59,  7, 55],
    [40, 24, 36, 20, 43, 27, 39, 23],
    [ 2, 50, 14, 62,  1, 49, 13, 61],
    [34, 18, 46, 30, 33, 17, 45, 29],
    [10, 58,  6, 54,  9, 57,  5, 53],
    [42, 26, 38, 22, 41, 25, 37, 21]
  ];
  const px = Math.floor(x % 8);
  const py = Math.floor(y % 8);
  return dither8x8[py][px] < (value * 64);
}

function initEnokiDither() {
  const canvas = document.getElementById('enoki-dither-pixel');
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  if (enokiDitherTimer) clearTimeout(enokiDitherTimer);
  
  // Clear background
  ctx.fillStyle = palette[8];
  ctx.fillRect(0, 0, 128, 128);
  
  // Define growth data
  enokiCluster = {
    baseY: 100,
    mushrooms: [],
    substrate: [],
    ditheredBackground: []
  };

  for(let i=0; i<12; i++) {
    enokiCluster.mushrooms.push({
      x: 32 + (i * 7) + (Math.random()*4),
      currentHeight: 1 + (Math.random()*5),
      targetHeight: 70 + (Math.random()*25),
      speed: 0.8 + (Math.random()*1.5),
      capSize: 3 + (Math.random()*2)
    });
  }

  // Generate dithered substrate and background texture once
  for (let y = 0; y < 128; y++) {
    for (let x = 0; x < 128; x++) {
      if (y > enokiCluster.baseY) {
        // Substrate dithering
        const brightness = (y - enokiCluster.baseY) / (128 - enokiCluster.baseY);
        if (getDitherPattern(brightness + (Math.random()*0.1), x, y)) {
           ctx.fillStyle = palette[7];
        } else {
           ctx.fillStyle = palette[6];
        }
        ctx.fillRect(x, y, 1, 1);
      } else {
        // Background dithering
        const depth = y / enokiCluster.baseY;
        if (!getDitherPattern(depth + (Math.random()*0.05), x, y)) {
          ctx.fillStyle = palette[9];
        } else {
          ctx.fillStyle = palette[8];
        }
        ctx.fillRect(x, y, 1, 1);
      }
    }
  }

  // Draw the initial state
  enokiCluster.mushrooms.forEach(m => drawEnokiMushroom(ctx, m));
  growEnokiDither(ctx);
}

function growEnokiDither(ctx) {
  let growing = false;
  enokiCluster.mushrooms.forEach(m => {
    if (m.currentHeight < m.targetHeight) {
      m.currentHeight += m.speed;
      growing = true;
    }
  });

  drawDitheredCluster(ctx);

  if (growing) {
    enokiDitherTimer = setTimeout(() => growEnokiDither(ctx), 100);
  }
}

function drawDitheredCluster(ctx) {
  // Redraw mushrooms on top of the static background
  enokiCluster.mushrooms.forEach(m => drawEnokiMushroom(ctx, m));
}

function drawEnokiMushroom(ctx, m) {
  const topY = enokiCluster.baseY - m.currentHeight;
  const stemWidth = 2;
  const shadowOffset = 1;

  // 1. Dithered Stem
  for (let y = enokiCluster.baseY; y > topY; y--) {
    const depth = (y - topY) / m.currentHeight;
    // Base color
    ctx.fillStyle = palette[3];
    ctx.fillRect(m.x, y, stemWidth, 1);
    
    // Shading dithering
    if(getDitherPattern(depth + 0.2, m.x + shadowOffset, y)) {
      ctx.fillStyle = palette[4];
      ctx.fillRect(m.x + shadowOffset, y, 1, 1);
    }
  }

  // 2. Dithered Cap
  if (m.currentHeight > 10) {
    drawDitheredPixelCap(ctx, m.x + (stemWidth / 2), topY, m.capSize);
  }
}

function drawDitheredPixelCap(ctx, centerX, centerY, size) {
  const roundedSize = Math.max(2, Math.round(size));
  ctx.fillStyle = palette[5];
  
  // Main Cap block
  ctx.fillRect(Math.round(centerX - roundedSize), Math.round(centerY - 1), Math.round(roundedSize * 2), 3);
  
  // Dithered cap rounded highlight
  for (let dx = -roundedSize; dx <= roundedSize; dx++) {
    for (let dy = -1; dy <= 1; dy++) {
       const x = Math.round(centerX + dx);
       const y = Math.round(centerY + dy);
       const brightness = 1 - (Math.abs(dx) / roundedSize);
       if(getDitherPattern(brightness + 0.3, x, y)) {
         ctx.fillStyle = palette[5];
       } else {
         ctx.fillStyle = palette[3];
       }
       ctx.fillRect(x, y, 1, 1);
    }
  }
}

// Start the dithered animation upon loading
setTimeout(initEnokiDither, 500);
</script>
