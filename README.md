<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>The Day The World Got You — 20 December 2011</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts: Cormorant Garamond (Serif), Plus Jakarta Sans (Modern Sans), Caveat (Handwritten) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Caveat:wght@500;600;700&family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600&family=Plus+Jakarta+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        obsidian: '#09080a',
                        burgundy: {
                            DEFAULT: '#3b0d18',
                            light: '#591122',
                            dark: '#21060c'
                        },
                        gold: {
                            DEFAULT: '#d4af37',
                            light: '#f3e5ab',
                            dim: '#9e7f20'
                        },
                        ivory: '#f5f2eb'
                    },
                    fontFamily: {
                        serif: ['"Cormorant Garamond"', 'Georgia', 'serif'],
                        sans: ['"Plus Jakarta Sans"', 'sans-serif'],
                        hand: ['"Caveat"', 'cursive']
                    }
                }
            }
        }
    </script>

    <style>
        :root {
            --obsidian: #09080a;
            --burgundy: #3b0d18;
            --burgundy-light: #591122;
            --gold: #d4af37;
            --gold-light: #f3e5ab;
            --ivory: #f5f2eb;
        }

        * {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        html, body {
            margin: 0;
            padding: 0;
            background-color: var(--obsidian);
            color: var(--ivory);
            font-family: 'Plus Jakarta Sans', sans-serif;
            overflow-x: hidden;
            scroll-behavior: smooth;
        }

        /* Cinematic Film Grain Overlay */
        .film-grain {
            position: fixed;
            inset: 0;
            pointer-events: none;
            z-index: 9998;
            opacity: 0.045;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
        }

        /* Ambient Particle Canvas */
        #ambient-canvas {
            position: fixed;
            inset: 0;
            pointer-events: none;
            z-index: 1;
        }

        /* Glassmorphic Dark-Burgundy Card */
        .luxury-card {
            background: linear-gradient(145deg, rgba(59, 13, 24, 0.38) 0%, rgba(9, 8, 10, 0.85) 100%);
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            border: 1px solid rgba(212, 175, 55, 0.25);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.75), inset 0 1px 0 rgba(243, 229, 171, 0.12);
        }

        .gold-glow-text {
            text-shadow: 0 0 24px rgba(212, 175, 55, 0.45);
        }

        /* Luxury Interactive Button */
        .btn-gold {
            background: linear-gradient(135deg, rgba(89, 17, 34, 0.85) 0%, rgba(33, 6, 12, 0.95) 100%);
            border: 1px solid rgba(212, 175, 55, 0.55);
            color: var(--gold-light);
            transition: all 0.4s cubic-bezier(0.22, 1, 0.36, 1);
            box-shadow: 0 4px 20px rgba(212, 175, 55, 0.15);
        }
        .btn-gold:hover, .btn-gold:active {
            border-color: var(--gold-light);
            box-shadow: 0 0 28px rgba(212, 175, 55, 0.4);
            transform: translateY(-2px);
        }

        /* Screen Transitions */
        .stage-section {
            min-height: 100dvh;
            width: 100%;
            position: relative;
            z-index: 10;
            transition: opacity 0.9s ease, transform 0.9s ease;
        }
        .hidden-stage {
            display: none !important;
            opacity: 0;
        }
        .fade-in-up {
            animation: fadeInUp 1.1s cubic-bezier(0.22, 1, 0.36, 1) forwards;
        }
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(24px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* ================= 01: OPENING ENVELOPE ================= */
        .envelope-wrapper {
            perspective: 1000px;
            width: 300px;
            height: 200px;
            margin: 0 auto;
            position: relative;
        }
        .envelope-body {
            width: 100%;
            height: 100%;
            background: linear-gradient(160deg, #4b101e 0%, #24060d 100%);
            border: 1px solid rgba(212, 175, 55, 0.4);
            border-radius: 12px;
            position: relative;
            box-shadow: 0 25px 60px rgba(0, 0, 0, 0.85), 0 0 35px rgba(89, 17, 34, 0.45);
            overflow: hidden;
        }
        .envelope-flap {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 115px;
            background: linear-gradient(180deg, #5e1325 0%, #380b16 100%);
            clip-path: polygon(0 0, 50% 85%, 100% 0);
            transform-origin: top center;
            transition: transform 0.9s cubic-bezier(0.4, 0, 0.2, 1);
            z-index: 4;
            border-top: 1px solid rgba(212, 175, 55, 0.5);
        }
        .envelope-wrapper.opened .envelope-flap {
            transform: rotateX(180deg);
            z-index: 1;
        }
        .wax-seal {
            position: absolute;
            top: 72px;
            left: 50%;
            transform: translateX(-50%);
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: radial-gradient(circle at 30% 30%, #f3e5ab, #d4af37 60%, #8a6d17 100%);
            box-shadow: 0 4px 15px rgba(0,0,0,0.6), 0 0 20px rgba(212, 175, 55, 0.5);
            z-index: 5;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #24060d;
            font-family: 'Cormorant Garamond', serif;
            font-weight: 700;
            font-size: 18px;
            transition: opacity 0.5s ease, transform 0.5s ease;
        }
        .envelope-wrapper.opened .wax-seal {
            opacity: 0;
            transform: translateX(-50%) scale(0.6);
            pointer-events: none;
        }
        .envelope-letter-preview {
            position: absolute;
            bottom: 10px;
            left: 16px;
            right: 16px;
            height: 165px;
            background: #f5f2eb;
            color: #1c1618;
            border-radius: 8px;
            padding: 16px;
            z-index: 2;
            transition: transform 0.9s cubic-bezier(0.22, 1, 0.36, 1) 0.35s;
            box-shadow: 0 -4px 20px rgba(0,0,0,0.4);
        }
        .envelope-wrapper.opened .envelope-letter-preview {
            transform: translateY(-75px);
            z-index: 6;
        }

        /* ================= 02: 3D LUXURY BIRTHDAY CAKE ================= */
        .cake-stage {
            position: relative;
            width: 260px;
            height: 230px;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-end;
        }
        .cake-topper {
            font-family: 'Cormorant Garamond', serif;
            font-weight: 700;
            letter-spacing: 0.18em;
            color: var(--gold-light);
            background: rgba(33, 6, 12, 0.9);
            border: 1px solid var(--gold);
            padding: 4px 14px;
            border-radius: 999px;
            font-size: 0.95rem;
            box-shadow: 0 0 20px rgba(212, 175, 55, 0.35);
            margin-bottom: 14px;
            z-index: 5;
        }
        .candles-row {
            display: flex;
            gap: 22px;
            margin-bottom: -4px;
            z-index: 4;
        }
        .candle {
            width: 10px;
            height: 42px;
            background: repeating-linear-gradient(45deg, #f5f2eb, #f5f2eb 5px, #d4af37 5px, #d4af37 10px);
            border-radius: 3px 3px 0 0;
            position: relative;
            box-shadow: 0 2px 6px rgba(0,0,0,0.5);
        }
        .flame {
            position: absolute;
            top: -18px;
            left: 50%;
            transform: translateX(-50%);
            width: 12px;
            height: 18px;
            background: radial-gradient(ellipse at bottom, #fff 10%, #ffd54f 55%, #ff6f00 100%);
            border-radius: 50% 50% 35% 35%;
            box-shadow: 0 0 18px #ffb300, 0 0 35px rgba(255, 179, 0, 0.6);
            animation: flicker 0.18s infinite alternate;
            transition: opacity 0.4s ease, transform 0.4s ease;
        }
        .flame.blown-out {
            opacity: 0;
            transform: translateX(-50%) scale(0.1);
        }
        .smoke {
            position: absolute;
            top: -24px;
            left: 50%;
            width: 6px;
            height: 20px;
            background: rgba(245, 242, 235, 0.45);
            border-radius: 50%;
            filter: blur(3px);
            opacity: 0;
            pointer-events: none;
        }
        .smoke.rising {
            animation: smokeRise 1.8s ease-out forwards;
        }
        @keyframes flicker {
            0% { transform: translateX(-50%) scale(1) rotate(-2deg); }
            100% { transform: translateX(-50%) scale(1.08) rotate(2deg); }
        }
        @keyframes smokeRise {
            0% { opacity: 0.8; transform: translate(-50%, 0) scale(1); }
            100% { opacity: 0; transform: translate(-30%, -35px) scale(2.4); }
        }
        .cake-tier-top {
            width: 150px;
            height: 48px;
            background: linear-gradient(90deg, #2d0912 0%, #5c1325 45%, #2d0912 100%);
            border-radius: 14px 14px 6px 6px;
            border-top: 3px solid #f3e5ab;
            border-bottom: 2px solid #d4af37;
            position: relative;
            box-shadow: 0 8px 20px rgba(0,0,0,0.6);
        }
        .cake-tier-bottom {
            width: 215px;
            height: 62px;
            background: linear-gradient(90deg, #21060c 0%, #4a0e1d 50%, #21060c 100%);
            border-radius: 14px 14px 10px 10px;
            border-top: 3px solid #d4af37;
            border-bottom: 3px solid #f3e5ab;
            position: relative;
            box-shadow: 0 15px 30px rgba(0,0,0,0.85);
            display: flex;
            align-items: center;
            justify-content: space-around;
            padding: 0 16px;
        }
        .cake-pearl {
            width: 7px;
            height: 7px;
            border-radius: 50%;
            background: radial-gradient(circle at 30% 30%, #fff, #d4af37);
        }
        .cake-plate {
            width: 250px;
            height: 12px;
            background: linear-gradient(90deg, #8a6d17, #f3e5ab, #8a6d17);
            border-radius: 50%;
            margin-top: -2px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.9);
        }

        /* ================= 04: KEN BURNS ZOOM FOR TIMELINE ================= */
        .ken-burns-img {
            animation: kenBurns 14s ease-in-out infinite alternate;
        }
        @keyframes kenBurns {
            0% { transform: scale(1.0) translate(0, 0); }
            100% { transform: scale(1.14) translate(-1.5%, -1.5%); }
        }

        /* ================= 07 & 08: HEARTBEAT PULSE ================= */
        .heartbeat-pulse {
            animation: heartThump 1s infinite;
        }
        @keyframes heartThump {
            0% { transform: scale(1); }
            14% { transform: scale(1.08); }
            28% { transform: scale(1); }
            42% { transform: scale(1.05); }
            70% { transform: scale(1); }
        }

        /* ================= 11: POLAROID GALLERY ================= */
        .polaroid-card {
            background: #f5f2eb;
            color: #1a1517;
            padding: 12px 12px 26px 12px;
            border-radius: 6px;
            box-shadow: 0 14px 35px rgba(0,0,0,0.75);
            transition: transform 0.35s ease, box-shadow 0.35s ease;
        }
        .polaroid-card:hover {
            transform: translateY(-6px) rotate(0deg) !important;
            box-shadow: 0 20px 45px rgba(212, 175, 55, 0.25);
        }

        /* ================= 13: GIFT BOX ================= */
        .gift-lid {
            transition: transform 0.7s cubic-bezier(0.34, 1.56, 0.64, 1);
            transform-origin: left bottom;
        }
        .gift-opened .gift-lid {
            transform: rotate(-28deg) translateY(-28px) translateX(-10px);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 5px;
        }
        ::-webkit-scrollbar-track {
            background: #09080a;
        }
        ::-webkit-scrollbar-thumb {
            background: #591122;
            border-radius: 10px;
        }
    </style>
</head>
<body class="bg-obsidian text-ivory selection:bg-burgundy-light selection:text-gold-light">

    <!-- Subtle Film Grain Overlay -->
    <div class="film-grain"></div>

    <!-- Ambient Gold Dust & Starfield Canvas -->
    <canvas id="ambient-canvas"></canvas>

    <!-- Floating Music Toggle Button -->
    <button id="music-toggle" aria-label="Toggle Music" class="fixed top-4 right-4 z-50 flex items-center gap-2 px-3.5 py-2 rounded-full luxury-card text-gold-light text-xs tracking-widest uppercase hover:border-gold transition-all">
        <span id="music-icon" class="text-base">🔇</span>
        <span id="music-label" class="hidden sm:inline font-medium">Sound Off</span>
    </button>

    <!-- =====================================================================
         STAGE 01: OPENING / SECRET NOTE
    ====================================================================== -->
    <section id="stage-01" class="stage-section flex flex-col items-center justify-center px-6 text-center">
        <div class="max-w-md w-full fade-in-up">
            <p class="text-xs uppercase tracking-[0.28em] text-gold/80 mb-8">20 • 12 • 2011</p>

            <!-- Interactive Envelope -->
            <div id="opening-envelope" class="envelope-wrapper mb-10 cursor-pointer" onclick="handleOpenEnvelope()">
                <div class="envelope-body">
                    <div class="envelope-letter-preview flex flex-col justify-center items-center text-center">
                        <p class="font-serif italic text-burgundy text-base leading-snug">
                            “This isn’t just a birthday wish.<br>I wanted to take you back to the day your story began…”
                        </p>
                    </div>
                </div>
                <div class="envelope-flap"></div>
                <div class="wax-seal">♡</div>
            </div>

            <!-- Initial Prompt -->
            <div id="opening-initial-text" class="space-y-6 transition-opacity duration-500">
                <h1 class="font-serif text-2xl sm:text-3xl text-ivory leading-relaxed font-normal">
                    For the girl whose birthday is today…<br>
                    <span class="italic text-gold-light">I made something for you.</span>
                </h1>
                <button onclick="handleOpenEnvelope()" class="btn-gold px-8 py-3.5 rounded-full text-sm tracking-[0.18em] uppercase font-medium">
                    Open it ♡
                </button>
            </div>

            <!-- Post-Open Continue Prompt -->
            <div id="opening-continue-text" class="hidden space-y-6 mt-6 fade-in-up">
                <p class="font-serif italic text-xl text-gold-light/95 leading-relaxed">
                    “Before you became my favorite person, you were just someone the world was waiting to meet.”
                </p>
                <button onclick="goToStage('stage-02', 'piano')" class="btn-gold px-8 py-3.5 rounded-full text-sm tracking-[0.18em] uppercase font-medium">
                    Continue →
                </button>
            </div>
        </div>
    </section>

    <!-- =====================================================================
         STAGE 02: BIRTHDAY CAKE
    ====================================================================== -->
    <section id="stage-02" class="stage-section hidden-stage flex flex-col items-center justify-center px-6 text-center">
        <div class="max-w-md w-full fade-in-up">
            <p class="text-xs uppercase tracking-[0.25em] text-gold/75 mb-6">Chapter Zero</p>

            <!-- 3D-Styled Luxury Cake -->
            <div class="cake-stage mb-10">
                <div class="cake-topper">20 • 12 • 2011</div>
                <div class="candles-row">
                    <div class="candle"><div class="flame" id="flame-1"></div><div class="smoke" id="smoke-1"></div></div>
                    <div class="candle"><div class="flame" id="flame-2"></div><div class="smoke" id="smoke-2"></div></div>
                    <div class="candle"><div class="flame" id="flame-3"></div><div class="smoke" id="smoke-3"></div></div>
                </div>
                <div class="cake-tier-top"></div>
                <div class="cake-tier-bottom">
                    <span class="cake-pearl"></span>
                    <span class="cake-pearl"></span>
                    <span class="cake-pearl"></span>
                    <span class="cake-pearl"></span>
                    <span class="cake-pearl"></span>
                </div>
                <div class="cake-plate"></div>
            </div>

            <div id="cake-prompt-before" class="space-y-6">
                <h2 class="font-serif text-2xl sm:text-3xl text-ivory leading-relaxed">
                    “Before I tell you why this date means so much to me…”
                </h2>
                <button onclick="blowOutCandles()" class="btn-gold px-8 py-3.5 rounded-full text-sm tracking-[0.18em] uppercase font-medium">
                    Make a wish ✨
                </button>
            </div>

            <div id="cake-prompt-after" class="hidden space-y-6 fade-in-up">
                <h2 class="font-serif italic text-2xl sm:text-3xl text-gold-light leading-relaxed">
                    “Let’s go back to the beginning.”
                </h2>
                <button onclick="goToStage('stage-03', 'ambient')" class="btn-gold px-8 py-3.5 rounded-full text-sm tracking-[0.18em] uppercase font-medium">
                    Step Back in Time →
                </button>
            </div>
        </div>
    </section>

    <!-- =====================================================================
         STAGE 03: THE DATE (20 DECEMBER 2011)
    ====================================================================== -->
    <section id="stage-03" class="stage-section hidden-stage flex flex-col items-center justify-center px-6 text-center">
        <div class="max-w-lg w-full space-y-8 fade-in-up">
            <div class="inline-block px-4 py-1.5 rounded-full border border-gold/30 bg-burgundy/30 text-gold text-xs tracking-[0.3em] uppercase">
                A Day Like Any Other
            </div>

            <h1 class="font-serif text-4xl sm:text-6xl font-semibold tracking-[0.12em] text-ivory gold-glow-text">
                20 DECEMBER 2011
            </h1>

            <div class="space-y-4 text-ivory/85 font-light text-base sm:text-lg leading-relaxed max-w-md mx-auto">
                <p>
                    Somewhere in the world, millions of people were waking up… living their ordinary day.
                </p>
                <p class="italic font-serif text-xl text-gold-light/95">
                    They didn’t know it yet…<br>
                    but someone very special was about to enter the world.
                </p>
            </div>

            <div class="pt-4 space-y-5">
                <p class="text-xs uppercase tracking-[0.28em] text-gold/80">24 hours before you…</p>
                <button onclick="startTimeCapsule()" class="btn-gold px-9 py-4 rounded-full text-sm tracking-[0.2em] uppercase font-semibold">
                    START JOURNEY →
                </button>
            </div>
        </div>
    </section>

    <!-- =====================================================================
         STAGES 04, 05 & 06: THE 24-HOUR TIME CAPSULE & THE WORLD GETS QUIETER
    ====================================================================== -->
    <section id="stage-04" class="stage-section hidden-stage relative flex flex-col justify-between overflow-hidden">
        <!-- Fullscreen Background Photo with Slow Ken Burns Zoom -->
        <div id="timeline-bg-wrapper" class="absolute inset-0 z-0 transition-opacity duration-1000">
            <img id="timeline-photo" src="" alt="20 December 2011 Snapshot" class="w-full h-full object-cover ken-burns-img opacity-55">
            <div id="timeline-vignette" class="absolute inset-0 bg-gradient-to-t from-obsidian via-obsidian/65 to-obsidian/80 transition-all duration-1000"></div>
        </div>

        <!-- Top Progress & Time Indicator -->
        <div class="relative z-20 pt-6 px-5 sm:px-10 max-w-2xl mx-auto w-full">
            <div class="flex items-center justify-between text-xs tracking-[0.22em] uppercase text-gold/85 mb-2.5">
                <span id="timeline-date-badge">20 DEC 2011</span>
                <span id="timeline-step-counter">1 / 10</span>
            </div>
            <!-- Progress Bar -->
            <div class="w-full h-1 bg-ivory/15 rounded-full overflow-hidden">
                <div id="timeline-progress-bar" class="h-full bg-gradient-to-r from-burgundy-light via-gold to-gold-light transition-all duration-500" style="width: 10%;"></div>
            </div>
        </div>

        <!-- Center / Bottom Narrative Card -->
        <div id="timeline-content-box" class="relative z-20 px-6 pb-10 pt-6 max-w-xl mx-auto w-full flex flex-col items-center text-center my-auto transition-all duration-700">
            <div id="timeline-location-tag" class="inline-block px-3.5 py-1 rounded-full bg-burgundy/50 border border-gold/30 text-gold-light text-[11px] tracking-[0.2em] uppercase mb-4">
                World Snapshot
            </div>

            <h2 id="timeline-hour-display" class="font-serif text-5xl sm:text-7xl font-semibold text-ivory tracking-wider mb-3 gold-glow-text">
                12:00 AM
            </h2>

            <p id="timeline-headline" class="font-serif italic text-xl sm:text-2xl text-gold-light mb-3">
                “The day had just begun.”
            </p>

            <p id="timeline-description" class="text-sm sm:text-base text-ivory/80 font-light leading-relaxed max-w-md mb-8">
                Across quiet city streets and winter skies, midnight marked the start of Tuesday, 20 December 2011.
            </p>

            <!-- Navigation Controls (Swipe or Tap) -->
            <div class="flex items-center justify-center gap-4 w-full">
                <button id="timeline-prev-btn" onclick="prevTimelineSlide()" class="px-5 py-3 rounded-full border border-ivory/20 text-ivory/70 text-xs uppercase tracking-widest hover:border-gold/50 hover:text-ivory transition-all">
                    ← Prev
                </button>
                <button id="timeline-next-btn" onclick="nextTimelineSlide()" class="btn-gold px-8 py-3.5 rounded-full text-xs sm:text-sm uppercase tracking-[0.2em] font-medium flex-1 max-w-[220px]">
                    Next Hour →
                </button>
            </div>
            <p id="swipe-hint" class="text-[11px] text-ivory/40 tracking-widest uppercase mt-4">
                Swipe left or tap to move through time
            </p>
        </div>
    </section>

    <!-- =====================================================================
         STAGE 07: 5:59 PM COUNTDOWN (EMOTIONAL CLIMAX BUILD-UP)
    ====================================================================== -->
    <section id="stage-07" class="stage-section hidden-stage bg-obsidian flex flex-col items-center justify-center px-6 text-center">
        <div class="max-w-md w-full space-y-6">
            <p class="text-xs uppercase tracking-[0.35em] text-gold/60">20 December 2011</p>

            <div id="countdown-clock" class="font-serif text-5xl sm:text-7xl font-bold tracking-widest text-ivory gold-glow-text py-4">
                05:59:50 PM
            </div>

            <div id="countdown-seconds-big" class="font-serif italic text-4xl sm:text-5xl text-gold-light h-14 flex items-center justify-center heartbeat-pulse">
                10…
            </div>

            <p id="countdown-subtext" class="text-xs uppercase tracking-[0.25em] text-ivory/45">
                Listen closely…
            </p>
        </div>
    </section>

    <!-- =====================================================================
         STAGE 08: THE BIRTH REVEAL (6:00 PM)
    ====================================================================== -->
    <section id="stage-08" class="stage-section hidden-stage flex flex-col items-center justify-center px-6 py-12 text-center relative overflow-hidden">
        <!-- Warm Golden Radial Glow -->
        <div class="absolute inset-0 pointer-events-none" style="background: radial-gradient(circle at center, rgba(212, 175, 55, 0.22) 0%, rgba(59, 13, 24, 0.25) 45%, rgba(9, 8, 10, 0.98) 80%);"></div>

        <div class="relative z-10 max-w-md w-full space-y-6">
            <p id="reveal-step-1" class="font-serif italic text-2xl text-ivory/90 opacity-0 transition-opacity duration-1000">
                “And then…”
            </p>

            <h1 id="reveal-step-2" class="font-serif text-5xl sm:text-6xl font-bold text-gold-light tracking-widest gold-glow-text opacity-0 transition-opacity duration-1000">
                6:00 PM
            </h1>

            <!-- Her Portrait Card -->
            <div id="reveal-photo-frame" class="opacity-0 transition-all duration-1000 transform scale-95 mx-auto w-64 sm:w-72 p-3 rounded-2xl luxury-card">
                <div class="aspect-[4/5] w-full rounded-xl overflow-hidden bg-burgundy-dark relative">
                    <img id="her-birth-reveal-photo" src="" alt="The Birthday Girl" class="w-full h-full object-cover">
                    <div class="absolute inset-0 ring-1 ring-inset ring-gold/30 rounded-xl"></div>
                </div>
                <p class="font-serif italic text-gold-light/90 text-sm mt-3">20 • 12 • 2011 — 6:00 PM</p>
            </div>

            <div id="reveal-step-3" class="space-y-3 opacity-0 transition-opacity duration-1000 pt-2">
                <p class="text-sm sm:text-base text-ivory/80 font-light">
                    The best moment of the day happened.
                </p>
                <blockquote class="font-serif text-2xl sm:text-3xl text-gold-light leading-snug font-semibold gold-glow-text">
                    “And that was the best time of the day…<br>my gurl was born. ❤️”
                </blockquote>
            </div>

            <div id="reveal-continue-btn" class="opacity-0 transition-opacity duration-1000 pt-4">
                <button onclick="enterStoryScrollMode()" class="btn-gold px-8 py-3.5 rounded-full text-xs sm:text-sm uppercase tracking-[0.2em] font-medium">
                    Continue Our Story ↓
                </button>
            </div>
        </div>
    </section>

    <!-- =====================================================================
         STAGES 09 TO 15: THE PERSONAL LOVE STORY EXPERIENCE (SCROLLABLE)
    ====================================================================== -->
    <main id="story-journey-container" class="hidden-stage relative z-10">

        <!-- ================= 09: "AND YEARS LATER..." ================= -->
        <section class="min-h-screen flex flex-col items-center justify-center px-6 py-20 text-center max-w-xl mx-auto">
            <div class="space-y-8">
                <p class="font-serif italic text-2xl sm:text-3xl text-ivory/85">“The world kept moving…”</p>
                <p class="font-serif italic text-2xl sm:text-3xl text-ivory/75">“Years passed.”</p>
                <div class="w-px h-14 bg-gradient-to-b from-gold/60 to-transparent mx-auto"></div>
                <p class="font-serif italic text-2xl sm:text-3xl text-gold-light">“And somehow…”</p>

                <!-- Couple Photo Frame -->
                <div class="p-3.5 rounded-2xl luxury-card max-w-xs sm:max-w-sm mx-auto">
                    <div class="aspect-[4/5] rounded-xl overflow-hidden">
                        <img id="years-later-couple-photo" src="" alt="Us" class="w-full h-full object-cover">
                    </div>
                </div>

                <h2 class="font-serif text-4xl sm:text-5xl text-ivory font-semibold gold-glow-text pt-2">
                    “I found you.” 🔥
                </h2>
            </div>
        </section>

        <!-- ================= 10: YOUR STORY (CHAPTERS 01 - 04) ================= -->
        <section class="py-20 px-6 max-w-3xl mx-auto">
            <div class="text-center mb-14">
                <p class="text-xs uppercase tracking-[0.3em] text-gold mb-3">Our Little Story</p>
                <h2 class="font-serif text-3xl sm:text-5xl text-ivory font-semibold">How We Became Us 🫶</h2>
            </div>

            <div id="chapters-container" class="space-y-12">
                <!-- Populated dynamically from CONFIG.chapters -->
            </div>
        </section>

        <!-- ================= 11: MEMORY GALLERY (POLAROID CARDS) ================= -->
        <section class="py-20 px-6 max-w-4xl mx-auto">
            <div class="text-center mb-14">
                <p class="text-xs uppercase tracking-[0.3em] text-gold mb-3">Snapshots of You & Me</p>
                <h2 class="font-serif text-3xl sm:text-5xl text-ivory font-semibold">Memory Gallery 📸</h2>
                <p class="text-xs text-ivory/60 mt-2">Tap any photo to view full screen</p>
            </div>

            <div id="polaroid-grid" class="grid grid-cols-1 sm:grid-cols-2 gap-8 max-w-2xl mx-auto">
                <!-- Populated dynamically from CONFIG.gallery -->
            </div>
        </section>

        <!-- ================= 12: "THINGS I LOVE ABOUT YOU" ================= -->
        <section class="py-24 px-6 max-w-lg mx-auto text-center">
            <p class="text-xs uppercase tracking-[0.3em] text-gold mb-3">Just A Few Reasons</p>
            <h2 class="font-serif text-3xl sm:text-4xl text-ivory font-semibold mb-10">Things I Love About You ❤️</h2>

            <div class="luxury-card rounded-3xl p-8 sm:p-10 min-h-[290px] flex flex-col items-center justify-between relative overflow-hidden">
                <div id="love-card-number" class="text-xs uppercase tracking-[0.3em] text-gold/80">
                    For You
                </div>

                <div id="love-card-body" class="my-6 space-y-3 transition-all duration-300">
                    <h3 id="love-card-title" class="font-serif text-2xl sm:text-3xl text-gold-light">
                        Want to know why you’re so special to me?
                    </h3>
                    <p id="love-card-desc" class="text-sm sm:text-base text-ivory/80 font-light leading-relaxed">
                        Tap below and let me tell you…
                    </p>
                </div>

                <button id="love-card-btn" onclick="nextLoveReason()" class="btn-gold px-8 py-3 rounded-full text-xs sm:text-sm uppercase tracking-[0.2em] font-medium">
                    Tell me ❤️
                </button>
            </div>
        </section>

        <!-- ================= 13: LITTLE SURPRISE (GIFT BOX) ================= -->
        <section class="py-20 px-6 max-w-md mx-auto text-center">
            <p class="text-xs uppercase tracking-[0.3em] text-gold mb-3">Before The Final Letter</p>
            <h2 class="font-serif text-3xl text-ivory font-semibold mb-8">One more thing… 🎁</h2>

            <div id="gift-box-container" onclick="openGiftBox()" class="cursor-pointer mx-auto w-44 h-44 relative flex flex-col items-center justify-center select-none">
                <!-- Gift Lid -->
                <div class="gift-lid w-40 h-9 bg-gradient-to-r from-burgundy-light via-burgundy to-burgundy-light border border-gold rounded-md relative z-20 shadow-lg flex items-center justify-center">
                    <div class="w-6 h-full bg-gold/80"></div>
                    <!-- Ribbon Bow -->
                    <div class="absolute -top-4 w-10 h-4 border-2 border-gold rounded-full"></div>
                </div>
                <!-- Gift Box Base -->
                <div class="w-36 h-28 bg-gradient-to-b from-burgundy to-burgundy-dark border-x border-b border-gold/60 rounded-b-lg relative z-10 shadow-2xl flex items-center justify-center">
                    <div class="w-6 h-full bg-gold/80"></div>
                </div>
                <p id="gift-tap-hint" class="text-xs uppercase tracking-widest text-gold-light mt-4 animate-pulse">
                    Tap to open gift
                </p>
            </div>

            <!-- Revealed Personal Short Note -->
            <div id="gift-secret-message" class="hidden mt-6 p-6 rounded-2xl luxury-card fade-in-up">
                <p id="gift-message-text" class="font-serif italic text-xl text-gold-light leading-relaxed">
                    <!-- Populated from CONFIG.giftNote -->
                </p>
            </div>
        </section>

        <!-- ================= 14: THE LETTER (HANDWRITTEN) ================= -->
        <section class="py-24 px-5 max-w-2xl mx-auto">
            <div class="text-center mb-10">
                <p class="text-xs uppercase tracking-[0.3em] text-gold mb-3">From My Heart To Yours</p>
                <h2 class="font-serif text-3xl sm:text-4xl text-ivory font-semibold">A letter I wrote just for you. 💌</h2>
            </div>

            <!-- Closed Letter Trigger -->
            <div id="final-letter-closed" onclick="openFinalLetter()" class="luxury-card rounded-2xl p-10 text-center cursor-pointer hover:border-gold transition-all max-w-md mx-auto">
                <div class="w-14 h-14 rounded-full bg-burgundy-light/70 border border-gold/50 flex items-center justify-center mx-auto mb-5 text-2xl text-gold-light">
                    ✉️
                </div>
                <p class="font-serif italic text-xl text-ivory mb-4">Sealed with all my love</p>
                <span class="btn-gold inline-block px-7 py-2.5 rounded-full text-xs uppercase tracking-[0.2em]">
                    Read Letter
                </span>
            </div>

            <!-- Opened Handwritten Letter -->
            <div id="final-letter-opened" class="hidden rounded-2xl p-7 sm:p-12 shadow-2xl fade-in-up relative" style="background: linear-gradient(165deg, #1c1316 0%, #100b0d 100%); border: 1px solid rgba(212, 175, 55, 0.35);">
                <div class="flex justify-between items-center border-b border-gold/20 pb-4 mb-6">
                    <span class="font-serif italic text-sm text-gold/80">20 December</span>
                    <span class="text-gold text-sm">♡</span>
                </div>

                <div id="letter-content-area" class="font-hand text-2xl sm:text-[27px] text-ivory/95 leading-[1.65] space-y-5 whitespace-pre-line">
                    <!-- Populated from CONFIG.letter -->
                </div>
            </div>
        </section>

        <!-- ================= 15: FINAL SCREEN (STARRY NIGHT CLOSING) ================= -->
        <section class="min-h-screen flex flex-col items-center justify-center px-6 py-24 text-center relative">
            <div class="max-w-md w-full space-y-8">
                <!-- Couple Favorite Photo -->
                <div class="p-3 rounded-2xl luxury-card w-64 sm:w-72 mx-auto shadow-2xl">
                    <div class="aspect-square rounded-xl overflow-hidden">
                        <img id="final-screen-photo" src="" alt="Forever Us" class="w-full h-full object-cover">
                    </div>
                </div>

                <div class="space-y-3 pt-2">
                    <p class="font-serif text-2xl sm:text-3xl text-ivory/90">“20 December 2011…”</p>
                    <p class="font-serif italic text-xl sm:text-2xl text-gold-light/90">“The day you were born.”</p>
                    <div class="w-px h-10 bg-gold/40 mx-auto my-3"></div>
                    <p class="font-serif text-2xl sm:text-3xl text-ivory/90">“Years later…”</p>
                    <p class="font-serif italic text-2xl sm:text-3xl text-gold-light font-semibold gold-glow-text">
                        “The day you became mine.” ❤️
                    </p>
                </div>

                <div class="pt-6 space-y-3">
                    <h1 class="font-serif text-4xl sm:text-5xl font-bold text-ivory gold-glow-text">
                        Happy Birthday, Mah Gurl.
                    </h1>
                    <p class="font-hand text-3xl text-gold-light pt-2">
                        I love you.
                    </p>
                </div>

                <div class="pt-10">
                    <button onclick="replayWholeJourney()" class="px-6 py-2.5 rounded-full border border-gold/30 text-gold/80 text-xs uppercase tracking-[0.22em] hover:border-gold hover:text-gold-light transition-all">
                        Replay Journey ↺
                    </button>
                </div>
            </div>
        </section>
    </main>

    <!-- Fullscreen Lightbox Modal for Memory Gallery -->
    <div id="photo-lightbox" onclick="closeLightbox()" class="fixed inset-0 z-[9990] bg-obsidian/95 backdrop-blur-md hidden flex-col items-center justify-center p-6">
        <button onclick="closeLightbox()" class="absolute top-5 right-5 text-ivory/80 hover:text-gold text-2xl px-3 py-1">✕</button>
        <img id="lightbox-img" src="" alt="Full Memory" class="max-h-[75vh] max-w-full rounded-xl border border-gold/30 shadow-2xl mb-4">
        <p id="lightbox-caption" class="font-hand text-2xl sm:text-3xl text-gold-light text-center"></p>
    </div>

    <!-- Confetti Canvas for Cake Wish -->
    <canvas id="confetti-canvas" class="fixed inset-0 pointer-events-none z-[9995]"></canvas>

    <!-- =====================================================================
         JAVASCRIPT: CUSTOMIZATION CONFIG, AUDIO ENGINE & INTERACTIVE FLOW
    ====================================================================== -->
    <script>
        /**
         * =====================================================================
         * 1. CUSTOMIZE YOUR PHOTOS, AUDIO, CHAPTERS & LETTER HERE
         * (GitHub-e upload korar age ei section-er text ar photo link gulo change korbe)
         * =====================================================================
         */
        const CONFIG = {
            // Optional: Nijer MP3 file-er link dite paro (e.g. "./music/song.mp3").
            // Khali ("") rakhle built-in Web Audio API Piano & Heartbeat music cholbe!
            customAudio: {
                openingPiano: "",
                timelineAmbient: "",
                romanticTheme: ""
            },

            // Main Portraits (Replace URLs with "./images/her-photo.jpg", "./images/us.jpg", etc.)
            photos: {
                herBirthReveal: "https://images.unsplash.com/photo-1518568814500-bf0f8d125f46?auto=format&fit=crop&w=800&q=80",
                yearsLaterCouple: "https://images.unsplash.com/photo-1516589178581-6cd7833ae3b2?auto=format&fit=crop&w=800&q=80",
                finalScreenCouple: "https://images.unsplash.com/photo-1522673607200-164d1b6ce486?auto=format&fit=crop&w=800&q=80"
            },

            // 20 December 2011 — Time Capsule Slides (12:00 AM -> 5:50 PM)
            // Includes real historical context & Bangladesh winter atmosphere from Dec 2011
            timeline: [
                {
                    hour: "12:00 AM",
                    tag: "World Snapshot • Midnight",
                    headline: "“The day had just begun.”",
                    description: "Across quiet city skylines and cold December streets, midnight marked the start of Tuesday, 20 December 2011.",
                    photo: "https://images.unsplash.com/photo-1519501025264-65ba15a82390?auto=format&fit=crop&w=1200&q=80",
                    dimLevel: 0
                },
                {
                    hour: "2:00 AM",
                    tag: "Global Night • Winter 2011",
                    headline: "“While the world was moving through another ordinary night…”",
                    description: "Two days before the December solstice, the northern hemisphere rested under long, crisp winter stars.",
                    photo: "https://images.unsplash.com/photo-1419242902214-272b3f66ee7a?auto=format&fit=crop&w=1200&q=80",
                    dimLevel: 0
                },
                {
                    hour: "6:00 AM",
                    tag: "Bangladesh • 20 Dec 2011 Morning",
                    headline: "“A misty December dawn broke over Bangladesh.”",
                    description: "Days after celebrating 40 years of Victory in December 2011, winter fog covered quiet morning streets and tea stalls across the country.",
                    photo: "https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=1200&q=80",
                    dimLevel: 0
                },
                {
                    hour: "9:00 AM",
                    tag: "Global Headlines • 20 Dec 2011",
                    headline: "“Somewhere far away, another story was unfolding.”",
                    description: "Around the world, newspapers reported on global summits, winter storms in Asia, and nations mourning Czech leader Václav Havel.",
                    photo: "https://images.unsplash.com/photo-1504711434969-e33886168f5c?auto=format&fit=crop&w=1200&q=80",
                    dimLevel: 0
                },
                {
                    hour: "12:00 PM",
                    tag: "Midday • 20 December 2011",
                    headline: "“Half the day had passed…”",
                    description: "Millions hurried through busy afternoon routines, completely unaware of the little miracle waiting just hours away.",
                    photo: "https://images.unsplash.com/photo-1477959858617-67f85cf4f1df?auto=format&fit=crop&w=1200&q=80",
                    dimLevel: 0
                },
                {
                    hour: "3:00 PM",
                    tag: "Afternoon Light",
                    headline: "“The afternoon sun began to soften.”",
                    description: "Golden winter light stretched across rooftops as afternoon slowly turned toward evening.",
                    photo: "https://images.unsplash.com/photo-1470252649378-9c29740c9fa8?auto=format&fit=crop&w=1200&q=80",
                    dimLevel: 0
                },
                {
                    hour: "4:00 PM",
                    tag: "The World Gets Quieter",
                    headline: "“Two hours left.”",
                    description: "The noise of the afternoon began to fade into the calm of dusk.",
                    photo: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=1200&q=80",
                    dimLevel: 1
                },
                {
                    hour: "5:00 PM",
                    tag: "Dusk Falls",
                    headline: "“The sky turned deep twilight.”",
                    description: "Everything felt softer. Quieter. Like the universe was holding its breath.",
                    photo: "https://images.unsplash.com/photo-1518837695005-2083093ee35b?auto=format&fit=crop&w=1200&q=80",
                    dimLevel: 2
                },
                {
                    hour: "5:30 PM",
                    tag: "Almost Time",
                    headline: "“Just thirty minutes away…”",
                    description: "Every second was leading to one unforgettable moment.",
                    photo: "https://images.unsplash.com/photo-1464802686167-b939a6910659?auto=format&fit=crop&w=1200&q=80",
                    dimLevel: 3
                },
                {
                    hour: "5:50 PM",
                    tag: "10 Minutes Before You",
                    headline: "“We’re getting close.”",
                    description: "The whole world went still.",
                    photo: "",
                    dimLevel: 4
                }
            ],

            // Section 10: Relationship Chapters
            chapters: [
                {
                    number: "Chapter 01",
                    title: "The Beginning",
                    story: "When our paths first crossed, I had no idea that a simple conversation would turn into my favorite part of every single day.",
                    photo: "https://images.unsplash.com/photo-1511632765486-a01980e01a18?auto=format&fit=crop&w=800&q=80"
                },
                {
                    number: "Chapter 02",
                    title: "Getting Close",
                    story: "Late-night talks, endless notifications, and realizing how effortlessly you understood things I never even said out loud.",
                    photo: "https://images.unsplash.com/photo-1529333166437-7750a6dd5a70?auto=format&fit=crop&w=800&q=80"
                },
                {
                    number: "Chapter 03",
                    title: "The Memories",
                    story: "All our silly inside jokes, random laughs, and little moments that nobody else knows about—those are my favorite treasures.",
                    photo: "https://images.unsplash.com/photo-1523438885200-e635ba2c371e?auto=format&fit=crop&w=800&q=80"
                },
                {
                    number: "Chapter 04",
                    title: "Us",
                    story: "Right here, right now. Out of billions of people in this world, I still can’t believe I get to call you mine.",
                    photo: "https://images.unsplash.com/photo-1518199266791-5375a83190b7?auto=format&fit=crop&w=800&q=80"
                }
            ],

            // Section 11: Polaroid Memory Gallery
            gallery: [
                {
                    caption: "My favorite smile.",
                    photo: "https://images.unsplash.com/photo-1524504388940-b1c1722653e1?auto=format&fit=crop&w=800&q=80",
                    rotate: "-2deg"
                },
                {
                    caption: "This picture >>>",
                    photo: "https://images.unsplash.com/photo-1517841905240-472988babdf9?auto=format&fit=crop&w=800&q=80",
                    rotate: "2deg"
                },
                {
                    caption: "One of my favorite memories.",
                    photo: "https://images.unsplash.com/photo-1529626455594-4ff0802cfb7e?auto=format&fit=crop&w=800&q=80",
                    rotate: "1.5deg"
                },
                {
                    caption: "Every moment with you.",
                    photo: "https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=800&q=80",
                    rotate: "-1.5deg"
                }
            ],

            // Section 12: Things I Love About You
            loveReasons: [
                {
                    num: "01",
                    title: "Your smile.",
                    desc: "“I don’t think you realize what your smile does to me. One look and my whole mood changes.”"
                },
                {
                    num: "02",
                    title: "Your little habits.",
                    desc: "“The tiny things you do without even noticing—your expressions, the way you talk when you’re excited, everything.”"
                },
                {
                    num: "03",
                    title: "The way you care.",
                    desc: "“You have the purest heart. The way you notice small details and care so deeply makes you one of a kind.”"
                },
                {
                    num: "04",
                    title: "The way you make ordinary days special.",
                    desc: "“Even the most boring day feels like my favorite memory whenever you’re around.”"
                }
            ],

            // Section 13: Little Surprise Gift Note (Keep it personal & short)
            giftNote: "“No matter where life takes us, I promise to always be your biggest supporter, your safe place, and the person who celebrates you every single day. Happy Birthday, my love.”",

            // Section 14: Handwritten Personal Birthday Letter
            letter: `Happy Birthday, Mah Gurl ❤️

I wanted to make something different for you today—something that reminds you just how much your existence means to me.

On 20 December 2011 at 6:00 PM, the world got a little brighter, even if nobody else realized it back then. Years later, meeting you became the best thing that ever happened to my life.

Thank you for your laugh, your patience, our late-night conversations, and all the little moments that only you and I understand. You don't even have to try—just being yourself makes my world complete.

I hope this year brings you all the happiness, peace, and warmth you give to everyone around you.

Forever yours,
Your Favorite Person ♡`
        };

        /**
         * =====================================================================
         * 2. WEB AUDIO API CINEMATIC SOUND ENGINE (PIANO, AMBIENT & HEARTBEAT)
         * =====================================================================
         */
        class SoundEngine {
            constructor() {
                this.ctx = null;
                this.isPlaying = false;
                this.currentMode = 'piano'; // 'piano' | 'ambient' | 'romantic' | 'muted'
                this.loopTimer = null;
                this.masterGain = null;
            }

            init() {
                if (!this.ctx) {
                    const AudioCtx = window.AudioContext || window.webkitAudioContext;
                    this.ctx = new AudioCtx();
                    this.masterGain = this.ctx.createGain();
                    this.masterGain.gain.value = 0.25;
                    this.masterGain.connect(this.ctx.destination);
                }
                if (this.ctx.state === 'suspended') {
                    this.ctx.resume();
                }
            }

            toggle() {
                if (!this.isPlaying) {
                    this.init();
                    this.isPlaying = true;
                    this.setMode(this.currentMode === 'muted' ? 'piano' : this.currentMode);
                } else {
                    this.isPlaying = false;
                    clearInterval(this.loopTimer);
                    if (this.masterGain && this.ctx) {
                        this.masterGain.gain.setTargetAtTime(0.0001, this.ctx.currentTime, 0.2);
                    }
                }
                this.updateUI();
            }

            updateUI() {
                const icon = document.getElementById('music-icon');
                const label = document.getElementById('music-label');
                if (this.isPlaying) {
                    icon.textContent = '🔊';
                    label.textContent = 'Sound On';
                } else {
                    icon.textContent = '🔇';
                    label.textContent = 'Sound Off';
                }
            }

            setMode(mode) {
                this.currentMode = mode;
                clearInterval(this.loopTimer);
                if (!this.isPlaying || !this.ctx) return;

                if (mode === 'muted') {
                    this.masterGain.gain.setTargetAtTime(0.0001, this.ctx.currentTime, 0.5);
                    return;
                }

                this.masterGain.gain.setTargetAtTime(0.25, this.ctx.currentTime, 0.5);

                if (mode === 'piano') {
                    const chords = [
                        [261.63, 329.63, 392.00, 493.88], // Cmaj7
                        [220.00, 261.63, 329.63, 392.00], // Am7
                        [174.61, 220.00, 261.63, 349.23], // Fmaj7
                        [196.00, 246.94, 293.66, 392.00]  // G6
                    ];
                    let idx = 0;
                    const playChord = () => {
                        if (!this.isPlaying) return;
                        const notes = chords[idx % chords.length];
                        notes.forEach((freq, i) => {
                            setTimeout(() => this.playSoftNote(freq, 2.8, 'sine', 0.14), i * 160);
                        });
                        idx++;
                    };
                    playChord();
                    this.loopTimer = setInterval(playChord, 3400);
                } else if (mode === 'ambient') {
                    const drones = [130.81, 146.83, 164.81, 196.00];
                    let idx = 0;
                    const playPad = () => {
                        if (!this.isPlaying) return;
                        const f = drones[idx % drones.length];
                        this.playSoftNote(f, 4.2, 'triangle', 0.10);
                        this.playSoftNote(f * 1.5, 4.2, 'sine', 0.08);
                        idx++;
                    };
                    playPad();
                    this.loopTimer = setInterval(playPad, 3800);
                } else if (mode === 'romantic') {
                    const melody = [
                        [329.63, 392.00, 493.88],
                        [349.23, 440.00, 523.25],
                        [293.66, 392.00, 493.88],
                        [261.63, 329.63, 392.00]
                    ];
                    let idx = 0;
                    const playRomantic = () => {
                        if (!this.isPlaying) return;
                        const notes = melody[idx % melody.length];
                        notes.forEach((freq, i) => {
                            setTimeout(() => this.playSoftNote(freq, 3.0, 'sine', 0.16), i * 220);
                        });
                        idx++;
                    };
                    playRomantic();
                    this.loopTimer = setInterval(playRomantic, 3200);
                }
            }

            playSoftNote(freq, duration, type = 'sine', volume = 0.15) {
                if (!this.ctx || !this.isPlaying) return;
                const now = this.ctx.currentTime;
                const osc = this.ctx.createOscillator();
                const gain = this.ctx.createGain();
                osc.type = type;
                osc.frequency.setValueAtTime(freq, now);

                gain.gain.setValueAtTime(0.0001, now);
                gain.gain.exponentialRampToValueAtTime(volume, now + 0.25);
                gain.gain.exponentialRampToValueAtTime(0.0001, now + duration);

                osc.connect(gain);
                gain.connect(this.masterGain);
                osc.start(now);
                osc.stop(now + duration + 0.1);
            }

            // Realistic Double-Thump Heartbeat (Lub-Dub)
            playHeartbeat(intensity = 1.0) {
                if (!this.ctx) this.init();
                if (!this.isPlaying) return;

                const thump = (delay, freq, vol) => {
                    const now = this.ctx.currentTime + delay;
                    const osc = this.ctx.createOscillator();
                    const gain = this.ctx.createGain();
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(freq, now);
                    osc.frequency.exponentialRampToValueAtTime(28, now + 0.18);

                    gain.gain.setValueAtTime(0.001, now);
                    gain.gain.exponentialRampToValueAtTime(vol * intensity, now + 0.03);
                    gain.gain.exponentialRampToValueAtTime(0.001, now + 0.22);

                    osc.connect(gain);
                    gain.connect(this.ctx.destination);
                    osc.start(now);
                    osc.stop(now + 0.25);
                };

                thump(0, 68, 0.45);     // Lub
                thump(0.18, 54, 0.32);  // Dub
            }
        }

        const audioEngine = new SoundEngine();
        document.getElementById('music-toggle').addEventListener('click', () => audioEngine.toggle());

        /**
         * =====================================================================
         * 3. STAGE NAVIGATION & INTERACTIVE LOGIC
         * =====================================================================
         */
        let currentTimelineIndex = 0;
        let currentLoveIndex = -1;

        function goToStage(stageId, audioMode = null) {
            document.querySelectorAll('.stage-section').forEach(sec => {
                sec.classList.add('hidden-stage');
            });
            const target = document.getElementById(stageId);
            if (target) {
                target.classList.remove('hidden-stage');
                window.scrollTo({ top: 0, behavior: 'smooth' });
            }
            if (audioMode) {
                audioEngine.setMode(audioMode);
            }
        }

        // Stage 01: Envelope Open
        function handleOpenEnvelope() {
            const env = document.getElementById('opening-envelope');
            if (env.classList.contains('opened')) return;

            // Auto-start soft music on first user gesture
            if (!audioEngine.isPlaying) {
                audioEngine.toggle();
            }

            env.classList.add('opened');
            document.getElementById('opening-initial-text').classList.add('hidden');
            setTimeout(() => {
                document.getElementById('opening-continue-text').classList.remove('hidden');
            }, 650);
        }

        // Stage 02: Blow Out Cake Candles + Confetti
        function blowOutCandles() {
            [1, 2, 3].forEach(i => {
                document.getElementById(`flame-${i}`).classList.add('blown-out');
                document.getElementById(`smoke-${i}`).classList.add('rising');
            });

            launchGoldConfetti();

            document.getElementById('cake-prompt-before').classList.add('hidden');
            setTimeout(() => {
                document.getElementById('cake-prompt-after').classList.remove('hidden');
            }, 600);
        }

        // Stage 04: Time Capsule Timeline
        function startTimeCapsule() {
            currentTimelineIndex = 0;
            goToStage('stage-04', 'ambient');
            renderTimelineSlide();
        }

        function renderTimelineSlide() {
            const item = CONFIG.timeline[currentTimelineIndex];
            const total = CONFIG.timeline.length;

            document.getElementById('timeline-step-counter').textContent = `${currentTimelineIndex + 1} / ${total}`;
            document.getElementById('timeline-progress-bar').style.width = `${((currentTimelineIndex + 1) / total) * 100}%`;

            document.getElementById('timeline-location-tag').textContent = item.tag;
            document.getElementById('timeline-hour-display').textContent = item.hour;
            document.getElementById('timeline-headline').textContent = item.headline;
            document.getElementById('timeline-description').textContent = item.description;

            const photoEl = document.getElementById('timeline-photo');
            const bgWrapper = document.getElementById('timeline-bg-wrapper');
            const nextBtn = document.getElementById('timeline-next-btn');

            if (item.photo) {
                photoEl.src = item.photo;
                bgWrapper.style.opacity = item.dimLevel === 0 ? '1' :
                                          item.dimLevel === 1 ? '0.65' :
                                          item.dimLevel === 2 ? '0.35' : '0.12';
            } else {
                bgWrapper.style.opacity = '0';
            }

            // Stage 06: The World Gets Quieter (Audio & UI softening near 6 PM)
            if (item.dimLevel === 2 && audioEngine.isPlaying && audioEngine.masterGain) {
                audioEngine.masterGain.gain.setTargetAtTime(0.10, audioEngine.ctx.currentTime, 0.8);
            } else if (item.dimLevel >= 3 && audioEngine.isPlaying && audioEngine.masterGain) {
                audioEngine.masterGain.gain.setTargetAtTime(0.02, audioEngine.ctx.currentTime, 0.8);
            }

            if (currentTimelineIndex === total - 1) {
                nextBtn.textContent = "5:59 PM →";
            } else {
                nextBtn.textContent = "Next Hour →";
            }
        }

        function nextTimelineSlide() {
            if (currentTimelineIndex < CONFIG.timeline.length - 1) {
                currentTimelineIndex++;
                renderTimelineSlide();
            } else {
                start559Countdown();
            }
        }

        function prevTimelineSlide() {
            if (currentTimelineIndex > 0) {
                currentTimelineIndex--;
                renderTimelineSlide();
            }
        }

        // Touch Swipe Support for Mobile Timeline
        let touchStartX = 0;
        const timelineSection = document.getElementById('stage-04');
        timelineSection.addEventListener('touchstart', e => {
            touchStartX = e.changedTouches[0].screenX;
        }, { passive: true });

        timelineSection.addEventListener('touchend', e => {
            const touchEndX = e.changedTouches[0].screenX;
            const diff = touchStartX - touchEndX;
            if (Math.abs(diff) > 45) {
                if (diff > 0) nextTimelineSlide();
                else prevTimelineSlide();
            }
        }, { passive: true });

        // Stage 07: 5:59:50 PM -> 6:00:00 PM Heartbeat Countdown
        function start559Countdown() {
            goToStage('stage-07', 'muted');

            let secondsLeft = 10;
            const clockEl = document.getElementById('countdown-clock');
            const bigSecEl = document.getElementById('countdown-seconds-big');

            clockEl.textContent = "05:59:50 PM";
            bigSecEl.textContent = "10…";
            audioEngine.playHeartbeat(0.7);

            const timer = setInterval(() => {
                secondsLeft--;
                if (secondsLeft > 0) {
                    const secFormatted = 60 - secondsLeft;
                    clockEl.textContent = `05:59:${secFormatted} PM`;
                    bigSecEl.textContent = `${secondsLeft}…`;
                    audioEngine.playHeartbeat(0.7 + (10 - secondsLeft) * 0.05);
                } else {
                    clearInterval(timer);
                    clockEl.textContent = "06:00:00 PM";
                    bigSecEl.textContent = "♡";
                    audioEngine.playHeartbeat(1.35);

                    // Dramatic blackout pause before Birth Reveal
                    setTimeout(() => {
                        triggerBirthReveal();
                    }, 1200);
                }
            }, 1000);
        }

        // Stage 08: The Birth Reveal (6:00 PM)
        function triggerBirthReveal() {
            goToStage('stage-08', 'romantic');

            setTimeout(() => {
                document.getElementById('reveal-step-1').classList.remove('opacity-0');
            }, 400);

            setTimeout(() => {
                document.getElementById('reveal-step-2').classList.remove('opacity-0');
            }, 1600);

            setTimeout(() => {
                const frame = document.getElementById('reveal-photo-frame');
                frame.classList.remove('opacity-0', 'scale-95');
                frame.classList.add('scale-100');
            }, 2800);

            setTimeout(() => {
                document.getElementById('reveal-step-3').classList.remove('opacity-0');
            }, 4000);

            setTimeout(() => {
                document.getElementById('reveal-continue-btn').classList.remove('opacity-0');
            }, 5400);
        }

        // Enter Scrollable Stages 09 -> 15
        function enterStoryScrollMode() {
            document.getElementById('story-journey-container').classList.remove('hidden-stage');
            const target = document.getElementById('story-journey-container');
            target.scrollIntoView({ behavior: 'smooth' });
        }

        // Stage 12: Interactive "Things I Love About You"
        function nextLoveReason() {
            currentLoveIndex++;
            const numEl = document.getElementById('love-card-number');
            const titleEl = document.getElementById('love-card-title');
            const descEl = document.getElementById('love-card-desc');
            const btnEl = document.getElementById('love-card-btn');

            if (currentLoveIndex < CONFIG.loveReasons.length) {
                const item = CONFIG.loveReasons[currentLoveIndex];
                numEl.textContent = `Reason ${item.num}`;
                titleEl.textContent = `${item.num} — ${item.title}`;
                descEl.textContent = item.desc;
                btnEl.textContent = currentLoveIndex === CONFIG.loveReasons.length - 1 ? "And finally… ❤️" : "Next →";
            } else {
                numEl.textContent = "∞";
                titleEl.textContent = "“I could list a thousand more…”";
                descEl.textContent = "Every single day gives me a new reason to fall for you all over again.";
                btnEl.textContent = "Read Again ↺";
                currentLoveIndex = -1;
            }
        }

        // Stage 13: Open Little Surprise Gift Box
        function openGiftBox() {
            const box = document.getElementById('gift-box-container');
            if (box.classList.contains('gift-opened')) return;
            box.classList.add('gift-opened');
            document.getElementById('gift-tap-hint').style.display = 'none';
            launchGoldConfetti();
            setTimeout(() => {
                document.getElementById('gift-secret-message').classList.remove('hidden');
            }, 400);
        }

        // Stage 14: Open Handwritten Letter
        function openFinalLetter() {
            document.getElementById('final-letter-closed').classList.add('hidden');
            document.getElementById('final-letter-opened').classList.remove('hidden');
        }

        // Stage 11: Lightbox
        function openLightbox(photoUrl, caption) {
            const lb = document.getElementById('photo-lightbox');
            document.getElementById('lightbox-img').src = photoUrl;
            document.getElementById('lightbox-caption').textContent = caption;
            lb.classList.remove('hidden');
            lb.classList.add('flex');
        }

        function closeLightbox() {
            const lb = document.getElementById('photo-lightbox');
            lb.classList.add('hidden');
            lb.classList.remove('flex');
        }

        // Replay Entire Experience
        function replayWholeJourney() {
            document.getElementById('story-journey-container').classList.add('hidden-stage');
            document.getElementById('opening-envelope').classList.remove('opened');
            document.getElementById('opening-initial-text').classList.remove('hidden');
            document.getElementById('opening-continue-text').classList.add('hidden');
            [1, 2, 3].forEach(i => {
                document.getElementById(`flame-${i}`).classList.remove('blown-out');
                document.getElementById(`smoke-${i}`).classList.remove('rising');
            });
            document.getElementById('cake-prompt-before').classList.remove('hidden');
            document.getElementById('cake-prompt-after').classList.add('hidden');
            goToStage('stage-01', 'piano');
        }

        /**
         * =====================================================================
         * 4. POPULATE DYNAMIC CONTENT & AMBIENT PARTICLE / CONFETTI CANVAS
         * =====================================================================
         */
        function populateContent() {
            document.getElementById('her-birth-reveal-photo').src = CONFIG.photos.herBirthReveal;
            document.getElementById('years-later-couple-photo').src = CONFIG.photos.yearsLaterCouple;
            document.getElementById('final-screen-photo').src = CONFIG.photos.finalScreenCouple;
            document.getElementById('gift-message-text').textContent = CONFIG.giftNote;
            document.getElementById('letter-content-area').textContent = CONFIG.letter;

            // Populate Story Chapters
            const chaptersEl = document.getElementById('chapters-container');
            chaptersEl.innerHTML = CONFIG.chapters.map((ch, index) => `
                <div class="luxury-card rounded-3xl p-6 sm:p-8 flex flex-col ${index % 2 === 1 ? 'sm:flex-row-reverse' : 'sm:flex-row'} items-center gap-6 sm:gap-8">
                    <div class="w-full sm:w-5/12 aspect-[4/5] rounded-2xl overflow-hidden shrink-0 border border-gold/25">
                        <img src="${ch.photo}" alt="${ch.title}" class="w-full h-full object-cover">
                    </div>
                    <div class="w-full sm:w-7/12 text-center sm:text-left space-y-3">
                        <span class="text-xs uppercase tracking-[0.28em] text-gold">${ch.number}</span>
                        <h3 class="font-serif text-2xl sm:text-3xl text-ivory font-semibold">${ch.title}</h3>
                        <p class="text-sm sm:text-base text-ivory/80 font-light leading-relaxed">${ch.story}</p>
                    </div>
                </div>
            `).join('');

            // Populate Polaroid Gallery
            const galleryEl = document.getElementById('polaroid-grid');
            galleryEl.innerHTML = CONFIG.gallery.map(item => `
                <div onclick="openLightbox('${item.photo}', '${item.caption.replace(/'/g, "\\'")}')" 
                     style="transform: rotate(${item.rotate});" 
                     class="polaroid-card cursor-pointer">
                    <div class="aspect-[4/5] w-full overflow-hidden rounded-sm bg-neutral-900 mb-3">
                        <img src="${item.photo}" alt="${item.caption}" class="w-full h-full object-cover">
                    </div>
                    <p class="font-hand text-2xl text-center text-neutral-800">${item.caption}</p>
                </div>
            `).join('');
        }

        // Ambient Floating Gold Particles & Twinkling Stars
        function initAmbientParticles() {
            const canvas = document.getElementById('ambient-canvas');
            const ctx = canvas.getContext('2d');
            let width, height, particles;

            function resize() {
                width = canvas.width = window.innerWidth;
                height = canvas.height = window.innerHeight;
            }

            function createParticles() {
                const count = Math.min(55, Math.floor((width * height) / 18000));
                particles = Array.from({ length: count }, () => ({
                    x: Math.random() * width,
                    y: Math.random() * height,
                    r: Math.random() * 1.8 + 0.5,
                    vx: (Math.random() - 0.5) * 0.22,
                    vy: -Math.random() * 0.28 - 0.05,
                    alpha: Math.random() * 0.7 + 0.2,
                    pulse: Math.random() * Math.PI * 2
                }));
            }

            function animate() {
                ctx.clearRect(0, 0, width, height);
                particles.forEach(p => {
                    p.x += p.vx;
                    p.y += p.vy;
                    p.pulse += 0.025;

                    if (p.y < -10) p.y = height + 10;
                    if (p.x < -10) p.x = width + 10;
                    if (p.x > width + 10) p.x = -10;

                    const currentAlpha = p.alpha * (0.65 + 0.35 * Math.sin(p.pulse));
                    ctx.beginPath();
                    ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
                    ctx.fillStyle = `rgba(243, 229, 171, ${currentAlpha})`;
                    ctx.fill();
                });
                requestAnimationFrame(animate);
            }

            window.addEventListener('resize', () => {
                resize();
                createParticles();
            });
            resize();
            createParticles();
            animate();
        }

        // Luxury Gold & Burgundy Confetti Burst
        function launchGoldConfetti() {
            const canvas = document.getElementById('confetti-canvas');
            const ctx = canvas.getContext('2d');
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;

            const colors = ['#d4af37', '#f3e5ab', '#591122', '#f5f2eb', '#9e7f20'];
            const pieces = Array.from({ length: 85 }, () => ({
                x: canvas.width / 2,
                y: canvas.height / 2,
                vx: (Math.random() - 0.5) * 14,
                vy: (Math.random() - 0.7) * 14,
                size: Math.random() * 7 + 4,
                color: colors[Math.floor(Math.random() * colors.length)],
                rot: Math.random() * 360,
                vRot: (Math.random() - 0.5) * 10
            }));

            let frame = 0;
            function step() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                pieces.forEach(p => {
                    p.x += p.vx;
                    p.y += p.vy;
                    p.vy += 0.28; // gravity
                    p.rot += p.vRot;

                    ctx.save();
                    ctx.translate(p.x, p.y);
                    ctx.rotate((p.rot * Math.PI) / 180);
                    ctx.fillStyle = p.color;
                    ctx.fillRect(-p.size / 2, -p.size / 2, p.size, p.size * 0.6);
                    ctx.restore();
                });
                frame++;
                if (frame < 130) {
                    requestAnimationFrame(step);
                } else {
                    ctx.clearRect(0, 0, canvas.width, canvas.height);
                }
            }
            step();
        }

        window.onload = function () {
            populateContent();
            initAmbientParticles();
        };
    </script>
</body>
</html>
