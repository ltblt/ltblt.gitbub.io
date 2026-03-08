<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>一可的周末魔法森林 V3.0</title>
    <style>
        :root {
            --primary: #FF9A9E; --secondary: #FECFEF; --accent: #A18CD1;
            --success: #2ed573; --danger: #ff4757; --text: #2f3542;
        }
        body {
            font-family: 'Comic Sans MS', 'Microsoft YaHei', sans-serif;
            background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);
            margin: 0; padding: 10px; color: var(--text);
            display: flex; justify-content: center; align-items: center; min-height: 100vh;
        }
        #game-app {
            background: rgba(255, 255, 255, 0.95);
            width: 100%; max-width: 900px; min-height: 650px;
            border-radius: 30px; box-shadow: 0 20px 50px rgba(0,0,0,0.3);
            padding: 30px; box-sizing: border-box; position: relative;
            overflow: hidden; text-align: center;
        }
        h1 { color: #ff6b81; font-size: 36px; text-shadow: 2px 2px #ffeaa7; margin-top: 0; }
        .subtitle { color: #747d8c; font-size: 18px; margin-bottom: 20px; font-weight: bold; }
        
        .btn {
            display: inline-block; padding: 15px 40px; margin: 10px;
            font-size: 24px; font-weight: bold; color: white; border: none;
            border-radius: 50px; cursor: pointer; transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        .btn:hover { transform: translateY(-3px) scale(1.05); box-shadow: 0 8px 25px rgba(0,0,0,0.3); }
        .btn-start { background: linear-gradient(45deg, #ff9a9e, #fecfef); color: #d63031; font-size: 28px; animation: pulse 2s infinite;}
        .btn-review { background: linear-gradient(45deg, #f6d365, #fda085); color: #d35400; }
        
        .hidden { display: none !important; }
        .question-text { font-size: 28px; color: #3742fa; font-weight: bold; margin: 15px 0; }
        
        /* 动态记忆图谱 */
        .mnemonic-box {
            background: #f1f2f6; border-radius: 20px; padding: 15px; margin: 15px auto;
            max-width: 650px; font-size: 26px; display: flex; justify-content: center; align-items: center; gap: 10px;
            border: 3px dashed #a18cd1;
        }
        .m-image { font-size: 55px; margin: 0 10px; animation: bounce 2s infinite; }

        /* 填空题 */
        .spell-display { font-size: 45px; letter-spacing: 10px; color: #2f3542; margin: 20px 0; font-family: monospace; font-weight: bold;}
        .blank-slot { display: inline-block; border-bottom: 5px solid #ff4757; width: 45px; text-align: center; color: #ff4757; cursor: pointer; height: 55px; line-height: 55px;}
        .blank-slot.active { border-bottom-color: #3742fa; background: #dfe4ea; border-radius: 8px; }
        .options-grid { display: flex; flex-wrap: wrap; justify-content: center; gap: 15px; margin-top: 20px; }
        .opt-chip { padding: 12px 25px; font-size: 26px; background: white; border: 4px solid #ced6e0; border-radius: 15px; cursor: pointer; font-weight: bold; transition: 0.2s;}
        .opt-chip:hover { border-color: #a18cd1; background: #f1f2f6; transform: scale(1.1); }
        
        /* 语音题 */
        .mic-btn { font-size: 70px; background: none; border: none; cursor: pointer; transition: 0.3s; margin: 10px 0;}
        .mic-btn.recording { color: #ff4757; animation: shake 0.5s infinite; filter: drop-shadow(0 0 15px #ff4757);}
        .phonics-hint { font-size: 32px; color: #e67e22; letter-spacing: 3px; font-weight: bold; }

        /* 词根实验室 (Lab) */
        .lab-equation { font-size: 40px; font-weight: bold; color: #2f3542; margin: 30px 0; display: flex; align-items: center; justify-content: center; gap: 15px;}
        .lab-box { background: #ffeaa7; border: 3px dashed #fdcb6e; padding: 10px 20px; border-radius: 15px; color: #d63031; }
        .lab-drop { background: white; border: 4px solid #ff7675; padding: 10px 30px; border-radius: 15px; min-width: 60px; color: #ff7675; cursor:help;}

        /* 倒计时遮罩 */
        #stage-transition {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(255,255,255,0.95); z-index: 100;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
        }
        .stage-title { font-size: 45px; color: #a18cd1; font-weight: bold; margin-bottom: 20px;}
        .count-number { font-size: 150px; color: #ff4757; font-weight: bold; animation: zoom 1s linear infinite; }
        
        /* 动画 */
        @keyframes bounce { 0%, 100% {transform: translateY(0);} 50% {transform: translateY(-10px);} }
        @keyframes pulse { 0% {transform: scale(1);} 50% {transform: scale(1.05);} 100% {transform: scale(1);} }
        @keyframes shake { 0%, 100% { transform: translateX(0); } 25% { transform: translateX(-5px); } 75% { transform: translateX(5px); } }
        @keyframes zoom { 0% {transform: scale(1.5); opacity: 0;} 20% {opacity: 1;} 80% {transform: scale(0.8); opacity: 1;} 100% {transform: scale(0.5); opacity: 0;} }

        #feedback { font-size: 28px; margin-top: 15px; font-weight: bold; min-height: 40px; }
        .top-bar { display: flex; justify-content: space-between; margin-bottom: 10px; font-size: 20px; font-weight: bold; color: #747d8c; }
    </style>
</head>
<body>

<div id="game-app">
    <!-- 主菜单 -->
    <div id="menu-view">
        <h1>🌟 一可特工：魔法森林 V3.0 🌟</h1>
        <div class="subtitle">包含 Unit1 所有拼写、句子，新增【词根合成实验室】！</div>
        <img src="https://api.iconify.design/noto:magic-wand.svg" alt="magic" width="100" style="margin: 10px auto; display: block;">
        <button class="btn btn-start" onclick="startAdventure()">🚀 开启 4 大连关挑战</button><br>
        <button class="btn btn-review" onclick="openReview()">🕰️ 记忆修复舱 (查漏补缺)</button>
    </div>

    <!-- 游戏主界面 -->
    <div id="game-view" class="hidden">
        <div class="top-bar">
            <span id="stage-text" style="color:#a18cd1;">关卡 1/4</span>
            <span id="progress-text">进度: 1/10</span>
            <button onclick="location.reload()" style="background:none; border:none; color:#ff4757; font-weight:bold; cursor:pointer; font-size:20px;">✖ 退出</button>
        </div>
        
        <div id="question-container" class="question-text"></div>
        <div id="mnemonic-container"></div>
        <div id="interactive-area"></div>
        <div id="feedback"></div>
    </div>

    <!-- 关卡切换倒计时 -->
    <div id="stage-transition" class="hidden">
        <div class="stage-title" id="trans-title">准备进入下一关！</div>
        <div id="count-num" class="count-number">3</div>
    </div>

    <!-- 复习界面 -->
    <div id="review-view" class="hidden">
        <h2 style="color:#d35400;">🕰️ 艾宾浩斯记忆修复舱</h2>
        <div id="review-list" style="text-align:left; background:#fff3e0; padding:20px; border-radius:15px; font-size:20px; max-height: 350px; overflow-y: auto;"></div>
        <button class="btn btn-review" onclick="location.reload()" style="margin-top: 20px;">返回大厅</button>
    </div>
</div>

<script>
// ================= 全量题库 (V3.0 升级版) =================

// 关卡1：重难点拼写填空 (加入 watch TV, like doing, usually 等)
const spellData =[
    { w: 'watch TV', zh: '看电视', html: '<span class="m-image">👀</span> w - a - t - c - h <span class="m-image">📺</span>', display: 'w _ t c h   T V', ans: ['a'], opts:['a','o','e','i'] },
    { w: 'usually', zh: '经常 (80%)', html: 'u - s - <span style="color:#ff4757">u</span> - a - l - l - <span style="color:#ff4757">y</span>', display: 'u s _ a l l _', ans: ['u','y'], opts: ['u','y','e','i'] },
    { w: 'like doing', zh: '喜欢做某事', html: '<span class="m-image">❤️</span> l - i - k - e   d - o - i - n - g', display: 'l _ k e   d o _ n g', ans: ['i','i'], opts: ['i','e','a','o'] },
    { w: 'sometimes', zh: '有时 (30%)', html: 's - <span style="color:#ff4757">o</span> - m - e - t - <span style="color:#ff4757">i</span> - m - e - s', display: 's _ m e t _ m e s', ans: ['o','i'], opts:['o','a','i','e'] },
    { w: 'children', zh: '孩子们 (复数)', html: '<span class="m-image">👶👧👦</span> ch - i - l - d - r - e - n', display: 'c h _ l d r _ n', ans:['i','e'], opts:['i','a','e','o'] },
    { w: 'cows', zh: '奶牛(复数)', html: '<span class="m-image">🐄🥛</span> c - <span style="color:#ff4757">ow</span> - s', display: 'c _ _ s', ans: ['o','w'], opts:['o','w','a','r'] },
    { w: 'always', zh: '一直 (100%)', html: 'a - l - w - <span style="color:#ff4757">a - y</span> - s', display: 'a l w _ _ s', ans: ['a','y'], opts: ['a','y','e','i'] },
    { w: 'often', zh: '通常 (60%)', html: '<span class="m-image">⏰</span> o - f - t - e - n', display: 'o f t _ n', ans:['e'], opts:['e','a','o'] },
    { w: 'seldom', zh: '几乎不 (10%)', html: '<span class="m-image">🪫</span> s - e - l - d - o - m', display: 's _ l d _ m', ans:['e','o'], opts:['e','a','o','u'] },
    { w: 'never', zh: '从不 (0%)', html: '<span class="m-image">🚫</span> n - e - v - e - r', display: 'n _ v _ r', ans: ['e','e'], opts: ['e','a','i'] },
    { w: 'skate', zh: '滑冰', html: '<span class="m-image">⛸️</span> <span style="color:#ff4757">s - k</span> - a - t - e', display: '_ _ a t e', ans:['s','k'], opts:['s','k','c','t'] },
    { w: 'ski', zh: '滑雪', html: '<span class="m-image">⛷️</span> <span style="color:#ff4757">s - k</span> - i', display: '_ _ i', ans: ['s','k'], opts:['s','k','c','h'] },
    { w: 'album', zh: '相册', html: '<span class="m-image">📔</span> a - l - b - u - m', display: 'a l b _ m', ans: ['u'], opts:['u','a','o'] }
];

// 关卡2：大声说短语 (训练口腔肌肉记忆)
const voiceData =[
    { w: 'visit Grandma and Grandpa', zh: '看望爷爷奶奶', html: '<span class="m-image">👵</span> <span class="m-image">🏠</span> <span class="m-image">👴</span>', ph: 'vi-sit Grand-ma and Grand-pa' },
    { w: 'see a film', zh: '看电影', html: '<span class="m-image">👀</span> <span class="m-image">🎬</span>', ph: 'see a film' },
    { w: 'have a good time', zh: '过得愉快', html: '<span class="m-image">😆</span> <span class="m-image">🎉</span>', ph: 'have a good time' },
    { w: 'on the farm', zh: '在农场', html: '<span class="m-image">🚜</span> <span class="m-image">🌾</span>', ph: 'on the farm' },
    { w: 'watch fireworks', zh: '看烟花', html: '<span class="m-image">👀</span> <span class="m-image">🎆</span>', ph: 'watch fire-works' },
    { w: 'take a family photo', zh: '拍全家福', html: '<span class="m-image">📸</span> <span class="m-image">👨‍👩‍👧‍👦</span>', ph: 'take a fa-mi-ly pho-to' }
];

// 关卡3：句子积木重组 (长句化整为零)
const sentenceData =[
    { text: 'What do you often do in the holidays ?', zh: '你在假期通常做什么？', html: '<span class="m-image">🏖️❓</span>' },
    { text: 'I see a new film . It is funny .', zh: '我经常看新电影。很好笑。', html: '<span class="m-image">🎬😂</span>' },
    { text: 'I skate with my dad . It is so cool .', zh: '我和爸爸滑冰。这太酷了。', html: '<span class="m-image">👨‍👧⛸️🧊</span>' },
    { text: 'I visit my grandma and grandpa . I have a good time .', zh: '我看望爷爷奶奶。我过得很愉快。', html: '<span class="m-image">👵👴😊</span>' },
    { text: 'Your holidays sound really great !', zh: '你的假期听起来真的很棒！', html: '<span class="m-image">👂✨</span>' },
    { text: 'Health is something like gold .', zh: '【名言】健康像金子一样。', html: '<span class="m-image">🏃‍♂️</span> = <span class="m-image">🥇</span>' },
    { text: 'Books are a pure and beautiful entity .', zh: '【名言】书籍是纯洁美好的。', html: '<span class="m-image">📚</span> 🌸' }
];

// 关卡4：词根与语法拓展实验室 (Morphemes & Word Roots)
const labData =[
    { q: '合成烟花！', p1: 'fire (火)', p2: '???', res: 'fireworks 🎆', ans: 'works', opts: ['works', 'words', 'walks'] },
    { q: '把小孩变成复数！', p1: 'child (小孩)', p2: '???', res: 'children 👶👧👦', ans: 'ren', opts: ['s', 'es', 'ren'] },
    { q: '同义词转换 (喜欢做某事)', p1: 'like doing', p2: '=', res: 'like to do ❤️', ans: 'like to do', opts: ['like do', 'like to do', 'likes'] },
    { q: '合成副词：有时', p1: 'some (一些)', p2: '???', res: 'sometimes ⏳', ans: 'times', opts: ['times', 'things', 'day'] },
    { q: '合成词：爷爷', p1: 'Grand (老/大)', p2: '???', res: 'Grandpa 👴', ans: 'pa', opts: ['ma', 'pa', 'dad'] },
    { q: '副词加后缀：经常', p1: 'usual (平常)', p2: '???', res: 'usually 🔁', ans: 'ly', opts: ['ly', 's', 'ing'] }
];

const stages =[
    { type: 'spell', data: spellData, title: '🧩 关卡1：硬核拼写' },
    { type: 'voice', data: voiceData, title: '🎙️ 关卡2：大声说短语' },
    { type: 'sentence', data: sentenceData, title: '🪄 关卡3：句子积木' },
    { type: 'lab', data: labData, title: '🧪 关卡4：词根合成实验室' }
];

let currentStageIdx = 0; let currentQIdx = 0; let recognition = null; let sentenceSelected =[];

// ================= TTS 语音 =================
function speak(text) {
    if ('speechSynthesis' in window) {
        window.speechSynthesis.cancel();
        let msg = new SpeechSynthesisUtterance(text.replace('???','').replace('=','equals'));
        msg.lang = 'en-US'; msg.rate = 0.85;
        window.speechSynthesis.speak(msg);
    }
}

// ================= 复习系统 =================
function recordMistake(text, zh) {
    let mistakes = JSON.parse(localStorage.getItem('yike_v3_mistakes')) || {};
    mistakes[text] = { zh: zh, time: new Date().toLocaleString() };
    localStorage.setItem('yike_v3_mistakes', JSON.stringify(mistakes));
}

function openReview() {
    document.getElementById('menu-view').classList.add('hidden');
    document.getElementById('review-view').classList.remove('hidden');
    let mistakes = JSON.parse(localStorage.getItem('yike_v3_mistakes')) || {};
    let listArea = document.getElementById('review-list');
    let items = Object.keys(mistakes);
    if (items.length === 0) {
        listArea.innerHTML = "<p style='color:#2ed573;'>🎉 完美！一可特工目前没有错题！</p>";
    } else {
        listArea.innerHTML = items.map(k => `<div style="padding:15px; border-bottom:2px dashed #ccc;">⚠️ <b>${k}</b> <br><span style="font-size:16px; color:#747d8c">${mistakes[k].zh}</span></div>`).join('');
    }
}

// ================= 游戏流控制 =================
function startAdventure() {
    document.getElementById('menu-view').classList.add('hidden');
    stages.forEach(stage => stage.data.sort(() => Math.random() - 0.5)); // 打乱
    currentStageIdx = 0; startStage();
}

function startStage() {
    currentQIdx = 0;
    let stageInfo = stages[currentStageIdx];
    document.getElementById('stage-transition').classList.add('hidden');
    document.getElementById('game-view').classList.remove('hidden');
    document.getElementById('stage-text').innerText = stageInfo.title;
    
    if (stageInfo.type === 'voice') initSpeechRecognition();
    else if (recognition) { recognition.stop(); recognition = null; }
    
    loadQuestion();
}

function loadQuestion() {
    let stageInfo = stages[currentStageIdx];
    if (currentQIdx >= stageInfo.data.length) { triggerStageTransition(); return; }

    let q = stageInfo.data[currentQIdx];
    document.getElementById('progress-text').innerText = `进度: ${currentQIdx + 1} / ${stageInfo.data.length}`;
    document.getElementById('question-container').innerText = q.zh || q.q;
    
    let mContainer = document.getElementById('mnemonic-container');
    if (q.html) {
        mContainer.innerHTML = `<div class="mnemonic-box">${q.html}</div>`;
        mContainer.classList.remove('hidden');
    } else mContainer.classList.add('hidden');

    document.getElementById('feedback').innerText = '';
    let area = document.getElementById('interactive-area');
    area.innerHTML = '';

    if (stageInfo.type === 'spell') renderSpell(q, area);
    else if (stageInfo.type === 'voice') renderVoice(q, area);
    else if (stageInfo.type === 'sentence') renderSentence(q, area);
    else if (stageInfo.type === 'lab') renderLab(q, area);

    if(stageInfo.type !== 'sentence' && stageInfo.type !== 'lab') speak(q.w);
}

function nextQuestionFast() { currentQIdx++; setTimeout(loadQuestion, 600); }

function triggerStageTransition() {
    currentStageIdx++;
    if (currentStageIdx >= stages.length) {
        document.getElementById('game-view').classList.add('hidden');
        document.getElementById('menu-view').classList.remove('hidden');
        document.querySelector('#menu-view h1').innerHTML = "🎉 Unit 1 通关大满贯！ 🎉";
        speak("Congratulations! You are super great!");
        return;
    }
    let overlay = document.getElementById('stage-transition');
    document.getElementById('trans-title').innerText = stages[currentStageIdx].title + " 即将开始！";
    overlay.classList.remove('hidden');
    
    let count = 3; document.getElementById('count-num').innerText = count;
    let timer = setInterval(() => {
        count--;
        if (count > 0) document.getElementById('count-num').innerText = count;
        else { clearInterval(timer); startStage(); }
    }, 1000);
}

// ================= 渲染：1. 拼写题 =================
function renderSpell(q, container) {
    let html = `
        <div class="spell-display">${q.display.split(' ').map(c => c === '_' ? '<span class="blank-slot" onclick="selectBlank(this)"></span>' : `<span>${c}</span>`).join(' ')}</div>
        <div class="options-grid" id="spell-opts"></div>`;
    container.innerHTML = html;
    let optsArea = document.getElementById('spell-opts');
    [...q.opts].sort(() => Math.random() - 0.5).forEach(opt => {
        let btn = document.createElement('div'); btn.className = 'opt-chip'; btn.innerText = opt;
        btn.onclick = () => fillBlank(opt, q); optsArea.appendChild(btn);
    });
    setTimeout(() => { let f = document.querySelector('.blank-slot'); if(f) selectBlank(f); }, 50);
}

function selectBlank(el) { document.querySelectorAll('.blank-slot').forEach(e => e.classList.remove('active')); el.classList.add('active'); }

function fillBlank(letter, q) {
    let active = document.querySelector('.blank-slot.active'); if (!active) return;
    active.innerText = letter; active.classList.remove('active');
    let next = Array.from(document.querySelectorAll('.blank-slot')).find(e => e.innerText === '');
    if (next) selectBlank(next); else {
        let ans = Array.from(document.querySelectorAll('.blank-slot')).map(e => e.innerText).join('');
        let fb = document.getElementById('feedback');
        if (ans === q.ans.join('')) { fb.innerHTML = '✅ 拼写完美！'; fb.style.color = 'var(--success)'; speak(q.w); nextQuestionFast(); } 
        else {
            fb.innerHTML = '❌ 字母排错啦，重来！'; fb.style.color = 'var(--danger)'; recordMistake(q.w, q.zh);
            setTimeout(() => { document.querySelectorAll('.blank-slot').forEach(e => e.innerText = ''); selectBlank(document.querySelector('.blank-slot')); fb.innerText=''; }, 1200);
        }
    }
}

// ================= 渲染：2. 语音题 =================
function renderVoice(q, container) {
    container.innerHTML = `
        <div class="phonics-hint">${q.ph}</div>
        <button id="mic-btn" class="mic-btn" onclick="toggleRecord()">🎤</button>
        <p id="speech-result" style="font-size:22px;">点击麦克风大声读</p>
        <button onclick="overrideVoice()" style="margin-top:10px; background:none; border:2px solid #ccc; border-radius:10px; padding:5px 15px; cursor:pointer;">发音准没识别？点我强行通关</button>
    `;
}
function initSpeechRecognition() {
    window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    if (window.SpeechRecognition) {
        recognition = new window.SpeechRecognition(); recognition.lang = 'en-US';
        recognition.onstart = () => { document.getElementById('mic-btn').classList.add('recording'); document.getElementById('speech-result').innerText = '正在倾听...👂'; };
        recognition.onresult = (e) => { 
            let t = e.results[0][0].transcript.toLowerCase().trim(); 
            document.getElementById('speech-result').innerText = `听到: "${t}"`; 
            checkVoice(t); document.getElementById('mic-btn').classList.remove('recording'); 
        };
        recognition.onerror = () => { document.getElementById('speech-result').innerText = '没听清，再点一次。'; document.getElementById('mic-btn').classList.remove('recording'); };
    }
}
function toggleRecord() { if(recognition) try{ recognition.start(); }catch(e){ recognition.stop(); setTimeout(()=>recognition.start(),200); } else alert("浏览器不支持录音哦。"); }
function checkVoice(t) {
    let q = stages[currentStageIdx].data[currentQIdx];
    let key = q.w.toLowerCase().split(' ').filter(w=>w.length>2)[0] || q.w;
    let fb = document.getElementById('feedback');
    if (t.includes(key) || q.w.toLowerCase().includes(t)) { fb.innerHTML = '🌟 发音很棒！'; fb.style.color = 'var(--success)'; nextQuestionFast(); } 
    else { fb.innerHTML = '🤔 再大声点试一次！'; fb.style.color = 'var(--danger)'; recordMistake(q.w, q.zh); speak(q.w); }
}
function overrideVoice() { document.getElementById('feedback').innerHTML = '✅ 特批通关！'; document.getElementById('feedback').style.color = 'var(--success)'; nextQuestionFast(); }

// ================= 渲染：3. 句子题 =================
function renderSentence(q, container) {
    sentenceSelected =[]; let wordsArray = q.text.split(' ');
    container.innerHTML = `<div id="target-sentence" style="min-height:70px; border:4px dashed #7bed9f; border-radius:15px; padding:15px; margin-bottom:20px; display:flex; flex-wrap:wrap; gap:10px; justify-content:center; align-items:center; background:white;"></div>
        <div id="word-bank" class="options-grid" style="background:#f1f2f6; padding:20px; border-radius:15px;"></div>`;
    let bankArea = document.getElementById('word-bank');
    [...wordsArray].sort(() => Math.random() - 0.5).forEach(w => {
        let chip = document.createElement('div'); chip.className = 'opt-chip'; chip.innerText = w;
        chip.onclick = () => {
            speak(w); document.getElementById('target-sentence').appendChild(chip); sentenceSelected.push(w); chip.onclick = null; chip.style.background = '#eccc68';
            let isCorrect = sentenceSelected.every((val, index) => val === wordsArray[index]);
            let fb = document.getElementById('feedback');
            if (!isCorrect) { fb.innerHTML = '❌ 积木搭错啦！重搭'; fb.style.color = 'var(--danger)'; recordMistake(q.text, q.zh); setTimeout(loadQuestion, 1000); } 
            else if (sentenceSelected.length === wordsArray.length) { fb.innerHTML = '✅ 完美拼装！'; fb.style.color = 'var(--success)'; speak(q.text); nextQuestionFast(); }
        }; bankArea.appendChild(chip);
    });
}

// ================= 渲染：4. 词根实验室 (新增) =================
function renderLab(q, container) {
    container.innerHTML = `
        <div class="lab-equation">
            <span class="lab-box">${q.p1}</span> + 
            <span class="lab-drop" id="lab-target"> [ 选药水填入 ] </span> = 
            <span style="color:#747d8c; font-size:30px;">${q.res}</span>
        </div>
        <div class="options-grid" id="lab-opts"></div>
    `;
    let optsArea = document.getElementById('lab-opts');
    [...q.opts].sort(()=>Math.random() - 0.5).forEach(opt => {
        let btn = document.createElement('div'); btn.className = 'opt-chip'; btn.innerText = opt;
        btn.onclick = () => {
            speak(opt);
            let fb = document.getElementById('feedback');
            if(opt === q.ans) {
                document.getElementById('lab-target').innerText = opt;
                document.getElementById('lab-target').style.borderColor = '#2ed573';
                document.getElementById('lab-target').style.color = '#2ed573';
                fb.innerHTML = '🧪 合成成功！太棒了！'; fb.style.color = 'var(--success)';
                speak(q.res.replace(/[^a-zA-Z\s]/g, '')); // 读出结果(去掉emoji)
                nextQuestionFast();
            } else {
                fb.innerHTML = '💥 砰！合成失败，药水选错啦！'; fb.style.color = 'var(--danger)';
                recordMistake(q.res, q.q);
            }
        }; optsArea.appendChild(btn);
    });
}

</script>
</body>
</html>
