<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/shaka-player/4.7.6/shaka-player.compiled.min.js"></script>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      background: black;
      height: 100%;
      width: 100%;
      overflow: hidden;
    }

    video {
      width: 100vw;
      height: 100vh;
      object-fit: cover;
      background: black;
    }
  </style>
</head>
<body>
  <video id="video" autoplay muted playsinline controls></video>

  <script>
    async function initPlayer() {
      const video = document.getElementById('video');
      const player = new shaka.Player(video);

      shaka.polyfill.installAll();

      if (!shaka.Player.isBrowserSupported()) {
        alert('Tu navegador no soporta Shaka Player');
        return;
      }

      const clearkeys = {
        '6cf9a13d6fd65a0f2e1cee3969aab9f5': 'ea61c3c1adee71b5c2e9744e41d4b75f'
      };

      player.configure({
        drm: {
          clearKeys: clearkeys
        }
      });

      try {
        await player.load('https://chromecast.cvattv.com.ar/live/c6eds/Universal_Channel_HD/SA_Live_dash_enc_C/Universal_Channel_HD.mpd');
        console.log('¡Stream cargado!');
      } catch (e) {
        console.error('Error al cargar el stream:', e);
      }
    }

    document.addEventListener('DOMContentLoaded', initPlayer);
  </script>
</body>
</html>
