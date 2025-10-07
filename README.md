<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>开心日历-摸鱼版</title>
    <link href="https://fonts.googleapis.com/css2?family=ZCOOL+KuaiLe&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'ZCOOL+KuaiLe', "Comic Sans MS", cursive;
        }
        body {
            background-color: #1a1a2e;
            padding: 10px;
        }
        .calendar-card {
            max-width: 170px; 
            margin: 0 auto;
            background-color: #252540;
            border-radius: 10px;
            padding: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.4);
        }
        .card-title {
            text-align: center;
            font-size: 16px;
            color: #e0c3fc;
            margin-bottom: 6px;
        }
        /* 2. 替换为CSS烟花彩带动画 */
        .celebration {
            text-align: center;
            font-size: 24px;
            margin: 10px 0;
            height: 40px; /* 固定高度，防止跳动 */
            position: relative;
            overflow: hidden;
        }
        .celebration span {
            display: inline-block;
            animation: confetti 3s infinite;
            color: transparent;
            text-shadow: 0 0 2px rgba(255,255,255,0.8);
        }
        .celebration span:nth-child(1) { animation-delay: 0s; color: #ff6b6b; }
        .celebration span:nth-child(2) { animation-delay: 0.2s; color: #4ecdc4; }
        .celebration span:nth-child(3) { animation-delay: 0.4s; color: #ffd166; }
        .celebration span:nth-child(4) { animation-delay: 0.6s; color: #6a0dad; }
        .celebration span:nth-child(5) { animation-delay: 0.8s; color: #06d6a0; }
        .celebration span:nth-child(6) { animation-delay: 1s; color: #118ab2; }
        .celebration span:nth-child(7) { animation-delay: 1.2s; color: #ef476f; }
        .celebration span:nth-child(8) { animation-delay: 1.4s; color: #ff8fa3; }
        @keyframes confetti {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-20px) rotate(720deg); opacity: 0; }
        }
        .remind-text {
            text-align: center;
            font-size: 11px;
            color: #a8c7ff;
            margin-bottom: 6px;
        }
        .time-section {
            text-align: center;
            margin-bottom: 6px;
        }
        .current-time {
            font-size: 20px;
            color: #76efff;
            text-shadow: 0 0 4px #76efff, 0 0 6px #4cc9f0;
            margin-bottom: 3px;
        }
        .current-date {
            font-size: 12px;
            color: #b0b0c8;
        }
        .greeting-text {
            text-align: center;
            font-size: 14px;
            color: #ffc8dd;
            margin-bottom: 6px;
        }
        .all-holidays-count {
            background-color: #2e2e4d;
            border-radius: 8px;
            padding: 6px;
            margin-bottom: 6px;
        }
        .count-title {
            font-size: 12px;
            color: #a8c7ff;
            text-align: center;
            margin-bottom: 4px;
        }
        .holiday-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 3px 0;
            border-bottom: 1px dashed #3d3d66;
        }
        .holiday-item:last-child {
            border-bottom: none;
        }
        .holiday-name {
            font-size: 11px;
            color: #e0c3fc;
        }
        .holiday-days {
            font-size: 11px;
            color: #76efff;
            font-weight: bold;
        }
        .warm-sentence {
            text-align: center;
            font-size: 12px;
            color: #ffc8dd;
            padding: 6px;
            background-color: #2e2e4d;
            border-radius: 8px;
        }
    </style>
</head>
<body>
    <div class="calendar-card">
        <h2 class="card-title">开心日历</h2>
        <!-- 1. 替换为CSS烟花彩带 -->
        <div class="celebration">
            <span>✦</span>
            <span>❀</span>
            <span>✧</span>
            <span>★</span>
            <span>✽</span>
            <span>❃</span>
            <span>✺</span>
            <span>✻</span>
        </div>
        <div class="remind-text">精彩瞬间，值得期待～</div>
        <div class="time-section">
            <div class="current-time" id="currentTime"></div>
            <div class="current-date" id="currentDate"></div>
        </div>
        <div class="greeting-text" id="greetingText"></div>
        <div class="all-holidays-count">
            <div class="count-title">2026年法定节假日倒计时</div>
            <div class="holiday-item">
                <div class="holiday-name">元旦</div>
                <div class="holiday-days" id="dayNewYear"></div>
            </div>
            <div class="holiday-item">
                <div class="holiday-name">春节</div>
                <div class="holiday-days" id="daySpringFestival"></div>
            </div>
            <div class="holiday-item">
                <div class="holiday-name">清明节</div>
                <div class="holiday-days" id="dayQingming"></div>
            </div>
            <div class="holiday-item">
                <div class="holiday-name">劳动节</div>
                <div class="holiday-days" id="dayLaborDay"></div>
            </div>
            <div class="holiday-item">
                <div class="holiday-name">端午节</div>
                <div class="holiday-days" id="dayDragonBoat"></div>
            </div>
            <div class="holiday-item">
                <div class="holiday-name">中秋节</div>
                <div class="holiday-days" id="dayMidAutumn"></div>
            </div>
            <div class="holiday-item">
                <div class="holiday-name">国庆节</div>
                <div class="holiday-days" id="dayNationalDay"></div>
            </div>
        </div>
        <div class="warm-sentence" id="warmSentence"></div>
    </div>

    <script>
        // 实时时间
        function updateTimeDate() {
            const now = new Date();
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            const seconds = String(now.getSeconds()).padStart(2, '0');
            document.getElementById('currentTime').textContent = `${hours}:${minutes}:${seconds}`;
            
            const year = now.getFullYear();
            const month = String(now.getMonth() + 1).padStart(2, '0');
            const day = String(now.getDate()).padStart(2, '0');
            const week = ['周日','周一','周二','周三','周四','周五','周六'][now.getDay()];
            document.getElementById('currentDate').textContent = `${year}-${month}-${day} ${week}`;
        }
        updateTimeDate();
        setInterval(updateTimeDate, 1000);

        // 时段问候
        function setGreeting() {
            const hour = new Date().getHours();
            const text = hour >=6 && hour<12 ? '早上好呀～' : 
                        hour>=12&&hour<18 ? '中午好呀～' : '晚上好呀～';
            document.getElementById('greetingText').textContent = text;
        }
        setGreeting();
        setInterval(setGreeting, 3600000);

        // 节假日倒计时
        function calculateDays(targetDate) {
            const now = new Date();
            let target = new Date(targetDate);
            target.setHours(23, 59, 59);
            
            if (target < now) {
                target.setFullYear(now.getFullYear() + 1);
            }
            
            const timeDiff = target - now;
            return Math.ceil(timeDiff / (1000 * 60 * 60 * 24));
        }

        const holidays = {
            newYear: new Date(2026, 0, 1),
            springFestival: new Date(2026, 1, 17),
            qingming: new Date(2026, 3, 4),
            laborDay: new Date(2026, 4, 1),
            dragonBoat: new Date(2026, 5, 19),
            midAutumn: new Date(2026, 8, 25),
            nationalDay: new Date(2026, 9, 1)
        };

        function updateAllHolidayDays() {
            document.getElementById('dayNewYear').textContent = `${calculateDays(holidays.newYear)} 天`;
            document.getElementById('daySpringFestival').textContent = `${calculateDays(holidays.springFestival)} 天`;
            document.getElementById('dayQingming').textContent = `${calculateDays(holidays.qingming)} 天`;
            document.getElementById('dayLaborDay').textContent = `${calculateDays(holidays.laborDay)} 天`;
            document.getElementById('dayDragonBoat').textContent = `${calculateDays(holidays.dragonBoat)} 天`;
            document.getElementById('dayMidAutumn').textContent = `${calculateDays(holidays.midAutumn)} 天`;
            document.getElementById('dayNationalDay').textContent = `${calculateDays(holidays.nationalDay)} 天`;
        }
        updateAllHolidayDays();
        setInterval(updateAllHolidayDays, 86400000);

        // 温馨话语
        const sentences = [
            '累了就歇会儿，休息是为了更好出发～',
            '今天的努力不会白费，坚持下去呀～',
            '生活需要小确幸，记得给自己多些鼓励～',
            '偶尔放慢脚步也没关系，明天继续向前～',
            '每一点付出都有意义，你真的很棒呀～',
            '别忘记喝水，照顾好自己才能更有力量～',
            '今天也在认真生活，为这样的你点赞～',
            '眼睛累了就远眺，让身心一起放个假～',
            '努力的同时别焦虑，你已经在慢慢变好～',
            '生活虽忙，也要留一点时间给自己～',
            '哪怕进步一点点，也是值得开心的事～',
            '累了就深呼吸，调整状态再继续加油～'
        ];
        function setRandomSentence() {
            const randomIdx = Math.floor(Math.random() * sentences.length);
            document.getElementById('warmSentence').textContent = sentences[randomIdx];
        }
        setRandomSentence();
        setInterval(setRandomSentence, 30000);
    </script>
</body>
</html>
