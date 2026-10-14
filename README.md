
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>HERO ARRIVAL | Emergency City</title>
<style>
* { box-sizing: border-box; }

:root {
  --cyan: #5deaff;
  --gold: #ffd36a;
}

body {
  margin: 0;
  color: white;
  font-family: system-ui, sans-serif;
  background: #080e20;
  overflow-x: hidden;
}

#scene {
  min-height: 100vh;
  min-height: 100svh;
  position: relative;
  overflow: hidden;
  isolation: isolate;
  background:
    radial-gradient(ellipse at 75% 30%, #6d215b66, transparent 36%),
    radial-gradient(ellipse at 45% 70%, #e54e2a33, transparent 45%),
    linear-gradient(180deg, #111d3b 0%, #3d354d 43%,
    #171d2c 72%, #080d18 100%);
  transition: filter .4s;
}

.sky {
  position: absolute;
  inset: 0;
  z-index: -1;
  overflow: hidden;
  background: linear-gradient(180deg, #17284955, transparent);
}

.moon {
  position: absolute;
  top: 7%;
  right: 13%;
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background: #d3f7ff;
  box-shadow: 0 0 70px #6fdfff99, 0 0 180px #419aff44;
  opacity: .65;
}

.city {
  position: absolute;
  bottom: 23%;
  left: -5%;
  right: -5%;
  height: 45%;
  display: flex;
  align-items: flex-end;
  gap: 5px;
  opacity: .8;
}

.building {
  flex: 1;
  min-width: 15px;
  height: var(--h);
  position: relative;
  background: linear-gradient(90deg, #111a2a, #29364b, #101726);
  border-top: 2px solid #72879c55;
}

.building::before {
  content: "";
  position: absolute;
  inset: 8px 5px;
  background: repeating-linear-gradient(
    0deg, transparent 0 14px, #ffbe6944 15px 19px
  );
  background-size: 100% 25px;
}

.building:nth-child(3n)::after {
  content: "";
  position: absolute;
  width: 4px;
  top: 10%;
  bottom: 0;
  left: 45%;
  background: #ff633b77;
  filter: blur(4px);
}

.smoke {
  position: absolute;
  bottom: 23%;
  width: 220px;
  height: 170px;
  border-radius: 50%;
  background: #9a91a722;
  filter: blur(35px);
  animation: smoke 7s ease-in-out infinite alternate;
}

.smoke.s1 { left: 8%; }
.smoke.s2 { right: 9%; animation-delay: -3s; }

@keyframes smoke {
  to { transform: translate(30px, -30px) scale(1.3); opacity: .4; }
}

.fire {
  position: absolute;
  bottom: 23%;
  left: 18%;
  font-size: 50px;
  filter: drop-shadow(0 0 20px #ff542d);
  animation: fire 1.4s infinite alternate;
}

@keyframes fire {
  to { transform: scale(1.2) rotate(5deg); }
}

.street {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 29%;
  background:
    linear-gradient(165deg, transparent 30%, #76839620 31%,
    transparent 32%),
    linear-gradient(180deg, #222a38, #080b13);
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}

.street::before {
  content: "";
  position: absolute;
  top: 35%;
  left: 0;
  width: 100%;
  height: 2px;
  background: #9cabb344;
  transform: rotate(-2deg);
}

.story {
  position: relative;
  z-index: 5;
  padding: 8vh 20px 35vh;
  text-align: center;
}

.eyebrow {
  color: var(--cyan);
  font-size: 11px;
  letter-spacing: .35em;
  font-weight: 800;
}

h1 {
  font-size: clamp(32px, 6vw, 68px);
  line-height: 1.15;
  margin: 15px 0;
  letter-spacing: .06em;
  text-shadow: 0 4px 30px #70dfff55;
}

.intro {
  color: #d0d6e5;
  font-size: 14px;
  line-height: 2;
}

.rescue-button {
  position: relative;
  margin-top: 22px;
  padding: 19px 38px;
  border: 1px solid #8af3ff;
  border-radius: 4px;
  background: linear-gradient(110deg, #0864a9, #182f71);
  color: white;
  font-size: 19px;
  font-weight: 900;
  letter-spacing: .12em;
  cursor: pointer;
  box-shadow: 0 0 25px #35d8ff55, inset 0 0 15px #54c9ff22;
  transition: .25s;
}

.rescue-button:hover {
  background: #1688bf;
  box-shadow: 0 0 45px #35d8ff99;
  transform: scale(1.04);
}

.rescue-button:disabled {
  cursor: wait;
  opacity: .7;
}

.rescue-button span {
  display: block;
  margin-top: 6px;
  font-size: 10px;
  font-weight: 400;
  letter-spacing: .1em;
}

.villain {
  position: absolute;
  z-index: 1;
  right: 8%;
  top: 24%;
  font-size: clamp(75px, 13vw, 155px);
  filter: drop-shadow(0 0 25px #e23dff88);
  animation: villainFloat 4s ease-in-out infinite;
  transition: opacity .5s, transform .7s;
}

@keyframes villainFloat {
  50% { transform: translateY(-12px) scale(1.03); }
}

.villain.defeated {
  opacity: .2;
  transform: translate(90px, 80px) scale(.7);
  filter: grayscale(1);
}

.villain-label {
  position: absolute;
  top: 23%;
  right: 8%;
  color: #ff9df7;
  font-size: 10px;
  letter-spacing: .2em;
  z-index: 2;
}

.citizen {
  position: absolute;
  bottom: 22%;
  left: 8%;
  font-size: clamp(45px, 7vw, 80px);
  z-index: 4;
  filter: drop-shadow(0 5px 5px #0008);
}

.citizen-text {
  position: absolute;
  z-index: 4;
  bottom: 31%;
  left: 5%;
  font-size: 12px;
  color: #fff0cc;
  background: #101827aa;
  padding: 8px 12px;
  border-left: 2px solid var(--gold);
}

#hero {
  position: absolute;
  z-index: 10;
  left: 50%;
  top: 45%;
  font-size: clamp(75px, 12vw, 135px);
  opacity: 0;
  pointer-events: none;
  transform: translate(-50%, -50%);
  filter: drop-shadow(0 0 15px #fff8);
  white-space: nowrap;
}

#hero.active { opacity: 1; }

#hero .hero-name {
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  white-space: nowrap;
  font-size: 13px;
  font-weight: 900;
  letter-spacing: .12em;
  padding: 8px 15px;
  background: #071323dd;
  border: 1px solid #ffffff55;
}

#hero.strong {
  animation: strongLanding 1.5s cubic-bezier(.15,.8,.2,1) forwards;
}

@keyframes strongLanding {
  0% { opacity: 0; top: -30%; transform: translate(-50%,-50%) scale(.25) rotate(-15deg); }
  35% { opacity: 1; top: 43%; transform: translate(-50%,-50%) scale(1.5) rotate(8deg); }
  48% { top: 36%; transform: translate(-50%,-50%) scale(1.15); }
  60% { top: 51%; transform: translate(-50%,-50%) scale(1.05, .7); }
  70% { top: 47%; transform: translate(-50%,-50%) scale(1); }
  100% { opacity: 1; top: 49%; transform: translate(-50%,-50%) scale(1); }
}

#hero.normal {
  animation: normalLanding 1.5s ease-out forwards;
}

@keyframes normalLanding {
  0% { opacity: 0; top: -20%; transform: translate(-50%,-50%) scale(.6); }
  55% { opacity: 1; top: 43%; transform: translate(-50%,-50%) scale(1); }
  75% { top: 49%; transform: translate(-50%,-50%) scale(.95); }
  100% { opacity: 1; top: 49%; transform: translate(-50%,-50%) scale(1); }
}

#hero.weak {
  animation: weakLanding 1.7s ease-in forwards;
}

@keyframes weakLanding {
  0% { opacity: 0; top: -15%; transform: translate(-50%,-50%) rotate(0) scale(.6); }
  45% { opacity: 1; top: 42%; transform: translate(-50%,-50%) rotate(180deg) scale(1.1); }
  72% { top: 58%; transform: translate(-50%,-50%) rotate(500deg) scale(.8); }
  85% { top: 60%; transform: translate(-50%,-50%) rotate(540deg) scale(.75); }
  100% { opacity: 1; top: 57%; transform: translate(-50%,-50%) rotate(540deg) scale(.8); }
}

#impact {
  position: absolute;
  z-index: 7;
  left: 50%;
  top: 53%;
  width: 20px;
  height: 20px;
  border: 3px solid white;
  border-radius: 50%;
  opacity: 0;
  pointer-events: none;
}

#impact.boom { animation: shockwave .9s ease-out; }

@keyframes shockwave {
  0% { opacity: 1; width: 10px; height: 10px; transform: translate(-50%,-50%); border-width: 8px; }
  100% { opacity: 0; width: 350px; height: 350px; transform: translate(-50%,-50%); border-width: 1px; }
}

#flash {
  position: absolute;
  z-index: 8;
  inset: 0;
  background: white;
  opacity: 0;
  pointer-events: none;
}

#flash.hit { animation: flash .5s ease-out; }

@keyframes flash {
  0% { opacity: .65; }
  100% { opacity: 0; }
}

#overlay {
  position: absolute;
  z-index: 12;
  inset: 0;
  opacity: 0;
  pointer-events: none;
  background: #04102055;
}

#overlay.show { animation: overlayFlash .8s ease-out; }

@keyframes overlayFlash {
  0%, 100% { opacity: 0; }
  30% { opacity: 1; }
}

#caption {
  position: absolute;
  z-index: 15;
  top: 70%;
  left: 50%;
  width: 90%;
  transform: translate(-50%, 10px);
  text-align: center;
  font-size: clamp(17px, 3vw, 30px);
  font-weight: 900;
  letter-spacing: .08em;
  text-shadow: 0 2px 20px #000;
  opacity: 0;
  pointer-events: none;
}

#caption.show {
  animation: captionIn .6s ease forwards;
}

