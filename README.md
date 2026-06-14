<!DOCTYPE html>
<html lang="ms" dir="ltr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Froggy Jumps - Kuiz Sahabat Nabi</title>
  
  <!-- Tailwind CSS & Google Font Fredoka untuk gaya kartun yang ceria -->
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@300..700&family=Noto+Naskh+Arabic:wght@400..700&family=Quicksand:wght@400;700&display=swap" rel="stylesheet">
  
  <style>
    body {
      font-family: 'Fredoka', 'Quicksand', sans-serif;
      background-color: #060c1c; /* Deep Dark Blue */
      overflow-x: hidden;
    }

    .jawi-text {
      font-family: 'Noto Naskh Arabic', 'Times New Roman', serif;
      direction: rtl;
      line-height: 1.8;
    }

    /* Animasi Daun Teratai Terapung */
    @keyframes floating {
      0% { transform: translateY(0px) rotate(0deg); }
      50% { transform: translateY(-8px) rotate(1.5deg); }
      100% { transform: translateY(0px) rotate(0deg); }
    }

    .floating-pad {
      animation: floating 4s ease-in-out infinite;
    }

    .floating-pad-delayed {
      animation: floating 4.5s ease-in-out infinite;
      animation-delay: 1s;
    }

    /* Animasi Bintang Bergerak di Latar Belakang */
    @keyframes drift {
      0% { transform: translateY(0) scale(0.8); opacity: 0.2; }
      50% { transform: translateY(-60px) scale(1.2); opacity: 0.9; }
      100% { transform: translateY(-120px) scale(0.8); opacity: 0.2; }
    }

    .star {
      position: absolute;
      background: radial-gradient(circle, #ffffff 0%, rgba(255,255,255,0) 70%);
      border-radius: 50%;
      pointer-events: none;
      animation: drift 7s ease-in-out infinite alternate;
    }

    /* Animasi Katak Melompat (Lengkung Parabola) */
    @keyframes jump-normal {
      0% { transform: scale(1) translateY(0); }
      30% { transform: scale(1.1, 0.9) translateY(-60px); }
      70% { transform: scale(0.9, 1.1) translateY(-140px); }
      100% { transform: scale(1) translateY(0); }
    }

    .frog-jumping {
      animation: jump-normal 0.8s ease-in-out forwards;
    }

    /* Animasi Gembira Katak */
    @keyframes happy-dance {
      0%, 100% { transform: scale(1) translateY(0); }
      25% { transform: scale(1.1, 0.9) translateY(-15px) rotate(-5deg); }
      50% { transform: scale(0.9, 1.1) translateY(-30px) rotate(5deg); }
      75% { transform: scale(1.1, 0.9) translateY(-15px) rotate(-5deg); }
    }

    .frog-happy {
      animation: happy-dance 0.6s ease-in-out 2;
    }

    /* Animasi Tenggelam Air (Splash) */
    @keyframes splash-down {
      0% { transform: scale(1) translateY(0); opacity: 1; }
      50% { transform: scale(0.7) translateY(20px); opacity: 0.5; }
      100% { transform: scale(0.1) translateY(50px); opacity: 0; }
    }

    .frog-splash {
      animation: splash-down 0.8s ease-in forwards;
    }

    /* Cetakan khas untuk Sijil Penghargaan sahaja */
    @media print {
      body * {
        visibility: hidden;
      }
      #certificate-print-section, #certificate-print-section * {
        visibility: visible;
      }
      #certificate-print-section {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        background: white !important;
        color: black !important;
      }
      .no-print {
        display: none !important;
      }
    }
  </style>
