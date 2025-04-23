
<html lang="es">
<head>
  <meta charset="UTF-8">

  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      background: #000;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    video {
      width: 90%;
      max-width: 960px;
      border: 2px solid white;
      border-radius: 12px;
      background-color: #000;
    }
  </style>
</head>
<body>
  <video id="video" controls autoplay></video>

  <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
  <script>
    const video = document.getElementById('video');
    const videoSrc = "https://shlsakamai3.akamaized.net/hlsorigin/tvg_hd_fm_2200/chunklist.m3u8?stream=philadelphia_mbr&cust=TVG&user=&t=1745420992&h=60c0c1772084cc2dd40168517a261cbc&type=live";

    if (Hls.isSupported()) {
      const hls = new Hls();
      hls.loadSource(videoSrc);
      hls.attachMedia(video);
      hls.on(Hls.Events.MANIFEST_PARSED, () => {
        video.play();
      });
    } else if (video.canPlayType('application/vnd.apple.mpegurl')) {
      // Para Safari
      video.src = videoSrc;
      video.addEventListener('loadedmetadata', () => {
        video.play();
      });
    } else {
      alert('Tu navegador no soporta reproducción de video en este formato.');
    }
  </script>
</body>
</html>
