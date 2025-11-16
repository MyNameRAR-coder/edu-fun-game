<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Edu-Fun — 100+ Soal</title>
<style>
body {
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: linear-gradient(135deg, #0f1724 0%, #1e293b 100%);
  color: #e6eef8;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  flex-direction: column;
  overflow: hidden;
}

h1, h2 {
  margin: 5px;
  text-align: center;
}

h1 {
  font-size: 2.5rem;
  margin-bottom: 20px;
  background: linear-gradient(90deg, #4f46e5, #7c3aed);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 0 2px 10px rgba(79, 70, 229, 0.3);
}

.btn {
  padding: 12px 24px;
  margin: 8px;
  background: #4f46e5;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.btn:hover {
  background: #4338ca;
  transform: translateY(-2px);
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
}

.card {
  background: rgba(11, 18, 32, 0.8);
  padding: 24px;
  border-radius: 12px;
  margin: 16px;
  width: 380px;
  text-align: center;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

select {
  padding: 10px;
  margin: 8px 0;
  background: #071627;
  color: #e6eef8;
  border: 1px solid #4f46e5;
  border-radius: 6px;
  width: 100%;
}

.options {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  margin-top: 16px;
}

.opt {
  padding: 12px;
  background: #071627;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  border: 1px solid rgba(255, 255, 255, 0.1);
  animation: slideIn 0.5s forwards;
  opacity: 0;
  transform: translateX(100%);
}

.opt:hover {
  background: #0d1e3a;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.opt.correct {
  background: #10b981;
  color: white;
}

.opt.wrong {
  background: #ef4444;
  color: white;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(100%);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.hidden {
  display: none;
}

#timer {
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 16px;
  color: #f59e0b;
}

#qText {
  font-size: 1.3rem;
  margin-bottom: 10px;
  line-height: 1.4;
}

#explain {
  margin-top: 16px;
  font-size: 14px;
  padding: 10px;
  border-radius: 6px;
  background: rgba(255, 255, 255, 0.1);
}

.progress-bar {
  width: 100%;
  height: 8px;
  background: #1e293b;
  border-radius: 4px;
  margin: 10px 0;
  overflow: hidden;
}

.progress {
  height: 100%;
  background: linear-gradient(90deg, #4f46e5, #7c3aed);
  border-radius: 4px;
  transition: width 0.3s ease;
}

.score-display {
  font-size: 1.5rem;
  font-weight: bold;
  margin: 10px 0;
  color: #10b981;
}

.game-stats {
  display: flex;
  justify-content: space-between;
  margin-bottom: 16px;
  font-size: 0.9rem;
  color: #94a3b8;
}
</style>
</head>
<body>

<h1>Edu-Fun 100+ Soal</h1>

<div id="intro" class="card">
  <h2>Selamat datang!</h2>
  <label>Pilih Mode:</label><br>
  <select id="modeSelect">
    <option value="general">Umum</option>
    <option value="math">Matematika</option>
    <option value="survival">Survival</option>
  </select><br>
  <label>Pilih Kesulitan:</label><br>
  <select id="levelSelect">
    <option value="easy">Mudah</option>
    <option value="medium">Sedang</option>
    <option value="hard">Sulit</option>
  </select><br>
  <button class="btn" onclick="startGame()">Mulai Game</button>
</div>

<div id="gameArea" class="card hidden">
  <div id="timer"></div>
  <div class="game-stats">
    <span id="scoreDisplay">Skor: 0</span>
    <span id="questionCount">Soal: 1/10</span>
  </div>
  <div class="progress-bar">
    <div id="progress" class="progress"></div>
  </div>
  <div id="qText"></div>
  <div class="options" id="opts"></div>
  <div id="explain"></div>
  <button class="btn" onclick="endGame()">Stop</button>
</div>

<div id="gameOver" class="card hidden">
  <h2>Game Over!</h2>
  <div class="score-display" id="scoreFinal"></div>
  <button class="btn" onclick="restartGame()">Main Lagi</button>
</div>

<script>
// ==== BANK SOAL 100+ ====
const questionBank = {
  general: {
    easy: [
      {q: 'Ibukota Indonesia?', opts: ['Jakarta', 'Bandung', 'Surabaya', 'Medan'], a: 'Jakarta', ex: 'Ibukota Indonesia adalah Jakarta'},
      {q: 'Presiden pertama Indonesia?', opts: ['Soekarno', 'Soeharto', 'Habibie', 'Jokowi'], a: 'Soekarno', ex: 'Presiden pertama adalah Soekarno'},
      {q: 'Hari kemerdekaan Indonesia?', opts: ['17 Agustus', '1 Januari', '25 Desember', '10 November'], a: '17 Agustus', ex: 'Hari kemerdekaan Indonesia 17 Agustus'},
      {q: 'Bendera merah putih bagian atas?', opts: ['Merah', 'Putih', 'Biru', 'Kuning'], a: 'Merah', ex: 'Merah di atas, putih di bawah'},
      {q: 'Bahasa resmi Indonesia?', opts: ['Indonesia', 'Inggris', 'Belanda', 'Jawa'], a: 'Indonesia', ex: 'Bahasa resmi adalah Indonesia'},
      {q: 'Warna bendera Indonesia?', opts: ['Merah-Putih', 'Putih-Merah', 'Merah-Hijau', 'Kuning-Hijau'], a: 'Merah-Putih', ex: 'Bendera Indonesia berwarna merah dan putih'},
      {q: 'Lambang negara Indonesia?', opts: ['Garuda Pancasila', 'Burung Hantu', 'Harimau', 'Elang'], a: 'Garuda Pancasila', ex: 'Lambang negara Indonesia adalah Garuda Pancasila'},
      {q: 'Pulau terbesar di Indonesia?', opts: ['Jawa', 'Sumatera', 'Kalimantan', 'Papua'], a: 'Papua', ex: 'Pulau terbesar di Indonesia adalah Papua'},
      {q: 'Mata uang Indonesia?', opts: ['Rupiah', 'Dollar', 'Ringgit', 'Baht'], a: 'Rupiah', ex: 'Mata uang Indonesia adalah Rupiah'},
      {q: 'Ibu kota provinsi Jawa Barat?', opts: ['Bandung', 'Jakarta', 'Semarang', 'Surabaya'], a: 'Bandung', ex: 'Ibu kota Jawa Barat adalah Bandung'}
    ],
    medium: [
      {q: 'Planet terbesar?', opts: ['Mars', 'Bumi', 'Jupiter', 'Saturnus'], a: 'Jupiter', ex: 'Planet terbesar adalah Jupiter'},
      {q: 'Gunung tertinggi di Indonesia?', opts: ['Kerinci', 'Semeru', 'Rinjani', 'Puncak Jaya'], a: 'Puncak Jaya', ex: 'Gunung tertinggi di Indonesia adalah Puncak Jaya'},
      {q: 'Presiden Indonesia kedua?', opts: ['Sukarno', 'Suharto', 'Habibie', 'Jokowi'], a: 'Suharto', ex: 'Presiden kedua Indonesia adalah Suharto'},
      {q: 'Benua terbesar di dunia?', opts: ['Asia', 'Afrika', 'Amerika', 'Eropa'], a: 'Asia', ex: 'Benua terbesar di dunia adalah Asia'},
      {q: 'Samudra terluas di dunia?', opts: ['Pasifik', 'Atlantik', 'Hindia', 'Arktik'], a: 'Pasifik', ex: 'Samudra terluas adalah Pasifik'},
      {q: 'Negara tetangga di utara Indonesia?', opts: ['Malaysia', 'Australia', 'Filipina', 'Thailand'], a: 'Malaysia', ex: 'Malaysia adalah negara tetangga di utara Indonesia'},
      {q: 'Ibu kota Australia?', opts: ['Sydney', 'Melbourne', 'Canberra', 'Perth'], a: 'Canberra', ex: 'Ibu kota Australia adalah Canberra'},
      {q: 'Penemu lampu pijar?', opts: ['Thomas Edison', 'Albert Einstein', 'Nikola Tesla', 'Alexander Graham Bell'], a: 'Thomas Edison', ex: 'Thomas Edison menemukan lampu pijar'},
      {q: 'Planet terdekat dengan matahari?', opts: ['Venus', 'Mars', 'Merkurius', 'Bumi'], a: 'Merkurius', ex: 'Planet terdekat dengan matahari adalah Merkurius'},
      {q: 'Satelit alami Bumi?', opts: ['Bulan', 'Mars', 'Venus', 'Matahari'], a: 'Bulan', ex: 'Satelit alami Bumi adalah Bulan'}
    ],
    hard: [
      {q: 'Tahun Proklamasi Indonesia?', opts: [1944, 1945, 1946, 1947], a: 1945, ex: 'Proklamasi Indonesia terjadi tahun 1945'},
      {q: 'Negara terkecil di dunia?', opts: ['Vatikan', 'Monaco', 'Malta', 'San Marino'], a: 'Vatikan', ex: 'Negara terkecil di dunia adalah Vatikan'},
      {q: 'Gunung tertinggi dunia?', opts: ['Everest', 'K2', 'Kilimanjaro', 'Elbrus'], a: 'Everest', ex: 'Gunung Everest tertinggi di dunia'},
      {q: 'Penulis novel "Laskar Pelangi"?', opts: ['Andrea Hirata', 'Tere Liye', 'Dee Lestari', 'Pramoedya Ananta Toer'], a: 'Andrea Hirata', ex: 'Andrea Hirata menulis "Laskar Pelangi"'},
      {q: 'Tahun berdirinya ASEAN?', opts: [1965, 1967, 1970, 1975], a: 1967, ex: 'ASEAN didirikan tahun 1967'},
      {q: 'Ibu kota Brasil?', opts: ['Rio de Janeiro', 'São Paulo', 'Brasília', 'Salvador'], a: 'Brasília', ex: 'Ibu kota Brasil adalah Brasília'},
      {q: 'Penemu telepon?', opts: ['Alexander Graham Bell', 'Thomas Edison', 'Nikola Tesla', 'Guglielmo Marconi'], a: 'Alexander Graham Bell', ex: 'Alexander Graham Bell menemukan telepon'},
      {q: 'Planet dengan cincin paling mencolok?', opts: ['Jupiter', 'Saturnus', 'Uranus', 'Neptunus'], a: 'Saturnus', ex: 'Saturnus memiliki cincin paling mencolok'},
      {q: 'Penemu teori relativitas?', opts: ['Isaac Newton', 'Albert Einstein', 'Stephen Hawking', 'Galileo Galilei'], a: 'Albert Einstein', ex: 'Albert Einstein menemukan teori relativitas'},
      {q: 'Tahun manusia pertama mendarat di bulan?', opts: [1967, 1969, 1971, 1973], a: 1969, ex: 'Manusia pertama mendarat di bulan tahun 1969'}
    ]
  },
  math: {
    easy: [
      {q: '2 + 3 = ?', opts: [4, 5, 6, 7], a: 5, ex: '2 + 3 = 5'},
      {q: '5 - 2 = ?', opts: [2, 3, 4, 5], a: 3, ex: '5 - 2 = 3'},
      {q: '3 x 2 = ?', opts: [5, 6, 7, 8], a: 6, ex: '3 x 2 = 6'},
      {q: '8 ÷ 4 = ?', opts: [1, 2, 3, 4], a: 2, ex: '8 ÷ 4 = 2'},
      {q: '7 + 5 = ?', opts: [11, 12, 13, 14], a: 12, ex: '7 + 5 = 12'},
      {q: '9 - 4 = ?', opts: [4, 5, 6, 7], a: 5, ex: '9 - 4 = 5'},
      {q: '4 x 3 = ?', opts: [10, 11, 12, 13], a: 12, ex: '4 x 3 = 12'},
      {q: '15 ÷ 3 = ?', opts: [3, 4, 5, 6], a: 5, ex: '15 ÷ 3 = 5'},
      {q: '6 + 7 = ?', opts: [12, 13, 14, 15], a: 13, ex: '6 + 7 = 13'},
      {q: '10 - 6 = ?', opts: [3, 4, 5, 6], a: 4, ex: '10 - 6 = 4'}
    ],
    medium: [
      {q: '(5 + 3) x 2 = ?', opts: [14, 15, 16, 17], a: 16, ex: '(5+3)x2=16'},
      {q: '20 ÷ (2 + 3) = ?', opts: [3, 4, 5, 6], a: 4, ex: '20 ÷ (2+3)=4'},
      {q: '7 x 8 ÷ 4 = ?', opts: [12, 13, 14, 15], a: 14, ex: '7x8 ÷4=14'},
      {q: '12 + 8 x 2 = ?', opts: [28, 32, 36, 40], a: 28, ex: '12 + (8x2) = 12 + 16 = 28'},
      {q: '25 - 5 x 3 = ?', opts: [10, 15, 20, 60], a: 10, ex: '25 - (5x3) = 25 - 15 = 10'},
      {q: '18 ÷ 3 + 4 = ?', opts: [8, 9, 10, 11], a: 10, ex: '(18÷3) + 4 = 6 + 4 = 10'},
      {q: '5² + 3² = ?', opts: [28, 32, 34, 36], a: 34, ex: '5² + 3² = 25 + 9 = 34'},
      {q: '100 ÷ 10 x 2 = ?', opts: [10, 15, 20, 25], a: 20, ex: '(100÷10) x 2 = 10 x 2 = 20'},
      {q: '15 + 7 x 2 - 5 = ?', opts: [24, 29, 34, 39], a: 24, ex: '15 + (7x2) - 5 = 15 + 14 - 5 = 24'},
      {q: '36 ÷ 6 + 3 x 2 = ?', opts: [9, 12, 15, 18], a: 12, ex: '(36÷6) + (3x2) = 6 + 6 = 12'}
    ],
    hard: [
      {q: '√144 = ?', opts: [10, 11, 12, 13], a: 12, ex: '√144 = 12'},
      {q: '(12 ÷ 3) x (4 + 1) = ?', opts: [18, 19, 20, 21], a: 20, ex: '(12 ÷3)x(4+1)=20'},
      {q: '7² - 15 = ?', opts: [33, 34, 35, 36], a: 34, ex: '7²-15=34'},
      {q: '3³ + 4² = ?', opts: [35, 37, 39, 43], a: 43, ex: '3³ + 4² = 27 + 16 = 43'},
      {q: '√81 + 5² = ?', opts: [30, 32, 34, 36], a: 34, ex: '√81 + 5² = 9 + 25 = 34'},
      {q: '15% dari 200 = ?', opts: [20, 25, 30, 35], a: 30, ex: '15% dari 200 = 0.15 x 200 = 30'},
      {q: 'Faktorisasi prima dari 36?', opts: ['2²x3²', '2x3³', '2³x3', '2²x3³'], a: '2²x3²', ex: 'Faktorisasi prima 36 = 2² x 3²'},
      {q: 'Kelipatan Persekutuan Terkecil (KPK) dari 6 dan 8?', opts: [24, 32, 36, 48], a: 24, ex: 'KPK dari 6 dan 8 adalah 24'},
      {q: 'Faktor Persekutuan Terbesar (FPB) dari 18 dan 24?', opts: [4, 6, 8, 12], a: 6, ex: 'FPB dari 18 dan 24 adalah 6'},
      {q: 'Hasil dari 2³ x 3² = ?', opts: [64, 68, 70, 72], a: 72, ex: '2³ x 3² = 8 x 9 = 72'}
    ]
  },
  survival: {
    easy: [
      {q: 'Bendera Indonesia?', opts: ['Merah', 'Putih', 'Merah-Putih', 'Biru'], a: 'Merah-Putih', ex: 'Bendera Indonesia merah-putih'},
      {q: '2 + 2 = ?', opts: [3, 4, 5, 6], a: 4, ex: '2 + 2 = 4'},
      {q: 'Ibukota Jepang?', opts: ['Seoul', 'Beijing', 'Tokyo', 'Bangkok'], a: 'Tokyo', ex: 'Ibukota Jepang adalah Tokyo'},
      {q: 'Warna daun?', opts: ['Merah', 'Biru', 'Hijau', 'Kuning'], a: 'Hijau', ex: 'Daun biasanya berwarna hijau'},
      {q: 'Planet kita?', opts: ['Mars', 'Bumi', 'Jupiter', 'Venus'], a: 'Bumi', ex: 'Planet kita adalah Bumi'}
    ],
    medium: [
      {q: '5 x 6 = ?', opts: [25, 30, 35, 40], a: 30, ex: '5 x 6 = 30'},
      {q: 'Ibukota Prancis?', opts: ['London', 'Berlin', 'Paris', 'Roma'], a: 'Paris', ex: 'Ibukota Prancis adalah Paris'},
      {q: 'Hewan tercepat di darat?', opts: ['Singa', 'Cheetah', 'Rusa', 'Kuda'], a: 'Cheetah', ex: 'Cheetah adalah hewan tercepat di darat'},
      {q: 'Warna langit cerah?', opts: ['Merah', 'Biru', 'Hijau', 'Kuning'], a: 'Biru', ex: 'Langit cerah berwarna biru'},
      {q: 'Planet terdekat dengan matahari?', opts: ['Venus', 'Mars', 'Merkurius', 'Bumi'], a: 'Merkurius', ex: 'Planet terdekat dengan matahari adalah Merkurius'}
    ],
    hard: [
      {q: '12² = ?', opts: [144, 132, 124, 120], a: 144, ex: '12² = 144'},
      {q: 'Ibukota Australia?', opts: ['Sydney', 'Melbourne', 'Canberra', 'Perth'], a: 'Canberra', ex: 'Ibukota Australia adalah Canberra'},
      {q: 'Penemu teori relativitas?', opts: ['Isaac Newton', 'Albert Einstein', 'Stephen Hawking', 'Galileo Galilei'], a: 'Albert Einstein', ex: 'Albert Einstein menemukan teori relativitas'},
      {q: 'Unsur kimia O adalah?', opts: ['Emas', 'Oksigen', 'Perak', 'Besi'], a: 'Oksigen', ex: 'O adalah simbol untuk Oksigen'},
      {q: 'Tahun manusia pertama mendarat di bulan?', opts: [1967, 1969, 1971, 1973], a: 1969, ex: 'Manusia pertama mendarat di bulan tahun 1969'}
    ]
  }
};

// ==== GAME STATE ====
let currentQuestions = [], currentIndex = 0, score = 0, timerInterval = null, timeLeft = 0, totalQuestions = 10;

function startGame() {
  const mode = document.getElementById('modeSelect').value;
  const level = document.getElementById('levelSelect').value;
  currentQuestions = shuffle(questionBank[mode][level]).slice(0, totalQuestions);
  currentIndex = 0;
  score = 0;

  document.getElementById('intro').classList.add('hidden');
  document.getElementById('gameArea').classList.remove('hidden');
  
  // Set timer berdasarkan mode
  if (mode === 'survival') {
    timeLeft = 10;
  } else if (level === 'easy') {
    timeLeft = 30;
  } else if (level === 'medium') {
    timeLeft = 25;
  } else {
    timeLeft = 20;
  }
  
  document.getElementById('timer').innerText = '⏱ ' + timeLeft + ' detik';
  document.getElementById('scoreDisplay').innerText = 'Skor: ' + score;
  document.getElementById('questionCount').innerText = 'Soal: 1/' + totalQuestions;
  document.getElementById('progress').style.width = '0%';
  
  timerInterval = setInterval(() => {
    timeLeft--;
    document.getElementById('timer').innerText = '⏱ ' + timeLeft + ' detik';
    if (timeLeft <= 0) {
      clearInterval(timerInterval);
      endGame();
    }
  }, 1000);

  loadQuestion();
}

function loadQuestion() {
  if (currentIndex >= currentQuestions.length) {
    endGame();
    return;
  }
  
  const q = currentQuestions[currentIndex];
  document.getElementById('qText').innerText = q.q;
  const optsDiv = document.getElementById('opts');
  optsDiv.innerHTML = '';
  
  // Update progress bar
  const progress = ((currentIndex) / totalQuestions) * 100;
  document.getElementById('progress').style.width = progress + '%';
  
  // Update question count
  document.getElementById('questionCount').innerText = 'Soal: ' + (currentIndex + 1) + '/' + totalQuestions;
  
  // Reset explanation
  document.getElementById('explain').innerText = '';
  document.getElementById('explain').className = '';
  
  // Create options with animation delay
  shuffle(q.opts).forEach((opt, index) => {
    const b = document.createElement('div');
    b.className = 'opt';
    b.innerText = opt;
    b.style.animationDelay = (index * 0.1) + 's';
    b.onclick = () => checkAnswer(opt, q);
    optsDiv.appendChild(b);
  });
}

function checkAnswer(selected, q) {
  const opts = document.querySelectorAll('.opt');
  let isCorrect = false;
  
  // Highlight correct and wrong answers
  opts.forEach(opt => {
    if (opt.innerText == q.a) {
      opt.classList.add('correct');
    }
    if (opt.innerText == selected && selected != q.a) {
      opt.classList.add('wrong');
    }
    opt.style.pointerEvents = 'none'; // Disable further clicks
  });
  
  // Update score and explanation
  if (selected == q.a) {
    score++;
    isCorrect = true;
    document.getElementById('scoreDisplay').innerText = 'Skor: ' + score;
    document.getElementById('explain').innerText = 'Benar! ' + q.ex;
    document.getElementById('explain').style.background = 'rgba(16, 185, 129, 0.2)';
  } else {
    document.getElementById('explain').innerText = 'Salah. ' + q.ex;
    document.getElementById('explain').style.background = 'rgba(239, 68, 68, 0.2)';
  }
  
  // Move to next question after a delay
  currentIndex++;
  setTimeout(loadQuestion, 1500);
}

function endGame() {
  clearInterval(timerInterval);
  document.getElementById('gameArea').classList.add('hidden');
  document.getElementById('gameOver').classList.remove('hidden');
  document.getElementById('scoreFinal').innerText = 'Skor Anda: ' + score + '/' + totalQuestions;
}

function restartGame() {
  document.getElementById('gameOver').classList.add('hidden');
  document.getElementById('intro').classList.remove('hidden');
}

function shuffle(a) {
  return a.slice().sort(() => Math.random() - 0.5);
}
</script>

</body>
</html>
