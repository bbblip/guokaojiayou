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
            padding: 10px; /* 缩小页面外边距 */
        }
        /* 核心：容器宽度缩小到原页面1/2以下，原380px→170px */
        .calendar-card {
            max-width: 170px; 
            margin: 0 auto;
            background-color: #252540;
            border-radius: 10px; /* 按比例缩小圆角 */
            padding: 10px; /* 缩小内边距 */
            box-shadow: 0 4px 10px rgba(0,0,0,0.4); /* 按比例缩小阴影 */
        }
        .card-title {
            text-align: center;
            font-size: 16px; /* 缩小字体 */
            color: #e0c3fc;
            margin-bottom: 6px; /* 缩小间距 */
        }
        .fish-stick-gif {
            text-align: center;
            margin-bottom: 4px; /* 缩小间距 */
        }
        .fish-stick-gif img {
            width: 50px; /* 图片缩小到原1/2以下 */
            height: auto;
            border-radius: 6px; /* 按比例缩小圆角 */
            box-shadow: 0 2px 4px rgba(0,0,0,0.2);
        }
        .remind-text {
            text-align: center;
            font-size: 11px; /* 缩小字体 */
            color: #a8c7ff;
            margin-bottom: 8px; /* 缩小间距 */
        }
        .time-section {
            text-align: center;
            margin-bottom: 8px; /* 缩小间距 */
        }
        .current-time {
            font-size: 20px; /* 缩小字体 */
            color: #76efff;
            text-shadow: 0 0 4px #76efff, 0 0 6px #4cc9f0;
            margin-bottom: 3px; /* 缩小间距 */
        }
        .current-date {
            font-size: 12px; /* 缩小字体 */
            color: #b0b0c8;
        }
        .greeting-text {
            text-align: center;
            font-size: 14px; /* 缩小字体 */
            color: #ffc8dd;
            margin-bottom: 6px; /* 缩小间距 */
        }
        .rest-advice {
            background-color: #2e2e4d;
            border-radius: 8px; /* 按比例缩小圆角 */
            padding: 8px; /* 缩小内边距 */
            margin-bottom: 8px; /* 缩小间距 */
        }
        .rest-advice p {
            font-size: 10px; /* 缩小字体 */
            color: #e0e0e8;
            text-align: center;
            line-height: 1.4;
            margin: 2px 0; /* 缩小间距 */
        }
        .all-holidays-count {
            background-color: #2e2e4d;
            border-radius: 8px; /* 按比例缩小圆角 */
            padding: 8px; /* 缩小内边距 */
            margin-bottom: 8px; /* 缩小间距 */
        }
        .count-title {
            font-size: 12px; /* 缩小字体 */
            color: #a8c7ff;
            text-align: center;
            margin-bottom: 6px; /* 缩小间距 */
        }
        .holiday-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 4px 0; /* 缩小间距 */
            border-bottom: 1px dashed #3d3d66;
        }
        .holiday-item:last-child {
            border-bottom: none;
        }
        .holiday-name {
            font-size: 11px; /* 缩小字体 */
            color: #e0c3fc;
        }
        .holiday-days {
            font-size: 11px; /* 缩小字体 */
            color: #76efff;
            font-weight: bold;
        }
        .warm-sentence {
            text-align: center;
            font-size: 12px; /* 缩小字体 */
            color: #ffc8dd;
            padding: 8px; /* 缩小内边距 */
            background-color: #2e2e4d;
            border-radius: 8px; /* 按比例缩小圆角 */
        }
    </style>
</head>
<body>
    <div class="calendar-card">
        <h2 class="card-title">开心日历</h2>
        <div class="fish-stick-gif">
            < img src="https://media.giphy.com/media/3ohs7R4xM7g8QdK4wo/giphy.gif" alt="摸鱼棒动图">
        </div>
        <div class="remind-text">[摸鱼棒] 已就位，记得休息～</div>
        <div class="time-section">
            <div class="current-time" id="currentTime"></div>
            <div class="current-date" id="currentDate"></div>
        </div>
        <div class="greeting-text" id="greetingText"></div>
        <div class="rest-advice">
            <p>摸鱼人，工作再忙别硬扛～</p >
            <p>起身去茶水间，或廊道走一走呀～</p >
        </div>
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

        // 计算天数
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

        // 节日日期
        const holidays = {
            newYear: new Date(2026, 0, 1),
            springFestival: new Date(2026, 1, 17),
            qingming: new Date(2026, 3, 4),
            laborDay: new Date(2026, 4, 1),
            dragonBoat: new Date(2026, 5, 19),
            midAutumn: new Date(2026, 8, 25),
            nationalDay: new Date(2026, 9, 1)
        };

        // 更新倒计时
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

        // 随机温馨句子
        const sentences = [
            '摸鱼棒在手，快乐我有～',
            '努力很重要，休息也必要呀～',
            '今天摸5分钟，明天效率冲～',
            '久坐会累，起来活动下再继续吧～'
        ];
        function setRandomSentence() {
            const randomIdx = Math.floor(Math.random() * sentences.length);
            document.getElementById('warmSentence').textContent = sentences[randomIdx];
        }
        setRandomSentence();
        setInterval(setRandomSentence, 1800000);
    </script>
</body>
</html>
