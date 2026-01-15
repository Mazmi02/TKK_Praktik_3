<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kuis Pengetahuan Umum Dasar</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f0f0f0;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
            overflow: hidden;
        }

        .quiz-container {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 600px;
            text-align: center;
            position: relative;
            transition: transform 0.2s ease;
            transform-origin: center center;
        }

        h1 {
            color: #333;
            margin-bottom: 10px;
        }

        /* --- HAMBURGER MENU ICON --- */
        .menu-icon {
            position: absolute;
            top: 15px;
            right: 20px;
            font-size: 24px;
            cursor: pointer;
            color: #333;
            z-index: 1001;
            user-select: none;
            padding: 5px;
        }

        /* --- SETTINGS MENU PANEL --- */
        .settings-menu {
            position: absolute;
            top: 50px;
            right: 20px;
            background-color: white;
            border: 1px solid #ddd;
            border-radius: 8px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            padding: 15px;
            width: 290px;
            z-index: 1000;
            display: flex;
            flex-direction: column;
            gap: 15px;
            text-align: left;
        }

        .menu-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.9em;
            color: #555;
            font-weight: bold;
        }

        /* --- STYLE KONTROL PLUS/MINUS --- */
        .number-control-wrapper {
            display: flex;
            align-items: center;
            gap: 10px;
            background-color: #f9f9f9;
            padding: 5px;
            border-radius: 5px;
        }

        .btn-control {
            width: 30px;
            height: 30px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 1.2em;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            line-height: 1;
        }
        .btn-control:hover { background-color: #0056b3; }
        .btn-control:active { transform: scale(0.95); }

        .control-value-text {
            width: 20px;
            text-align: center;
            font-size: 1em;
            color: #333;
        }

        /* --- Toggle Switch Style (iOS) --- */
        .switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 28px;
        }
        .switch input { opacity: 0; width: 0; height: 0; }
        .slider {
            position: absolute;
            cursor: pointer;
            top: 0; left: 0; right: 0; bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 34px;
        }
        .slider:before {
            position: absolute;
            content: "";
            height: 20px; width: 20px;
            left: 4px; bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }
        input:checked + .slider { background-color: #28a745; }
        input:focus + .slider { box-shadow: 0 0 1px #28a745; }
        input:checked + .slider:before { transform: translateX(22px); }

        /* --- Tampilan Counter --- */
        .question-counter-text {
            font-size: 1em;
            color: #666;
            margin-bottom: 20px;
            display: block; 
            min-height: 1.2em;
        }

        #question-container { margin-bottom: 20px; }
        #question {
            font-size: 1.5em;
            font-weight: bold;
            margin-bottom: 25px;
            color: #444;
        }

        .btn-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-bottom: 20px;
        }

        .btn {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 12px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1em;
            transition: background-color 0.2s ease;
            word-wrap: break-word;
            min-height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            outline: none;
            font-weight: bold;
        }

        .btn:not(.correct):not(.wrong):not(.skip-btn):not(.btn-nav) { background-color: #007bff; }
        .btn.correct { background-color: #28a745 !important; }
        .btn.wrong { background-color: #dc3545 !important; }
        .btn:disabled { cursor: not-allowed; opacity: 0.65; }
        .btn:disabled:not(.correct):not(.wrong) { background-color: #6c757d !important; color: #ccc !important; }

        .controls {
            display: flex;
            justify-content: center;
            gap: 10px;
        }

        #skip-navigation-controls {
            justify-content: space-between; 
            margin-top: 40px;
            margin-bottom: 10px;
            display: flex; 
            align-items: center;
        }

        .skip-btn { 
            background-color: #28a745; color: white;
            padding: 8px 12px; font-size: 0.9em; min-width: 60px; border-radius: 5px;
        }
        .skip-btn:hover { background-color: #218838; }
        .skip-btn:disabled { background-color: #a3d8b0 !important; }

        .btn-nav {
            background-color: #5F9EA0; color: white; 
            padding: 8px 12px; font-size: 0.9em; min-width: 50px; border-radius: 5px;
            font-weight: bold;
        }
        .btn-nav:hover:not([disabled]) { background-color: #4682B4; }
        .btn-nav:disabled { background-color: #B0C4DE !important; color: #666666 !important; }

        #completion-message {
            color: #28a745; font-size: 1.2em; font-weight: bold;
            margin-top: 5px; margin-bottom: 20px;
        }

        .hide { display: none !important; }
    </style>
</head>
<body>

    <div class="quiz-container" id="main-container">
        <div id="menu-icon" class="menu-icon">≡</div>

        <div id="settings-menu" class="settings-menu hide">
            
            <div class="menu-row">
                <span>Info Soal</span>
                <label class="switch">
                    <input type="checkbox" id="toggle-counter" checked>
                    <span class="slider round"></span>
                </label>
            </div>

            <div class="menu-row">
                <span>Tombol Next (&gt;)</span>
                <label class="switch">
                    <input type="checkbox" id="toggle-next-btn">
                    <span class="slider round"></span>
                </label>
            </div>

            <div class="menu-row">
                <span>Zoom (1-10)</span>
                <div class="number-control-wrapper">
                    <button id="zoom-out-btn" class="btn-control">-</button>
                    <span id="zoom-value-display" class="control-value-text">5</span>
                    <button id="zoom-in-btn" class="btn-control">+</button>
                </div>
            </div>

            <div class="menu-row">
                <span>Next Soal (Detik)</span>
                <div class="number-control-wrapper">
                    <button id="timer-minus-btn" class="btn-control">-</button>
                    <span id="timer-value-display" class="control-value-text">3</span>
                    <button id="timer-plus-btn" class="btn-control">+</button>
                </div>
            </div>

            <div class="menu-row">
                <span>Otomatis Klik</span>
                <label class="switch">
                    <input type="checkbox" id="toggle-auto-click">
                    <span class="slider round"></span>
                </label>
            </div>

        </div>

        <h1>Pengetahuan Umum Dasar</h1>
        <p id="completion-message" class="hide">Selamat Kuis Sudah Selesai 🎉</p>
        
        <div id="initial-controls" class="controls">
            <button id="start-btn" class="btn">Mulai</button>
            <button id="continue-btn" class="btn hide">Lanjutkan</button>
        </div>
        
        <div id="question-counter" class="question-counter-text hide">0/0</div>
        
        <div id="question-container" class="hide">
            <div id="question">Kata Bahasa Inggris</div>
            <div id="answer-buttons" class="btn-grid">
            </div>
            
            <div id="skip-navigation-controls" class="controls hide">
                <button id="prev-50-btn" class="btn skip-btn">&laquo; 50</button>
                <div style="display: flex; gap: 5px;">
                    <button id="prev-question-btn" class="btn btn-nav">&lt;</button>
                    <button id="next-question-btn" class="btn btn-nav hide">&gt;</button>
                </div>
                <button id="next-50-btn" class="btn skip-btn">50 &raquo;</button>
            </div>
        </div>
    </div>

    <script>
        const mainContainer = document.getElementById('main-container');
        const startButton = document.getElementById('start-btn');
        const continueButton = document.getElementById('continue-btn');
        const initialControls = document.getElementById('initial-controls');
        const completionMessageElement = document.getElementById('completion-message');
        const questionContainerElement = document.getElementById('question-container');
        const questionElement = document.getElementById('question');
        const answerButtonsElement = document.getElementById('answer-buttons');
        const questionCounterElement = document.getElementById('question-counter');

        // Navigasi
        const skipNavigationControls = document.getElementById('skip-navigation-controls');
        const prev50Button = document.getElementById('prev-50-btn');
        const prevQuestionButton = document.getElementById('prev-question-btn');
        const nextQuestionButton = document.getElementById('next-question-btn'); 
        const next50Button = document.getElementById('next-50-btn');
        const JUMP_AMOUNT = 50;

        // Menu & Pengaturan Elements
        const menuIcon = document.getElementById('menu-icon');
        const settingsMenu = document.getElementById('settings-menu');
        const toggleCounterInput = document.getElementById('toggle-counter');
        const toggleNextBtnInput = document.getElementById('toggle-next-btn');
        const toggleAutoClickInput = document.getElementById('toggle-auto-click');
        
        // ZOOM Elements
        const zoomOutBtn = document.getElementById('zoom-out-btn');
        const zoomInBtn = document.getElementById('zoom-in-btn');
        const zoomValueDisplay = document.getElementById('zoom-value-display');
        let currentZoomLevel = 5; 

        // TIMER Elements
        const timerMinusBtn = document.getElementById('timer-minus-btn');
        const timerPlusBtn = document.getElementById('timer-plus-btn');
        const timerValueDisplay = document.getElementById('timer-value-display');
        let autoNextDelay = 3; 

        let orderedQuestions, currentQuestionIndex;
        let score = 0;
        let questionTimeout;
        let autoClickTimeout; 
        
        // --- LOGIKA MENU PENGATURAN ---

        menuIcon.addEventListener('click', (e) => {
            e.stopPropagation(); 
            settingsMenu.classList.toggle('hide');
        });
        settingsMenu.addEventListener('click', (e) => {
            e.stopPropagation(); 
        });
        document.addEventListener('click', (e) => {
            if (!settingsMenu.contains(e.target) && e.target !== menuIcon) {
                settingsMenu.classList.add('hide');
            }
        });

        // Info Soal
        toggleCounterInput.addEventListener('change', updateCounterDisplay);
        function updateCounterDisplay() {
            if (!orderedQuestions) return;
            const current = currentQuestionIndex + 1;
            const total = orderedQuestions.length;
            if (toggleCounterInput.checked) {
                questionCounterElement.innerText = `${current} / ${total}`;
                questionCounterElement.style.fontSize = "1em"; 
            } else {
                questionCounterElement.innerText = "∞";
                questionCounterElement.style.fontSize = "1.2em"; 
            }
        }

        // Tombol Next
        toggleNextBtnInput.addEventListener('change', () => {
            if (toggleNextBtnInput.checked) {
                nextQuestionButton.classList.remove('hide');
            } else {
                nextQuestionButton.classList.add('hide');
            }
        });

        // Zoom Control
        function applyZoom() {
            zoomValueDisplay.innerText = currentZoomLevel;
            const scale = 0.5 + (currentZoomLevel * 0.1);
            mainContainer.style.transform = `scale(${scale})`;
        }
        zoomOutBtn.addEventListener('click', (e) => {
            if (currentZoomLevel > 1) {
                currentZoomLevel--;
                applyZoom();
            }
        });
        zoomInBtn.addEventListener('click', (e) => {
            if (currentZoomLevel < 10) {
                currentZoomLevel++;
                applyZoom();
            }
        });
        applyZoom();

        // Timer Control
        function updateTimerDisplay() {
            timerValueDisplay.innerText = autoNextDelay;
        }
        timerMinusBtn.addEventListener('click', (e) => {
            if (autoNextDelay > 1) {
                autoNextDelay--;
                updateTimerDisplay();
            }
        });
        timerPlusBtn.addEventListener('click', (e) => {
            if (autoNextDelay < 15) {
                autoNextDelay++;
                updateTimerDisplay();
            }
        });
        updateTimerDisplay(); 

        // PERBAIKAN: LOGIKA EVENT LISTENER UNTUK AUTO KLIK
        // Saat tombol digeser, langsung cek apakah bisa menjawab
        toggleAutoClickInput.addEventListener('change', () => {
            if (toggleAutoClickInput.checked) {
                // Cek apakah sedang ada soal yang aktif dan belum dijawab
                const correctBtn = Array.from(answerButtonsElement.children).find(b => b.dataset.correct === 'true');
                if (correctBtn && !correctBtn.disabled) {
                    // Jika ada soal aktif, langsung trigger auto answer dalam 1 detik
                    clearTimeout(autoClickTimeout); // Bersihkan timer lama jika ada
                    autoClickTimeout = setTimeout(() => {
                        selectAnswer({ target: correctBtn });
                    }, 1000);
                }
            } else {
                // Jika dimatikan, batalkan timer yang sedang berjalan
                clearTimeout(autoClickTimeout);
            }
        });


        // --- LOGIKA KUIS ---

        const rawVocabularyList = [
		
  { "en": "Apa Fungsi Perintah Line (AutoCAD)?", "id": "Membuat Garis Lurus." },
  { "en": "Apa Shortcut Untuk Perintah Circle (AutoCAD)?", "id": "Ketik C + Enter." },
  { "en": "Apa Fungsi Trim (AutoCAD)?", "id": "Memotong Garis Yang Bersinggungan." },
  { "en": "Tombol Apa Untuk Mengaktifkan Ortho Mode (AutoCAD)?", "id": "Tombol F8." },
  { "en": "Apa Fungsi Perintah Eraser (AutoCAD)?", "id": "Menghapus Objek Gambar." },
  { "en": "Apa Shortcut Untuk Perintah Move (AutoCAD)?", "id": "Ketik M + Enter." },
  { "en": "Apa Fungsi Mirror (AutoCAD)?", "id": "Mencerminkan Objek Terpilih." },
  { "en": "Apa Fungsi Offset (AutoCAD)?", "id": "Membuat Garis Sejajar." },
  { "en": "Tombol F3 Berfungsi Untuk Apa (AutoCAD)?", "id": "Mengaktifkan Object Snap." },
  { "en": "Apa Fungsi Perintah Copy (AutoCAD)?", "id": "Menggandakan Objek Gambar." },
  { "en": "Apa Shortcut Untuk Perintah Rectangle (AutoCAD)?", "id": "Ketik REC + Enter." },
  { "en": "Apa Fungsi Fillet (AutoCAD)?", "id": "Melengkungkan Sudut Garis." },
  { "en": "Apa Fungsi Chamfer (AutoCAD)?", "id": "Memangkas Sudut Garis." },
  { "en": "Apa Fungsi Dimension (AutoCAD)?", "id": "Memberi Ukuran Gambar." },
  { "en": "Apa Shortcut Untuk Undo (AutoCAD)?", "id": "Tekan Ctrl + Z." },
  { "en": "Apa Fungsi Zoom Extents (AutoCAD)?", "id": "Menampilkan Seluruh Gambar." },
  { "en": "Bahasa Pemrograman Apa Yang Digunakan (Arduino IDE)?", "id": "Bahasa C++." },
  { "en": "Apa Fungsi Void Setup (Arduino IDE)?", "id": "Menjalankan Kode 1 Kali." },
  { "en": "Apa Fungsi Void Loop (Arduino IDE)?", "id": "Menjalankan Kode Berulang." },
  { "en": "Apa Fungsi Serial Monitor (Arduino IDE)?", "id": "Menampilkan Data Serial." },
  { "en": "Apa Fungsi PinMode (Arduino IDE)?", "id": "Mengatur Mode Pin." },
  { "en": "Apa Fungsi DigitalWrite (Arduino IDE)?", "id": "Mengirim Sinyal Digital." },
  { "en": "Apa Fungsi DigitalRead (Arduino IDE)?", "id": "Membaca Sinyal Digital." },
  { "en": "Apa Fungsi AnalogRead (Arduino IDE)?", "id": "Membaca Sinyal Analog." },
  { "en": "Apa Fungsi Delay (Arduino IDE)?", "id": "Memberi Jeda Waktu." },
  { "en": "Tombol Apa Untuk Upload Kode (Arduino IDE)?", "id": "Tombol Panah Kanan." },
  { "en": "Apa Fungsi Verify (Arduino IDE)?", "id": "Mengecek Kesalahan Kode." },
  { "en": "Apa Arti LED (Arduino IDE)?", "id": "Dioda Pemancar Cahaya." },
  { "en": "Berapa Tegangan Kerja Arduino Uno (Arduino IDE)?", "id": "5 Volt DC." },
  { "en": "Apa Fungsi Library (Arduino IDE)?", "id": "Menambah Fungsi Tambahan." },
  { "en": "Apa Itu Sketch (Arduino IDE)?", "id": "Program Yang Ditulis." },
  { "en": "Apa Fungsi AnalogWrite (Arduino IDE)?", "id": "Mengirim Sinyal PWM." },
  { "en": "CX Programmer Digunakan Untuk PLC Merk Apa (CX Programmer)?", "id": "Merk Omron." },
  { "en": "Apa Simbol Kontak NO (CX Programmer)?", "id": "2 Garis Terputus." },
  { "en": "Apa Simbol Kontak NC (CX Programmer)?", "id": "Garis Terputus Berpalang." },
  { "en": "Apa Fungsi Coil Pada Ladder (CX Programmer)?", "id": "Output Logika Program." },
  { "en": "Apa Shortcut Membuat Kontak Baru (CX Programmer)?", "id": "Ketik C." },
  { "en": "Apa Shortcut Membuat Coil Baru (CX Programmer)?", "id": "Ketik O." },
  { "en": "Apa Fungsi Timer (CX Programmer)?", "id": "Menunda Waktu Eksekusi." },
  { "en": "Apa Fungsi Counter (CX Programmer)?", "id": "Menghitung Jumlah Input." },
  { "en": "Apa Instruksi MOV (CX Programmer)?", "id": "Memindahkan Data Memori." },
  { "en": "Apa Fungsi Compile (CX Programmer)?", "id": "Mengecek Error Program." },
  { "en": "Apa Arti Mnemonic (CX Programmer)?", "id": "Bentuk Teks Instruksi." },
  { "en": "Apa Fungsi Work Online (CX Programmer)?", "id": "Terhubung Ke PLC." },
  { "en": "Apa Shortcut Menambah Garis Horizontal (CX Programmer)?", "id": "Ctrl + Panah Kanan." },
  { "en": "Apa Fungsi Instruksi END (CX Programmer)?", "id": "Mengakhiri Program PLC." },
  { "en": "Apa Fungsi Differential Up (CX Programmer)?", "id": "Deteksi Sinyal Naik." },
  { "en": "Apa Fungsi Differential Down (CX Programmer)?", "id": "Deteksi Sinyal Turun." },
  { "en": "Aplikasi Ini Digunakan Untuk Simulasi Apa (Proteus)?", "id": "Rangkaian Elektronika." },
  { "en": "Apa Fungsi ISIS (Proteus)?", "id": "Menggambar Skematik Rangkaian." },
  { "en": "Apa Fungsi ARES (Proteus)?", "id": "Membuat Desain PCB." },
  { "en": "Bagaimana Cara Menambah Komponen (Proteus)?", "id": "Klik Tombol P." },
  { "en": "Apa Fungsi Ground Pada Simulasi (Proteus)?", "id": "Referensi Tegangan 0." },
  { "en": "Apa Fungsi VCC (Proteus)?", "id": "Sumber Tegangan Positif." },
  { "en": "Apa Fungsi Virtual Terminal (Proteus)?", "id": "Melihat Data Serial." },
  { "en": "Apa Fungsi Oscilloscope (Proteus)?", "id": "Melihat Bentuk Gelombang." },
  { "en": "Apa Warna Kabel Error (Proteus)?", "id": "Warna Kuning." },
  { "en": "Apa Fungsi Voltmeter (Proteus)?", "id": "Mengukur Tegangan Listrik." },
  { "en": "Apa Fungsi Ammeter (Proteus)?", "id": "Mengukur Arus Listrik." },
  { "en": "Apa Tombol Untuk Menjalankan Simulasi (Proteus)?", "id": "Tombol Play." },
  { "en": "Apa Tombol Untuk Menghentikan Simulasi (Proteus)?", "id": "Tombol Stop." },
  { "en": "Apa Fungsi Wire Label (Proteus)?", "id": "Menamai Jalur Kabel." },
  { "en": "Apa Fungsi Bus Mode (Proteus)?", "id": "Membuat Jalur Bus." },
  { "en": "Apa Fungsi Generator Mode (Proteus)?", "id": "Memberi Sinyal Input." },
  { "en": "Aplikasi Ini Digunakan Untuk Apa (ETAP)?", "id": "Analisis Sistem Tenaga." },
  { "en": "Apa Fungsi Load Flow Analysis (ETAP)?", "id": "Analisis Aliran Daya." },
  { "en": "Apa Fungsi Short Circuit Analysis (ETAP)?", "id": "Analisis Hubung Singkat." },
  { "en": "Apa Simbol Bus Pada Single Line (ETAP)?", "id": "Garis Tebal Lurus." },
  { "en": "Apa Fungsi Generator (ETAP)?", "id": "Sumber Daya Listrik." },
  { "en": "Apa Fungsi Transformer (ETAP)?", "id": "Mengubah Level Tegangan." },
  { "en": "Apa Fungsi Cable (ETAP)?", "id": "Penghantar Arus Listrik." },
  { "en": "Apa Fungsi Motor Induction (ETAP)?", "id": "Beban Motor Listrik." },
  { "en": "Apa Satuan Daya Aktif (ETAP)?", "id": "Watt Atau Kilowatt." },
  { "en": "Apa Satuan Daya Reaktif (ETAP)?", "id": "VAR." },
  { "en": "Apa Fungsi Grid (ETAP)?", "id": "Sumber Listrik PLN." },
  { "en": "Apa Fungsi Protective Device Coordination (ETAP)?", "id": "Koordinasi Alat Pengaman." },
  { "en": "Apa Fungsi Lumped Load (ETAP)?", "id": "Beban Terpusat Gabungan." },
  { "en": "Apa Warna Bus Saat De-Energized (ETAP)?", "id": "Warna Abu Abu." },
  { "en": "Apa Fungsi Composite Network (ETAP)?", "id": "Menyederhanakan Diagram Rangkaian." },
  { "en": "Apa Fungsi Star Evaluation (ETAP)?", "id": "Evaluasi Seting Relay." },
  { "en": "GX Works Digunakan Untuk PLC Merk Apa (GX Works)?", "id": "Merk Mitsubishi." },
  { "en": "Bahasa Pemrograman Utama Apa (GX Works)?", "id": "Ladder Diagram." },
  { "en": "Apa Shortcut Mode Write (GX Works)?", "id": "Tombol F2." },
  { "en": "Apa Shortcut Mode Read (GX Works)?", "id": "Shift + F2." },
  { "en": "Apa Shortcut Membuat Kontak Open (GX Works)?", "id": "Tombol F5." },
  { "en": "Apa Shortcut Membuat Kontak Close (GX Works)?", "id": "Tombol F6." },
  { "en": "Apa Shortcut Membuat Coil Output (GX Works)?", "id": "Tombol F7." },
  { "en": "Apa Shortcut Membuat Garis Vertikal (GX Works)?", "id": "Shift + F9." },
  { "en": "Apa Shortcut Membuat Garis Horizontal (GX Works)?", "id": "Tombol F9." },
  { "en": "Apa Fungsi Device Comment (GX Works)?", "id": "Memberi Catatan Alamat." },
  { "en": "Apa Fungsi PLC Diagnostics (GX Works)?", "id": "Diagnosa Error PLC." },
  { "en": "Apa Fungsi Monitor Mode (GX Works)?", "id": "Memantau Status Program." },
  { "en": "Apa Fungsi Simulation Start (GX Works)?", "id": "Memulai Simulasi PLC." },
  { "en": "Apa Instruksi SET (GX Works)?", "id": "Mengaktifkan Bit Permanen." },
  { "en": "Apa Instruksi RST (GX Works)?", "id": "Mematikan Bit." },
  { "en": "Apa Alamat Input Pada PLC Mitsubishi (GX Works)?", "id": "Huruf X." },
  { "en": "Apa Alamat Output Pada PLC Mitsubishi (GX Works)?", "id": "Huruf Y." },
  { "en": "Apa Alamat Internal Relay Mitsubishi (GX Works)?", "id": "Huruf M." },
  { "en": "Apa Fungsi Timer On Delay (GX Works)?", "id": "Tunda Waktu On." },
  { "en": "Apa Fungsi Batch Monitor (GX Works)?", "id": "Memantau Banyak Alamat." },
  { "en": "Apa Fungsi Perintah Rotate (AutoCAD)?", "id": "Memutar Objek Gambar." },
  { "en": "Apa Shortcut Perintah Scale (AutoCAD)?", "id": "Ketik SC + Enter." },
  { "en": "Apa Fungsi Explode (AutoCAD)?", "id": "Memecah Objek Menjadi Garis." },
  { "en": "Apa Fungsi Perintah Join (AutoCAD)?", "id": "Menyambung Garis Terputus." },
  { "en": "Apa Fungsi Layer Properties (AutoCAD)?", "id": "Mengatur Lapisan Gambar." },
  { "en": "Apa Fungsi Hatch (AutoCAD)?", "id": "Memberi Arsiran Bidang." },
  { "en": "Apa Shortcut Membuat Teks (AutoCAD)?", "id": "Ketik T Atau DT." },
  { "en": "Apa Shortcut Save As (AutoCAD)?", "id": "Ctrl + Shift + S." },
  { "en": "Apa Fungsi Perintah Array (AutoCAD)?", "id": "Menggandakan Pola Teratur." },
  { "en": "Apa Shortcut Untuk Plot (AutoCAD)?", "id": "Tekan Ctrl + P." },
  { "en": "Apa Fungsi Units Command (AutoCAD)?", "id": "Mengatur Satuan Gambar." },
  { "en": "Apa Fungsi Tombol F7 (AutoCAD)?", "id": "Menampilkan Grid Layar." },
  { "en": "Apa Fungsi Perintah Pan (AutoCAD)?", "id": "Menggeser Tampilan Layar." },
  { "en": "Apa Fungsi Stretch (AutoCAD)?", "id": "Menarik Objek Gambar." },
  { "en": "Apa Shortcut Perintah Arc (AutoCAD)?", "id": "Ketik A + Enter." },
  { "en": "Apa Shortcut Perintah Ellipse (AutoCAD)?", "id": "Ketik EL + Enter." },
  { "en": "Apa Fungsi Polygon (AutoCAD)?", "id": "Membuat Segi Banyak." },
  { "en": "Berapa Ukuran Tipe Data Integer (Arduino IDE)?", "id": "16 Bit." },
  { "en": "Apa Fungsi Tipe Data Float (Arduino IDE)?", "id": "Menyimpan Bilangan Desimal." },
  { "en": "Apa Fungsi Tipe Data Char (Arduino IDE)?", "id": "Menyimpan 1 Karakter." },
  { "en": "Apa Nilai Tipe Data Boolean (Arduino IDE)?", "id": "True Atau False." },
  { "en": "Apa Fungsi Keyword Const (Arduino IDE)?", "id": "Membuat Nilai Tetap." },
  { "en": "Apa Fungsi Serial Begin (Arduino IDE)?", "id": "Memulai Komunikasi Serial." },
  { "en": "Berapa Baud Rate Standar (Arduino IDE)?", "id": "9600 bps." },
  { "en": "Apa Simbol Pin PWM (Arduino IDE)?", "id": "Tanda Gelombang Cacing." },
  { "en": "Apa Fungsi Pin TX (Arduino IDE)?", "id": "Mengirim Data Serial." },
  { "en": "Apa Fungsi Pin RX (Arduino IDE)?", "id": "Menerima Data Serial." },
  { "en": "Apa Fungsi Syntax Include (Arduino IDE)?", "id": "Memasukkan Library Luar." },
  { "en": "Berapa Nilai Konstanta High (Arduino IDE)?", "id": "1 Atau 5 Volt." },
  { "en": "Berapa Nilai Konstanta Low (Arduino IDE)?", "id": "0 Atau Ground." },
  { "en": "Apa Simbol Komentar Satu Baris (Arduino IDE)?", "id": "2 Garis Miring." },
  { "en": "Apa Fungsi If Statement (Arduino IDE)?", "id": "Pengkondisian Logika Program." },
  { "en": "Apa Fungsi For Loop (Arduino IDE)?", "id": "Perulangan Dengan Batasan." },
  { "en": "Apa Fungsi Instruksi Keep (CX Programmer)?", "id": "Menahan Status Bit." },
  { "en": "Instruksi Counter Membutuhkan Input Apa (CX Programmer)?", "id": "Input Sinyal Reset." },
  { "en": "Berapa Satuan Waktu Timer (CX Programmer)?", "id": "100 ms." },
  { "en": "Apa Fungsi Area CIO (CX Programmer)?", "id": "Area Memori Input Output." },
  { "en": "Apa Fungsi Holding Relay (CX Programmer)?", "id": "Menyimpan Data Saat Mati." },
  { "en": "Apa Fungsi Auxiliary Relay (CX Programmer)?", "id": "Status Sistem PLC." },
  { "en": "Apa Fungsi Data Memory (CX Programmer)?", "id": "Menyimpan Data Angka." },
  { "en": "Apa Fungsi Instruksi Compare (CX Programmer)?", "id": "Membandingkan 2 Data." },
  { "en": "Apa Itu Variabel Global (CX Programmer)?", "id": "Variabel Semua Program." },
  { "en": "Apa Itu Variabel Lokal (CX Programmer)?", "id": "Variabel 1 Program." },
  { "en": "Bagaimana Cara Insert Row (CX Programmer)?", "id": "Klik Kanan Insert Row." },
  { "en": "Apa Arti Upload From PLC (CX Programmer)?", "id": "Mengambil Program Dari PLC." },
  { "en": "Apa Arti Download To PLC (CX Programmer)?", "id": "Mengirim Program Ke PLC." },
  { "en": "Apa Fungsi Force On (CX Programmer)?", "id": "Memaksa Bit Aktif." },
  { "en": "Apa Fungsi Force Off (CX Programmer)?", "id": "Memaksa Bit Mati." },
  { "en": "Apa Fungsi Section (CX Programmer)?", "id": "Membagi Blok Program." },
  { "en": "Apa Fungsi Komponen 7 Segment (Proteus)?", "id": "Menampilkan Angka Desimal." },
  { "en": "Apa Kode Pencarian Resistor (Proteus)?", "id": "Ketik RES." },
  { "en": "Apa Kode Pencarian Kapasitor (Proteus)?", "id": "Ketik CAP." },
  { "en": "Apa Kode Pencarian Tombol (Proteus)?", "id": "Ketik Button." },
  { "en": "Apa Fungsi Logic State (Proteus)?", "id": "Memberi Logika Input." },
  { "en": "Apa Fungsi Logic Probe (Proteus)?", "id": "Mengecek Logika Pin." },
  { "en": "Apa Fungsi PCB Layout (Proteus)?", "id": "Desain Papan Sirkuit." },
  { "en": "Apa Fungsi Autorouter (Proteus)?", "id": "Membuat Jalur Otomatis." },
  { "en": "Apa Fungsi 3D Visualizer (Proteus)?", "id": "Melihat Bentuk Asli PCB." },
  { "en": "Apa Fungsi Mirror X (Proteus)?", "id": "Mencerminkan Secara Horizontal." },
  { "en": "Apa Fungsi Mirror Y (Proteus)?", "id": "Mencerminkan Secara Vertikal." },
  { "en": "Apa Fungsi Rotate Clockwise (Proteus)?", "id": "Putar Arah Jarum Jam." },
  { "en": "Ikon Apa Untuk Mode Komponen (Proteus)?", "id": "Ikon Op Amp Segitiga." },
  { "en": "Ikon Apa Untuk Mode Terminal (Proteus)?", "id": "Ikon 2 Terminal." },
  { "en": "Apa Fungsi Power Rail (Proteus)?", "id": "Jalur Sumber Daya." },
  { "en": "Apa Ekstensi File Proyek (Proteus)?", "id": "DSN Atau PDSJ." },
  { "en": "Apa Fungsi Motor Starting Analysis (ETAP)?", "id": "Analisis Asut Motor." },
  { "en": "Apa Fungsi Harmonic Analysis (ETAP)?", "id": "Analisis Distorsi Gelombang." },
  { "en": "Apa Fungsi Transient Stability Analysis (ETAP)?", "id": "Analisis Kestabilan Transien." },
  { "en": "Apa Fungsi Circuit Breaker (ETAP)?", "id": "Pemutus Arus Beban Lebih." },
  { "en": "Apa Simbol Fuse (ETAP)?", "id": "Garis Bergelombang." },
  { "en": "Apa Fungsi Current Transformer (ETAP)?", "id": "Menurunkan Arus Ukur." },
  { "en": "Apa Fungsi Potential Transformer (ETAP)?", "id": "Menurunkan Tegangan Ukur." },
  { "en": "Apa Fungsi Alert View (ETAP)?", "id": "Menampilkan Daftar Peringatan." },
  { "en": "Apa Itu Single Line Diagram (ETAP)?", "id": "Diagram 1 Garis." },
  { "en": "Apa Satuan Rating Busbar (ETAP)?", "id": "Ampere Dan Kilovolt." },
  { "en": "Apa Satuan Impedansi Pada Kabel (ETAP)?", "id": "Ohm Atau Persen." },
  { "en": "Berapa Power Factor Standar (ETAP)?", "id": "0,85." },
  { "en": "Berapa Frekuensi Standar Indonesia (ETAP)?", "id": "50 Hz." },
  { "en": "Berapa Sudut Tegangan Swing Bus (ETAP)?", "id": "0 Derajat." },
  { "en": "Berapa Batas Voltage Drop Standar (ETAP)?", "id": "Maksimal 5 Persen." },
  { "en": "Apa Elemen Alternating Current (ETAP)?", "id": "Elemen Arus Bolak Balik." },
  { "en": "Apa Elemen Direct Current (ETAP)?", "id": "Elemen Arus Searah." },
  { "en": "Apa Instruksi Load Pulse (GX Works)?", "id": "Deteksi Sisi Naik Awal." },
  { "en": "Apa Instruksi Load Falling (GX Works)?", "id": "Deteksi Sisi Turun Awal." },
  { "en": "Apa Instruksi Pulse (GX Works)?", "id": "Output 1 Siklus Naik." },
  { "en": "Apa Instruksi Pulse Falling (GX Works)?", "id": "Output 1 Siklus Turun." },
  { "en": "Apa Fungsi Master Control (GX Works)?", "id": "Kontrol Utama Program." },
  { "en": "Apa Fungsi Master Control Reset (GX Works)?", "id": "Reset Kontrol Utama." },
  { "en": "Apa Fungsi Instruksi Alternate (GX Works)?", "id": "Mengubah Status On Off." },
  { "en": "Apa Kode Timer 100ms (GX Works)?", "id": "Kode T." },
  { "en": "Apa Kode Counter 16 Bit (GX Works)?", "id": "Kode C." },
  { "en": "Apa Kode Data Register (GX Works)?", "id": "Huruf D." },
  { "en": "Apa Kode File Register (GX Works)?", "id": "Huruf R." },
  { "en": "Apa Kode Link Relay (GX Works)?", "id": "Huruf B." },
  { "en": "Apa Kode Link Register (GX Works)?", "id": "Huruf W." },
  { "en": "Apa Shortcut Menampilkan Komentar (GX Works)?", "id": "Ctrl + F5." },
  { "en": "Apa Shortcut Zoom In (GX Works)?", "id": "Ctrl + Scroll Atas." },
  { "en": "Apa Shortcut Zoom Out (GX Works)?", "id": "Ctrl + Scroll Bawah." },
  { "en": "Apa Fungsi Perintah Pline (AutoCAD)?", "id": "Membuat Garis Bersambung Satu Objek." },
  { "en": "Apa Fungsi Perintah Spline (AutoCAD)?", "id": "Membuat Garis Melengkung Halus." },
  { "en": "Apa Shortcut Membuat File Baru (AutoCAD)?", "id": "Tekan Ctrl + N." },
  { "en": "Apa Shortcut Membuka File (AutoCAD)?", "id": "Tekan Ctrl + O." },
  { "en": "Apa Fungsi Tombol F9 (AutoCAD)?", "id": "Mengaktifkan Snap Mode." },
  { "en": "Apa Fungsi Perintah Area (AutoCAD)?", "id": "Menghitung Luas Area Tertutup." },
  { "en": "Apa Fungsi Perintah Break (AutoCAD)?", "id": "Memutus Garis Di 2 Titik." },
  { "en": "Apa Fungsi Perintah Extend (AutoCAD)?", "id": "Memanjangkan Garis Ke Batas." },
  { "en": "Apa Fungsi Perintah Regen (AutoCAD)?", "id": "Menyegarkan Tampilan Layar." },
  { "en": "Apa Fungsi Perintah Divide (AutoCAD)?", "id": "Membagi Objek Sama Rata." },
  { "en": "Apa Fungsi Perintah Measure (AutoCAD)?", "id": "Mengukur Jarak Tertentu." },
  { "en": "Apa Fungsi Perintah Gradient (AutoCAD)?", "id": "Memberi Warna Gradasi." },
  { "en": "Apa Fungsi Perintah Wblock (AutoCAD)?", "id": "Menyimpan Blok Ke File." },
  { "en": "Apa Fungsi Perintah Group (AutoCAD)?", "id": "Mengelompokkan Objek Sementara." },
  { "en": "Apa Fungsi Perintah Ungroup (AutoCAD)?", "id": "Memisahkan Kelompok Objek." },
  { "en": "Apa Fungsi Perintah Distance (AutoCAD)?", "id": "Mengukur Jarak Antara 2 Titik." },
  { "en": "Apa Fungsi Mtext (AutoCAD)?", "id": "Membuat Teks Paragraf." },
  { "en": "Apa Fungsi Fungsi Millis (Arduino IDE)?", "id": "Waktu Sejak Program Jalan." },
  { "en": "Apa Fungsi Fungsi Micros (Arduino IDE)?", "id": "Waktu Dalam Satuan Mikrosekon." },
  { "en": "Apa Fungsi Fungsi Random (Arduino IDE)?", "id": "Menghasilkan Angka Acak." },
  { "en": "Apa Fungsi Fungsi Abs (Arduino IDE)?", "id": "Menghitung Nilai Mutlak." },
  { "en": "Apa Fungsi Fungsi Min (Arduino IDE)?", "id": "Mencari Nilai Terkecil." },
  { "en": "Apa Fungsi Fungsi Max (Arduino IDE)?", "id": "Mencari Nilai Terbesar." },
  { "en": "Apa Fungsi Fungsi Sqrt (Arduino IDE)?", "id": "Menghitung Akar Kuadrat." },
  { "en": "Apa Fungsi Fungsi Pow (Arduino IDE)?", "id": "Menghitung Pangkat Bilangan." },
  { "en": "Apa Fungsi Fungsi Map (Arduino IDE)?", "id": "Memetakan Rentang Nilai." },
  { "en": "Apa Fungsi Fungsi Constrain (Arduino IDE)?", "id": "Membatasi Rentang Nilai." },
  { "en": "Apa Beda Print Dan Println (Arduino IDE)?", "id": "Println Menambah Baris Baru." },
  { "en": "Apa Fungsi AnalogReference (Arduino IDE)?", "id": "Mengatur Tegangan Referensi." },
  { "en": "Apa Fungsi NoTone (Arduino IDE)?", "id": "Mematikan Suara Buzzer." },
  { "en": "Apa Fungsi Tone (Arduino IDE)?", "id": "Menghasilkan Frekuensi Suara." },
  { "en": "Apa Fungsi ShiftOut (Arduino IDE)?", "id": "Mengirim Data Bit Berurutan." },
  { "en": "Apa Instruksi Jump (CX Programmer)?", "id": "Melompati Bagian Program." },
  { "en": "Apa Instruksi Jump End (CX Programmer)?", "id": "Penanda Akhir Lompatan." },
  { "en": "Apa Instruksi Interlock (CX Programmer)?", "id": "Mengunci Bagian Program." },
  { "en": "Apa Instruksi Interlock Clear (CX Programmer)?", "id": "Akhir Penguncian Program." },
  { "en": "Apa Instruksi Set Stack (CX Programmer)?", "id": "Mengatur Stack Memori." },
  { "en": "Apa Instruksi TIMH (CX Programmer)?", "id": "Timer Kecepatan Tinggi." },
  { "en": "Apa Shortcut Find (CX Programmer)?", "id": "Tekan Ctrl + F." },
  { "en": "Apa Shortcut Replace (CX Programmer)?", "id": "Tekan Ctrl + R." },
  { "en": "Apa Fungsi Simbol P_On (CX Programmer)?", "id": "Bit Selalu Hidup." },
  { "en": "Apa Fungsi Simbol P_Off (CX Programmer)?", "id": "Bit Selalu Mati." },
  { "en": "Apa Fungsi Simbol P_1s (CX Programmer)?", "id": "Pulsa Detak 1 Detik." },
  { "en": "Apa Fungsi Simbol P_First_Cycle (CX Programmer)?", "id": "Aktif Saat Start Awal." },
  { "en": "Apa Fungsi Work Area (CX Programmer)?", "id": "Memori Internal Sementara." },
  { "en": "Apa Instruksi Shift Register (CX Programmer)?", "id": "Menggeser Bit Data." },
  { "en": "Apa Instruksi Subroutine Entry (CX Programmer)?", "id": "Memanggil Sub Program." },
  { "en": "Apa Fungsi Pick Devices (Proteus)?", "id": "Memilih Komponen Baru." },
  { "en": "Apa Fungsi Terminal Mode (Proteus)?", "id": "Menampilkan Port Koneksi." },
  { "en": "Apa Fungsi Graph Mode (Proteus)?", "id": "Membuat Grafik Simulasi." },
  { "en": "Apa Fungsi Decompose (Proteus)?", "id": "Memecah Komponen Jadi Simbol." },
  { "en": "Apa Fungsi Auto Arranger (Proteus)?", "id": "Merapikan Posisi Komponen." },
  { "en": "Apa Fungsi Netlist (Proteus)?", "id": "Daftar Koneksi Rangkaian." },
  { "en": "Apa Fungsi Bill Of Materials (Proteus)?", "id": "Daftar Kebutuhan Komponen." },
  { "en": "Apa Fungsi Electrical Rule Check (Proteus)?", "id": "Memeriksa Aturan Listrik." },
  { "en": "Apa Fungsi Design Rule Check (Proteus)?", "id": "Memeriksa Desain PCB." },
  { "en": "Apa Fungsi Zone Mode (Proteus)?", "id": "Membuat Area Tembaga." },
  { "en": "Apa Fungsi Ratnest Mode (Proteus)?", "id": "Melihat Jalur Belum Terhubung." },
  { "en": "Apa Fungsi Pad Mode (Proteus)?", "id": "Menambah Pad Solder." },
  { "en": "Apa Fungsi Track Mode (Proteus)?", "id": "Membuat Jalur PCB." },
  { "en": "Apa Fungsi Via Mode (Proteus)?", "id": "Membuat Lubang Tembus." },
  { "en": "Apa Fungsi Project Merge (ETAP)?", "id": "Menggabungkan 2 Proyek." },
  { "en": "Apa Fungsi Data Manager (ETAP)?", "id": "Mengelola Database Proyek." },
  { "en": "Apa Fungsi Library Manager (ETAP)?", "id": "Mengelola Data Komponen." },
  { "en": "Apa Fungsi Cable Sizing (ETAP)?", "id": "Menentukan Ukuran Kabel." },
  { "en": "Apa Fungsi Transformer Sizing (ETAP)?", "id": "Menentukan Ukuran Trafo." },
  { "en": "Apa Fungsi Ground Grid Analysis (ETAP)?", "id": "Analisis Grid Pembumian." },
  { "en": "Apa Fungsi Battery Sizing (ETAP)?", "id": "Menghitung Kapasitas Baterai." },
  { "en": "Apa Fungsi Reliability Analysis (ETAP)?", "id": "Analisis Keandalan Sistem." },
  { "en": "Apa Fungsi Optimal Power Flow (ETAP)?", "id": "Aliran Daya Optimal." },
  { "en": "Apa Fungsi Voltage Drop (ETAP)?", "id": "Jatuh Tegangan Saluran." },
  { "en": "Apa Fungsi Relay Coordination (ETAP)?", "id": "Koordinasi Proteksi Relay." },
  { "en": "Apa Fungsi Sequence Of Operation (ETAP)?", "id": "Urutan Operasi Logika." },
  { "en": "Apa Fungsi Unlimited Bus (ETAP)?", "id": "Bus Tak Terbatas." },
  { "en": "Apa Fungsi Static Load (ETAP)?", "id": "Beban Statis Tetap." },
  { "en": "Apa Fungsi Capacitor Bank (ETAP)?", "id": "Memperbaiki Faktor Daya." },
  { "en": "Apa Fungsi DC Load Flow (ETAP)?", "id": "Aliran Daya DC." },
  { "en": "Apa Fungsi DC Short Circuit (ETAP)?", "id": "Hubung Singkat DC." },
  { "en": "Apa Fungsi Tombol F4 (GX Works)?", "id": "Kompilasi Program Ladder." },
  { "en": "Apa Shortcut Copy (GX Works)?", "id": "Tekan Ctrl + C." },
  { "en": "Apa Shortcut Paste (GX Works)?", "id": "Tekan Ctrl + V." },
  { "en": "Apa Instruksi Conditional Jump (GX Works)?", "id": "Lompat Jika Syarat Penuh." },
  { "en": "Apa Instruksi CALL (GX Works)?", "id": "Memanggil Subroutine." },
  { "en": "Apa Instruksi Subroutine Return (GX Works)?", "id": "Kembali Dari Subroutine." },
  { "en": "Apa Instruksi First End (GX Works)?", "id": "Akhir Program Utama." },
  { "en": "Apa Instruksi Watchdog Timer (GX Works)?", "id": "Pengawas Waktu Sistem." },
  { "en": "Apa Instruksi Bit Reset (GX Works)?", "id": "Reset Bit Word." },
  { "en": "Apa Instruksi Enable Interrupt (GX Works)?", "id": "Mengizinkan Interupsi." },
  { "en": "Apa Instruksi Disable Interrupt (GX Works)?", "id": "Melarang Interupsi." },
  { "en": "Apa Instruksi Interrupt Return (GX Works)?", "id": "Kembali Dari Interupsi." },
  { "en": "Apa Fungsi File Register (GX Works)?", "id": "Register File Zona." },
  { "en": "Apa Fungsi Latch Relay (GX Works)?", "id": "Relay Tahan Posisi." },
  { "en": "Apa Fungsi Special Relay (GX Works)?", "id": "Relay Khusus Sistem." },
  { "en": "Apa Fungsi Special Register (GX Works)?", "id": "Register Khusus Sistem." },
  { "en": "Apa Fungsi Link Relay (GX Works)?", "id": "Relay Komunikasi Network." },
  { "en": "Apa Shortcut Mencari Kontak (GX Works)?", "id": "Tekan Ctrl + F." },
  { "en": "Apa Fungsi Comment Display (GX Works)?", "id": "Menampilkan Deskripsi Alamat." },
  { "en": "Apa Fungsi Cross Reference (GX Works)?", "id": "Melacak Penggunaan Alamat." },
  { "en": "Apa Fungsi Construction Line (AutoCAD)?", "id": "Membuat Garis Bantu Tak Terbatas." },
  { "en": "Apa Fungsi Perintah Donut (AutoCAD)?", "id": "Membuat Lingkaran Berisi Padat." },
  { "en": "Apa Shortcut Membuka Properties (AutoCAD)?", "id": "Tekan Ctrl + 1." },
  { "en": "Apa Shortcut Membuka Design Center (AutoCAD)?", "id": "Tekan Ctrl + 2." },
  { "en": "Apa Fungsi Match Properties (AutoCAD)?", "id": "Menyamakan Sifat Objek Gambar." },
  { "en": "Apa Fungsi Perintah Purge (AutoCAD)?", "id": "Menghapus Item Tidak Terpakai." },
  { "en": "Apa Fungsi Model Space (AutoCAD)?", "id": "Ruang Untuk Menggambar Objek." },
  { "en": "Apa Fungsi Layout Space (AutoCAD)?", "id": "Ruang Untuk Mengatur Cetakan." },
  { "en": "Apa Fungsi Snap Endpoint (AutoCAD)?", "id": "Menangkap Ujung Garis." },
  { "en": "Apa Fungsi Snap Midpoint (AutoCAD)?", "id": "Menangkap Titik Tengah Garis." },
  { "en": "Apa Fungsi Perintah Revision Cloud (AutoCAD)?", "id": "Memberi Tanda Revisi Gambar." },
  { "en": "Apa Fungsi Perintah Helix (AutoCAD)?", "id": "Membuat Objek Spiral 3D." },
  { "en": "Apa Shortcut Toggle Command Line (AutoCAD)?", "id": "Tekan Ctrl + 9." },
  { "en": "Apa Fungsi Perintah Wipeout (AutoCAD)?", "id": "Menutupi Area Gambar." },
  { "en": "Apa Fungsi Perintah Spell (AutoCAD)?", "id": "Mengecek Ejaan Teks." },
  { "en": "Apa Fungsi Quick Select (AutoCAD)?", "id": "Memilih Objek Berdasarkan Kriteria." },
  { "en": "Apa Fungsi Perintah Rename (AutoCAD)?", "id": "Mengubah Nama Blok." },
  { "en": "Apa Fungsi Switch Case (Arduino IDE)?", "id": "Percabangan Banyak Kondisi." },
  { "en": "Apa Fungsi While Loop (Arduino IDE)?", "id": "Perulangan Selama Syarat Benar." },
  { "en": "Apa Fungsi Break Dalam Loop (Arduino IDE)?", "id": "Menghentikan Perulangan Paksa." },
  { "en": "Apa Fungsi Continue Dalam Loop (Arduino IDE)?", "id": "Melanjutkan Iterasi Berikutnya." },
  { "en": "Apa Fungsi Return Dalam Fungsi (Arduino IDE)?", "id": "Mengembalikan Nilai Fungsi." },
  { "en": "Apa Fungsi PulseIn (Arduino IDE)?", "id": "Membaca Durasi Pulsa." },
  { "en": "Apa Fungsi AttachInterrupt (Arduino IDE)?", "id": "Menjalankan Fungsi Saat Interupsi." },
  { "en": "Apa Library Untuk Motor Servo (Arduino IDE)?", "id": "Library Servo.h." },
  { "en": "Apa Library Untuk Layar LCD (Arduino IDE)?", "id": "Library LiquidCrystal.h." },
  { "en": "Apa Fungsi EEPROM (Arduino IDE)?", "id": "Menyimpan Data Permanen." },
  { "en": "Apa Fungsi Wire Library (Arduino IDE)?", "id": "Komunikasi I2C." },
  { "en": "Apa Fungsi SPI (Arduino IDE)?", "id": "Komunikasi Serial Sinkron." },
  { "en": "Apa Fungsi SoftwareSerial (Arduino IDE)?", "id": "Membuat Port Serial Virtual." },
  { "en": "Apa Simbol Operator Logika AND (Arduino IDE)?", "id": "Simbol &&." },
  { "en": "Apa Simbol Operator Logika OR (Arduino IDE)?", "id": "Simbol ||." },
  { "en": "Apa Simbol Operator Logika NOT (Arduino IDE)?", "id": "Tanda Seru (!)." },
  { "en": "Apa Fungsi Instruksi ADD (CX Programmer)?", "id": "Menjumlahkan Dua Data." },
  { "en": "Apa Fungsi Instruksi SUB (CX Programmer)?", "id": "Mengurangkan Dua Data." },
  { "en": "Apa Fungsi Instruksi Multiply (CX Programmer)?", "id": "Mengalikan Dua Data." },
  { "en": "Apa Fungsi Instruksi Divide (CX Programmer)?", "id": "Membagi Dua Data." },
  { "en": "Apa Fungsi Instruksi Equal (CX Programmer)?", "id": "Membandingkan Kesamaan Data." },
  { "en": "Apa Fungsi Instruksi Greater Than (CX Programmer)?", "id": "Membandingkan Lebih Besar." },
  { "en": "Apa Fungsi Instruksi Less Than (CX Programmer)?", "id": "Membandingkan Lebih Kecil." },
  { "en": "Apa Fungsi Simbol Increment (CX Programmer)?", "id": "Menambah Nilai 1." },
  { "en": "Apa Fungsi Simbol Decrement (CX Programmer)?", "id": "Mengurang Nilai 1." },
  { "en": "Apa Fungsi Instruksi BCD (CX Programmer)?", "id": "Konversi Biner Ke Desimal." },
  { "en": "Apa Fungsi Instruksi Binary (CX Programmer)?", "id": "Konversi Desimal Ke Biner." },
  { "en": "Apa Fungsi Rung Comment (CX Programmer)?", "id": "Memberi Keterangan Baris Program." },
  { "en": "Apa Fungsi Symbol Table (CX Programmer)?", "id": "Daftar Nama Alamat I/O." },
  { "en": "Apa Fungsi Watch Window (CX Programmer)?", "id": "Memantau Nilai Alamat Tertentu." },
  { "en": "Apa Fungsi PLC Memory Utility (CX Programmer)?", "id": "Mengelola Memori PLC." },
  { "en": "Apa Fungsi Compare Programs (CX Programmer)?", "id": "Membandingkan 2 File Program." },
  { "en": "Apa Fungsi Option Board Settings (CX Programmer)?", "id": "Mengatur Modul Tambahan." },
  { "en": "Apa Fungsi Subcircuit Mode (Proteus)?", "id": "Membuat Rangkaian Bertingkat." },
  { "en": "Apa Fungsi Block Copy (Proteus)?", "id": "Menyalin Sekelompok Komponen." },
  { "en": "Apa Fungsi Block Move (Proteus)?", "id": "Memindahkan Sekelompok Komponen." },
  { "en": "Apa Fungsi X-Cursor (Proteus)?", "id": "Kursor Bentuk Silang Besar." },
  { "en": "Apa Fungsi Set Origin (Proteus)?", "id": "Menentukan Titik Nol Koordinat." },
  { "en": "Apa Fungsi Snap 0.1in (Proteus)?", "id": "Mengatur Jarak Grid Standar." },
  { "en": "Apa Fungsi Grid Size (Proteus)?", "id": "Mengubah Ukuran Kotak Bantuan." },
  { "en": "Apa Fungsi Signal Generator (Proteus)?", "id": "Pembangkit Sinyal Gelombang." },
  { "en": "Apa Fungsi Logic Analyser (Proteus)?", "id": "Menganalisis Banyak Sinyal Digital." },
  { "en": "Apa Fungsi I2C Debugger (Proteus)?", "id": "Debugging Komunikasi I2C." },
  { "en": "Apa Fungsi SPI Debugger (Proteus)?", "id": "Debugging Komunikasi SPI." },
  { "en": "Apa Fungsi Komponen Value (Proteus)?", "id": "Mengubah Nilai Komponen." },
  { "en": "Apa Fungsi Edit Properties (Proteus)?", "id": "Mengedit Parameter Komponen." },
  { "en": "Apa Fungsi Metric Imperial Toggle (Proteus)?", "id": "Mengubah Satuan Ukuran." },
  { "en": "Apa Fungsi Hidden Pins Mode (Proteus)?", "id": "Menampilkan Pin Tersembunyi." },
  { "en": "Apa Fungsi Autosave (Proteus)?", "id": "Menyimpan Otomatis Berkala." },
  { "en": "Apa Fungsi Arc Flash Analysis (ETAP)?", "id": "Analisis Bahaya Kilat Busur." },
  { "en": "Apa Fungsi Scenario Wizard (ETAP)?", "id": "Membuat Skenario Operasi Berbeda." },
  { "en": "Apa Fungsi Study Case (ETAP)?", "id": "Mengatur Parameter Simulasi." },
  { "en": "Apa Fungsi Output Report (ETAP)?", "id": "Laporan Hasil Analisis." },
  { "en": "Apa Fungsi One Line View (ETAP)?", "id": "Tampilan Diagram 1 Garis." },
  { "en": "Apa Fungsi Theme Manager (ETAP)?", "id": "Mengatur Tampilan Warna Diagram." },
  { "en": "Apa Fungsi Inverter (ETAP)?", "id": "Mengubah DC Menjadi AC." },
  { "en": "Apa Fungsi VFD (ETAP)?", "id": "Mengatur Kecepatan Motor." },
  { "en": "Apa Fungsi UPS (ETAP)?", "id": "Cadangan Daya Sementara." },
  { "en": "Apa Fungsi Solar Panel (ETAP)?", "id": "Sumber Listrik Tenaga Surya." },
  { "en": "Apa Fungsi Wind Turbine (ETAP)?", "id": "Sumber Listrik Tenaga Angin." },
  { "en": "Apa Fungsi Exciter Generator (ETAP)?", "id": "Memberi Arus Penguat Medan." },
  { "en": "Apa Fungsi Governor Generator (ETAP)?", "id": "Mengatur Putaran Mesin." },
  { "en": "Apa Fungsi Sync Check Relay (ETAP)?", "id": "Cek Syarat Sinkronisasi." },
  { "en": "Apa Fungsi Phase Adapter (ETAP)?", "id": "Menyesuaikan Koneksi Fasa." },
  { "en": "Apa Fungsi Earthing Adapter (ETAP)?", "id": "Koneksi Ke Tanah." },
  { "en": "Apa Satuan Kapasitas Baterai (ETAP)?", "id": "Ampere Hour." },
  { "en": "Apa Fungsi Statement List (GX Works)?", "id": "Pemrograman Berbasis Teks." },
  { "en": "Apa Fungsi Structured Ladder (GX Works)?", "id": "Ladder Dengan Struktur Blok." },
  { "en": "Apa Fungsi Function Block (GX Works)?", "id": "Blok Fungsi Digunakan Ulang." },
  { "en": "Apa Fungsi Label Editor (GX Works)?", "id": "Mengedit Nama Variabel." },
  { "en": "Apa Fungsi Parameter Setup PLC (GX Works)?", "id": "Mengatur Hardware PLC." },
  { "en": "Apa Fungsi Verify With PLC (GX Works)?", "id": "Mencocokkan Program PC PLC." },
  { "en": "Apa Fungsi Online Change (GX Works)?", "id": "Edit Program Saat PLC Jalan." },
  { "en": "Apa Fungsi Watch Window (GX Works)?", "id": "Memantau Data Realtime." },
  { "en": "Apa Fungsi Device Memory Monitor (GX Works)?", "id": "Melihat Isi Memori PLC." },
  { "en": "Apa Fungsi Buffer Memory Monitor (GX Works)?", "id": "Memori Modul Cerdas." },
  { "en": "Apa Fungsi Intelligent Module Monitor (GX Works)?", "id": "Pantau Modul Khusus." },
  { "en": "Apa Fungsi Connection Destination (GX Works)?", "id": "Mengatur Koneksi Kabel PLC." },
  { "en": "Apa Fungsi Undo (GX Works)?", "id": "Membatalkan Perubahan Terakhir." },
  { "en": "Apa Fungsi Redo (GX Works)?", "id": "Mengulang Perubahan Dibatalkan." },
  { "en": "Apa Fungsi Instruction Help (GX Works)?", "id": "Bantuan Penjelasan Instruksi." },
  { "en": "Apa Shortcut Insert Line (GX Works)?", "id": "Tekan Shift + Insert." },
  { "en": "Apa Shortcut Delete Line (GX Works)?", "id": "Tekan Shift + Delete." },
  { "en": "Apa Fungsi Perintah Block (AutoCAD)?", "id": "Menyatukan Objek Menjadi Satu." },
  { "en": "Apa Fungsi Perintah Insert Block (AutoCAD)?", "id": "Memasukkan Blok Ke Gambar." },
  { "en": "Apa Fungsi Attributes Blok (AutoCAD)?", "id": "Menyimpan Data Teks Blok." },
  { "en": "Apa Fungsi External Reference (AutoCAD)?", "id": "Menampilkan Gambar File Lain." },
  { "en": "Apa Fungsi Viewport Layout (AutoCAD)?", "id": "Jendela Tampilan Gambar Model." },
  { "en": "Apa Shortcut Membuka Layer Manager (AutoCAD)?", "id": "Ketik LA + Enter." },
  { "en": "Apa Fungsi Isolate Object (AutoCAD)?", "id": "Menyembunyikan Objek Tidak Terpilih." },
  { "en": "Apa Fungsi Hide Object (AutoCAD)?", "id": "Menyembunyikan Objek Terpilih." },
  { "en": "Apa Fungsi Perintah Overkill (AutoCAD)?", "id": "Menghapus Garis Tumpuk Ganda." },
  { "en": "Apa Fungsi Quick Properties (AutoCAD)?", "id": "Info Singkat Saat Kursor Diam." },
  { "en": "Apa Fungsi Multileader (AutoCAD)?", "id": "Garis Penunjuk Dengan Teks." },
  { "en": "Apa Fungsi Table Command (AutoCAD)?", "id": "Membuat Tabel Data Baris Kolom." },
  { "en": "Apa Fungsi Design Center (AutoCAD)?", "id": "Mengambil Konten File Lain." },
  { "en": "Apa Shortcut Paste As Block (AutoCAD)?", "id": "Ctrl + Shift + V." },
  { "en": "Apa Fungsi Command Alias Editor (AutoCAD)?", "id": "Mengubah Shortcut Perintah." },
  { "en": "Apa Fungsi Drawing Recovery Manager (AutoCAD)?", "id": "Memulihkan File Setelah Crash." },
  { "en": "Apa Fungsi Operator Modulo (Arduino IDE)?", "id": "Mencari Sisa Bagi." },
  { "en": "Apa Fungsi BitRead (Arduino IDE)?", "id": "Membaca Status Bit Tertentu." },
  { "en": "Apa Fungsi BitWrite (Arduino IDE)?", "id": "Menulis Nilai Bit Tertentu." },
  { "en": "Apa Fungsi BitSet (Arduino IDE)?", "id": "Mengubah Bit Menjadi 1." },
  { "en": "Apa Fungsi BitClear (Arduino IDE)?", "id": "Mengubah Bit Menjadi 0." },
  { "en": "Apa Fungsi Keyword Volatile (Arduino IDE)?", "id": "Variabel Untuk Interupsi." },
  { "en": "Apa Fungsi Keyword Static (Arduino IDE)?", "id": "Nilai Variabel Tetap Tersimpan." },
  { "en": "Apa Fungsi Tipe Data Unsigned Int (Arduino IDE)?", "id": "Menyimpan Angka Positif Saja." },
  { "en": "Apa Fungsi Tipe Data Long (Arduino IDE)?", "id": "Menyimpan Angka Integer Besar." },
  { "en": "Apa Fungsi Tipe Data Double (Arduino IDE)?", "id": "Bilangan Desimal Presisi Ganda." },
  { "en": "Apa Fungsi String Object (Arduino IDE)?", "id": "Memanipulasi Data Teks." },
  { "en": "Apa Fungsi ToInt Pada String (Arduino IDE)?", "id": "Mengubah String Ke Integer." },
  { "en": "Apa Fungsi ToFloat Pada String (Arduino IDE)?", "id": "Mengubah String Ke Float." },
  { "en": "Apa Fungsi Substring Pada String (Arduino IDE)?", "id": "Mengambil Bagian Teks." },
  { "en": "Apa Fungsi Instruksi Floating (CX Programmer)?", "id": "Konversi Integer Ke Float." },
  { "en": "Apa Fungsi Instruksi Fix Float (CX Programmer)?", "id": "Konversi Float Ke Integer." },
  { "en": "Apa Fungsi Instruksi Block Transfer (CX Programmer)?", "id": "Menyalin Banyak Data Memori." },
  { "en": "Apa Fungsi Instruksi Block Set (CX Programmer)?", "id": "Mengisi Memori Dengan Nilai Sama." },
  { "en": "Apa Fungsi Instruksi Distribution (CX Programmer)?", "id": "Mendistribusikan Data Ke Stack." },
  { "en": "Apa Fungsi Instruksi Data Collect (CX Programmer)?", "id": "Mengambil Data Dari Stack." },
  { "en": "Apa Fungsi Instruksi Square Root (CX Programmer)?", "id": "Menghitung Akar Kuadrat." },
  { "en": "Apa Fungsi Instruksi Negation (CX Programmer)?", "id": "Mengubah Tanda Positif Negatif." },
  { "en": "Apa Simbol Kontak Rising Edge (CX Programmer)?", "id": "Garis Vertikal Panah Atas." },
  { "en": "Apa Simbol Kontak Falling Edge (CX Programmer)?", "id": "Garis Vertikal Panah Bawah." },
  { "en": "Apa Fungsi Clock Pulse 1 Detik (CX Programmer)?", "id": "Sinyal Hidup Mati Per Detik." },
  { "en": "Apa Fungsi Clock Pulse 0.02 Detik (CX Programmer)?", "id": "Sinyal Cepat 0,02 Detik." },
  { "en": "Apa Fungsi Trace Memory (CX Programmer)?", "id": "Merekam Riwayat Eksekusi." },
  { "en": "Apa Fungsi PLC Setup (CX Programmer)?", "id": "Konfigurasi Hardware PLC." },
  { "en": "Apa Fungsi IO Table (CX Programmer)?", "id": "Mapping Modul Input Output." },
  { "en": "Apa Fungsi Component Mode (Proteus)?", "id": "Memilih Komponen Elektronika." },
  { "en": "Apa Fungsi Junction Dot Mode (Proteus)?", "id": "Membuat Titik Sambung Kabel." },
  { "en": "Apa Fungsi Wire Auto Router (Proteus)?", "id": "Merutekan Kabel Otomatis." },
  { "en": "Apa Fungsi Scripting Mode (Proteus)?", "id": "Menulis Skrip Python." },
  { "en": "Apa Fungsi Current Probe (Proteus)?", "id": "Mengukur Arus Tanpa Memutus." },
  { "en": "Apa Fungsi Voltage Probe (Proteus)?", "id": "Mengukur Tegangan Titik Tertentu." },
  { "en": "Apa Fungsi Audio Graph (Proteus)?", "id": "Analisis Respon Frekuensi Audio." },
  { "en": "Apa Fungsi Fourier Graph (Proteus)?", "id": "Analisis Spektrum Frekuensi." },
  { "en": "Apa Fungsi Noise Analysis (Proteus)?", "id": "Analisis Gangguan Sinyal." },
  { "en": "Apa Fungsi Distorsion Analysis (Proteus)?", "id": "Analisis Cacat Sinyal." },
  { "en": "Apa Fungsi AC Sweep Analysis (Proteus)?", "id": "Analisis Respon Frekuensi." },
  { "en": "Apa Fungsi DC Sweep Analysis (Proteus)?", "id": "Analisis Perubahan Tegangan DC." },
  { "en": "Apa Fungsi Interactive Simulation (Proteus)?", "id": "Simulasi Bisa Dikontrol User." },
  { "en": "Apa Fungsi Step Simulation (Proteus)?", "id": "Simulasi Langkah Demi Langkah." },
  { "en": "Apa Fungsi Pause Simulation (Proteus)?", "id": "Menahan Simulasi Sementara." },
  { "en": "Apa Fungsi Unbalanced Load Flow (ETAP)?", "id": "Analisis Beban Tidak Seimbang." },
  { "en": "Apa Fungsi Motor Acceleration Analysis (ETAP)?", "id": "Analisis Start Motor." },
  { "en": "Apa Fungsi Transformer Tap Setting (ETAP)?", "id": "Mengatur Sadapan Trafo." },
  { "en": "Apa Fungsi Cable Ampacity Derating (ETAP)?", "id": "Penurunan Kapasitas Arus Kabel." },
  { "en": "Apa Fungsi Typical Data (ETAP)?", "id": "Mengisi Data Standar Otomatis." },
  { "en": "Apa Fungsi Lock Unlocked (ETAP)?", "id": "Mengunci Editing Elemen." },
  { "en": "Apa Fungsi Grouping Elemen (ETAP)?", "id": "Mengelompokkan Elemen Rangkaian." },
  { "en": "Apa Fungsi Auto Build One Line (ETAP)?", "id": "Membuat Diagram Otomatis." },
  { "en": "Apa Fungsi Filter Result (ETAP)?", "id": "Menghapus Tampilan Hasil." },
  { "en": "Apa Fungsi Display Options (ETAP)?", "id": "Mengatur Tampilan Diagram." },
  { "en": "Apa Fungsi Result Analyzer (ETAP)?", "id": "Membandingkan Hasil Skenario." },
  { "en": "Apa Fungsi Cable Pulling Analysis (ETAP)?", "id": "Analisis Tarikan Kabel." },
  { "en": "Apa Fungsi Underground Raceway System (ETAP)?", "id": "Sistem Kabel Bawah Tanah." },
  { "en": "Apa Fungsi Overhead Line Parameters (ETAP)?", "id": "Parameter Saluran Udara." },
  { "en": "Apa Fungsi Transmission Line Modeling (ETAP)?", "id": "Pemodelan Saluran Transmisi." },
  { "en": "Apa Instruksi Shift Write (GX Works)?", "id": "Menulis Data Register Geser." },
  { "en": "Apa Instruksi Shift Read (GX Works)?", "id": "Membaca Data Register Geser." },
  { "en": "Apa Instruksi Fill Move (GX Works)?", "id": "Mengisi Banyak Alamat Sama." },
  { "en": "Apa Instruksi Block Move (GX Works)?", "id": "Memindahkan Blok Data." },
  { "en": "Apa Instruksi Edge Pulse (GX Works)?", "id": "Deteksi Sisi Naik." },
  { "en": "Apa Instruksi Edge Falling (GX Works)?", "id": "Deteksi Sisi Turun." },
  { "en": "Apa Fungsi Global Label (GX Works)?", "id": "Variabel Untuk Seluruh Proyek." },
  { "en": "Apa Fungsi Local Label (GX Works)?", "id": "Variabel Untuk Satu Program." },
  { "en": "Apa Fungsi Structured Text (GX Works)?", "id": "Bahasa Pemrograman Teks Pascal." },
  { "en": "Apa Fungsi Function Chart (GX Works)?", "id": "Pemrograman Alur Diagram." },
  { "en": "Apa Fungsi PLC Read (GX Works)?", "id": "Membaca Program Dari PLC." },
  { "en": "Apa Fungsi PLC Write (GX Works)?", "id": "Menulis Program Ke PLC." },
  { "en": "Apa Fungsi Verify With File (GX Works)?", "id": "Membandingkan Dengan File Lain." },
  { "en": "Apa Fungsi Keyword Retentive (GX Works)?", "id": "Data Tersimpan Saat Mati." },
  { "en": "Apa Shortcut Compile All (GX Works)?", "id": "Tekan Shift + Alt + F4." },
  { "en": "Apa Shortcut Find and Replace (GX Works)?", "id": "Tekan Ctrl + H." },
  { "en": "Apa Shortcut Go To Comment (GX Works)?", "id": "Tekan Ctrl + J." },
  { "en": "Apa Shortcut Ladder Monitoring (GX Works)?", "id": "Tekan F3." },
  { "en": "Apa Fungsi Reset Watchdog Timer (GX Works)?", "id": "Mencegah Error Waktu Scan." },
  { "en": "Apa Instruksi SWAP (GX Works)?", "id": "Menukar Byte Data." },
  { "en": "Apa Instruksi Rotate Left (GX Works)?", "id": "Geser Bit Ke Kiri." },
  { "en": "Apa Instruksi Rotate Right (GX Works)?", "id": "Geser Bit Ke Kanan." },
  { "en": "Apa Fungsi Perintah Extrude (AutoCAD)?", "id": "Mengubah Objek 2D Menjadi 3D." },
  { "en": "Apa Fungsi Perintah Revolve (AutoCAD)?", "id": "Memutar Profil Mengelilingi Sumbu." },
  { "en": "Apa Fungsi Perintah Union (AutoCAD)?", "id": "Menggabungkan 2 Solid Menjadi 1." },
  { "en": "Apa Fungsi Perintah Subtract (AutoCAD)?", "id": "Memotong Objek Solid Dengan Lainnya." },
  { "en": "Apa Fungsi Perintah Intersect (AutoCAD)?", "id": "Mengambil Bagian Perpotongan Objek." },
  { "en": "Apa Shortcut Mengaktifkan 3D Orbit (AutoCAD)?", "id": "Tekan Shift + Scroll Tengah." },
  { "en": "Apa Fungsi Visual Styles (AutoCAD)?", "id": "Mengubah Tampilan Render Objek." },
  { "en": "Apa Fungsi ViewCube (AutoCAD)?", "id": "Alat Navigasi Pandangan 3D." },
  { "en": "Apa Fungsi Perintah Loft (AutoCAD)?", "id": "Membuat 3D Antara Penampang." },
  { "en": "Apa Fungsi Perintah Sweep (AutoCAD)?", "id": "Membuat 3D Mengikuti Jalur." },
  { "en": "Apa Fungsi Layout Tabs (AutoCAD)?", "id": "Beralih Antara Model Dan Kertas." },
  { "en": "Apa Fungsi Page Setup Manager (AutoCAD)?", "id": "Mengatur Ukuran Kertas Plotter." },
  { "en": "Apa Fungsi Perintah Audit (AutoCAD)?", "id": "Memperbaiki Error Database Gambar." },
  { "en": "Apa Fungsi Perintah Fillet Edge (AutoCAD)?", "id": "Melengkungkan Sudut Objek 3D." },
  { "en": "Apa Fungsi Perintah Chamfer Edge (AutoCAD)?", "id": "Memangkas Sudut Objek 3D." },
  { "en": "Apa Fungsi Perintah Slice (AutoCAD)?", "id": "Memotong Benda Padat 3D." },
  { "en": "Apa Ekstensi File Template (AutoCAD)?", "id": "Ekstensi DWT." },
  { "en": "Apa Fungsi Pin SDA (Arduino IDE)?", "id": "Data Serial Komunikasi I2C." },
  { "en": "Apa Fungsi Pin SCL (Arduino IDE)?", "id": "Clock Serial Komunikasi I2C." },
  { "en": "Dimana Letak Pin SDA Uno (Arduino IDE)?", "id": "Pin A4 Atau Dekat USB." },
  { "en": "Dimana Letak Pin SCL Uno (Arduino IDE)?", "id": "Pin A5 Atau Dekat USB." },
  { "en": "Apa Fungsi Pin MISO SPI (Arduino IDE)?", "id": "Master Input Slave Output." },
  { "en": "Apa Fungsi Pin MOSI SPI (Arduino IDE)?", "id": "Master Output Slave Input." },
  { "en": "Apa Fungsi Pin SCK SPI (Arduino IDE)?", "id": "Serial Clock Komunikasi SPI." },
  { "en": "Apa Fungsi Pin SS SPI (Arduino IDE)?", "id": "Slave Select Komunikasi SPI." },
  { "en": "Apa Fungsi Library Stepper (Arduino IDE)?", "id": "Mengontrol Gerakan Motor Stepper." },
  { "en": "Apa Fungsi EEPROM Read (Arduino IDE)?", "id": "Membaca Byte Dari EEPROM." },
  { "en": "Apa Fungsi EEPROM Write (Arduino IDE)?", "id": "Menulis Byte Ke EEPROM." },
  { "en": "Apa Fungsi EEPROM Update (Arduino IDE)?", "id": "Menulis Jika Nilai Berbeda." },
  { "en": "Apa Fungsi Fungsi Atan (Arduino IDE)?", "id": "Menghitung Arc Tangen." },
  { "en": "Apa Fungsi Fungsi Cos (Arduino IDE)?", "id": "Menghitung Nilai Cosinus." },
  { "en": "Apa Fungsi Fungsi Sin (Arduino IDE)?", "id": "Menghitung Nilai Sinus." },
  { "en": "Apa Fungsi IsAlpha (Arduino IDE)?", "id": "Cek Apakah Karakter Huruf." },
  { "en": "Apa Fungsi IsDigit (Arduino IDE)?", "id": "Cek Apakah Karakter Angka." },
  { "en": "Apa Instruksi PID (CX Programmer)?", "id": "Kontrol Proporsional Integral Derivatif." },
  { "en": "Apa Fungsi Instruksi Arithmetic Process (CX Programmer)?", "id": "Perhitungan Aritmatika Kompleks." },
  { "en": "Apa Fungsi Instruksi Scaling (CX Programmer)?", "id": "Konversi Nilai Analog Linear." },
  { "en": "Apa Fungsi Instruksi Scaling 2 (CX Programmer)?", "id": "Konversi Scaling Dengan Offset." },
  { "en": "Apa Fungsi Instruksi Average (CX Programmer)?", "id": "Menghitung Rata Rata Data." },
  { "en": "Apa Fungsi Instruksi Maximum (CX Programmer)?", "id": "Mencari Nilai Tertinggi Data." },
  { "en": "Apa Fungsi Instruksi Minimum (CX Programmer)?", "id": "Mencari Nilai Terendah Data." },
  { "en": "Apa Fungsi Task Allocation (CX Programmer)?", "id": "Membagi Tugas Program PLC." },
  { "en": "Apa Fungsi Interrupt Task (CX Programmer)?", "id": "Program Prioritas Tinggi." },
  { "en": "Apa Fungsi Cycle Time (CX Programmer)?", "id": "Waktu 1 Putaran Program." },
  { "en": "Apa Fungsi Error Log (CX Programmer)?", "id": "Riwayat Kesalahan Sistem." },
  { "en": "Apa Fungsi Data Trace (CX Programmer)?", "id": "Grafik Nilai Bit Word." },
  { "en": "Apa Fungsi Online Edit (CX Programmer)?", "id": "Edit Program Tanpa Stop." },
  { "en": "Apa Fungsi Memory Card (CX Programmer)?", "id": "Media Penyimpanan Eksternal." },
  { "en": "Apa Fungsi Source Current (Proteus)?", "id": "Sumber Arus Konstan." },
  { "en": "Apa Fungsi Sine Generator (Proteus)?", "id": "Pembangkit Gelombang Sinus." },
  { "en": "Apa Fungsi Pulse Generator (Proteus)?", "id": "Pembangkit Gelombang Kotak." },
  { "en": "Apa Fungsi Audio Generator (Proteus)?", "id": "Sumber Sinyal Suara Audio." },
  { "en": "Apa Fungsi Digital Clock (Proteus)?", "id": "Sumber Detak Logika Digital." },
  { "en": "Apa Fungsi Pattern Generator (Proteus)?", "id": "Pembangkit Pola Data Digital." },
  { "en": "Apa Fungsi Voltage Source (Proteus)?", "id": "Sumber Tegangan DC Adjustable." },
  { "en": "Apa Fungsi Current Source (Proteus)?", "id": "Sumber Arus DC Adjustable." },
  { "en": "Apa Fungsi Wattmeter (Proteus)?", "id": "Mengukur Daya Listrik." },
  { "en": "Apa Fungsi Frequency Counter (Proteus)?", "id": "Mengukur Frekuensi Sinyal." },
  { "en": "Apa Fungsi Export Gerber (Proteus)?", "id": "Membuat File Produksi PCB." },
  { "en": "Apa Fungsi Print Layout (Proteus)?", "id": "Mencetak Desain PCB." },
  { "en": "Apa Fungsi Time Current Curve (ETAP)?", "id": "Kurva Karakteristik Arus Waktu." },
  { "en": "Apa Fungsi Pickup Value (ETAP)?", "id": "Batas Arus Mulai Bekerja." },
  { "en": "Apa Fungsi Time Dial Setting (ETAP)?", "id": "Pengaturan Waktu Tunda Relay." },
  { "en": "Apa Fungsi Instantaneous Setting (ETAP)?", "id": "Seting Putus Seketika." },
  { "en": "Apa Fungsi CT Ratio (ETAP)?", "id": "Hitung Rasio Trafo Arus." },
  { "en": "Apa Fungsi Flux Analysis (ETAP)?", "id": "Analisis Fluks Magnetik Trafo." },
  { "en": "Apa Fungsi Harmonic Order (ETAP)?", "id": "Urutan Frekuensi Harmonisa." },
  { "en": "Apa Fungsi Total Harmonic Distortion (ETAP)?", "id": "Total Distorsi Harmonisa." },
  { "en": "Apa Fungsi Battery Discharge (ETAP)?", "id": "Analisis Pengosongan Baterai." },
  { "en": "Apa Fungsi Cable Ampacity (ETAP)?", "id": "Kemampuan Hantar Arus Kabel." },
  { "en": "Apa Fungsi Swing Bus (ETAP)?", "id": "Bus Penyeimbang Daya Sistem." },
  { "en": "Apa Fungsi Voltage Control Bus (ETAP)?", "id": "Bus Pengatur Tegangan Generator." },
  { "en": "Apa Fungsi Load Bus (ETAP)?", "id": "Bus Tanpa Pembangkitan." },
  { "en": "Apa Fungsi Fuse Cutout (ETAP)?", "id": "Pengaman Lebur Tegangan Menengah." },
  { "en": "Apa Fungsi Recloser (ETAP)?", "id": "Pemutus Penutup Otomatis." },
  { "en": "Apa Fungsi Isolator Switch (ETAP)?", "id": "Pemisah Rangkaian Tanpa Beban." },
  { "en": "Apa Fungsi CC-Link Parameter (GX Works)?", "id": "Pengaturan Jaringan Mitsubishi." },
  { "en": "Apa Fungsi Ethernet Port (GX Works)?", "id": "Pengaturan IP Address PLC." },
  { "en": "Apa Fungsi Built-In IO (GX Works)?", "id": "Konfigurasi Input Output Bawaan." },
  { "en": "Apa Fungsi High Speed Counter (GX Works)?", "id": "Penghitung Pulsa Cepat." },
  { "en": "Apa Fungsi Pulse Catch (GX Works)?", "id": "Menangkap Sinyal Sangat Singkat." },
  { "en": "Apa Fungsi Interrupt Input (GX Works)?", "id": "Input Pemicu Interupsi." },
  { "en": "Apa Fungsi Positioning Control (GX Works)?", "id": "Kontrol Posisi Motor Servo." },
  { "en": "Apa Fungsi XY Table (GX Works)?", "id": "Tabel Alamat Input Output." },
  { "en": "Apa Instruksi Pulse Variable (GX Works)?", "id": "Output Pulsa Kecepatan Variabel." },
  { "en": "Apa Instruksi Drive Increment (GX Works)?", "id": "Gerakan Posisi Relatif." },
  { "en": "Apa Instruksi Drive Absolute (GX Works)?", "id": "Gerakan Posisi Mutlak." },
  { "en": "Apa Instruksi Zero Return (GX Works)?", "id": "Kembali Ke Titik Nol." },
  { "en": "Apa Instruksi Absolute (GX Works)?", "id": "Mengambil Nilai Mutlak." },
  { "en": "Apa Instruksi Increment (GX Works)?", "id": "Menambah Nilai Data 1." },
  { "en": "Apa Instruksi Decrement (GX Works)?", "id": "Mengurang Nilai Data 1." },
  { "en": "Apa Fungsi Sampling Trace (GX Works)?", "id": "Mengambil Sampel Data Cepat." },
  { "en": "Apa Shortcut Stop Simulation (GX Works)?", "id": "Tidak Ada Shortcut Standar." },
  { "en": "Apa Shortcut Switch Window (GX Works)?", "id": "Tekan Ctrl + Tab." },
  { "en": "Apa Fungsi Dimlinear (AutoCAD)?", "id": "Mengukur Garis Horizontal Vertikal." },
  { "en": "Apa Fungsi Dimaligned (AutoCAD)?", "id": "Mengukur Garis Miring Sejajar." },
  { "en": "Apa Fungsi Dimangular (AutoCAD)?", "id": "Mengukur Sudut Antara Garis." },
  { "en": "Apa Fungsi Dimradius (AutoCAD)?", "id": "Mengukur Jari Jari Lingkaran." },
  { "en": "Apa Fungsi Dimdiameter (AutoCAD)?", "id": "Mengukur Diameter Lingkaran." },
  { "en": "Apa Fungsi Dimstyle (AutoCAD)?", "id": "Mengatur Gaya Tampilan Dimensi." },
  { "en": "Apa Fungsi Leader (AutoCAD)?", "id": "Membuat Garis Penunjuk Keterangan." },
  { "en": "Apa Fungsi Tolerance (AutoCAD)?", "id": "Memberi Simbol Toleransi Geometris." },
  { "en": "Apa Fungsi Center Mark (AutoCAD)?", "id": "Memberi Tanda Titik Tengah." },
  { "en": "Apa Fungsi Dimjogged (AutoCAD)?", "id": "Memberi Dimensi Radius Putus." },
  { "en": "Apa Fungsi Dimordinate (AutoCAD)?", "id": "Memberi Koordinat Titik XY." },
  { "en": "Apa Fungsi Perintah Oops (AutoCAD)?", "id": "Mengembalikan Objek Terhapus Terakhir." },
  { "en": "Apa Fungsi Imageattach (AutoCAD)?", "id": "Memasukkan Gambar Ke AutoCAD." },
  { "en": "Apa Fungsi Xclip (AutoCAD)?", "id": "Memotong Tampilan Blok Xref." },
  { "en": "Apa Fungsi Mslide (AutoCAD)?", "id": "Membuat File Slide Gambar." },
  { "en": "Apa Fungsi Vslide (AutoCAD)?", "id": "Melihat File Slide Gambar." },
  { "en": "Apa Fungsi Color Command (AutoCAD)?", "id": "Mengubah Warna Objek Aktif." },
  { "en": "Apa Fungsi Operator += (Arduino IDE)?", "id": "Menjumlahkan Nilai Ke Variabel." },
  { "en": "Apa Fungsi Operator -= (Arduino IDE)?", "id": "Mengurangkan Nilai Ke Variabel." },
  { "en": "Apa Fungsi Operator *= (Arduino IDE)?", "id": "Mengalikan Nilai Ke Variabel." },
  { "en": "Apa Fungsi Operator /= (Arduino IDE)?", "id": "Membagi Nilai Ke Variabel." },
  { "en": "Apa Fungsi Operator == (Arduino IDE)?", "id": "Memeriksa Apakah 2 Nilai Sama." },
  { "en": "Apa Fungsi Operator != (Arduino IDE)?", "id": "Memeriksa Apakah 2 Nilai Beda." },
  { "en": "Apa Fungsi Operator <= (Arduino IDE)?", "id": "Kurang Dari Atau Sama Dengan." },
  { "en": "Apa Fungsi Operator >= (Arduino IDE)?", "id": "Lebih Dari Atau Sama Dengan." },
  { "en": "Apa Fungsi Operator Geser Kiri (Arduino IDE)?", "id": "Menggeser Bit Ke Kiri." },
  { "en": "Apa Fungsi Operator Geser Kanan (Arduino IDE)?", "id": "Menggeser Bit Ke Kanan." },
  { "en": "Apa Fungsi Operator Ternary (Arduino IDE)?", "id": "Logika If Else Satu Baris." },
  { "en": "Apa Fungsi Sizeof (Arduino IDE)?", "id": "Menghitung Ukuran Byte Variabel." },
  { "en": "Apa Fungsi Tipe Data Byte (Arduino IDE)?", "id": "Menyimpan Angka 0 Sampai 255." },
  { "en": "Apa Fungsi Tipe Data Unsigned Long (Arduino IDE)?", "id": "Menyimpan Angka Positif Besar." },
  { "en": "Apa Fungsi Tipe Data Word (Arduino IDE)?", "id": "Sama Dengan Unsigned Int." },
  { "en": "Apa Fungsi NoInterrupts (Arduino IDE)?", "id": "Mematikan Fungsi Interupsi." },
  { "en": "Apa Fungsi Interrupts (Arduino IDE)?", "id": "Mengaktifkan Kembali Interupsi." },
  { "en": "Apa Instruksi AND LD (CX Programmer)?", "id": "Seri Antara 2 Blok Paralel." },
  { "en": "Apa Instruksi OR LD (CX Programmer)?", "id": "Paralel Antara 2 Blok Seri." },
  { "en": "Apa Fungsi Temporary Relay (CX Programmer)?", "id": "Menyimpan Sementara Cabang Logika." },
  { "en": "Apa Instruksi NOT (CX Programmer)?", "id": "Membalikkan Logika Bit." },
  { "en": "Apa Instruksi Exclusive OR (CX Programmer)?", "id": "Aktif Jika Input Berbeda." },
  { "en": "Apa Instruksi Exclusive NOR (CX Programmer)?", "id": "Aktif Jika Input Sama." },
  { "en": "Apa Instruksi Clear Carry (CX Programmer)?", "id": "Membersihkan Flag Carry." },
  { "en": "Apa Instruksi Set Carry (CX Programmer)?", "id": "Mengaktifkan Flag Carry." },
  { "en": "Apa Instruksi Complement (CX Programmer)?", "id": "Membalik Semua Bit Word." },
  { "en": "Apa Instruksi Move Register (CX Programmer)?", "id": "Memindahkan Alamat Memori." },
  { "en": "Apa Instruksi PUSH (CX Programmer)?", "id": "Menyimpan Data Ke Stack." },
  { "en": "Apa Instruksi POP (CX Programmer)?", "id": "Mengambil Data Dari Stack." },
  { "en": "Apa Fungsi Top Copper (Proteus)?", "id": "Lapisan Tembaga Atas PCB." },
  { "en": "Apa Fungsi Bottom Copper (Proteus)?", "id": "Lapisan Tembaga Bawah PCB." },
  { "en": "Apa Fungsi Top Silk (Proteus)?", "id": "Gambar Cetak Bagian Atas." },
  { "en": "Apa Fungsi Bottom Silk (Proteus)?", "id": "Gambar Cetak Bagian Bawah." },
  { "en": "Apa Fungsi Drill Hole (Proteus)?", "id": "Lubang Bor Pada PCB." },
  { "en": "Apa Fungsi Board Edge (Proteus)?", "id": "Garis Batas Potong PCB." },
  { "en": "Apa Fungsi Keepout Layer (Proteus)?", "id": "Area Larangan Jalur Komponen." },
  { "en": "Apa Fungsi Pad Stack (Proteus)?", "id": "Bentuk Tumpukan Lapisan Pad." },
  { "en": "Apa Fungsi Via Shielding (Proteus)?", "id": "Via Pelindung Interferensi." },
  { "en": "Apa Fungsi Teardrops (Proteus)?", "id": "Memperkuat Sambungan Pad Jalur." },
  { "en": "Apa Fungsi Power Plane (Proteus)?", "id": "Membuat Area Ground Plane." },
  { "en": "Apa Fungsi Layer Selector (Proteus)?", "id": "Memilih Lapisan PCB Aktif." },
  { "en": "Apa Fungsi 3D Visualization (Proteus)?", "id": "Melihat Simulasi Bentuk PCB." },
  { "en": "Apa Fungsi Distance Measurement (Proteus)?", "id": "Mengukur Jarak Antar Komponen." },
  { "en": "Apa Fungsi Project Information (ETAP)?", "id": "Data Proyek Dan Klien." },
  { "en": "Apa Fungsi Standards IEC (ETAP)?", "id": "Standar Kelistrikan Internasional." },
  { "en": "Apa Fungsi Standards ANSI (ETAP)?", "id": "Standar Kelistrikan Amerika." },
  { "en": "Apa Fungsi Base KV (ETAP)?", "id": "Tegangan Dasar Sistem." },
  { "en": "Apa Fungsi MVA Base (ETAP)?", "id": "Daya Dasar Perhitungan." },
  { "en": "Apa Fungsi Report Manager (ETAP)?", "id": "Mengelola Laporan Hasil Analisis." },
  { "en": "Apa Fungsi Bus Dump Report (ETAP)?", "id": "Laporan Detail Data Bus." },
  { "en": "Apa Fungsi Crystal Reports (ETAP)?", "id": "Format Laporan Standar ETAP." },
  { "en": "Apa Fungsi Impedance Tolerance (ETAP)?", "id": "Toleransi Nilai Impedansi Komponen." },
  { "en": "Apa Fungsi Cable Library (ETAP)?", "id": "Database Spesifikasi Kabel." },
  { "en": "Apa Fungsi Motor Library (ETAP)?", "id": "Database Spesifikasi Motor." },
  { "en": "Apa Fungsi Fuse Library (ETAP)?", "id": "Database Spesifikasi Sekering." },
  { "en": "Apa Fungsi Relay Library (ETAP)?", "id": "Database Spesifikasi Relay." },
  { "en": "Apa Fungsi Auto-Save (ETAP)?", "id": "Penyimpanan Otomatis Berkala." },
  { "en": "Apa Fungsi Password Protection (ETAP)?", "id": "Melindungi Proyek Dengan Sandi." },
  { "en": "Apa Fungsi User Manager (ETAP)?", "id": "Mengatur Hak Akses Pengguna." },
  { "en": "Apa Kode SM400 (GX Works)?", "id": "Bit Selalu ON." },
  { "en": "Apa Kode SM401 (GX Works)?", "id": "Bit Selalu OFF." },
  { "en": "Apa Kode SM402 (GX Works)?", "id": "Pulsa ON Saat Start." },
  { "en": "Apa Kode SM412 (GX Works)?", "id": "Clock Pulse 1 Detik." },
  { "en": "Apa Kode SM413 (GX Works)?", "id": "Clock Pulse 2 Detik." },
  { "en": "Apa Kode SD0 (GX Works)?", "id": "Diagnosa Kesalahan CPU." },
  { "en": "Apa Kode SD203 (GX Works)?", "id": "Tipe CPU Yang Dipakai." },
  { "en": "Apa Instruksi BCDP (GX Works)?", "id": "Konversi BCD Satu Siklus." },
  { "en": "Apa Instruksi BINP (GX Works)?", "id": "Konversi Biner Satu Siklus." },
  { "en": "Apa Instruksi ADDP (GX Works)?", "id": "Penjumlahan Satu Siklus." },
  { "en": "Apa Instruksi SUBP (GX Works)?", "id": "Pengurangan Satu Siklus." },
  { "en": "Apa Shortcut Header Footer (GX Works)?", "id": "Mengatur Judul Cetakan Program." },
  { "en": "Apa Shortcut Page Break (GX Works)?", "id": "Pemisah Halaman Cetak." },
  { "en": "Apa Shortcut Print Preview (GX Works)?", "id": "Melihat Tampilan Sebelum Cetak." },
  { "en": "Apa Shortcut Cross Reference (GX Works)?", "id": "Daftar Penggunaan Alamat." },
  { "en": "Apa Shortcut Used Device (GX Works)?", "id": "Daftar Perangkat Yang Terpakai." },
  { "en": "Apa Shortcut Unused Device (GX Works)?", "id": "Daftar Perangkat Tidak Terpakai." },
  { "en": "Apa Fungsi Scaling 1:1 (AutoCAD)?", "id": "Ukuran Gambar Sama Asli." },
  { "en": "Apa Fungsi Scaling 1:100 (AutoCAD)?", "id": "Satu Gambar Seratus Asli." },
  { "en": "Apa Shortcut F1 (AutoCAD)?", "id": "Membuka Menu Bantuan." },
  { "en": "Apa Shortcut F2 (AutoCAD)?", "id": "Membuka Riwayat Perintah." },
  { "en": "Apa Shortcut F10 (AutoCAD)?", "id": "Mengaktifkan Polar Tracking." },
  { "en": "Apa Shortcut F11 (AutoCAD)?", "id": "Mengaktifkan Object Snap Tracking." },
  { "en": "Apa Shortcut F12 (AutoCAD)?", "id": "Mengaktifkan Dynamic Input." },
  { "en": "Apa Fungsi Ltscale (AutoCAD)?", "id": "Mengatur Skala Garis Putus." },
  { "en": "Apa Fungsi Regenall (AutoCAD)?", "id": "Refresh Tampilan Semua Viewport." },
  { "en": "Apa Fungsi Attedit (AutoCAD)?", "id": "Mengedit Nilai Atribut Blok." },
  { "en": "Apa Fungsi Chspace (AutoCAD)?", "id": "Pindah Objek Model Ke Layout." },
  { "en": "Apa Fungsi Torient (AutoCAD)?", "id": "Memutar Teks Agar Mudah Dibaca." },
  { "en": "Apa Fungsi Tcount (AutoCAD)?", "id": "Memberi Nomor Urut Teks Otomatis." },
  { "en": "Apa Fungsi Burst (AutoCAD)?", "id": "Pecah Blok Tanpa Hapus Atribut." },
  { "en": "Apa Fungsi Mline (AutoCAD)?", "id": "Membuat Garis Ganda Paralel." },
  { "en": "Apa Fungsi Ray (AutoCAD)?", "id": "Garis Bantu Satu Arah Tak Hingga." },
  { "en": "Apa Fungsi Point (AutoCAD)?", "id": "Membuat Objek Titik Tunggal." },
  { "en": "Apa Fungsi Ptype (AutoCAD)?", "id": "Mengubah Bentuk Tampilan Titik." },
  { "en": "Apa Fungsi Boundary (AutoCAD)?", "id": "Membuat Polyline Dari Area Tertutup." },
  { "en": "Apa Fungsi Region (AutoCAD)?", "id": "Mengubah Bidang Menjadi Area Fisik." },
  { "en": "Apa Fungsi Massprop (AutoCAD)?", "id": "Menghitung Massa Dan Volume 3D." },
  { "en": "Apa Fungsi Matlib (AutoCAD)?", "id": "Membuka Pustaka Material Render." },
  { "en": "Apa Fungsi Solprof (AutoCAD)?", "id": "Membuat Profil 2D Dari 3D." },
  { "en": "Apa Fungsi Keyword Progmem (Arduino IDE)?", "id": "Menyimpan Data Di Flash Memory." },
  { "en": "Apa Fungsi Macro F (Arduino IDE)?", "id": "Menyimpan String Di Flash Memory." },
  { "en": "Apa Fungsi Fungsi Tan (Arduino IDE)?", "id": "Menghitung Nilai Tangen Sudut." },
  { "en": "Apa Fungsi Acos (Arduino IDE)?", "id": "Menghitung Arc Cosinus." },
  { "en": "Apa Fungsi Asin (Arduino IDE)?", "id": "Menghitung Arc Sinus." },
  { "en": "Apa Fungsi Ceil (Arduino IDE)?", "id": "Pembulatan Angka Ke Atas." },
  { "en": "Apa Fungsi Floor (Arduino IDE)?", "id": "Pembulatan Angka Ke Bawah." },
  { "en": "Apa Fungsi Round (Arduino IDE)?", "id": "Pembulatan Angka Terdekat." },
  { "en": "Apa Fungsi IsSpace (Arduino IDE)?", "id": "Cek Karakter Spasi." },
  { "en": "Apa Fungsi IsUpperCase (Arduino IDE)?", "id": "Cek Huruf Kapital." },
  { "en": "Apa Fungsi IsLowerCase (Arduino IDE)?", "id": "Cek Huruf Kecil." },
  { "en": "Apa Fungsi ToUpperCase (Arduino IDE)?", "id": "Ubah Ke Huruf Kapital." },
  { "en": "Apa Fungsi ToLowerCase (Arduino IDE)?", "id": "Ubah Ke Huruf Kecil." },
  { "en": "Apa Fungsi Flag Error (CX Programmer)?", "id": "Menandakan Terjadi Kesalahan Instruksi." },
  { "en": "Apa Fungsi Flag Carry (CX Programmer)?", "id": "Menandakan Sisa Hasil Operasi." },
  { "en": "Apa Fungsi Flag Equal (CX Programmer)?", "id": "Menandakan Hasil Banding Sama." },
  { "en": "Apa Fungsi Flag Greater Than (CX Programmer)?", "id": "Menandakan Nilai Lebih Besar." },
  { "en": "Apa Fungsi Flag Less Than (CX Programmer)?", "id": "Menandakan Nilai Lebih Kecil." },
  { "en": "Apa Fungsi Flag Overflow (CX Programmer)?", "id": "Menandakan Hasil Melebihi Kapasitas." },
  { "en": "Apa Instruksi Arithmetic Shift Left (CX Programmer)?", "id": "Geser Aritmatika Ke Kiri." },
  { "en": "Apa Instruksi Arithmetic Shift Right (CX Programmer)?", "id": "Geser Aritmatika Ke Kanan." },
  { "en": "Apa Instruksi Rotate Left (CX Programmer)?", "id": "Putar Bit Ke Kiri." },
  { "en": "Apa Instruksi Rotate Right (CX Programmer)?", "id": "Putar Bit Ke Kanan." },
  { "en": "Apa Instruksi Exchange (CX Programmer)?", "id": "Menukar Isi Dua Data Word." },
  { "en": "Apa Fungsi Invoke Gate (Proteus)?", "id": "Memilih Gerbang Logika Multi Bagian." },
  { "en": "Apa Fungsi Power Rail Configuration (Proteus)?", "id": "Mengatur Tegangan VCC Dan Ground." },
  { "en": "Apa Fungsi Global Annotation (Proteus)?", "id": "Penomoran Komponen Otomatis." },
  { "en": "Apa Fungsi Find Object (Proteus)?", "id": "Mencari Komponen Di Skematik." },
  { "en": "Apa Fungsi Property Assignment (Proteus)?", "id": "Mengatur Properti Banyak Komponen." },
  { "en": "Apa Fungsi Search And Tag (Proteus)?", "id": "Mencari Dan Menandai Objek." },
  { "en": "Apa Fungsi Design Explorer (Proteus)?", "id": "Menjelajah Struktur Desain Proyek." },
  { "en": "Apa Fungsi Bus Tap (Proteus)?", "id": "Menyambung Kabel Ke Bus." },
  { "en": "Apa Fungsi 2D Graphics Box (Proteus)?", "id": "Menggambar Kotak Grafik 2D." },
  { "en": "Apa Fungsi 2D Graphics Circle (Proteus)?", "id": "Menggambar Lingkaran Grafik 2D." },
  { "en": "Apa Fungsi 2D Graphics Text (Proteus)?", "id": "Menulis Teks Non Simulasi." },
  { "en": "Apa Fungsi Marker Mode (Proteus)?", "id": "Memberi Tanda Pada Grafik." },
  { "en": "Apa Fungsi Diversity Factor (ETAP)?", "id": "Faktor Keserempakan Beban." },
  { "en": "Apa Fungsi Demand Factor (ETAP)?", "id": "Rasio Beban Maksimum Terpasang." },
  { "en": "Apa Fungsi Coincidence Factor (ETAP)?", "id": "Kebalikan Dari Diversity Factor." },
  { "en": "Apa Fungsi Load Growth (ETAP)?", "id": "Proyeksi Pertumbuhan Beban Tahunan." },
  { "en": "Apa Fungsi Alert Threshold (ETAP)?", "id": "Batas Pemicu Alarm Peringatan." },
  { "en": "Apa Fungsi Marginal Alert (ETAP)?", "id": "Peringatan Kondisi Hampir Kritis." },
  { "en": "Apa Fungsi Critical Alert (ETAP)?", "id": "Peringatan Kondisi Bahaya." },
  { "en": "Apa Fungsi Scenario Editor (ETAP)?", "id": "Mengedit Kondisi Operasi Sistem." },
  { "en": "Apa Fungsi Configuration Status (ETAP)?", "id": "Status Breaker Open Close." },
  { "en": "Apa Fungsi Study Wizard (ETAP)?", "id": "Panduan Melakukan Analisis." },
  { "en": "Apa Fungsi Bus Editor (ETAP)?", "id": "Mengubah Parameter Bus Detail." },
  { "en": "Apa Fungsi Grounding Mode (ETAP)?", "id": "Jenis Pembumian Sistem." },
  { "en": "Apa Kode M8000 (GX Works)?", "id": "Kontak Run Monitor Selalu ON." },
  { "en": "Apa Kode M8002 (GX Works)?", "id": "Pulsa Awal Saat Start." },
  { "en": "Apa Kode M8013 (GX Works)?", "id": "Clock Pulse 1 Detik." },
  { "en": "Apa Kode M8014 (GX Works)?", "id": "Clock Pulse 1 Menit." },
  { "en": "Apa Instruksi Word And (GX Works)?", "id": "Logika AND Data Word." },
  { "en": "Apa Instruksi Word Or (GX Works)?", "id": "Logika OR Data Word." },
  { "en": "Apa Instruksi Word XOR (GX Works)?", "id": "Logika XOR Data Word." },
  { "en": "Apa Instruksi Negation (GX Works)?", "id": "Membalik Tanda Positif Negatif." },
  { "en": "Apa Instruksi Zone Compare (GX Works)?", "id": "Membandingkan Data Dalam Rentang." },
  { "en": "Apa Instruksi Search (GX Works)?", "id": "Mencari Data Dalam Blok." },
  { "en": "Apa Instruksi Sum Check (GX Works)?", "id": "Menghitung Jumlah Bit ON." },
  { "en": "Apa Instruksi Bit On Check (GX Works)?", "id": "Cek Status Bit Posisi Tertentu." },
  { "en": "Apa Instruksi Mean (GX Works)?", "id": "Menghitung Nilai Rata Rata." },
  { "en": "Apa Instruksi Square Root (GX Works)?", "id": "Menghitung Akar Kuadrat." },
  { "en": "Apa Fungsi Cross Reference Window (GX Works)?", "id": "Melacak Alamat Yang Digunakan." },
  { "en": "Apa Fungsi Ladder Monitoring (GX Works)?", "id": "Melihat Status Program Realtime." },
  { "en": "Apa Shortcut Ctrl + Home (GX Works)?", "id": "Pindah Ke Awal Program." },
  { "en": "Apa Shortcut Ctrl + End (GX Works)?", "id": "Pindah Ke Akhir Program." },
  { "en": "Apa Fungsi Status Bar (AutoCAD)?", "id": "Menampilkan Koordinat Dan Mode." },
  { "en": "Apa Fungsi Menu Browser (AutoCAD)?", "id": "Akses Menu File Utama." },
  { "en": "Apa Fungsi Quick Access (AutoCAD)?", "id": "Akses Cepat Perintah Umum." },
  { "en": "Apa Fungsi Ribbon (AutoCAD)?", "id": "Panel Ikon Perintah Kelompok." },
  { "en": "Apa Fungsi ViewCube Compass (AutoCAD)?", "id": "Menunjukkan Arah Mata Angin." },
  { "en": "Apa Fungsi SteeringWheels (AutoCAD)?", "id": "Roda Navigasi Kursor 2D 3D." },
  { "en": "Apa Fungsi InfoCenter (AutoCAD)?", "id": "Pusat Bantuan Dan Pencarian." },
  { "en": "Apa Fungsi Tool Palettes (AutoCAD)?", "id": "Tab Blok Dan Hatch." },
  { "en": "Apa Fungsi Sheet Set (AutoCAD)?", "id": "Mengelola Kumpulan Lembar Gambar." },
  { "en": "Apa Fungsi Markup Set (AutoCAD)?", "id": "Mengelola Catatan Revisi Gambar." },
  { "en": "Apa Fungsi Perintah Align (AutoCAD)?", "id": "Mensejajarkan Objek Dengan Objek Lain." },
  { "en": "Apa Fungsi Perintah Lengthen (AutoCAD)?", "id": "Mengubah Panjang Garis Tanpa Trim." },
  { "en": "Apa Fungsi Mirrtext (AutoCAD)?", "id": "Mengatur Arah Teks Saat Dicerminkan." },
  { "en": "Apa Fungsi Filedia (AutoCAD)?", "id": "Menampilkan Kotak Dialog File." },
  { "en": "Apa Fungsi Pickbox (AutoCAD)?", "id": "Mengatur Ukuran Kotak Kursor Seleksi." },
  { "en": "Apa Fungsi Perintah Overkill (AutoCAD)?", "id": "Menghapus Garis Yang Bertumpuk." },
  { "en": "Apa Fungsi Rename Command (AutoCAD)?", "id": "Mengganti Nama Layer Atau Blok." },
  { "en": "Apa Ekstensi Backup (AutoCAD)?", "id": "Ekstensi BAK." },
  { "en": "Apa Ekstensi Template Standar (AutoCAD)?", "id": "Ekstensi DWT." },
  { "en": "Apa Ekstensi Pertukaran Gambar (AutoCAD)?", "id": "Ekstensi DXF." },
  { "en": "Apa Fungsi Zoom Window (AutoCAD)?", "id": "Memperbesar Area Kotak Tertentu." },
  { "en": "Apa Fungsi Zoom Previous (AutoCAD)?", "id": "Kembali Ke Tampilan Zoom Sebelumnya." },
  { "en": "Apa Fungsi Zoom Object (AutoCAD)?", "id": "Memperbesar Fokus Ke Objek Terpilih." },
  { "en": "Apa Fungsi Perintah Mview (AutoCAD)?", "id": "Membuat Jendela Viewport Baru." },
  { "en": "Apa Fungsi Psetupin (AutoCAD)?", "id": "Impor Pengaturan Halaman File Lain." },
  { "en": "Apa Fungsi Bootloader (Arduino IDE)?", "id": "Program Awal Untuk Upload Sketch." },
  { "en": "Apa Itu SRAM (Arduino IDE)?", "id": "Memori Data Sementara Saat Nyala." },
  { "en": "Apa Itu Flash Memory (Arduino IDE)?", "id": "Memori Penyimpan Program Sketch." },
  { "en": "Apa Fungsi Library Servo (Arduino IDE)?", "id": "Mengendalikan Motor Servo." },
  { "en": "Apa Fungsi Servo Attach (Arduino IDE)?", "id": "Menghubungkan Servo Ke Pin." },
  { "en": "Apa Fungsi Servo Write (Arduino IDE)?", "id": "Menggerakkan Servo Ke Sudut Tertentu." },
  { "en": "Apa Fungsi Servo Read (Arduino IDE)?", "id": "Membaca Posisi Sudut Servo." },
  { "en": "Apa Fungsi DetachInterrupt (Arduino IDE)?", "id": "Mematikan Fungsi Interupsi." },
  { "en": "Apa Fungsi AnalogReference INTERNAL (Arduino IDE)?", "id": "Menggunakan Referensi Tegangan Internal." },
  { "en": "Apa Fungsi AnalogReference EXTERNAL (Arduino IDE)?", "id": "Menggunakan Referensi Tegangan AREF." },
  { "en": "Apa Fungsi Pin AREF (Arduino IDE)?", "id": "Input Tegangan Referensi Analog." },
  { "en": "Apa Fungsi Pin IOREF (Arduino IDE)?", "id": "Referensi Tegangan Operasi Shield." },
  { "en": "Apa Fungsi Tombol Reset (Arduino IDE)?", "id": "Memulai Ulang Program Arduino." },
  { "en": "Apa Instruksi 7 Segment Decoder (CX Programmer)?", "id": "Konversi Kode Ke 7 Segment." },
  { "en": "Apa Instruksi ASCII Convert (CX Programmer)?", "id": "Konversi Hexadesimal Ke Kode ASCII." },
  { "en": "Apa Instruksi ASCII To Hex (CX Programmer)?", "id": "Konversi Kode ASCII Ke Hexadesimal." },
  { "en": "Apa Instruksi Data Multiplexer (CX Programmer)?", "id": "Memilih Data Dari Banyak Sumber." },
  { "en": "Apa Instruksi Data Demultiplexer (CX Programmer)?", "id": "Membagi Data Ke Banyak Tujuan." },
  { "en": "Apa Fungsi Instruksi Seconds (CX Programmer)?", "id": "Konversi Waktu Ke Detik." },
  { "en": "Apa Fungsi Instruksi Hours Minutes (CX Programmer)?", "id": "Konversi Detik Ke Jam Menit." },
  { "en": "Apa Fungsi I/O Comment (CX Programmer)?", "id": "Memberi Nama Pada Alamat Pin." },
  { "en": "Apa Fungsi Rung Header (CX Programmer)?", "id": "Judul Untuk Baris Logika." },
  { "en": "Apa Fungsi Symbol Global (CX Programmer)?", "id": "Variabel Semua Program." },
  { "en": "Apa Fungsi Symbol Local (CX Programmer)?", "id": "Variabel Hanya Satu Program Saja." },
  { "en": "Apa Fungsi Instruksi PIDAT (CX Programmer)?", "id": "Kontrol PID Dengan Autotuning." },
  { "en": "Apa Fungsi Breakpoint (Proteus)?", "id": "Titik Henti Simulasi Kode." },
  { "en": "Apa Fungsi Single Step (Proteus)?", "id": "Menjalankan Kode Baris Per Baris." },
  { "en": "Apa Fungsi Watch Window (Proteus)?", "id": "Memantau Nilai Variabel Coding." },
  { "en": "Apa Fungsi Simulation Error (Proteus)?", "id": "Daftar Kesalahan Saat Simulasi." },
  { "en": "Apa Error Timestep Too Small (Proteus)?", "id": "Simulasi Terlalu Berat Bagi CPU." },
  { "en": "Apa Error Gmin Stepping (Proteus)?", "id": "Kegagalan Konvergensi Rangkaian Analog." },
  { "en": "Apa Fungsi ERC Errors (Proteus)?", "id": "Kesalahan Aturan Listrik Skematik." },
  { "en": "Apa Fungsi Component Value Error (Proteus)?", "id": "Nilai Komponen Tidak Valid." },
  { "en": "Apa Fungsi Pin Not Connected (Proteus)?", "id": "Kaki Komponen Tidak Tersambung." },
  { "en": "Apa Fungsi Power Pin Error (Proteus)?", "id": "Pin Power Belum Dapat Tegangan." },
  { "en": "Apa Fungsi Duplicate Part (Proteus)?", "id": "Nama Komponen Ganda Di Desain." },
  { "en": "Apa Fungsi Missing Model (Proteus)?", "id": "Model Simulasi Tidak Ditemukan." },
  { "en": "Apa Fungsi Netlist Compiler (Proteus)?", "id": "Gagal Membuat Daftar Koneksi." },
  { "en": "Apa Itu Fault Current (ETAP)?", "id": "Arus Gangguan Hubung Singkat." },
  { "en": "Apa Itu X/R Ratio (ETAP)?", "id": "Rasio Reaktansi Terhadap Resistansi." },
  { "en": "Apa Itu Clearing Time (ETAP)?", "id": "Waktu Pemutusan Gangguan." },
  { "en": "Apa Itu Pick-Up Current (ETAP)?", "id": "Arus Pemicu Relay Bekerja." },
  { "en": "Apa Itu Time Dial Multiplier (ETAP)?", "id": "Pengali Waktu Kurva Relay." },
  { "en": "Apa Fungsi Bus Duct (ETAP)?", "id": "Saluran Busbar Terlindung." },
  { "en": "Apa Fungsi Capacitor Switching (ETAP)?", "id": "Analisis Saklar Kapasitor Bank." },
  { "en": "Apa Fungsi Unbalanced Load Flow (ETAP)?", "id": "Analisis Aliran Daya Tak Seimbang." },
  { "en": "Apa Fungsi Sequence Impedance (ETAP)?", "id": "Impedansi Urutan Positif Negatif Nol." },
  { "en": "Apa Fungsi Positive Sequence (ETAP)?", "id": "Komponen Urutan Fasa Normal." },
  { "en": "Apa Fungsi Negative Sequence (ETAP)?", "id": "Komponen Urutan Fasa Terbalik." },
  { "en": "Apa Fungsi Zero Sequence (ETAP)?", "id": "Komponen Urutan Fasa Nol." },
  { "en": "Apa Instruksi Decode (GX Works)?", "id": "Dekoder Kode Bit." },
  { "en": "Apa Instruksi Encode (GX Works)?", "id": "Enkoder Kode Bit." },
  { "en": "Apa Instruksi 7 Segment (GX Works)?", "id": "Konversi Ke Tampilan 7 Segment." },
  { "en": "Apa Instruksi Bit Count (GX Works)?", "id": "Menghitung Jumlah Bit Angka 1." },
  { "en": "Apa Instruksi FIFO Write (GX Works)?", "id": "Tulis Data Antrian Masuk." },
  { "en": "Apa Instruksi FIFO Read (GX Works)?", "id": "Baca Data Antrian Keluar." },
  { "en": "Apa Instruksi Fill Move (GX Works)?", "id": "Mengisi Blok Memori Nilai Sama." },
  { "en": "Apa Instruksi Word To Byte (GX Works)?", "id": "Pecah Word Ke Byte." },
  { "en": "Apa Instruksi Byte To Word (GX Works)?", "id": "Gabung Byte Ke Word." },
  { "en": "Apa Instruksi Unite 4 Bit (GX Works)?", "id": "Gabung 4 Bit Ke Word." },
  { "en": "Apa Instruksi Dissociate (GX Works)?", "id": "Pecah Word Ke 4 Bit." },
  { "en": "Apa Fungsi Verify Parameter (GX Works)?", "id": "Cek Parameter PC Lawan PLC." },
  { "en": "Apa Fungsi Delete Unused (GX Works)?", "id": "Hapus Komentar Tidak Terpakai." },
  { "en": "Apa Fungsi Change PLC Type (GX Works)?", "id": "Mengubah Tipe CPU Proyek." },
  { "en": "Apa Fungsi Lock Program (GX Works)?", "id": "Mengunci Program Dengan Password." },
  { "en": "Apa Fungsi Unlock Program (GX Works)?", "id": "Membuka Kunci Program PLC." },
  { "en": "Apa Fungsi IP Address Filter (GX Works)?", "id": "Batasi Akses IP Ke PLC." },
  { "en": "Apa Fungsi Remote Operation (GX Works)?", "id": "Kontrol PLC Jarak Jauh." },
  { "en": "Apa Fungsi Format Memory Card (GX Works)?", "id": "Hapus Seluruh Data Memori Eksternal." },
  { "en": "Apa Shortcut Ctrl + S (AutoCAD)?", "id": "Menyimpan Proyek Saat Ini." },
  { "en": "Apa Shortcut Ctrl + A (AutoCAD)?", "id": "Memilih Semua Objek." },
  { "en": "Apa Shortcut Ctrl + X (AutoCAD)?", "id": "Potong Objek Terpilih." },
  { "en": "Apa Shortcut Ctrl + Y (AutoCAD)?", "id": "Redo Atau Ulangi Perintah." },
  { "en": "Apa Shortcut Esc (AutoCAD)?", "id": "Membatalkan Perintah Aktif." },
  { "en": "Apa Shortcut Delete (AutoCAD)?", "id": "Menghapus Objek Terpilih." },
  { "en": "Apa Shortcut Space Bar (AutoCAD)?", "id": "Konfirmasi Atau Ulangi Perintah." },
  { "en": "Apa Shortcut Enter (AutoCAD)?", "id": "Eksekusi Perintah Atau Baris Baru." },
  { "en": "Apa Fungsi Status Bar Bawah (AutoCAD)?", "id": "Info Status Dan Mode Aplikasi." },
  { "en": "Apa Fungsi Title Bar Atas (AutoCAD)?", "id": "Nama File Dan Program Aktif." },
  { "en": "Apa Fungsi Scroll Bar (AutoCAD)?", "id": "Geser Tampilan Atas Bawah." },
  { "en": "Apa Fungsi Minimize Window (AutoCAD)?", "id": "Sembunyikan Jendela Ke Taskbar." },
  { "en": "Apa Fungsi Maximize Window (AutoCAD)?", "id": "Perbesar Jendela Layar Penuh." },
  { "en": "Apa Fungsi Close Window (AutoCAD)?", "id": "Tutup Aplikasi Atau Dokumen." },
  { "en": "Apa Fungsi Tab Parametric (AutoCAD)?", "id": "Mengatur Batasan Geometris Dan Dimensi." },
  { "en": "Apa Fungsi Constraint Coincident (AutoCAD)?", "id": "Menyatukan Dua Titik Objek." },
  { "en": "Apa Fungsi Constraint Collinear (AutoCAD)?", "id": "Membuat Garis Segaris Lurus." },
  { "en": "Apa Fungsi Constraint Concentric (AutoCAD)?", "id": "Membuat Lingkaran Satu Pusat." },
  { "en": "Apa Fungsi Constraint Parallel (AutoCAD)?", "id": "Membuat Dua Garis Sejajar." },
  { "en": "Apa Fungsi Constraint Perpendicular (AutoCAD)?", "id": "Membuat Garis Tegak Lurus." },
  { "en": "Apa Fungsi Constraint Tangent (AutoCAD)?", "id": "Membuat Garis Bersinggungan Lingkaran." },
  { "en": "Apa Fungsi Dimensional Constraint (AutoCAD)?", "id": "Mengunci Ukuran Objek Gambar." },
  { "en": "Apa Fungsi Delconstraint (AutoCAD)?", "id": "Menghapus Semua Batasan Constraint." },
  { "en": "Apa Fungsi Parameters Manager (AutoCAD)?", "id": "Mengelola Rumus Dan Variabel." },
  { "en": "Apa Fungsi Etransmit (AutoCAD)?", "id": "Mengemas File Siap Kirim." },
  { "en": "Apa Fungsi Dwgcompare (AutoCAD)?", "id": "Membandingkan Perbedaan Dua Gambar." },
  { "en": "Apa Fungsi Pdfimport (AutoCAD)?", "id": "Mengimpor File PDF Ke CAD." },
  { "en": "Apa Fungsi Txt2mtxt (AutoCAD)?", "id": "Ubah Teks Biasa Ke Paragraf." },
  { "en": "Apa Fungsi Count (AutoCAD)?", "id": "Menghitung Jumlah Blok Otomatis." },
  { "en": "Apa Fungsi Fungsi Sq (Arduino IDE)?", "id": "Menghitung Kuadrat Suatu Angka." },
  { "en": "Apa Fungsi Fungsi Radians (Arduino IDE)?", "id": "Konversi Derajat Ke Radian." },
  { "en": "Apa Fungsi Fungsi Degrees (Arduino IDE)?", "id": "Konversi Radian Ke Derajat." },
  { "en": "Apa Fungsi RandomSeed (Arduino IDE)?", "id": "Mengacak Sumber Angka Random." },
  { "en": "Apa Fungsi Word (Arduino IDE)?", "id": "Konversi Tipe Data Ke Word." },
  { "en": "Apa Fungsi LowByte (Arduino IDE)?", "id": "Mengambil Byte Terendah Data." },
  { "en": "Apa Fungsi HighByte (Arduino IDE)?", "id": "Mengambil Byte Tertinggi Data." },
  { "en": "Apa Fungsi Stream Class (Arduino IDE)?", "id": "Kelas Dasar Komunikasi Karakter." },
  { "en": "Apa Fungsi Keyboard Library (Arduino IDE)?", "id": "Simulasi Keyboard Komputer USB." },
  { "en": "Apa Fungsi Mouse Library (Arduino IDE)?", "id": "Simulasi Mouse Komputer USB." },
  { "en": "Apa Fungsi Instruksi Float Add (CX Programmer)?", "id": "Penjumlahan Bilangan Desimal." },
  { "en": "Apa Fungsi Instruksi Float Sub (CX Programmer)?", "id": "Pengurangan Bilangan Desimal." },
  { "en": "Apa Fungsi Instruksi Float Mul (CX Programmer)?", "id": "Perkalian Bilangan Desimal." },
  { "en": "Apa Fungsi Instruksi Float Div (CX Programmer)?", "id": "Pembagian Bilangan Desimal." },
  { "en": "Apa Fungsi Instruksi Sine (CX Programmer)?", "id": "Menghitung Sinus Sudut Radian." },
  { "en": "Apa Fungsi Instruksi Cosine (CX Programmer)?", "id": "Menghitung Cosinus Sudut Radian." },
  { "en": "Apa Fungsi Instruksi Tangent (CX Programmer)?", "id": "Menghitung Tangen Sudut Radian." },
  { "en": "Apa Fungsi Instruksi Arc Sine (CX Programmer)?", "id": "Menghitung Invers Sinus PLC." },
  { "en": "Apa Fungsi Instruksi Arc Cosine (CX Programmer)?", "id": "Menghitung Invers Cosinus PLC." },
  { "en": "Apa Fungsi Instruksi Arc Tangent (CX Programmer)?", "id": "Menghitung Invers Tangen PLC." },
  { "en": "Apa Fungsi Instruksi Radian (CX Programmer)?", "id": "Konversi Derajat Ke Radian." },
  { "en": "Apa Fungsi Instruksi Degree (CX Programmer)?", "id": "Konversi Radian Ke Derajat." },
  { "en": "Apa Fungsi Instruksi Logarithm (CX Programmer)?", "id": "Menghitung Logaritma Natural." },
  { "en": "Apa Fungsi Instruksi Exponential (CX Programmer)?", "id": "Menghitung Pangkat Bilangan." },
  { "en": "Apa Simbol Kontak P_GT (CX Programmer)?", "id": "Aktif Jika Hasil Lebih Besar." },
  { "en": "Apa Simbol Kontak P_EQ (CX Programmer)?", "id": "Aktif Jika Hasil Sama." },
  { "en": "Apa Simbol Kontak P_LT (CX Programmer)?", "id": "Aktif Jika Hasil Lebih Kecil." },
  { "en": "Apa Fungsi Packaging Tool (Proteus)?", "id": "Menghubungkan Simbol Ke Footprint." },
  { "en": "Apa Fungsi Make Device (Proteus)?", "id": "Membuat Komponen Baru Custom." },
  { "en": "Apa Fungsi Decompose Tagging (Proteus)?", "id": "Memecah Komponen Untuk Diedit." },
  { "en": "Apa Fungsi Wire Router Setting (Proteus)?", "id": "Mengatur Strategi Jalur Kabel." },
  { "en": "Apa Fungsi Global Style (Proteus)?", "id": "Mengatur Font Warna Global." },
  { "en": "Apa Fungsi Junction Dot Style (Proteus)?", "id": "Mengubah Ukuran Titik Sambung." },
  { "en": "Apa Fungsi Solder Mask (Proteus)?", "id": "Lapisan Pelindung Tembaga PCB." },
  { "en": "Apa Fungsi Paste Mask (Proteus)?", "id": "Lapisan Cetakan Pasta Solder." },
  { "en": "Apa Fungsi Mechanical Layer (Proteus)?", "id": "Informasi Dimensi Mekanik PCB." },
  { "en": "Apa Fungsi Legacy Library (Proteus)?", "id": "Pustaka Komponen Versi Lama." },
  { "en": "Apa Fungsi Ratsnest Mode (Proteus)?", "id": "Menampilkan Garis Koneksi Udara." },
  { "en": "Apa Fungsi Force Update (Proteus)?", "id": "Paksa Perbarui Perubahan Skematik." },
  { "en": "Apa Fungsi Library Manager (ETAP)?", "id": "Mengedit Data Pustaka Komponen." },
  { "en": "Apa Fungsi Cable Manager (ETAP)?", "id": "Mengelola Daftar Semua Kabel." },
  { "en": "Apa Fungsi Report PDF (ETAP)?", "id": "Ekspor Laporan Ke PDF." },
  { "en": "Apa Fungsi Report Excel (ETAP)?", "id": "Ekspor Laporan Ke Excel." },
  { "en": "Apa Fungsi Arc Flash Labels (ETAP)?", "id": "Label Peringatan Bahaya Busur." },
  { "en": "Apa Fungsi PPE Level (ETAP)?", "id": "Tingkat Alat Pelindung Diri." },
  { "en": "Apa Fungsi Working Distance (ETAP)?", "id": "Jarak Aman Kerja Listrik." },
  { "en": "Apa Fungsi Incident Energy (ETAP)?", "id": "Energi Panas Saat Gangguan." },
  { "en": "Apa Fungsi Star View (ETAP)?", "id": "Tampilan Kurva Koordinasi Proteksi." },
  { "en": "Apa Fungsi Time Current Characteristic (ETAP)?", "id": "Kurva Waktu Arus Proteksi." },
  { "en": "Apa Fungsi Curve Shifting (ETAP)?", "id": "Menggeser Kurva Seting Relay." },
  { "en": "Apa Fungsi Relay Test (ETAP)?", "id": "Simulasi Pengujian Relay Proteksi." },
  { "en": "Apa Fungsi Sequence Of Event (ETAP)?", "id": "Urutan Kejadian Sistem Proteksi." },
  { "en": "Apa Instruksi Floating Add (GX Works)?", "id": "Penjumlahan Float Mitsubishi." },
  { "en": "Apa Instruksi Floating Sub (GX Works)?", "id": "Pengurangan Float Mitsubishi." },
  { "en": "Apa Instruksi Floating Mul (GX Works)?", "id": "Perkalian Float Mitsubishi." },
  { "en": "Apa Instruksi Floating Div (GX Works)?", "id": "Pembagian Float Mitsubishi." },
  { "en": "Apa Instruksi Sine Float (GX Works)?", "id": "Hitung Sinus Float Mitsubishi." },
  { "en": "Apa Instruksi Cosine Float (GX Works)?", "id": "Hitung Cosinus Float Mitsubishi." },
  { "en": "Apa Instruksi Tangent Float (GX Works)?", "id": "Hitung Tangen Float Mitsubishi." },
  { "en": "Apa Instruksi Integer (GX Works)?", "id": "Konversi Float Ke Integer." },
  { "en": "Apa Instruksi Float (GX Works)?", "id": "Konversi Integer Ke Float." },
  { "en": "Apa Instruksi SSTR (GX Works)?", "id": "Deklarasi Data String Teks." },
  { "en": "Apa Instruksi Length (GX Works)?", "id": "Hitung Panjang Karakter String." },
  { "en": "Apa Instruksi String (GX Works)?", "id": "Konversi Angka Ke String." },
  { "en": "Apa Instruksi Value (GX Works)?", "id": "Konversi String Ke Angka." },
  { "en": "Apa Instruksi Ascii (GX Works)?", "id": "Konversi String Ke ASCII." },
  { "en": "Apa Fungsi Project Tree (GX Works)?", "id": "Navigasi Struktur Proyek PLC." },
  { "en": "Apa Fungsi Cross Reference Window (GX Works)?", "id": "Jendela Pelacakan Alamat Bit." },
  { "en": "Apa Fungsi Watch 1 (GX Works)?", "id": "Jendela Pantau Variabel 1." },
  { "en": "Apa Fungsi Intelligent Module (GX Works)?", "id": "Modul Fungsi Cerdas PLC." },
  { "en": "Apa Shortcut Ctrl + P (AutoCAD)?", "id": "Mencetak Diagram Atau Kode." },
  { "en": "Apa Shortcut F5 (AutoCAD)?", "id": "Pindah Bidang Isometrik." },
  { "en": "Apa Shortcut Ctrl + 0 (AutoCAD)?", "id": "Membersihkan Layar Clean Screen." },
  { "en": "Apa Shortcut Ctrl + 8 (AutoCAD)?", "id": "Membuka Kalkulator Cepat." },
  { "en": "Apa Shortcut Ctrl + 3 (AutoCAD)?", "id": "Membuka Tool Palettes." },
  { "en": "Apa Shortcut Ctrl + 4 (AutoCAD)?", "id": "Membuka Sheet Set Manager." },
  { "en": "Apa Shortcut Ctrl + 6 (AutoCAD)?", "id": "Membuka DBConnect Manager." },
  { "en": "Apa Shortcut Ctrl + 7 (AutoCAD)?", "id": "Membuka Markup Set Manager." },
  { "en": "Apa Fungsi Application Menu (AutoCAD)?", "id": "Logo A Merah Pojok Kiri." },
  { "en": "Apa Fungsi Workspace Switching (AutoCAD)?", "id": "Ganti Tampilan 2D Ke 3D." },
  { "en": "Apa Fungsi Hardware Acceleration (AutoCAD)?", "id": "Mempercepat Grafis Dengan GPU." },
  { "en": "Apa Fungsi Plot Style (AutoCAD)?", "id": "Mengatur Warna Hasil Cetak." },
  { "en": "Apa Ekstensi CTB (AutoCAD)?", "id": "Gaya Cetak Berbasis Warna." },
  { "en": "Apa Ekstensi STB (AutoCAD)?", "id": "Gaya Cetak Berbasis Nama." },
  { "en": "Apa Fungsi Batch Plot (AutoCAD)?", "id": "Mencetak Banyak Gambar Sekaligus." },
  { "en": "Apa Perbedaan Teks Dan Mtext (AutoCAD)?", "id": "Mtext Bisa Banyak Baris Paragraf." },
  { "en": "Apa Fungsi Perintah Scaletext (AutoCAD)?", "id": "Mengubah Skala Objek Teks." },
  { "en": "Apa Fungsi Perintah Justifytext (AutoCAD)?", "id": "Mengubah Titik Tumpu Teks." },
  { "en": "Apa Fungsi Perintah Textalign (AutoCAD)?", "id": "Meluruskan Posisi Beberapa Teks." },
  { "en": "Apa Fungsi Perintah Find (AutoCAD)?", "id": "Mencari Dan Mengganti Kata." },
  { "en": "Apa Shortcut Ctrl + Shift + C (AutoCAD)?", "id": "Copy Dengan Titik Acuan." },
  { "en": "Apa Shortcut Ctrl + Shift + V (AutoCAD)?", "id": "Paste Sebagai Blok." },
  { "en": "Apa Fungsi Perintah Spell Check (AutoCAD)?", "id": "Memeriksa Ejaan Kata." },
  { "en": "Apa Fungsi Font Style Standard (AutoCAD)?", "id": "Gaya Huruf Bawaan AutoCAD." },
  { "en": "Apa Fungsi Font Style Annotative (AutoCAD)?", "id": "Ukuran Huruf Menyesuaikan Skala." },
  { "en": "Apa Fungsi Perintah Style (AutoCAD)?", "id": "Membuka Pengaturan Gaya Teks." },
  { "en": "Apa Fungsi Character Map (AutoCAD)?", "id": "Menyisipkan Simbol Khusus Teks." },
  { "en": "Apa Fungsi Text Height (AutoCAD)?", "id": "Mengatur Tinggi Huruf." },
  { "en": "Apa Fungsi Text Rotation (AutoCAD)?", "id": "Mengatur Sudut Putar Teks." },
  { "en": "Apa Fungsi Width Factor (AutoCAD)?", "id": "Mengatur Lebar Karakter Huruf." },
  { "en": "Apa Fungsi Oblique Angle (AutoCAD)?", "id": "Mengatur Kemiringan Huruf." },
  { "en": "Apa Fungsi Upside Down (AutoCAD)?", "id": "Membalik Teks Vertikal." },
  { "en": "Apa Fungsi Backwards (AutoCAD)?", "id": "Membalik Teks Horizontal." },
  { "en": "Apa Fungsi Background Mask (AutoCAD)?", "id": "Memberi Latar Belakang Teks." },
  { "en": "Apa Fungsi Import Text (AutoCAD)?", "id": "Mengambil Teks Dari File Luar." },
  { "en": "Apa Fungsi Fungsi Microseconds (Arduino IDE)?", "id": "Waktu Dalam Satuan Mikrodetik." },
  { "en": "Apa Fungsi Operator Modulus (Arduino IDE)?", "id": "Sisa Hasil Pembagian." },
  { "en": "Apa Fungsi Operator Increment (Arduino IDE)?", "id": "Menambah 1 Ke Variabel." },
  { "en": "Apa Fungsi Operator Decrement (Arduino IDE)?", "id": "Mengurang 1 Dari Variabel." },
  { "en": "Apa Fungsi Compound Addition (Arduino IDE)?", "id": "Tambah Dan Simpan Hasil." },
  { "en": "Apa Fungsi Compound Subtraction (Arduino IDE)?", "id": "Kurang Dan Simpan Hasil." },
  { "en": "Apa Fungsi Compound Multiplication (Arduino IDE)?", "id": "Kali Dan Simpan Hasil." },
  { "en": "Apa Fungsi Compound Division (Arduino IDE)?", "id": "Bagi Dan Simpan Hasil." },
  { "en": "Apa Fungsi Logical NOT (Arduino IDE)?", "id": "Membalikkan Nilai Kebenaran." },
  { "en": "Apa Fungsi Pointer (Arduino IDE)?", "id": "Mengakses Alamat Memori." },
  { "en": "Apa Fungsi Reference (Arduino IDE)?", "id": "Mendapatkan Alamat Variabel." },
  { "en": "Apa Fungsi Array (Arduino IDE)?", "id": "Kumpulan Variabel Sejenis." },
  { "en": "Apa Indeks Awal Array (Arduino IDE)?", "id": "Indeks 0." },
  { "en": "Apa Fungsi Multidimensional Array (Arduino IDE)?", "id": "Array Dalam Array." },
  { "en": "Apa Fungsi Break Switch Case (Arduino IDE)?", "id": "Keluar Dari Blok Case." },
  { "en": "Apa Fungsi Default Case (Arduino IDE)?", "id": "Jalan Jika Tidak Cocok." },
  { "en": "Apa Instruksi Shift Register (GX Works)?", "id": "Geser Bit Kanan Kiri." },
  { "en": "Apa Instruksi Shift Left (GX Works)?", "id": "Geser Bit Ke Kiri." },
  { "en": "Apa Instruksi Shift Right (GX Works)?", "id": "Geser Bit Ke Kanan." },
  { "en": "Apa Instruksi Word Shift Left (GX Works)?", "id": "Geser Word Ke Kiri." },
  { "en": "Apa Instruksi Word Shift Right (GX Works)?", "id": "Geser Word Ke Kanan." },
  { "en": "Apa Instruksi Rotate Right (GX Works)?", "id": "Putar Bit Ke Kanan." },
  { "en": "Apa Instruksi Rotate Left (GX Works)?", "id": "Putar Bit Ke Kiri." },
  { "en": "Apa Instruksi Rotate Carry Right (GX Works)?", "id": "Putar Kanan Dengan Carry." },
  { "en": "Apa Instruksi Rotate Carry Left (GX Works)?", "id": "Putar Kiri Dengan Carry." },
  { "en": "Apa Fungsi Kontak P_0_1s (CX Programmer)?", "id": "Pulsa Detak 0,1 Detik." },
  { "en": "Apa Fungsi Kontak P_0_2s (CX Programmer)?", "id": "Pulsa Detak 0,2 Detik." },
  { "en": "Apa Fungsi Kontak P_1m (CX Programmer)?", "id": "Pulsa Detak 1 Menit." },
  { "en": "Apa Fungsi Kontak P_ER (CX Programmer)?", "id": "Aktif Saat Ada Error." },
  { "en": "Apa Fungsi Kontak P_CY (CX Programmer)?", "id": "Aktif Saat Ada Sisa." },
  { "en": "Apa Fungsi Kontak P_N (CX Programmer)?", "id": "Aktif Saat Hasil Negatif." },
  { "en": "Apa Fungsi Kontak P_Z (CX Programmer)?", "id": "Aktif Saat Hasil Nol." },
  { "en": "Apa Fungsi Grid Snap (Proteus)?", "id": "Kursor Menempel Titik Grid." },
  { "en": "Apa Fungsi Component Replacement (Proteus)?", "id": "Mengganti Komponen Tanpa Hapus." },
  { "en": "Apa Fungsi Wire Auto-Router (Proteus)?", "id": "Membuat Kabel Otomatis." },
  { "en": "Apa Fungsi Manual Routing (Proteus)?", "id": "Membuat Kabel Manual." },
  { "en": "Apa Fungsi Block Copy (Proteus)?", "id": "Menyalin Area Terseleksi." },
  { "en": "Apa Fungsi Block Delete (Proteus)?", "id": "Menghapus Area Terseleksi." },
  { "en": "Apa Fungsi Block Rotate (Proteus)?", "id": "Memutar Area Terseleksi." },
  { "en": "Apa Fungsi Mirror Component (Proteus)?", "id": "Mencerminkan Posisi Komponen." },
  { "en": "Apa Fungsi X-Mirror (Proteus)?", "id": "Cermin Sumbu X." },
  { "en": "Apa Fungsi Y-Mirror (Proteus)?", "id": "Cermin Sumbu Y." },
  { "en": "Apa Fungsi Edit Label (Proteus)?", "id": "Mengubah Teks Label." },
  { "en": "Apa Fungsi Edit Value (Proteus)?", "id": "Mengubah Nilai Komponen." },
  { "en": "Apa Fungsi Edit Footprint (Proteus)?", "id": "Mengubah Kemasan PCB." },
  { "en": "Apa Fungsi Hidden Pins (Proteus)?", "id": "Pin Yang Tidak Terlihat." },
  { "en": "Apa Fungsi Pin Number (Proteus)?", "id": "Nomor Kaki Komponen." },
  { "en": "Apa Fungsi Pin Name (Proteus)?", "id": "Nama Fungsi Kaki Komponen." },
  { "en": "Apa Fungsi Load Flow Alert (ETAP)?", "id": "Peringatan Beban Berlebih." },
  { "en": "Apa Fungsi Marginal Voltage Alert (ETAP)?", "id": "Tegangan Hampir Kritis." },
  { "en": "Apa Fungsi Critical Voltage Alert (ETAP)?", "id": "Tegangan Sangat Kritis." },
  { "en": "Apa Fungsi Cable Overload Alert (ETAP)?", "id": "Arus Kabel Melebihi Kapasitas." },
  { "en": "Apa Fungsi Transformer Overload (ETAP)?", "id": "Trafo Kelebihan Beban." },
  { "en": "Apa Fungsi Generator Excitation (ETAP)?", "id": "Batas Penguatan Generator." },
  { "en": "Apa Fungsi Governor Setting (ETAP)?", "id": "Pengaturan Kecepatan Generator." },
  { "en": "Apa Fungsi Exciter Setting (ETAP)?", "id": "Pengaturan Tegangan Generator." },
  { "en": "Apa Fungsi Power System Stabilizer (ETAP)?", "id": "Penstabil Sistem Tenaga." },
  { "en": "Apa Fungsi Inertia Constant (ETAP)?", "id": "Konstanta Kelembaman Rotor." },
  { "en": "Apa Fungsi Subtransient Reactance (ETAP)?", "id": "Reaktansi Awal Hubung Singkat." },
  { "en": "Apa Fungsi Transient Reactance (ETAP)?", "id": "Reaktansi Saat Peralihan." },
  { "en": "Apa Fungsi Synchronous Reactance (ETAP)?", "id": "Reaktansi Saat Stabil." },
  { "en": "Apa Fungsi Zero Sequence Impedance (ETAP)?", "id": "Impedansi Urutan Nol." },
  { "en": "Apa Fungsi Negative Sequence Impedance (ETAP)?", "id": "Impedansi Urutan Negatif." },
  { "en": "Apa Fungsi Grounding Resistor (ETAP)?", "id": "Tahanan Pembumian Titik Netral." },
  { "en": "Apa Fungsi Grounding Reactor (ETAP)?", "id": "Reaktor Pembumian Titik Netral." },
  { "en": "Apa Fungsi Solid Grounding (ETAP)?", "id": "Pembumian Langsung Tanpa Tahanan." },
  { "en": "Apa Shortcut Ctrl + S (ETAP)?", "id": "Menyimpan Proyek." },
  { "en": "Apa Shortcut Ctrl + P (ETAP)?", "id": "Mencetak One Line Diagram." },
  { "en": "Apa Shortcut Zoom Fit (ETAP)?", "id": "Menampilkan Seluruh Diagram." },
  { "en": "Apa Shortcut Zoom Window (ETAP)?", "id": "Zoom Area Tertentu." },
  { "en": "Apa Fungsi Pan Tool (ETAP)?", "id": "Menggeser Tampilan Diagram." },
  { "en": "Apa Fungsi Ruler (GX Works)?", "id": "Penggaris Ukuran Langkah Ladder." },
  { "en": "Apa Fungsi Statement Comment (GX Works)?", "id": "Komentar Blok Ladder." },
  { "en": "Apa Fungsi Note (GX Works)?", "id": "Catatan Pada Output." },
  { "en": "Apa Fungsi Project Title (GX Works)?", "id": "Judul Proyek PLC." },
  { "en": "Apa Fungsi Project Property (GX Works)?", "id": "Informasi Detail Proyek." },
  { "en": "Apa Fungsi Device Initial Value (GX Works)?", "id": "Nilai Awal Saat Start." },
  { "en": "Apa Fungsi Latch Range Setting (GX Works)?", "id": "Rentang Memori Tahan Data." },
  { "en": "Apa Fungsi Table Style (AutoCAD)?", "id": "Mengatur Tampilan Tabel." },
  { "en": "Apa Fungsi Perintah Battman (AutoCAD)?", "id": "Mengelola Atribut Blok." },
  { "en": "Apa Fungsi Perintah Eattedit (AutoCAD)?", "id": "Edit Atribut Blok Langsung." },
  { "en": "Apa Fungsi Perintah Attdef (AutoCAD)?", "id": "Mendefinisikan Atribut Baru." },
  { "en": "Apa Fungsi Perintah Attdisp (AutoCAD)?", "id": "Mengatur Visibilitas Atribut." },
  { "en": "Apa Fungsi Perintah Field (AutoCAD)?", "id": "Membuat Teks Otomatis Berubah." },
  { "en": "Apa Fungsi Updatefield (AutoCAD)?", "id": "Memperbarui Nilai Field." },
  { "en": "Apa Fungsi Data Link (AutoCAD)?", "id": "Menghubungkan Tabel Ke Excel." },
  { "en": "Apa Fungsi Perintah Eattext (AutoCAD)?", "id": "Ekspor Atribut Ke Tabel." },
  { "en": "Apa Shortcut Ctrl + 9 (AutoCAD)?", "id": "Menampilkan Command Line." },
  { "en": "Apa Fungsi Perintah Wipeoutframe (AutoCAD)?", "id": "Mengatur Bingkai Wipeout." },
  { "en": "Apa Fungsi Perintah Imageframe (AutoCAD)?", "id": "Mengatur Bingkai Gambar." },
  { "en": "Apa Fungsi Xrefframe (AutoCAD)?", "id": "Mengatur Bingkai Referensi Eksternal." },
  { "en": "Apa Fungsi Perintah Olescale (AutoCAD)?", "id": "Mengatur Skala Objek OLE." },
  { "en": "Apa Fungsi Perintah Olelinks (AutoCAD)?", "id": "Mengatur Link Objek OLE." },
  { "en": "Apa Fungsi Perintah Insertobj (AutoCAD)?", "id": "Menyisipkan Objek Aplikasi Lain." },
  { "en": "Apa Fungsi Perintah Pastespec (AutoCAD)?", "id": "Paste Spesial Dengan Opsi." },
  { "en": "Apa Fungsi Serial Available (Arduino IDE)?", "id": "Cek Jumlah Byte Di Buffer." },
  { "en": "Apa Fungsi Serial Read (Arduino IDE)?", "id": "Membaca 1 Byte Data." },
  { "en": "Apa Fungsi Serial Peek (Arduino IDE)?", "id": "Baca Byte Tanpa Menghapusnya." },
  { "en": "Apa Fungsi Serial Flush (Arduino IDE)?", "id": "Menunggu Data Terkirim Selesai." },
  { "en": "Apa Fungsi Serial End (Arduino IDE)?", "id": "Menutup Komunikasi Serial." },
  { "en": "Apa Fungsi Serial ParseInt (Arduino IDE)?", "id": "Mencari Angka Integer Di Buffer." },
  { "en": "Apa Fungsi Serial ParseFloat (Arduino IDE)?", "id": "Mencari Angka Float Di Buffer." },
  { "en": "Apa Fungsi ReadBytes (Arduino IDE)?", "id": "Membaca Beberapa Byte Ke Buffer." },
  { "en": "Apa Fungsi ReadString (Arduino IDE)?", "id": "Membaca Input Sebagai String." },
  { "en": "Apa Fungsi String Trim (Arduino IDE)?", "id": "Menghapus Spasi Awal Akhir." },
  { "en": "Apa Fungsi String Length (Arduino IDE)?", "id": "Menghitung Panjang Karakter String." },
  { "en": "Apa Fungsi String Concat (Arduino IDE)?", "id": "Menggabungkan 2 String." },
  { "en": "Apa Fungsi String Equals (Arduino IDE)?", "id": "Membandingkan Isi 2 String." },
  { "en": "Apa Fungsi String IndexOf (Arduino IDE)?", "id": "Mencari Posisi Karakter." },
  { "en": "Apa Instruksi Double Compare (CX Programmer)?", "id": "Membandingkan Data Double Word." },
  { "en": "Apa Instruksi Multiple Compare (CX Programmer)?", "id": "Membandingkan Banyak Data Sekaligus." },
  { "en": "Apa Instruksi Table Compare (CX Programmer)?", "id": "Membandingkan Nilai Dengan Tabel." },
  { "en": "Apa Instruksi Block Compare (CX Programmer)?", "id": "Membandingkan Blok Data." },
  { "en": "Apa Instruksi Zone Compare (CX Programmer)?", "id": "Cek Nilai Dalam Rentang." },
  { "en": "Apa Instruksi Signed Compare (CX Programmer)?", "id": "Bandingkan Binary Bertanda." },
  { "en": "Apa Instruksi Double Signed (CX Programmer)?", "id": "Bandingkan Double Binary Bertanda." },
  { "en": "Apa Instruksi Area Range (CX Programmer)?", "id": "Cek Data Dalam Area Memori." },
  { "en": "Apa Instruksi Maximum Find (CX Programmer)?", "id": "Cari Nilai Terbesar Di Area." },
  { "en": "Apa Instruksi Minimum Find (CX Programmer)?", "id": "Cari Nilai Terkecil Di Area." },
  { "en": "Apa Instruksi Average Calc (CX Programmer)?", "id": "Hitung Rata Rata Area." },
  { "en": "Apa Instruksi Summation (CX Programmer)?", "id": "Menjumlahkan Seluruh Area." },
  { "en": "Apa Instruksi FCS Calculate (CX Programmer)?", "id": "Hitung Frame Check Sequence." },
  { "en": "Apa Instruksi Twos Complement (CX Programmer)?", "id": "Ubah Ke Bilangan Negatif." },
  { "en": "Apa Instruksi Double Neg (CX Programmer)?", "id": "Ubah Double Ke Negatif." },
  { "en": "Apa Fungsi Frequency Graph (Proteus)?", "id": "Grafik Respon Frekuensi Rangkaian." },
  { "en": "Apa Fungsi Fourier Graph (Proteus)?", "id": "Grafik Spektrum Frekuensi Sinyal." },
  { "en": "Apa Fungsi Noise Graph (Proteus)?", "id": "Grafik Tingkat Kebisingan Sinyal." },
  { "en": "Apa Fungsi Distortion Graph (Proteus)?", "id": "Grafik Distorsi Harmonisa." },
  { "en": "Apa Fungsi DC Sweep Graph (Proteus)?", "id": "Grafik Karakteristik DC Komponen." },
  { "en": "Apa Fungsi AC Sweep Graph (Proteus)?", "id": "Grafik Karakteristik AC Komponen." },
  { "en": "Apa Fungsi Transfer Function (Proteus)?", "id": "Grafik Fungsi Transfer Sistem." },
  { "en": "Apa Fungsi Conformance Graph (Proteus)?", "id": "Grafik Kesesuaian Digital." },
  { "en": "Apa Fungsi Digital Graph (Proteus)?", "id": "Grafik Waktu Sinyal Digital." },
  { "en": "Apa Fungsi Interactive Analysis (Proteus)?", "id": "Analisis Saat Simulasi Jalan." },
  { "en": "Apa Fungsi Transient Settings (Proteus)?", "id": "Mengatur Waktu Mulai Berhenti." },
  { "en": "Apa Fungsi Initial Conditions (Proteus)?", "id": "Kondisi Awal Voltase Kapasitor." },
  { "en": "Apa Fungsi Netlist Formatter (Proteus)?", "id": "Format Output Daftar Koneksi." },
  { "en": "Apa Fungsi BOM Template (Proteus)?", "id": "Template Daftar Komponen." },
  { "en": "Apa Fungsi Harmonic Flow (ETAP)?", "id": "Analisis Aliran Daya Harmonisa." },
  { "en": "Apa Fungsi Harmonic Library (ETAP)?", "id": "Pustaka Sumber Arus Harmonisa." },
  { "en": "Apa Fungsi Total Distortion (ETAP)?", "id": "Persentase Cacat Total Gelombang." },
  { "en": "Apa Fungsi Individual Distortion (ETAP)?", "id": "Cacat Pada Orde Tertentu." },
  { "en": "Apa Fungsi Harmonic Filter (ETAP)?", "id": "Penyaring Frekuensi Harmonisa." },
  { "en": "Apa Fungsi Single Tuned (ETAP)?", "id": "Filter 1 Frekuensi Khusus." },
  { "en": "Apa Fungsi High Pass (ETAP)?", "id": "Filter Lolos Frekuensi Tinggi." },
  { "en": "Apa Fungsi Frequency Scan (ETAP)?", "id": "Pindai Respon Frekuensi Sistem." },
  { "en": "Apa Fungsi Reliability Index (ETAP)?", "id": "Indeks Keandalan Sistem Tenaga." },
  { "en": "Apa Kepanjangan SAIFI (ETAP)?", "id": "System Average Interruption Frequency Index." },
  { "en": "Apa Kepanjangan SAIDI (ETAP)?", "id": "System Average Interruption Duration Index." },
  { "en": "Apa Kepanjangan CAIDI (ETAP)?", "id": "Customer Average Interruption Duration Index." },
  { "en": "Apa Fungsi Energy Assessment (ETAP)?", "id": "Penilaian Penggunaan Energi." },
  { "en": "Apa Fungsi Busway Library (ETAP)?", "id": "Data Spesifikasi Busway." },
  { "en": "Apa Fungsi CB Library (ETAP)?", "id": "Data Spesifikasi Pemutus Sirkuit." },
  { "en": "Apa Fungsi Relay Library (ETAP)?", "id": "Data Karakteristik Relay Proteksi." },
  { "en": "Apa Instruksi Float Add (GX Works)?", "id": "Tambah Bilangan Desimal FX." },
  { "en": "Apa Instruksi Float Sub (GX Works)?", "id": "Kurang Bilangan Desimal FX." },
  { "en": "Apa Instruksi Float Mul (GX Works)?", "id": "Kali Bilangan Desimal FX." },
  { "en": "Apa Instruksi Float Div (GX Works)?", "id": "Bagi Bilangan Desimal FX." },
  { "en": "Apa Instruksi Word Switch (GX Works)?", "id": "Switch Nilai Data Word." },
  { "en": "Apa Instruksi Digital Switch (GX Works)?", "id": "Baca Input Dip Switch." },
  { "en": "Apa Instruksi Read Module (GX Works)?", "id": "Baca Data Modul Khusus." },
  { "en": "Apa Instruksi Write Module (GX Works)?", "id": "Tulis Data Modul Khusus." },
  { "en": "Apa Instruksi Read Analog (GX Works)?", "id": "Baca Blok Analog FX." },
  { "en": "Apa Instruksi Write Analog (GX Works)?", "id": "Tulis Blok Analog FX." },
  { "en": "Apa Fungsi Buffer Memory (GX Works)?", "id": "Memori Modul Analog Cerdas." },
  { "en": "Apa Kode U (GX Works)?", "id": "Nomor Unit Modul Khusus." },
  { "en": "Apa Kode G (GX Works)?", "id": "Nomor Buffer Memory Modul." },
  { "en": "Apa Fungsi Local Variable (GX Works)?", "id": "Variabel Hanya Di POU." },
  { "en": "Apa Fungsi Global Variable (GX Works)?", "id": "Variabel Di Seluruh Proyek." },
  { "en": "Apa Fungsi System Variable (GX Works)?", "id": "Variabel Sistem PLC Bawaan." },
  { "en": "Apa Fungsi Retain Variable (GX Works)?", "id": "Variabel Tahan Saat Mati." },
  { "en": "Apa Fungsi Constant Variable (GX Works)?", "id": "Variabel Nilai Tetap." },
  { "en": "Apa Shortcut Ctrl + Q (GX Works)?", "id": "Keluar Dari Aplikasi." },
  { "en": "Apa Shortcut Ctrl + W (GX Works)?", "id": "Menutup Jendela Gambar." },
  { "en": "Apa Shortcut Alt + F4 (GX Works)?", "id": "Menutup Program Paksa." },
  { "en": "Apa Shortcut Alt + F11 (GX Works)?", "id": "Membuka Visual Basic Editor." },
  { "en": "Apa Shortcut Alt + F8 (GX Works)?", "id": "Menjalankan Macro VBA." },
  { "en": "Apa Fungsi Perintah Publish (AutoCAD)?", "id": "Mencetak Banyak Sheet Sekaligus." },
  { "en": "Apa Fungsi Perintah Archive (AutoCAD)?", "id": "Mengemas File Proyek Arsip." },
  { "en": "Apa Fungsi Export Layout (AutoCAD)?", "id": "Simpan Layout Ke Model Baru." },
  { "en": "Apa Fungsi Import Layout (AutoCAD)?", "id": "Ambil Layout Dari File Lain." },
  { "en": "Apa Fungsi Dimscale (AutoCAD)?", "id": "Mengatur Skala Global Dimensi." },
  { "en": "Apa Fungsi Dimasz (AutoCAD)?", "id": "Mengatur Ukuran Panah Dimensi." },
  { "en": "Apa Fungsi Dimtxt (AutoCAD)?", "id": "Mengatur Tinggi Teks Dimensi." },
  { "en": "Apa Fungsi Dimdec (AutoCAD)?", "id": "Mengatur Jumlah Desimal Dimensi." },
  { "en": "Apa Fungsi Celtscale (AutoCAD)?", "id": "Skala Garis Objek Saat Ini." },
  { "en": "Apa Fungsi Psltscale (AutoCAD)?", "id": "Skala Garis Pada Viewport Layout." },
  { "en": "Apa Fungsi Group Edit (AutoCAD)?", "id": "Menambah Atau Hapus Anggota Grup." },
  { "en": "Apa Fungsi Pedit (AutoCAD)?", "id": "Mengedit Garis Poligon Bersambung." },
  { "en": "Apa Opsi Join (AutoCAD)?", "id": "Menyambung Garis Menjadi Polyline." },
  { "en": "Apa Opsi Width (AutoCAD)?", "id": "Mengubah Ketebalan Garis Polyline." },
  { "en": "Apa Opsi Spline (AutoCAD)?", "id": "Melengkungkan Polyline Menjadi Kurva." },
  { "en": "Apa Opsi Decurve (AutoCAD)?", "id": "Luruskan Kembali Garis Kurva." },
  { "en": "Apa Fungsi Wire Begin (Arduino IDE)?", "id": "Memulai Bus Komunikasi I2C." },
  { "en": "Apa Fungsi BeginTransmission (Arduino IDE)?", "id": "Mulai Kirim Data Ke Slave." },
  { "en": "Apa Fungsi EndTransmission (Arduino IDE)?", "id": "Akhiri Pengiriman Data I2C." },
  { "en": "Apa Fungsi Wire Write (Arduino IDE)?", "id": "Kirim Byte Data I2C." },
  { "en": "Apa Fungsi Wire Read (Arduino IDE)?", "id": "Baca Byte Data I2C." },
  { "en": "Apa Fungsi RequestFrom (Arduino IDE)?", "id": "Minta Data Dari Slave I2C." },
  { "en": "Apa Fungsi SPI Begin (Arduino IDE)?", "id": "Memulai Bus Komunikasi SPI." },
  { "en": "Apa Fungsi SPI Transfer (Arduino IDE)?", "id": "Kirim Dan Terima Data SPI." },
  { "en": "Apa Fungsi setBitOrder (Arduino IDE)?", "id": "Atur Urutan Bit MSB LSB." },
  { "en": "Apa Fungsi setClockDivider (Arduino IDE)?", "id": "Atur Kecepatan Clock SPI." },
  { "en": "Apa Fungsi setDataMode (Arduino IDE)?", "id": "Atur Fase Dan Polaritas Clock." },
  { "en": "Apa Operator Bitwise AND (Arduino IDE)?", "id": "Logika AND Per Bit." },
  { "en": "Apa Operator Bitwise OR (Arduino IDE)?", "id": "Logika OR Per Bit." },
  { "en": "Apa Operator Bitwise XOR (Arduino IDE)?", "id": "Logika XOR Per Bit." },
  { "en": "Apa Operator Bitwise NOT (Arduino IDE)?", "id": "Membalik Semua Bit Data." },
  { "en": "Apa Fungsi Mode RISING (Arduino IDE)?", "id": "Picu Saat Sinyal Naik." },
  { "en": "Apa Fungsi Mode FALLING (Arduino IDE)?", "id": "Picu Saat Sinyal Turun." },
  { "en": "Apa Fungsi Mode CHANGE (Arduino IDE)?", "id": "Picu Saat Sinyal Berubah." },
  { "en": "Apa Instruksi Double Add (CX Programmer)?", "id": "Penjumlahan Data 2 Word." },
  { "en": "Apa Instruksi Double Sub (CX Programmer)?", "id": "Pengurangan Data 2 Word." },
  { "en": "Apa Instruksi Double Mul (CX Programmer)?", "id": "Perkalian Data 2 Word." },
  { "en": "Apa Instruksi Double Div (CX Programmer)?", "id": "Pembagian Data 2 Word." },
  { "en": "Apa Fungsi Index Register (CX Programmer)?", "id": "Pointer Alamat Memori Indirect." },
  { "en": "Apa Fungsi Data Register (CX Programmer)?", "id": "Offset Untuk Index Register." },
  { "en": "Apa Simbol Prefix Keong (CX Programmer)?", "id": "Eksekusi Hanya Sekali (Diferensial)." },
  { "en": "Apa Simbol Prefix Persen (CX Programmer)?", "id": "Menunjukkan Alamat Memori Fisik." },
  { "en": "Apa Fungsi Area H (CX Programmer)?", "id": "Memori Tahan Saat Listrik Mati." },
  { "en": "Apa Fungsi Area A (CX Programmer)?", "id": "Memori Status Sistem PLC." },
  { "en": "Apa Fungsi Area T (CX Programmer)?", "id": "Menyimpan Nilai Waktu Timer." },
  { "en": "Apa Fungsi Area C (CX Programmer)?", "id": "Menyimpan Nilai Hitungan Counter." },
  { "en": "Apa Instruksi Move Digit (CX Programmer)?", "id": "Pindahkan Digit Tertentu Data." },
  { "en": "Apa Instruksi Move Bit (CX Programmer)?", "id": "Pindahkan Bit Tertentu Data." },
  { "en": "Apa Fungsi Trace Mode (CX Programmer)?", "id": "Rekam Data Siklus Scan." },
  { "en": "Apa Fungsi Gerber Viewer (Proteus)?", "id": "Melihat Hasil File Produksi." },
  { "en": "Apa Fungsi Pre-Production Check (Proteus)?", "id": "Cek Error Sebelum Cetak PCB." },
  { "en": "Apa Fungsi Drill Table (Proteus)?", "id": "Tabel Ukuran Lubang Bor." },
  { "en": "Apa Fungsi Layer Stackup (Proteus)?", "id": "Atur Susunan Lapisan PCB." },
  { "en": "Apa Fungsi Inner Layer 1 (Proteus)?", "id": "Lapisan Tembaga Dalam Pertama." },
  { "en": "Apa Fungsi Inner Layer 2 (Proteus)?", "id": "Lapisan Tembaga Dalam Kedua." },
  { "en": "Apa Fungsi Blind Via (Proteus)?", "id": "Via Dari Luar Ke Dalam." },
  { "en": "Apa Fungsi Buried Via (Proteus)?", "id": "Via Tertanam Di Lapisan Dalam." },
  { "en": "Apa Fungsi 3D Settings (Proteus)?", "id": "Atur Kualitas Render 3D." },
  { "en": "Apa Fungsi STEP Export (Proteus)?", "id": "Ekspor Model 3D Ke CAD." },
  { "en": "Apa Fungsi Pick And Place (Proteus)?", "id": "File Koordinat Penempatan Komponen." },
  { "en": "Apa Fungsi ODB++ Output (Proteus)?", "id": "Format Data Manufaktur Canggih." },
  { "en": "Apa Fungsi Ground Grid (ETAP)?", "id": "Sistem Jaring Pembumian Gardu." },
  { "en": "Apa Fungsi FEM (ETAP)?", "id": "Metode Hitung Elemen Hingga." },
  { "en": "Apa Fungsi Step Voltage (ETAP)?", "id": "Tegangan Langkah Kaki Manusia." },
  { "en": "Apa Fungsi Touch Voltage (ETAP)?", "id": "Tegangan Sentuh Tangan Manusia." },
  { "en": "Apa Fungsi GPR (ETAP)?", "id": "Kenaikan Potensial Tanah." },
  { "en": "Apa Fungsi Surface Material (ETAP)?", "id": "Lapisan Batu Kerikil Permukaan." },
  { "en": "Apa Fungsi Soil Resistivity (ETAP)?", "id": "Tahanan Jenis Tanah." },
  { "en": "Apa Fungsi Reflection Factor (ETAP)?", "id": "Faktor Pantulan Lapisan Tanah." },
  { "en": "Apa Fungsi Grid Conductor (ETAP)?", "id": "Kabel Tembaga Jaring Tanah." },
  { "en": "Apa Fungsi Ground Rod (ETAP)?", "id": "Batang Tembaga Tanam Vertikal." },
  { "en": "Apa Fungsi Decrement Factor (ETAP)?", "id": "Faktor Penurunan Arus DC." },
  { "en": "Apa Fungsi Split Factor (ETAP)?", "id": "Faktor Pembagi Arus Gangguan." },
  { "en": "Apa Fungsi Ground Grid Report (ETAP)?", "id": "Laporan Analisis Keamanan Tanah." },
  { "en": "Apa Instruksi Block Reset (GX Works)?", "id": "Reset Banyak Bit Sekaligus." },
  { "en": "Apa Instruksi Block Add (GX Works)?", "id": "Jumlahkan Data Blok Memori." },
  { "en": "Apa Instruksi Block Sub (GX Works)?", "id": "Kurangkan Data Blok Memori." },
  { "en": "Apa Instruksi Byte Swap (GX Works)?", "id": "Tukar Posisi Byte Data." },
  { "en": "Apa Instruksi Word To Byte (GX Works)?", "id": "Pisah Word Jadi Byte." },
  { "en": "Apa Instruksi Byte To Word (GX Works)?", "id": "Gabung Byte Jadi Word." },
  { "en": "Apa Instruksi Gray Code (GX Works)?", "id": "Konversi Biner Ke Gray Code." },
  { "en": "Apa Instruksi Gray To Bin (GX Works)?", "id": "Konversi Gray Code Ke Biner." },
  { "en": "Apa Fungsi Remote Run (GX Works)?", "id": "Jalankan PLC Dari Komputer." },
  { "en": "Apa Fungsi Remote Stop (GX Works)?", "id": "Hentikan PLC Dari Komputer." },
  { "en": "Apa Fungsi Remote Pause (GX Works)?", "id": "Jeda PLC Dari Komputer." },
  { "en": "Apa Fungsi Program Check (GX Works)?", "id": "Cek Logika Program." },
  { "en": "Apa Fungsi Write To PLC (GX Works)?", "id": "Transfer Program Ke PLC." },
  { "en": "Apa Fungsi Read From PLC (GX Works)?", "id": "Ambil Program Dari PLC." },
  { "en": "Apa Fungsi Zoom 100% (GX Works)?", "id": "Tampilan Ukuran Asli." },
  { "en": "Apa Fungsi Zoom 75% (GX Works)?", "id": "Tampilan Diperkecil Sedikit." },
  { "en": "Apa Shortcut Ctrl + G (AutoCAD)?", "id": "Grup Objek." },
  { "en": "Apa Shortcut Ctrl + Shift + G (AutoCAD)?", "id": "Ungroup Objek." },
  { "en": "Apa Shortcut Ctrl + L (AutoCAD)?", "id": "Mode Ortho Toggle." },
  { "en": "Apa Shortcut Ctrl + D (AutoCAD)?", "id": "Mode Dynamic UCS Toggle." },
  { "en": "Apa Shortcut Ctrl + E (AutoCAD)?", "id": "Ganti Bidang Isometrik." },
  { "en": "Apa Fungsi Laywalk (AutoCAD)?", "id": "Menjelajahi Layer 1 Per 1." },
  { "en": "Apa Fungsi Layiso (AutoCAD)?", "id": "Mengisolasi Layer Objek Terpilih." },
  { "en": "Apa Fungsi Layuniso (AutoCAD)?", "id": "Mengembalikan Layer Diisolasi." },
  { "en": "Apa Fungsi Laymcur (AutoCAD)?", "id": "Jadikan Layer Objek Sebagai Aktif." },
  { "en": "Apa Fungsi Layoff (AutoCAD)?", "id": "Mematikan Layer Objek Terpilih." },
  { "en": "Apa Fungsi Layon (AutoCAD)?", "id": "Menyalakan Semua Layer." },
  { "en": "Apa Fungsi Laythw (AutoCAD)?", "id": "Mencairkan Semua Layer Beku." },
  { "en": "Apa Fungsi Laylck (AutoCAD)?", "id": "Mengunci Layer Objek Terpilih." },
  { "en": "Apa Fungsi Layulck (AutoCAD)?", "id": "Membuka Kunci Layer Objek." },
  { "en": "Apa Fungsi Texttofront (AutoCAD)?", "id": "Membawa Teks Ke Depan Objek." },
  { "en": "Apa Fungsi Sendtoback (AutoCAD)?", "id": "Mengirim Objek Ke Belakang." },
  { "en": "Apa Fungsi Bringtofront (AutoCAD)?", "id": "Membawa Objek Ke Depan." },
  { "en": "Apa Shortcut Ctrl + R (AutoCAD)?", "id": "Pindah Antar Viewport Layout." },
  { "en": "Apa Shortcut Ctrl + Shift + H (AutoCAD)?", "id": "Sembunyikan Atau Tampilkan Palet." },
  { "en": "Apa Shortcut Ctrl + Shift + I (AutoCAD)?", "id": "Mengaktifkan Infer Constraints." },
  { "en": "Apa Fungsi Visretain (AutoCAD)?", "id": "Mengatur Visibilitas Layer Xref." },
  { "en": "Apa Fungsi Proxyshow (AutoCAD)?", "id": "Menampilkan Objek Proxy." },
  { "en": "Apa Fungsi Pdmode (AutoCAD)?", "id": "Mengatur Tampilan Objek Point." },
  { "en": "Apa Fungsi Pdsize (AutoCAD)?", "id": "Mengatur Ukuran Objek Point." },
  { "en": "Apa Fungsi Sketch (AutoCAD)?", "id": "Membuat Garis Sketsa Tangan Bebas." },
  { "en": "Apa Fungsi Bit (Arduino IDE)?", "id": "Menghitung Nilai Bit Tertentu." },
  { "en": "Apa Fungsi AnalogWriteResolution (Arduino IDE)?", "id": "Mengatur Resolusi Output PWM." },
  { "en": "Apa Fungsi AnalogReadResolution (Arduino IDE)?", "id": "Mengatur Resolusi Input Analog." },
  { "en": "Apa Fungsi ShiftIn (Arduino IDE)?", "id": "Menerima Data Bit Bergeser." },
  { "en": "Apa Fungsi Tone (Arduino IDE)?", "id": "Menghasilkan Gelombang Suara Kotak." },
  { "en": "Apa Fungsi NoTone (Arduino IDE)?", "id": "Menghentikan Output Suara." },
  { "en": "Apa Fungsi Unsigned Char (Arduino IDE)?", "id": "Tipe Data 1 Byte Positif." },
  { "en": "Apa Fungsi Short (Arduino IDE)?", "id": "Tipe Data Integer 16 Bit." },
  { "en": "Apa Fungsi Double (Arduino IDE)?", "id": "Bilangan Desimal Presisi Ganda." },
  { "en": "Apa Fungsi Exit (Arduino IDE)?", "id": "Menghentikan Program Arduino." },
  { "en": "Apa Fungsi Yield (Arduino IDE)?", "id": "Memberi Waktu Tugas Latar Belakang." },
  { "en": "Apa Fungsi Stream Read (Arduino IDE)?", "id": "Membaca Karakter Berikutnya." },
  { "en": "Apa Fungsi Stream Available (Arduino IDE)?", "id": "Cek Data Tersedia Di Stream." },
  { "en": "Apa Fungsi Library SPI (Arduino IDE)?", "id": "Library Komunikasi Serial Periferal." },
  { "en": "Apa Fungsi Library Wire (Arduino IDE)?", "id": "Library Komunikasi I2C." },
  { "en": "Apa Instruksi Interrupt Refresh (CX Programmer)?", "id": "Menyegarkan Input Interrupt." },
  { "en": "Apa Instruksi Disable Interrupts (CX Programmer)?", "id": "Mematikan Interupsi Sementara." },
  { "en": "Apa Instruksi Enable Interrupts (CX Programmer)?", "id": "Mengaktifkan Kembali Interupsi." },
  { "en": "Apa Instruksi Interrupt Mask (CX Programmer)?", "id": "Mengatur Masker Interupsi." },
  { "en": "Apa Instruksi Clear Interrupt (CX Programmer)?", "id": "Menghapus Data Interupsi." },
  { "en": "Apa Instruksi Network Receive (CX Programmer)?", "id": "Menerima Data Dari Jaringan." },
  { "en": "Apa Instruksi Network Send (CX Programmer)?", "id": "Mengirim Data Ke Jaringan." },
  { "en": "Apa Instruksi Start Up (CX Programmer)?", "id": "Mengubah Parameter Port Serial." },
  { "en": "Apa Instruksi Decoder (CX Programmer)?", "id": "Konversi Hex Ke 7 Segment." },
  { "en": "Apa Instruksi Multi Timer (CX Programmer)?", "id": "Timer Dengan Banyak Output." },
  { "en": "Apa Fungsi Triangle Generator (Proteus)?", "id": "Pembangkit Sinyal Segitiga." },
  { "en": "Apa Fungsi Excite Generator (Proteus)?", "id": "Sumber Eksitasi Jembatan Wheatstone." },
  { "en": "Apa Fungsi EasyHDL (Proteus)?", "id": "Bahasa Deskripsi Hardware Sederhana." },
  { "en": "Apa Fungsi Scripting Interface (Proteus)?", "id": "Antarmuka Kontrol Simulasi Eksternal." },
  { "en": "Apa Fungsi VSM Studio (Proteus)?", "id": "IDE Coding Mikrokontroler Internal." },
  { "en": "Apa Fungsi Compiler Options (Proteus)?", "id": "Pengaturan Kompilator Kode." },
  { "en": "Apa Fungsi Debugging Window (Proteus)?", "id": "Jendela Pelacakan Error Kode." },
  { "en": "Apa Fungsi Watch Point (Proteus)?", "id": "Pantau Variabel Saat Simulasi." },
  { "en": "Apa Fungsi Source Code (Proteus)?", "id": "Tab Editor Kode Program." },
  { "en": "Apa Fungsi Variable Dump (Proteus)?", "id": "Melihat Semua Nilai Variabel." },
  { "en": "Apa Fungsi Step Over (Proteus)?", "id": "Lewati Fungsi Saat Debugging." },
  { "en": "Apa Fungsi Step Into (Proteus)?", "id": "Masuk Fungsi Saat Debugging." },
  { "en": "Apa Fungsi Step Out (Proteus)?", "id": "Keluar Fungsi Saat Debugging." },
  { "en": "Apa Fungsi Busbar Sizing (ETAP)?", "id": "Menentukan Dimensi Busbar." },
  { "en": "Apa Fungsi Transformer Sizing (ETAP)?", "id": "Menentukan Kapasitas Trafo." },
  { "en": "Apa Fungsi Generator Sizing (ETAP)?", "id": "Menentukan Kapasitas Generator." },
  { "en": "Apa Fungsi Inverter Sizing (ETAP)?", "id": "Menentukan Kapasitas Inverter." },
  { "en": "Apa Fungsi Charger Sizing (ETAP)?", "id": "Menentukan Kapasitas Charger Baterai." },
  { "en": "Apa Fungsi Filter Sizing (ETAP)?", "id": "Menentukan Parameter Filter Harmonisa." },
  { "en": "Apa Fungsi Parameter Estimation (ETAP)?", "id": "Estimasi Data Motor Tidak Lengkap." },
  { "en": "Apa Fungsi Cable Estimation (ETAP)?", "id": "Estimasi Impedansi Kabel." },
  { "en": "Apa Fungsi Line Estimation (ETAP)?", "id": "Estimasi Impedansi Saluran Transmisi." },
  { "en": "Apa Fungsi Result Analyzer (ETAP)?", "id": "Analisis Perbandingan Hasil Studi." },
  { "en": "Apa Fungsi Data Exchange (ETAP)?", "id": "Pertukaran Data Antar Aplikasi." },
  { "en": "Apa Fungsi Excel Import (ETAP)?", "id": "Impor Data Dari Excel." },
  { "en": "Apa Fungsi Project Merge (ETAP)?", "id": "Menggabungkan 2 File Proyek." },
  { "en": "Apa Instruksi Serial Read (GX Works)?", "id": "Membaca Data Serial Modul." },
  { "en": "Apa Instruksi Serial Write (GX Works)?", "id": "Menulis Data Serial Modul." },
  { "en": "Apa Instruksi Modbus Req (GX Works)?", "id": "Permintaan Komunikasi Modbus." },
  { "en": "Apa Instruksi Link Output (GX Works)?", "id": "Output Ke Network Module." },
  { "en": "Apa Instruksi Link Input (GX Works)?", "id": "Input Dari Network Module." },
  { "en": "Apa Instruksi File Open (GX Works)?", "id": "Membuka File Di Memori." },
  { "en": "Apa Instruksi File Close (GX Works)?", "id": "Menutup File Di Memori." },
  { "en": "Apa Instruksi File Read (GX Works)?", "id": "Baca Data Dari File." },
  { "en": "Apa Instruksi File Write (GX Works)?", "id": "Tulis Data Ke File." },
  { "en": "Apa Fungsi IE Field (GX Works)?", "id": "Jaringan Ethernet Industri Mitsubishi." },
  { "en": "Apa Fungsi Motion Module (GX Works)?", "id": "Modul Kontrol Gerak Sederhana." },
  { "en": "Apa Fungsi IO Assignment (GX Works)?", "id": "Penetapan Alamat Modul Fisik." },
  { "en": "Apa Fungsi System Tab (GX Works)?", "id": "Tab Pengaturan Sistem PLC." },
  { "en": "Apa Fungsi Clear Memory (GX Works)?", "id": "Menghapus Semua Program PLC." },
  { "en": "Apa Fungsi SD Format (GX Works)?", "id": "Format Kartu Memori SD." },
  { "en": "Apa Fungsi Connection Test (GX Works)?", "id": "Tes Sambungan Kabel Komunikasi." },
  { "en": "Apa Shortcut Shift + Klik (AutoCAD)?", "id": "Menu Snap Objek Sementara." },
  { "en": "Apa Shortcut Ctrl + PageUp (AutoCAD)?", "id": "Pindah Tab Layout Sebelumnya." },
  { "en": "Apa Shortcut Ctrl + PageDown (AutoCAD)?", "id": "Pindah Tab Layout Berikutnya." },
  { "en": "Apa Shortcut F4 (AutoCAD)?", "id": "Toggle 3D Osnap." },
  { "en": "Apa Shortcut F6 (AutoCAD)?", "id": "Toggle Dynamic UCS." },
  { "en": "Apa Shortcut Alt + F11 (AutoCAD)?", "id": "Membuka Editor VBA." },
  { "en": "Apa Shortcut Ctrl + Shift + P (AutoCAD)?", "id": "Toggle Quick Properties." },
  { "en": "Apa Fungsi Perintah Solview (AutoCAD)?", "id": "Membuat Tampilan Ortografi, Dari Objek 3D." },
  { "en": "Apa Fungsi Perintah Soldraw (AutoCAD)?", "id": "Menghasilkan Profil 2D, Dari Solview." },
  { "en": "Apa Fungsi Perintah Solprof (AutoCAD)?", "id": "Membuat Profil Blok, Dari Objek Solid." },
  { "en": "Apa Fungsi Perintah Section (AutoCAD)?", "id": "Membuat Irisan Bidang, Dari Objek 3D." },
  { "en": "Apa Fungsi Perintah Interfere (AutoCAD)?", "id": "Mengecek Tabrakan Fisik, Antar Objek 3D." },
  { "en": "Apa Fungsi Perintah Render (AutoCAD)?", "id": "Membuat Gambar Realistik, Bertekstur Cahaya." },
  { "en": "Apa Fungsi Perintah Light (AutoCAD)?", "id": "Menambah Sumber Cahaya, Dalam Desain." },
  { "en": "Apa Fungsi Perintah Sunproperties (AutoCAD)?", "id": "Mengatur Cahaya Matahari, Secara Realistik." },
  { "en": "Apa Fungsi Perintah Materialmap (AutoCAD)?", "id": "Mengatur Letak Tekstur, Pada Objek." },
  { "en": "Apa Fungsi Perintah Anipath (AutoCAD)?", "id": "Membuat Animasi Kamera, Mengikuti Jalur." },
  { "en": "Apa Fungsi Perintah 3DConfig (AutoCAD)?", "id": "Mengatur Optimasi Kartu Grafis, Perangkat Keras." },
  { "en": "Apa Fungsi Perintah Vpoint (AutoCAD)?", "id": "Mengatur Sudut Pandang, Secara Numerik." },
  { "en": "Apa Fungsi Perintah Plan (AutoCAD)?", "id": "Mengembalikan Pandangan, Ke Arah Atas." },
  { "en": "Apa Fungsi Perintah Box (AutoCAD)?", "id": "Membuat Objek Padat, Berbentuk Kotak." },
  { "en": "Apa Fungsi Perintah Sphere (AutoCAD)?", "id": "Membuat Objek Padat, Berbentuk Bola." },
  { "en": "Apa Fungsi Perintah Cylinder (AutoCAD)?", "id": "Membuat Objek Padat, Berbentuk Tabung." },
  { "en": "Apa Fungsi Perintah Cone (AutoCAD)?", "id": "Membuat Objek Padat, Berbentuk Kerucut." },
  { "en": "Apa Fungsi Perintah Torus (AutoCAD)?", "id": "Membuat Objek Padat, Berbentuk Donat." },
  { "en": "Apa Fungsi Perintah Pyramid (AutoCAD)?", "id": "Membuat Objek Padat, Berbentuk Limas." },
  { "en": "Apa Fungsi Perintah Wedge (AutoCAD)?", "id": "Membuat Objek Padat, Berbentuk Pasak." },
  { "en": "Apa Fungsi Register TCNT1 (Arduino IDE)?", "id": "Menyimpan Nilai Cacahan, Timer 1." },
  { "en": "Apa Fungsi Register OCR1A (Arduino IDE)?", "id": "Menyimpan Nilai Perbandingan, Output A." },
  { "en": "Apa Fungsi Register ICR1 (Arduino IDE)?", "id": "Menyimpan Nilai Puncak, Gelombang PWM." },
  { "en": "Apa Fungsi Library LiquidCrystal_I2C (Arduino IDE)?", "id": "Mengontrol Layar LCD, Lewat I2C." },
  { "en": "Apa Fungsi Library MFRC522 (Arduino IDE)?", "id": "Mengontrol Modul Pembaca, Kartu RFID." },
  { "en": "Apa Fungsi Library DHT (Arduino IDE)?", "id": "Membaca Data Sensor, Suhu Kelembapan." },
  { "en": "Apa Fungsi Library Adafruit_GFX (Arduino IDE)?", "id": "Library Dasar Grafis, Layar OLED." },
  { "en": "Apa Fungsi Library RTClib (Arduino IDE)?", "id": "Mengatur Waktu Realtime, Modul RTC." },
  { "en": "Apa Fungsi Library Servo (Arduino IDE)?", "id": "Mengontrol Posisi Sudut, Motor Servo." },
  { "en": "Apa Fungsi Keyword Unsigned Long (Arduino IDE)?", "id": "Bilangan Bulat Besar, Tanpa Negatif." },
  { "en": "Apa Fungsi Keyword Boolean (Arduino IDE)?", "id": "Tipe Data Logika, Benar Salah." },
  { "en": "Apa Fungsi Fungsi Serial.println (Arduino IDE)?", "id": "Kirim Data Serial, Baris Baru." },
  { "en": "Apa Fungsi Fungsi Map (Arduino IDE)?", "id": "Memetakan Rentang Nilai, Secara Linear." },
  { "en": "Apa Fungsi Fungsi Constrain (Arduino IDE)?", "id": "Membatasi Nilai, Dalam Rentang Tertentu." },
  { "en": "Apa Fungsi Fungsi PulseIn (Arduino IDE)?", "id": "Membaca Panjang Pulsa, Dari Pin." },
  { "en": "Apa Instruksi BCNT (CX Programmer)?", "id": "Menghitung Jumlah Bit, Kondisi ON." },
  { "en": "Apa Instruksi SDEC (CX Programmer)?", "id": "Konversi Hexadesimal, Menjadi 7-Segment." },
  { "en": "Apa Instruksi HEX (CX Programmer)?", "id": "Konversi Kode ASCII, Menjadi Hexadesimal." },
  { "en": "Apa Instruksi ASC (CX Programmer)?", "id": "Konversi Hexadesimal, Menjadi Kode ASCII." },
  { "en": "Apa Instruksi SIGN (CX Programmer)?", "id": "Ubah Nilai Positif, Menjadi Negatif." },
  { "en": "Apa Instruksi AVG (CX Programmer)?", "id": "Menghitung Nilai Rata-Rata, Banyak Data." },
  { "en": "Apa Instruksi SQR (CX Programmer)?", "id": "Menghitung Akar Kuadrat, Suatu Bilangan." },
  { "en": "Apa Instruksi PWR (CX Programmer)?", "id": "Menghitung Hasil Pangkat, Suatu Bilangan." },
  { "en": "Apa Instruksi LOG (CX Programmer)?", "id": "Menghitung Logaritma Natural, Suatu Bilangan." },
  { "en": "Apa Instruksi EXP (CX Programmer)?", "id": "Menghitung Nilai Eksponensial, Suatu Bilangan." },
  { "en": "Apa Instruksi SIN (CX Programmer)?", "id": "Menghitung Nilai Sinus, Sudut Radian." },
  { "en": "Apa Instruksi COS (CX Programmer)?", "id": "Menghitung Nilai Cosinus, Sudut Radian." },
  { "en": "Apa Instruksi TAN (CX Programmer)?", "id": "Menghitung Nilai Tangen, Sudut Radian." },
  { "en": "Apa Instruksi ASIN (CX Programmer)?", "id": "Menghitung Invers Sinus, Suatu Bilangan." },
  { "en": "Apa Instruksi ACOS (CX Programmer)?", "id": "Menghitung Invers Cosinus, Suatu Bilangan." },
  { "en": "Apa Fungsi Design Rule Manager (Proteus)?", "id": "Mengatur Batasan Fisik, Pembuatan PCB." },
  { "en": "Apa Fungsi Pin Swap (Proteus)?", "id": "Menukar Pin Komponen, Saat Routing." },
  { "en": "Apa Fungsi Gate Swap (Proteus)?", "id": "Menukar Gerbang Logika, Saat Routing." },
  { "en": "Apa Fungsi Component Re-Annotator (Proteus)?", "id": "Memberi Nomor Ulang, Semua Komponen." },
  { "en": "Apa Fungsi Mechanical Layer (Proteus)?", "id": "Lapisan Informasi Fisik, Luar Jalur." },
  { "en": "Apa Fungsi 3D Front View (Proteus)?", "id": "Melihat Tampilan Depan, Objek PCB." },
  { "en": "Apa Fungsi 3D Back View (Proteus)?", "id": "Melihat Tampilan Belakang, Objek PCB." },
  { "en": "Apa Fungsi Drill Density (Proteus)?", "id": "Informasi Kepadatan Lubang, Pada PCB." },
  { "en": "Apa Fungsi Board Statistics (Proteus)?", "id": "Melihat Ringkasan Detail, Desain PCB." },
  { "en": "Apa Fungsi Netlist Importer (Proteus)?", "id": "Memasukkan Daftar Koneksi, Ke Ares." },
  { "en": "Apa Fungsi Auto-Placer (Proteus)?", "id": "Menempatkan Komponen Otomatis, Pada PCB." },
  { "en": "Apa Fungsi Live DRC (Proteus)?", "id": "Cek Aturan Desain, Secara Langsung." },
  { "en": "Apa Fungsi Thermal Relief (Proteus)?", "id": "Koneksi Pad, Ke Area Tembaga." },
  { "en": "Apa Fungsi Corner Mitering (Proteus)?", "id": "Menghaluskan Sudut Jalur, Yang Tajam." },
  { "en": "Apa Fungsi Length Tuning (Proteus)?", "id": "Menyamakan Panjang Jalur, Sinyal Cepat." },
  { "en": "Apa Fungsi Harmonic Library (ETAP)?", "id": "Menyimpan Model Sumber, Gangguan Harmonisa." },
  { "en": "Apa Fungsi Motor Starter (ETAP)?", "id": "Simulasi Perangkat Pengasutan, Motor Listrik." },
  { "en": "Apa Fungsi Capacitor Bank (ETAP)?", "id": "Perangkat Kompensasi Daya, Faktor Daya." },
  { "en": "Apa Fungsi Static Var Compensator (ETAP)?", "id": "Kompensator Daya Reaktif, Secara Dinamis." },
  { "en": "Apa Fungsi Phase Shifting Transformer (ETAP)?", "id": "Mengatur Aliran Daya, Sudut Fasa." },
  { "en": "Apa Fungsi Harmonic Distortion Limit (ETAP)?", "id": "Batas Maksimal Gangguan, Gelombang Harmonisa." },
  { "en": "Apa Fungsi Frequency Scan (ETAP)?", "id": "Melihat Karakteristik Impedansi, Terhadap Frekuensi." },
  { "en": "Apa Fungsi Alert Summary (ETAP)?", "id": "Ringkasan Seluruh Kondisi, Sistem Kritis." },
  { "en": "Apa Fungsi Report Manager (ETAP)?", "id": "Mengelola Dan Mencetak, Laporan Analisis." },
  { "en": "Apa Fungsi Scenario Wizard (ETAP)?", "id": "Membuat Berbagai Kondisi, Operasi Jaringan." },
  { "en": "Apa Fungsi Configuration Manager (ETAP)?", "id": "Mengatur Status Pemutus, Di Diagram." },
  { "en": "Apa Fungsi Grounding Analysis (ETAP)?", "id": "Analisis Keamanan Sistem, Terhadap Tanah." },
  { "en": "Apa Fungsi Voltage Stability (ETAP)?", "id": "Analisis Batas Tegangan, Menghindari Blackout." },
  { "en": "Apa Fungsi Optimal Power Flow (ETAP)?", "id": "Pengaturan Aliran Daya, Paling Efisien." },
  { "en": "Apa Fungsi Reliability Assessment (ETAP)?", "id": "Menghitung Probabilitas Gangguan, Sistem Tenaga." },
  { "en": "Apa Fungsi Special Relay SM400 (GX Works)?", "id": "Kontak Yang Selalu, Kondisi ON." },
  { "en": "Apa Fungsi Special Relay SM401 (GX Works)?", "id": "Kontak Yang Selalu, Kondisi OFF." },
  { "en": "Apa Fungsi Special Relay SM402 (GX Works)?", "id": "Kontak ON Sesaat, Saat Start." },
  { "en": "Apa Fungsi Special Relay SM412 (GX Works)?", "id": "Kontak Detak Waktu, 1 Detik." },
  { "en": "Apa Fungsi Special Relay SM413 (GX Works)?", "id": "Kontak Detak Waktu, 2 Detik." },
  { "en": "Apa Fungsi Special Register SD0 (GX Works)?", "id": "Menyimpan Kode Kesalahan, Sistem PLC." },
  { "en": "Apa Fungsi Special Register SD210 (GX Works)?", "id": "Menyimpan Informasi Waktu, Scan Program." },
  { "en": "Apa Fungsi Global Label (GX Works)?", "id": "Variabel Yang Diakses, Seluruh Program." },
  { "en": "Apa Fungsi Local Label (GX Works)?", "id": "Variabel Yang Diakses, Satu Program." },
  { "en": "Apa Fungsi Project Tree (GX Works)?", "id": "Navigasi Folder Dan Data, Proyek." },
  { "en": "Apa Fungsi Device Test (GX Works)?", "id": "Mengubah Nilai Bit, Saat Simulasi." },
  { "en": "Apa Fungsi Batch Monitor (GX Works)?", "id": "Memantau Banyak Alamat, Secara Serentak." },
  { "en": "Apa Fungsi Ladder Monitoring (GX Works)?", "id": "Melihat Aliran Logika, Secara Realtime." },
  { "en": "Apa Fungsi PLC Read (GX Works)?", "id": "Mengambil Data Program, Dari Hardware." },
  { "en": "Apa Fungsi PLC Write (GX Works)?", "id": "Mengirim Data Program, Ke Hardware." },
  { "en": "Apa Fungsi Simulation Start (GX Works)?", "id": "Menjalankan PLC Virtual, Tanpa Hardware." },
  { "en": "Apa Shortcut F4 (GX Works)?", "id": "Melakukan Kompilasi Program, Yang Dibuat." },
  { "en": "Apa Shortcut Shift + F3 (GX Works)?", "id": "Mengubah Mode Monitor, Secara Cepat." },
  { "en": "Apa Shortcut Ctrl + F10 (GX Works)?", "id": "Membuka Menu Pencarian, Alamat Device." },
  { "en": "Apa Shortcut Ctrl + Shift + F (GX Works)?", "id": "Mencari Teks Tertentu, Seluruh Proyek." },
  { "en": "Apa Shortcut F2 (GX Works)?", "id": "Berpindah Antara Mode Tulis dan Baca." },
  { "en": "Apa Shortcut F3 (GX Works)?", "id": "Mengaktifkan Mode Monitor Pada Program." },
  { "en": "Apa Shortcut F5 (GX Works)?", "id": "Membuat Kontak Normally Open (NO)." },
  { "en": "Apa Shortcut F6 (GX Works)?", "id": "Membuat Kontak Normally Closed (NC)." },
  { "en": "Apa Shortcut F7 (GX Works)?", "id": "Memasukkan Instruksi Out (Coil)." },
  { "en": "Apa Shortcut F8 (GX Works)?", "id": "Memasukkan Instruksi Khusus atau Function Block." },
  { "en": "Apa Shortcut Shift + F5 (GX Works)?", "id": "Membuat Kontak NO Secara Paralel." },
  { "en": "Apa Shortcut Shift + F7 (GX Works)?", "id": "Membuat Instruksi Out Secara Paralel." },
  { "en": "Apa Shortcut Ctrl + F4 (GX Works)?", "id": "Melakukan Konversi (Compile) Baris Saat Ini." },
  { "en": "Apa Shortcut Alt + F1 (GX Works)?", "id": "Membuka Jendela Device Comment." },
  { "en": "Apa Shortcut Ctrl + S (GX Works)?", "id": "Menyimpan Proyek Yang Sedang Dikerjakan." },
  { "en": "Apa Shortcut Ctrl + Z (GX Works)?", "id": "Membatalkan Perintah Terakhir (Undo)." },
  { "en": "Apa Shortcut Ctrl + Y (GX Works)?", "id": "Mengulangi Perintah Yang Dibatalkan (Redo)." },
  { "en": "Apa Shortcut Ctrl + N (GX Works)?", "id": "Membuat Proyek Baru Pada Software." },
  { "en": "Apa Shortcut Ctrl + O (GX Works)?", "id": "Membuka Proyek Yang Sudah Ada." },
  { "en": "Apa Shortcut Ctrl + P (GX Works)?", "id": "Mencetak Program Ladder Ke Kertas." },
  { "en": "Apa Fungsi Instruksi MOV?", "id": "Memindahkan Data Dari Satu Register Ke Lainnya." },
  { "en": "Apa Fungsi Instruksi SET?", "id": "Mengaktifkan Output Secara Permanen Hingga Di-RST." },
  { "en": "Apa Fungsi Instruksi RST?", "id": "Mematikan Output Yang Diaktifkan Oleh SET." },
  { "en": "Apa Itu Latching Dalam Ladder?", "id": "Teknik Mengunci Output Menggunakan Kontak Sendiri." },
  { "en": "Apa Fungsi Kontak Rising Edge?", "id": "Mendeteksi Perubahan Sinyal Dari OFF Ke ON." },
  { "en": "Apa Fungsi Kontak Falling Edge?", "id": "Mendeteksi Perubahan Sinyal Dari ON Ke OFF." },
  { "en": "Apa Arti Device X Pada PLC?", "id": "Input Fisik Yang Masuk Ke PLC." },
  { "en": "Apa Arti Device Y Pada PLC?", "id": "Output Fisik Keluar Dari PLC." },
  { "en": "Apa Arti Device M Pada PLC?", "id": "Internal Relay Atau Penanda Dalam Program." },
  { "en": "Apa Arti Device D Pada PLC?", "id": "Data Register Untuk Menyimpan Nilai Angka." },
  { "en": "Apa Fungsi Timer (T) Pada PLC?", "id": "Menunda Aktifnya Output Selama Waktu Tertentu." },
  { "en": "Apa Fungsi Counter (C) Pada PLC?", "id": "Menghitung Jumlah Pulsa Atau Kejadian Input." },
  { "en": "Apa Itu Program Scan Time?", "id": "Waktu Yang Dibutuhkan PLC Untuk Menjalankan Seluruh Program." },
  { "en": "Apa Itu Watchdog Timer?", "id": "Sistem Keamanan Untuk Mendeteksi Error Scan Time." },
  { "en": "Apa Fungsi Jendela Navigation?", "id": "Mengelola Struktur Program Dan Parameter PLC." },
  { "en": "Apa Fungsi Intelligent Function Module?", "id": "Modul Khusus Seperti Analog Atau Komunikasi." },
  { "en": "Apa Itu Label Global Dalam GX Works?", "id": "Variabel Yang Bisa Digunakan Di Seluruh Program." },
  { "en": "Apa Itu Label Lokal Dalam GX Works?", "id": "Variabel Yang Hanya Berlaku Dalam Satu Program." },
  { "en": "Apa Fungsi Simulation Mode?", "id": "Menjalankan Program Tanpa Harus Menggunakan PLC Fisik." },
  { "en": "Apa Itu Write To PLC?", "id": "Proses Mengirim Program Dari Komputer Ke PLC." },
  { "en": "Apa Itu Read From PLC?", "id": "Proses Mengambil Program Dari PLC Ke Komputer." },
  { "en": "Apa Fungsi Verify With PLC?", "id": "Membandingkan Program Di Komputer Dan Di PLC." },
  { "en": "Apa Itu Remote RUN?", "id": "Mengubah Status PLC Menjadi RUN Melalui Software." },
  { "en": "Apa Itu Remote STOP?", "id": "Menghentikan Jalannya Program PLC Melalui Software." },
  { "en": "Apa Fungsi Cross Reference?", "id": "Melihat Di Mana Saja Sebuah Device Digunakan." },
  { "en": "Apa Itu Device Test?", "id": "Mengubah Nilai Device Secara Manual Saat Monitoring." },
  { "en": "Apa Shortcut Shift + F3 (GX Works 3)?", "id": "Berpindah Antara Monitor Dan Edit Mode." },
  { "en": "Apa Kegunaan Instruksi CMP?", "id": "Membandingkan Dua Buah Nilai Data." },
  { "en": "Apa Kegunaan Instruksi INC?", "id": "Menambah Nilai Register Sebesar Satu." },
  { "en": "Apa Kegunaan Instruksi DEC?", "id": "Mengurangi Nilai Register Sebesar Satu." },
  { "en": "Apa Itu BCD Conversion?", "id": "Mengonversi Angka Desimal Ke Format BCD." },
  { "en": "Apa Fungsi Register Spesial SM?", "id": "Menyimpan Status Sistem PLC Secara Internal." },
  { "en": "Apa Fungsi Register Spesial SD?", "id": "Menyimpan Data Diagnostik Sistem PLC." },
  { "en": "Apa Itu Floating Point Data?", "id": "Format Data Untuk Bilangan Desimal Pecahan." },
  { "en": "Apa Fungsi Instruksi ALT?", "id": "Membuat Output Bergantian Hidup Dan Mati." },
  { "en": "Apa Itu SFC (Sequential Function Chart)?", "id": "Bahasa Pemrograman Berdasarkan Langkah Berurutan." },
  { "en": "Apa Itu ST (Structured Text)?", "id": "Bahasa Pemrograman PLC Berbasis Teks." },
  { "en": "Apa Fungsi FB (Function Block)?", "id": "Blok Program Yang Bisa Digunakan Berulang Kali." },
  { "en": "Apa Itu Parameter Network?", "id": "Pengaturan Komunikasi Antar PLC Atau Modul." },
  { "en": "Apa Kegunaan Modul Analog Input?", "id": "Membaca Sinyal Voltase Atau Arus Dari Sensor." },
  { "en": "Apa Kegunaan Modul Analog Output?", "id": "Mengirim Sinyal Voltase Untuk Mengatur Inverter." },
  { "en": "Apa Itu Resolusi Bit Analog?", "id": "Ketelitian Konversi Sinyal Analog Ke Digital." },
  { "en": "Apa Fungsi Shielded Cable?", "id": "Kabel Berpelindung Untuk Mengurangi Interferensi Noise." },
  { "en": "Apa Itu Sink Input?", "id": "Tipe Input Di Mana Common Dihubungkan Ke Positif." },
  { "en": "Apa Itu Source Input?", "id": "Tipe Input Di Mana Common Dihubungkan Ke Negatif." },
  { "en": "Apa Itu Transistor Output?", "id": "Output PLC Tanpa Kontak Mekanik, Sangat Cepat." },
  { "en": "Apa Itu Relay Output?", "id": "Output PLC Menggunakan Kontak Mekanik, Arus Besar." },
  { "en": "Apa Fungsi Instruksi PLS?", "id": "Memberikan Pulsa Satu Scan Saat Input Aktif." },
  { "en": "Apa Fungsi Instruksi PLF?", "id": "Memberikan Pulsa Satu Scan Saat Input Mati." },
  { "en": "Apa Shortcut Ctrl + Alt + F4?", "id": "Melakukan Rebuild All Proyek Secara Total." },
  { "en": "Apa Itu Comment Dalam Program?", "id": "Catatan Penjelasan Untuk Alamat Device." },
  { "en": "Apa Itu Statement Dalam Program?", "id": "Catatan Penjelasan Untuk Baris Ladder." },
  { "en": "Apa Itu Note Dalam Program?", "id": "Catatan Tambahan Di Samping Instruksi Output." },
  { "en": "Apa Fungsi Modul High Speed Counter?", "id": "Menghitung Pulsa Frekuensi Tinggi Dari Encoder." },
  { "en": "Apa Itu PWM (Pulse Width Modulation)?", "id": "Metode Pengaturan Kecepatan Motor Melalui Pulsa." },
  { "en": "Apa Fungsi Instruksi MEAN?", "id": "Mencari Nilai Rata-Rata Dari Kumpulan Data." },
  { "en": "Apa Itu Interlock Dalam Program?", "id": "Sistem Keamanan Mencegah Dua Output Aktif Bersamaan." },
  { "en": "Apa Itu Emergency Stop Loop?", "id": "Rangkaian Seri Kabel Untuk Mematikan Mesin Seketika." },
  { "en": "Apa Itu Modbus TCP?", "id": "Protokol Komunikasi Data Melalui Kabel LAN." },
  { "en": "Apa Itu RS485?", "id": "Standar Komunikasi Serial Untuk Jarak Jauh." },
  { "en": "Apa Itu Baud Rate?", "id": "Kecepatan Pengiriman Data Dalam Komunikasi Serial." },
  { "en": "Apa Fungsi Terminasi Resistor?", "id": "Mencegah Pantulan Sinyal Pada Kabel Komunikasi." },
  { "en": "Apa Itu Checksum Error?", "id": "Kesalahan Validasi Data Saat Komunikasi." },
  { "en": "Apa Fungsi Batere Backup PLC?", "id": "Menjaga Program Dan Data Saat Listrik Padam." },
  { "en": "Apa Arti LED ERR Pada PLC?", "id": "Menandakan Terjadi Kesalahan Program Atau Hardware." },
  { "en": "Apa Arti LED PROG Pada PLC?", "id": "Menandakan PLC Sedang Dalam Mode Pemrograman." },
  { "en": "Apa Itu Memory Cassette?", "id": "Modul Tambahan Untuk Memperbesar Kapasitas Program." },
  { "en": "Apa Itu Program Password?", "id": "Fitur Keamanan Untuk Mengunci Akses Ke Program." },
  { "en": "Apa Itu Unit Address PLC?", "id": "Alamat Unik PLC Dalam Sebuah Jaringan." },
  { "en": "Apa Fungsi Instruksi NEG?", "id": "Mengubah Nilai Positif Menjadi Negatif." },
  { "en": "Apa Itu Overflow Dalam Perhitungan?", "id": "Hasil Perhitungan Melebihi Batas Kapasitas Register." },
  { "en": "Apa Itu Underflow Dalam Perhitungan?", "id": "Hasil Perhitungan Di Bawah Batas Minimum Register." },
  { "en": "Apa Shortcut Ctrl + F?", "id": "Mencari Alamat Atau Kata Dalam Program." },
  { "en": "Apa Shortcut Ctrl + H?", "id": "Mengganti Alamat Device Secara Massal." },
  { "en": "Apa Fungsi Global Device Comment?", "id": "Memberikan Nama Pada Device Untuk Semua Program." },
  { "en": "Apa Itu Sampling Trace?", "id": "Merekam Grafik Sinyal Untuk Analisa Gangguan." },
  { "en": "Apa Itu I/O Assignment?", "id": "Proses Mendaftarkan Modul Yang Terpasang Di PLC." },
  { "en": "Apa Fungsi Intelligent Function Utility?", "id": "Alat Bantu Untuk Setting Modul Analog/Komunikasi." },
  { "en": "Apa Itu Master Link?", "id": "PLC Utama Yang Mengatur Data Ke PLC Slave." },
  { "en": "Apa Itu Remote I/O?", "id": "Modul Input Output Yang Letaknya Jauh Dari PLC Utama." },
  { "en": "Apa Shortcut Shift + Alt + F1 (GX Works 2)?", "id": "Menampilkan atau Menyembunyikan Jendela Device Market." },
  { "en": "Apa Shortcut Alt + F1 (GX Works 3)?", "id": "Membuka Jendela Element Selection Untuk Instruksi." },
  { "en": "Apa Shortcut Ctrl + F1 (GX Works 2)?", "id": "Membuka Menu Bantuan atau Manual Penggunaan Software." },
  { "en": "Apa Fungsi 'Check Program' (GX Works 2)?", "id": "Memeriksa Kesalahan Sintaks Atau Error Pada Ladder." },
  { "en": "Apa Fungsi 'Label' (GX Works 3)?", "id": "Mengganti Alamat Device Dengan Nama Variabel Teks." },
  { "en": "Apa Fungsi 'Module Configuration' (GX Works 3)?", "id": "Mengatur Susunan Hardware PLC Secara Visual." },
  { "en": "Apa Shortcut F10 (GX Works 2)?", "id": "Memasukkan Garis Horizontal Pada Gambar Ladder." },
  { "en": "Apa Shortcut Shift + F10 (GX Works 2)?", "id": "Menghapus Garis Horizontal Pada Gambar Ladder." },
  { "en": "Apa Shortcut Ctrl + F9 (GX Works 3)?", "id": "Memasukkan Garis Vertikal Pada Gambar Ladder." },
  { "en": "Apa Shortcut Ctrl + Alt + F10 (GX Works 3)?", "id": "Membuka Jendela Event History Dari PLC." },
  { "en": "Apa Fungsi 'Build' (GX Works 2)?", "id": "Mengompilasi Program Yang Baru Saja Diedit." },
  { "en": "Apa Fungsi 'Rebuild All' (GX Works 3)?", "id": "Mengompilasi Seluruh Program Dan Konfigurasi Label." },
  { "en": "Apa Fungsi 'Watch Window' (GX Works 2)?", "id": "Memantau Nilai Beberapa Register Dalam Satu Tabel." },
  { "en": "Apa Fungsi 'Simulation' (GX Works 3)?", "id": "Menjalankan PLC Virtual Untuk Tes Tanpa Alat." },
  { "en": "Apa Fungsi 'Communication Setting' (GX Works 2)?", "id": "Mengatur Koneksi Kabel USB Atau LAN Ke PLC." },
  { "en": "Apa Fungsi 'Read from PLC' (GX Works 3)?", "id": "Mengambil Data Program Dari PLC Ke Komputer." },
  { "en": "Apa Fungsi 'Write to PLC' (GX Works 2)?", "id": "Mengirim Program Dari Komputer Ke Dalam PLC." },
  { "en": "Apa Fungsi 'Verify with PLC' (GX Works 3)?", "id": "Membandingkan Program Di PC Dengan Yang Ada Di PLC." },
  { "en": "Apa Fungsi 'Remote RUN/STOP' (GX Works 2)?", "id": "Mengontrol Status Operasi PLC Melalui Software." },
  { "en": "Apa Fungsi 'Password Setting' (GX Works 3)?", "id": "Melindungi Program PLC Agar Tidak Bisa Dibaca Orang Lain." },
  { "en": "Apa Kegunaan 'System Monitor' (GX Works 2)?", "id": "Melihat Status Kesehatan Tiap Modul Yang Terpasang." },
  { "en": "Apa Kegunaan 'Device Test' (GX Works 3)?", "id": "Memaksa (Force) Nilai Bit Atau Register Secara Manual." },
  { "en": "Apa Kegunaan 'Cross Reference' (GX Works 2)?", "id": "Mencari Di Mana Saja Alamat Device Tertentu Digunakan." },
  { "en": "Apa Kegunaan 'Entry Data Monitor' (GX Works 3)?", "id": "Mendaftarkan List Device Yang Ingin Dipantau Terus." },
  { "en": "Apa Fungsi 'Global Label' (GX Works 2)?", "id": "Membuat Variabel Yang Berlaku Untuk Semua Program." },
  { "en": "Apa Fungsi 'Local Label' (GX Works 3)?", "id": "Membuat Variabel Yang Hanya Berlaku Di Satu Program." },
  { "en": "Apa Fungsi 'FB (Function Block)' (GX Works 2)?", "id": "Membuat Blok Logika Yang Bisa Digunakan Berulang Kali." },
  { "en": "Apa Fungsi 'Structured Text' (GX Works 3)?", "id": "Menulis Program PLC Menggunakan Bahasa Berbasis Teks." },
  { "en": "Apa Fungsi 'SFC' (GX Works 2)?", "id": "Pemrograman Berdasarkan Diagram Alur Langkah Kerja." },
  { "en": "Apa Fungsi 'Inline Controller' (GX Works 3)?", "id": "Menulis Perintah Teks Singkat Di Dalam Baris Ladder." },
  { "en": "Apa Kegunaan 'Clear PLC Memory' (GX Works 2)?", "id": "Menghapus Seluruh Isi Program Dan Data Di Dalam PLC." },
  { "en": "Apa Kegunaan 'Flash ROM Write' (GX Works 3)?", "id": "Menyimpan Program Secara Permanen Ke Memori Flash." },
  { "en": "Apa Kegunaan 'I/O Assignment' (GX Works 2)?", "id": "Mendefinisikan Alamat Input Dan Output Tiap Modul." },
  { "en": "Apa Kegunaan 'Network Parameter' (GX Works 3)?", "id": "Mengatur Komunikasi Antar PLC Atau Perangkat Lain." },
  { "en": "Apa Fungsi 'Intelligent Function Module' (GX Works 2)?", "id": "Mengatur Settingan Khusus Modul Analog Atau High Speed." },
  { "en": "Apa Fungsi 'Sampling Trace' (GX Works 3)?", "id": "Merekam Grafik Gelombang Data Sesuai Waktu." },
  { "en": "Apa Fungsi 'Offline Chart' (GX Works 2)?", "id": "Menganalisa Hasil Rekaman Data Tanpa Terhubung PLC." },
  { "en": "Apa Fungsi 'Merge' (GX Works 3)?", "id": "Menggabungkan Dua Baris Ladder Menjadi Satu." },
  { "en": "Apa Fungsi 'Split' (GX Works 2)?", "id": "Membagi Satu Tampilan Program Menjadi Dua Jendela." },
  { "en": "Apa Kegunaan 'Device Comment' (GX Works 3)?", "id": "Memberikan Keterangan Nama Pada Alamat X, Y, Atau D." },
  { "en": "Apa Kegunaan 'Statement' (GX Works 2)?", "id": "Memberikan Judul Penjelasan Di Atas Baris Ladder." },
  { "en": "Apa Kegunaan 'Note' (GX Works 3)?", "id": "Memberikan Catatan Samping Pada Instruksi Output." },
  { "en": "Apa Fungsi 'Export to CSV' (GX Works 2)?", "id": "Mengeluarkan Daftar Alamat Device Ke File Excel." },
  { "en": "Apa Fungsi 'Import from CSV' (GX Works 3)?", "id": "Memasukkan Daftar Nama Label Dari File Excel." },
  { "en": "Apa Fungsi 'Ladder Symbol' (GX Works 2)?", "id": "Mengubah Tampilan Alamat Menjadi Simbol Komponen." },
  { "en": "Apa Fungsi 'Zoom In/Out' (GX Works 3)?", "id": "Memperbesar Atau Memperkecil Tampilan Gambar Ladder." },
  { "en": "Apa Kegunaan 'Find/Replace' (GX Works 2)?", "id": "Mencari Dan Mengganti Alamat Device Secara Cepat." },
  { "en": "Apa Kegunaan 'Change PLC Type' (GX Works 3)?", "id": "Mengubah Model PLC Dalam Proyek Yang Sudah Ada." },
  { "en": "Apa Kegunaan 'Print Preview' (GX Works 2)?", "id": "Melihat Tampilan Program Sebelum Dicetak Ke Kertas." },
  { "en": "Apa Fungsi 'Custom Key' (GX Works 3)?", "id": "Mengatur Sendiri Tombol Shortcut Sesuai Keinginan." },
  { "en": "Apa Fungsi 'Lamp' (GT Designer 3)?", "id": "Menampilkan Status On Atau Off Dari PLC Di Layar HMI." },
  { "en": "Apa Fungsi 'Bit Switch' (GT Designer 3)?", "id": "Tombol Layar Untuk Mengaktifkan Input Bit Di PLC." },
  { "en": "Apa Fungsi 'Word Switch' (GT Designer 3)?", "id": "Tombol Layar Untuk Mengubah Nilai Angka Di PLC." },
  { "en": "Apa Fungsi 'Numerical Display' (GT Designer 3)?", "id": "Menampilkan Angka Dari Register PLC Ke Layar HMI." },
  { "en": "Apa Fungsi 'Numerical Input' (GT Designer 3)?", "id": "Kotak Input Untuk Memasukkan Angka Ke PLC Lewat HMI." },
  { "en": "Apa Fungsi 'Comment Display' (GT Designer 3)?", "id": "Menampilkan Pesan Teks Berdasarkan Status Device PLC." },
  { "en": "Apa Fungsi 'Alarm Display' (GT Designer 3)?", "id": "Menampilkan Daftar Kerusakan Yang Sedang Terjadi." },
  { "en": "Apa Fungsi 'Historical Trend Graph' (GT Designer 3)?", "id": "Menampilkan Grafik Riwayat Data Dalam Jangka Waktu Lama." },
  { "en": "Apa Fungsi 'Screen Switching' (GT Designer 3)?", "id": "Tombol Untuk Berpindah Halaman Di Layar HMI." },
  { "en": "Apa Fungsi 'Station No Setting' (GT Designer 3)?", "id": "Menentukan Alamat ID PLC Yang Dihubungkan Ke HMI." },
  { "en": "Apa Kegunaan 'Project Check' (GT Designer 3)?", "id": "Memeriksa Jika Ada Alamat Device Yang Salah Di HMI." },
  { "en": "Apa Kegunaan 'Simulator' (GT Designer 3)?", "id": "Menjalankan Tampilan HMI Di Komputer Tanpa Alat Fisik." },
  { "en": "Apa Kegunaan 'Write to HMI' (GT Designer 3)?", "id": "Mengirim Desain Tampilan Dari Laptop Ke Unit HMI." },
  { "en": "Apa Kegunaan 'System Setting' (GT Designer 3)?", "id": "Mengatur Jenis Kabel Dan Protokol Komunikasi HMI." },
  { "en": "Apa Fungsi 'Recipe' (GT Designer 3)?", "id": "Mengatur Kumpulan Data Parameter Untuk Produk Berbeda." },
  { "en": "Apa Fungsi 'Logger' (GT Designer 3)?", "id": "Merekam Data Dari PLC Ke SD Card Yang Ada Di HMI." },
  { "en": "Apa Fungsi 'Security Setting' (GT Designer 3)?", "id": "Membatasi Siapa Saja Yang Boleh Menekan Tombol Di HMI." },
  { "en": "Apa Fungsi 'Language Switching' (GT Designer 3)?", "id": "Mengubah Bahasa Tampilan Di HMI (Misal Indo Ke Inggris)." },
  { "en": "Apa Fungsi 'Overlap Window' (GT Designer 3)?", "id": "Menampilkan Jendela Kecil Di Atas Layar Utama HMI." },
  { "en": "Apa Fungsi 'Key Window' (GT Designer 3)?", "id": "Menampilkan Keyboard Virtual Untuk Input Angka/Teks." },
  { "en": "Apa Kegunaan 'Resource Data' (GT Designer 3)?", "id": "Mengelola Gambar Atau Font Yang Digunakan Di HMI." },
  { "en": "Apa Kegunaan 'Common Setting' (GT Designer 3)?", "id": "Mengatur Fungsi Umum Seperti Jam Dan Alarm." },
  { "en": "Apa Kegunaan 'Ethernet Setting' (GT Designer 3)?", "id": "Mengatur Alamat IP Agar HMI Bisa Connect Ke Jaringan." },
  { "en": "Apa Kegunaan 'VNC Server' (GT Designer 3)?", "id": "Fitur Untuk Melihat Tampilan HMI Dari Jarak Jauh." },
  { "en": "Apa Fungsi 'Object List' (GT Designer 3)?", "id": "Melihat Daftar Semua Komponen Yang Ada Di Satu Layar." },
  { "en": "Apa Fungsi 'Property Window' (GT Designer 3)?", "id": "Mengubah Warna, Ukuran, Dan Alamat Suatu Tombol." },
  { "en": "Apa Fungsi 'Group' (GT Designer 3)?", "id": "Menyatukan Beberapa Objek Agar Mudah Dipindahkan." },
  { "en": "Apa Fungsi 'Align' (GT Designer 3)?", "id": "Merapikan Letak Tombol Agar Sejajar Dan Rapi." },
  { "en": "Apa Fungsi 'Layer' (GT Designer 3)?", "id": "Mengatur Urutan Objek Agar Tidak Tumpang Tindih." },
  { "en": "Apa Fungsi 'Grid' (GT Designer 3)?", "id": "Menampilkan Garis Bantu Untuk Meletakkan Objek." },
  { "en": "Apa Kegunaan 'Preview' (GT Designer 3)?", "id": "Melihat Hasil Desain Sebelum Di-Download Ke HMI." },
  { "en": "Apa Kegunaan 'Screen Property' (GT Designer 3)?", "id": "Mengatur Warna Background Dan Judul Halaman." },
  { "en": "Apa Kegunaan 'Script' (GT Designer 3)?", "id": "Membuat Logika Pemrograman Sederhana Di Dalam HMI." },
  { "en": "Apa Kegunaan 'Label Group' (GT Designer 3)?", "id": "Mengatur Daftar Nama Variabel Untuk Objek HMI." },
  { "en": "Apa Fungsi 'Multi-press' (GT Designer 3)?", "id": "Fitur Di Mana Tombol Bereaksi Jika Ditekan Lama." },
  { "en": "Apa Fungsi 'Momentary Switch' (GT Designer 3)?", "id": "Tombol Yang Hanya On Saat Ditekan Dan Off Saat Dilepas." },
  { "en": "Apa Fungsi 'Alternate Switch' (GT Designer 3)?", "id": "Tombol Yang Menjadi On Jika Ditekan Sekali, Off Jika Ditekan Lagi." },
  { "en": "Apa Fungsi 'Data Copy' (GT Designer 3)?", "id": "Menyalin Nilai Dari Satu Register Ke Register Lain Lewat HMI." },
  { "en": "Apa Fungsi 'Time Display' (GT Designer 3)?", "id": "Menampilkan Jam Dan Tanggal Saat Ini Pada Layar HMI." },
  { "en": "Apa Fungsi 'Meter Display' (GT Designer 3)?", "id": "Menampilkan Data Dalam Bentuk Jarum Jam (Analog Meter)." },
  { "en": "Apa Kegunaan 'Bar Graph' (GT Designer 3)?", "id": "Menampilkan Level Ketinggian Data Secara Visual." },
  { "en": "Apa Kegunaan 'Slider' (GT Designer 3)?", "id": "Menggeser Objek Untuk Mengubah Nilai Angka Di PLC." },
  { "en": "Apa Kegunaan 'Video Display' (GT Designer 3)?", "id": "Menampilkan Gambar Kamera CCTV Langsung Di Layar HMI." },
  { "en": "Apa Kegunaan 'PDF Display' (GT Designer 3)?", "id": "Membaca Dokumen Manual Mesin Langsung Dari Layar HMI." },
  { "en": "Apa Fungsi 'Operator Authentication' (GT Designer 3)?", "id": "Sistem Login Menggunakan Kartu Atau Fingerprint Di HMI." },
  { "en": "Apa Fungsi 'Data Transfer' (GT Designer 3)?", "id": "Mengirim Data Hasil Produksi Ke Database Server." },
  { "en": "Apa Fungsi 'Report Function' (GT Designer 3)?", "id": "Membuat Laporan Kerja Otomatis Dalam Bentuk File." },
  { "en": "Apa Fungsi 'Sound Output' (GT Designer 3)?", "id": "Mengeluarkan Suara Peringatan Saat Terjadi Bahaya." },
  { "en": "Apa Kegunaan 'FTP Server' (GT Designer 3)?", "id": "Mengambil File Hasil Logging Dari HMI Lewat Internet." },
  { "en": "Apa Kegunaan 'Remote Personal Computer' (GT Designer 3)?", "id": "Mengontrol Desktop Komputer Melalui Layar HMI." },
  { "en": "Apa Shortcut Shift + F4 (GX Works 3)?", "id": "Melakukan Rebuild All, Kompilasi Seluruh Proyek." },
  { "en": "Apa Shortcut Ctrl + Alt + F4 (GX Works 2)?", "id": "Melakukan Rebuild All Proyek Secara Menyeluruh." },
  { "en": "Apa Shortcut Alt + F2 (GX Works 3)?", "id": "Membuka Jendela Navigation Untuk Struktur Proyek." },
  { "en": "Apa Shortcut Alt + F3 (GX Works 3)?", "id": "Menampilkan Jendela Output Untuk Log Kompilasi." },
  { "en": "Apa Shortcut Alt + F4 (GX Works 3)?", "id": "Menampilkan Jendela Watch Untuk Monitor Variabel." },
  { "en": "Apa Shortcut Alt + F5 (GX Works 3)?", "id": "Menampilkan Jendela Intelligent Function Module." },
  { "en": "Apa Shortcut Alt + F6 (GX Works 3)?", "id": "Menampilkan Jendela Device Comment." },
  { "en": "Apa Shortcut Alt + F7 (GX Works 3)?", "id": "Menampilkan Jendela Cross Reference." },
  { "en": "Apa Shortcut Alt + F8 (GX Works 3)?", "id": "Menampilkan Jendela Device List." },
  { "en": "Apa Shortcut Alt + 1 (GX Works 2)?", "id": "Membuka Jendela Proyek Di Sisi Kiri Layar." },
  { "en": "Apa Shortcut Alt + 2 (GX Works 2)?", "id": "Membuka Jendela Network Parameter." },
  { "en": "Apa Shortcut Alt + 3 (GX Works 2)?", "id": "Membuka Jendela Intelligent Function Module." },
  { "en": "Apa Shortcut Ctrl + Shift + F5 (GX Works 3)?", "id": "Melakukan Reset Mode Monitor." },
  { "en": "Apa Shortcut Ctrl + Shift + F7 (GX Works 3)?", "id": "Mengaktifkan Mode Monitor (All Windows)." },
  { "en": "Apa Shortcut Ctrl + Shift + F8 (GX Works 3)?", "id": "Menghentikan Mode Monitor (All Windows)." },
  { "en": "Apa Shortcut Ctrl + F1 (GX Works 3)?", "id": "Membuka File Bantuan (Manual) GX Works 3." },
  { "en": "Apa Shortcut Ctrl + Shift + O (GX Works 2)?", "id": "Membuka Proyek Yang Sudah Ada." },
  { "en": "Apa Shortcut Ctrl + Shift + S (GX Works 2)?", "id": "Menyimpan Proyek Dengan Nama Berbeda (Save As)." },
  { "en": "Apa Fungsi Instruksi MC (GX Works 3)?", "id": "Memulai Blok Kendali Master (Master Control)." },
  { "en": "Apa Fungsi Instruksi MCR (GX Works 3)?", "id": "Mengakhiri Blok Kendali Master (Master Control Reset)." },
  { "en": "Apa Fungsi Instruksi PLSY (GX Works 3)?", "id": "Mengeluarkan Pulsa Dengan Frekuensi Tertentu (Output Pulse)." },
  { "en": "Apa Fungsi Instruksi PLSR (GX Works 3)?", "id": "Mengeluarkan Pulsa Dengan Akselerasi Dan Deselerasi." },
  { "en": "Apa Fungsi Instruksi PWM (GX Works 3)?", "id": "Mengatur Lebar Pulsa (Pulse Width Modulation)." },
  { "en": "Apa Fungsi Instruksi SPD (GX Works 3)?", "id": "Mendeteksi Kecepatan Berdasarkan Input Pulsa." },
  { "en": "Apa Fungsi Instruksi DSIN (GX Works 3)?", "id": "Menghitung Nilai Sinus Dari Data 32-bit." },
  { "en": "Apa Fungsi Instruksi DCOS (GX Works 3)?", "id": "Menghitung Nilai Cosinus Dari Data 32-bit." },
  { "en": "Apa Fungsi Instruksi DTAN (GX Works 3)?", "id": "Menghitung Nilai Tangen Dari Data 32-bit." },
  { "en": "Apa Fungsi Instruksi DASIN (GX Works 3)?", "id": "Menghitung Nilai Arc Sinus Dari Data 32-bit." },
  { "en": "Apa Fungsi Instruksi DACOS (GX Works 3)?", "id": "Menghitung Nilai Arc Cosinus Dari Data 32-bit." },
  { "en": "Apa Fungsi Instruksi DATAN (GX Works 3)?", "id": "Menghitung Nilai Arc Tangen Dari Data 32-bit." },
  { "en": "Apa Fungsi Instruksi DEXP (GX Works 3)?", "id": "Menghitung Nilai Eksponensial Data 32-bit." },
  { "en": "Apa Fungsi Instruksi DLOG (GX Works 3)?", "id": "Menghitung Nilai Logaritma Data 32-bit." },
  { "en": "Apa Fungsi Instruksi DSQRT (GX Works 3)?", "id": "Menghitung Akar Kuadrat Data 32-bit." },
  { "en": "Apa Fungsi Instruksi SCL (GX Works 2)?", "id": "Melakukan Penskalaan (Scaling) Sinyal Analog." },
  { "en": "Apa Fungsi Instruksi SCL2 (GX Works 2)?", "id": "Penskalaan Analog Dengan Offset Dan Gain." },
  { "en": "Apa Fungsi Instruksi MEAN (GX Works 3)?", "id": "Menghitung Nilai Rata-Rata Dari Sekumpulan Data." },
  { "en": "Apa Fungsi Instruksi SORT (GX Works 3)?", "id": "Mengurutkan Data Dari Terkecil Ke Terbesar." },
  { "en": "Apa Fungsi Instruksi SER (GX Works 3)?", "id": "Mencari Data Tertentu Dalam Sekumpulan Register." },
  { "en": "Apa Fungsi Instruksi SUM (GX Works 3)?", "id": "Menghitung Jumlah Bit Yang Aktif Dalam Satu Word." },
  { "en": "Apa Fungsi Instruksi BON (GX Works 3)?", "id": "Memeriksa Apakah Bit Tertentu Sedang ON." },
  { "en": "Apa Fungsi Instruksi ALT (GX Works 2)?", "id": "Membalikkan Status Output (Toggle) Tiap Kali Dipicu." },
  { "en": "Apa Fungsi Instruksi RAMP (GX Works 3)?", "id": "Menaikkan Atau Menurunkan Nilai Secara Bertahap." },
  { "en": "Apa Fungsi Instruksi PID (GX Works 3)?", "id": "Melakukan Kontrol Proportional Integral Derivative." },
  { "en": "Apa Fungsi Instruksi FLT (GX Works 3)?", "id": "Mengonversi Bilangan Bulat Menjadi Bilangan Pecahan." },
  { "en": "Apa Fungsi Instruksi INT (GX Works 3)?", "id": "Mengonversi Bilangan Pecahan Menjadi Bilangan Bulat." },
  { "en": "Apa Fungsi Instruksi BCD (GX Works 3)?", "id": "Mengonversi Data Binari Menjadi Format BCD." },
  { "en": "Apa Fungsi Instruksi BIN (GX Works 3)?", "id": "Mengonversi Data BCD Menjadi Format Binari." },
  { "en": "Apa Fungsi Instruksi GRY (GX Works 3)?", "id": "Mengonversi Data Binari Menjadi Format Gray Code." },
  { "en": "Apa Fungsi Instruksi GBIN (GX Works 3)?", "id": "Mengonversi Data Gray Code Menjadi Format Binari." },
  { "en": "Apa Fungsi 'Label Manager' (GX Works 3)?", "id": "Mengelola Semua Daftar Variabel Dalam Satu Tempat." },
  { "en": "Apa Fungsi 'Module Parameter' (GX Works 3)?", "id": "Mengatur Konfigurasi Internal Modul Tertentu." },
  { "en": "Apa Fungsi 'CPU Parameter' (GX Works 3)?", "id": "Mengatur Kecepatan Scan Dan Kapasitas Memori PLC." },
  { "en": "Apa Fungsi 'Ethernet Configuration' (GX Works 3)?", "id": "Mengatur IP Address Dan Port Protokol Komunikasi." },
  { "en": "Apa Fungsi 'Serial Communication Setting' (GX Works 2)?", "id": "Mengatur Baud Rate Dan Parity Untuk RS232/RS485." },
  { "en": "Apa Fungsi 'Device Memory Map' (GX Works 3)?", "id": "Melihat Alokasi Penggunaan Memori PLC." },
  { "en": "Apa Fungsi 'Online Change' (GX Works 2)?", "id": "Mengubah Program Saat PLC Sedang Berjalan (RUN)." },
  { "en": "Apa Fungsi 'Program Scan' (GX Works 3)?", "id": "Menjalankan Program Secara Rutin Terus Menerus." },
  { "en": "Apa Fungsi 'Fixed Cycle Program' (GX Works 3)?", "id": "Menjalankan Program Pada Interval Waktu Yang Tetap." },
  { "en": "Apa Fungsi 'Event Program' (GX Works 3)?", "id": "Menjalankan Program Hanya Saat Terjadi Event Tertentu." },
  { "en": "Apa Fungsi 'Safety Program' (GX Works 3)?", "id": "Membuat Logika Keamanan Untuk Safety PLC." },
  { "en": "Apa Fungsi 'Global Label Setting' (GX Works 2)?", "id": "Definisi Variabel Yang Bisa Digunakan Di Seluruh Program." },
  { "en": "Apa Fungsi 'Local Label Setting' (GX Works 3)?", "id": "Definisi Variabel Yang Hanya Berlaku Di Satu POU." },
  { "en": "Apa Fungsi 'Watchdog Timer Setting' (GX Works 3)?", "id": "Mengatur Batas Waktu Maksimal Satu Siklus Scan." },
  { "en": "Apa Fungsi 'Remote Maintenance' (GX Works 3)?", "id": "Melakukan Diagnosa PLC Dari Jarak Jauh Lewat Internet." },
  { "en": "Apa Fungsi 'Device Data Logging' (GX Works 3)?", "id": "Merekam Perubahan Data Ke Dalam SD Card PLC." },
  { "en": "Apa Fungsi 'Memory Card Setting' (GX Works 2)?", "id": "Mengatur Penggunaan Memori Eksternal Pada PLC." },
  { "en": "Apa Fungsi 'Multi CPU Setting' (GX Works 3)?", "id": "Sinkronisasi Data Antar Beberapa CPU Dalam Satu Rak." },
  { "en": "Apa Fungsi 'SLMP Setting' (GX Works 3)?", "id": "Mengaktifkan Protokol Komunikasi Seamless Message." },
  { "en": "Apa Fungsi 'FTP Server Setting' (GX Works 3)?", "id": "Mengatur Akses File Memori PLC Lewat Protokol FTP." },
  { "en": "Apa Fungsi 'SNTP Setting' (GX Works 3)?", "id": "Sinkronisasi Jam PLC Dengan Server Waktu Internet." },
  { "en": "Apa Fungsi 'Web Server Setting' (GX Works 3)?", "id": "Menampilkan Data PLC Melalui Browser Web." },
  { "en": "Apa Fungsi 'Security Key Setting' (GX Works 3)?", "id": "Mengunci Program Dengan Kunci Keamanan Hardware." },
  { "en": "Apa Fungsi 'Device Initial Value' (GX Works 2)?", "id": "Memberikan Nilai Awal Pada Register Saat PLC Start." },
  { "en": "Apa Fungsi 'Comment Display' (GT Designer 3)?", "id": "Menampilkan Teks Penjelasan Berdasarkan Status PLC." },
  { "en": "Apa Fungsi 'Alarm History' (GT Designer 3)?", "id": "Mencatat Urutan Kejadian Alarm Berdasarkan Waktu." },
  { "en": "Apa Fungsi 'Trend Graph' (GT Designer 3)?", "id": "Menampilkan Pergerakan Data Register Dalam Grafik." },
  { "en": "Apa Fungsi 'Data Logging' (GT Designer 3)?", "id": "Menyimpan Data Variabel PLC Ke Dalam File CSV." },
  { "en": "Apa Fungsi 'Recipe Manager' (GT Designer 3)?", "id": "Mengatur Berbagai Setingan Parameter Produksi." },
  { "en": "Apa Fungsi 'User Authorization' (GT Designer 3)?", "id": "Mengatur Level Keamanan Dan Password Operator." },
  { "en": "Apa Fungsi 'VNC Server' (GT Designer 3)?", "id": "Mengizinkan Remote Desktop Layar HMI Dari Tablet." },
  { "en": "Apa Fungsi 'Language Switching' (GT Designer 3)?", "id": "Mengganti Bahasa Tampilan Antarmuka HMI." },
  { "en": "Apa Fungsi 'Screen Capture' (GT Designer 3)?", "id": "Mengambil Gambar Tampilan HMI Untuk Dokumentasi." },
  { "en": "Apa Fungsi 'Operation Log' (GT Designer 3)?", "id": "Mencatat Siapa Saja Yang Menekan Tombol Di HMI." },
  { "en": "Apa Fungsi 'Object List' (GT Designer 3)?", "id": "Melihat Dan Mengelola Semua Komponen Di Satu Layar." },
  { "en": "Apa Fungsi 'Key Window' (GT Designer 3)?", "id": "Menampilkan Keyboard Virtual Untuk Input Data." },
  { "en": "Apa Fungsi 'Overlap Window' (GT Designer 3)?", "id": "Menampilkan Jendela Pop-up Di Atas Layar Utama." },
  { "en": "Apa Fungsi 'Report' (GT Designer 3)?", "id": "Mencetak Laporan Produksi Langsung Dari HMI." },
  { "en": "Apa Fungsi 'Script' (GT Designer 3)?", "id": "Membuat Kode Program Tambahan Di Sisi HMI." },
  { "en": "Apa Fungsi 'Station Setting' (GT Designer 3)?", "id": "Menghubungkan HMI Ke Beberapa Merk PLC Berbeda." },
  { "en": "Apa Fungsi 'Resource' (GT Designer 3)?", "id": "Mengelola Gambar, Font, Dan Suara Yang Digunakan." },
  { "en": "Apa Fungsi 'Preview' (GT Designer 3)?", "id": "Simulasi Tampilan Sebelum Di-Download Ke Alat." },
  { "en": "Apa Fungsi 'Project Check' (GT Designer 3)?", "id": "Mencari Kesalahan Alamat Atau Objek Yang Error." },
  { "en": "Apa Fungsi 'Update Firmware' (GT Designer 3)?", "id": "Memperbarui Sistem Operasi Pada Unit HMI." },
  { "en": "Apa Fungsi 'Backup/Restore' (GT Designer 3)?", "id": "Mencadangkan Data HMI Ke Flashdisk." },
  { "en": "Apa Fungsi 'Screen Switching' (GT Designer 3)?", "id": "Membuat Navigasi Antar Halaman Di HMI." },
  { "en": "Apa Fungsi 'Slider' (GT Designer 3)?", "id": "Mengatur Nilai Register Dengan Menggeser Objek." },
  { "en": "Apa Fungsi 'Meter' (GT Designer 3)?", "id": "Menampilkan Nilai Register Dalam Bentuk Jarum Analog." },
  { "en": "Apa Fungsi 'Video Player' (GT Designer 3)?", "id": "Memutar Video Tutorial Atau Rekaman Kamera CCTV." },
  { "en": "Apa Fungsi 'FTP Client' (GT Designer 3)?", "id": "Mengirim File Hasil Logging Ke Server Pusat." }
			 
			 
        ];

        let questions = [];

        rawVocabularyList.sort((a, b) => {
            const enA = a.en.toLowerCase();
            const enB = b.en.toLowerCase();
            if (enA < enB) return -1;
            if (enA > enB) return 1;
            return 0;
        });

        function generateQuestions() {
            const allIndonesianTranslations = rawVocabularyList.map(item => item.id);
            questions = [];
            rawVocabularyList.forEach(vocabItem => {
                const correctAnswer = vocabItem.id;
                const distractors = [];
                let attempts = 0;
                while (distractors.length < 3 && attempts < allIndonesianTranslations.length * 2) {
                    const randomIndex = Math.floor(Math.random() * allIndonesianTranslations.length);
                    const potentialDistractor = allIndonesianTranslations[randomIndex];
                    if (potentialDistractor !== correctAnswer && !distractors.includes(potentialDistractor)) {
                        distractors.push(potentialDistractor);
                    }
                    attempts++;
                }
                while (distractors.length < 3) {
                   distractors.push("Opsi " + Math.random());
                }
                const answerOptions = [
                    { text: correctAnswer, correct: true },
                    { text: distractors[0], correct: false },
                    { text: distractors[1], correct: false },
                    { text: distractors[2], correct: false }
                ];
                questions.push({
                    question: vocabItem.en,
                    answers: answerOptions
                });
            });
        }

        generateQuestions();

        function saveProgress() {
            if (!questionContainerElement.classList.contains('hide') && orderedQuestions && currentQuestionIndex < orderedQuestions.length) {
                 const progress = {
                    currentQuestionIndex: currentQuestionIndex,
                    score: score,
                    orderedQuestions: orderedQuestions
                };
                localStorage.setItem('quizProgress', JSON.stringify(progress));
            }
        }

        function loadProgress() {
            const savedProgress = localStorage.getItem('quizProgress');
            if (savedProgress) {
                try {
                    const progressData = JSON.parse(savedProgress);
                    if (progressData && Array.isArray(progressData.orderedQuestions)) { 
                        return progressData;
                    } else {
                        clearProgress();
                        return null;
                    }
                } catch (e) {
                    clearProgress();
                    return null;
                }
            }
            return null;
        }

        function clearProgress() {
            localStorage.removeItem('quizProgress');
        }

        prev50Button.addEventListener('click', () => navigateQuestions(-JUMP_AMOUNT));
        prevQuestionButton.addEventListener('click', () => navigateQuestions(-1)); 
        nextQuestionButton.addEventListener('click', () => navigateQuestions(1)); 
        next50Button.addEventListener('click', () => navigateQuestions(JUMP_AMOUNT));


        function navigateQuestions(amount) {
            clearTimeout(questionTimeout);
            clearTimeout(autoClickTimeout);

            if (!orderedQuestions || orderedQuestions.length === 0) return;

            let newIndex = currentQuestionIndex + amount;
            if (newIndex < 0) newIndex = 0;
            else if (newIndex >= orderedQuestions.length) newIndex = orderedQuestions.length - 1;

            if (newIndex !== currentQuestionIndex) {
                currentQuestionIndex = newIndex;
                setNextQuestion();
            } else {
                updateSkipButtonStates();
            }
        }

        function updateSkipButtonStates() {
            if (!orderedQuestions || orderedQuestions.length === 0 || questionContainerElement.classList.contains('hide')) {
                skipNavigationControls.classList.add('hide');
                return;
            }
            skipNavigationControls.classList.remove('hide');
            const isFirstQuestion = currentQuestionIndex === 0;
            const isLastQuestion = currentQuestionIndex === (orderedQuestions.length - 1);

            if(prev50Button) prev50Button.disabled = isFirstQuestion;
            if(prevQuestionButton) prevQuestionButton.disabled = isFirstQuestion; 
            
            if(nextQuestionButton) nextQuestionButton.disabled = isLastQuestion;
            if(next50Button) next50Button.disabled = isLastQuestion;
        }


        window.addEventListener('load', () => {
            const savedData = loadProgress();
            startButton.innerText = 'Mulai';
            completionMessageElement.classList.add('hide');
            if (savedData) {
                continueButton.classList.remove('hide');
            } else {
                continueButton.classList.add('hide');
            }
            if (questionContainerElement.classList.contains('hide')) {
                initialControls.classList.remove('hide');
                skipNavigationControls.classList.add('hide');
                questionCounterElement.classList.add('hide');
            } else {
                 initialControls.classList.add('hide');
            }
        });

        startButton.addEventListener('click', () => startGame(false));
        continueButton.addEventListener('click', () => startGame(true));

        function startGame(isContinuing = false) {
            clearTimeout(questionTimeout);
            completionMessageElement.classList.add('hide');
            if (!isContinuing) {
                startButton.innerText = 'Mulai';
            }
            initialControls.classList.add('hide');
            questionContainerElement.classList.remove('hide');
            questionCounterElement.classList.remove('hide');

            const savedData = loadProgress();
            if (isContinuing && savedData && savedData.orderedQuestions && savedData.orderedQuestions.length === questions.length) {
                orderedQuestions = savedData.orderedQuestions;
                currentQuestionIndex = savedData.currentQuestionIndex;
                score = savedData.score;
            } else {
                clearProgress();
                orderedQuestions = [...questions];
                currentQuestionIndex = 0;
                score = 0;
            }

            if (!orderedQuestions || orderedQuestions.length === 0) {
                showResults();
                completionMessageElement.innerText = "Tidak ada soal untuk ditampilkan.";
                completionMessageElement.style.color = "#dc3545";
                completionMessageElement.classList.remove('hide');
                startButton.innerText = 'Mulai';
                return;
            }
            setNextQuestion();
        }

        function setNextQuestion() {
            resetState();
            if (orderedQuestions && currentQuestionIndex < orderedQuestions.length) {
                updateCounterDisplay(); 
                showQuestion(orderedQuestions[currentQuestionIndex]);
                saveProgress();
                if (document.activeElement && typeof document.activeElement.blur === 'function') {
                    document.activeElement.blur();
                }
            } else {
                showResults();
            }
            updateSkipButtonStates(); 
        }

        function showQuestion(questionData) {
            questionElement.innerText = questionData.question;
            answerButtonsElement.innerHTML = '';
            const shuffledAnswers = [...questionData.answers].sort(() => Math.random() - 0.5);
            shuffledAnswers.forEach(answer => {
                const button = document.createElement('button');
                button.innerText = answer.text;
                button.classList.add('btn');
                if (answer.correct) {
                    button.dataset.correct = answer.correct;
                }
                button.addEventListener('click', selectAnswer);
                answerButtonsElement.appendChild(button);
            });

            // LOGIKA OTOMATIS KLIK
            if (toggleAutoClickInput.checked) {
                autoClickTimeout = setTimeout(() => {
                    const correctBtn = Array.from(answerButtonsElement.children).find(b => b.dataset.correct === 'true');
                    if (correctBtn && !correctBtn.disabled) {
                        selectAnswer({ target: correctBtn });
                    }
                }, 2500); 
            }
        }

        function resetState() {
            clearTimeout(questionTimeout);
            clearTimeout(autoClickTimeout); 
            while (answerButtonsElement.firstChild) {
                answerButtonsElement.removeChild(answerButtonsElement.firstChild);
            }
        }

        function selectAnswer(e) {
            const selectedButton = e.target;
            const correct = selectedButton.dataset.correct === 'true';
            if (correct) { score++; }
            Array.from(answerButtonsElement.children).forEach(button => {
                if (button.dataset.correct === 'true') {
                    button.classList.add('correct');
                } else {
                    button.classList.add('wrong');
                }
                button.disabled = true;
            });
            saveProgress();
            
            questionTimeout = setTimeout(() => {
                if (orderedQuestions && currentQuestionIndex < orderedQuestions.length -1) {
                    currentQuestionIndex++;
                    setNextQuestion();
                } else if (orderedQuestions && currentQuestionIndex === orderedQuestions.length -1) {
                    showResults();
                }
            }, autoNextDelay * 1000); 
        }

        function showResults() {
            clearTimeout(questionTimeout);
            clearTimeout(autoClickTimeout);
            questionContainerElement.classList.add('hide');
            questionCounterElement.classList.add('hide'); 
            skipNavigationControls.classList.add('hide');
            clearProgress();
            completionMessageElement.innerText = "Selamat Kuis Sudah Selesai 🎉";
            completionMessageElement.classList.remove('hide');
            startButton.innerText = 'Ulangi Kuis';
            initialControls.classList.remove('hide');
            continueButton.classList.add('hide');
        }
    </script>
</body>
</html>
