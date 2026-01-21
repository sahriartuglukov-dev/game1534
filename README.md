<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Академия Героев: REBORN</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Exo+2:wght@400;600;800&display=swap');

        :root {
            --glass: rgba(13, 17, 23, 0.85);
            --glass-hover: rgba(20, 30, 45, 0.95);
            --accent: #00f2ff;
            --danger: #ff003c;
            --success: #00ff9d;
            --gold: #ffcc00;
            --font-head: 'Orbitron', sans-serif;
            --font-body: 'Exo 2', sans-serif;
        }

        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }

        body {
            font-family: var(--font-body);
            margin: 0; padding: 0;
            color: #e0e6ed;
            min-height: 100vh;
            background-color: #050505;
            background-size: cover; background-position: center; background-attachment: fixed;
            transition: background-image 0.8s ease-in-out;
            overflow-x: hidden;
        }

        /* --- НОВЫЕ ФОНОВЫЕ ИЗОБРАЖЕНИЯ ПО ТВОЕМУ ЗАПРОСУ --- */
        
        /* Старт: Башня Академии (Твоя первая ссылка) */
        #start-screen { 
            background-image: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.8)), url('https://static.wikia.nocookie.net/marvelvscapcom/images/8/8f/Avengers_Tower.png/revision/latest/scale-to-width-down/1200?cb=20171123083437'); 
        }
        
        /* Рекрут (1 уровень): Та же Башня Академии */
        body.theme-newbie { 
            background-image: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.9)), url('https://static.wikia.nocookie.net/marvelvscapcom/images/8/8f/Avengers_Tower.png/revision/latest/scale-to-width-down/1200?cb=20171123083437'); 
        }
        
        /* Агент (2 уровень): Коридор Академии (Заменил дубликат на подходящий коридор) */
        body.theme-agent { 
            background-image: linear-gradient(rgba(10,0,20,0.8), rgba(0,0,0,0.9)), url('https://images.unsplash.com/photo-1507643195032-c9e956934891?q=80&w=1920'); 
        }
        
        /* Мастер (3 уровень): Защита города (Твоя третья ссылка, комикс-стиль) */
        body.theme-master { 
            background-image: linear-gradient(rgba(20,0,0,0.8), rgba(0,0,0,0.95)), url('https://s.tmimgcdn.com/scr/800x500/152100/superhero-power-in-city-illustration_152188-original.jpg'); 
            background-position: top center;
        }
        
        /* Финал: Спасенный город (Оставил прошлый, т.к. ты забыл ссылку) */
        #final-screen { 
            background-image: url('https://images.unsplash.com/photo-1480714378408-67cf0d13bc1b?q=80&w=1920'); 
        }


        /* UI ЭЛЕМЕНТЫ */
        .glass-panel {
            background: var(--glass);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(0, 242, 255, 0.2);
            border-radius: 12px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.5);
            transition: transform 0.2s, border-color 0.2s, background 0.2s;
        }

        header {
            padding: 15px 20px;
            display: flex; justify-content: space-between; align-items: center;
            position: sticky; top: 0; z-index: 100;
            background: rgba(5, 5, 10, 0.95);
            border-bottom: 2px solid var(--accent);
            box-shadow: 0 4px 20px rgba(0, 242, 255, 0.15);
        }

        .stats-box { 
            font-family: var(--font-head);
            background: rgba(255,255,255,0.03); 
            padding: 8px 16px; border-radius: 4px; 
            border: 1px solid rgba(255,255,255,0.1);
            display: flex; align-items: center; gap: 8px;
            font-size: 0.9rem; letter-spacing: 1px;
            font-weight: bold;
        }

        .hero-section { text-align: center; padding: 40px 20px; animation: fadeIn 1s; }
        .hero-title { 
            font-family: var(--font-head); font-size: 2.5rem; 
            text-transform: uppercase; text-shadow: 0 0 15px var(--accent); margin: 0 0 10px 0;
            color: white;
        }
        .hero-desc { color: #8899a6; font-size: 1.1rem; max-width: 600px; margin: 0 auto; }

        .grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px; max-width: 1100px; margin: 0 auto; padding: 20px;
        }

        .card {
            padding: 25px; cursor: pointer; text-align: center; user-select: none;
            position: relative; overflow: hidden;
        }
        .card:active { transform: scale(0.98); }
        .card:hover { 
            transform: translateY(-5px); 
            border-color: var(--accent); 
            background: var(--glass-hover);
            box-shadow: 0 0 20px rgba(0, 242, 255, 0.15);
        }
        .card h3 { font-family: var(--font-head); margin: 15px 0 10px 0; color: #fff; }
        .icon { font-size: 3rem; margin-bottom: 10px; display: block; filter: drop-shadow(0 0 10px rgba(255,255,255,0.3)); }

        .card.special { border-color: var(--danger); }
        .card.special:hover { box-shadow: 0 0 20px rgba(255, 0, 60, 0.3); }
        
        .card.completed { border-color: var(--success); opacity: 0.7; pointer-events: none; }
        .card.completed h3 { color: var(--success); }

        .progress-bar { height: 6px; background: #222; width: 100%; margin-top: 15px; border-radius: 3px; overflow: hidden; }
        .progress-fill { height: 100%; background: var(--accent); width: 0%; transition: width 0.5s ease; box-shadow: 0 0 8px var(--accent); }

        /* КНОПКИ */
        .btn-main {
            padding: 15px 40px; font-size: 1.5rem; font-family: var(--font-head); font-weight: 900;
            background: var(--accent); border: none; cursor: pointer; color: #000;
            text-transform: uppercase; letter-spacing: 2px;
            clip-path: polygon(10px 0, 100% 0, 100% calc(100% - 10px), calc(100% - 10px) 100%, 0 100%, 0 10px);
            transition: all 0.3s;
            position: relative; z-index: 10;
        }
        .btn-main:hover { background: white; box-shadow: 0 0 30px var(--accent); transform: scale(1.05); }
        .btn-main:active { transform: scale(0.95); }

        /* ЭКРАНЫ */
        .screen-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            z-index: 5000; display: none; 
            justify-content: center; align-items: center;
            flex-direction: column;
            background-color: #000; 
            background-size: cover; background-position: center;
        }

        #start-screen { display: flex; z-index: 9999; }
        
        .story-box {
            max-width: 700px; width: 90%; padding: 40px;
            background: rgba(0,0,0,0.9); border: 2px solid var(--accent);
            text-align: center; position: relative;
            box-shadow: 0 0 50px rgba(0, 242, 255, 0.2);
        }
        .story-text {
            font-size: 1.3rem; line-height: 1.6; color: #ccc; margin-bottom: 30px; text-align: left;
            font-family: monospace; border-left: 4px solid var(--accent); padding-left: 20px;
        }

        /* ВОПРОСНИК */
        .modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.85); backdrop-filter: blur(5px);
            z-index: 6000; display: none;
            justify-content: center; align-items: center;
            opacity: 0; transition: opacity 0.3s;
        }
        .modal.open { display: flex; opacity: 1; }

        .modal-content {
            background: #0f1219; border: 1px solid var(--accent);
            padding: 30px; border-radius: 12px; width: 90%; max-width: 600px;
            box-shadow: 0 0 40px rgba(0,0,0,0.8);
            transform: scale(0.9); transition: transform 0.3s;
        }
        .modal.open .modal-content { transform: scale(1); }

        .q-text { font-size: 1.4rem; font-weight: bold; margin-bottom: 25px; color: white; line-height: 1.4; }
        
        .ans-btn {
            background: rgba(255,255,255,0.05); border: 1px solid #333;
            color: #ddd; padding: 15px; width: 100%; text-align: left;
            margin-bottom: 10px; cursor: pointer; font-size: 1.1rem;
            transition: 0.2s; border-radius: 6px;
        }
        .ans-btn:hover { border-color: var(--accent); background: rgba(0, 242, 255, 0.1); color: white; }
        .ans-btn.correct { background: rgba(0, 255, 157, 0.2); border-color: var(--success); color: var(--success); }
        .ans-btn.wrong { background: rgba(255, 0, 60, 0.2); border-color: var(--danger); color: var(--danger); }

        /* ТИТРЫ */
        #final-screen { z-index: 10000; overflow: hidden; }
        .final-score {
            font-family: var(--font-head); font-size: 6rem; color: var(--success);
            text-shadow: 0 0 30px var(--success); margin-bottom: 50px; text-align: center;
            animation: pulse 2s infinite;
        }
        @keyframes pulse { 0%{opacity:0.8;} 50%{opacity:1;} 100%{opacity:0.8;} }
        
        .credits {
            position: absolute; bottom: -100px; width: 100%; text-align: center;
            animation: creditsRoll 15s linear forwards; pointer-events: none;
        }
        @keyframes creditsRoll { from { transform: translateY(100vh); } to { transform: translateY(-110vh); } }
        .cr-role { color: var(--accent); font-size: 0.9rem; letter-spacing: 2px; text-transform: uppercase; margin-top: 40px; }
        .cr-name { font-size: 2rem; font-weight: bold; font-family: var(--font-head); }

        /* УВЕДОМЛЕНИЯ */
        #notif-area { position: fixed; top: 80px; right: 20px; z-index: 7000; display: flex; flex-direction: column; gap: 10px; }
        .notif {
            padding: 15px 25px; background: #111; border-left: 4px solid #fff;
            color: #fff; font-weight: bold; box-shadow: 0 5px 15px rgba(0,0,0,0.5);
            animation: slideInRight 0.3s;
        }
        .notif.success { border-color: var(--success); }
        .notif.error { border-color: var(--danger); }
        @keyframes slideInRight { from{transform: translateX(100%);} to{transform: translateX(0);} }

        /* Кнопка закрытия */
        .close-icon { position: absolute; top: 15px; right: 20px; font-size: 2rem; cursor: pointer; color: #555; transition:0.2s; }
        .close-icon:hover { color: var(--danger); }

    </style>
</head>
<body class="theme-newbie">

    <div id="start-screen" class="screen-overlay" style="display: flex;">
        <h1 style="font-family: 'Orbitron'; font-size: 4rem; text-align: center; text-shadow: 0 0 30px var(--accent); margin-bottom: 0;">ACADEMY<br><span style="color:var(--accent)">REBORN</span></h1>
        <p style="color:#aaa; margin-bottom: 40px; letter-spacing: 2px;">SYSTEM READY /// V.12.0</p>
        <button class="btn-main" onclick="startGame()">НАЧАТЬ</button>
    </div>

    <div id="story-screen" class="screen-overlay">
        <div class="story-box">
            <h2 id="story-title" style="color:var(--gold); font-family: 'Orbitron';">ВХОДЯЩИЙ СИГНАЛ</h2>
            <div id="story-text" class="story-text"></div>
            <button class="btn-main" onclick="closeStory()" style="font-size: 1.2rem;">ПРИНЯТЬ МИССИЮ</button>
        </div>
    </div>

    <div id="final-screen" class="screen-overlay">
        <div style="position: absolute; top:0; left:0; width:100%; height:100%; background: linear-gradient(to top, black, transparent);"></div>
        
        <div style="z-index: 2; text-align: center; margin-bottom: auto; margin-top: 15vh;">
            <div style="font-family: 'Orbitron'; font-size: 2rem; color: white;">РЕЙТИНГ МИССИИ</div>
            <div class="final-score">10 / 10</div>
        </div>

        <div class="credits">
            <div class="cr-role">ГЛАВНЫЙ ГЕРОЙ</div><div class="cr-name">ТЫ</div>
            <div class="cr-role">РАЗРАБОТКА</div><div class="cr-name">ТУГЛУКОВ ШАХРИЯР</div>
            <div class="cr-role">СЦЕНАРИЙ</div><div class="cr-name">ТУГЛУКОВ ШАХРИЯР</div>
            <div class="cr-role">AI ASSISTANT</div><div class="cr-name">GEMINI</div>
            
            <div style="margin-top: 80px;">
                <button class="btn-main" onclick="fullReset()" style="font-size: 1rem; padding: 10px 30px;">ПЕРЕЗАГРУЗКА</button>
            </div>
        </div>
    </div>

    <div id="game-ui" style="display:none;">
        <header>
            <div style="color: var(--accent); font-family: 'Orbitron'; font-size: 1.4rem; font-weight: bold;">🛡️ ACADEMY OS</div>
            <div style="display: flex; gap: 10px;">
                <div class="stats-box"><span id="rank-name">РЕКРУТ</span></div>
                <div class="stats-box" style="border-color: var(--gold); color: var(--gold);">🪙 <span id="coins">0</span></div>
            </div>
        </header>

        <section class="hero-section">
            <h1 class="hero-title" id="location-name">ХОЛЛ АКАДЕМИИ</h1>
            <p class="hero-desc" id="location-desc">Базовый уровень доступа. Выполняй задания для повышения ранга.</p>
        </section>

        <div class="grid">
            <div class="card glass-panel" onclick="openTask('speech')">
                <span class="icon">🗣️</span>
                <h3>ЭТИКЕТ</h3>
                <div class="progress-bar"><div class="progress-fill" id="bar-speech"></div></div>
            </div>
            <div class="card glass-panel" onclick="openTask('logic')">
                <span class="icon">🧠</span>
                <h3>ЛОГИКА</h3>
                <div class="progress-bar"><div class="progress-fill" id="bar-logic"></div></div>
            </div>
            <div class="card glass-panel" onclick="openTask('crit')">
                <span class="icon">👁️</span>
                <h3>БЕЗОПАСНОСТЬ</h3>
                <div class="progress-bar"><div class="progress-fill" id="bar-crit"></div></div>
            </div>
            
            <div class="card glass-panel special" id="card-hack" onclick="openHack()">
                <span class="icon">🎲</span>
                <h3 id="hack-title">ВЗЛОМ</h3>
                <p id="hack-desc" style="font-size:0.9rem; color:#ff88aa;">Награда: Высокая</p>
            </div>

            <div class="card glass-panel" onclick="checkRankUp()" style="border-color: var(--gold);">
                <span class="icon">🚀</span>
                <h3>ПОВЫШЕНИЕ</h3>
                <p style="font-size:0.9rem; color:#aaa;">След. уровень</p>
            </div>
        </div>
    </div>

    <div id="quiz-modal" class="modal">
        <div class="modal-content">
            <div id="quiz-text" class="q-text"></div>
            <div id="quiz-answers"></div>
        </div>
    </div>

    <div id="hack-modal" class="modal">
        <div class="modal-content" style="text-align: center;">
            <div class="close-icon" onclick="closeModal('hack-modal')">&times;</div>
            <h2 style="color:var(--accent); font-family:'Orbitron'">СИСТЕМА ЗАЩИТЫ</h2>
            <div id="hack-content"></div>
        </div>
    </div>

    <div id="store-modal" class="modal">
        <div class="modal-content" style="text-align: center;">
            <div class="close-icon" onclick="closeModal('store-modal')">&times;</div>
            <h2 style="font-family:'Orbitron'">ДОСТУП К СЛЕДУЮЩЕМУ УРОВНЮ</h2>
            <div id="store-content"></div>
        </div>
    </div>

    <div id="notif-area"></div>

    <script>
        // --- ДАННЫЕ (Короткие вопросы) ---
        const db = {
            newbie: { 
                speech: [
                    {q:"Учитель вошел в класс. Твои действия?", a:["Встать и поздороваться.", "Сидеть молча."]}, 
                    {q:"Друг уронил пенал. Что сделаешь?", a:["Помогу собрать.", "Посмеюсь."]}, 
                    {q:"Надо спросить время у взрослого.", a:["«Извините, который час?»", "«Эй, время есть?»"]},
                    {q:"Толкнул кого-то случайно.", a:["«Извини, пожалуйста.»", "«Смотри куда прешь!»"]},
                    {q:"Бабушка дала невкусную конфету.", a:["«Спасибо за заботу!»", "«Фу, гадость.»"]}
                ],
                logic: [
                    {q:"2 яблока + 3 груши. Сколько фруктов?", a:["5 фруктов", "2 яблока"]}, 
                    {q:"Что легче: кг ваты или кг гвоздей?", a:["Одинаково", "Гвозди тяжелее"]}, 
                    {q:"У стола 4 угла. Один отпилили. Сколько стало?", a:["5 углов", "3 угла"]},
                    {q:"Сколько пальцев на 2 руках?", a:["10", "2"]},
                    {q:"Лед растаял. Чем он стал?", a:["Водой", "Паром"]}
                ],
                crit: [
                    {q:"Сайт пишет: «Ты выиграл iPhone!». Жмешь?", a:["Нет, это обман.", "Да, забираю!"]}, 
                    {q:"Незнакомец зовет в машину смотреть котят.", a:["Убегу и расскажу взрослым.", "Пойду смотреть."]}, 
                    {q:"Просят пароль от игры, чтобы «прокачать».", a:["Не дам пароль.", "Дам, пусть качает."]},
                    {q:"Нашел чужую карту на улице.", a:["Отдам родителям/полиции.", "Пойду в магазин."]},
                    {q:"Друг зовет гулять на стройку.", a:["Откажусь, там опасно.", "Пойду, я смелый."]}
                ]
            },
            agent: {
                speech: [
                    {q:"Одноклассник грустит. Что скажешь?", a:["«Могу я чем-то помочь?»", "«Чего ноешь?»"]}, 
                    {q:"Тебя ругают ни за что. Реакция?", a:["Спокойно объясню ситуацию.", "Начну кричать."]}, 
                    {q:"Новичок в классе никого не знает.", a:["Подойду познакомиться.", "Буду игнорировать."]},
                    {q:"Опоздал на встречу.", a:["«Простите за опоздание.»", "«Я же пришел, всё ок.»"]},
                    {q:"Мама устала после работы.", a:["Помогу по дому.", "Попрошу кушать."]}
                ],
                logic: [
                    {q:"Что идет после вторника?", a:["Среда", "Четверг"]}, 
                    {q:"Сколько месяцев имеют 28 дней?", a:["Все 12", "Один"]}, 
                    {q:"Сын моего отца, но не я.", a:["Мой брат", "Дядя"]},
                    {q:"Что можно разбить, не трогая?", a:["Слово (или обещание)", "Стакан"]},
                    {q:"Чем больше берешь, тем больше становится.", a:["Яма", "Куча"]}
                ],
                crit: [
                    {q:"Звонят с незнакомого номера и молчат.", a:["Положу трубку.", "Буду кричать «Алло»."]}, 
                    {q:"В интернете просят твое фото.", a:["Не отправлю.", "Отправлю красивое."]}, 
                    {q:"Нашел флешку на улице. Вставишь в ПК?", a:["Нет, там могут быть вирусы.", "Да, посмотрю что там."]},
                    {q:"Предлагают попробовать сигареты.", a:["Твердо откажусь.", "Попробую разок."]},
                    {q:"В чате оскорбляют друга.", a:["Поддержу друга.", "Присоединюсь к травле."]}
                ]
            },
            master: {
                speech: [
                    {q:"Выиграл в конкурсе. Что скажешь?", a:["«Спасибо всем за поддержку!»", "«Я круче всех!»"]}, 
                    {q:"Увидел, как старшие обижают малыша.", a:["Сообщу учителю/охране.", "Пройду мимо."]}, 
                    {q:"Друг рассказал секрет.", a:["Сохраню в тайне.", "Расскажу всем."]},
                    {q:"Нужно отказать в просьбе.", a:["«Извини, я не могу сейчас.»", "«Отстань.»"]},
                    {q:"Разбил вазу в гостях.", a:["Извинюсь и предложу помощь.", "Спрячу осколки."] }
                ],
                logic: [
                    {q:"Города без домов, реки без воды.", a:["Карта", "Сон"]}, 
                    {q:"Что не влезает даже в самую большую кастрюлю?", a:["Её крышка", "Суп"]}, 
                    {q:"Человек под дождем без зонта, но волосы сухие.", a:["Он лысый", "Дождь грибной"]},
                    {q:"Что принадлежит тебе, но другие пользуются чаще?", a:["Имя", "Деньги"]},
                    {q:"Можно ли принести воду в решете?", a:["Да, если она лед", "Нет, вытечет"]}
                ],
                crit: [
                    {q:"«Банк» просит код из СМС.", a:["Никому не скажу код.", "Скажу, это же банк."]}, 
                    {q:"Пришло письмо: «Скачай файл срочно».", a:["Удалю письмо.", "Скачаю."]}, 
                    {q:"В соцсети незнакомец притворяется другом.", a:["Проверю, задав личный вопрос.", "Поверю сразу."]},
                    {q:"Предлагают легкий заработок (закладки).", a:["Откажусь, это преступление.", "Соглашусь ради денег."]},
                    {q:"Твой аккаунт пытались взломать.", a:["Сменю пароль и включу 2FA.", "Ничего не сделаю."]}
                ]
            }
        };

        const ranks = {
            newbie: { name: "РЕКРУТ", theme: "theme-newbie", loc: "АКАДЕМИЯ", desc: "Докажи, что ты готов к реальному миру.", cost: 1000, rewardQ: 100, rewardH: 500, next: "agent" },
            agent: { name: "АГЕНТ", theme: "theme-agent", loc: "КОРИДОРЫ ВЛАСТИ", desc: "Улицы полны опасностей. Будь начеку.", cost: 2500, rewardQ: 200, rewardH: 1000, next: "master" },
            master: { name: "МАСТЕР", theme: "theme-master", loc: "ЛИНИЯ ФРОНТА", desc: "Финальный рубеж. Защити город.", cost: 5000, rewardQ: 300, rewardH: 2000, next: "omega" }
        };

        const stories = {
            start: "Внимание, курсант!<br><br>Ты прибыл в Академию Героев (Башня Мстителей). Здесь мы готовим защитников будущего. Твоя первая задача — пройти базовую подготовку и доказать, что ты достоин носить это звание.<br><br>Удачи.",
            toAgent: "Поздравляю с повышением!<br><br>Ты отлично справился с теорией. Теперь практика. Тебя переводят в оперативный штаб. Изучи коридоры власти, научись принимать сложные решения на ходу.",
            toMaster: "Невероятно!<br><br>Ты показал себя настоящим профессионалом. Город в опасности, и нам нужны лучшие из лучших на передовой. Ты получаешь ранг МАСТЕР. Твоя миссия — прямая защита граждан.",
            end: "МИССИЯ ВЫПОЛНЕНА.<br><br>Ты сделал это! Благодаря твоим ответам, логике и честности, город спасен. Жители могут спать спокойно, зная, что такие герои, как ты, стоят на страже.<br><br>Ты — настоящая Легенда."
        };

        // --- СОСТОЯНИЕ ИГРЫ ---
        let state = {
            rank: 'newbie',
            coins: 0,
            prog: { speech: 0, logic: 0, crit: 0 },
            hackDone: false
        };
        let tempNextRank = null; // Для перехода

        // --- ФУНКЦИИ ---

        function startGame() {
            // Проверка сохранения (Ключ новый V12)
            const save = localStorage.getItem('heroSaveV12_Fixed');
            document.getElementById('start-screen').style.display = 'none';

            if (save) {
                state = JSON.parse(save);
                if (state.rank === 'omega') {
                    showFinal();
                } else {
                    initGameUI();
                }
            } else {
                // Новая игра - показать сюжет
                showStory('start');
            }
        }

        function showStory(key) {
            const txt = stories[key];
            const screen = document.getElementById('story-screen');
            document.getElementById('story-text').innerHTML = txt;
            screen.style.display = 'flex'; // Явный flex
            
            // Если это конец
            if(key === 'end') {
                document.querySelector('#story-screen button').onclick = () => {
                     document.getElementById('story-screen').style.display = 'none';
                     showFinal();
                };
            }
        }

        function closeStory() {
            document.getElementById('story-screen').style.display = 'none';
            
            // Если был запланирован переход на новый ранг
            if (tempNextRank) {
                state.rank = tempNextRank;
                state.prog = { speech: 0, logic: 0, crit: 0 };
                state.hackDone = false;
                tempNextRank = null;
            }
            
            initGameUI();
            saveGame();
        }

        function initGameUI() {
            document.getElementById('game-ui').style.display = 'block';
            updateUI();
        }

        function updateUI() {
            const rData = ranks[state.rank];
            document.body.className = rData.theme;
            
            document.getElementById('rank-name').innerText = rData.name;
            document.getElementById('coins').innerText = state.coins;
            document.getElementById('location-name').innerText = rData.loc;
            document.getElementById('location-desc').innerText = rData.desc;

            // Прогресс бары
            ['speech', 'logic', 'crit'].forEach(type => {
                const pct = (state.prog[type] / 5) * 100;
                document.getElementById(`bar-${type}`).style.width = pct + '%';
            });

            // Карточка взлома
            const hCard = document.getElementById('card-hack');
            if (state.hackDone) {
                hCard.classList.remove('special');
                hCard.classList.add('completed');
                document.getElementById('hack-title').innerText = "ВЗЛОМАНО";
                document.getElementById('hack-desc').innerText = "Доступ получен";
                document.getElementById('hack-desc').style.color = "var(--success)";
            } else {
                hCard.classList.add('special');
                hCard.classList.remove('completed');
                document.getElementById('hack-title').innerText = "ВЗЛОМ";
                document.getElementById('hack-desc').innerText = `Награда: ${rData.rewardH} 🪙`;
                document.getElementById('hack-desc').style.color = "#ff88aa";
            }
            saveGame();
        }

        function openTask(type) {
            if (state.prog[type] >= 5) {
                notify("Этот навык уже прокачан на максимум!", "success");
                return;
            }

            const qList = db[state.rank][type];
            const qIndex = state.prog[type]; // Берем вопрос по порядку 0..4
            const qData = qList[qIndex];

            const modal = document.getElementById('quiz-modal');
            const txt = document.getElementById('quiz-text');
            const ansDiv = document.getElementById('quiz-answers');
            
            txt.innerText = qData.q;
            ansDiv.innerHTML = '';

            // Перемешиваем ответы
            let answers = [
                { t: qData.a[0], ok: true },
                { t: qData.a[1], ok: false }
            ].sort(() => Math.random() - 0.5);

            answers.forEach(ans => {
                let btn = document.createElement('div');
                btn.className = 'ans-btn';
                btn.innerText = ans.t;
                btn.onclick = () => checkAnswer(btn, ans.ok, type);
                ansDiv.appendChild(btn);
            });

            openModal('quiz-modal');
        }

        function checkAnswer(btn, isCorrect, type) {
            // Блокируем все кнопки
            const all = document.querySelectorAll('.ans-btn');
            all.forEach(b => b.style.pointerEvents = 'none');

            if (isCorrect) {
                btn.classList.add('correct');
                const reward = ranks[state.rank].rewardQ;
                state.coins += reward;
                state.prog[type]++;
                notify(`ВЕРНО! +${reward} монет`, "success");
                
                setTimeout(() => {
                    closeModal('quiz-modal');
                    updateUI();
                }, 1000);
            } else {
                btn.classList.add('wrong');
                notify("Ошибка! Попробуй снова.", "error");
                setTimeout(() => {
                    closeModal('quiz-modal');
                }, 1000);
            }
        }

        function openHack() {
            if(state.hackDone) return;
            
            let html = '';
            let q = ''; 
            let correct = 0;
            let options = [];

            // Генерация примера
            if(state.rank === 'newbie') {
                let a = rInt(10, 50), b = rInt(10, 50);
                correct = a + b; q = `${a} + ${b} = ?`;
                options = [correct, correct+5, correct-2];
            } else if (state.rank === 'agent') {
                let a = rInt(3, 10), b = rInt(3, 10);
                correct = a * b; q = `${a} × ${b} = ?`;
                options = [correct, correct+2, correct-3];
            } else {
                let a = rInt(5, 15), b = rInt(2, 5), c = rInt(10, 100);
                correct = a * b + c; q = `${a} × ${b} + ${c} = ?`;
                options = [correct, correct+10, correct-10];
            }
            options.sort(()=>Math.random()-0.5);

            html += `<h1 style="color:white; font-size:3rem; margin:20px 0;">${q}</h1>`;
            html += `<div style="display:flex; gap:10px; justify-content:center;">`;
            options.forEach(opt => {
                html += `<button class="btn-main" onclick="solveHack(${opt}, ${correct})" style="font-size:1.2rem; min-width:80px;">${opt}</button>`;
            });
            html += `</div>`;

            document.getElementById('hack-content').innerHTML = html;
            openModal('hack-modal');
        }

        function solveHack(val, correct) {
            if (val === correct) {
                state.hackDone = true;
                const r = ranks[state.rank].rewardH;
                state.coins += r;
                notify(`СИСТЕМА ВЗЛОМАНА! +${r} монет`, "success");
                closeModal('hack-modal');
                updateUI();
            } else {
                notify("ОШИБКА ДОСТУПА", "error");
                closeModal('hack-modal');
            }
        }

        function checkRankUp() {
            const p = state.prog;
            const fullSkills = (p.speech >= 5 && p.logic >= 5 && p.crit >= 5);
            const nextKey = ranks[state.rank].next;
            const cost = ranks[state.rank].cost;

            if (!fullSkills) {
                notify("Сначала прокачай все навыки до максимума!", "error");
                return;
            }
            if (!nextKey) return;

            let html = `<p style="font-size:1.2rem; color:#aaa;">Стоимость перехода: <span style="color:var(--gold); font-weight:bold;">${cost} 🪙</span></p>`;
            
            if (state.coins >= cost) {
                html += `<button class="btn-main" onclick="buyRank('${nextKey}', ${cost})">КУПИТЬ ДОСТУП</button>`;
            } else {
                html += `<button class="btn-main" style="background:#444; color:#888; cursor:not-allowed;">НЕДОСТАТОЧНО СРЕДСТВ</button>`;
            }

            document.getElementById('store-content').innerHTML = html;
            openModal('store-modal');
        }

        function buyRank(nextKey, cost) {
            state.coins -= cost;
            closeModal('store-modal');
            tempNextRank = nextKey; 
            
            let storyKey = '';
            if (nextKey === 'agent') storyKey = 'toAgent';
            if (nextKey === 'master') storyKey = 'toMaster';
            if (nextKey === 'omega') storyKey = 'end';

            document.getElementById('game-ui').style.display = 'none';
            showStory(storyKey);
        }

        function showFinal() {
            state.rank = 'omega';
            saveGame();
            
            document.getElementById('game-ui').style.display = 'none';
            document.getElementById('start-screen').style.display = 'none';
            document.getElementById('story-screen').style.display = 'none';
            
            const final = document.getElementById('final-screen');
            final.style.display = 'flex';
        }

        // --- УТИЛИТЫ ---
        function rInt(min, max) { return Math.floor(Math.random() * (max - min + 1) ) + min; }
        
        function openModal(id) {
            const m = document.getElementById(id);
            m.style.display = 'flex';
            setTimeout(() => { m.classList.add('open'); }, 10);
        }

        function closeModal(id) {
            const m = document.getElementById(id);
            m.classList.remove('open');
            setTimeout(() => { m.style.display = 'none'; }, 300);
        }

        function notify(msg, type) {
            const n = document.createElement('div');
            n.className = `notif ${type}`;
            n.innerText = msg;
            document.getElementById('notif-area').appendChild(n);
            setTimeout(() => n.remove(), 3000);
        }

        function saveGame() {
            localStorage.setItem('heroSaveV12_Fixed', JSON.stringify(state));
        }

        function fullReset() {
            if(confirm("Начать игру с самого начала?")) {
                localStorage.removeItem('heroSaveV12_Fixed');
                location.reload();
            }
        }

    </script>
</body>
</html>\
