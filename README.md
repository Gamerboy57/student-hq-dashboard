<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HQ // STUDENT DASHBOARD</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&family=IBM+Plex+Mono:wght@300;400;600&family=Rajdhani:wght@500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-dark: #050b14;
            --bg-card: #0a111f;
            --neon-blue: #00f2ff;
            --neon-purple: #bc13fe;
            --neon-red: #ff003c;
            --neon-green: #39ff14;
            --neon-yellow: #fefe33;
            --text-main: #e0e6ed;
            --grid-color: rgba(0, 242, 255, 0.05);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            scroll-behavior: smooth;
        }

        body {
            background-color: var(--bg-dark);
            background-image: 
                linear-gradient(var(--grid-color) 1px, transparent 1px),
                linear-gradient(90deg, var(--grid-color) 1px, transparent 1px);
            background-size: 30px 30px;
            color: var(--text-main);
            font-family: 'IBM Plex Mono', monospace;
            line-height: 1.6;
            overflow-x: hidden;
        }

        h1, h2, h3, .nav-link {
            font-family: 'Orbitron', sans-serif;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        /* --- NAVIGATION --- */
        nav {
            position: fixed;
            top: 0;
            width: 100%;
            background: rgba(5, 11, 20, 0.95);
            border-bottom: 2px solid var(--neon-blue);
            z-index: 1000;
            display: flex;
            justify-content: center;
            padding: 15px 0;
            backdrop-filter: blur(10px);
        }

        .nav-container {
            display: flex;
            gap: 30px;
        }

        .nav-link {
            text-decoration: none;
            color: var(--text-main);
            font-size: 0.9rem;
            position: relative;
            padding: 5px 10px;
            transition: 0.3s;
        }

        .nav-link:hover {
            color: var(--neon-blue);
            text-shadow: 0 0 8px var(--neon-blue);
        }

        /* --- LAYOUT --- */
        .container {
            max-width: 1100px;
            margin: 100px auto;
            padding: 20px;
        }

        section {
            margin-bottom: 100px;
            padding-top: 40px;
        }

        .section-title {
            font-size: 2rem;
            margin-bottom: 30px;
            color: var(--neon-blue);
            border-left: 5px solid var(--neon-blue);
            padding-left: 15px;
            display: flex;
            align-items: center;
        }

        /* --- SCHEDULE TABS --- */
        .tabs-header {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .tab-btn {
            background: var(--bg-card);
            border: 1px solid #1a2a40;
            color: #8892b0;
            padding: 10px 20px;
            cursor: pointer;
            font-family: 'Rajdhani', sans-serif;
            font-weight: bold;
            clip-path: polygon(10% 0, 100% 0, 100% 70%, 90% 100%, 0 100%, 0 30%);
            transition: 0.3s;
        }

        .tab-btn.active {
            background: var(--neon-blue);
            color: var(--bg-dark);
            border-color: var(--neon-blue);
            box-shadow: 0 0 15px rgba(0, 242, 255, 0.4);
        }

        .status-dot {
            height: 8px;
            width: 8px;
            background-color: var(--neon-green);
            border-radius: 50%;
            display: inline-block;
            margin-right: 8px;
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.5); opacity: 0.5; }
            100% { transform: scale(1); opacity: 1; }
        }

        .schedule-grid {
            display: none;
            animation: fadeIn 0.5s ease-in;
        }

        .schedule-grid.active {
            display: block;
        }

        .event-card {
            background: var(--bg-card);
            margin-bottom: 10px;
            padding: 15px 20px;
            display: flex;
            align-items: center;
            border-left: 4px solid #333;
            transition: 0.3s;
        }

        /* Category Colors */
        .cat-workout { border-color: var(--neon-purple); }
        .cat-school { border-color: var(--neon-blue); }
        .cat-study { border-color: var(--neon-yellow); }
        .cat-lang { border-color: var(--neon-green); }
        .cat-read { border-color: #ffffff; }
        .cat-game { border-color: var(--neon-red); }
        .cat-free { border-color: #555; }

        /* --- SUBJECT GRID --- */
        .subject-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
            gap: 15px;
        }

        .subject-card {
            background: var(--bg-card);
            border: 1px solid #1a2a40;
            padding: 20px;
            text-align: center;
            clip-path: polygon(0 0, 85% 0, 100% 25%, 100% 100%, 15% 100%, 0 75%);
        }

        /* --- TIMER --- */
        .timer-panel {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            background: var(--bg-card);
            padding: 30px;
            border: 1px solid #1a2a40;
        }

        #countdown {
            font-size: 4rem;
            font-family: 'Orbitron', sans-serif;
            color: var(--neon-blue);
            text-align: center;
            margin: 20px 0;
            text-shadow: 0 0 20px rgba(0, 242, 255, 0.5);
        }

        .timer-controls {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 20px;
        }

        .btn-start {
            background: none;
            border: 2px solid var(--neon-green);
            color: var(--neon-green);
            padding: 10px 30px;
            cursor: pointer;
            font-family: 'Orbitron', sans-serif;
            transition: 0.3s;
        }

        .yt-module {
            margin-top: 20px;
            padding: 15px;
            background: rgba(0, 0, 0, 0.4);
            border: 1px dashed var(--neon-blue);
        }

        .yt-input {
            width: 100%;
            background: #050b14;
            border: 1px solid #1a2a40;
            color: var(--neon-blue);
            padding: 8px;
            font-family: 'IBM Plex Mono';
            font-size: 0.7rem;
            margin-bottom: 10px;
            outline: none;
        }

        .step {
            margin-bottom: 15px;
            padding-left: 15px;
            border-left: 2px solid #333;
            font-size: 0.85rem;
        }

        .step.active-step {
            border-color: var(--neon-yellow);
            color: var(--neon-yellow);
        }

        /* --- TOURNAMENT --- */
        .briefing-card {
            background: linear-gradient(135deg, #0a111f 0%, #1a0505 100%);
            border: 1px solid var(--neon-red);
            padding: 30px;
        }

        #t-timer {
            font-size: 2rem;
            color: var(--neon-red);
            font-family: 'Orbitron', sans-serif;
        }

        @media (max-width: 768px) {
            .timer-panel { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

<nav>
    <div class="nav-container">
        <a href="#schedule" class="nav-link">Schedule</a>
        <a href="#subjects" class="nav-link">Subjects</a>
        <a href="#timer" class="nav-link">Study Timer</a>
        <a href="#tournament" class="nav-link">Tournament</a>
    </div>
</nav>

<div class="container">

    <section id="schedule">
        <h2 class="section-title"><span class="status-dot"></span> Weekly Deployment</h2>
        <div class="tabs-header">
            <button class="tab-btn active" onclick="openDay(event, 'Mon')">MON</button>
            <button class="tab-btn" onclick="openDay(event, 'Tue')">TUE</button>
            <button class="tab-btn" onclick="openDay(event, 'Wed')">WED</button>
            <button class="tab-btn" onclick="openDay(event, 'Thu')">THU</button>
            <button class="tab-btn" onclick="openDay(event, 'Fri')">FRI</button>
            <button class="tab-btn" onclick="openDay(event, 'Sat')">SAT</button>
            <button class="tab-btn" onclick="openDay(event, 'Sun')">SUN</button>
        </div>

        <div id="Mon" class="schedule-grid active">
            <div class="event-card cat-workout"><span style="min-width:120px; color:var(--neon-blue)">06:00 - 07:30</span><span>Push/Pull Day</span></div>
            <div class="event-card cat-school"><span style="min-width:120px; color:var(--neon-blue)">08:00 - 13:15</span><span>School Session</span></div>
            <div class="event-card cat-study"><span style="min-width:120px; color:var(--neon-blue)">14:00 - 16:00</span><span>Math Repetition</span></div>
        </div>
        </section>

    <section id="subjects">
        <h2 class="section-title">Exam Subject Matrix</h2>
        <div class="subject-container">
            <div class="subject-card"><h4>Math</h4><p style="font-size:0.7rem; color:#8892b0">Mon, Thu</p></div>
            <div class="subject-card"><h4>Physics</h4><p style="font-size:0.7rem; color:#8892b0">Mon, Wed</p></div>
            <div class="subject-card"><h4>Biology</h4><p style="font-size:0.7rem; color:#8892b0">Tue, Thu</p></div>
            <div class="subject-card"><h4>MLBB Meta</h4><p style="font-size:0.7rem; color:#8892b0">Daily</p></div>
        </div>
    </section>

    <section id="timer">
        <h2 class="section-title">Deep Work Protocol</h2>
        <div class="timer-panel">
            <div>
                <div id="yt-player" style="display: none;"></div>
                <div id="countdown">45:00</div>
                
                <div class="timer-controls">
                    <button class="btn-start" id="main-trigger" onclick="toggleTimer()">ACTIVATE</button>
                    <button class="btn-start" style="border-color:var(--neon-red); color:var(--neon-red)" onclick="resetTimer()">RESET</button>
                </div>

                <div class="yt-module">
                    <p style="font-size: 0.6rem; color: var(--neon-blue); margin-bottom: 8px; font-family: 'Orbitron';">Audio Satellite Link</p>
                    <input type="text" id="yt-url" class="yt-input" placeholder="Paste YouTube Link Here...">
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <span style="font-size: 0.6rem; color: var(--neon-blue);">VOL</span>
                        <input type="range" id="volume-slider" min="0" max="100" value="50" style="flex-grow:1; accent-color:var(--neon-blue);" oninput="updateVolume(this.value)">
                    </div>
                </div>
            </div>

            <div class="guide-steps">
                <div class="step" id="step1"><strong>00-05m: Focus</strong><br>Objective setting.</div>
                <div class="step" id="step2"><strong>05-20m: Recall</strong><br>Active blurting.</div>
                <div class="step" id="step3"><strong>20-40m: Practice</strong><br>Problem sets.</div>
                <div class="step" id="step4"><strong>40-45m: Lock-in</strong><br>Final summary.</div>
            </div>
        </div>
    </section>

    <section id="tournament">
        <h2 class="section-title">Tournament Intel</h2>
        <div class="briefing-card">
            <p style="font-size: 0.8rem; color: #8892b0; margin-bottom: 10px; text-align: center;">COMMENCING IN:</p>
            <div id="t-timer" style="text-align: center;">00d 00h 00m 00s</div>
        </div>
    </section>

</div>

<script>
    // --- TABS ---
    function openDay(evt, dayName) {
        let i, tabcontent, tablinks;
        tabcontent = document.getElementsByClassName("schedule-grid");
        for (i = 0; i < tabcontent.length; i++) tabcontent[i].style.display = "none";
        tablinks = document.getElementsByClassName("tab-btn");
        for (i = 0; i < tablinks.length; i++) tablinks[i].className = tablinks[i].className.replace(" active", "");
        document.getElementById(dayName).style.display = "block";
        evt.currentTarget.className += " active";
    }

    // --- YOUTUBE API ---
    let player;
    let isRunning = false;
    let timerInterval;
    let timeLeft = 45 * 60;

    const tag = document.createElement('script');
    tag.src = "https://www.youtube.com/iframe_api";
    document.head.appendChild(tag);

    function onYouTubeIframeAPIReady() {
        player = new YT.Player('yt-player', {
            height: '0', width: '0', videoId: '',
            events: { 'onReady': (e) => e.target.setVolume(50) }
        });
    }

    function updateVolume(val) { if (player && player.setVolume) player.setVolume(val); }

    function getYouTubeID(url) {
        const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
        const match = url.match(regExp);
        return (match && match[2].length === 11) ? match[2] : url;
    }

    // --- TIMER & CONTROL ---
    function toggleTimer() {
        const btn = document.getElementById('main-trigger');
        const ytInput = document.getElementById('yt-url').value;

        if (!isRunning) {
            if (ytInput) {
                const vid = getYouTubeID(ytInput);
                player.loadVideoById(vid);
            }
            startTimerLogic();
            btn.innerText = "DEACTIVATE";
            btn.style.borderColor = "var(--neon-yellow)";
            btn.style.color = "var(--neon-yellow)";
            isRunning = true;
        } else {
            clearInterval(timerInterval);
            player.pauseVideo();
            btn.innerText = "ACTIVATE";
            btn.style.borderColor = "var(--neon-green)";
            btn.style.color = "var(--neon-green)";
            isRunning = false;
        }
    }

    function startTimerLogic() {
        clearInterval(timerInterval);
        timerInterval = setInterval(() => {
            if(timeLeft <= 0) {
                clearInterval(timerInterval);
                player.pauseVideo();
                return;
            }
            timeLeft--;
            updateTimerDisplay();
            updateStepHighlight();
        }, 1000);
    }

    function resetTimer() {
        clearInterval(timerInterval);
        timeLeft = 45 * 60;
        isRunning = false;
        if (player) player.stopVideo();
        document.getElementById('main-trigger').innerText = "ACTIVATE";
        updateTimerDisplay();
        document.querySelectorAll('.step').forEach(s => s.classList.remove('active-step'));
    }

    function updateTimerDisplay() {
        const mins = Math.floor(timeLeft / 60);
        const secs = timeLeft % 60;
        document.getElementById('countdown').innerText = `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
    }

    function updateStepHighlight() {
        const mins = (45 * 60 - timeLeft) / 60;
        document.querySelectorAll('.step').forEach(s => s.classList.remove('active-step'));
        if (mins < 5) document.getElementById('step1').classList.add('active-step');
        else if (mins < 20) document.getElementById('step2').classList.add('active-step');
        else if (mins < 40) document.getElementById('step3').classList.add('active-step');
        else document.getElementById('step4').classList.add('active-step');
    }

    // --- TOURNAMENT COUNTDOWN ---
    const target = new Date("April 15, 2026 00:00:00").getTime();
    setInterval(() => {
        const now = new Date().getTime();
        const diff = target - now;
        const d = Math.floor(diff / 86400000);
        const h = Math.floor((diff % 86400000) / 3600000);
        const m = Math.floor((diff % 3600000) / 60000);
        const s = Math.floor((diff % 60000) / 1000);
        document.getElementById('t-timer').innerText = `${d}d ${h}h ${m}m ${s}s`;
    }, 1000);
</script>

</body>
</html>
