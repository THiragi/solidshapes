<script lang="ts">
  let sides = $state(3); 
  let width = 500;
  let height = 500;

  let canvas: HTMLCanvasElement | null = null;

  $effect(() => {
    canvas = document.getElementById('polygon') as HTMLCanvasElement | null;
    drawPolygon();
  });


  function drawPolygon() {
    if (!canvas) return;

    const context: CanvasRenderingContext2D | null = canvas.getContext('2d');

    if (!context) return;

    context.clearRect(0, 0, canvas.width, canvas.height);

    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    const radius = 100;
    const angle = (Math.PI * 2) / sides;

    context.beginPath();
    context.moveTo(centerX + radius * Math.cos(0), centerY + radius * Math.sin(0));

    for (let i = 1;  i <= sides; i++) {
      context.lineTo(centerX + radius * Math.cos(i * angle), centerY + radius * Math.sin(i * angle));
    }

    context.closePath();
    context.stroke();
  }  
</script>

<label>
  Number of sides: 
  <input type="range" bind:value={sides} min="3" max="12" onchange={drawPolygon}>
  {sides}
</label>
<div>
  <canvas id="polygon" {width} {height}>
  </canvas>
</div>

<style>
</style>