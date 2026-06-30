# will-you-go-out-with-me
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will You Go On A Date With Me? 💖</title>
    <style>
        :root {
            --bg-gradient: linear-gradient(145deg, #1f102a 0%, #4a154b 40%, #831a61 75%, #bd246b 100%);
            --card-bg: rgba(255, 255, 255, 0.08);
            --card-border: rgba(255, 255, 255, 0.15);
            --text-glow: 0 0 15px rgba(255, 182, 193, 0.6);
            --pink-accent: #ff6097;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Playfair Display', 'Didot', 'Georgia', 'Segoe UI', serif;
        }

        body {
            background: var(--bg-gradient);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        /* Floating Background Hearts */
        .hearts-bg {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
            top: 0;
            left: 0;
            z-index: 1;
            pointer-events: none;
        }

        .floating-heart {
            position: absolute;
            bottom: -10%;
            color: rgba(255, 96, 151, 0.25);
            font-size: 24px;
            animation: floatUp 10s infinite linear;
            text-shadow: 0 0 10px rgba(255, 96, 151, 0.4);
        }

        @keyframes floatUp {
            0% { transform: translateY(0) scale(0.8) rotate(0deg); opacity: 0; }
            10% { opacity: 0.7; }
            90% { opacity: 0.4; }
            100% { transform: translateY(-115vh) scale(1.2) rotate(360deg); opacity: 0; }
        }

        /* Premium Glassmorphism Container Card */
        .container {
            width: 90%;
            max-width: 440px;
            background: var(--card-bg);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid var(--card-border);
            border-radius: 28px;
            padding: 35px 25px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4), 0 0 40px rgba(255, 96, 151, 0.1);
            text-align: center;
            z-index: 2;
            position: relative;
            min-height: 560px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            transition: all 0.5s ease;
        }

        .step {
            display: none;
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.5s ease, transform 0.5s ease;
            flex-direction: column;
            height: 100%;
            justify-content: space-between;
        }

        .step.active {
            display: flex;
            opacity: 1;
            transform: translateY(0);
        }

        /* Typography */
        h1 {
            color: #fff9fb;
            font-size: 26px;
            font-weight: 400;
            margin-bottom: 6px;
            text-shadow: var(--text-glow);
            letter-spacing: 0.5px;
        }

        .subtitle {
            color: rgba(255, 192, 203, 0.7);
            font-size: 11px;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin-bottom: 25px;
            font-family: 'Segoe UI', sans-serif;
        }

        /* Custom Interactive Calendar System */
        .calendar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: #fff;
            margin-bottom: 15px;
            padding: 0 5px;
        }
        .calendar-header span {
            font-family: 'Segoe UI', sans-serif;
            font-weight: 600;
            font-size: 14px;
            letter-spacing: 1px;
        }
        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 6px;
            color: #fff;
            font-family: 'Segoe UI', sans-serif;
            font-size: 13px;
        }
        .day-name {
            color: rgba(255, 255, 255, 0.4);
            font-size: 11px;
            font-weight: bold;
            padding-bottom: 5px;
        }
        .day-number {
            height: 36px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        .day-number:hover:not(.empty) {
            background: rgba(255, 255, 255, 0.15);
        }
        .day-number.selected {
            background: var(--pink-accent) !important;
            box-shadow: 0 0 15px var(--pink-accent);
            font-weight: bold;
        }
        .day-number.empty { cursor: default; }

        /* Time Block Option Slots */
        .time-wrapper {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin: 10px 0;
        }
        .time-row {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            padding: 16px 20px;
            border-radius: 16px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.2s ease;
            color: #fff;
            font-family: 'Segoe UI', sans-serif;
        }
        .time-row .period-label {
            font-size: 15px;
            font-weight: 500;
        }
        .time-row .time-digits {
            opacity: 0.6;
            font-size: 13px;
        }
        .time-row:hover {
            background: rgba(255, 255, 255, 0.1);
            border-color: rgba(255, 255, 255, 0.2);
        }
        .time-row.selected {
            background: rgba(255, 96, 151, 0.2);
            border-color: var(--pink-accent);
            box-shadow: inset 0 0 10px rgba(255, 96, 151, 0.2);
        }

        /* Food Choice Grid Selection */
        .food-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin-bottom: 10px;
        }
        .food-item {
            background: rgba(255, 255, 255, 0.04);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 16px;
            padding: 16px 5px;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 6px;
        }
        .food-item .emoji { font-size: 26px; }
        .food-item .name {
            font-size: 11px;
            color: rgba(255, 255, 255, 0.7);
            font-family: 'Segoe UI', sans-serif;
            letter-spacing: 0.5px;
        }
        .food-item:hover {
            background: rgba(255, 255, 255, 0.08);
        }
        .food-item.selected {
            background: rgba(255, 96, 151, 0.15);
            border-color: var(--pink-accent);
            transform: scale(1.04);
        }
        .selection-breadcrumb {
            color: var(--pink-accent);
            font-size: 12px;
            font-family: 'Segoe UI', sans-serif;
            margin-top: 10px;
            min-height: 18px;
            font-style: italic;
        }

        /* Places to Visit Interactive List Options */
        .places-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
            max-height: 290px;
            overflow-y: auto;
            padding-right: 5px;
            margin-bottom: 5px;
        }
        .places-list::-webkit-scrollbar {
            width: 5px;
        }
        .places-list::-webkit-scrollbar-thumb {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 10px;
        }
        .place-item {
            background: rgba(255, 255, 255, 0.04);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 14px;
            padding: 12px 18px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 15px;
            transition: all 0.2s ease;
            color: #fff;
            text-align: left;
            font-family: 'Segoe UI', sans-serif;
        }
        .place-item .place-emoji { font-size: 20px; }
        .place-item .place-name { font-size: 14px; font-weight: 500; }
        .place-item:hover { background: rgba(255, 255, 255, 0.08); }
        .place-item.selected {
            background: rgba(255, 96, 151, 0.15);
            border-color: var(--pink-accent);
        }

        /* Buttons Styling */
        .btn-container {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-top: 20px;
        }
        .action-btn {
            background: #fff;
            color: #333;
            border: none;
            padding: 13px 32px;
            font-size: 14px;
            font-weight: 600;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: 'Segoe UI', sans-serif;
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }
        .action-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 24px rgba(255, 96, 151, 0.3);
            background: #fff9fb;
        }
        .btn-back {
            background: transparent;
            color: rgba(255, 255, 255, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: none;
        }
        .btn-back:hover {
            background: rgba(255, 255, 255, 0.05);
            color: #fff;
            border-color: rgba(255, 255, 255, 0.4);
            transform: none;
            box-shadow: none;
        }

        /* Receipt Box Output Styling */
        .summary-card {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 18px;
            padding: 18px;
            text-align: left;
            margin: 15px 0;
            border: 1px dashed rgba(255, 255, 255, 0.2);
            font-family: 'Segoe UI', sans-serif;
        }
        .summary-row { margin-bottom: 12px; }
        .summary-row:last-child { margin-bottom: 0; }
        .summary-head {
            font-size: 10px;
            text-transform: uppercase;
            color: rgba(255, 192, 203, 0.5);
            letter-spacing: 1.5px;
            margin-bottom: 2px;
        }
        .summary-body { font-size: 14px; color: #fff; font-weight: 400; white-space: pre-line; }
        .final-quote {
            font-style: italic;
            color: var(--pink-accent);
            margin: 12px 0;
            font-size: 14px;
            text-shadow: 0 0 10px rgba(255, 96, 151, 0.2);
        }
    </style>
</head>
<body>

    <!-- Aesthetic Decorative Heart Particle Engine Layout Canvas Layer -->
    <div class="hearts-bg" id="heartsBackground"></div>

    <div class="container">
        
        <!-- STEP 1: Invitation Question -->
        <div class="step active" id="step1">
            <div>
                <div style="font-size: 45px; margin-bottom: 15px; filter: drop-shadow(var(--text-glow));">🤍</div>
                <h1>Will you go on a date with me?</h1>
                <p class="subtitle">A question worth asking</p>
            </div>
            <div class="btn-container">
                <button class="action-btn" onclick="goToStep(2)">Yes</button>
                <button class="action-btn btn-back" id="evadeBtn" onmouseover="teleportButton()">No</button>
            </div>
        </div>

        <!-- STEP 2: The Calendar Picker -->
        <div class="step" id="step2">
            <div>
                <div style="font-size: 35px; margin-bottom: 10px;">📅</div>
                <h1>When are you free?</h1>
                <p class="subtitle">Pick a date</p>
                
                <div style="background: rgba(0,0,0,0.15); padding: 15px; border-radius: 20px; border: 1px solid rgba(255,255,255,0.05);">
                    <div class="calendar-header">
                        <span id="monthYearDisplay">JUNE 2026</span>
                    </div>
                    <div class="calendar-grid" id="calendarDays">
                        <div class="day-name">Su</div><div class="day-name">Mo</div><div class="day-name">Tu</div>
                        <div class="day-name">We</div><div class="day-name">Th</div><div class="day-name">Fr</div>
                        <div class="day-name">Sa</div>
                    </div>
                </div>
            </div>
            <div class="btn-container">
                <button class="action-btn" onclick="verifyDateSelection()">Next ✨</button>
            </div>
        </div>

        <!-- STEP 3: Time Slot Selector (Morning, Evening, Night) -->
        <div class="step" id="step3">
            <div>
                <div style="font-size: 35px; margin-bottom: 10px;">⏰</div>
                <h1>What time?</h1>
                <p class="subtitle">Choose your hour</p>
                
                <div class="time-wrapper">
                    <div class="time-row" onclick="bindTimeSelection(this, 'Morning', '10:30 AM')">
                        <span class="period-label">🌅 Morning</span>
                        <span class="time-digits">10:30 AM</span>
                    </div>
                    <div class="time-row" onclick="bindTimeSelection(this, 'Evening', '6:00 PM')">
                        <span class="period-label">🌆 Evening</span>
                        <span class="time-digits">6:00 PM</span>
                    </div>
                    <div class="time-row" onclick="bindTimeSelection(this, 'Night', '8:30 PM')">
                        <span class="period-label">🌃 Night</span>
                        <span class="time-digits">8:30 PM</span>
                    </div>
                </div>
            </div>
            <div class="btn-container">
                <button class="action-btn btn-back" onclick="goToStep(2)">Back</button>
                <button class="action-btn" onclick="verifyTimeSelection()">Next ✨</button>
            </div>
        </div>

        <!-- STEP 4: Food Preference Selector -->
        <div class="step" id="step4">
            <div>
                <div style="font-size: 35px; margin-bottom: 10px;">🍕</div>
                <h1>What are we feeling?</h1>
                <p class="subtitle">Pick one or more</p>
                
                <div class="food-grid">
                    <div class="food-item" onclick="bindFoodSelection(this, 'Sushi')">
                        <span class="emoji">🍣</span><span class="name">Sushi</span>
                    </div>
                    <div class="food-item" onclick="bindFoodSelection(this, 'Pasta')">
                        <span class="emoji">🍝</span><span class="name">Pasta</span>
                    </div>
                    <div class="food-item" onclick="bindFoodSelection(this, 'Pizza')">
                        <span class="emoji">🍕</span><span class="name">Pizza</span>
                    </div>
                    <div class="food-item" onclick="bindFoodSelection(this, 'Biryani')">
                        <span class="emoji">🍛</span><span class="name">Biryani</span>
                    </div>
                    <div class="food-item" onclick="bindFoodSelection(this, 'Burgers')">
                        <span class="emoji">🍔</span><span class="name">Burgers</span>
                    </div>
                    <div class="food-item" onclick="bindFoodSelection(this, 'Desserts')">
                        <span class="emoji">🍰</span><span class="name">Desserts</span>
                    </div>
                </div>
                <div class="selection-breadcrumb" id="foodBreadcrumb"></div>
            </div>
            <div class="btn-container">
                <button class="action-btn btn-back" onclick="goToStep(3)">Back</button>
                <button class="action-btn" onclick="verifyFoodSelection()">Next ✨</button>
            </div>
        </div>

        <!-- STEP 5: Places to Visit Option List -->
        <div class="step" id="step5">
            <div>
                <div style="font-size: 35px; margin-bottom: 10px;">🗺️</div>
                <h1>Where shall we go?</h1>
                <p class="subtitle">Pick an adventure spot</p>
                
                <div class="places-list">
                    <div class="place-item" onclick="bindPlaceSelection(this, 'Majnu-ka-tilla')">
                        <span class="place-emoji">🥢</span><span class="place-name">Majnu-ka-tilla</span>
                    </div>
                    <div class="place-item" onclick="bindPlaceSelection(this, 'Swaminarayan Akshardham')">
                        <span class="place-emoji">🛕</span><span class="place-name">Swaminarayan Akshardham</span>
                    </div>
                    <div class="place-item" onclick="bindPlaceSelection(this, 'Qutub Minar')">
                        <span class="place-emoji">🗼</span><span class="place-name">Qutub Minar</span>
                    </div>
                    <div class="place-item" onclick="bindPlaceSelection(this, 'Humayun\'s Tomb')">
                        <span class="place-emoji">🕌</span><span class="place-name">Humayun's Tomb</span>
                    </div>
                    <div class="place-item" onclick="bindPlaceSelection(this, 'Gurudwara Bangla Sahib')">
                        <span class="place-emoji">✨</span><span class="place-name">Gurudwara Bangla Sahib</span>
                    </div>
                    <div class="place-item" onclick="bindPlaceSelection(this, 'India Gate')">
                        <span class="place-emoji">🏛️</span><span class="place-name">India Gate</span>
                    </div>
                    <div class="place-item" onclick="bindPlaceSelection(this, 'Lodhi Garden')">
                        <span class="place-emoji">🌳</span><span class="place-name">Lodhi Garden</span>
                    </div>
                    <div class="place-item" onclick="bindPlaceSelection(this, 'Lotus Temple')">
                        <span class="place-emoji">🪷</span><span class="place-name">Lotus Temple</span>
                    </div>
                </div>
                <div class="selection-breadcrumb" id="placeBreadcrumb"></div>
            </div>
            <div class="btn-container">
                <button class="action-btn btn-back" onclick="goToStep(4)">Back</button>
                <button class="action-btn" onclick="verifyPlaceSelection()">Let's Go ✨</button>
            </div>
        </div>

        <!-- STEP 6: Final Confirmation Receipt Screen -->
        <div class="step" id="step6">
            <div>
                <div style="font-size: 45px; margin-bottom: 12px; filter: drop-shadow(0 0 10px rgba(255,96,151,0.5));">✨</div>
                <h1>It's a date.</h1>
                <p class="subtitle">Something wonderful awaits</p>
                
                <div class="summary-card">
                    <div class="summary-row">
                        <div class="summary-head">📍 When & Where</div>
                        <div class="summary-body" id="finalLocationText">Saturday, June 20 @ Lotus Temple</div>
                    </div>
                    <div class="summary-row">
                        <div class="summary-head">🍽️ What we're having</div>
                        <div class="summary-body" id="finalFoodText">Biryani & Desserts</div>
                    </div>
                </div>
                <p class="final-quote">"I can't wait to spend time with you ❤️"</p>
            </div>
            <div class="btn-container">
                <button class="action-btn" style="background: var(--pink-accent); color:#fff; box-shadow:0 10px 25px rgba(255,96,151,0.4);" onclick="triggerConfirmation()">Confirm Date 💌</button>
            </div>
        </div>

    </div>

    <script>
        // Trackers for current runtime parameters
        let selectedDayNumber = null;
        let selectedMonthIndex = 5; // Fixed mockup tracking for June
        let selectedYear = 2026;
        
        let appointmentData = {
            formattedDate: '',
            timeOfDay: '',
            exactHour: '',
            foodsList: [],
            selectedPlace: ''
        };

        // Inject data structure logic matching calendar views shown in WhatsApp Video 2026-06-23 at 10.24.12 AM.mp4
        function buildCalendarEngine() {
            const gridContainer = document.getElementById('calendarDays');
            const paddingSpaces = 1; 
            const totalDaysInMonth = 30;

            for(let i=0; i<paddingSpaces; i++) {
                let emptyCell = document.createElement('div');
                emptyCell.classList.add('day-number', 'empty');
                gridContainer.appendChild(emptyCell);
            }

            for(let day=1; day<=totalDaysInMonth; day++) {
                let dayCell = document.createElement('div');
                dayCell.classList.add('day-number');
                dayCell.innerText = day;
                dayCell.onclick = function() {
                    document.querySelectorAll('.day-number').forEach(el => el.classList.remove('selected'));
                    dayCell.classList.add('selected');
                    selectedDayNumber = day;
                };
                gridContainer.appendChild(dayCell);
            }
        }
        buildCalendarEngine();

        function goToStep(stepNumber) {
            document.querySelectorAll('.step').forEach(element => element.classList.remove('active'));
            document.getElementById(`step${stepNumber}`).classList.add('active');
        }

        function verifyDateSelection() {
            if(!selectedDayNumber) {
                alert("Please select a date from the calendar first! 💞");
                return;
            }
            const weekdayString = new Date(selectedYear, selectedMonthIndex, selectedDayNumber).toLocaleDateString('en-US', { weekday: 'long' });
            const monthString = new Date(selectedYear, selectedMonthIndex, selectedDayNumber).toLocaleDateString('en-US', { month: 'long' });
            appointmentData.formattedDate = `${weekdayString}, ${monthString} ${selectedDayNumber}`;
            goToStep(3);
        }

        function bindTimeSelection(element, dayPeriod, clockTime) {
            document.querySelectorAll('.time-row').forEach(row => row.classList.remove('selected'));
            element.classList.add('selected');
            appointmentData.timeOfDay = dayPeriod;
            appointmentData.exactHour = clockTime;
        }

        function verifyTimeSelection() {
            if(!appointmentData.timeOfDay) {
                alert("Please select your preferred time of day! ⏰");
                return;
            }
            goToStep(4);
        }

        function bindFoodSelection(element, designator) {
            element.classList.toggle('selected');
            const locationIndex = appointmentData.foodsList.indexOf(designator);
            if(locationIndex > -1) {
                appointmentData.foodsList.splice(locationIndex, 1);
            } else {
                appointmentData.foodsList.push(designator);
            }

            const breadcrumb = document.getElementById('foodBreadcrumb');
            if(appointmentData.foodsList.length > 0) {
                breadcrumb.innerText = appointmentData.foodsList.join(' + ') + " — delicious selection!";
            } else {
                breadcrumb.innerText = "";
            }
        }

        function verifyFoodSelection() {
            if(appointmentData.foodsList.length === 0) {
                alert("Please select at least one food option! 🍕");
                return;
            }
            goToStep(5);
        }

        function bindPlaceSelection(element, placeName) {
            document.querySelectorAll('.place-item').forEach(item => item.classList.remove('selected'));
            element.classList.add('selected');
            appointmentData.selectedPlace = placeName;
            document.getElementById('placeBreadcrumb').innerText = `${placeName} — sounds perfect! ✨`;
        }

        function verifyPlaceSelection() {
            if(!appointmentData.selectedPlace) {
                alert("Please select a place to visit! 🗺️");
                return;
            }
            compileReceiptSummary();
            goToStep(6);
        }

        function compileReceiptSummary() {
            document.getElementById('finalLocationText').innerText = `${appointmentData.formattedDate} @ ${appointmentData.exactHour} (${appointmentData.timeOfDay})\n📍 ${appointmentData.selectedPlace}`;
            document.getElementById('finalFoodText').innerText = appointmentData.foodsList.join(' & ');
        }

        // Teleports the "No" button systematically away from mouse hovering vectors
        function teleportButton() {
            const button = document.getElementById('evadeBtn');
            const safeWidthZone = window.innerWidth - button.offsetWidth - 40;
            const safeHeightZone = window.innerHeight - button.offsetHeight - 40;
            
            button.style.position = 'absolute';
            button.style.left = Math.max(20, Math.random() * safeWidthZone) + 'px';
            button.style.top = Math.max(20, Math.random() * safeHeightZone) + 'px';
        }

        // Floating ambient heart generator
        function startAestheticHeartEngine() {
            const container = document.getElementById('heartsBackground');
            const heartVariants = ['💖', '✨', '❤️', '🌸', '🪷'];
            
            setInterval(() => {
                const particle = document.createElement('div');
                particle.classList.add('floating-heart');
                particle.innerText = heartVariants[Math.floor(Math.random() * heartVariants.length)];
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDuration = (Math.random() * 4 + 7) + 's';
                particle.style.fontSize = (Math.random() * 16 + 16) + 'px';
                
                container.appendChild(particle);
                setTimeout(() => particle.remove(), 11000);
            }, 600);
        }
        startAestheticHeartEngine();

        function triggerConfirmation() {
            alert("✨ Date confirmed! Take a quick screenshot of this screen and share your perfect plan! 😉💕");
        }
    </script>
</body>
</html>