@keyframes captionIn {
  to { opacity: 1; transform: translate(-50%, 0); }
}

.particle {
  position: absolute;
  z-index: 9;
  pointer-events: none;
  will-change: transform, opacity;
}

@media (max-width: 600px) {
  .story { padding-top: 6vh; padding-bottom: 35vh; }
  .intro { max-width: 320px; margin-inline: auto; }
  .rescue-button { padding: 16px 25px; }
  .villain { top: 38%; right: 4%; }
  .villain-label { top: 36%; right: 4%; }
  .citizen { left: 4%; }
  .citizen-text { left: 4%; bottom: 30%; }
  #hero { top: 48%; }
}
</style>
</head>

<body>
<div id="scene">
  <div class="sky">
    <div class="moon"></div>
    <div class="city" id="city"></div>
    <div class="smoke s1"></div>
    <div class="smoke s2"></div>
    <div class="fire">🔥</div>
    <div class="street"></div>
  </div>

  <div class="villain" id="villain">👿</div>
  <div class="villain-label">DANGER LEVEL : MAX</div>

  <div class="story">
    <div class="eyebrow">EMERGENCY TRANSMISSION // 001</div>
    <h1>THE CITY NEEDS A HERO.</h1>
    <p class="intro" id="intro">
      ヴィランに支配された街。<br>
      最後の希望は、あなたの救援要請だけ。
    </p>
    <button class="rescue-button" id="call">
      ヒーローを呼ぶ
      <span>PRESS TO REQUEST BACKUP</span>
    </button>
  </div>

  <div class="citizen">🧎</div>
  <div class="citizen-text" id="citizenText">
    「誰か……助けてくれ！」
  </div>

  <div id="hero"></div>
  <div id="impact"></div>
  <div id="flash"></div>
  <div id="overlay"></div>
  <div id="caption"></div>
