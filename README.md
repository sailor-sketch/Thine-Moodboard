[index.html.txt](https://github.com/user-attachments/files/24484064/index.html.txt)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thine Moodboard ✨</title>
<link href="https://fonts.googleapis.com/css2?family=Hind:wght@400;700&family=Noto+Sans+JP:wght@400;700&family=Noto+Sans+KR:wght@400;700&family=Noto+Sans+SC:wght@400;700&display=swap" rel="stylesheet">
<style>
:root {
--bg-color: #ffcce6;
--dot-color: #ffffff;
--frame-bg: #fffcfd;
--accent-main: #ff85c2;
--accent-dark: #d63384;
--card-bg: #ffffff;
--text-color: #d63384;
--border-color: #ffb3d9;
--sparkle-color: #fff;
}

[data-theme="dark"] {
--bg-color: #0a0a0a;
--dot-color: #220000;
--frame-bg: #000000;
--accent-main: #b30000;
--accent-dark: #ff4d4d;
--card-bg: #151515;
--text-color: #ff4d4d;
--border-color: #440000;
--sparkle-color: #ff0000;
}

body {
background-color: var(--bg-color);
background-image: radial-gradient(var(--dot-color) 15%, transparent 16%);
background-size: 30px 30px;
font-family: 'Segoe UI', 'Noto Sans JP', 'Noto Sans SC', 'Noto Sans KR', 'Hind', sans-serif;
display: flex;
justify-content: center;
padding: 40px 20px;
color: var(--text-color);
transition: background-color 0.8s ease, color 0.5s ease;
min-height: 100vh;
margin: 0;
overflow-x: hidden;
}

.sparkle {
position: fixed;
pointer-events: none;
background: var(--sparkle-color);
border-radius: 50%;
z-index: 9999;
animation: fadeOut 0.8s linear forwards;
}

@keyframes fadeOut {
0% { transform: scale(1); opacity: 1; }
100% { transform: scale(0); opacity: 0; }
}

.main-frame {
background: var(--frame-bg);
border: 10px double var(--border-color);
border-radius: 40px;
width: 100%;
max-width: 1000px;
padding: 40px 20px;
position: relative;
box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
text-align: center;
box-sizing: border-box;
}

.bow { position: absolute; font-size: 60px; top: -35px; z-index: 2; }
.left-bow { left: -20px; }
.right-bow { right: -20px; }

h1 {
font-family: 'Brush Script MT', cursive;
font-size: clamp(2.5rem, 8vw, 4rem);
margin: 0 0 20px 0;
color: var(--accent-main);
text-shadow: 2px 2px var(--frame-bg);
}

nav {
margin-bottom: 30px;
display: flex;
flex-wrap: wrap;
justify-content: center;
gap: 10px;
}

.nav-btn, .lang-select {
background: var(--card-bg);
color: var(--accent-main);
border: 2px solid var(--accent-main);
padding: 10px 20px;
border-radius: 50px;
cursor: pointer;
font-weight: bold;
transition: 0.3s;
font-size: 0.9rem;
}

.nav-btn:hover {
background: var(--accent-main);
color: white;
transform: translateY(-2px);
}

.grid {
display: grid;
grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
gap: 30px;
padding: 10px;
}

.card {
background: var(--card-bg);
padding: 15px 15px 45px 15px;
box-shadow: 0 10px 20px rgba(0,0,0,0.1);
border: 1px solid var(--border-color);
transition: 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
position: relative;
}

.card:hover { transform: rotate(-3deg) translateY(-8px); }

.card-img-container {
width: 100%;
height: 220px;
background: #111;
display: flex;
align-items: center;
justify-content: center;
overflow: hidden;
}

.card-img-container img { width: 100%; height: 100%; object-fit: cover; }

.card-title {
margin-top: 15px;
font-weight: bold;
font-size: 1.1rem;
word-wrap: break-word;
}

#fileInput { display: none; }

.footer {
margin-top: 40px;
font-size: 0.8rem;
opacity: 0.7;
font-style: italic;
}
</style>
</head>
<body data-theme="light">

<div class="main-frame">
<div class="bow left-bow">🎀</div>
<div class="bow right-bow">🎀</div>

<h1 id="mainTitle">Thine Moodboard</h1>

<nav>
<button class="nav-btn" onclick="document.getElementById('fileInput').click()" id="addBtn">🌸 Add Idea</button>
<button class="nav-btn" onclick="toggleTheme()" id="themeBtn">🌓 Mode</button>
<select class="lang-select" onchange="changeLang(this.value)" id="langPicker">
<option value="en">English</option>
<option value="es">Español</option>
<option value="fr">Français</option>
<option value="ko">한국어</option>
<option value="zh">中文</option>
<option value="ja">日本語</option>
<option value="hi">हिन्दी</option>
</select>
<button class="nav-btn" onclick="clearAll()" id="clearBtn" style="opacity: 0.5;">Reset</button>
</nav>

<input type="file" id="fileInput" accept="image/*" onchange="handleImage(this)">

<div class="grid" id="ideaGrid"></div>

<div class="footer" id="footerText">✨ Organize Your Dreams ✨</div>
</div>

<script>
const translations = {
en: { title: "Thine Moodboard", add: "🌸 Add Idea", theme: "🌓 Mode", clear: "Reset", prompt: "Idea name:", defaultTitle: "New Inspiration", footer: "✨ Organize Your Dreams ✨" },
es: { title: "Tu Moodboard", add: "🌸 Añadir Idea", theme: "🌓 Modo", clear: "Limpiar", prompt: "Nombre de la idea:", defaultTitle: "Nueva Inspiración", footer: "✨ Organiza tus Sueños ✨" },
fr: { title: "Ton Moodboard", add: "🌸 Ajouter une Idée", theme: "🌓 Mode", clear: "Réinitialiser", prompt: "Nom de l'idée:", defaultTitle: "Nouvelle Inspiration", footer: "✨ Organisez Vos Rêves ✨" },
ko: { title: "나의 무드보드", add: "🌸 아이디어 추가", theme: "🌓 모드", clear: "초기화", prompt: "아이디어 이름:", defaultTitle: "새로운 영감", footer: "✨ 당신의 꿈을 정리하세요 ✨" },
zh: { title: "你的情绪板", add: "🌸 添加创意", theme: "🌓 模式", clear: "重置", prompt: "创意名称:", defaultTitle: "新灵感", footer: "✨ 整理你的梦想 ✨" },
ja: { title: "あなたのムードボード", add: "🌸 アイデアを追加", theme: "🌓 モード", clear: "リセット", prompt: "アイデアの名前:", defaultTitle: "新しいインスピレーション", footer: "✨ 夢を整理しましょう ✨" },
hi: { title: "आपका मूडबोर्ड", add: "🌸 विचार जोड़ें", theme: "🌓 मोड", clear: "रीसेट", prompt: "विचार का नाम:", defaultTitle: "नई प्रेरणा", footer: "✨ अपने सपनों को व्यवस्थित करें ✨" }
};

let currentLang = localStorage.getItem('hubLang') || 'en';

function changeLang(lang) {
currentLang = lang;
localStorage.setItem('hubLang', lang);
updateUI();
}

function updateUI() {
const t = translations[currentLang];
document.getElementById('mainTitle').innerText = t.title;
document.getElementById('addBtn').innerText = t.add;
document.getElementById('themeBtn').innerText = t.theme;
document.getElementById('clearBtn').innerText = t.clear;
document.getElementById('footerText').innerText = t.footer;
document.getElementById('langPicker').value = currentLang;
}

document.addEventListener('mousemove', (e) => {
const sparkle = document.createElement('div');
sparkle.className = 'sparkle';
const size = Math.random() * 8 + 2;
sparkle.style.width = sparkle.style.height = `${size}px`;
sparkle.style.left = `${e.clientX}px`;
sparkle.style.top = `${e.clientY}px`;
document.body.appendChild(sparkle);
setTimeout(() => sparkle.remove(), 800);
});

function toggleTheme() {
const body = document.body;
const newTheme = body.getAttribute('data-theme') === 'light' ? 'dark' : 'light';
body.setAttribute('data-theme', newTheme);
localStorage.setItem('hubTheme', newTheme);
}

function handleImage(input) {
if (input.files && input.files[0]) {
const reader = new FileReader();
const title = prompt(translations[currentLang].prompt, translations[currentLang].defaultTitle);
if (!title) return;

reader.onload = (e) => {
const imageData = e.target.result;
saveIdea(title, imageData);
renderCard(title, imageData);
};
reader.readAsDataURL(input.files[0]);
}
}

function saveIdea(title, image) {
let ideas = JSON.parse(localStorage.getItem('hubIdeas')) || [];
ideas.push({ title, image });
localStorage.setItem('hubIdeas', JSON.stringify(ideas));
}

function renderCard(title, image) {
const grid = document.getElementById('ideaGrid');
const card = document.createElement('div');
card.className = 'card';
card.innerHTML = `<div class="card-img-container"><img src="${image}"></div><div class="card-title">${title}</div>`;
grid.prepend(card);
}

function clearAll() {
if(confirm("Delete everything?")) {
localStorage.removeItem('hubIdeas');
location.reload();
}
}

window.onload = () => {
updateUI();
document.body.setAttribute('data-theme', localStorage.getItem('hubTheme') || 'light');
const ideas = JSON.parse(localStorage.getItem('hubIdeas')) || [];
ideas.forEach(item => renderCard(item.title, item.image));
};
</script>
</body>
</html>
