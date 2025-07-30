<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>August Slimdown Challenge 2025</title>
    
    <!-- Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts: Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;900&display=swap" rel="stylesheet">
    
    <!-- Three.js for 3D background -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    
    <!-- Canvas Confetti for celebration -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>

    <style>
        body {
            font-family: 'Inter', sans-serif;
            color: #e5e7eb; /* gray-200 */
            background-color: #111827; /* gray-900 */
            overflow-x: hidden;
        }
        #bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 0;
        }
        .main-container {
            position: relative;
            z-index: 10;
        }
        header {
            position: sticky;
            top: 0;
            z-index: 30;
            background: rgba(17, 24, 39, 0.8);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            padding-top: 1.5rem;
            padding-bottom: 1.5rem;
            transition: all 0.3s ease;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        .glass-card {
            background: rgba(31, 41, 55, 0.7); /* gray-800 */
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .btn-gradient {
            background-image: linear-gradient(to right, #dc2626, #ef4444); /* red-600 to red-500 */
            color: #ffffff;
            transition: all 0.3s ease;
        }
        .btn-gradient:hover {
            background-image: linear-gradient(to right, #b91c1c, #dc2626); /* red-700 to red-600 */
            transform: scale(1.02);
        }
        .title-gradient {
            background: linear-gradient(to right, #fef2f2, #fee2e2); /* red-50 to red-100 */
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 0 20px rgba(239, 68, 68, 0.5);
        }
        .form-input {
            width: 100%;
            background-color: rgba(55, 65, 81, 0.5); /* gray-700 */
            border: 1px solid #4b5563; /* gray-600 */
            border-radius: 0.5rem;
            padding: 0.5rem 0.75rem;
            color: white;
            transition: all 0.2s;
        }
        .form-input:focus {
            outline: none;
            border-color: #ef4444; /* red-500 */
            box-shadow: 0 0 0 2px rgba(239, 68, 68, 0.5);
        }
        .notification {
            transition: all 0.5s ease-in-out;
            transform: translateX(110%);
            opacity: 0;
        }
        .notification.show {
            transform: translateX(0);
            opacity: 1;
        }
        @keyframes reveal { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .reveal-animation { animation: reveal 0.7s ease-out forwards; opacity: 0; }

        @keyframes pulse-ring {
            0% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.7); }
            70% { box-shadow: 0 0 0 12px rgba(239, 68, 68, 0); }
            100% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0); }
        }
        .pulsing-ring {
            border-radius: 9999px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            border: 2px solid #ef4444; /* red-500 */
            animation: pulse-ring 1.5s infinite;
        }
        .ai-modal {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.9);
            width: 90vw;
            height: 90vh;
            z-index: 50;
            opacity: 0;
            pointer-events: none;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .ai-modal.show {
            transform: translate(-50%, -50%) scale(1);
            opacity: 1;
            pointer-events: auto;
        }
        @keyframes pulse-brain {
            0% { transform: scale(1); filter: drop-shadow(0 0 2px #ef4444); }
            50% { transform: scale(1.05); filter: drop-shadow(0 0 5px #ef4444); }
            100% { transform: scale(1); filter: drop-shadow(0 0 2px #ef4444); }
        }
        .pulsing-brain {
            animation: pulse-brain 2s infinite ease-in-out;
        }
        .lang-flag {
            cursor: pointer;
            transition: all 0.2s ease-in-out;
            opacity: 0.5;
            border: 2px solid transparent;
        }
        .lang-flag.active {
            opacity: 1;
            transform: scale(1.1);
            border-color: #ef4444;
        }
    </style>
</head>
<body class="bg-gray-900">

    <canvas id="bg-canvas"></canvas>

    <!-- Notification Container -->
    <div id="notification-container" class="fixed top-24 right-5 z-50 flex flex-col items-end gap-3 w-full max-w-xs"></div>

    <!-- Modals -->
    <div id="modal-backdrop" class="fixed inset-0 bg-black bg-opacity-70 z-40 hidden"></div>
    <div id="delete-modal" class="fixed inset-0 z-50 flex items-center justify-center hidden p-4">
        <div class="glass-card rounded-2xl p-6 shadow-2xl w-full max-w-sm text-center">
            <h3 class="text-xl font-bold text-white mb-4" data-lang="deleteConfirmTitle">Konfirmasi Hapus</h3>
            <p class="text-gray-300 mb-4" data-lang="deleteConfirmBody">Masukkan password admin untuk menghapus.</p>
            <input type="password" id="delete-password" class="form-input mb-6" data-lang-placeholder="adminPasswordPlaceholder">
            <div class="flex justify-center gap-4">
                <button id="delete-cancel-btn" class="bg-gray-600 hover:bg-gray-500 text-white font-bold py-2 px-6 rounded-lg transition" data-lang="cancelButton">Batal</button>
                <button id="delete-confirm-btn" class="bg-red-600 hover:bg-red-500 text-white font-bold py-2 px-6 rounded-lg transition" data-lang="deleteButton">Hapus</button>
            </div>
        </div>
    </div>
    <div id="winner-password-modal" class="fixed inset-0 z-50 flex items-center justify-center hidden p-4">
        <div class="glass-card rounded-2xl p-6 shadow-2xl w-full max-w-sm text-center">
            <h3 class="text-xl font-bold text-white mb-4" data-lang="viewWinnerTitle">Lihat Pemenang</h3>
            <p class="text-gray-300 mb-4" data-lang="viewWinnerBody">Masukkan password admin untuk melihat pemenang.</p>
            <input type="password" id="view-winner-password" class="form-input mb-6" data-lang-placeholder="adminPasswordPlaceholder">
            <div class="flex justify-center gap-4">
                <button id="view-winner-cancel-btn" class="bg-gray-600 hover:bg-gray-500 text-white font-bold py-2 px-6 rounded-lg transition" data-lang="cancelButton">Batal</button>
                <button id="view-winner-confirm-btn" class="btn-gradient text-white font-bold py-2 px-6 rounded-lg" data-lang="viewButton">Lihat</button>
            </div>
        </div>
    </div>
    
    <!-- AI Modal -->
    <div id="ai-modal" class="ai-modal">
        <div class="glass-card rounded-2xl w-full h-full flex flex-col p-6">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-2xl font-bold title-gradient" data-lang="askAITitle">Tanya AI</h2>
                <button id="ai-close-btn" class="p-2 text-gray-400 hover:text-white hover:bg-white/10 rounded-full">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
                </button>
            </div>
            <div id="ai-response-area" class="flex-grow bg-black/20 rounded-lg p-4 overflow-y-auto mb-4 text-gray-300 space-y-4">
                <p data-lang="aiGreeting">Ada yang bisa dibantu?</p>
            </div>
            <form id="ai-form" class="flex gap-4">
                <input type="text" id="ai-prompt" class="form-input flex-grow" data-lang-placeholder="aiPlaceholder">
                <button type="submit" class="btn-gradient font-bold py-2 px-6 rounded-lg flex items-center gap-2" data-lang="sendButton">
                    Kirim
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path d="M10.894 2.553a1 1 0 00-1.788 0l-7 14a1 1 0 001.169 1.409l5-1.429A1 1 0 009 15.571V11a1 1 0 112 0v4.571a1 1 0 00.725.962l5 1.428a1 1 0 001.17-1.408l-7-14z" /></svg>
                </button>
            </form>
        </div>
    </div>
    
    <!-- AI Toggle Button -->
    <button id="ai-toggle-btn" class="fixed bottom-5 right-5 z-30 bg-gray-800/50 backdrop-blur-sm p-3 rounded-full shadow-lg transform hover:scale-110 transition-transform flex flex-col items-center gap-1">
        <span class="text-xs text-white" data-lang="askAITitle">Tanya AI</span>
        <svg class="h-8 w-8 text-red-500 pulsing-brain" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 2C6.477 2 2 6.477 2 12s4.477 10 10 10 10-4.477 10-10S17.523 2 12 2zm-1 5a1 1 0 112 0v2a1 1 0 11-2 0V7zm0 4a1 1 0 112 0v6a1 1 0 11-2 0v-6z" />
            <path d="M12.5,8.5h-1A1.5,1.5,0,0,0,10,10v1a1.5,1.5,0,0,0,1.5,1.5h1A1.5,1.5,0,0,0,14,11v-1A1.5,1.5,0,0,0,12.5,8.5Zm-1,2.5v-1h1v1Z" />
            <path d="M17.5,11.5h-1a.5.5,0,0,0-.5.5v1a.5.5,0,0,0,.5.5h1a.5.5,0,0,0,.5-.5v-1A.5.5,0,0,0,17.5,11.5Z" />
            <path d="M7.5,11.5h-1a.5.5,0,0,0-.5.5v1a.5.5,0,0,0,.5.5h1a.5.5,0,0,0,.5-.5v-1A.5.5,0,0,0,7.5,11.5Z" />
        </svg>
    </button>

    <header>
        <div class="container mx-auto px-4 flex flex-col sm:flex-row justify-between items-center gap-4 sm:gap-0">
            <div class="w-full sm:w-1/3 order-2 sm:order-1"></div>
            <div class="w-full sm:w-1/3 text-center order-1 sm:order-2">
                <h1 class="text-2xl sm:text-3xl md:text-4xl font-black title-gradient tracking-tight" data-lang="mainTitle">
                    August Slimdown Challenge 2025
                </h1>
            </div>
            <div class="w-full sm:w-1/3 flex justify-center sm:justify-end items-center gap-3 order-3">
                <img src="https://flagcdn.com/id.svg" width="30" class="lang-flag rounded-sm" id="lang-id" alt="Bahasa Indonesia">
                <img src="https://flagcdn.com/gb.svg" width="30" class="lang-flag rounded-sm" id="lang-en" alt="English">
            </div>
        </div>
    </header>

    <div class="main-container container mx-auto px-4 py-8 md:py-12">
        
        <main class="grid grid-cols-1 lg:grid-cols-5 gap-8">
            
            <div class="lg:col-span-2 reveal-animation" style="animation-delay: 0.3s;">
                <div class="glass-card rounded-2xl p-6 shadow-2xl">
                    <h2 class="text-2xl font-bold text-white mb-6 text-center lg:text-left" data-lang="addParticipantTitle">Tambah Peserta Baru</h2>
                    <form id="add-participant-form" class="space-y-4">
                        <input type="text" id="name" name="name" required class="form-input" data-lang-placeholder="participantNamePlaceholder">
                        <select id="company" name="company" required class="form-input">
                            <option value="" disabled selected data-lang="selectCompanyOption">Pilih Perusahaan</option>
                            <option value="Grand Jatra Hotel Balikpapan">Grand Jatra Hotel Balikpapan</option>
                            <option value="Astara Hotel Balikpapan">Astara Hotel Balikpapan</option>
                            <option value="Pentacity Hotel Balikpapan">Pentacity Hotel Balikpapan</option>
                            <option value="J-Icon Hotel Balikpapan">J-Icon Hotel Balikpapan</option>
                        </select>
                        <select id="gender" name="gender" required class="form-input">
                             <option value="" disabled selected data-lang="selectGenderOption">Pilih Jenis Kelamin</option>
                            <option value="Pria" data-lang="genderMale">Pria</option>
                            <option value="Wanita" data-lang="genderFemale">Wanita</option>
                        </select>
                        <div>
                            <label for="start-weight" class="block text-sm font-medium text-gray-400 mb-1" data-lang="startWeightLabel">Berat Awal (1 Agustus)</label>
                            <div class="relative">
                                <input type="number" step="0.1" id="start-weight" name="start-weight" required class="form-input pr-10" placeholder="0.0">
                                <span class="absolute inset-y-0 right-3 flex items-center text-gray-400">kg</span>
                            </div>
                        </div>
                        <input type="password" id="weight-key" name="weight-key" class="form-input" data-lang-placeholder="createKeyPlaceholder">
                        <button type="submit" class="w-full btn-gradient font-bold py-3 px-4 rounded-lg shadow-lg" data-lang="registerButton">
                            Daftarkan
                        </button>
                    </form>
                </div>
            </div>

            <div class="lg:col-span-3 reveal-animation" style="animation-delay: 0.5s;">
                <div class="glass-card rounded-2xl p-6 shadow-2xl">
                    <div class="flex flex-col md:flex-row justify-between items-center mb-6 gap-4">
                        <h2 class="text-2xl font-bold text-white text-center lg:text-left" data-lang="participantListTitle">Daftar Peserta</h2>
                        <div class="pulsing-ring p-1">
                            <span class="text-3xl font-black title-gradient min-w-[40px] text-center" id="participant-count">0</span>
                        </div>
                    </div>
                    
                    <div class="flex flex-col sm:flex-row gap-4 mb-6">
                        <select id="filter-gender" class="form-input flex-1" aria-label="Filter Jenis Kelamin">
                            <option value="Semua" data-lang="filterAllGenders">Semua Jenis Kelamin</option>
                            <option value="Pria" data-lang="genderMale">Pria</option>
                            <option value="Wanita" data-lang="genderFemale">Wanita</option>
                        </select>
                        <input type="text" id="search-company" class="form-input flex-1" aria-label="Cari Nama Perusahaan" data-lang-placeholder="searchCompanyPlaceholder">
                    </div>

                    <div id="participant-list" class="space-y-4 max-h-[50vh] overflow-y-auto pr-2"></div>
                </div>
            </div>

        </main>
        
        <!-- Winner Section -->
        <div id="winner-section" class="mt-12 reveal-animation" style="animation-delay: 0.7s;">
            <div class="glass-card rounded-2xl p-8 shadow-2xl text-center">
                <svg id="crown-icon" class="mx-auto h-16 w-16 text-red-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12,2.5L9,7.35L3.15,6.5L6.18,11.37L4.22,16.85L9.6,15.4L12,20.5L14.4,15.4L19.78,16.85L17.82,11.37L20.85,6.5L15,7.35L12,2.5Z" />
                </svg>
                <div id="winner-display" class="hidden">
                    <h2 class="text-3xl font-bold title-gradient mt-4" data-lang="winnerAnnouncedTitle">Selamat kepada Pemenang!</h2>
                    <p class="text-2xl text-white mt-2" id="winner-name-display"></p>
                    <p class="text-lg text-gray-300" id="winner-result-display"></p>
                </div>
                <div id="no-winner-display">
                    <h2 class="text-2xl font-bold text-white mt-4" data-lang="waitingForWinnerTitle">Menunggu Pemenang</h2>
                    <p class="text-gray-400 mt-1" data-lang="waitingForWinnerBody">Pemenang diumumkan setelah semua data terisi.</p>
                </div>
                <button id="view-winner-btn" class="mt-4 btn-gradient text-white font-bold py-2 px-6 rounded-lg hidden" data-lang="viewWinnerButton">Lihat Pemenang</button>
            </div>
        </div>
        
        <footer class="text-center mt-12 text-gray-300 text-lg reveal-animation" style="animation-delay: 0.8s;">
            <a href="http://www.jatrahotels.com" target="_blank" rel="noopener noreferrer" class="hover:text-white transition" style="text-shadow: 0 0 5px rgba(255,255,255,0.5);">www.jatrahotels.com</a>
        </footer>
    </div>

    <!-- Firebase SDK -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, addDoc, onSnapshot, doc, deleteDoc, updateDoc, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        const appId = typeof __app_id !== 'undefined' ? __app_id : 'slimdown-challenge-2025';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : { apiKey: "DEMO", authDomain: "DEMO", projectId: "DEMO" };
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);

        // DOM Elements & Global State
        const elements = {
            participantList: document.getElementById('participant-list'),
            participantCount: document.getElementById('participant-count'),
            addForm: document.getElementById('add-participant-form'),
            filterGender: document.getElementById('filter-gender'),
            searchCompany: document.getElementById('search-company'),
            notificationContainer: document.getElementById('notification-container'),
            modalBackdrop: document.getElementById('modal-backdrop'),
            deleteModal: {
                el: document.getElementById('delete-modal'),
                confirmBtn: document.getElementById('delete-confirm-btn'),
                cancelBtn: document.getElementById('delete-cancel-btn'),
                passwordInput: document.getElementById('delete-password')
            },
            winnerPasswordModal: {
                el: document.getElementById('winner-password-modal'),
                confirmBtn: document.getElementById('view-winner-confirm-btn'),
                cancelBtn: document.getElementById('view-winner-cancel-btn'),
                passwordInput: document.getElementById('view-winner-password')
            },
            winnerDisplay: document.getElementById('winner-display'),
            noWinnerDisplay: document.getElementById('no-winner-display'),
            winnerName: document.getElementById('winner-name-display'),
            winnerResult: document.getElementById('winner-result-display'),
            viewWinnerBtn: document.getElementById('view-winner-btn'),
            ai: {
                modal: document.getElementById('ai-modal'),
                toggleBtn: document.getElementById('ai-toggle-btn'),
                closeBtn: document.getElementById('ai-close-btn'),
                form: document.getElementById('ai-form'),
                promptInput: document.getElementById('ai-prompt'),
                responseArea: document.getElementById('ai-response-area')
            },
            langId: document.getElementById('lang-id'),
            langEn: document.getElementById('lang-en')
        };
        
        let appInitialized = false;
        let allParticipants = []; 
        let deleteCallback = null;
        let determinedWinner = null;
        let currentLanguage = 'id';

        // --- TRANSLATIONS ---
        const translations = {
            id: {
                mainTitle: "August Slimdown Challenge 2025",
                addParticipantTitle: "Tambah Peserta Baru",
                participantNamePlaceholder: "Nama Peserta",
                selectCompanyOption: "Pilih Perusahaan",
                selectGenderOption: "Pilih Jenis Kelamin",
                genderMale: "Pria",
                genderFemale: "Wanita",
                startWeightLabel: "Berat Awal (1 Agustus)",
                createKeyPlaceholder: "Buat Kunci (Opsional)",
                registerButton: "Daftarkan",
                participantListTitle: "Daftar Peserta",
                filterAllGenders: "Semua Jenis Kelamin",
                searchCompanyPlaceholder: "Cari berdasarkan perusahaan...",
                waitingForWinnerTitle: "Menunggu Pemenang",
                waitingForWinnerBody: "Pemenang diumumkan setelah semua data terisi.",
                viewWinnerButton: "Lihat Pemenang",
                winnerAnnouncedTitle: "Selamat kepada Pemenang!",
                deleteConfirmTitle: "Konfirmasi Hapus",
                deleteConfirmBody: "Masukkan password admin untuk menghapus.",
                adminPasswordPlaceholder: "Password Admin",
                cancelButton: "Batal",
                deleteButton: "Hapus",
                viewWinnerTitle: "Lihat Pemenang",
                viewWinnerBody: "Masukkan password admin untuk melihat pemenang.",
                viewButton: "Lihat",
                askAITitle: "Tanya AI",
                aiGreeting: "Ada yang bisa dibantu?",
                aiPlaceholder: "Ketik pertanyaan Anda di sini...",
                sendButton: "Kirim",
                notifSuccessAdd: "Peserta berhasil ditambahkan!",
                notifSuccessDelete: "Peserta berhasil dihapus.",
                notifSuccessUpdate: "Berat akhir berhasil disimpan!",
                notifSuccessUnlock: "Kunci berhasil dibuka!",
                notifErrorGeneric: "Terjadi kesalahan.",
                notifErrorPassword: "Password admin salah.",
                notifErrorUnlock: "Kunci yang dimasukkan salah.",
                notifErrorFillAll: "Mohon lengkapi nama, perusahaan, gender, dan berat awal.",
                notifErrorInvalidWeight: "Mohon masukkan angka yang valid.",
                notifErrorAI: "Maaf, terjadi kesalahan saat menghubungi AI.",
                notifErrorAIConnect: "Maaf, tidak dapat terhubung ke layanan AI saat ini.",
                aiThinking: "AI sedang berpikir...",
                registeredOn: "Terdaftar",
                savedOn: "Disimpan",
                startWeightCardLabel: "Berat Awal (1 Agustus)",
                finalWeightCardLabel: "Berat Akhir (31 Agustus)",
                unlockKeyPlaceholder: "Masukkan Kunci",
                weightLossResult: (kg) => `Turun ${kg} kg`,
                weightGainResult: (kg) => `Naik ${kg} kg`,
                weightSameResult: "Berat Tetap"
            },
            en: {
                mainTitle: "August Slimdown Challenge 2025",
                addParticipantTitle: "Add New Participant",
                participantNamePlaceholder: "Participant's Name",
                selectCompanyOption: "Select Company",
                selectGenderOption: "Select Gender",
                genderMale: "Male",
                genderFemale: "Female",
                startWeightLabel: "Start Weight (1 August)",
                createKeyPlaceholder: "Create Key (Optional)",
                registerButton: "Register",
                participantListTitle: "Participant List",
                filterAllGenders: "All Genders",
                searchCompanyPlaceholder: "Search by company...",
                waitingForWinnerTitle: "Awaiting Winner",
                waitingForWinnerBody: "The winner will be announced after all data is filled.",
                viewWinnerButton: "View Winner",
                winnerAnnouncedTitle: "Congratulations to the Winner!",
                deleteConfirmTitle: "Confirm Deletion",
                deleteConfirmBody: "Enter admin password to delete.",
                adminPasswordPlaceholder: "Admin Password",
                cancelButton: "Cancel",
                deleteButton: "Delete",
                viewWinnerTitle: "View Winner",
                viewWinnerBody: "Enter admin password to view the winner.",
                viewButton: "View",
                askAITitle: "Ask AI",
                aiGreeting: "How can I help you?",
                aiPlaceholder: "Type your question here...",
                sendButton: "Send",
                notifSuccessAdd: "Participant added successfully!",
                notifSuccessDelete: "Participant deleted successfully.",
                notifSuccessUpdate: "Final weight saved successfully!",
                notifSuccessUnlock: "Key unlocked successfully!",
                notifErrorGeneric: "An error occurred.",
                notifErrorPassword: "Incorrect admin password.",
                notifErrorUnlock: "Incorrect key entered.",
                notifErrorFillAll: "Please complete name, company, gender, and start weight.",
                notifErrorInvalidWeight: "Please enter a valid number.",
                notifErrorAI: "Sorry, an error occurred while contacting the AI.",
                notifErrorAIConnect: "Sorry, cannot connect to the AI service right now.",
                aiThinking: "AI is thinking...",
                registeredOn: "Registered",
                savedOn: "Saved",
                startWeightCardLabel: "Start Weight (1 Aug)",
                finalWeightCardLabel: "Final Weight (31 Aug)",
                unlockKeyPlaceholder: "Enter Key",
                weightLossResult: (kg) => `Lost ${kg} kg`,
                weightGainResult: (kg) => `Gained ${kg} kg`,
                weightSameResult: "Weight Unchanged"
            }
        };

        function setLanguage(lang) {
            currentLanguage = lang;
            const langData = translations[lang];
            document.querySelectorAll('[data-lang]').forEach(el => {
                const key = el.getAttribute('data-lang');
                if (langData[key]) el.textContent = langData[key];
            });
            document.querySelectorAll('[data-lang-placeholder]').forEach(el => {
                const key = el.getAttribute('data-lang-placeholder');
                if (langData[key]) el.placeholder = langData[key];
            });

            elements.langId.classList.toggle('active', lang === 'id');
            elements.langEn.classList.toggle('active', lang === 'en');
            renderFilteredParticipants(); // Re-render cards with new language
        }

        // --- HELPER FUNCTIONS ---
        async function hashString(str) {
            const data = new TextEncoder().encode(str);
            const hashBuffer = await crypto.subtle.digest('SHA-256', data);
            return Array.from(new Uint8Array(hashBuffer)).map(b => b.toString(16).padStart(2, '0')).join('');
        }

        function showNotification(messageKey, type = 'success') {
            const message = translations[currentLanguage][messageKey] || translations[currentLanguage]['notifErrorGeneric'];
            const borderColor = type === 'success' ? 'border-green-500' : 'border-red-500';
            const notif = document.createElement('div');
            notif.className = `notification glass-card p-4 rounded-lg shadow-lg w-full border-l-4 ${borderColor}`;
            notif.innerHTML = `<p class="text-white font-medium">${message}</p>`;
            elements.notificationContainer.appendChild(notif);
            setTimeout(() => { notif.classList.add('show'); }, 10);
            setTimeout(() => {
                notif.classList.remove('show');
                notif.addEventListener('transitionend', () => notif.remove());
            }, 2000);
        }

        function showModal(modalElement) {
            elements.modalBackdrop.classList.remove('hidden');
            modalElement.classList.remove('hidden');
        }

        function hideAllModals() {
            elements.modalBackdrop.classList.add('hidden');
            elements.deleteModal.el.classList.add('hidden');
            elements.winnerPasswordModal.el.classList.add('hidden');
        }
        
        function formatTimestamp(timestamp) {
            if (!timestamp || !timestamp.seconds) return '';
            const date = new Date(timestamp.seconds * 1000);
            return date.toLocaleString(currentLanguage === 'id' ? 'id-ID' : 'en-GB', {
                day: '2-digit', month: 'short', year: 'numeric', hour: '2-digit', minute: '2-digit'
            });
        }

        function launchConfetti() {
            const duration = 5 * 1000;
            const animationEnd = Date.now() + duration;
            const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 100, colors: ['#EF4444', '#F87171', '#FCA5A5', '#FFFFFF'] };
            function randomInRange(min, max) { return Math.random() * (max - min) + min; }
            const interval = setInterval(function() {
                const timeLeft = animationEnd - Date.now();
                if (timeLeft <= 0) return clearInterval(interval);
                const particleCount = 50 * (timeLeft / duration);
                confetti({ ...defaults, particleCount, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 } });
                confetti({ ...defaults, particleCount, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 } });
            }, 250);
        }

        function checkAndHandleWinnerState() {
            if (allParticipants.length === 0) {
                determinedWinner = null;
                elements.noWinnerDisplay.classList.remove('hidden');
                elements.viewWinnerBtn.classList.add('hidden');
                elements.winnerDisplay.classList.add('hidden');
                return;
            }
            const allFilled = allParticipants.every(doc => doc.data().finalWeight !== null);
            
            if (allFilled) {
                let winnerCandidate = null;
                let maxLoss = -Infinity;

                for (const doc of allParticipants) {
                    const participantData = doc.data();
                    if (participantData.startWeight && participantData.finalWeight) {
                        const loss = participantData.startWeight - participantData.finalWeight;
                        if (loss > maxLoss) {
                            maxLoss = loss;
                            winnerCandidate = participantData;
                        }
                    }
                }
                
                if (winnerCandidate) {
                    determinedWinner = { ...winnerCandidate, loss: maxLoss };
                } else {
                    determinedWinner = null;
                }

                elements.noWinnerDisplay.classList.add('hidden');
                elements.viewWinnerBtn.classList.remove('hidden');
                elements.winnerDisplay.classList.add('hidden');
            } else {
                determinedWinner = null;
                elements.noWinnerDisplay.classList.remove('hidden');
                elements.viewWinnerBtn.classList.add('hidden');
                elements.winnerDisplay.classList.add('hidden');
            }
        }
        
        elements.deleteModal.confirmBtn.addEventListener('click', () => {
            if (elements.deleteModal.passwordInput.value === '131dualima') {
                if (deleteCallback) deleteCallback();
                hideAllModals();
            } else { showNotification('notifErrorPassword', 'error'); }
        });
        elements.deleteModal.cancelBtn.addEventListener('click', hideAllModals);

        elements.viewWinnerBtn.addEventListener('click', () => showModal(elements.winnerPasswordModal.el));
        elements.winnerPasswordModal.cancelBtn.addEventListener('click', hideAllModals);
        elements.winnerPasswordModal.confirmBtn.addEventListener('click', () => {
            if (elements.winnerPasswordModal.passwordInput.value === '131dualima') {
                if (determinedWinner) {
                    elements.winnerName.textContent = determinedWinner.name;
                    elements.winnerResult.textContent = translations[currentLanguage].weightLossResult(determinedWinner.loss.toFixed(1));
                    elements.winnerDisplay.classList.remove('hidden');
                    elements.viewWinnerBtn.classList.add('hidden');
                    launchConfetti();
                }
                hideAllModals();
            } else {
                showNotification('notifErrorPassword', 'error');
            }
        });

        function renderFilteredParticipants() {
            const genderFilter = elements.filterGender.value;
            const companySearch = elements.searchCompany.value.toLowerCase();
            const filtered = allParticipants.filter(doc => {
                const p = doc.data();
                const genderMatch = (genderFilter === 'Semua') || (p.gender === genderFilter);
                const companyMatch = p.company.toLowerCase().includes(companySearch);
                return genderMatch && companyMatch;
            });
            elements.participantList.innerHTML = '';
            elements.participantCount.textContent = filtered.length;
            if (filtered.length === 0) {
                elements.participantList.innerHTML = `<p class="text-center text-gray-400 py-4">Tidak ada peserta yang cocok.</p>`;
            } else {
                filtered.forEach(doc => renderParticipantCard(doc));
            }
            checkAndHandleWinnerState();
        }

        function renderParticipantCard(doc) {
            const participant = doc.data();
            const card = document.createElement('div');
            card.className = 'glass-card rounded-lg p-4 flex flex-col gap-4 reveal-animation';
            card.setAttribute('data-id', doc.id);

            const nameColorClass = participant.gender === 'Pria' ? 'text-blue-400' : 'text-green-400';
            const langData = translations[currentLanguage];

            let weightDisplayHTML = participant.isWeightVisible
                ? `<p class="text-sm text-red-400"><strong>${participant.startWeight} kg</strong></p>`
                : `<div class="flex items-center gap-2">
                        <input type="password" class="form-input text-sm flex-grow unlock-key-input" placeholder="${langData.unlockKeyPlaceholder}">
                        <button class="unlock-btn p-2 bg-red-600/80 hover:bg-red-500 rounded-lg transition" aria-label="Buka Kunci Berat Awal">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M10 1a4.5 4.5 0 00-4.5 4.5V9H5a2 2 0 00-2 2v6a2 2 0 002 2h10a2 2 0 002-2v-6a2 2 0 00-2-2h-.5V5.5A4.5 4.5 0 0010 1zm3 8V5.5a3 3 0 10-6 0V9h6z" clip-rule="evenodd" /></svg>
                        </button>
                    </div>`;
            
            let conversionHTML = '';
            if (participant.startWeight && participant.finalWeight) {
                const diff = participant.startWeight - participant.finalWeight;
                if (diff > 0) {
                    conversionHTML = `<p class="text-sm font-bold text-green-400">${langData.weightLossResult(diff.toFixed(1))}</p>`;
                } else if (diff < 0) {
                    conversionHTML = `<p class="text-sm font-bold text-yellow-400">${langData.weightGainResult(Math.abs(diff).toFixed(1))}</p>`;
                } else {
                    conversionHTML = `<p class="text-sm font-bold text-gray-400">${langData.weightSameResult}</p>`;
                }
            }
            
            const finalWeightTimestamp = participant.finalWeightUpdatedAt ? `<div class="text-xs text-red-500">${langData.savedOn}: ${formatTimestamp(participant.finalWeightUpdatedAt)}</div>` : '';

            card.innerHTML = `
                <div class="flex-grow flex justify-between items-start">
                    <div>
                        <h3 class="font-bold text-lg"><span class="${nameColorClass}">${participant.name}</span> <span class="text-sm font-normal text-gray-400">(${langData[participant.gender === 'Pria' ? 'genderMale' : 'genderFemale']})</span></h3>
                        <p class="text-sm text-gray-300">${participant.company}</p>
                    </div>
                    <button class="delete-btn p-2 text-red-500 hover:bg-red-500/10 rounded-full transition" aria-label="Hapus Peserta">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm4 0a1 1 0 012 0v6a1 1 0 11-2 0V8z" clip-rule="evenodd" /></svg>
                    </button>
                </div>
                <div class="space-y-3">
                    <div>
                        <label class="block text-sm font-medium text-gray-400">${langData.startWeightCardLabel}</label>
                        ${weightDisplayHTML}
                        <div class="text-xs text-red-500 mt-1">${langData.registeredOn}: ${formatTimestamp(participant.createdAt)}</div>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-400">${langData.finalWeightCardLabel}</label>
                        <div class="flex items-center gap-2">
                            <input type="number" step="0.1" placeholder="0.0" value="${participant.finalWeight || ''}" class="form-input w-full pr-10 text-sm final-weight-input">
                            <button class="update-btn p-2 bg-green-600/80 hover:bg-green-500 rounded-lg transition" aria-label="Simpan Berat Akhir">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" /></svg>
                            </button>
                        </div>
                        ${finalWeightTimestamp}
                    </div>
                    ${conversionHTML ? `<div class="pt-2 border-t border-gray-700">${conversionHTML}</div>` : ''}
                </div>`;
            elements.participantList.appendChild(card);
        }

        // --- MAIN APP LOGIC ---
        function initializeAppLogic() {
            const collectionPath = `/artifacts/${appId}/public/data/participants`;
            
            setLanguage('id'); // Set default language on load

            onSnapshot(collection(db, collectionPath), (snapshot) => {
                allParticipants = snapshot.docs;
                renderFilteredParticipants();
            });

            elements.filterGender.addEventListener('change', renderFilteredParticipants);
            elements.searchCompany.addEventListener('input', renderFilteredParticipants);

            elements.addForm.addEventListener('submit', async (e) => {
                e.preventDefault();
                const { name, company, gender, 'start-weight': startWeight, 'weight-key': weightKey } = elements.addForm;
                if (name.value && company.value && gender.value && startWeight.value) {
                    try {
                        let participantData = { name: name.value, company: company.value, gender: gender.value, startWeight: parseFloat(startWeight.value), finalWeight: null, isWeightVisible: true, createdAt: new Date(), finalWeightUpdatedAt: null, weightKey: null };
                        if (weightKey.value) {
                            participantData.weightKey = await hashString(weightKey.value);
                            participantData.isWeightVisible = false;
                        }
                        await addDoc(collection(db, collectionPath), participantData);
                        showNotification('notifSuccessAdd', 'success');
                        elements.addForm.reset();
                    } catch (error) { showNotification('notifErrorGeneric', 'error'); }
                } else { showNotification('notifErrorFillAll', 'error'); }
            });

            elements.participantList.addEventListener('click', async (e) => {
                const target = e.target.closest('button');
                if (!target) return;
                const card = target.closest('[data-id]');
                const id = card.getAttribute('data-id');
                const docRef = doc(db, collectionPath, id);

                if (target.classList.contains('delete-btn')) {
                    showModal(elements.deleteModal.el);
                    deleteCallback = async () => {
                        try {
                            await deleteDoc(docRef);
                            showNotification('notifSuccessDelete', 'success');
                        } catch (error) { showNotification('notifErrorGeneric', 'error'); }
                    };
                }
                
                if (target.classList.contains('update-btn')) {
                    const finalWeight = parseFloat(card.querySelector('.final-weight-input').value);
                    if (isNaN(finalWeight) || finalWeight <= 0) { showNotification('notifErrorInvalidWeight', 'error'); return; }
                    try {
                        await updateDoc(docRef, { finalWeight, finalWeightUpdatedAt: new Date() });
                        showNotification('notifSuccessUpdate', 'success');
                    } catch (error) { showNotification('notifErrorGeneric', 'error'); }
                }

                if (target.classList.contains('unlock-btn')) {
                    const keyInput = card.querySelector('.unlock-key-input');
                    if (!keyInput.value) { showNotification('notifErrorUnlock', 'error'); return; }
                    const participantDoc = allParticipants.find(p => p.id === id);
                    const storedHash = participantDoc.data().weightKey;
                    const enteredHash = await hashString(keyInput.value);
                    if (enteredHash === storedHash) {
                        await updateDoc(docRef, { isWeightVisible: true });
                        showNotification('notifSuccessUnlock', 'success');
                    } else { showNotification('notifErrorUnlock', 'error'); }
                }
            });
            
            // AI Modal Logic
            elements.ai.toggleBtn.addEventListener('click', () => elements.ai.modal.classList.add('show'));
            elements.ai.closeBtn.addEventListener('click', () => elements.ai.modal.classList.remove('show'));
            elements.ai.form.addEventListener('submit', async (e) => {
                e.preventDefault();
                const prompt = elements.ai.promptInput.value.trim();
                if (!prompt) return;
                
                if(elements.ai.responseArea.querySelector('p')?.textContent === translations[currentLanguage].aiGreeting){
                    elements.ai.responseArea.innerHTML = '';
                }

                elements.ai.responseArea.innerHTML += `<div class="text-right"><p class="bg-red-500 inline-block rounded-lg px-3 py-2">${prompt}</p></div>`;
                elements.ai.responseArea.innerHTML += `<div id="thinking" class="text-left"><p class="bg-gray-600 inline-block rounded-lg px-3 py-2">${translations[currentLanguage].aiThinking}</p></div>`;
                elements.ai.responseArea.scrollTop = elements.ai.responseArea.scrollHeight;
                elements.ai.promptInput.value = '';

                try {
                    const payload = { contents: [{ role: "user", parts: [{ text: prompt }] }] };
                    const apiKey = "";
                    const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;
                    const response = await fetch(apiUrl, { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(payload) });
                    const result = await response.json();
                    document.getElementById('thinking')?.remove();
                    if (result.candidates && result.candidates[0].content.parts[0].text) {
                        const text = result.candidates[0].content.parts[0].text;
                        elements.ai.responseArea.innerHTML += `<div class="text-left"><p class="bg-gray-600 inline-block rounded-lg px-3 py-2">${text.replace(/\n/g, '<br>')}</p></div>`;
                    } else {
                        elements.ai.responseArea.innerHTML += `<div class="text-left"><p class="bg-red-600 inline-block rounded-lg px-3 py-2">${translations[currentLanguage].notifErrorAI}</p></div>`;
                    }
                } catch(error) {
                    document.getElementById('thinking')?.remove();
                    elements.ai.responseArea.innerHTML += `<div class="text-left"><p class="bg-red-600 inline-block rounded-lg px-3 py-2">${translations[currentLanguage].notifErrorAIConnect}</p></div>`;
                }
                elements.ai.responseArea.scrollTop = elements.ai.responseArea.scrollHeight;
            });

            // Language Switcher Logic
            elements.langId.addEventListener('click', () => setLanguage('id'));
            elements.langEn.addEventListener('click', () => setLanguage('en'));
        }

        onAuthStateChanged(auth, async (user) => {
            if (user && !appInitialized) {
                appInitialized = true;
                initializeAppLogic();
            } else if (!user) {
                appInitialized = false;
                try {
                    if (initialAuthToken) await signInWithCustomToken(auth, initialAuthToken);
                    else await signInAnonymously(auth);
                } catch (error) { 
                    // Do not show error on initial load, as it might be a temporary connection issue.
                    console.error("Authentication failed:", error);
                }
            }
        });
    </script>
    
    <!-- 3D Background Script (Waving Flag) -->
    <script>
        let scene, camera, renderer, flag;
        let time = 0;

        function initFlag() {
            scene = new THREE.Scene();
            camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            renderer = new THREE.WebGLRenderer({ canvas: document.getElementById('bg-canvas'), alpha: true, antialias: true });
            renderer.setSize(window.innerWidth, window.innerHeight);
            camera.position.z = 5;

            const flagGeometry = new THREE.PlaneGeometry(10, 6, 50, 30);
            const flagMaterial = new THREE.ShaderMaterial({
                uniforms: {
                    time: { value: 0.0 }
                },
                vertexShader: `
                    uniform float time;
                    varying vec2 vUv;
                    void main() {
                        vUv = uv;
                        vec3 pos = position;
                        float waveX1 = 0.1 * sin(pos.x * 2.0 + time * 2.0);
                        float waveX2 = 0.05 * sin(pos.x * 3.0 + time * 1.5);
                        float waveY1 = 0.05 * sin(pos.y * 5.0 + time * 2.5);
                        pos.z += waveX1 + waveX2 + waveY1;
                        gl_Position = projectionMatrix * modelViewMatrix * vec4(pos, 1.0);
                    }
                `,
                fragmentShader: `
                    varying vec2 vUv;
                    void main() {
                        vec3 red = vec3(0.8, 0.1, 0.1);
                        vec3 white = vec3(0.95, 0.95, 0.95);
                        vec3 color = mix(white, red, step(0.5, vUv.y));
                        gl_FragColor = vec4(color, 1.0);
                    }
                `
            });

            flag = new THREE.Mesh(flagGeometry, flagMaterial);
            flag.rotation.x = -0.2;
            scene.add(flag);

            const ambientLight = new THREE.AmbientLight(0xffffff, 0.7);
            scene.add(ambientLight);
            const directionalLight = new THREE.DirectionalLight(0xffffff, 0.5);
            directionalLight.position.set(0, 1, 1);
            scene.add(directionalLight);

            animateFlag();
        }

        function animateFlag() {
            requestAnimationFrame(animateFlag);
            time += 0.01;
            flag.material.uniforms.time.value = time;
            renderer.render(scene, camera);
        }
        
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

        initFlag();
    </script>
</body>
</html>