</div>

<script>
const $ = id => document.getElementById(id);

const scene = $("scene");
const hero = $("hero");
const impact = $("impact");
const flash = $("flash");
const overlay = $("overlay");
const caption = $("caption");
const call = $("call");
const villain = $("villain");
const intro = $("intro");
const citizenText = $("citizenText");

const heroes = [
  {
    id: "strong",
    name: "最強のヒーロー",
    emoji: "🦸",
    title: "「この街には、指一本触れさせない。」",
    description: "超高速で飛来！大地を揺るがすヒーロー着地！",
    color: "#ffd66b",
    weight: 1
  },
  {
    id: "normal",
    name: "普通のヒーロー",
    emoji: "🦸‍♂️",
    title: "「待たせたな。あとは任せてくれ！」",
    description: "空から颯爽と登場。頼れる正統派ヒーロー。",
    color: "#72e5ff",
    weight: 3
  },
  {
    id: "weak",
    name: "弱小ヒーロー",
    emoji: "🦸‍♀️",
    title: "「だ、大丈夫！たぶん助けられます！」",
    description: "着地失敗！でも、勇気だけは誰にも負けない。",
    color: "#ffb7cb",
    weight: 3
  }
];

// 街のビルを自動生成
for (let i = 0; i < 30; i++) {
  const building = document.createElement("div");
  building.className = "building";
  building.style.setProperty("--h", (25 + Math.random() * 75) + "%");
  $("city").appendChild(building);
}

let busy = false;
let previous = -1;
let timers = [];

function later(fn, ms) {
  const t = setTimeout(fn, ms);
  timers.push(t);
}

function clearTimers() {
  timers.forEach(clearTimeout);
  timers = [];
}

function chooseHero() {
  // 直前と同じヒーローが連続しないようにする
  const pool = heroes
    .map((h, i) => ({ ...h, index: i }))
    .filter(h => h.index !== previous);

  const total = pool.reduce((sum, h) => sum + h.weight, 0);
  let r = Math.random() * total;

  for (const h of pool) {
    r -= h.weight;
    if (r <= 0) {
      previous = h.index;
      return h;
    }
  }
  return pool[0];
}

