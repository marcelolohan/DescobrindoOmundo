<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Contagem Regressiva do Bebê</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #fffaf0;
      text-align: center;
      padding: 50px;
    }

    .title {
      font-size: 2em;
      color: #ff69b4;
      margin-bottom: 30px;
    }

    img {
      max-width: 300px;
      margin: 30px auto;
      display: block;
    }

    #countdown {
      font-size: 1.5em;
      color: #333;
      margin-top: 30px;
    }

    audio {
      margin-top: 40px;
    }
  </style>
</head>
<body>

  <div class="title">Um novo amor está a caminho...</div>

  <img src="https://via.placeholder.com/300x200.png?text=Bebê+a+Caminho" alt="Imagem do Bebê" />

  <div id="countdown"></div>

  <audio controls autoplay loop>
    <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mp3">
    Seu navegador não suporta áudio.
  </audio>

  <script>
    // 259 dias a partir de hoje
    const birthDate = new Date();
    birthDate.setDate(birthDate.getDate() + 259);

    function updateCountdown() {
      const now = new Date();
      const distance = birthDate - now;

      const days = Math.floor(distance / (1000 * 60 * 60 * 24));
      const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
      const seconds = Math.floor((distance % (1000 * 60)) / 1000);

      document.getElementById("countdown").innerHTML =
        `Faltam ${days} dias, ${hours} horas, ${minutes} minutos e ${seconds} segundos para a chegada!`;

      if (distance < 0) {
        document.getElementById("countdown").innerHTML = "O bebê chegou! 🎉";
      }
    }

    setInterval(updateCountdown, 1000);
    updateCountdown();
  </script>

</body>
</html>
