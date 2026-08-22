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