function effect(el, className) {
  el.classList.remove(className);
  void el.offsetWidth;
  el.classList.add(className);
}

function particle(x, y, emoji, dx, dy, duration, size) {
  const p = document.createElement("div");
  p.className = "particle";
  p.textContent = emoji;
  p.style.left = x + "px";
  p.style.top = y + "px";
  p.style.fontSize = size + "px";
  scene.appendChild(p);

  const animation = p.animate([
    { transform: "translate(-50%,-50%) scale(.3)", opacity: 0 },
    { opacity: 1, offset: .15 },
    {
      transform: `translate(calc(-50% + ${dx}px), calc(-50% + ${dy}px)) scale(1.2)`,
      opacity: 0
    }
  ], {
    duration,
    easing: "cubic-bezier(.2,.7,.3,1)"
  });

  animation.onfinish = () => p.remove();
}

function burst(count, emoji, spread = 200) {
  const x = innerWidth / 2;
  const y = innerHeight * .53;

  for (let i = 0; i < count; i++) {
    const angle = Math.random() * Math.PI * 2;
    const distance = spread * (.4 + Math.random());
    particle(
      x, y, emoji,
      Math.cos(angle) * distance,
      Math.sin(angle) * distance,
      600 + Math.random() * 700,
      12 + Math.random() * 25
    );
  }
}

function arrival(h) {
  hero.className = "";
  hero.innerHTML = `${h.emoji}<div class="hero-name">${h.name}</div>`;
  hero.style.filter = `drop-shadow(0 0 22px ${h.color})`;
  hero.style.color = h.color;
  void hero.offsetWidth;
  hero.classList.add("active", h.id);

  intro.innerHTML = h.description;
  citizenText.textContent = "「ヒーローが来てくれた……！」";

  caption.textContent = h.title;
  caption.style.color = h.color;
  effect(caption, "show");

  if (h.id === "strong") {
    later(() => {
      effect(flash, "hit");
      effect(impact, "boom");
      effect(overlay, "show");
      burst(35, "⚡", 280);
      burst(22, "💥", 200);
      scene.animate([
        { transform: "translate(0,0)" },
        { transform: "translate(-8px,4px)" },
        { transform: "translate(8px,-4px)" },
        { transform: "translate(-5px,2px)" },
        { transform: "translate(0,0)" }
      ], { duration: 450 });
    }, 650);
  }

  if (h.id === "normal") {
    later(() => {
      burst(15, "✨", 150);
      burst(12, "💨", 110);
    }, 650);
  }

  if (h.id === "weak") {
    later(() => {
      burst(12, "💫", 100);
      burst(8, "💨", 70);
    }, 850);
  }

  later(() => {
    villain.classList.add("defeated");
    citizenText.textContent =
      h.id === "weak"
        ? "「転んでるけど……ありがとう！」"
        : "「街に平和が戻ってきた！」";

    statusMessage(h);
    call.disabled = false;
    call.innerHTML =
      "もう一度ヒーローを呼ぶ" +
      "<span>CALL ANOTHER HERO</span>";
    busy = false;
  }, 2300);
}

function statusMessage(h) {
  caption.textContent =
    h.id === "weak"
      ? "MISSION... なんとか成功？"
      : "MISSION COMPLETE — CITY SECURED";
}

call.addEventListener("click", () => {
  if (busy) return;
  busy = true;
  call.disabled = true;

  clearTimers();

  villain.classList.remove("defeated");
  hero.className = "";
  caption.className = "";
  caption.style.opacity = "0";
  caption.style.animation = "none";
  void caption.offsetWidth;
  caption.style.animation = "";

  const h = chooseHero();

  intro.innerHTML = "救援信号を送信中……<br>ヒーローの到着を待て！";
  citizenText.textContent = "「お願い……間に合ってくれ！」";
  call.innerHTML = "救援信号送信中…<span>INCOMING TRANSMISSION</span>";

  // 飛来前の警告演出
  later(() => {
    caption.textContent = "INCOMING HERO DETECTED";
    caption.style.color = "#ffffff";
    effect(caption, "show");
    burst(12, "✨", 130);
  }, 350);

  // ヒーロー着地
  later(() => arrival(h), 850);

  // 再登場まで待てるようにする
  later(() => {
    hero.className = "";
    caption.classList.remove("show");
    call.disabled = false;
    call.innerHTML =
      "もう一度ヒーローを呼ぶ" +
      "<span>CALL ANOTHER HERO</span>";
    busy = false;
  }, 6500);
});
</script>
</body>
</html>
# 245001
