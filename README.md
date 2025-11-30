<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Калькулятор материалов для ремонта</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #e0e0e0;
            background-color: #293147;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background-color: #1e2430;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
        }

        h1 {
            color: #ffffff;
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .subtitle {
            color: #a0a0a0;
            font-size: 1.2em;
        }

        .calculators-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 20px;
        }

        .calculator {
            background-color: #1e2430;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            transition: transform 0.3s ease;
        }

        .calculator:hover {
            transform: translateY(-5px);
        }

        .calculator h3 {
            color: #ffffff;
            margin-bottom: 20px;
            font-size: 1.4em;
            border-bottom: 2px solid #293147;
            padding-bottom: 10px;
        }

        .input-group {
            margin-bottom: 15px;
        }

        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #c0c0c0;
        }

        .input-group input,
        .input-group select {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #293147;
            border-radius: 6px;
            font-size: 16px;
            background-color: #293147;
            color: #e0e0e0;
            transition: all 0.3s ease;
        }

        .input-group input:focus,
        .input-group select:focus {
            outline: none;
            border-color: #5d4e6d;
            box-shadow: 0 0 0 2px rgba(93, 78, 109, 0.3);
        }

        button {
            background-color: #293147;
            color: white;
            border: none;
            padding: 14px 25px;
            border-radius: 6px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 10px;
            width: 100%;
        }

        button:hover {
            background-color: #3a435e;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        .result {
            margin-top: 20px;
            padding: 15px;
            border-radius: 6px;
            display: none;
        }

        .success {
            background-color: #293147;
            border: 1px solid #3a435e;
            color: #e0e0e0;
            display: block;
        }

        .error {
            background-color: #3a1a1a;
            border: 1px solid #5a2d2d;
            color: #e0c0c0;
            display: block;
        }

        .success strong {
            color: #ffffff;
            font-size: 1.1em;
        }

        footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            color: #a0a0a0;
            font-size: 0.9em;
        }

        /* Адаптивность для мобильных */
        @media (max-width: 768px) {
            .calculators-grid {
                grid-template-columns: 1fr;
            }
            
            .container {
                padding: 10px;
            }
            
            h1 {
                font-size: 2em;
            }
            
            .calculator {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Калькулятор материалов для ремонта</h1>
            <p class="subtitle">Рассчитайте необходимое количество материалов для вашего проекта</p>
        </header>
        
        <div class="calculators-grid">
            <!-- Калькулятор обоев -->
            <div class="calculator">
                <h3>Калькулятор обоев</h3>
                
                <div class="input-group">
                    <label for="wall-length">Длина комнаты (м):</label>
                    <input type="number" id="wall-length" step="0.1" placeholder="4.5" value="4.5">
                </div>
                
                <div class="input-group">
                    <label for="wall-width">Ширина комнаты (м):</label>
                    <input type="number" id="wall-width" step="0.1" placeholder="3.2" value="3.2">
                </div>
                
                <div class="input-group">
                    <label for="wall-height">Высота потолков (м):</label>
                    <input type="number" id="wall-height" step="0.1" placeholder="2.7" value="2.7">
                </div>
                
                <div class="input-group">
                    <label for="windows-count">Количество окон:</label>
                    <input type="number" id="windows-count" value="1" min="0">
                </div>
                
                <div class="input-group">
                    <label for="doors-count">Количество дверей:</label>
                    <input type="number" id="doors-count" value="1" min="0">
                </div>
                
                <div class="input-group">
                    <label for="wallpaper-type">Тип обоев:</label>
                    <select id="wallpaper-type">
                        <option value="1.1">Обычные (10% запас)</option>
                        <option value="1.15">С крупным рисунком (15% запас)</option>
                    </select>
                </div>
                
                <button onclick="calculateWallpaper()">Рассчитать обои</button>
                <div id="wallpaper-result" class="result"></div>
            </div>

            <!-- Калькулятор плитки -->
            <div class="calculator">
                <h3>Калькулятор плитки</h3>
                
                <div class="input-group">
                    <label for="tile-length">Длина помещения (м):</label>
                    <input type="number" id="tile-length" step="0.1" placeholder="3.0" value="3.0">
                </div>
                
                <div class="input-group">
                    <label for="tile-width">Ширина помещения (м):</label>
                    <input type="number" id="tile-width" step="0.1" placeholder="2.5" value="2.5">
                </div>
                
                <div class="input-group">
                    <label for="tile-tile-length">Длина плитки (см):</label>
                    <input type="number" id="tile-tile-length" value="30" step="0.1">
                </div>
                
                <div class="input-group">
                    <label for="tile-tile-width">Ширина плитки (см):</label>
                    <input type="number" id="tile-tile-width" value="30" step="0.1">
                </div>
                
                <div class="input-group">
                    <label for="tile-laying-type">Способ укладки:</label>
                    <select id="tile-laying-type">
                        <option value="1.1">Прямая (10% запас)</option>
                        <option value="1.15">Диагональная (15% запас)</option>
                    </select>
                </div>
                
                <button onclick="calculateTile()">Рассчитать плитку</button>
                <div id="tile-result" class="result"></div>
            </div>

            <!-- Калькулятор краски -->
            <div class="calculator">
                <h3>Калькулятор краски</h3>
                
                <div class="input-group">
                    <label for="paint-length">Длина комнаты (м):</label>
                    <input type="number" id="paint-length" step="0.1" placeholder="4.5" value="4.5">
                </div>
                
                <div class="input-group">
                    <label for="paint-width">Ширина комнаты (м):</label>
                    <input type="number" id="paint-width" step="0.1" placeholder="3.2" value="3.2">
                </div>
                
                <div class="input-group">
                    <label for="paint-height">Высота потолков (м):</label>
                    <input type="number" id="paint-height" step="0.1" placeholder="2.7" value="2.7">
                </div>
                
                <div class="input-group">
                    <label for="paint-windows">Количество окон:</label>
                    <input type="number" id="paint-windows" value="1" min="0">
                </div>
                
                <div class="input-group">
                    <label for="paint-doors">Количество дверей:</label>
                    <input type="number" id="paint-doors" value="1" min="0">
                </div>
                
                <div class="input-group">
                    <label for="paint-consumption">Расход краски (л/кв.м):</label>
                    <input type="number" id="paint-consumption" value="0.12" step="0.01">
                </div>
                
                <div class="input-group">
                    <label for="paint-coats">Количество слоев:</label>
                    <input type="number" id="paint-coats" value="2" min="1">
                </div>
                
                <button onclick="calculatePaint()">Рассчитать краску</button>
                <div id="paint-result" class="result"></div>
            </div>

            <!-- Калькулятор ламината -->
            <div class="calculator">
                <h3>Калькулятор ламината</h3>
                
                <div class="input-group">
                    <label for="laminate-length">Длина комнаты (м):</label>
                    <input type="number" id="laminate-length" step="0.1" placeholder="4.5" value="4.5">
                </div>
                
                <div class="input-group">
                    <label for="laminate-width">Ширина комнаты (м):</label>
                    <input type="number" id="laminate-width" step="0.1" placeholder="3.2" value="3.2">
                </div>
                
                <div class="input-group">
                    <label for="laminate-pack-area">Площадь в упаковке (кв.м):</label>
                    <input type="number" id="laminate-pack-area" value="2.5" step="0.1">
                </div>
                
                <div class="input-group">
                    <label for="laminate-laying">Способ укладки:</label>
                    <select id="laminate-laying">
                        <option value="1.05">Экономная (5% запас)</option>
                        <option value="1.1" selected>Классическая (10% запас)</option>
                        <option value="1.15">Диагональная (15% запас)</option>
                    </select>
                </div>
                
                <button onclick="calculateLaminate()">Рассчитать ламинат</button>
                <div id="laminate-result" class="result"></div>
            </div>
        </div>
        
        <footer>
            <p>Калькулятор материалов для ремонта &copy; 2025 | Все расчеты приблизительные</p>
        </footer>
    </div>

    <script>
        // Калькулятор обоев
        function calculateWallpaper() {
            const length = parseFloat(document.getElementById('wall-length').value);
            const width = parseFloat(document.getElementById('wall-width').value);
            const height = parseFloat(document.getElementById('wall-height').value);
            const windows = parseInt(document.getElementById('windows-count').value) || 0;
            const doors = parseInt(document.getElementById('doors-count').value) || 0;
            const wallpaperType = parseFloat(document.getElementById('wallpaper-type').value);
            const resultDiv = document.getElementById('wallpaper-result');

            // Проверка введенных данных
            if (!length || !width || !height) {
                resultDiv.innerHTML = '<div class="error">❌ Заполните длину, ширину и высоту комнаты!</div>';
                resultDiv.className = 'result error';
                resultDiv.style.display = 'block';
                return;
            }

            // Расчет по формуле технолога
            const perimeter = (length + width) * 2;
            const totalWallArea = perimeter * height;
            
            // Площадь проемов (стандартные размеры)
            const windowArea = windows * (1.2 * 1.5); // стандартное окно 1.2x1.5 м
            const doorArea = doors * (2.0 * 0.8);     // стандартная дверь 2.0x0.8 м
            
            // Полезная площадь для оклейки
            const effectiveArea = totalWallArea - windowArea - doorArea;
            
            // Стандартный рулон 0.53x10 м
            const rollArea = 0.53 * 10;
            
            // Количество рулонов с учетом запаса
            let rolls = Math.ceil(effectiveArea / rollArea * wallpaperType);

            // Вывод результата
            resultDiv.innerHTML = `
                <div class="success">
                    <strong>Результат расчета обоев:</strong><br><br>
                    • Общая площадь стен: <strong>${totalWallArea.toFixed(1)} кв.м</strong><br>
                    • Площадь проемов: <strong>${(windowArea + doorArea).toFixed(1)} кв.м</strong><br>
                    • Полезная площадь: <strong>${effectiveArea.toFixed(1)} кв.м</strong><br>
                    • Необходимое количество рулонов: <strong style="color: #90ee90; font-size: 1.2em;">${rolls} шт.</strong><br><br>
                    Рекомендация: Покупайте рулоны из одной партии.
                </div>
            `;
            resultDiv.className = 'result success';
            resultDiv.style.display = 'block';
        }

        // Калькулятор плитки
        function calculateTile() {
            const roomLength = parseFloat(document.getElementById('tile-length').value);
            const roomWidth = parseFloat(document.getElementById('tile-width').value);
            const tileLength = parseFloat(document.getElementById('tile-tile-length').value) / 100; // переводим в метры
            const tileWidth = parseFloat(document.getElementById('tile-tile-width').value) / 100;   // переводим в метры
            const layingType = parseFloat(document.getElementById('tile-laying-type').value);
            const resultDiv = document.getElementById('tile-result');

            // Проверка введенных данных
            if (!roomLength || !roomWidth || !tileLength || !tileWidth) {
                resultDiv.innerHTML = '<div class="error">❌ Заполните все поля!</div>';
                resultDiv.className = 'result error';
                resultDiv.style.display = 'block';
                return;
            }

            // Расчет по формуле технолога
            const roomArea = roomLength * roomWidth;
            const tileArea = tileLength * tileWidth;
            const tilesWithoutWaste = roomArea / tileArea;
            const tilesWithWaste = Math.ceil(tilesWithoutWaste * layingType);
            const totalArea = tilesWithWaste * tileArea;

            // Вывод результата
            resultDiv.innerHTML = `
                <div class="success">
                    <strong>Результат расчета плитки:</strong><br><br>
                    • Площадь помещения: <strong>${roomArea.toFixed(2)} кв.м</strong><br>
                    • Площадь одной плитки: <strong>${tileArea.toFixed(3)} кв.м</strong><br>
                    • Количество плиток: <strong style="color: #90ee90; font-size: 1.2em;">${tilesWithWaste} шт.</strong><br>
                    • Общая площадь с запасом: <strong>${totalArea.toFixed(2)} кв.м</strong><br><br>
                    Рекомендация: Не забудьте приобрести затирку для швов.
                </div>
            `;
            resultDiv.className = 'result success';
            resultDiv.style.display = 'block';
        }

        // Калькулятор краски
        function calculatePaint() {
            const length = parseFloat(document.getElementById('paint-length').value);
            const width = parseFloat(document.getElementById('paint-width').value);
            const height = parseFloat(document.getElementById('paint-height').value);
            const windows = parseInt(document.getElementById('paint-windows').value) || 0;
            const doors = parseInt(document.getElementById('paint-doors').value) || 0;
            const consumption = parseFloat(document.getElementById('paint-consumption').value);
            const coats = parseInt(document.getElementById('paint-coats').value);
            const resultDiv = document.getElementById('paint-result');

            // Проверка введенных данных
            if (!length || !width || !height || !consumption || !coats) {
                resultDiv.innerHTML = '<div class="error">❌ Заполните все поля!</div>';
                resultDiv.className = 'result error';
                resultDiv.style.display = 'block';
                return;
            }

            // Расчет по формуле технолога
            const perimeter = (length + width) * 2;
            const totalWallArea = perimeter * height;
            
            // Площадь проемов
            const windowArea = windows * (1.2 * 1.5);
            const doorArea = doors * (2.0 * 0.8);
            
            // Полезная площадь для окрашивания
            const effectiveArea = totalWallArea - windowArea - doorArea;
            
            // Расход краски с запасом 10%
            const paintNeeded = effectiveArea * consumption * coats * 1.1;
            const cans = Math.ceil(paintNeeded / 2.5); // банка 2.5 л

            // Вывод результата
            resultDiv.innerHTML = `
                <div class="success">
                    <strong>Результат расчета краски:</strong><br><br>
                    • Площадь окрашивания: <strong>${effectiveArea.toFixed(1)} кв.м</strong><br>
                    • Необходимо краски: <strong style="color: #90ee90; font-size: 1.2em;">${paintNeeded.toFixed(2)} л</strong><br>
                    • Количество банок (2.5 л): <strong>${cans} шт.</strong><br><br>
                    Рекомендация: Краску тщательно перемешивайте перед использованием.
                </div>
            `;
            resultDiv.className = 'result success';
            resultDiv.style.display = 'block';
        }

        // Калькулятор ламината
        function calculateLaminate() {
            const length = parseFloat(document.getElementById('laminate-length').value);
            const width = parseFloat(document.getElementById('laminate-width').value);
            const packArea = parseFloat(document.getElementById('laminate-pack-area').value);
            const wasteFactor = parseFloat(document.getElementById('laminate-laying').value);
            const resultDiv = document.getElementById('laminate-result');

            // Проверка введенных данных
            if (!length || !width || !packArea) {
                resultDiv.innerHTML = '<div class="error">❌ Заполните все поля!</div>';
                resultDiv.className = 'result error';
                resultDiv.style.display = 'block';
                return;
            }

            // Расчет по формуле технолога
            const roomArea = length * width;
            const totalAreaNeeded = roomArea * wasteFactor;
            const packsNeeded = Math.ceil(totalAreaNeeded / packArea);

            // Вывод результата
            resultDiv.innerHTML = `
                <div class="success">
                    <strong>Результат расчета ламината:</strong><br><br>
                    • Площадь комнаты: <strong>${roomArea.toFixed(2)} кв.м</strong><br>
                    • Необходимое количество упаковок: <strong style="color: #90ee90; font-size: 1.2em;">${packsNeeded} шт.</strong><br>
                    • Общая площадь с запасом: <strong>${totalAreaNeeded.toFixed(2)} кв.м</strong><br><br>
                    Рекомендация: Перед укладкой дайте ламинату акклиматизироваться 48 часов.
                </div>
            `;
            resultDiv.className = 'result success';
            resultDiv.style.display = 'block';
        }
    </script>
</body>
</html>
