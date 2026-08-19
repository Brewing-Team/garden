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
