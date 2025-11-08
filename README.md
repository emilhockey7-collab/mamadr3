<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Приглашение на юбилей 50 лет</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 25%, #f093fb 50%, #4facfe 75%, #00f2fe 100%);
            background-size: 400% 400%;
            animation: gradientShift 15s ease infinite;
            min-height: 100vh;
            overflow-x: hidden;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
        }

        .invitation-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 30px;
            padding: 40px;
            margin: 40px auto;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.3);
            position: relative;
            overflow: hidden;
            animation: fadeInUp 1s ease-out;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .invitation-card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255, 215, 0, 0.1), transparent);
            animation: shine 3s infinite;
        }

        @keyframes shine {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .header-image {
            text-align: center;
            margin-bottom: 30px;
            position: relative;
            z-index: 1;
        }

        .header-image img {
            max-width: 250px;
            width: 100%;
            height: auto;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }

        .golden-number {
            font-size: 120px;
            font-weight: bold;
            background: linear-gradient(135deg, #f9d423 0%, #ff4e50 100%);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            text-align: center;
            line-height: 1;
            margin: 20px 0;
            animation: pulse 2s ease-in-out infinite;
            text-shadow: 0 5px 15px rgba(255, 215, 0, 0.3);
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .subtitle {
            text-align: center;
            font-size: 24px;
            color: #667eea;
            margin-bottom: 30px;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .invitation-text {
            font-size: 20px;
            line-height: 1.8;
            color: #333;
            text-align: center;
            margin-bottom: 30px;
            position: relative;
            z-index: 1;
        }

        .invitation-text strong {
            color: #764ba2;
            font-size: 24px;
        }

        .details-box {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            border-radius: 20px;
            margin: 30px 0;
            box-shadow: 0 15px 35px rgba(102, 126, 234, 0.4);
            position: relative;
            z-index: 1;
            animation: slideIn 1s ease-out 0.5s both;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateX(-50px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .detail-item {
            display: flex;
            align-items: center;
            margin: 15px 0;
            font-size: 18px;
        }

        .detail-icon {
            width: 40px;
            height: 40px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            font-size: 20px;
        }

        .map-container {
            margin-top: 40px;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            height: 400px;
            position: relative;
            z-index: 1;
            animation: fadeIn 1s ease-out 1s both;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        #map {
            height: 100%;
            width: 100%;
        }

        .decorative-elements {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            pointer-events: none;
            overflow: hidden;
        }

        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background: #f9d423;
            animation: fall linear infinite;
        }

        @keyframes fall {
            to {
                transform: translateY(100vh) rotate(360deg);
            }
        }

        .confetti:nth-child(1) { left: 10%; animation-duration: 3s; background: #ff4e50; }
        .confetti:nth-child(2) { left: 20%; animation-duration: 4s; background: #667eea; }
        .confetti:nth-child(3) { left: 30%; animation-duration: 3.5s; background: #f093fb; }
        .confetti:nth-child(4) { left: 40%; animation-duration: 4.5s; background: #4facfe; }
        .confetti:nth-child(5) { left: 50%; animation-duration: 3s; background: #00f2fe; }
        .confetti:nth-child(6) { left: 60%; animation-duration: 4s; background: #f9d423; }
        .confetti:nth-child(7) { left: 70%; animation-duration: 3.5s; background: #ff4e50; }
        .confetti:nth-child(8) { left: 80%; animation-duration: 4.5s; background: #667eea; }
        .confetti:nth-child(9) { left: 90%; animation-duration: 3s; background: #764ba2; }

        .footer-text {
            text-align: center;
            margin-top: 30px;
            font-size: 18px;
            color: #333;
            font-style: italic;
            position: relative;
            z-index: 1;
        }

        @media (max-width: 768px) {
            .invitation-card {
                padding: 25px;
                margin: 20px auto;
            }

            .golden-number {
                font-size: 80px;
            }

            .subtitle {
                font-size: 20px;
            }

            .invitation-text {
                font-size: 18px;
            }

            .details-box {
                padding: 20px;
            }

            .detail-item {
                font-size: 16px;
            }

            .map-container {
                height: 300px;
            }

            .header-image img {
                max-width: 200px;
            }
        }

        @media (max-width: 480px) {
            .golden-number {
                font-size: 60px;
            }

            .subtitle {
                font-size: 18px;
            }

            .invitation-text {
                font-size: 16px;
            }
        }
    </style>
</head>
<body>
    <div class="decorative-elements">
        <div class="confetti"></div>
        <div class="confetti"></div>
        <div class="confetti"></div>
        <div class="confetti"></div>
        <div class="confetti"></div>
        <div class="confetti"></div>
        <div class="confetti"></div>
        <div class="confetti"></div>
        <div class="confetti"></div>
    </div>

    <div class="container">
        <div class="invitation-card">
            <div class="header-image">
                <img src="https://storage.yandexcloud.net/testegetutor/ChatGPT%20Image%20Nov%208%2C%202025%2C%2007_20_45%20PM.png" alt="Юбиляр">
            </div>

            <div class="golden-number">50</div>
            <div class="subtitle">🎉 Юбилейное торжество 🎉</div>

            <div class="invitation-text">
                <strong>13 декабря 2025 года</strong><br><br>
                У меня есть прекрасный повод провести несколько незабываемых часов в кругу самых дорогих и близких мне людей!<br><br>
                С огромной радостью приглашаю Вас на торжественное празднование моего <strong>50-летнего Юбилея!</strong><br><br>
                Буду счастлив разделить этот особенный день с Вами!
            </div>

            <div class="details-box">
                <div class="detail-item">
                    <div class="detail-icon">📅</div>
                    <div><strong>Дата:</strong> 13 декабря 2025 года (суббота)</div>
                </div>
                <div class="detail-item">
                    <div class="detail-icon">⏰</div>
                    <div><strong>Время:</strong> Начало в 17:00</div>
                </div>
                <div class="detail-item">
                    <div class="detail-icon">📍</div>
                    <div><strong>Место:</strong> Кафе «Девон»<br>пгт. Джалиль, ул. 30 лет Победы, 4<br>Сармановский район, Республика Татарстан</div>
                </div>
            </div>

            <div class="map-container">
                <div id="map"></div>
            </div>

            <div class="footer-text">
                ✨ Ваше присутствие — лучший подарок! ✨<br>
                С нетерпением жду встречи!
            </div>
        </div>
    </div>

    <script>
        // Инициализация карты
        const map = L.map('map').setView([55.0267, 52.737104], 15);

        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '© OpenStreetMap contributors'
        }).addTo(map);

        // Добавление маркера
        const marker = L.marker([55.0267, 52.737104]).addTo(map);
        marker.bindPopup('<b>Кафе "Девон"</b><br>ул. 30 лет Победы, 4<br>пгт. Джалиль').openPopup();

        // Дополнительная анимация для конфетти
        const confettiElements = document.querySelectorAll('.confetti');
        confettiElements.forEach((el, i) => {
            el.style.animationDelay = `${i * 0.3}s`;
        });
    </script>
</body>
</html>
