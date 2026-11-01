<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Kemer Agent Dashboard</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        darkBg: '#070b14',
                        cardBg: '#182234',
                        cardBorder: '#2a374a',
                        brandYellow: '#facc15',
                        brandYellowDark: '#eab308',
                        brandGreen: '#22c55e',
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        html, body {
            height: 100%;
            margin: 0;
            padding: 0;
            overflow: hidden;
            background-color: #070b14;
            color: #f8fafc;
            font-family: 'Inter', sans-serif;
            -webkit-tap-highlight-color: transparent;
            touch-action: manipulation;
        }
        
        .yellow-glow {
            border-color: #facc15;
            box-shadow: 0 0 12px rgba(250, 204, 21, 0.25);
        }
        .green-glow {
            box-shadow: 0 0 12px rgba(34, 197, 94, 0.25);
        }
    </style>
</head>
<body class="w-full h-full flex flex-col items-center justify-center p-2 text-slate-200 select-none">

    <!-- Container scaling directly to screen -->
    <div class="w-full max-w-md h-full max-h-[850px] bg-[#0f172a] rounded-[24px] border border-slate-800/80 shadow-2xl overflow-hidden flex flex-col justify-between">
        
        <!-- Header Bar -->
        <div class="px-4 pt-3 pb-2 flex items-center justify-between border-b border-slate-800/50">
            <!-- Agent Badge -->
            <div class="flex items-center gap-2 px-3 py-1 rounded-full bg-[#182234] border border-slate-700/60 shadow-sm">
                <span id="agentDot" class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                <span class="text-xs font-semibold text-emerald-400 tracking-wide">Agent #01</span>
            </div>
            
            <!-- Time Indicator -->
            <div class="text-xs font-semibold tracking-wider text-slate-400">
                EAT <span id="clockDisplay">14:41</span>
            </div>
        </div>

        <!-- Main Content -->
        <div class="px-3.5 py-2.5 space-y-2.5 flex-1 flex flex-col justify-between">

            <!-- SECTION 1: Status Card -->
            <div class="bg-[#182234] rounded-xl p-3 border border-slate-800/70 relative shadow-lg">
                <!-- Header Title -->
                <div class="flex items-center justify-between mb-2">
                    <div class="flex items-center gap-2">
                        <span id="statusIndicatorBar" class="w-1.5 h-3.5 bg-emerald-500 rounded-full"></span>
                        <h2 class="text-xs font-semibold text-slate-200">Your status</h2>
                    </div>
                    <span class="text-[10px] text-slate-400 font-normal">tap a duration to go online</span>
                </div>

                <!-- Main Status Banner -->
                <div id="statusBanner" class="text-center py-3 rounded-lg bg-[#0f172a]/90 border border-slate-800/80 mb-2.5 transition-all duration-300">
                    <div class="flex items-center justify-center gap-1.5 mb-0.5">
                        <span id="statusPulseDot" class="w-1.5 h-1.5 rounded-full bg-slate-500"></span>
                        <span id="statusSubHeader" class="text-[10px] uppercase tracking-wider font-bold text-slate-400">YOU ARE OFFLINE</span>
                    </div>
                    <h1 id="statusText" class="text-xl font-bold text-white mb-0.5">Offline</h1>
                    <p id="statusSubtitle" class="text-[11px] text-slate-400">pick a duration below to come back</p>
                    <div id="timerDisplay" class="hidden mt-1 text-base font-mono font-bold text-emerald-400">00:00:00</div>
                </div>

                <!-- Duration Buttons -->
                <div class="grid grid-cols-5 gap-1.5">
                    <button onclick="setDuration(15)" class="duration-btn relative flex flex-col items-center justify-center py-2 bg-[#0f172a]/90 border border-slate-800 hover:border-slate-600 rounded-lg transition duration-150 active:scale-95">
                        <span class="text-xs font-bold text-slate-200">15</span>
                        <span class="text-[8px] text-slate-400 font-medium tracking-wider">MIN</span>
                    </button>
                    
                    <button onclick="setDuration(30)" class="duration-btn relative flex flex-col items-center justify-center py-2 bg-[#0f172a]/90 border border-slate-800 hover:border-slate-600 rounded-lg transition duration-150 active:scale-95">
                        <span class="text-xs font-bold text-slate-200">30</span>
                        <span class="text-[8px] text-slate-400 font-medium tracking-wider">MIN</span>
                    </button>

                    <button onclick="setDuration(45)" class="duration-btn relative flex flex-col items-center justify-center py-2 bg-[#0f172a]/90 border border-slate-800 hover:border-slate-600 rounded-lg transition duration-150 active:scale-95">
                        <span class="text-xs font-bold text-slate-200">45</span>
                        <span class="text-[8px] text-slate-400 font-medium tracking-wider">MIN</span>
                    </button>

                    <button onclick="setDuration(60)" class="duration-btn relative flex flex-col items-center justify-center py-2 bg-[#0f172a]/90 border border-slate-800 hover:border-slate-600 rounded-lg transition duration-150 active:scale-95">
                        <span class="text-xs font-bold text-slate-200">60</span>
                        <span class="text-[8px] text-slate-400 font-medium tracking-wider">MIN</span>
                    </button>

                    <button id="btn120" onclick="setDuration(120)" class="duration-btn yellow-glow relative flex flex-col items-center justify-center py-2 bg-[#0f172a]/90 border border-yellow-500/80 rounded-lg transition duration-150 active:scale-95">
                        <i class="fa-solid fa-star text-[7px] text-yellow-400 absolute top-1 right-1"></i>
                        <span class="text-xs font-bold text-slate-200">120</span>
                        <span class="text-[8px] text-slate-400 font-medium tracking-wider">MIN</span>
                    </button>
                </div>
            </div>

            <!-- SECTION 2: Withdrawal Settings Card -->
            <div class="bg-[#182234] rounded-xl p-3 border border-slate-800/70 space-y-2 shadow-lg flex-1 flex flex-col justify-between">
                
                <!-- Section Header with Badge -->
                <div class="flex items-center justify-between">
                    <div class="flex items-center gap-2">
                        <span class="w-1.5 h-3.5 bg-yellow-400 rounded-full"></span>
                        <h2 class="text-xs font-semibold text-slate-200">Withdrawal settings</h2>
                    </div>
                    <span id="topLimitBadge" class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-yellow-500/10 text-yellow-400 border border-yellow-500/30">
                        Up to 10,000 ETB
                    </span>
                </div>

                <!-- Toggle Buttons -->
                <div class="grid grid-cols-2 p-0.5 bg-[#0f172a] rounded-lg border border-slate-800/80">
                    <button id="toggleDepositOnly" onclick="setMode('deposit')" class="py-2 text-[11px] font-semibold rounded-md text-slate-400 transition duration-200">
                        Deposit only
                    </button>
                    <button id="toggleDepositWithdraw" onclick="setMode('both')" class="py-2 text-[11px] font-bold rounded-md bg-yellow-400 text-slate-950 shadow-md transition duration-200">
                        Deposit + Withdraw
                    </button>
                </div>

                <!-- Maximum Payout Control -->
                <div class="space-y-1">
                    <label class="text-[9px] font-bold tracking-wider text-slate-400 uppercase">
                        MAXIMUM I CAN PAY OUT RIGHT NOW
                    </label>
                    <div class="flex items-center gap-2">
                        <button onclick="adjustAmount(-500)" class="w-9 h-9 flex items-center justify-center bg-yellow-500/10 hover:bg-yellow-500/20 text-yellow-400 font-bold text-lg rounded-lg border border-yellow-500/30 transition active:scale-95">
                            -
                        </button>
                        
                        <div class="flex-1 h-9 bg-[#0f172a] border border-yellow-500/40 rounded-lg flex items-center justify-center text-yellow-400 font-extrabold text-xs tracking-wide yellow-glow">
                            <span id="payoutDisplay">10,000 ETB</span>
                        </div>

                        <button onclick="adjustAmount(500)" class="w-9 h-9 flex items-center justify-center bg-yellow-500/10 hover:bg-yellow-500/20 text-yellow-400 font-bold text-lg rounded-lg border border-yellow-500/30 transition active:scale-95">
                            +
                        </button>
                    </div>
                </div>

                <!-- Dynamic Helper Text -->
                <p class="text-[9.5px] text-slate-400 leading-tight font-normal">
                    Lower this any time you're running out of cash — players asking for more than this won't see you. Minimum withdrawal (<span class="text-slate-300 font-medium">200 ETB</span>) and maximum (<span class="text-slate-300 font-medium">100,000 ETB</span>) are set by admin.
                </p>

                <!-- SECTION 3: Withdrawal ID Section -->
                <div class="pt-1.5 border-t border-slate-800/60 space-y-1">
                    <div class="flex items-center justify-between text-[10px]">
                        <span class="text-slate-400 font-medium">MY WITHDRAWAL ID</span>
                        <span class="text-yellow-400 font-medium">· set by admin</span>
                    </div>

                    <div class="relative flex items-center">
                        <input type="text" readonly value="40223" class="w-full h-8 bg-[#0f172a] border border-slate-800 rounded-lg px-3 text-slate-300 font-medium text-xs focus:outline-none cursor-not-allowed">
                        <div class="absolute right-2 flex items-center gap-1 text-[8.5px] font-bold text-slate-400 bg-slate-800/80 px-1.5 py-0.5 rounded border border-slate-700/80">
                            <i class="fa-solid fa-lock text-[8px] text-slate-400"></i>
                            <span>READ ONLY</span>
                        </div>
                    </div>

                    <p class="text-[9px] text-slate-400 leading-tight">
                        Players' auto-message includes this ID so they can start the withdrawal immediately.
                    </p>
                </div>

                <!-- Save Settings Action Button -->
                <div class="pt-1">
                    <button id="saveBtn" onclick="saveSettings()" class="w-full py-2.5 bg-slate-800/90 border border-slate-700/60 rounded-lg text-slate-400 font-bold text-[10px] tracking-wider uppercase hover:bg-slate-700/80 active:scale-[0.99] transition duration-150">
                        Save withdrawal settings
                    </button>
                </div>

            </div>

        </div>

        <!-- Footer Bar Simulation -->
        <div class="bg-[#0b1120] border-t border-slate-800/70 py-2 px-5 flex items-center justify-between text-slate-400 text-xs">
            <div class="flex items-center gap-1.5 text-slate-300 font-medium text-[11px]">
                <i class="fa-solid fa-globe text-slate-400 text-xs"></i>
                <span>kemeragent.com</span>
            </div>
            <div class="flex items-center gap-4 text-slate-400">
                <i class="fa-solid fa-arrow-left cursor-pointer hover:text-white"></i>
                <i class="fa-solid fa-arrow-right cursor-pointer hover:text-white"></i>
                <i class="fa-solid fa-rotate-right cursor-pointer hover:text-white"></i>
            </div>
        </div>

    </div>

    <!-- Custom Modal/Toast Alert Container -->
    <div id="toast" class="fixed bottom-6 left-1/2 transform -translate-x-1/2 bg-slate-900 text-white px-4 py-2 rounded-xl border border-yellow-500/50 shadow-2xl flex items-center gap-2 transition-all duration-300 opacity-0 pointer-events-none z-50">
        <i id="toastIcon" class="fa-solid fa-circle-check text-yellow-400 text-sm"></i>
        <span id="toastMessage" class="text-xs font-semibold">Settings saved successfully!</span>
    </div>

    <script>
        let currentPayout = 10000;
        const minPayout = 200;
        const maxPayout = 100000;
        let isOnline = false;
        let timerInterval = null;
        let remainingSeconds = 0;
        let currentMode = 'both';

        function updateClock() {
            const now = new Date();
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            document.getElementById('clockDisplay').textContent = `${hours}:${minutes}`;
        }
        setInterval(updateClock, 1000);
        updateClock();

        function adjustAmount(delta) {
            let nextVal = currentPayout + delta;
            if (nextVal < minPayout) nextVal = minPayout;
            if (nextVal > maxPayout) nextVal = maxPayout;
            currentPayout = nextVal;
            
            const formatted = currentPayout.toLocaleString() + ' ETB';
            document.getElementById('payoutDisplay').textContent = formatted;
            document.getElementById('topLimitBadge').textContent = `Up to ${formatted}`;

            enableSaveButton();
        }

        function setMode(mode) {
            currentMode = mode;
            const depBtn = document.getElementById('toggleDepositOnly');
            const bothBtn = document.getElementById('toggleDepositWithdraw');

            if (mode === 'deposit') {
                depBtn.className = "py-2 text-[11px] font-bold rounded-md bg-yellow-400 text-slate-950 shadow-md transition duration-200";
                bothBtn.className = "py-2 text-[11px] font-semibold rounded-md text-slate-400 transition duration-200";
            } else {
                bothBtn.className = "py-2 text-[11px] font-bold rounded-md bg-yellow-400 text-slate-950 shadow-md transition duration-200";
                depBtn.className = "py-2 text-[11px] font-semibold rounded-md text-slate-400 transition duration-200";
            }
            enableSaveButton();
        }

        function enableSaveButton() {
            const saveBtn = document.getElementById('saveBtn');
            saveBtn.className = "w-full py-2.5 bg-yellow-400 hover:bg-yellow-300 border border-yellow-500 rounded-lg text-slate-950 font-extrabold text-[10px] tracking-wider uppercase shadow-lg transition duration-150 active:scale-[0.99]";
        }

        function saveSettings() {
            const saveBtn = document.getElementById('saveBtn');
            saveBtn.className = "w-full py-2.5 bg-slate-800/90 border border-slate-700/60 rounded-lg text-slate-400 font-bold text-[10px] tracking-wider uppercase hover:bg-slate-700/80 active:scale-[0.99] transition duration-150";
            showToast("Withdrawal settings updated!", "fa-circle-check", "#facc15");
        }

        function setDuration(minutes) {
            clearInterval(timerInterval);
            isOnline = true;
            remainingSeconds = minutes * 60;

            document.getElementById('statusSubHeader').textContent = "YOU ARE ONLINE";
            document.getElementById('statusSubHeader').className = "text-[10px] uppercase tracking-wider font-bold text-emerald-400";
            
            document.getElementById('statusText').textContent = "Online";
            document.getElementById('statusSubtitle').textContent = `Agent active for ${minutes} minutes`;
            
            document.getElementById('statusPulseDot').className = "w-1.5 h-1.5 rounded-full bg-emerald-500 animate-ping";
            document.getElementById('statusIndicatorBar').className = "w-1.5 h-3.5 bg-emerald-400 rounded-full";
            
            const banner = document.getElementById('statusBanner');
            banner.className = "text-center py-3 rounded-lg bg-emerald-950/20 border border-emerald-500/40 mb-2.5 transition-all duration-300 green-glow";

            const timerDisp = document.getElementById('timerDisplay');
            timerDisp.classList.remove('hidden');

            updateTimerText();
            timerInterval = setInterval(() => {
                remainingSeconds--;
                if (remainingSeconds <= 0) {
                    clearInterval(timerInterval);
                    setOffline();
                } else {
                    updateTimerText();
                }
            }, 1000);

            showToast(`Status updated: Online for ${minutes} mins`, "fa-bolt", "#22c55e");
        }

        function updateTimerText() {
            const hrs = Math.floor(remainingSeconds / 3600);
            const mins = Math.floor((remainingSeconds % 3600) / 60);
            const secs = remainingSeconds % 60;

            const formatted = 
                `${String(hrs).padStart(2, '0')}:${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
            document.getElementById('timerDisplay').textContent = formatted;
        }

        function setOffline() {
            isOnline = false;
            document.getElementById('statusSubHeader').textContent = "YOU ARE OFFLINE";
            document.getElementById('statusSubHeader').className = "text-[10px] uppercase tracking-wider font-bold text-slate-400";
            
            document.getElementById('statusText').textContent = "Offline";
            document.getElementById('statusSubtitle').textContent = "pick a duration below to come back";
            
            document.getElementById('statusPulseDot').className = "w-1.5 h-1.5 rounded-full bg-slate-500";
            document.getElementById('statusIndicatorBar').className = "w-1.5 h-3.5 bg-slate-500 rounded-full";

            const banner = document.getElementById('statusBanner');
            banner.className = "text-center py-3 rounded-lg bg-[#0f172a]/90 border border-slate-800/80 mb-2.5 transition-all duration-300";

            document.getElementById('timerDisplay').classList.add('hidden');
        }

        function showToast(msg, iconClass = "fa-circle-check", color = "#facc15") {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toastMessage');
            const toastIcon = document.getElementById('toastIcon');

            toastMsg.textContent = msg;
            toastIcon.className = `fa-solid ${iconClass}`;
            toastIcon.style.color = color;

            toast.classList.remove('opacity-0', 'pointer-events-none');
            toast.classList.add('opacity-100');

            setTimeout(() => {
                toast.classList.remove('opacity-100');
                toast.classList.add('opacity-0', 'pointer-events-none');
            }, 2500);
        }
    </script>
</body>
</html>
