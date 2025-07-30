<!DOCTYPE html>
<html lang="en">
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
    
    <!-- Canvas Confetti for celebration -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>

    <style>
        html, body {
            height: 100%;
        }
        body {
            font-family: 'Inter', sans-serif;
            color: #e5e7eb; /* gray-200 */
            background-color: #030712; /* gray-950 as fallback */
            overflow: hidden; /* Prevent main page scroll */
            position: relative;
            display: flex;
            flex-direction: column;
        }
        /* New Flag Background */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: linear-gradient(to bottom, #ED2939 50%, #FFFFFF 50%);
        }
        body::after {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(3, 7, 18, 0.8); /* dark overlay */
            z-index: -1;
        }
        .main-container {
            position: relative;
            z-index: 1;
            flex-grow: 1; /* Make main container fill available space */
            overflow: hidden; /* Prevent this container from scrolling */
            display: flex;
            flex-direction: column;
        }
        header {
            position: sticky;
            top: 0;
            z-index: 30;
            background: rgba(31, 41, 55, 0.7); /* Updated transparency */
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            padding-top: 1.5rem;
            padding-bottom: 1.5rem;
            transition: all 0.3s ease;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            flex-shrink: 0;
        }
        footer {
            flex-shrink: 0;
        }
        .glass-card {
            background: rgba(31, 41, 55, 0.7); /* gray-800 */
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .btn-gradient-red {
            background-image: linear-gradient(to right, #dc2626, #ef4444); /* red-600 to red-500 */
            color: #ffffff;
            transition: all 0.3s ease;
        }
        .btn-gradient-red:hover {
            background-image: linear-gradient(to right, #b91c1c, #dc2626); /* red-700 to red-600 */
            transform: scale(1.02);
        }
        /* Button color */
        .btn-primary {
             background-image: linear-gradient(to right, #3b82f6, #8b5cf6); /* blue-500 to purple-500 */
        }
        .btn-primary:hover {
            background-image: linear-gradient(to right, #2563eb, #7c3aed); /* blue-600 to purple-600 */
            transform: scale(1.02);
        }
        /* New text gradient for titles */
        .text-gradient-primary {
            background-image: linear-gradient(to right, #3b82f6, #a78bfa); /* blue-500 to purple-400 */
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        /* New static gradient for "2025" and main title */
        .text-flag-gradient {
            background: linear-gradient(to bottom, #ED2939 50%, #FFFFFF 50%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            display: inline-block; /* Needed for gradient to apply correctly */
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
            border-color: #8b5cf6; /* purple-500 */
            box-shadow: 0 0 0 2px rgba(139, 92, 246, 0.5);
        }
        .form-input:disabled {
            background-color: rgba(55, 65, 81, 0.2);
            cursor: not-allowed;
            opacity: 0.6;
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
            0% { box-shadow: 0 0 0 0 rgba(96, 165, 250, 0.7); } /* Bright Blue */
            70% { box-shadow: 0 0 0 12px rgba(96, 165, 250, 0); }
            100% { box-shadow: 0 0 0 0 rgba(96, 165, 250, 0); }
        }
        .pulsing-ring {
            border-radius: 9999px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            border: 2px solid #60a5fa; /* blue-400 */
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
        #winner-trigger {
            cursor: pointer;
            transition: all 0.2s ease-in-out;
        }
        #winner-trigger:hover {
            filter: brightness(1.2);
            transform: scale(1.05);
        }
        /* Custom scrollbar */
        .scroll-container::-webkit-scrollbar {
            width: 8px;
        }
        .scroll-container::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
        }
        .scroll-container::-webkit-scrollbar-thumb {
            background: #8b5cf6; /* purple-500 */
            border-radius: 10px;
        }
        .scroll-container::-webkit-scrollbar-thumb:hover {
            background: #7c3aed; /* purple-600 */
        }

        /* Neuron Animation */
        .neuron-path {
            stroke-dasharray: 1000;
            stroke-dashoffset: 1000;
            animation: dash 2.5s linear infinite;
        }
        .neuron-core {
            animation: pulse-glow 1.5s ease-in-out infinite;
        }
        @keyframes dash {
            from { stroke-dashoffset: 1000; }
            to { stroke-dashoffset: 0; }
        }
        @keyframes pulse-glow {
            0%, 100% { filter: drop-shadow(0 0 2px #fff) drop-shadow(0 0 5px #fff) drop-shadow(0 0 10px #3b82f6); }
            50% { filter: drop-shadow(0 0 5px #fff) drop-shadow(0 0 10px #3b82f6) drop-shadow(0 0 20px #3b82f6); }
        }


        /* Mobile Slider Styles */
        .mobile-tab-button {
            padding: 0.75rem 1rem;
            border-bottom: 3px solid transparent;
            color: #9ca3af; /* gray-400 */
            font-weight: 600;
            transition: all 0.3s ease;
            display: flex;
            justify-content: center;
            align-items: center;
            flex: 1;
        }
        .mobile-tab-button.active {
            color: #ffffff;
            border-bottom-color: #8b5cf6; /* purple-500 */
        }
        @media (max-width: 1023px) { /* Below lg */
            #slider.slide-to-list {
                transform: translateX(-100%);
            }
        }
        #countdown-modal {
            transition: background-color 0.5s ease;
        }
        #countdown-number {
            font-size: 15rem; /* Larger countdown number */
        }
        /* Waving text animation */
        #wavy-welcome {
            font-size: clamp(1.5rem, 8vw, 4rem);
            line-height: 1.2;
            max-width: 80vw;
        }
        #wavy-welcome span {
            position: relative;
            display: inline-block;
            animation: wave 1.5s infinite;
            animation-delay: calc(.1s * var(--i));
        }
        @keyframes wave {
            0%, 40%, 100% {
                transform: translateY(0);
            }
            20% {
                transform: translateY(-10px);
            }
        }
    </style>
</head>
<body>
    <!-- Welcome Overlay -->
    <div id="welcome-overlay" class="fixed inset-0 bg-black z-[100] flex flex-col items-center justify-center text-center p-4 transition-opacity duration-1000">
        <div class="flex-grow flex flex-col items-center justify-center">
            <h1 id="wavy-welcome" class="font-black text-flag-gradient mb-4 tracking-tight"></h1>
        </div>
        <footer class="w-full text-center py-4 text-gray-400 text-sm">
            <a href="http://www.jatrahotels.com" target="_blank" rel="noopener noreferrer" class="text-flag-gradient hover:brightness-125 transition text-lg font-bold">www.jatrahotels.com</a>
        </footer>
    </div>

    <!-- Notification Container -->
    <div id="notification-container" class="fixed top-24 right-5 z-50 flex flex-col items-end gap-3 w-full max-w-xs"></div>

    <!-- Modals -->
    <div id="modal-backdrop" class="fixed inset-0 bg-black bg-opacity-70 z-40 hidden"></div>
    <div id="delete-modal" class="fixed inset-0 z-50 flex items-center justify-center hidden p-4">
        <div class="glass-card rounded-2xl p-6 shadow-2xl w-full max-w-sm text-center">
            <h3 class="text-xl font-bold text-white mb-4">Confirm Deletion</h3>
            <p class="text-gray-300 mb-4">Enter admin password to delete.</p>
            <input type="password" id="delete-password" class="form-input mb-6" placeholder="Admin Password">
            <div class="flex justify-center gap-4">
                <button id="delete-cancel-btn" class="bg-gray-600 hover:bg-gray-500 text-white font-bold py-2 px-6 rounded-lg transition">Cancel</button>
                <button id="delete-confirm-btn" class="bg-red-600 hover:bg-red-500 text-white font-bold py-2 px-6 rounded-lg transition">Delete</button>
            </div>
        </div>
    </div>
    <div id="winner-password-modal" class="fixed inset-0 z-50 flex items-center justify-center hidden p-4">
        <div class="glass-card rounded-2xl p-6 shadow-2xl w-full max-w-sm text-center">
            <h3 class="text-xl font-bold text-white mb-4">View Winner</h3>
            <p class="text-gray-300 mb-4">Enter admin password to view the winner.</p>
            <input type="password" id="view-winner-password" class="form-input mb-6" placeholder="Admin Password">
            <div class="flex justify-center gap-4">
                <button id="view-winner-cancel-btn" class="bg-gray-600 hover:bg-gray-500 text-white font-bold py-2 px-6 rounded-lg transition">Cancel</button>
                <button id="view-winner-confirm-btn" class="btn-gradient-red text-white font-bold py-2 px-6 rounded-lg">View</button>
            </div>
        </div>
    </div>
    
    <!-- Fullscreen Winner Modal -->
    <div id="winner-modal" class="fixed inset-0 z-40 bg-black/90 backdrop-blur-sm flex items-center justify-center hidden p-4">
        <button id="winner-modal-close-btn" class="absolute top-5 right-5 p-2 text-gray-400 hover:text-white hover:bg-white/10 rounded-full z-50">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
        </button>
        <div class="reveal-animation w-full max-w-2xl">
            <div class="glass-card rounded-2xl p-8 shadow-2xl text-center flex flex-col justify-center items-center">
                <svg id="crown-icon" class="mx-auto h-16 w-16 text-yellow-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M5 16L3 5L8.5 9.5L12 4L15.5 9.5L21 5L19 16H5M19 19C19 19.55 18.55 20 18 20H6C5.45 20 5 19.55 5 19V18H19V19Z" />
                </svg>
                <div id="winner-display" class="hidden text-left space-y-2 mt-4">
                    <h2 class="text-3xl font-bold title-gradient text-center">Congratulations to the Winner!</h2>
                    <p class="text-xl text-white"><strong class="text-gray-400">Name:</strong> <span id="winner-name-display"></span></p>
                    <p class="text-xl text-white"><strong class="text-gray-400">Gender:</strong> <span id="winner-gender-display"></span></p>
                    <p class="text-xl text-white"><strong class="text-gray-400">Company:</strong> <span id="winner-company-display"></span></p>
                    <p class="text-xl text-white"><strong class="text-gray-400">Start Weight:</strong> <span id="winner-start-weight-display"></span> kg</p>
                    <p class="text-xl text-white"><strong class="text-gray-400">Final Weight:</strong> <span id="winner-final-weight-display"></span> kg</p>
                    <p class="text-2xl text-green-400 font-bold text-center pt-2"><strong class="text-gray-400">Total Loss:</strong> <span id="winner-result-display"></span> kg</p>
                </div>
                <div id="no-winner-display">
                    <h2 class="text-2xl font-bold text-white mt-4">Awaiting Winner</h2>
                    <p class="text-gray-400 mt-1">The winner will be announced after all data is filled.</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Countdown Modal -->
    <div id="countdown-modal" class="fixed inset-0 z-50 bg-black/95 flex items-center justify-center hidden">
        <span id="countdown-number" class="font-black transition-colors duration-500"></span>
    </div>

    <!-- AI Modal -->
    <div id="ai-modal" class="ai-modal">
        <div class="glass-card rounded-2xl w-full h-full flex flex-col p-6">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-2xl font-bold text-gradient-primary">Ask AI</h2>
                <button id="ai-close-btn" class="p-2 text-gray-400 hover:text-white hover:bg-white/10 rounded-full">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
                </button>
            </div>
            <div id="ai-response-area" class="flex-grow bg-black/20 rounded-lg p-4 overflow-y-auto mb-4 text-gray-300 space-y-4">
                <p>Hello! What healthy insights can I get for you today?</p>
            </div>
            <form id="ai-form" class="flex gap-4">
                <input type="text" id="ai-prompt" class="form-input flex-grow py-3" placeholder="Type your question here...">
                <button type="submit" class="btn-primary text-white font-bold py-2 px-6 rounded-lg flex items-center gap-2">
                    Send
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path d="M10.894 2.553a1 1 0 00-1.788 0l-7 14a1 1 0 001.169 1.409l5-1.429A1 1 0 009 15.571V11a1 1 0 112 0v4.571a1 1 0 00.725.962l5 1.428a1 1 0 001.17-1.408l-7-14z" /></svg>
                </button>
            </form>
        </div>
    </div>

    <header>
        <div class="container mx-auto px-4 relative flex flex-col justify-center items-center">
            <h1 class="text-2xl sm:text-3xl md:text-4xl font-black text-flag-gradient tracking-tight text-center">
                August Slimdown Challenge <span id="winner-trigger">2025</span>
            </h1>
            <div id="challenge-countdown" class="text-center text-white text-lg md:text-xl font-bold mt-2"></div>
        </div>
    </header>

    <div class="main-container container mx-auto px-4 pt-4 pb-8 md:py-12 flex flex-col">
        
        <!-- Mobile Tab Navigation -->
        <div id="mobile-tab-nav" class="lg:hidden flex justify-around border-b border-gray-700 mb-4">
            <button data-tab="add" class="mobile-tab-button active">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M19 7.5v3m0 0v3m0-3h3m-3 0h-3m-2.25-4.125a3.375 3.375 0 11-6.75 0 3.375 3.375 0 016.75 0zM4 19.235v-.11a6.375 6.375 0 0112.75 0v.109A12.318 12.318 0 0110.5 21.75c-2.676 0-5.216-.584-7.5-1.636z" />
                </svg>
            </button>
            <button data-tab="list" class="mobile-tab-button">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" viewBox="0 0 24 24" fill="currentColor"><path d="M4 6h16v2H4zm0 5h16v2H4zm0 5h16v2H4z"/></svg>
            </button>
        </div>
        
        <!-- Main Content Slider -->
        <div class="flex-grow overflow-hidden">
            <div id="slider" class="flex h-full transition-transform duration-500 ease-in-out lg:grid lg:grid-cols-2 lg:gap-6">
                
                <!-- Slide 1: Add Participant -->
                <div class="w-full flex-shrink-0 lg:w-auto reveal-animation flex flex-col h-full">
                    <div class="glass-card rounded-2xl p-6 shadow-2xl h-full flex flex-col">
                        <div class="flex-shrink-0">
                             <div class="flex justify-between items-center mb-6 gap-4">
                                <h2 class="text-2xl font-bold text-gradient-primary">Add New Participant</h2>
                                <button id="ai-toggle-btn" class="bg-transparent p-1 rounded-full transform hover:scale-110 transition-transform flex flex-col items-center">
                                    <span class="text-xs text-white mb-1">Ask AI</span>
                                    <svg class="h-8 w-8 text-white" viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
                                        <path class="neuron-path" d="M32 5V18M32 46V59M44 32H58M6 32H20M16.858 16.858L25 25M39 39L47.142 47.142M16.858 47.142L25 39M39 25L47.142 16.858" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                                        <circle class="neuron-core" cx="32" cy="32" r="8" fill="currentColor"/>
                                    </svg>
                                </button>
                            </div>
                            <div class="mb-4">
                               <input type="text" id="name" form="add-participant-form" name="name" class="form-input" placeholder="Participant's Name">
                            </div>
                        </div>
                        <div class="flex-grow overflow-y-auto pr-2 scroll-container">
                            <form id="add-participant-form" class="space-y-4">
                                <select id="company" name="company" class="form-input">
                                    <option value="">Select Company</option>
                                    <option value="Grand Jatra Hotel Pekanbaru">Grand Jatra Hotel Pekanbaru</option>
                                    <option value="Grand Jatra Hotel Balikpapan">Grand Jatra Hotel Balikpapan</option>
                                    <option value="Astara Hotel Balikpapan">Astara Hotel Balikpapan</option>
                                    <option value="Pentacity Hotel Balikpapan">Pentacity Hotel Balikpapan</option>
                                    <option value="Stark Boutique Hotel Bali">Stark Boutique Hotel Bali</option>
                                    <option value="J-Icon Hotel Balikpapan">J-Icon Hotel Balikpapan</option>
                                </select>
                                <select id="department" name="department" class="form-input">
                                    <option value="">Select Department</option>
                                    <option value="Admin and General">Admin and General</option>
                                    <option value="Human Resource">Human Resource</option>
                                    <option value="Accounting">Accounting</option>
                                    <option value="Front Office">Front Office</option>
                                    <option value="Housekeeping">Housekeeping</option>
                                    <option value="F&B Product">F&B Product</option>
                                    <option value="F&B Service">F&B Service</option>
                                </select>
                                <select id="community" name="community" class="form-input">
                                    <option value="">Select Community</option>
                                    <option value="Personal">Personal</option>
                                </select>
                                <select id="gender" name="gender" class="form-input">
                                    <option value="">Select Gender</option>
                                    <option value="Male">Male</option>
                                    <option value="Female">Female</option>
                                </select>
                                <div>
                                    <label for="start-weight" class="block text-sm font-medium text-gray-400 mb-1">Start Weight (1 August)</label>
                                    <div class="relative">
                                        <input type="number" step="0.1" id="start-weight" name="start-weight" class="form-input pr-10" placeholder="0.0">
                                        <span class="absolute inset-y-0 right-3 flex items-center text-gray-400">kg</span>
                                    </div>
                                </div>
                                <div>
                                    <input type="password" id="weight-key" name="weight-key" class="form-input" placeholder="Create Key to Hide Weight (Optional)">
                                    <p class="text-xs text-gray-400 mt-2">Note: Please choose either Company/Department or Community. You do not need to fill both.</p>
                                </div>
                            </form>
                        </div>
                        <div class="flex-shrink-0 pt-4">
                             <button id="register-btn" type="submit" form="add-participant-form" class="w-full btn-primary font-bold py-3 px-4 rounded-lg shadow-lg transition-transform">
                                Register
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Slide 2: Participant List -->
                <div class="w-full flex-shrink-0 lg:w-auto reveal-animation flex flex-col h-full" style="animation-delay: 0.2s;">
                    <div class="glass-card rounded-2xl p-6 shadow-2xl h-full flex flex-col">
                        <div class="flex-shrink-0">
                            <div class="flex justify-between items-start mb-6 gap-4">
                                <h2 class="text-2xl font-bold text-gradient-primary">Participant List</h2>
                                <div class="flex items-center gap-2">
                                    <div id="percentage-indicator" class="text-lg"></div>
                                    <div class="pulsing-ring p-1">
                                        <span class="text-3xl font-black text-gradient-primary min-w-[40px] text-center" id="participant-count">0</span>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                                <select id="filter-gender" class="form-input" aria-label="Filter Gender">
                                    <option value="All">All Genders</option>
                                    <option value="Male">Male</option>
                                    <option value="Female">Female</option>
                                </select>
                                <select id="filter-company" class="form-input" aria-label="Filter Company">
                                    <option value="All">All Companies</option>
                                    <option value="Grand Jatra Hotel Pekanbaru">Grand Jatra Hotel Pekanbaru</option>
                                    <option value="Grand Jatra Hotel Balikpapan">Grand Jatra Hotel Balikpapan</option>
                                    <option value="Astara Hotel Balikpapan">Astara Hotel Balikpapan</option>
                                    <option value="Pentacity Hotel Balikpapan">Pentacity Hotel Balikpapan</option>
                                    <option value="Stark Boutique Hotel Bali">Stark Boutique Hotel Bali</option>
                                    <option value="J-Icon Hotel Balikpapan">J-Icon Hotel Balikpapan</option>
                                </select>
                                <select id="filter-department" class="form-input" aria-label="Filter Department">
                                    <option value="All">All Departments</option>
                                    <option value="Admin and General">Admin and General</option>
                                    <option value="Human Resource">Human Resource</option>
                                    <option value="Accounting">Accounting</option>
                                    <option value="Front Office">Front Office</option>
                                    <option value="Housekeeping">Housekeeping</option>
                                    <option value="F&B Product">F&B Product</option>
                                    <option value="F&B Service">F&B Service</option>
                                </select>
                                <select id="filter-community" class="form-input" aria-label="Filter Community">
                                    <option value="All">All Communities</option>
                                    <option value="Personal">Personal</option>
                                </select>
                            </div>
                        </div>

                        <div id="participant-list" class="flex flex-col gap-4 overflow-y-scroll flex-grow pr-2 scroll-container lg:max-h-[34rem]">
                            <!-- Participant cards are rendered here by JS -->
                        </div>
                    </div>
                </div>

            </div>
        </div>
        
    </div>
    
    <footer class="text-center py-4 text-gray-400 text-sm">
        <a href="http://www.jatrahotels.com" target="_blank" rel="noopener noreferrer" class="text-flag-gradient hover:brightness-125 transition text-lg font-bold">www.jatrahotels.com</a>
    </footer>

    <!-- Firebase SDK -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, addDoc, onSnapshot, doc, deleteDoc, updateDoc, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        const appId = typeof __app_id !== 'undefined' ? __app_id : 'slimdown-challenge-2025';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : { 
            apiKey: "AIzaSyDQvtYoVomVoKBvh2UKlx-unF23Hhs9MhI",
            authDomain: "slimdownchallenge2025.firebaseapp.com",
            projectId: "slimdownchallenge2025",
            storageBucket: "slimdownchallenge2025.firebasestorage.app",
            messagingSenderId: "987445662572",
            appId: "1:987445662572:web:dccad49c1875f77f83d949"
        };
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);

        // DOM Elements & Global State
        const elements = {
            welcomeOverlay: document.getElementById('welcome-overlay'),
            wavyWelcome: document.getElementById('wavy-welcome'),
            participantList: document.getElementById('participant-list'),
            participantCount: document.getElementById('participant-count'),
            percentageIndicator: document.getElementById('percentage-indicator'),
            addForm: document.getElementById('add-participant-form'),
            addCompany: document.getElementById('company'),
            addDepartment: document.getElementById('department'),
            addCommunity: document.getElementById('community'),
            registerBtn: document.getElementById('register-btn'),
            challengeCountdown: document.getElementById('challenge-countdown'),
            filterGender: document.getElementById('filter-gender'),
            filterCompany: document.getElementById('filter-company'),
            filterDepartment: document.getElementById('filter-department'),
            filterCommunity: document.getElementById('filter-community'),
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
            winnerModal: {
                el: document.getElementById('winner-modal'),
                closeBtn: document.getElementById('winner-modal-close-btn'),
                display: document.getElementById('winner-display'),
                noWinner: document.getElementById('no-winner-display'),
                name: document.getElementById('winner-name-display'),
                gender: document.getElementById('winner-gender-display'),
                company: document.getElementById('winner-company-display'),
                startWeight: document.getElementById('winner-start-weight-display'),
                finalWeight: document.getElementById('winner-final-weight-display'),
                result: document.getElementById('winner-result-display')
            },
            countdownModal: {
                el: document.getElementById('countdown-modal'),
                number: document.getElementById('countdown-number')
            },
            winnerTrigger: document.getElementById('winner-trigger'),
            ai: {
                modal: document.getElementById('ai-modal'),
                toggleBtn: document.getElementById('ai-toggle-btn'),
                closeBtn: document.getElementById('ai-close-btn'),
                form: document.getElementById('ai-form'),
                promptInput: document.getElementById('ai-prompt'),
                responseArea: document.getElementById('ai-response-area')
            },
            mobileTabNav: document.getElementById('mobile-tab-nav'),
            slider: document.getElementById('slider')
        };
        
        let allParticipants = []; 
        let deleteCallback = null;
        let determinedWinner = null;
        let unsubscribeFromParticipants = null;
        let confettiInterval = null;

        // --- HELPER FUNCTIONS ---
        async function hashString(str) {
            const data = new TextEncoder().encode(str);
            const hashBuffer = await crypto.subtle.digest('SHA-256', data);
            return Array.from(new Uint8Array(hashBuffer)).map(b => b.toString(16).padStart(2, '0')).join('');
        }

        function showNotification(message, type = 'success') {
            const borderColor = type === 'success' ? 'border-green-500' : 'border-red-500';
            const notif = document.createElement('div');
            notif.className = `notification glass-card p-4 rounded-lg shadow-lg w-full border-l-4 ${borderColor}`;
            notif.innerHTML = `<p class="text-white font-medium">${message}</p>`;
            elements.notificationContainer.appendChild(notif);
            setTimeout(() => { notif.classList.add('show'); }, 10);
            setTimeout(() => {
                notif.classList.remove('show');
                notif.addEventListener('transitionend', () => notif.remove());
            }, 3000);
        }

        function showModal(modalElement) {
            elements.modalBackdrop.classList.remove('hidden');
            modalElement.classList.remove('hidden');
        }

        function hideAllModals() {
            elements.modalBackdrop.classList.add('hidden');
            elements.deleteModal.el.classList.add('hidden');
            elements.winnerPasswordModal.el.classList.add('hidden');
            elements.winnerModal.el.classList.add('hidden');
            elements.countdownModal.el.classList.add('hidden');
        }
        
        function formatTimestamp(timestamp) {
            if (!timestamp || !timestamp.seconds) return '';
            const date = new Date(timestamp.seconds * 1000);
            return date.toLocaleString('en-GB', {
                day: '2-digit', month: 'short', year: 'numeric', hour: '2-digit', minute: '2-digit'
            });
        }

        function startContinuousConfetti() {
            if (confettiInterval) return;
            const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 100, colors: ['#EF4444', '#F87171', '#FCA5A5', '#FFFFFF'] };
            function randomInRange(min, max) { return Math.random() * (max - min) + min; }
            confettiInterval = setInterval(function() {
                confetti({ ...defaults, particleCount: 50, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 } });
                confetti({ ...defaults, particleCount: 50, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 } });
            }, 250);
        }

        function stopContinuousConfetti() {
            if (confettiInterval) {
                clearInterval(confettiInterval);
                confettiInterval = null;
            }
        }

        function checkAndHandleWinnerState() {
            if (allParticipants.length === 0) {
                determinedWinner = null;
                return;
            }
            const allFilled = allParticipants.every(doc => doc.data().finalWeight !== null && doc.data().finalWeight > 0);
            
            if (allFilled) {
                let winnerCandidate = null;
                let maxLoss = -Infinity;

                for (const doc of allParticipants) {
                    const participantData = doc.data();
                    if (participantData.startWeight && participantData.finalWeight) {
                        const loss = participantData.startWeight - participantData.finalWeight;
                        if (loss > maxLoss) {
                            maxLoss = loss;
                            winnerCandidate = { ...participantData, id: doc.id };
                        }
                    }
                }
                
                if (winnerCandidate) {
                    determinedWinner = { ...winnerCandidate, loss: maxLoss };
                } else {
                    determinedWinner = null;
                }
            } else {
                determinedWinner = null;
            }
        }
        
        function renderFilteredParticipants() {
            const genderFilter = elements.filterGender.value;
            const companyFilter = elements.filterCompany.value;
            const departmentFilter = elements.filterDepartment.value;
            const communityFilter = elements.filterCommunity.value;

            const filtered = allParticipants.filter(doc => {
                const p = doc.data();
                const genderMatch = (genderFilter === 'All') || (p.gender === genderFilter);
                const companyMatch = (companyFilter === 'All') || (p.company === companyFilter);
                const departmentMatch = (departmentFilter === 'All') || (p.department === departmentFilter);
                const communityMatch = (communityFilter === 'All') || (p.community === communityFilter);
                return genderMatch && companyMatch && departmentMatch && communityMatch;
            });
            
            elements.participantList.innerHTML = '';
            elements.participantCount.textContent = filtered.length;

            const baseline = 6;
            let percentage = 0;
            if (filtered.length !== baseline) {
                percentage = ((filtered.length - baseline) / baseline) * 100;
            }

            let indicatorHTML = '';
            if (filtered.length < baseline) {
                indicatorHTML = `<span class="text-red-500 flex items-center"><svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-11a1 1 0 10-2 0v4a1 1 0 102 0V7z" clip-rule="evenodd" /></svg>${percentage.toFixed(0)}%</span>`;
            } else if (filtered.length > baseline) {
                indicatorHTML = `<span class="text-green-500 flex items-center"><svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 0l-3 3a1 1 0 001.414 1.414L9 9.414V13a1 1 0 102 0V9.414l1.293 1.293a1 1 0 001.414-1.414z" clip-rule="evenodd" /></svg>${percentage.toFixed(0)}%</span>`;
            } else {
                 indicatorHTML = `<span class="text-gray-400">0%</span>`;
            }
            elements.percentageIndicator.innerHTML = indicatorHTML;


            if (filtered.length === 0) {
                elements.participantList.innerHTML = `<p class="text-center text-gray-400 py-4">No matching participants found.</p>`;
            } else {
                filtered.forEach(doc => renderParticipantCard(doc));
            }
        }

        function renderParticipantCard(doc) {
            const participant = doc.data();
            const card = document.createElement('div');
            card.className = 'glass-card rounded-lg p-4 flex flex-col gap-4 reveal-animation flex-shrink-0';
            card.setAttribute('data-id', doc.id);

            const nameColorClass = participant.gender === 'Male' ? 'text-blue-400' : 'text-green-400';
            
            let affiliationHTML = '';
            if (participant.company) {
                affiliationHTML = `<p class="text-sm text-gray-300">${participant.company} - ${participant.department || 'N/A'}</p>`;
            } else if (participant.community) {
                affiliationHTML = `<p class="text-sm text-gray-300">Community: ${participant.community}</p>`;
            }

            let weightDisplayHTML = participant.isWeightVisible
                ? `<p class="text-sm text-red-400"><strong>${participant.startWeight} kg</strong></p>`
                : `<div class="flex items-center gap-2">
                        <input type="password" class="form-input text-sm flex-grow unlock-key-input" placeholder="Enter Key to View Weight">
                        <button class="unlock-btn p-2 bg-red-600/80 hover:bg-red-500 rounded-lg transition" aria-label="Unlock Start Weight">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M10 1a4.5 4.5 0 00-4.5 4.5V9H5a2 2 0 00-2 2v6a2 2 0 002 2h10a2 2 0 002-2v-6a2 2 0 00-2-2h-.5V5.5A4.5 4.5 0 0010 1zm3 8V5.5a3 3 0 10-6 0V9h6z" clip-rule="evenodd" /></svg>
                        </button>
                    </div>`;
            
            let conversionHTML = '';
            if (participant.startWeight && participant.finalWeight) {
                const diff = participant.startWeight - participant.finalWeight;
                const percentage = (diff / participant.startWeight) * 100;
                let percentageHTML = '';

                if (diff > 0) {
                    percentageHTML = `<span class="text-green-400 text-xs flex items-center ml-2">(<svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3 mr-1" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 0l-3 3a1 1 0 001.414 1.414L9 9.414V13a1 1 0 102 0V9.414l1.293 1.293a1 1 0 001.414-1.414z" clip-rule="evenodd" /></svg>${percentage.toFixed(1)}%)</span>`;
                    conversionHTML = `<p class="text-sm font-bold text-green-400 flex items-center">Lost ${diff.toFixed(1)} kg ${percentageHTML}</p>`;
                } else if (diff < 0) {
                     percentageHTML = `<span class="text-red-400 text-xs flex items-center ml-2">(<svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3 mr-1" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-11a1 1 0 10-2 0v4a1 1 0 102 0V7z" clip-rule="evenodd" /></svg>${Math.abs(percentage).toFixed(1)}%)</span>`;
                    conversionHTML = `<p class="text-sm font-bold text-yellow-400 flex items-center">Gained ${Math.abs(diff).toFixed(1)} kg ${percentageHTML}</p>`;
                } else {
                    conversionHTML = `<p class="text-sm font-bold text-gray-400">Weight Unchanged</p>`;
                }
            }
            
            const finalWeightTimestamp = participant.finalWeightUpdatedAt ? `<div class="text-xs text-red-500">Saved: ${formatTimestamp(participant.finalWeightUpdatedAt)}</div>` : '';

            card.innerHTML = `
                <div class="flex-grow flex justify-between items-start">
                    <div>
                        <h3 class="font-bold text-lg"><span class="${nameColorClass}">${participant.name}</span> <span class="text-sm font-normal text-gray-400">(${participant.gender})</span></h3>
                        ${affiliationHTML}
                    </div>
                    <button class="delete-btn p-2 text-red-500 hover:bg-red-500/10 rounded-full transition" aria-label="Delete Participant">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm4 0a1 1 0 012 0v6a1 1 0 11-2 0V8z" clip-rule="evenodd" /></svg>
                    </button>
                </div>
                <div class="space-y-3">
                    <div>
                        <label class="block text-sm font-medium text-gray-400">Start Weight (1 Aug)</label>
                        ${weightDisplayHTML}
                        <div class="text-xs text-red-500 mt-1">Registered: ${formatTimestamp(participant.createdAt)}</div>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-400">Final Weight (31 Aug)</label>
                        <div class="flex items-center gap-2">
                            <input type="number" step="0.1" placeholder="0.0" value="${participant.finalWeight || ''}" class="form-input w-full pr-10 text-sm final-weight-input">
                            <button class="update-btn p-2 bg-green-600/80 hover:bg-green-500 rounded-lg transition" aria-label="Save Final Weight">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" /></svg>
                            </button>
                        </div>
                        ${finalWeightTimestamp}
                    </div>
                    ${conversionHTML ? `<div class="pt-2 border-t border-gray-700">${conversionHTML}</div>` : ''}
                </div>`;
            elements.participantList.appendChild(card);
        }

        function startCountdown() {
            let count = 8;
            const colors = [
                { bg: 'bg-red-600', text: 'text-white' },
                { bg: 'bg-white', text: 'text-black' },
                { bg: 'bg-red-600', text: 'text-white' },
                { bg: 'bg-white', text: 'text-black' },
                { bg: 'bg-red-600', text: 'text-white' },
                { bg: 'bg-white', text: 'text-black' },
                { bg: 'bg-red-600', text: 'text-white' },
                { bg: 'bg-white', text: 'text-black' },
            ];
            
            elements.countdownModal.el.classList.remove('hidden');
            
            const updateCountdown = () => {
                if (count > 0) {
                    const color = colors[count - 1] || colors[0];
                    elements.countdownModal.el.className = `fixed inset-0 z-50 flex items-center justify-center transition-colors duration-500 ${color.bg}`;
                    elements.countdownModal.number.className = `font-black transition-colors duration-500 ${color.text}`;
                    elements.countdownModal.number.textContent = count;
                    elements.countdownModal.number.style.fontSize = '15rem';
                }
            };

            updateCountdown();

            const countdownInterval = setInterval(() => {
                count--;
                if (count < 1) {
                    clearInterval(countdownInterval);
                    elements.countdownModal.number.textContent = "Are You Ready???";
                    elements.countdownModal.number.style.fontSize = '5rem';
                    setTimeout(() => {
                        hideAllModals();
                        elements.winnerModal.el.classList.remove('hidden');
                        startContinuousConfetti();
                    }, 3000);
                } else {
                    updateCountdown();
                }
            }, 1000);
        }

        function startChallengeCountdown() {
            const challengeStart = new Date('2025-08-01T00:00:00+08:00').getTime();
            const challengeEnd = new Date('2025-08-31T23:59:59+08:00').getTime();

            const interval = setInterval(() => {
                const now = new Date().getTime();
                const nowWITA = now + (new Date().getTimezoneOffset() * 60000) + (8 * 3600000);

                if (nowWITA < challengeStart) {
                    const distance = challengeStart - nowWITA;
                    const days = Math.floor(distance / (1000 * 60 * 60 * 24));
                    const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                    const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
                    const seconds = Math.floor((distance % (1000 * 60)) / 1000);
                    elements.challengeCountdown.innerHTML = `Challenge starts in: ${days}d ${hours}h ${minutes}m ${seconds}s`;
                } else if (nowWITA >= challengeStart && nowWITA <= challengeEnd) {
                    elements.challengeCountdown.innerHTML = `<span class="text-green-400">Challenge is ON!</span>`;
                } else {
                    elements.challengeCountdown.innerHTML = `<span class="text-red-400">Challenge has ended.</span>`;
                    // Disable form
                    elements.addForm.querySelectorAll('input, select').forEach(el => el.disabled = true);
                    elements.registerBtn.disabled = true;
                    elements.registerBtn.classList.add('opacity-50', 'cursor-not-allowed');
                }
            }, 1000);
        }

        // --- ATTACH UI LISTENERS ONCE ---
        function attachUIListeners() {
            const welcomeText = "Welcome to the August Slimdown Challenge 2025";
            elements.wavyWelcome.innerHTML = welcomeText.split('').map((letter, i) => `<span style="--i:${i}">${letter === ' ' ? '&nbsp;' : letter}</span>`).join('');
            setTimeout(() => {
                elements.welcomeOverlay.style.opacity = '0';
                elements.welcomeOverlay.addEventListener('transitionend', () => elements.welcomeOverlay.classList.add('hidden'));
            }, 3000);


            elements.deleteModal.confirmBtn.addEventListener('click', () => {
                if (elements.deleteModal.passwordInput.value === '131dualima') {
                    if (deleteCallback) deleteCallback();
                    hideAllModals();
                } else { showNotification('Incorrect admin password.', 'error'); }
            });
            elements.deleteModal.cancelBtn.addEventListener('click', hideAllModals);
            elements.winnerPasswordModal.cancelBtn.addEventListener('click', hideAllModals);
            
            elements.winnerModal.closeBtn.addEventListener('click', () => {
                hideAllModals();
                stopContinuousConfetti();
            });

            elements.winnerTrigger.addEventListener('click', () => {
                checkAndHandleWinnerState();
                if (determinedWinner) {
                    elements.winnerModal.display.classList.remove('hidden');
                    elements.winnerModal.noWinner.classList.add('hidden');
                    elements.winnerModal.name.textContent = determinedWinner.name;
                    elements.winnerModal.gender.textContent = determinedWinner.gender;
                    elements.winnerModal.company.textContent = determinedWinner.company;
                    elements.winnerModal.startWeight.textContent = determinedWinner.startWeight;
                    elements.winnerModal.finalWeight.textContent = determinedWinner.finalWeight;
                    elements.winnerModal.result.textContent = determinedWinner.loss.toFixed(1);
                    showModal(elements.winnerPasswordModal.el);
                } else {
                    showNotification('Not all final weights have been entered.', 'error');
                }
            });

            elements.winnerPasswordModal.confirmBtn.addEventListener('click', () => {
                if (elements.winnerPasswordModal.passwordInput.value === '131dualima') {
                    hideAllModals();
                    startCountdown();
                } else {
                    showNotification('Incorrect admin password.', 'error');
                }
            });

            // --- Form Locking Logic ---
            elements.addCompany.addEventListener('change', (e) => {
                if (e.target.value) {
                    elements.addCommunity.value = '';
                    elements.addCommunity.disabled = true;
                } else {
                    elements.addCommunity.disabled = false;
                }
            });

            elements.addCommunity.addEventListener('change', (e) => {
                if (e.target.value) {
                    elements.addCompany.value = '';
                    elements.addDepartment.value = '';
                    elements.addCompany.disabled = true;
                    elements.addDepartment.disabled = true;
                } else {
                    elements.addCompany.disabled = false;
                    elements.addDepartment.disabled = false;
                }
            });

            // --- Filter Listeners ---
            elements.filterGender.addEventListener('change', renderFilteredParticipants);
            elements.filterCompany.addEventListener('change', renderFilteredParticipants);
            elements.filterDepartment.addEventListener('change', renderFilteredParticipants);
            elements.filterCommunity.addEventListener('change', renderFilteredParticipants);

            elements.addForm.addEventListener('submit', async (e) => {
                e.preventDefault();
                const { name, company, department, community, gender, 'start-weight': startWeight, 'weight-key': weightKey } = e.target.elements;

                // --- Validation ---
                if (!name.value || !gender.value || !startWeight.value) {
                    showNotification('Please fill Name, Gender, and Start Weight.', 'error');
                    return;
                }
                if (!company.value && !community.value) {
                    showNotification('Please select a Company or a Community.', 'error');
                    return;
                }
                 if (company.value && !department.value) {
                    showNotification('Please select a Department for the chosen Company.', 'error');
                    return;
                }

                try {
                    let participantData = { 
                        name: name.value, 
                        company: company.value, 
                        department: department.value,
                        community: community.value,
                        gender: gender.value, 
                        startWeight: parseFloat(startWeight.value), 
                        finalWeight: null, 
                        isWeightVisible: true, 
                        createdAt: new Date(), 
                        finalWeightUpdatedAt: null, 
                        weightKey: null 
                    };

                    if (weightKey.value) {
                        participantData.weightKey = await hashString(weightKey.value);
                        participantData.isWeightVisible = false;
                    }
                    const collectionPath = `/artifacts/${appId}/public/data/participants`;
                    await addDoc(collection(db, collectionPath), participantData);
                    showNotification('Participant added successfully!', 'success');
                    elements.addForm.reset();
                    // Manually enable fields after reset
                    elements.addCompany.disabled = false;
                    elements.addDepartment.disabled = false;
                    elements.addCommunity.disabled = false;

                } catch (error) { 
                    showNotification('An error occurred while adding participant.', 'error'); 
                    console.error("Error adding document: ", error); 
                }
            });

            elements.participantList.addEventListener('click', async (e) => {
                const target = e.target.closest('button');
                if (!target) return;
                const card = target.closest('[data-id]');
                if (!card) return;
                const id = card.getAttribute('data-id');
                const collectionPath = `/artifacts/${appId}/public/data/participants`;
                const docRef = doc(db, collectionPath, id);

                if (target.classList.contains('delete-btn')) {
                    showModal(elements.deleteModal.el);
                    deleteCallback = async () => {
                        try {
                            await deleteDoc(docRef);
                            showNotification('Participant deleted successfully.', 'success');
                        } catch (error) { showNotification('An error occurred.', 'error'); }
                    };
                }
                
                if (target.classList.contains('update-btn')) {
                    const finalWeight = parseFloat(card.querySelector('.final-weight-input').value);
                    if (isNaN(finalWeight) || finalWeight <= 0) { showNotification('Please enter a valid number.', 'error'); return; }
                    try {
                        await updateDoc(docRef, { finalWeight, finalWeightUpdatedAt: new Date() });
                        showNotification('Final weight saved successfully!', 'success');
                    } catch (error) { showNotification('An error occurred.', 'error'); }
                }

                if (target.classList.contains('unlock-btn')) {
                    const keyInput = card.querySelector('.unlock-key-input');
                    if (!keyInput.value) { showNotification('Incorrect key entered.', 'error'); return; }
                    const participantDoc = allParticipants.find(p => p.id === id);
                    const storedHash = participantDoc.data().weightKey;
                    const enteredHash = await hashString(keyInput.value);
                    if (enteredHash === storedHash) {
                        await updateDoc(docRef, { isWeightVisible: true });
                        showNotification('Key unlocked successfully!', 'success');
                    } else { showNotification('Incorrect key entered.', 'error'); }
                }
            });
            
            elements.ai.toggleBtn.addEventListener('click', () => elements.ai.modal.classList.add('show'));
            elements.ai.closeBtn.addEventListener('click', () => elements.ai.modal.classList.remove('show'));
            elements.ai.form.addEventListener('submit', async (e) => {
                e.preventDefault();
                const prompt = elements.ai.promptInput.value.trim();
                if (!prompt) return;
                
                if(elements.ai.responseArea.querySelector('p')?.textContent === "Hello! What healthy insights can I get for you today?"){
                    elements.ai.responseArea.innerHTML = '';
                }

                elements.ai.responseArea.innerHTML += `<div class="text-right"><p class="bg-blue-500 inline-block rounded-lg px-3 py-2">${prompt}</p></div>`;
                elements.ai.responseArea.innerHTML += `<div id="thinking" class="text-left"><p class="bg-gray-600 inline-block rounded-lg px-3 py-2">AI is thinking...</p></div>`;
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
                        elements.ai.responseArea.innerHTML += `<div class="text-left"><p class="bg-red-600 inline-block rounded-lg px-3 py-2">Sorry, an error occurred while contacting the AI.</p></div>`;
                    }
                } catch(error) {
                    document.getElementById('thinking')?.remove();
                    elements.ai.responseArea.innerHTML += `<div class="text-left"><p class="bg-red-600 inline-block rounded-lg px-3 py-2">Sorry, cannot connect to the AI service right now.</p></div>`;
                }
                elements.ai.responseArea.scrollTop = elements.ai.responseArea.scrollHeight;
            });

            elements.mobileTabNav.addEventListener('click', (e) => {
                const button = e.target.closest('.mobile-tab-button');
                if (!button) return;

                elements.mobileTabNav.querySelectorAll('.mobile-tab-button').forEach(btn => btn.classList.remove('active'));
                button.classList.add('active');

                const tab = button.dataset.tab;
                if (tab === 'list') {
                    elements.slider.classList.add('slide-to-list');
                } else {
                    elements.slider.classList.remove('slide-to-list');
                }
            });
        }
        
        // --- FIRESTORE & AUTH LOGIC ---
        function setupFirestoreListener() {
            if (unsubscribeFromParticipants) {
                unsubscribeFromParticipants();
            }
            const collectionPath = `/artifacts/${appId}/public/data/participants`;
            unsubscribeFromParticipants = onSnapshot(collection(db, collectionPath), (snapshot) => {
                allParticipants = snapshot.docs;
                renderFilteredParticipants();
                checkAndHandleWinnerState();
            }, (error) => {
                console.error("Firestore listener error:", error);
                showNotification("Error fetching data from server.", "error");
            });
        }

        onAuthStateChanged(auth, async (user) => {
            if (user) {
                // User is authenticated, set up the data listener.
                setupFirestoreListener();
            } else {
                // User is not authenticated. Clean up and attempt to sign in.
                if (unsubscribeFromParticipants) {
                    unsubscribeFromParticipants();
                    unsubscribeFromParticipants = null;
                }
                allParticipants = [];
                renderFilteredParticipants(); 

                try {
                    if (initialAuthToken) {
                        await signInWithCustomToken(auth, initialAuthToken);
                    } else {
                        await signInAnonymously(auth);
                    }
                } catch (error) { 
                    console.error("Authentication failed:", error);
                    showNotification("Authentication failed. Please refresh.", "error");
                }
            }
        });

        // Initialize the app by attaching UI listeners
        attachUIListeners();
        startChallengeCountdown();

    </script>
</body>
</html>
