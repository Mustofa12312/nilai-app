<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Nilai Otomatis Elegan</title>
  <style>
    :root {
      --primary: #3a86ff;
      --background: #f9f9f9;
      --card: #ffffff;
      --shadow: rgba(0, 0, 0, 0.05);
    }

    body {
      margin: 0;
      padding: 0;
      background-color: var(--background);
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      padding-top: 40px;
    }

    .container {
      background-color: var(--card);
      padding: 30px;
      border-radius: 16px;
      width: 90%;
      max-width: 500px;
      box-shadow: 0 8px 20px var(--shadow);
    }

    h2 {
      text-align: center;
      margin-bottom: 30px;
      color: var(--primary);
    }

    .input-group {
      margin-bottom: 20px;
    }

    label {
      font-weight: 600;
      display: block;
      margin-bottom: 8px;
      color: #333;
    }

    input[type="number"] {
      width: 100%;
      padding: 12px;
      font-size: 16px;
      border: 1px solid #ddd;
      border-radius: 10px;
      box-sizing: border-box;
      transition: border-color 0.3s;
    }

    input[type="number"]:focus {
      border-color: var(--primary);
      outline: none;
    }

    #hasil {
      margin-top: 30px;
      padding: 15px;
      background-color: var(--primary);
      color: white;
      text-align: center;
      border-radius: 10px;
      font-size: 20px;
      font-weight: bold;
    }

    @media screen and (max-width: 600px) {
      .container {
        padding: 20px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Penilaian Ujian</h2>

    <div class="input-group">
      <label for="salah1">Salah Romawi I (10 soal × 3 poin)</label>
      <input type="number" id="salah1" min="0" max="10" />
    </div>

    <div class="input-group">
      <label for="salah2">Salah Romawi II (10 soal × 4 poin)</label>
      <input type="number" id="salah2" min="0" max="10" />
    </div>

    <div class="input-group">
      <label for="salah3">Salah Romawi III (5 soal × 6 poin)</label>
      <input type="number" id="salah3" min="0" max="5" />
    </div>

    <div id="hasil">Total Nilai: 0 / 100</div>
  </div>

  <script>
    const inputs = Array.from(document.querySelectorAll("input"));
    const hasil = document.getElementById("hasil");

    // Isi dari localStorage
    inputs.forEach(input => {
      input.value = localStorage.getItem(input.id) || '';
    });

    inputs.forEach((input, index) => {
      input.addEventListener("keydown", function(e) {
        const isNumberKey = e.key >= '0' && e.key <= '9';

        if (e.key === "ArrowDown") {
          e.preventDefault();
          const next = inputs[index + 1];
          if (next) next.focus();
        } else if (e.key === "ArrowUp") {
          e.preventDefault();
          const prev = inputs[index - 1];
          if (prev) prev.focus();
        } else if (isNumberKey) {
          e.preventDefault();
          input.value = e.key;
          hitungNilai();
        }
      });

      input.addEventListener("input", hitungNilai);
    });

    function hitungNilai() {
      const salah1 = parseInt(document.getElementById('salah1').value) || 0;
      const salah2 = parseInt(document.getElementById('salah2').value) || 0;
      const salah3 = parseInt(document.getElementById('salah3').value) || 0;

      localStorage.setItem('salah1', salah1);
      localStorage.setItem('salah2', salah2);
      localStorage.setItem('salah3', salah3);

      const benar1 = 10 - salah1;
      const benar2 = 10 - salah2;
      const benar3 = 5 - salah3;

      const nilai = (benar1 * 3) + (benar2 * 4) + (benar3 * 6);
      hasil.innerText = `Total Nilai: ${nilai} / 100`;
    }

    hitungNilai();
  </script>
</body>
</html>
