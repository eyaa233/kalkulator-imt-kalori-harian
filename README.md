KALKULATOR IMT DAN KALORI HARIAN
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title></title>
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Montserrat:wght@600;700&display=swap">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body {
      font-family: 'Montserrat', Arial, sans-serif;
      background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);
      min-height: 100vh;
      margin: 0;
      padding: 0;
    }
    .container {
      max-width: 420px;
      margin: 40px auto;
      background: #fff;
      border-radius: 24px;
      box-shadow: 0 4px 24px rgba(0,0,0,.14);
      padding: 32px 26px 16px 26px;
      text-align: center;
      opacity: 0;
      animation: fadeIn 1.2s forwards;
    }
    @keyframes fadeIn {
      to { opacity: 1;}
    }
    .section-title {
      font-weight: 700;
      font-size: 1.7em;
      margin-bottom: 18px;
      letter-spacing: 1px;
      color: #3a3a3a;
    }
    .form-group { margin-bottom: 17px; text-align: left;}
    label { font-size: 1em; margin-bottom: 4px; display: block; color: #555;}
    input, select {
      width: 100%;
      padding: 8px 12px;
      border-radius: 8px;
      border: 1px solid #e4e4e4;
      font-size: 1em;
      outline: none;
      transition: border-color .2s;
    }
    input:focus, select:focus { border-color: #91c8e4;}
    button {
      padding: 12px 32px;
      background: linear-gradient(90deg, #a8edea 0%, #fed6e3 100%);
      color: #222;
      font-weight: bold;
      border: none;
      border-radius: 10px;
      font-size: 1.06em;
      cursor: pointer;
      transition: box-shadow .2s;
      margin-top: 8px;
      box-shadow: 0 2px 8px rgba(168,237,234,0.12);
    }
    button:hover { box-shadow: 0 4px 14px rgba(255,105,180,0.16);}
    .result {
      margin-top: 20px;
      padding: 18px 14px;
      border-radius: 12px;
      font-size: 1.13em;
      font-weight: 600;
      box-shadow: 0 2px 12px rgba(0,0,0,.09);
      opacity: 0;
      animation: popResult .7s forwards;
      transition: background .6s;
    }
    @keyframes popResult {
      0% { transform: scale(0.8); opacity: 0;}
      70% { transform: scale(1.08);}
      100% { transform: scale(1); opacity: 1;}
    }
    .imt-kurus { background: #e3f7ff; color: #0077b6;}
    .imt-normal { background: #e9ffe3; color: #43a047;}
    .imt-gemuk { background: #fffbe3; color: #fbc02d;}
    .imt-obesitas { background: #ffeaea; color: #f44336;}
    .imt-icon { font-size: 2.2em; margin-bottom: 9px;}
    .motivasi { margin-top: 10px; font-size: 0.96em; font-weight: 500;}
    .kalori-icon { font-size: 2em; margin-bottom: 7px; color: #ffb300;}
    .divider { height: 2px; background: linear-gradient(90deg,#a8edea,#fed6e3); border-radius: 2px; margin: 32px 0 20px 0;}
    @media(max-width:500px){
      .container{max-width:97vw; padding:20px;}
      .section-title{font-size:1.13em;}
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="section-title"><i class="fa-solid fa-heart-pulse" style="color:#e0647a"></i> Kalkulator IMT</div>
    <form id="bmiForm">
      <div class="form-group">
        <label for="height">Tinggi badan (cm):</label>
        <input type="number" id="height" min="50" max="250" required>
      </div>
      <div class="form-group">
        <label for="weight">Berat badan (kg):</label>
        <input type="number" id="weight" min="20" max="250" required>
      </div>
      <button type="button" onclick="hitungBMI()">Cek IMT Saya</button>
      <div class="result" id="bmiResult" style="display:none"></div>
    </form>
    <div class="divider"></div>

    <div class="section-title"><i class="fa-solid fa-fire-flame-curved kalori-icon"></i>Kalkulator Kalori Harian</div>
    <form id="calorieForm">
      <div class="form-group">
        <label for="gender">Jenis kelamin:</label>
        <select id="gender">
          <option value="male">Pria</option>
          <option value="female">Wanita</option>
        </select>
      </div>
      <div class="form-group">
        <label for="age">Umur (tahun):</label>
        <input type="number" id="age" min="10" max="100" required>
      </div>
      <div class="form-group">
        <label for="calHeight">Tinggi badan (cm):</label>
        <input type="number" id="calHeight" min="50" max="250" required>
      </div>
      <div class="form-group">
        <label for="calWeight">Berat badan (kg):</label>
        <input type="number" id="calWeight" min="20" max="250" required>
      </div>
      <div class="form-group">
        <label for="activity">Aktivitas fisik:</label>
        <select id="activity">
          <option value="1.2">Tidak aktif (jarang olahraga)</option>
          <option value="1.375">Sedikit aktif (olahraga ringan 1-3x/minggu)</option>
          <option value="1.55">Cukup aktif (olahraga sedang 3-5x/minggu)</option>
          <option value="1.725">Sangat aktif (olahraga berat 6-7x/minggu)</option>
          <option value="1.9">Ekstra aktif (kerja fisik/latihan berat)</option>
        </select>
      </div>
      <button type="button" onclick="hitungKalori()">Cek Kalori Harian</button>
      <div class="result" id="calorieResult" style="display:none"></div>
    </form>
  </div>
  <script>
    // Motivasi sesuai kategori IMT
    const motivasiIMT = {
      kurus: "Yuk, jaga pola makan & olahraga agar berat badan ideal!",
      normal: "Selamat! Berat badanmu ideal. Pertahankan pola hidup sehat.",
      gemuk: "Mulai atur pola makan & tingkatkan aktivitas fisik.",
      obesitas: "Tetap semangat! Konsultasi ke ahli gizi & rutin olahraga ya."
    };

    function hitungBMI() {
      const tinggi = parseFloat(document.getElementById('height').value) / 100;
      const berat = parseFloat(document.getElementById('weight').value);
      const resultDiv = document.getElementById('bmiResult');
      if (tinggi > 0 && berat > 0) {
        const bmi = berat / (tinggi * tinggi);
        let kategori = '', kelas = '', icon = '', motivasi = '';
        if (bmi < 18.5) {
          kategori = 'Kurus'; kelas = 'imt-kurus'; icon = '<i class="fa-solid fa-leaf imt-icon"></i>'; motivasi = motivasiIMT.kurus;
        }
        else if (bmi < 25) {
          kategori = 'Normal'; kelas = 'imt-normal'; icon = '<i class="fa-solid fa-circle-check imt-icon"></i>'; motivasi = motivasiIMT.normal;
        }
        else if (bmi < 30) {
          kategori = 'Gemuk'; kelas = 'imt-gemuk'; icon = '<i class="fa-solid fa-burger imt-icon"></i>'; motivasi = motivasiIMT.gemuk;
        }
        else {
          kategori = 'Obesitas'; kelas = 'imt-obesitas'; icon = '<i class="fa-solid fa-triangle-exclamation imt-icon"></i>'; motivasi = motivasiIMT.obesitas;
        }
        resultDiv.className = `result ${kelas}`;
        resultDiv.style.display = 'block';
        resultDiv.innerHTML = `${icon}IMT Anda: <span style="font-size:1.15em">${bmi.toFixed(2)}</span><br>
        <span style="font-weight:700">${kategori}</span>
        <div class="motivasi">${motivasi}</div>`;
      } else {
        resultDiv.className = "result imt-kurus";
        resultDiv.style.display = 'block';
        resultDiv.innerHTML = 'Masukkan nilai yang valid!';
      }
    }

    function hitungKalori() {
      const gender = document.getElementById('gender').value;
      const umur = parseInt(document.getElementById('age').value);
      const tinggi = parseFloat(document.getElementById('calHeight').value);
      const berat = parseFloat(document.getElementById('calWeight').value);
      const aktivitas = parseFloat(document.getElementById('activity').value);
      const resultDiv = document.getElementById('calorieResult');

      if (umur > 0 && tinggi > 0 && berat > 0) {
        let bmr;
        if (gender === 'male') {
          bmr = 88.362 + (13.397 * berat) + (4.799 * tinggi) - (5.677 * umur);
        } else {
          bmr = 447.593 + (9.247 * berat) + (3.098 * tinggi) - (4.330 * umur);
        }
        const kaloriTotal = bmr * aktivitas;
        let tips = "";
        if (kaloriTotal < 1800) tips = "Pastikan cukup nutrisi agar tetap bertenaga!";
        else if (kaloriTotal < 2500) tips = "Jaga pola makan & aktivitas fisik seimbang.";
        else tips = "Kamu butuh energi ekstra! Cocok untuk gaya hidup aktif.";

        resultDiv.className = "result imt-normal";
        resultDiv.style.display = 'block';
        resultDiv.innerHTML = `<i class="fa-solid fa-fire-flame-curved kalori-icon"></i>
        Kebutuhan kalori harian Anda: <span style="font-size:1.22em">${Math.round(kaloriTotal)} kkal</span>
        <div class="motivasi">${tips}</div>`;
      } else {
        resultDiv.className = "result imt-kurus";
        resultDiv.style.display = 'block';
        resultDiv.innerHTML = 'Masukkan data yang valid!';
      }
    }
  </script>
</body>
</html>