</head>
<body class="min-h-screen flex flex-col justify-between text-white relative">

  <!-- BACKGROUND DECORATIONS -->
  <div class="absolute inset-0 z-0 overflow-hidden pointer-events-none">
    <!-- Air Kolam Gradient (Vibrant Dark Blue Midnight Theme) -->
    <div class="absolute inset-0 bg-gradient-to-b from-[#020617] via-[#0b1329] to-[#1e1b4b]"></div>
    
    <!-- Wadah Bintang Bergerak Dinamik -->
    <div id="stars-container-bg" class="absolute inset-0"></div>
    
    <!-- Lukisan Algae / Rumput Kolam Kartun -->
    <svg class="absolute bottom-0 left-0 w-full h-32 text-indigo-950/45" preserveAspectRatio="none" viewBox="0 0 1440 120">
      <path fill="currentColor" d="M0,96L48,85.3C96,75,192,53,288,53.3C384,53,480,75,576,85.3C672,96,768,96,864,85.3C960,75,1056,53,1152,42.7C1248,32,1344,32,1392,32L1440,32L1440,120L1392,120C1344,120,1248,120,1152,120C1056,120,960,120,864,120C768,120,672,120,576,120C480,120,384,120,288,120C192,120,96,120,48,120L0,120Z"></path>
    </svg>
  </div>

  <!-- MAIN HEADER (No Print) -->
  <header class="w-full py-4 px-6 z-10 flex justify-between items-center bg-[#0f172a]/90 backdrop-blur border-b border-indigo-500/30 no-print shadow-md">
    <div class="flex items-center gap-3">
      <span class="text-3xl animate-bounce">🐸</span>
      <div>
        <h1 class="text-xl font-black tracking-wider text-yellow-300 drop-shadow">FROGGY JUMPS</h1>
        <p class="text-xs text-sky-200 font-bold">Kuiz Pendidikan Kisah Sahabat</p>
      </div>
    </div>
    <div class="flex items-center gap-4">
      <button onclick="toggleMute()" id="sound-btn" class="bg-indigo-600 hover:bg-indigo-500 px-3.5 py-1.5 rounded-full text-sm font-bold flex items-center gap-2 transition-all shadow-md border border-indigo-400">
        <span>🔊</span> <span id="sound-text" class="hidden sm:inline">Bunyi Aktif</span>
      </button>
    </div>
  </header>

  <!-- MAIN CONTAINER FOR SCREENS -->
  <main class="flex-grow flex items-center justify-center p-4 z-10 no-print">

    <!-- ================= SCREEN 1: WELCOME & REGISTRATION ================= -->
    <div id="screen-welcome" class="w-full max-w-lg bg-gradient-to-br from-indigo-900 via-slate-900 to-indigo-950 border-4 border-yellow-400 rounded-3xl p-6 sm:p-8 text-center shadow-[0_15px_30px_rgba(0,0,0,0.4)] relative transition-all duration-500 scale-100">
      
      <!-- Katak Maskot daripada pautan Imgur -->
      <div class="absolute -top-16 left-1/2 -translate-x-1/2 w-32 h-32 drop-shadow-xl animate-bounce">
        <img id="welcome-frog-img" src="https://i.imgur.com/UdA0LH9.png" alt="Froggy" class="w-full h-full object-contain" onerror="this.onerror=null; this.src='https://placehold.co/128x128/22c55e/ffffff?text=🐸';">
      </div>

      <h2 class="text-3xl sm:text-4xl font-extrabold text-yellow-300 mt-12 mb-2 tracking-wide uppercase drop-shadow-[0_3px_0_rgba(15,23,42,0.8)]">KISAH SAHABAT RASULULLAH</h2>
      <p class="text-sky-100 text-sm sm:text-base mb-6 font-medium bg-black/30 rounded-2xl p-3 border border-indigo-500/20">Bantu si katak ceria melompat ke seberang kolam dengan answering kuiz kisah keteguhan iman para sahabat Nabi!</p>

      <!-- Input Form (Tona Kuning Ceria) -->
      <div class="space-y-4 mb-6 text-left">
        <div>
          <label class="block text-yellow-300 font-bold mb-1 text-sm tracking-wide drop-shadow-sm">NAMA PELAJAR:</label>
          <input type="text" id="player-name" placeholder="Masukkan nama anda..." 
            class="w-full bg-slate-950/80 border-2 border-yellow-400 rounded-xl px-4 py-3 text-yellow-300 text-lg font-bold placeholder-yellow-300/40 focus:outline-none focus:border-yellow-300 transition-all shadow-inner">
        </div>
        <div>
          <label class="block text-yellow-300 font-bold mb-1 text-sm tracking-wide drop-shadow-sm">KELAS / TINGKATAN:</label>
          <input type="text" id="player-class" placeholder="Contoh: 4 Ibnu Sina, Kelas Melur..." 
            class="w-full bg-slate-950/80 border-2 border-yellow-400 rounded-xl px-4 py-3 text-yellow-300 text-lg font-bold placeholder-yellow-300/40 focus:outline-none focus:border-yellow-300 transition-all shadow-inner">
        </div>
      </div>

      <!-- Play Button -->
      <button onclick="startGame()" class="w-full bg-gradient-to-r from-yellow-400 to-amber-500 hover:from-yellow-300 hover:to-amber-400 text-slate-950 text-xl font-black py-4 px-8 rounded-2xl transform active:scale-95 transition-all shadow-[0_6px_0_#9a3412] hover:shadow-[0_4px_0_#9a3412] hover:translate-y-[2px] active:translate-y-[6px] tracking-widest">
        MULA MAIN! 🚀
      </button>

      <p class="text-sky-300 text-xs mt-4 font-semibold">Pastikan pembesar suara anda dibuka untuk menikmati suasana kolam yang ceria!</p>
    </div>

    <!-- ================= SCREEN 2: THE GAME BOARD ================= -->
    <div id="screen-game" class="hidden w-full max-w-4xl flex flex-col gap-4">
      
      <!-- Top Status HUD -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-3 bg-slate-900/90 border-2 border-indigo-500/40 rounded-2xl p-4 shadow-lg">
        <div class="flex items-center gap-2">
          <span class="text-2xl">👤</span>
          <div class="overflow-hidden">
            <p class="text-[10px] text-sky-200 uppercase font-bold tracking-wider leading-none">Pemain</p>
            <p id="hud-name" class="font-bold text-yellow-300 truncate text-sm sm:text-base drop-shadow-sm">Pemain</p>
          </div>
        </div>
        <div class="flex items-center gap-2">
          <span class="text-2xl">🏫</span>
          <div class="overflow-hidden">
            <p class="text-[10px] text-sky-200 uppercase font-bold tracking-wider leading-none">Kelas</p>
            <p id="hud-class" class="font-bold text-yellow-300 truncate text-sm sm:text-base drop-shadow-sm">Kelas</p>
          </div>
        </div>
        <div class="flex items-center justify-between col-span-2 md:col-span-2 flex-wrap gap-2 pt-2 border-t border-slate-700 md:pt-0 md:border-t-0">
          <div class="flex items-center gap-1.5">
            <span class="text-red-500 text-xl">❤️</span>
            <span class="text-xs font-bold mr-1 text-sky-200">NYAWA:</span>
            <div id="hud-lives" class="flex gap-1 text-lg">
              <!-- Hearts injection -->
            </div>
          </div>
          <div class="flex items-center gap-1.5">
            <span class="text-amber-300 text-xl">⭐</span>
            <span class="text-xs font-bold text-sky-200">SKOR:</span>
            <span id="hud-score" class="font-black text-xl text-yellow-300 drop-shadow-sm">0</span>
          </div>
        </div>
      </div>

      <!-- Game Stage & Floating Elements Area -->
      <div class="relative bg-slate-900/50 border-4 border-indigo-500/30 rounded-3xl p-6 shadow-2xl overflow-hidden min-h-[480px] flex flex-col justify-between">
        
        <!-- Jangka Masa Timer & Progress Bar -->
        <div class="w-full flex items-center gap-3 bg-black/30 px-3 py-2 rounded-full mb-4">
          <span class="text-sm font-bold text-yellow-300 whitespace-nowrap">SOALAN <span id="current-question-num">1</span>/10</span>
          <div class="flex-grow bg-slate-950 h-3 rounded-full overflow-hidden border border-indigo-500/30">
            <div id="progress-bar" class="bg-gradient-to-r from-green-400 to-yellow-300 h-full w-10% transition-all duration-500"></div>
          </div>
          <div class="flex items-center gap-1 bg-red-600/80 px-2.5 py-0.5 rounded-full border border-red-400">
            <span class="animate-pulse">⏱️</span>
            <span id="hud-timer" class="font-mono font-bold text-white text-sm">30s</span>
          </div>
        </div>

        <!-- Question Box -->
        <div class="bg-yellow-50 text-slate-950 rounded-2xl p-4 sm:p-6 shadow-xl border-3 border-amber-300 relative">
          <!-- RTL Jawi / Arab Support -->
          <div id="question-text" class="jawi-text text-right text-xl sm:text-2xl font-bold leading-relaxed tracking-wide py-1">
            Sila tunggu...
          </div>
          
          <!-- Hint/Pembayaran Button -->
          <button onclick="revealHint()" id="hint-btn" class="absolute -bottom-4 right-6 bg-yellow-400 hover:bg-yellow-300 text-amber-950 font-black text-xs px-4 py-1.5 rounded-full shadow-md flex items-center gap-1 transition-all border border-amber-200">
            <span>💡</span> PEMBAYANG (HINT)
          </button>
        </div>

        <!-- Hint Overlay Card -->
        <div id="hint-card" class="hidden mt-4 bg-amber-100/95 border-2 border-amber-300 text-amber-900 rounded-xl p-3 text-xs sm:text-sm flex gap-2 items-start transition-all shadow-md">
          <span class="text-lg">💡</span>
          <div>
            <span class="font-bold">Pembayang:</span>
            <span id="hint-text" class="italic jawi-text text-right block mt-1 text-base">Pembayang</span>
          </div>
        </div>

        <!-- Interactive Pond / Lily Pad Area -->
        <div class="relative flex-grow flex flex-col justify-end items-center my-8 min-h-[220px]">
          
          <!-- Options Lily Pads Grid (Dark Purple Theme with white font) -->
          <div id="options-grid" class="w-full grid grid-cols-1 md:grid-cols-2 gap-4 z-10">
            <!-- Dynamic Buttons with pure JS to avoid template strings -->
          </div>

          <!-- Central Starting Water Lily with Frog (Imgur Katak) -->
          <div class="absolute bottom-[-10px] left-1/2 -translate-x-1/2 flex flex-col items-center z-20">
            <div id="froggy-character" class="w-24 h-24 transition-all duration-500 origin-bottom">
              <img id="game-frog-img" src="https://i.imgur.com/UdA0LH9.png" alt="Froggy Character" class="w-full h-full object-contain drop-shadow-lg" onerror="this.onerror=null; this.src='https://placehold.co/128x128/22c55e/ffffff?text=🐸';">
            </div>
            
            <!-- Base Starting Lily Pad -->
            <div class="w-32 h-8 bg-green-600 rounded-full border-b-4 border-green-800 flex items-center justify-center -mt-4 shadow-lg">
              <span class="text-[10px] text-green-100 tracking-widest font-black uppercase">MULA</span>
            </div>
          </div>

          <!-- Splash Effect Container -->
          <div id="splash-effect" class="absolute bottom-4 left-1/2 -translate-x-1/2 w-32 h-32 hidden z-10 pointer-events-none">
            <div class="absolute inset-0 rounded-full border-4 border-cyan-300 opacity-0 animate-ping"></div>
            <div class="absolute inset-4 rounded-full border-2 border-sky-300 opacity-0 animate-pulse" style="animation-duration: 0.5s;"></div>
            <span class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 text-xl font-bold text-sky-100 uppercase tracking-widest drop-shadow">SPLASH!</span>
          </div>
        </div>

      </div>
    </div>

    <!-- ================= SCREEN 3: RESULTS & SCOREBOARD ================= -->
    <div id="screen-score" class="hidden w-full max-w-3xl bg-gradient-to-br from-indigo-950 via-slate-900 to-indigo-900 border-4 border-yellow-400 rounded-3xl p-6 sm:p-8 text-center shadow-2xl relative transition-all duration-500">
      
      <span class="text-6xl block mb-2">🏆</span>
      <h2 class="text-3xl font-extrabold text-yellow-300 mb-1 tracking-wide uppercase drop-shadow-[0_2px_0_rgba(0,0,0,0.5)]">REKOD KEPUTUSAN</h2>
      <p class="text-sky-200 text-sm mb-6">Syabas! Anda telah melengkapkan Kuiz Sahabat.</p>

      <!-- Student Badge Card -->
      <div class="bg-indigo-950/60 border-2 border-indigo-500/40 rounded-2xl p-4 mb-6 flex flex-col sm:flex-row justify-between items-center gap-4">
        <div class="text-left w-full sm:w-auto">
          <p class="text-xs text-sky-300 font-bold uppercase">Nama Pemain</p>
          <h3 id="score-name" class="text-2xl font-black text-yellow-300">Nama</h3>
          <p class="text-xs text-sky-300 font-bold uppercase mt-2">Kelas / Tingkatan</p>
          <p id="score-class" class="text-lg font-bold text-white">Kelas</p>
        </div>
        <div class="bg-gradient-to-b from-yellow-400 to-amber-500 text-slate-950 p-4 rounded-xl text-center shadow-lg w-full sm:w-36">
          <p class="text-xs font-black uppercase tracking-wider leading-none">SKOR AKHIR</p>
          <p id="score-final" class="text-4xl font-extrabold mt-1">100</p>
          <p class="text-[10px] font-bold mt-1 text-slate-800" id="score-accuracy">Akurasi: 100%</p>
        </div>
      </div>

      <!-- Rating Stars -->
      <div class="mb-6 bg-black/30 rounded-2xl p-4">
        <p class="text-xs text-sky-200 uppercase font-black tracking-widest mb-2">Penarafan Anda</p>
        <div id="stars-container" class="flex justify-center gap-2 text-4xl">
          <!-- Dynamic Stars Injection -->
        </div>
        <p id="rating-feedback" class="text-yellow-300 font-bold mt-2">Sangat Cemerlang!</p>
      </div>

      <!-- Review Section -->
      <div class="mb-8 text-left">
        <h4 class="text-lg font-bold text-yellow-300 mb-3 border-b border-indigo-500/30 pb-2">🔍 ULASAN JAWAPAN KUIZ</h4>
        <div id="review-list" class="space-y-4 max-h-[250px] overflow-y-auto pr-2 custom-scrollbar">
          <!-- Dynamic review injected with pure JS -->
        </div>
      </div>

      <!-- Actions Buttons -->
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
        <button onclick="window.print()" class="bg-gradient-to-r from-blue-500 to-indigo-600 hover:from-blue-400 hover:to-indigo-500 text-white font-bold py-3.5 px-6 rounded-xl transform active:scale-95 transition-all shadow-lg flex items-center justify-center gap-2">
          <span>🖨️</span> CETAK SIJIL KEPUTUSAN
        </button>
        <button onclick="restartGame()" class="bg-gradient-to-r from-yellow-400 to-amber-500 hover:from-yellow-300 hover:to-amber-400 text-slate-950 font-black py-3.5 px-6 rounded-xl transform active:scale-95 transition-all shadow-lg flex items-center justify-center gap-2">
          <span>🔄</span> MAIN SEMULA
        </button>
      </div>

    </div>

  </main>

  <!-- ================= KOTAK AMARAN KUSTOM (CUSTOM TOAST) ================= -->
  <!-- Mencegah isu tersekatnya fungsi browser alert() lalai dalam pelayar terbenam -->
  <div id="custom-modal-alert" class="hidden fixed inset-0 bg-black/70 flex items-center justify-center z-50 p-4">
    <div class="bg-slate-900 border-4 border-yellow-400 rounded-3xl p-6 max-w-sm w-full text-center shadow-2xl transform scale-95 transition-transform duration-300">
      <span class="text-5xl block mb-2">💡</span>
      <h3 class="text-xl font-bold text-yellow-300 mb-2">MAKLUMAT DIPERLUKAN</h3>
      <p id="custom-modal-text" class="text-sky-200 text-sm mb-6">Sila isi Nama dan Kelas anda terlebih dahulu sebelum memulakan cabaran kuiz!</p>
      <button onclick="hideAlert()" class="w-full bg-gradient-to-r from-yellow-400 to-amber-500 text-slate-950 font-black py-2.5 px-6 rounded-xl shadow-md transform active:scale-95 transition-transform">
        FAHAM, OK!
      </button>
    </div>
  </div>

  <!-- ================= PRINT SECTION: THE CERTIFICATE ================= -->
  <div id="certificate-print-section" class="hidden p-8 max-w-4xl mx-auto border-[16px] border-indigo-950 bg-white text-slate-950 text-center relative flex-col justify-between" style="min-height: 297mm; font-family: 'Times New Roman', serif;">
    <div class="border-4 border-yellow-500 p-8 flex-grow flex flex-col justify-between">
      
      <!-- Decor Frame -->
      <div>
        <span class="text-6xl block">🐸🏆🐸</span>
        <h1 class="text-4xl font-extrabold text-indigo-950 mt-4 tracking-widest uppercase">SIJIL PENGHARGAAN</h1>
        <p class="text-xl italic text-indigo-800 mt-1">CABARAN KUIZ FROGGY JUMPS</p>
        <div class="w-48 h-1 bg-yellow-500 mx-auto my-4"></div>
      </div>

      <div class="my-8">
        <p class="text-lg text-slate-700">Sijil ini dengan bangganya dianugerahkan kepada:</p>
        <h2 id="cert-name" class="text-3xl font-bold text-yellow-600 underline decoration-yellow-500 underline-offset-8 mt-2 mb-1">Nama Pelajar</h2>
        <p class="text-lg text-slate-700">dari kelas / tingkatan</p>
        <p id="cert-class" class="text-xl font-bold text-slate-950">Nama Kelas</p>
      </div>

      <div class="my-6 max-w-xl mx-auto bg-slate-50 p-6 rounded-xl border border-slate-200">
        <p class="text-base text-slate-800 leading-relaxed">
          Kerana telah berjaya menyelesaikan ujian interaktif <strong class="text-slate-950">Kuiz Kisah Keteguhan Iman Sahabat Nabi</strong> dengan pencapaian yang berikut:
        </p>
        
        <div class="grid grid-cols-3 gap-4 mt-4 text-center">
          <div class="border-r border-slate-200">
            <span class="block text-xs uppercase text-slate-500">Skor Diperoleh</span>
            <span id="cert-score" class="text-2xl font-extrabold text-indigo-950">0/100</span>
          </div>
          <div class="border-r border-slate-200">
            <span class="block text-xs uppercase text-slate-500">Bintang Penarafan</span>
            <span id="cert-lives" class="text-2xl font-extrabold text-indigo-950">⭐</span>
          </div>
          <div>
            <span class="block text-xs uppercase text-slate-500">Akurasi</span>
            <span id="cert-accuracy" class="text-2xl font-extrabold text-indigo-950">0%</span>
          </div>
        </div>
      </div>

      <div>
        <p class="text-sm text-slate-600 italic">"Keteguhan iman para sahabat adalah pelita jalan kehidupan mukmin sejati."</p>
        <div class="flex justify-between items-end mt-12 px-8">
          <div class="text-left">
            <div class="w-36 border-t border-slate-800 my-1"></div>
            <p class="text-xs uppercase text-slate-500">Tandatangan Guru</p>
          </div>
          <div class="text-right">
            <p class="text-xs text-slate-500">Tarikh:</p>
            <p id="cert-date" class="text-sm font-bold text-slate-950">12 Jun 2026</p>
          </div>
        </div>
      </div>

    </div>
  </div>

  <!-- FOOTER -->
  <footer class="w-full py-3 text-center bg-slate-950 border-t border-indigo-950 text-sky-200 text-xs z-10 no-print font-medium shadow-inner">
    <p>© 2026 Froggy Jumps Educaplay. Hak Cipta Terpelihara.</p>
  </footer>

  <!-- JAVASCRIPT GAME ENGINE -->
  <script>
    const questions = [
      {
        id: 1,
        question: "سياڤاكه صحابة يڠ دڤوكول سهيڠݢ تيدق سدركن ديري كتيک ممبري اوچڤن مڠاجق قوم قريش كڤد إسلام؟",
        hint: "فيكيركن صحابة يڠ دباوا ڤولڠ اوليه اهلي كلوارݢڽ ستله ڤيڠسن دڤوكول.",
        options: [
          { key: "A", text: "عبد الله بن مسعود" },
          { key: "B", text: "بلال بن رباح" },
          { key: "C", text: "سيدنا عثمان بن عفان" },
          { key: "D", text: "سيدنا ابو بكر الصديق" }
        ],
        correct: "D",
        rationale: "سيدنا ابو بكر الصديق دڤوكول اوليه سكومڤولن قوم قريش كتيک براني مڽوواراكن دعوه سچارا تربوک."
      },
      {
        id: 2,
        question: "اڤاكه يڠ برلاكو كڤد سمية سماس دسيقسا اوليه ابو جهل؟",
        hint: "فيكيركن سجنيس سنجات تاجيم يڠ دڬوناكن اوليه ابو جهل.",
        options: [
          { key: "A", text: "دتيكم دڠن لمبيڠ سهيڠݢ ماتي" },
          { key: "B", text: "دليتقكن باتو يڠ بسر دأتس دادا" },
          { key: "C", text: "دايکت كدوا تاڠنڽ دان دبياركن" },
          { key: "D", text: "دڤوكول سهيڠݢ برلوموران داره" }
        ],
        correct: "A",
        rationale: "سمية منيڠݢل دنيا ستله دتيكم اوليه ابو جهل دڠن لمبيڠ سماس دسيقسا."
      },
      {
        id: 3,
        question: "سياڤاكه يڠ مڽقسا بلال بن رباح داتس ڤاسير يڠ ڤانس؟",
        hint: "اين مروڤاكن اوندڠ٢ زمان جاهيلية دمان سأورڠ همبا اداله ميليق سبارڠ كڤد كاد توانڽ.",
        options: [
          { key: "A", text: "ابو جهل" },
          { key: "B", text: "سكومڤولن قريش" },
          { key: "C", text: "باڤ سودارا" },
          { key: "D", text: "توانڽ سنديري" }
        ],
        correct: "D",
        rationale: "سباڬاي سأورڠ همبا, بلال تله دسيقسا اوليه توانڽ سنديري (امية بن خلف) كران مملوق اڬام إسلام."
      },
      {
        id: 4,
        question: "مڠاڤاكه عبد الله بن مسعود دڤوكول اوليه قوم قريش سهيڠݢ لوكا-لوكا؟",
        hint: "فيكيركن عنصور كأڬاماءن يڠ ڤالڠ دبنچي اوليه قريش اونتوق ددڠر سچارا تربوک.",
        options: [
          { key: "A", text: "ابو بكر" },
          { key: "B", text: "كران مڠاجق ابو جهل ماسوق إسلام" },
          { key: "C", text: "كران برهجره ك مدینه" },
          { key: "D", text: "كران ممباچ القرءان" }
        ],
        correct: "D",
        rationale: "بلياو دڤوكول كتيک سدڠ ممباچ ايات٢ سوچي القرءان دالونن يڠ ددڠري اوليه قوم قريش."
      },
      {
        id: 5,
        question: "باڬايماناکه عثمان بن عفان دسيقسا اوليه باڤ ساوداراڽ؟",
        hint: "سيقساءن اين ملبتكن ڤربواتن مڠکت اڠݢوتا بادn بلياو.",
        options: [
          { key: "A", text: "دڤقسا ممباچ القرءان" },
          { key: "B", text: "دايکت كدوا تاڠنڽ" },
          { key: "C", text: "دجامين ماسوق نراک" },
          { key: "D", text: "دڤوكول دڠن كايو" }
        ],
        correct: "B",
        rationale: "بلياو دسيقسا دڠن چارا دايکت دان دبياركن سلما ببراڤ هاري."
      },
      {
        id: 6,
        question: "ياسر، ياءيت باڤ عمار، تله منيڠݢل دنيا کران سيقساءن ابو جهل.",
        hint: "فيكيركن نصيب يڠ دتريما اوليه كدوا-دوا ايبو دان باڤ عمار بن ياسر.",
        options: [
          { key: "A", text: "بتول" },
          { key: "B", text: "ساله" }
        ],
        correct: "A",
        rationale: "تيكس مڽاتاكن بهاوا ياسر منيڠݢل دنيا كران سيقساءن كجم يڠ دtريماڽ."
      },
      {
        id: 7,
        question: "سيدنا ابو بكر الصديق اداله اورڠ يڠ مڽيقسا بلال بن رباح سبلوم ممرديكاكنڽ.",
        hint: "ڤرنهكه سأورڠ صحابة يڠ ايمانڽ كوات مڽيقسا صحابة يڠ لاءين؟",
        options: [
          { key: "A", text: "ساله" },
          { key: "B", text: "بتول" }
        ],
        correct: "A",
        rationale: "سيدنا ابو بكر الصديق اداله ڤپلامت يڠ ممبري سڬالاڽ اونتوق ممرديكاكن بلال، بوكن مڽيقساڽ."
      },
      {
        id: 8,
        question: "ڤارا صحابة يڠ دسيقسا تتڤ تڬوه ايمان دان صبر مڠهادڤي چوباءن ترسبوت.",
        hint: "فيكيركن سبب مريک دجامين شرک اوليه نبي محمد ﷺ.",
        options: [
          { key: "A", text: "بتول" },
          { key: "B", text: "ساله" }
        ],
        correct: "A",
        rationale: "تيكس مڽاتاكن بهاوا ايمان مريک تيدق براوبه والاوڤون دسيقسا دڠن تروق."
      },
      {
        id: 9,
        question: "اهلي كلوارڬ سيدنا ابو بكر تله داتڠ ممبنتو دان منولوڠڽ سماس بلياو دڤوكول.",
        hint: "ليهت كڤد باهاڬيان اول تيكس يڠ مڽبوتكن تنتڠ بلياو دباوا كلوار.",
        options: [
          { key: "A", text: "ساله" },
          { key: "B", text: "بتول" }
        ],
        correct: "B",
        rationale: "موجورله اهلي كلوارڬ بلياو داتڠ ممبنتو سبلوم ڤركارا يڠ لبيه بوروق برلاكو."
      },
      {
        id: 10,
        question: "بلال بن رباح دسيقسا دڠن دليتقكن باتو دأتس كڤالاڽ سماس دجمور.",
        hint: "فيكيركن اڠڬوتا بادن يڠ برادا دباوه ليهير.",
        options: [
          { key: "A", text: "ساله" },
          { key: "B", text: "بتول" }
        ],
        correct: "A",
        rationale: "باتو ترسبوت دليتقكن دأتس دادا بلياو، بوكن دأتس كڤالا."
      }
    ];

    // State Permainan
    var player = {
      name: "",
      className: "",
      score: 0,
      lives: 3,
      currentQuestionIdx: 0,
      answers: []
    };

    var timer = null;
    var timeLeft = 30;
    var soundEnabled = true;

    // Web Audio API Synthesizer Engine dengan kawalan ralat murni
    var audioCtx = null;

    function initAudio() {
      if (!audioCtx) {
        try {
          audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        } catch (e) {
          console.warn("Sistem Audio tidak disokong pada pelayar ini.", e);
        }
      }
    }

    function toggleMute() {
      soundEnabled = !soundEnabled;
      var soundBtn = document.getElementById('sound-btn');
      if (soundEnabled) {
        soundBtn.innerHTML = '<span>🔊</span> <span id="sound-text" class="hidden sm:inline">Bunyi Aktif</span>';
        soundBtn.className = "bg-indigo-600 hover:bg-indigo-500 px-3.5 py-1.5 rounded-full text-sm font-bold flex items-center gap-2 transition-all shadow-md border border-indigo-400";
      } else {
        soundBtn.innerHTML = '<span>🔇</span> <span id="sound-text" class="hidden sm:inline">Bunyi Senyap</span>';
        soundBtn.className = "bg-red-500 hover:bg-red-400 px-3.5 py-1.5 rounded-full text-sm font-bold flex items-center gap-2 transition-all shadow-md border border-red-300";
      }
    }

    function playSound(type) {
      if (!soundEnabled) return;
      initAudio();
      if (!audioCtx) return;

      if (audioCtx.state === 'suspended') {
        audioCtx.resume();
      }

      try {
        var osc = audioCtx.createOscillator();
        var gainNode = audioCtx.createGain();
        osc.connect(gainNode);
        gainNode.connect(audioCtx.destination);

        var now = audioCtx.currentTime;

        if (type === 'jump') {
          osc.frequency.setValueAtTime(150, now);
          osc.frequency.exponentialRampToValueAtTime(600, now + 0.35);
          gainNode.gain.setValueAtTime(0.2, now);
          gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.35);
          osc.start(now);
          osc.stop(now + 0.35);
        } else if (type === 'splash') {
          osc.type = 'triangle';
          osc.frequency.setValueAtTime(120, now);
          osc.frequency.exponentialRampToValueAtTime(40, now + 0.5);
          gainNode.gain.setValueAtTime(0.3, now);
          gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.5);
          osc.start(now);
          osc.stop(now + 0.5);
        } else if (type === 'correct') {
          osc.type = 'sine';
          var notes = [330, 440, 660];
          notes.forEach(function(freq, idx) {
            var oscNode = audioCtx.createOscillator();
            var gainN = audioCtx.createGain();
            oscNode.connect(gainN);
            gainN.connect(audioCtx.destination);
            oscNode.frequency.setValueAtTime(freq, now + idx * 0.08);
            gainN.gain.setValueAtTime(0.15, now + idx * 0.08);
            gainN.gain.exponentialRampToValueAtTime(0.01, now + idx * 0.08 + 0.2);
            oscNode.start(now + idx * 0.08);
            oscNode.stop(now + idx * 0.08 + 0.2);
          });
        } else if (type === 'incorrect') {
          osc.type = 'sawtooth';
          osc.frequency.setValueAtTime(180, now);
          osc.frequency.linearRampToValueAtTime(120, now + 0.4);
          gainNode.gain.setValueAtTime(0.25, now);
          gainNode.gain.exponentialRampToValueAtTime(0.01, now + 0.4);
          osc.start(now);
          osc.stop(now + 0.4);
        } else if (type === 'gameover') {
          osc.type = 'triangle';
          var fanfare = [261.63, 329.63, 392.00, 523.25];
          fanfare.forEach(function(freq, idx) {
            var oscNode = audioCtx.createOscillator();
            var gainN = audioCtx.createGain();
            oscNode.connect(gainN);
            gainN.connect(audioCtx.destination);
            oscNode.frequency.setValueAtTime(freq, now + idx * 0.15);
            gainN.gain.setValueAtTime(0.18, now + idx * 0.15);
            gainN.gain.exponentialRampToValueAtTime(0.01, now + idx * 0.15 + 0.4);
            oscNode.start(now + idx * 0.15);
            oscNode.stop(now + idx * 0.15 + 0.4);
          });
        }
      } catch (err) {
        console.warn("Kesalahan pensintesis bunyi:", err);
      }
    }

    function initMovingStars() {
      var container = document.getElementById('stars-container-bg');
      if (!container) return;
      container.innerHTML = '';
      for (var i = 0; i < 35; i++) {
        var star = document.createElement('div');
        star.className = 'star';
        var size = Math.random() * 4 + 2; 
        star.style.width = size + 'px';
        star.style.height = size + 'px';
        star.style.left = (Math.random() * 100) + '%';
        star.style.top = (Math.random() * 100) + '%';
        star.style.animationDelay = (Math.random() * 6) + 's';
        star.style.animationDuration = (Math.random() * 4 + 4) + 's';
        star.style.boxShadow = '0 0 8px #fef08a';
        container.appendChild(star);
      }
    }

    function showAlert(msg) {
      document.getElementById('custom-modal-text').innerText = msg;
      var modal = document.getElementById('custom-modal-alert');
      modal.classList.remove('hidden');
      setTimeout(function() {
        modal.querySelector('div').classList.remove('scale-95');
        modal.querySelector('div').classList.add('scale-100');
      }, 50);
    }

    function hideAlert() {
      var modal = document.getElementById('custom-modal-alert');
      modal.querySelector('div').classList.remove('scale-100');
      modal.querySelector('div').classList.add('scale-95');
      setTimeout(function() {
        modal.classList.add('hidden');
      }, 150);
    }

    function startGame() {
      var nameInput = document.getElementById('player-name').value.trim();
      var classInput = document.getElementById('player-class').value.trim();

      if (!nameInput || !classInput) {
        showAlert("Sila masukkan Nama dan Kelas anda sebelum memulakan permainan!");
        return;
      }

      player.name = nameInput;
      player.className = classInput;
      player.score = 0;
      player.lives = 3;
      player.currentQuestionIdx = 0;
      player.answers = [];

      document.getElementById('hud-name').innerText = player.name;
      document.getElementById('hud-class').innerText = player.className;
      document.getElementById('hud-score').innerText = player.score;
      updateLivesHUD();

      document.getElementById('screen-welcome').classList.add('hidden');
      document.getElementById('screen-game').classList.remove('hidden');

      initAudio();
      loadQuestion();
    }

    function updateLivesHUD() {
      var container = document.getElementById('hud-lives');
      container.innerHTML = '';
      for (var i = 0; i < 3; i++) {
        if (i < player.lives) {
          container.innerHTML += '<span class="text-red-500 animate-pulse">❤️</span>';
        } else {
          container.innerHTML += '<span class="opacity-30">🖤</span>';
        }
      }
    }

    function loadQuestion() {
      var currentQ = questions[player.currentQuestionIdx];
      
      document.getElementById('current-question-num').innerText = player.currentQuestionIdx + 1;
      document.getElementById('progress-bar').style.width = ((player.currentQuestionIdx) / questions.length * 100) + '%';
      
      var qTextContainer = document.getElementById('question-text');
      qTextContainer.innerText = currentQ.question;
      
      document.getElementById('hint-card').classList.add('hidden');
      document.getElementById('hint-text').innerText = currentQ.hint;
      document.getElementById('hint-btn').classList.remove('opacity-50', 'pointer-events-none');

      var optionsGrid = document.getElementById('options-grid');
      optionsGrid.innerHTML = '';

      // Menjana butang jawapan secara dinamik menggunakan createElement bagi mengelakkan sebarang ralat sintaksis
      currentQ.options.forEach(function(opt, idx) {
        var delayClass = (idx % 2 === 0) ? 'floating-pad' : 'floating-pad-delayed';
        
        var btn = document.createElement('button');
        btn.onclick = function() { selectOption(opt.key, btn); };
        btn.className = 'group relative flex items-center justify-between bg-purple-900 hover:bg-purple-800 border-3 border-purple-400 hover:border-yellow-300 rounded-3xl p-4 shadow-[0_8px_0_#3b0764] hover:shadow-[0_4px_0_#3b0764] transition-all transform active:scale-95 text-right w-full ' + delayClass + ' hover:translate-y-[2px] active:translate-y-[6px]';
        
        var badge = document.createElement('div');
        badge.className = 'w-10 h-10 rounded-full bg-yellow-300 border-2 border-purple-950 flex items-center justify-center font-black text-purple-950 text-lg group-hover:scale-110 transition-transform';
        badge.innerText = opt.key;
        
        var textDiv = document.createElement('div');
        textDiv.className = 'jawi-text text-white font-black text-lg sm:text-xl pr-2 text-right w-full drop-shadow-[0_1.5px_0_rgba(22,101,52,0.8)]';
        textDiv.innerText = opt.text;
        
        btn.appendChild(badge);
        btn.appendChild(textDiv);
        optionsGrid.appendChild(btn);
      });

      var frog = document.getElementById('froggy-character');
      frog.className = "w-24 h-24 transition-all duration-500 origin-bottom";
      frog.style.transform = "none";
      
      startTimer();
    }

    function revealHint() {
      document.getElementById('hint-card').classList.remove('hidden');
      document.getElementById('hint-btn').classList.add('opacity-50', 'pointer-events-none');
    }

    function startTimer() {
      clearInterval(timer);
      timeLeft = 30;
      document.getElementById('hud-timer').innerText = timeLeft + 's';
      document.getElementById('hud-timer').className = "font-mono font-bold text-white text-sm";

      timer = setInterval(function() {
        timeLeft--;
        document.getElementById('hud-timer').innerText = timeLeft + 's';

        if (timeLeft <= 10) {
          document.getElementById('hud-timer').className = "font-mono font-bold text-yellow-300 text-sm animate-bounce";
        }
        if (timeLeft <= 0) {
          clearInterval(timer);
          timeoutAction();
        }
      }, 1000);
    }

    function timeoutAction() {
      disableAllOptions();
      playSound('incorrect');

      var frog = document.getElementById('froggy-character');
      frog.classList.add('frog-splash');

      var splash = document.getElementById('splash-effect');
      splash.classList.remove('hidden');

      player.lives--;
      updateLivesHUD();

      var currentQ = questions[player.currentQuestionIdx];
      player.answers.push({
        questionId: currentQ.id,
        userAns: "TIADA JAWAPAN",
        isCorrect: false
      });

      highlightAnswers(currentQ.correct, null);

      setTimeout(function() {
        splash.classList.add('hidden');
        nextStep();
      }, 3000);
    }

    function disableAllOptions() {
      var pads = document.querySelectorAll('#options-grid button');
      pads.forEach(function(p) {
        p.disabled = true;
        p.style.pointerEvents = 'none';
        p.classList.remove('floating-pad', 'floating-pad-delayed');
      });
    }

    function selectOption(selectedKey, buttonElement) {
      clearInterval(timer);
      disableAllOptions();

      var currentQ = questions[player.currentQuestionIdx];
      var isCorrect = selectedKey === currentQ.correct;

      var frog = document.getElementById('froggy-character');
      var rectButton = buttonElement.getBoundingClientRect();
      var rectFrog = frog.getBoundingClientRect();

      var diffX = rectButton.left + (rectButton.width / 2) - (rectFrog.left + (rectFrog.width / 2));
      var diffY = rectButton.top - rectFrog.top - 20;

      playSound('jump');

      frog.style.transform = 'translate(' + diffX + 'px, ' + diffY + 'px)';
      frog.classList.add('frog-jumping');

      player.answers.push({
        questionId: currentQ.id,
        userAns: selectedKey,
        isCorrect: isCorrect
      });

      setTimeout(function() {
        frog.classList.remove('frog-jumping');

        if (isCorrect) {
          playSound('correct');
          frog.classList.add('frog-happy');
          buttonElement.classList.add('bg-green-600', 'border-green-300', 'shadow-[0_8px_0_#14532d]');
          
          player.score += 10;
          document.getElementById('hud-score').innerText = player.score;
        } else {
          playSound('incorrect');
          setTimeout(function() { playSound('splash'); }, 250);
          
          frog.classList.add('frog-splash');
          buttonElement.classList.add('bg-red-600', 'border-red-300', 'shadow-[0_8px_0_#7f1d1d]');
          
          var splash = document.getElementById('splash-effect');
          splash.style.left = (rectButton.left + (rectButton.width/2) - (window.innerWidth - document.querySelector('main').offsetWidth)/2) + 'px';
          splash.classList.remove('hidden');

          player.lives--;
          updateLivesHUD();
        }

        highlightAnswers(currentQ.correct, selectedKey);

        setTimeout(function() {
          document.getElementById('splash-effect').classList.add('hidden');
          nextStep();
        }, 2500);

      }, 800);
    }

    function highlightAnswers(correctKey, userKey) {
      var pads = document.querySelectorAll('#options-grid button');
      pads.forEach(function(p) {
        var optionKey = p.querySelector('.w-10').innerText.trim();
        if (optionKey === correctKey) {
          p.classList.remove('bg-purple-900');
          p.classList.add('bg-green-600', 'border-green-300', 'shadow-[0_8px_0_#14532d]');
        } else if (optionKey === userKey && userKey !== correctKey) {
          p.classList.remove('bg-purple-900');
          p.classList.add('bg-red-600', 'border-red-300', 'shadow-[0_8px_0_#7f1d1d]');
        }
      });
    }

    function nextStep() {
      if (player.lives <= 0 || player.currentQuestionIdx >= questions.length - 1) {
        endGame();
      } else {
        player.currentQuestionIdx++;
        loadQuestion();
      }
    }

    function endGame() {
      clearInterval(timer);
      playSound('gameover');

      document.getElementById('screen-game').classList.add('hidden');
      document.getElementById('screen-score').classList.remove('hidden');

      document.getElementById('score-name').innerText = player.name;
      document.getElementById('score-class').innerText = player.className;
      document.getElementById('score-final').innerText = player.score + '/100';

      var accuracy = (player.answers.filter(function(a) { return a.isCorrect; }).length / questions.length) * 100;
      document.getElementById('score-accuracy').innerText = 'Akurasi Jawapan: ' + accuracy + '%';

      var starsContainer = document.getElementById('stars-container');
      var ratingFeedback = document.getElementById('rating-feedback');
      starsContainer.innerHTML = '';

      var numStars = 1;
      if (player.score >= 90) {
        numStars = 3;
        ratingFeedback.innerText = "🏆 CEMERLANG: Pejuang Teratai Emas! 🏆";
        ratingFeedback.className = "text-yellow-300 font-extrabold text-lg tracking-wide";
      } else if (player.score >= 50) {
        numStars = 2;
        ratingFeedback.innerText = "⭐ SANGAT BAIK: Teruskan Usaha Anda! ⭐";
        ratingFeedback.className = "text-green-300 font-bold text-md";
      } else {
        numStars = 1;
        ratingFeedback.innerText = "🌱 USAHA LAGI: Imbas Kembali Kisah Sahabat! 🌱";
        ratingFeedback.className = "text-red-300 font-bold text-md";
      }

      for (var i = 0; i < 3; i++) {
        if (i < numStars) {
          starsContainer.innerHTML += '<span class="text-yellow-400 drop-shadow-[0_2px_4px_rgba(0,0,0,0.5)]">⭐</span>';
        } else {
          starsContainer.innerHTML += '<span class="opacity-20">⭐</span>';
        }
      }

      document.getElementById('cert-name').innerText = player.name.toUpperCase();
      document.getElementById('cert-class').innerText = player.className.toUpperCase();
      document.getElementById('cert-score').innerText = player.score + '/100';
      document.getElementById('cert-accuracy').innerText = accuracy + '%';
      
      var certStars = '';
      for (var i = 0; i < numStars; i++) certStars += '⭐';
      document.getElementById('cert-lives').innerText = certStars;

      var dateNow = new Date();
      var options = { day: 'numeric', month: 'long', year: 'numeric' };
      document.getElementById('cert-date').innerText = dateNow.toLocaleDateString('ms-MY', options);

      var reviewList = document.getElementById('review-list');
      reviewList.innerHTML = '';

      // Membina senarai ulasan jawapan dengan kaedah DOM yang bersih bagi mengelakkan sebarang ralat sintaksis
      questions.forEach(function(q, idx) {
        var userAttempt = player.answers.find(function(a) { return a.questionId === q.id; });
        var attemptedText = userAttempt ? userAttempt.userAns : "TIADA";
        var isCorrect = userAttempt ? userAttempt.isCorrect : false;

        var borderClass = isCorrect ? 'border-green-500' : 'border-red-500';
        var bgClass = isCorrect ? 'bg-green-950/80' : 'bg-red-950/80';
        var textClass = isCorrect ? 'text-green-300' : 'text-red-300';
        var badgeSign = isCorrect ? '✔️ BETUL' : '❌ SALAH';

        var itemDiv = document.createElement('div');
        itemDiv.className = 'border-2 ' + borderClass + ' ' + bgClass + ' ' + textClass + ' rounded-xl p-4 transition-all';
        
        var headerDiv = document.createElement('div');
        headerDiv.className = 'flex justify-between items-center gap-2 flex-wrap-reverse mb-2';
        
        var badgeSpan = document.createElement('span');
        badgeSpan.className = 'text-xs font-bold px-2.5 py-1 rounded-full bg-black/40 tracking-widest';
        badgeSpan.innerText = badgeSign;
        
        var numSpan = document.createElement('span');
        numSpan.className = 'text-xs text-yellow-300 font-bold';
        numSpan.innerText = 'SOALAN ' + (idx + 1);
        
        headerDiv.appendChild(badgeSpan);
        headerDiv.appendChild(numSpan);
        
        var qText = document.createElement('p');
        qText.className = 'jawi-text text-right text-lg text-white font-medium mb-2 border-b border-white/10 pb-2';
        qText.innerText = q.question;
        
        var infoGrid = document.createElement('div');
        infoGrid.className = 'grid grid-cols-2 gap-2 text-xs text-teal-100';
        
        var userDiv = document.createElement('div');
        userDiv.innerHTML = 'Jawapan Anda: <strong class="text-white">' + attemptedText + '</strong>';
        
        var correctDiv = document.createElement('div');
        correctDiv.innerHTML = 'Jawapan Betul: <strong class="text-yellow-300">' + q.correct + '</strong>';
        
        infoGrid.appendChild(userDiv);
        infoGrid.appendChild(correctDiv);
        
        var rationaleDiv = document.createElement('div');
        rationaleDiv.className = 'mt-2 bg-black/20 p-2.5 rounded-lg text-xs leading-relaxed text-yellow-200';
        rationaleDiv.innerHTML = '<strong>📖 Huraian:</strong> ' + q.rationale;
        
        itemDiv.appendChild(headerDiv);
        itemDiv.appendChild(qText);
        itemDiv.appendChild(infoGrid);
        itemDiv.appendChild(rationaleDiv);
        
        reviewList.appendChild(itemDiv);
      });
    }

    function restartGame() {
      document.getElementById('screen-score').classList.add('hidden');
      document.getElementById('screen-welcome').classList.remove('hidden');
      document.getElementById('player-name').value = '';
      document.getElementById('player-class').value = '';
    }

    // Memulakan bintang malam semasa pelayar dimuatkan
    window.onload = function() {
      initMovingStars();
    }
  </script>
</body>
</html>
