!DOCTYPE html>
<html>
<head>
  <title>Sonido de Finanzas</title>
</head>
<body>
  <h2>Monitor de Finanzas 💸</h2>
  <p>Escuchando cambios en la hoja de cálculo...</p>
  <audio id="monedaAudio" src="https://www.soundjay.com/misc/sounds/coins-dropped-1.mp3" preload="auto"></audio>

  <script>
    const sheetUrl = 'https://spreadsheets.google.com/feeds/cells/1bbq2yAM14_vMXJsf6I277CSD_o8MlakuswxpGfdhxiI/1/public/full?alt=json';
    let lastData = '';

    async function checkForChange() {
      try {
        const response = await fetch(sheetUrl);
        const data = await response.json();
        const text = data.feed.entry.map(cell => cell.content.$t).join(',');

        if (lastData && lastData !== text) {
          console.log('Cambio detectado. Reproduciendo sonido...');
          document.getElementById('monedaAudio').play();
        }

        lastData = text;
      } catch (error) {
        console.error('Error al obtener datos:', error);
      }
    }

    setInterval(checkForChange, 5000); // Checa cada 5 segundos
  </script>
</body>
</html>
