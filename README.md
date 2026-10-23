# --1[index.html](https://github.com/user-attachments/files/33872296/index.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<title>魔法师分类收纳</title>
<style>
/* ============ 基础 ============ */
*{ box-sizing: border-box; margin:0; padding:0; }
html,body{ height:100%; overflow:hidden; }
body{
  font-family: "Georgia", "Songti SC", "Noto Serif SC", "Microsoft YaHei", serif;
  color:#e9e2ff;
  background:
    radial-gradient(circle at 50% 8%, rgba(124,84,224,.34), transparent 56%),
    radial-gradient(circle at 12% 72%, rgba(40,110,200,.20), transparent 52%),
    radial-gradient(circle at 88% 38%, rgba(178,58,200,.14), transparent 46%),
    linear-gradient(180deg,#0a0716 0%, #120a26 46%, #090512 100%);
  user-select:none; -webkit-user-select:none;
  -webkit-tap-highlight-color:transparent;
  touch-action:none;
  overflow:hidden;
}
#stage{ position:fixed; inset:0; overflow:hidden; }

/* ============ 背景星尘 ============ */
#stars,.bg-dust{ position:absolute; inset:0; pointer-events:none; }
.star{
  position:absolute; border-radius:50%; background:#fff;
  box-shadow:0 0 6px rgba(200,180,255,.9);
  animation: twinkle var(--t,3s) ease-in-out infinite alternate;
}
@keyframes twinkle{ from{ opacity:.12; transform:scale(.6) } to{ opacity:.95; transform:scale(1) } }

.mote{
  position:absolute; bottom:-12px; width:5px; height:5px; border-radius:50%;
  background: radial-gradient(circle,#f2e9ff,#9d7bff 55%, rgba(157,123,255,0) 72%);
  animation: rise linear infinite;
  opacity:0;
}
@keyframes rise{
  0%{ transform: translate3d(0,0,0) scale(.6); opacity:0 }
  12%{ opacity:.85 }
  80%{ opacity:.35 }
  100%{ transform: translate3d(var(--dx,26px),-74vh,0) scale(1.1); opacity:0 }
}
.vignette{
  position:absolute; inset:0; pointer-events:none;
  background: radial-gradient(ellipse at 50% 42%, transparent 40%, rgba(4,2,10,.55) 100%);
}

/* ============ HUD ============ */
.hud{
  position:absolute; top:14px; left:0; right:0; text-align:center;
  z-index:30; pointer-events:none;
}
.hud .title{
  font-size: clamp(16px, 2vw, 24px);
  letter-spacing:.34em; text-indent:.34em;
  color:#efe7ff;
  text-shadow: 0 0 16px rgba(160,120,255,.85), 0 0 46px rgba(110,70,220,.55);
}
.hud .sub{
  margin-top:7px; font-size:11.5px; letter-spacing:.16em; color:#9d8fc9;
}
.hud-right{
  position:absolute; top:16px; right:18px; z-index:31;
  display:flex; align-items:center; gap:10px;
}
.pill{
  font-size:12.5px; letter-spacing:.1em; color:#d8ccff;
  padding:7px 14px; border-radius:999px;
  background: linear-gradient(180deg, rgba(120,90,220,.28), rgba(60,40,130,.24));
  border:1px solid rgba(160,130,255,.35);
  box-shadow: 0 0 18px rgba(120,80,240,.25), inset 0 1px 0 rgba(255,255,255,.12);
  backdrop-filter: blur(6px);
}
.pill b{ color:#fff; font-weight:600; }
.icon-btn{
  width:34px; height:34px; border-radius:50%; cursor:pointer;
  font-size:15px; line-height:1; color:#dcd2ff;
  background: linear-gradient(180deg, rgba(120,90,220,.24), rgba(50,34,110,.3));
  border:1px solid rgba(160,130,255,.35);
  box-shadow: 0 0 14px rgba(120,80,240,.25), inset 0 1px 0 rgba(255,255,255,.12);
  display:grid; place-items:center;
  transition: transform .18s, box-shadow .25s, color .2s;
}
.icon-btn:hover{ transform: translateY(-2px); color:#fff; box-shadow:0 0 22px rgba(160,120,255,.55); }
.icon-btn:active{ transform: scale(.94); }

/* ============ 工作台 ============ */
.bench{
  position:absolute; left:0; right:0; bottom:0; height:41%;
  z-index:3;
  background:
    repeating-linear-gradient(91deg,
      rgba(0,0,0,.13) 0 1px,
      rgba(255,255,255,.028) 1px 4px,
      rgba(0,0,0,.05) 4px 9px,
      rgba(255,255,255,.02) 9px 15px,
      rgba(0,0,0,0) 15px 26px),
    radial-gradient(ellipse at 50% 0%, rgba(255,190,120,.14), transparent 60%),
    linear-gradient(180deg,#7b5030 0%, #633d21 26%, #4a2b16 60%, #331d0e 100%);
  box-shadow: 0 -22px 50px rgba(0,0,0,.55);
}
.bench::before{
  content:''; position:absolute; left:0; right:0; top:0; height:14px;
  background: linear-gradient(180deg, #a2714688, #6b432688 55%, transparent);
  border-top:2px solid rgba(255,214,160,.35);
  box-shadow: 0 6px 18px rgba(0,0,0,.4), inset 0 2px 0 rgba(255,230,190,.22);
}
.bench::after{
  content:''; position:absolute; inset:0; pointer-events:none;
  background:
    radial-gradient(circle at 22% 42%, rgba(0,0,0,.22) 0 22px, transparent 42px),
    radial-gradient(circle at 71% 68%, rgba(0,0,0,.16) 0 16px, transparent 34px),
    radial-gradient(circle at 88% 30%, rgba(0,0,0,.16) 0 12px, transparent 30px),
    linear-gradient(180deg, rgba(0,0,0,.28), transparent 22%, transparent 70%, rgba(0,0,0,.42));
  mix-blend-mode: multiply;
}
.bench-lip{
  position:absolute; left:0; right:0; bottom:0; height:26px; z-index:4;
  background: linear-gradient(180deg,#2a180c,#180d06);
  box-shadow: inset 0 2px 0 rgba(255,200,140,.14);
}
.carve{
  position:absolute; bottom:6px; left:50%; transform:translateX(-50%);
  font-size:11px; letter-spacing:.55em; color:rgba(255,214,160,.20);
  z-index:5; white-space:nowrap;
}

/* ============ 魔法阵 ============ */
.circle-wrap{
  position:absolute; left:50%; top:31%;
  transform: translate(-50%,-50%);
  z-index:6; pointer-events:none;
}
.circle{
  position:relative; width:var(--cs); height:var(--cs);
  animation: breathe 5.5s ease-in-out infinite;
  transition: filter .6s;
}
@keyframes breathe{
  0%,100%{ transform: scale(1); filter: brightness(1) }
  50%    { transform: scale(1.035); filter: brightness(1.16) }
}
.circle .glow{
  position:absolute; inset:-16%; border-radius:50%;
  background: radial-gradient(circle, rgba(146,104,255,.32) 0%, rgba(92,58,204,.16) 44%, rgba(60,30,140,0) 70%);
  filter: blur(14px);
  animation: glowPulse 5.5s ease-in-out infinite;
  transition: background .6s;
}
@keyframes glowPulse{
  0%,100%{ opacity:.5; transform: scale(.97) }
  50%    { opacity:1;  transform: scale(1.06) }
}
.ring{ position:absolute; border-radius:50%; }
.r1{
  inset:3%;
  border:2px solid rgba(176,146,255,.5);
  box-shadow: 0 0 26px rgba(140,100,255,.45), inset 0 0 44px rgba(120,80,240,.22);
  animation: spin 48s linear infinite;
}
.r2{
  inset:14%;
  border:2px dashed rgba(206,188,255,.28);
  animation: spin 72s linear infinite reverse;
}
.r3{
  inset:0; border:none;
  background: repeating-conic-gradient(from 0deg, rgba(196,168,255,.55) 0deg .8deg, transparent .8deg 12deg);
  -webkit-mask: radial-gradient(closest-side, transparent 0 88%, #000 89% 96%, transparent 97%);
          mask: radial-gradient(closest-side, transparent 0 88%, #000 89% 96%, transparent 97%);
  animation: spin 120s linear infinite reverse;
}
/* 齿轮纹理环：细齿贴着槽位外侧慢速转动 */
.ring.gear{
  inset:7%;
  background: repeating-conic-gradient(from 0deg, rgba(198,170,255,.5) 0deg 4.5deg, transparent 4.5deg 10deg);
  -webkit-mask: radial-gradient(closest-side, transparent 0 93%, #000 94% 100%);
          mask: radial-gradient(closest-side, transparent 0 93%, #000 94% 100%);
  animation: spin 26s linear infinite;
  opacity:.85;
}
/* 内圈虚线弧环 */
.ring.arcs{
  inset:28%;
  border:3px dashed rgba(206,188,255,.42);
  animation: spin 38s linear infinite reverse;
}
/* 内圈细实线环 */
.ring.thin{
  inset:23.5%;
  border:1px solid rgba(176,146,255,.3);
  animation: spin 70s linear infinite;
}
/* 环绕光点：沿着法阵轨道游走 */
.orbit{ position:absolute; inset:0; animation: spin 13s linear infinite; }
.orbit i{
  position:absolute; left:50%; top:50%; width:7px; height:7px; margin:-3.5px;
  border-radius:50%;
  background: radial-gradient(circle,#fff,#c9a9ff 55%, rgba(160,120,255,0) 75%);
  box-shadow: 0 0 12px rgba(190,160,255,.95);
  transform: rotate(var(--oa)) translateY(calc(var(--cs) * -0.16));
}
.orbit i:nth-child(2){ animation: twinkle 1.3s ease-in-out infinite alternate; }
.orbit i:nth-child(3){ animation: twinkle 1.9s ease-in-out infinite alternate; }
/* 从核心向外扩散的能量脉冲环 */
.pulse{
  position:absolute; left:50%; top:50%; width:26%; height:26%;
  border-radius:50%;
  border:2px solid rgba(196,168,255,.6);
  box-shadow: 0 0 18px rgba(160,120,255,.5);
  transform: translate(-50%,-50%) scale(.35);
  animation: pulseOut 4.4s cubic-bezier(.2,.6,.4,1) infinite;
}
.pulse.p2{ animation-delay: 2.2s; }
@keyframes pulseOut{
  0%{ transform: translate(-50%,-50%) scale(.35); opacity:.85 }
  70%{ opacity:.15 }
  100%{ transform: translate(-50%,-50%) scale(3.2); opacity:0 }
}
@keyframes spin{ to{ transform: rotate(360deg) } }

.glyph{ position:absolute; inset:16%; width:68%; height:68%; animation: spin 160s linear infinite; }
.glyph2{ position:absolute; inset:31%; width:38%; height:38%; animation: spin 44s linear infinite reverse; opacity:.65; }

.runes{ position:absolute; inset:6%; animation: spin 96s linear infinite; }
.runes span{
  position:absolute; left:50%; top:50%;
  font-size: calc(var(--cs) * 0.026);
  color:#cbb8ff;
  text-shadow: 0 0 12px rgba(160,120,255,.95);
  opacity:.7;
  transform: translate(-50%,-50%) rotate(var(--a)) translateY(calc(var(--cs) * -0.442)) rotate(calc(var(--a) * -1));
}
.core{
  position:absolute; left:50%; top:50%; width:13%; height:13%;
  transform: translate(-50%,-50%);
  border-radius:50%;
  background: radial-gradient(circle at 50% 45%, #fff 0 8%, #ded0ff 22%, #8d6cf2 58%, rgba(88,48,200,0) 76%);
  box-shadow: 0 0 46px rgba(160,120,255,.75);
  animation: corePulse 3.6s ease-in-out infinite;
}
@keyframes corePulse{
  0%,100%{ transform: translate(-50%,-50%) scale(.9); opacity:.8 }
  50%    { transform: translate(-50%,-50%) scale(1.12); opacity:1 }
}

/* ============ 槽位 ============ */
.slots{ position:absolute; left:50%; top:31%; width:0; height:0; z-index:7; pointer-events:none; }
.slot{
  position:absolute; transform: translate(-50%,-50%);
  width: calc(var(--cs) * 0.125); height: calc(var(--cs) * 0.125);
  border-radius:50%;
  display:grid; place-items:center;
  background: radial-gradient(circle at 50% 38%, rgba(152,122,255,.20), rgba(74,52,160,.10) 66%, rgba(40,24,90,.02) 72%);
  border:1.5px dashed rgba(186,164,255,.42);
  box-shadow: inset 0 0 18px rgba(120,86,240,.34), 0 0 0 0 rgba(160,120,255,0);
  transition: border-color .28s, box-shadow .28s, background .28s, transform .22s;
  will-change: transform;
}
.slot .ghost{
  display:grid; place-items:center;
  opacity:.3;
  filter: saturate(.8) brightness(1.15);
  transition: opacity .3s;
}
/* Emoji 类槽位虚影 → 白色剪影 */
.slot .ghost .art.emoji{
  filter: brightness(0) invert(1);
  opacity:.42;
}
.slot .count{
  position:absolute; right:-5px; bottom:-5px;
  min-width:20px; height:18px; padding:0 5px;
  display:grid; place-items:center;
  font-size:10.5px; letter-spacing:.02em;
  color:#e8ddff; border-radius:999px;
  background: linear-gradient(180deg, rgba(110,80,210,.9), rgba(58,38,128,.9));
  border:1px solid rgba(180,150,255,.45);
  box-shadow: 0 0 12px rgba(120,80,240,.45);
  font-family: "Segoe UI", sans-serif;
}
#stage.dragging .slot{ border-color: rgba(200,180,255,.62); }
.slot.hover{
  transform: translate(-50%,-50%) scale(1.09);
  border-color:#e3d6ff;
  background: radial-gradient(circle at 50% 38%, rgba(190,160,255,.34), rgba(90,64,180,.18) 68%, transparent 74%);
  box-shadow: inset 0 0 22px rgba(170,130,255,.6), 0 0 24px rgba(170,130,255,.55);
}
.slot.hover .ghost{ opacity:.6; }
.slot.flash{ animation: slotFlash .62s ease-out; }
@keyframes slotFlash{
  0%{ box-shadow: 0 0 0 0 rgba(255,255,255,.9), inset 0 0 26px rgba(200,170,255,.9); border-color:#fff }
  40%{ box-shadow: 0 0 30px 10px rgba(190,150,255,.55), inset 0 0 30px rgba(220,200,255,.7); border-color:#fff }
  100%{ box-shadow: 0 0 0 0 rgba(255,255,255,0), inset 0 0 18px rgba(120,86,240,.34); }
}
.slot.bad{ animation: slotBad .5s ease; border-color:#ff7a9a; }
@keyframes slotBad{
  0%,100%{ transform: translate(-50%,-50%) scale(1) }
  25%{ transform: translate(calc(-50% - 5px),-50%) scale(1.04) }
  60%{ transform: translate(calc(-50% + 5px),-50%) scale(1.04) }
}
.slot.done{ border-style:solid; border-color: rgba(255,226,150,.55); box-shadow: inset 0 0 22px rgba(255,208,120,.28), 0 0 20px rgba(255,206,120,.28); }
.slot.done .count{ background: linear-gradient(180deg,#e0aa46,#8a5f1c); color:#2a1a05; border-color:rgba(255,236,180,.7); }
.slot.done .ghost{ opacity:.12; }

/* ============ 物品 ============ */
.items{ position:absolute; inset:0; z-index:9; pointer-events:none; }
.item{
  position:absolute;
  display:grid; place-items:center;
  transform: translate(-50%,-50%) rotate(var(--r,0deg)) scale(var(--s,1)) translate(var(--jx,0px), var(--jy,0px));
  transition: left .34s cubic-bezier(.34,1.42,.6,1),
              top  .34s cubic-bezier(.34,1.42,.6,1),
              transform .26s cubic-bezier(.34,1.42,.6,1);
  cursor:grab; pointer-events:auto; touch-action:none;
  will-change: left, top, transform;
  -webkit-user-drag:none;
}
.item::after{
  content:''; position:absolute; left:50%; bottom:-2px; width:46px; height:10px;
  transform: translateX(-50%);
  border-radius:50%;
  background: radial-gradient(rgba(0,0,0,.55), rgba(0,0,0,0) 72%);
  filter: blur(3px);
  opacity:.7;
  pointer-events:none;
}
.item-inner{
  display:grid; place-items:center; position:relative; z-index:1;
  animation: bob var(--dur,4s) ease-in-out infinite;
  animation-delay: var(--delay,0s);
  pointer-events:none;
}
@keyframes bob{
  0%,100%{ transform: translateY(-4px) rotate(-1deg) }
  50%    { transform: translateY(4px) rotate(1deg) }
}
.item.dragging{ transition:none; cursor:grabbing; }
/* 被青蛙挤开时：带过冲的弹性位移 */
.item.jolt{ transition: transform .5s cubic-bezier(.22,1.8,.4,1); }
.item.dragging .item-inner{ animation-play-state: paused; }
.item.dragging::after{ opacity:.3; }
.item.placed{ cursor:default; }
.item.reject .item-inner{ animation: shake .46s ease; }
@keyframes shake{
  0%,100%{ transform: translate(0,0) }
  15%{ transform: translate(-5px,-2px) rotate(-4deg) }
  35%{ transform: translate(5px,1px) rotate(4deg) }
  55%{ transform: translate(-3px,-1px) rotate(-2deg) }
  78%{ transform: translate(2px,0) rotate(2deg) }
}
.item.hint{ animation: hintPulse 1.6s ease-in-out 3; }
@keyframes hintPulse{
  0%,100%{ filter:none }
  50%{ filter: drop-shadow(0 0 14px rgba(255,220,140,.9)) }
}

/* ============ CSS 手绘物品 ============ */
.art{ position:relative; }
.art i{ display:block; position:absolute; font-style:normal; }

/* 药水瓶 */
.art.potion{ width:46px; height:58px; }
.art.potion .body{
  left:0; bottom:0; width:46px; height:40px;
  border-radius:15px 15px 19px 19px / 11px 11px 21px 21px;
  background: linear-gradient(175deg, rgba(232,242,255,.24), rgba(150,175,230,.12));
  border:2px solid rgba(216,230,255,.48);
  box-shadow: inset -4px -5px 10px rgba(0,10,30,.28), 0 0 16px rgba(140,180,255,.22);
  overflow:hidden;
}
.art.potion .liquid{
  left:-2px; right:-2px; bottom:-2px; height:66%;
  border-radius:0 0 19px 19px;
  background: linear-gradient(180deg, var(--liq1), var(--liq2));
  box-shadow: inset 0 4px 0 rgba(255,255,255,.35);
}
.art.potion.red{ --liq1:#ff7a94; --liq2:#a5103c; }
.art.potion.blue{ --liq1:#7ad9ff; --liq2:#13439f; }
.art.potion .shine{
  left:6px; top:6px; width:7px; height:16px; border-radius:50%;
  background: linear-gradient(rgba(255,255,255,.8), rgba(255,255,255,0));
  transform: rotate(12deg);
}
.art.potion .neck{
  left:50%; bottom:38px; width:16px; height:13px; margin-left:-8px;
  background: rgba(200,222,255,.18);
  border-left:2px solid rgba(216,230,255,.45);
  border-right:2px solid rgba(216,230,255,.45);
}
.art.potion .cork{
  left:50%; bottom:49px; width:20px; height:9px; margin-left:-10px;
  border-radius:3px;
  background: linear-gradient(180deg,#dcb27a,#8a6033);
  box-shadow: 0 1px 3px rgba(0,0,0,.45), inset 0 1px 0 rgba(255,235,200,.6);
}

/* 羽毛笔 */
.art.quill{ width:42px; height:62px; transform: rotate(12deg); }
.art.quill .vane{
  left:50%; top:2px; width:27px; height:46px; margin-left:-13.5px;
  background:
    repeating-linear-gradient(102deg, rgba(255,255,255,.5) 0 1px, rgba(255,255,255,0) 1px 5px),
    linear-gradient(158deg,#f2ecff,#bfaeee 58%, #8e78cb);
  -webkit-clip-path: polygon(50% 0%, 100% 28%, 80% 88%, 50% 100%, 20% 88%, 0% 28%);
          clip-path: polygon(50% 0%, 100% 28%, 80% 88%, 50% 100%, 20% 88%, 0% 28%);
  filter: drop-shadow(0 0 9px rgba(190,170,255,.55));
}
.art.quill .spine{
  left:50%; top:6px; width:2px; height:52px; margin-left:-1px;
  border-radius:2px;
  background: linear-gradient(180deg,#fffaea,#e2cf9f 55%,#a8894f);
  box-shadow: 0 0 4px rgba(255,250,220,.6);
}
.art.quill .tip{
  left:50%; bottom:0; width:4px; height:8px; margin-left:-2px;
  background: linear-gradient(180deg,#c9a45f,#4a3a1e);
  clip-path: polygon(0 0,100% 0,50% 100%);
}

/* 水晶球：半透明玻璃 + 内部闪电 */
.art.crystal{ width:54px; height:60px; }
.art.crystal .orb{
  left:50%; top:0; width:50px; height:50px; margin-left:-25px;
  border-radius:50%;
  background:
    radial-gradient(circle at 30% 22%, rgba(255,255,255,.5) 0 6%, rgba(214,240,255,.14) 20%, rgba(120,180,255,.08) 48%, rgba(70,110,220,.18) 78%, rgba(16,26,70,.42) 100%);
  border:2px solid rgba(205,238,255,.62);
  box-shadow: 0 0 20px rgba(120,200,255,.6), inset 0 0 26px rgba(150,215,255,.32);
  overflow:hidden;
}
.art.crystal .bolt{
  left:50%; top:7px; width:26px; height:37px; margin-left:-13px;
  background: linear-gradient(180deg,#f4fcff,#a4e0ff 50%,#5fa8f2);
  -webkit-clip-path: polygon(60% 0, 22% 55%, 46% 55%, 34% 100%, 82% 42%, 55% 42%, 76% 0);
          clip-path: polygon(60% 0, 22% 55%, 46% 55%, 34% 100%, 82% 42%, 55% 42%, 76% 0);
  filter: drop-shadow(0 0 7px rgba(170,225,255,.95));
  animation: boltFlicker 3.4s linear infinite;
}
@keyframes boltFlicker{
  0%,14%,17%,46%,50%,82%,86%,100%{ opacity:1 }
  15%,16%{ opacity:.15 }
  47%,49%{ opacity:.35 }
  83%,85%{ opacity:.22 }
}
.art.crystal .bolt2{
  left:9px; bottom:4px; width:12px; height:17px; opacity:.75;
  background: linear-gradient(180deg,#dff4ff,#7fc2f5);
  -webkit-clip-path: polygon(60% 0, 18% 55%, 46% 55%, 30% 100%, 84% 40%, 52% 40%, 76% 0);
          clip-path: polygon(60% 0, 18% 55%, 46% 55%, 30% 100%, 84% 40%, 52% 40%, 76% 0);
  animation: boltFlicker 2.3s linear infinite reverse;
}
.art.crystal .gleam{
  left:7px; top:5px; width:12px; height:20px; border-radius:50%;
  background: linear-gradient(rgba(255,255,255,.85), rgba(255,255,255,0));
  transform: rotate(16deg);
}
.art.crystal .spark2{
  right:9px; bottom:10px; width:5px; height:5px; border-radius:50%;
  background:#fff; box-shadow: 0 0 8px #bfe9ff;
  animation: twinkle 1.4s ease-in-out infinite alternate;
}
.art.crystal .stand{
  left:50%; bottom:0; width:36px; height:12px; margin-left:-18px;
  border-radius:50%;
  background: linear-gradient(180deg,#8676c2,#3b2f63);
  box-shadow: 0 4px 10px rgba(0,0,0,.45), inset 0 2px 3px rgba(255,255,255,.28);
}

/* 卷轴 */
.art.scroll{ width:56px; height:42px; transform: rotate(-6deg); }
.art.scroll .paper{
  left:11px; right:11px; top:5px; bottom:5px;
  background:
    repeating-linear-gradient(180deg, rgba(120,88,44,.30) 0 1px, rgba(120,88,44,0) 1px 6px),
    linear-gradient(100deg,#f7edd6,#dcc8a2 60%,#c3a87c);
  box-shadow: inset 0 0 10px rgba(110,80,40,.4), 0 2px 6px rgba(0,0,0,.35);
}
.art.scroll .roll{
  top:0; bottom:0; width:13px; border-radius:7px;
  background: linear-gradient(90deg,#a5854a,#f2e3c2 42%,#e0cb9f 58%,#a5854a);
  box-shadow: 0 3px 8px rgba(0,0,0,.45), inset 0 1px 0 rgba(255,255,255,.55);
}
.art.scroll .roll.l{ left:0 }
.art.scroll .roll.r{ right:0 }

/* 魔法帽 */
.art.hat{ width:66px; height:58px; }
.art.hat .cone{
  left:50%; bottom:9px; width:46px; height:46px; margin-left:-23px;
  background: linear-gradient(102deg,#7a58d6,#4a2f92 52%,#241348);
  -webkit-clip-path: polygon(50% 0%, 94% 100%, 6% 100%);
          clip-path: polygon(50% 0%, 94% 100%, 6% 100%);
  filter: drop-shadow(0 0 10px rgba(150,120,255,.45));
}
.art.hat .brim{
  left:0; right:0; bottom:1px; height:16px;
  border-radius:50%;
  background: radial-gradient(ellipse at 50% 28%, #563c9e, #2b1a5e 72%);
  box-shadow: 0 7px 14px rgba(0,0,0,.5), inset 0 -3px 7px rgba(0,0,0,.4), inset 0 2px 3px rgba(190,170,255,.35);
}
.art.hat .band{
  left:50%; bottom:12px; width:35px; height:7px; margin-left:-17.5px;
  border-radius:2px;
  background: linear-gradient(180deg,#ffe3a0,#c08a2e);
  box-shadow: 0 0 10px rgba(255,200,110,.5);
}
.art.hat .star{
  left:50%; bottom:27px; margin-left:-6px; width:12px; text-align:center;
  font-size:12px; line-height:1; color:#ffeaa9;
  text-shadow: 0 0 10px rgba(255,210,120,.95);
}

/* Emoji 杂物 */
.art.emoji{
  width:48px; height:48px;
  display:grid; place-items:center;
  font-size:37px; line-height:1;
  font-family:"Segoe UI Emoji","Apple Color Emoji","Noto Color Emoji",sans-serif;
  filter: drop-shadow(0 3px 5px rgba(0,0,0,.55));
}
.art.emoji.toad{   filter: sepia(.5) saturate(.35) contrast(1.3) brightness(.78) drop-shadow(0 3px 5px rgba(0,0,0,.55)); }
.art.emoji.key{    filter: sepia(.35) brightness(.95) drop-shadow(0 3px 5px rgba(0,0,0,.55)); }
.art.emoji.candle{ filter: brightness(1.08) drop-shadow(0 0 13px rgba(255,190,90,.8)) drop-shadow(0 3px 5px rgba(0,0,0,.5)); }
.art.emoji.ring{   filter: drop-shadow(0 0 9px rgba(255,120,200,.55)) drop-shadow(0 3px 5px rgba(0,0,0,.5)); }
.art.emoji.crown{  filter: drop-shadow(0 0 10px rgba(255,210,110,.7)) drop-shadow(0 3px 5px rgba(0,0,0,.5)); }

/* ============ 躲避鼠标的青蛙 ============ */
.frog{
  position:absolute; width:58px; height:58px;
  display:grid; place-items:center;
  transform: translate(-50%,-50%);
  transition: left .52s cubic-bezier(.3,1.3,.5,1), top .52s cubic-bezier(.3,1.3,.5,1);
  pointer-events:none;
  z-index:500;
  will-change: left, top;
}
.frog-inner{
  font-size:42px; line-height:1;
  font-family:"Segoe UI Emoji","Apple Color Emoji","Noto Color Emoji",sans-serif;
  filter: drop-shadow(0 0 12px rgba(110,255,140,.7)) drop-shadow(0 4px 6px rgba(0,0,0,.55));
  animation: frogIdle 2.4s ease-in-out infinite;
}
@keyframes frogIdle{
  0%,100%{ transform: translateY(0) scale(1,1) }
  50%    { transform: translateY(-3px) scale(.95,1.06) }
}
.frog.hopping .frog-inner{ animation: frogHop .52s cubic-bezier(.3,.6,.4,1); }
@keyframes frogHop{
  0%  { transform: translateY(0) scale(1,1) }
  30% { transform: translateY(-16px) scale(1.15,.85) rotate(-6deg) }
  62% { transform: translateY(3px) scale(.88,1.12) rotate(4deg) }
  100%{ transform: translateY(0) scale(1,1) }
}

/* ============ 胜利爆发粒子 ============ */
.burst{ position:absolute; left:50%; top:31%; z-index:8; pointer-events:none; }
.burst i{
  position:absolute; width:6px; height:6px; border-radius:50%;
  background: radial-gradient(circle,#fff,#ffd47a 45%, rgba(255,180,90,0) 72%);
  box-shadow: 0 0 12px rgba(255,214,140,.95);
  animation: spark 1.5s cubic-bezier(.2,.7,.3,1) forwards;
}
@keyframes spark{
  0%{ transform: translate(-50%,-50%) rotate(var(--a)) translateY(0) scale(.4); opacity:0 }
  12%{ opacity:1 }
  100%{ transform: translate(-50%,-50%) rotate(var(--a)) translateY(calc(var(--d) * -1)) scale(.25); opacity:0 }
}

.circle.win{ animation: breatheWin 1.1s ease-in-out infinite; }
@keyframes breatheWin{
  0%,100%{ transform: scale(1) rotate(0deg); filter: brightness(1.15) saturate(1.1) }
  50%    { transform: scale(1.06) rotate(2deg); filter: brightness(1.55) saturate(1.45) }
}
.circle.win .glow{
  background: radial-gradient(circle, rgba(255,224,150,.55) 0%, rgba(190,110,255,.35) 42%, rgba(90,50,200,0) 72%);
}
.circle.win .r1{ animation-duration: 5s; border-color: rgba(255,235,190,.85); box-shadow: 0 0 60px rgba(255,214,140,.65), inset 0 0 60px rgba(190,150,255,.45); }
.circle.win .r2{ animation-duration: 9s; border-color: rgba(255,240,210,.55); }
.circle.win .r3{ animation-duration: 14s; background: repeating-conic-gradient(from 0deg, rgba(255,232,180,.85) 0deg 1deg, transparent 1deg 10deg); }
.circle.win .glyph{ animation-duration: 22s; }
.circle.win .glyph2{ animation-duration: 8s; }
.circle.win .runes span{ color:#ffeec2; text-shadow: 0 0 16px rgba(255,214,140,.95); opacity:1; }
.circle.win .core{ box-shadow: 0 0 90px rgba(255,228,160,.95); }
.circle.win .gear{ animation-duration: 3.5s; }
.circle.win .arcs{ animation-duration: 7s; }
.circle.win .thin{ animation-duration: 12s; }
.circle.win .orbit{ animation-duration: 4s; }
.circle.win .pulse{ animation-duration: 1.6s; border-color: rgba(255,228,160,.8); box-shadow: 0 0 22px rgba(255,214,140,.7); }
#stage.win .bench{ filter: brightness(.72) saturate(.85); transition: filter .8s; }

/* ============ 通关结算弹窗 ============ */
.win{
  position:fixed; inset:0; z-index:60;
  display:grid; place-items:center;
  opacity:0; pointer-events:none;
  transition: opacity .5s ease;
}
.win.show{ opacity:1; }
.win-backdrop{
  position:absolute; inset:0;
  background: radial-gradient(ellipse at 50% 42%, rgba(64,36,130,.42), rgba(5,3,12,.8) 78%);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
}
.win-panel{
  position:relative;
  padding: 42px 60px 34px;
  border-radius: 24px;
  text-align:center;
  background: linear-gradient(180deg, rgba(82,52,168,.6), rgba(30,16,72,.78));
  border:1px solid rgba(198,168,255,.55);
  box-shadow: 0 0 60px rgba(140,90,255,.5), 0 24px 70px rgba(0,0,0,.6), inset 0 1px 0 rgba(255,255,255,.22);
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  transform: translateY(34px) scale(.88);
  transition: transform .55s cubic-bezier(.18,1.5,.4,1);
}
.win.show .win-panel{ transform: translateY(0) scale(1); }
.win-halo{
  position:absolute; inset:-34px; z-index:-1; border-radius:30px;
  background: conic-gradient(from 0deg, rgba(255,214,140,.4), rgba(160,110,255,.4), rgba(120,210,255,.4), rgba(255,214,140,.4));
  filter: blur(30px);
  animation: spin 9s linear infinite;
  opacity:.85;
}
.win-text{
  font-size: clamp(24px, 4.4vw, 42px);
  letter-spacing:.1em;
  color:#fff;
  text-shadow: 0 0 22px rgba(255,226,150,.95), 0 0 62px rgba(196,128,255,.9), 0 0 120px rgba(120,80,255,.7);
  animation: winGlow 2.6s ease-in-out infinite;
  white-space:nowrap;
}
@keyframes winGlow{
  0%,100%{ text-shadow: 0 0 22px rgba(255,226,150,.95), 0 0 62px rgba(196,128,255,.9), 0 0 120px rgba(120,80,255,.7) }
  50%{ text-shadow: 0 0 30px rgba(255,236,180,1), 0 0 80px rgba(210,150,255,1), 0 0 150px rgba(140,100,255,.85) }
}
.win-sub{
  margin-top:10px; font-size:12.5px; letter-spacing:.24em; color:#d8c8ff;
  text-shadow: 0 0 18px rgba(140,100,255,.8);
}
.win-stats{
  display:flex; justify-content:center; margin:22px 0 4px;
}
.stat{
  display:flex; flex-direction:column; align-items:center; gap:5px;
  padding:0 28px;
  border-right:1px solid rgba(190,160,255,.28);
}
.stat:last-child{ border-right:none; }
.stat b{
  font-size:23px; color:#ffe9b8; font-weight:600;
  font-family:"Segoe UI",sans-serif;
  text-shadow: 0 0 16px rgba(255,210,120,.65);
}
.stat span{ font-size:10.5px; letter-spacing:.34em; text-indent:.34em; color:#b6a6e0; }
.again{
  margin-top:22px; padding:14px 46px; cursor:pointer;
  font-family:inherit; font-size:16px; font-weight:700;
  letter-spacing:.3em; text-indent:.3em;
  color:#3a2305; border-radius:999px;
  background: linear-gradient(180deg,#ffe9ae,#ffc861 45%,#e29a34);
  border:1px solid #ffe7b0;
  box-shadow: 0 0 32px rgba(255,200,110,.6), inset 0 2px 0 rgba(255,255,255,.75), 0 8px 20px rgba(0,0,0,.45);
  opacity:0; animation: fadeUp .7s ease .45s forwards;
  pointer-events:none;
  transition: transform .2s, box-shadow .25s;
}
.win.show .again{ pointer-events:auto; }
.again:hover{
  transform: translateY(-2px) scale(1.03);
  box-shadow: 0 0 50px rgba(255,218,140,.95), inset 0 2px 0 rgba(255,255,255,.85), 0 10px 24px rgba(0,0,0,.5);
}
.again:active{ transform: scale(.95); }
.win-tip{
  margin-top:14px; font-size:11px; letter-spacing:.2em; color:#a294cc;
  opacity:0; animation: fadeUp .7s ease .65s forwards;
}
@keyframes fadeUp{ from{ opacity:0; transform: translateY(10px) } to{ opacity:1; transform: translateY(0) } }

/* 小屏适配 */
@media (max-width: 720px){
  .hud .sub{ display:none; }
  .hud-right{ top:12px; right:10px; }
  .pill{ font-size:11px; padding:6px 10px; }
  .win-panel{ padding: 30px 26px 26px; }
  .win-text{ white-space:normal; }
  .stat{ padding:0 16px; }
}
@media (max-height: 700px){
  .hud .sub{ display:none; }
  .hud .title{ font-size:clamp(14px,2vw,19px); }
}
</style>
</head>
<body>
<div id="stage">
  <div id="stars" class="bg"></div>
  <div id="dust" class="bg-dust bg"></div>
  <div class="vignette"></div>

  <header class="hud">
    <div class="title">魔法师分类收纳</div>
    <div class="sub">杂物堆得乱七八糟 —— 拖动最上层的法器送回魔法阵；工作台上还有一只活青蛙，小心别吓到它</div>
  </header>
  <div class="hud-right">
    <div class="pill">归位 <b id="count">0</b> / <span id="total">25</span></div>
    <button id="soundBtn" class="icon-btn" title="音效开关">🔊</button>
    <button id="resetBtn" class="icon-btn" title="重新散落">↻</button>
  </div>

  <div class="circle-wrap">
    <div class="circle" id="circle">
      <div class="glow"></div>
      <div class="ring r3"></div>
      <div class="ring r1"></div>
      <div class="ring r2"></div>
      <div class="ring gear"></div>
      <div class="ring arcs"></div>
      <div class="ring thin"></div>
      <div class="orbit"><i style="--oa:0deg"></i><i style="--oa:120deg"></i><i style="--oa:240deg"></i></div>
      <div class="pulse"></div>
      <div class="pulse p2"></div>
      <svg class="glyph" viewBox="0 0 200 200" aria-hidden="true">
        <defs>
          <linearGradient id="gs" x1="0" y1="0" x2="1" y2="1">
            <stop offset="0" stop-color="#c6b0ff"/>
            <stop offset="1" stop-color="#78e6ff"/>
          </linearGradient>
          <linearGradient id="gs2" x1="0" y1="1" x2="1" y2="0">
            <stop offset="0" stop-color="#ffd8a0"/>
            <stop offset="1" stop-color="#a98cff"/>
          </linearGradient>
        </defs>
        <circle cx="100" cy="100" r="96" fill="none" stroke="url(#gs)" stroke-width=".7" opacity=".5"/>
        <circle cx="100" cy="100" r="88" fill="none" stroke="url(#gs)" stroke-width=".45" opacity=".4" stroke-dasharray="2 5"/>
        <polygon points="100,30 141.1,156.6 33.4,78.4 166.6,78.4 58.9,156.6"
                 fill="none" stroke="url(#gs2)" stroke-width=".9" stroke-linejoin="round" opacity=".55"/>
        <circle cx="100" cy="100" r="40" fill="none" stroke="url(#gs)" stroke-width=".6" opacity=".45"/>
        <circle cx="100" cy="100" r="54" fill="none" stroke="url(#gs2)" stroke-width=".5" opacity=".28" stroke-dasharray="1 4"/>
      </svg>
      <svg class="glyph2" viewBox="0 0 200 200" aria-hidden="true">
        <polygon points="100,26 164,100 100,174 36,100" fill="none" stroke="url(#gs)" stroke-width="1" opacity=".35"/>
        <polygon points="100,50 140,100 100,150 60,100" fill="none" stroke="url(#gs2)" stroke-width=".8" opacity=".4"/>
      </svg>
      <div class="runes" id="runes"></div>
      <div class="core"></div>
    </div>
  </div>

  <div class="slots" id="slots"></div>

  <div class="bench" id="bench">
    <div class="carve">· 炼 金 工 作 台 ·</div>
    <div class="bench-lip"></div>
  </div>

  <div class="items" id="items"></div>
  <div class="burst" id="burst"></div>

  <div class="win" id="win">
    <div class="win-backdrop"></div>
    <div class="win-panel">
      <div class="win-halo"></div>
      <h2 class="win-text">✨ 魔法归位，大功告成！ ✨</h2>
      <p class="win-sub">所有法器都回到了魔法阵，沉睡的力量苏醒了</p>
      <div class="win-stats">
        <div class="stat"><b id="stTime">0:00</b><span>用时</span></div>
        <div class="stat"><b id="stErr">0</b><span>失误</span></div>
        <div class="stat"><b id="stTotal">25</b><span>法器</span></div>
      </div>
      <button class="again" id="againBtn">重新开始游戏</button>
      <div class="win-tip">点击按钮后，所有法器将重新散落在工作台上</div>
    </div>
  </div>
</div>

<script>
(function(){
'use strict';

/* ================= 数据 ================= */
/* kind: css = CSS 手绘, emoji = Emoji 字符; w/h = 点击热区尺寸 */
const TYPES = [
  { id:'potion-red',  name:'红药水',   cap:3, w:48, h:62, kind:'css' },
  { id:'potion-blue', name:'蓝药水',   cap:3, w:48, h:62, kind:'css' },
  { id:'quill',       name:'羽毛笔',   cap:2, w:46, h:64, kind:'css' },
  { id:'crystal',     name:'水晶球',   cap:2, w:54, h:60, kind:'css' },
  { id:'scroll',      name:'卷轴',     cap:3, w:58, h:44, kind:'css' },
  { id:'toad',        name:'干瘪蟾蜍', cap:2, w:50, h:48, kind:'emoji' },
  { id:'ring',        name:'魔法戒指', cap:3, w:48, h:48, kind:'emoji' },
  { id:'key',         name:'旧钥匙',   cap:3, w:52, h:48, kind:'emoji' },
  { id:'candle',      name:'蜡烛',     cap:2, w:44, h:52, kind:'emoji' },
  { id:'crown',       name:'魔法王冠', cap:2, w:48, h:48, kind:'emoji' }
];

const EMOJI = { toad:'🐸', ring:'💍', key:'🗝️', candle:'🕯️', crown:'👑' };

const ART = {
  'potion-red' : '<div class="art potion red"><i class="cork"></i><i class="neck"></i><i class="body"><i class="liquid"></i><i class="shine"></i></i></div>',
  'potion-blue': '<div class="art potion blue"><i class="cork"></i><i class="neck"></i><i class="body"><i class="liquid"></i><i class="shine"></i></i></div>',
  'quill'      : '<div class="art quill"><i class="vane"></i><i class="spine"></i><i class="tip"></i></div>',
  'crystal'    : '<div class="art crystal"><i class="stand"></i><i class="orb"><i class="bolt"></i><i class="bolt2"></i><i class="gleam"></i><i class="spark2"></i></i></div>',
  'scroll'     : '<div class="art scroll"><i class="paper"></i><i class="roll l"></i><i class="roll r"></i></div>'
};
Object.keys(EMOJI).forEach(k=>{
  ART[k] = `<div class="art emoji ${k}">${EMOJI[k]}</div>`;
});

const RUNE_CHARS = ['✦','✧','☾','✶','⚹','✷','☽','✹','⚝','✵','✴','❈','✺','✻','✽','✾','❋','✵','✶','☾'];

/* ================= DOM ================= */
const stage      = document.getElementById('stage');
const circleEl   = document.getElementById('circle');
const slotsRoot  = document.getElementById('slots');
const benchEl    = document.getElementById('bench');
const itemsRoot  = document.getElementById('items');
const winEl      = document.getElementById('win');
const countEl    = document.getElementById('count');
const totalEl    = document.getElementById('total');
const burstEl    = document.getElementById('burst');
const runesEl    = document.getElementById('runes');
const stTimeEl   = document.getElementById('stTime');
const stErrEl    = document.getElementById('stErr');
const stTotalEl  = document.getElementById('stTotal');

const state = { slots:[], items:[], placed:0, drag:null, locked:false,
                mistakes:0, startAt:null };

/* ================= 工具 ================= */
const rnd = (a,b)=> a + Math.random()*(b-a);
const clamp = (v,a,b)=> Math.max(a, Math.min(b, v));
function fmtTime(sec){
  const m = Math.floor(sec/60), s = sec % 60;
  return m + ':' + String(s).padStart(2,'0');
}

/* ================= 音效 ================= */
let actx = null, soundOn = true;
const NOTES = {
  pick : [[520,.07,'sine',.05]],
  place: [[680,.08,'sine',.06],[1020,.15,'sine',.045]],
  bad  : [[190,.14,'sawtooth',.045],[120,.16,'sine',.04]],
  frog : [[330,.08,'sine',.05],[494,.1,'sine',.04]],
  win  : [[523,.11,'triangle',.06],[659,.11,'triangle',.06],[784,.11,'triangle',.06],[1046,.42,'triangle',.055]]
};
function sfx(kind){
  if(!soundOn) return;
  const seq = NOTES[kind];
  if(!seq) return;
  try{
    if(!actx) actx = new (window.AudioContext || window.webkitAudioContext)();
    if(actx.state === 'suspended') actx.resume();
    let t = actx.currentTime, d = 0;
    seq.forEach(([f,dur,type,vol])=>{
      const o = actx.createOscillator(), g = actx.createGain();
      o.type = type; o.frequency.setValueAtTime(f, t + d);
      g.gain.setValueAtTime(0.0001, t + d);
      g.gain.linearRampToValueAtTime(vol, t + d + .012);
      g.gain.exponentialRampToValueAtTime(.0001, t + d + dur);
      o.connect(g).connect(actx.destination);
      o.start(t + d); o.stop(t + d + dur + .03);
      d += dur * .92;
    });
  }catch(e){ /* 静默失败 */ }
}

/* ================= 背景装饰 ================= */
(function buildStars(){
  const root = document.getElementById('stars');
  let html = '';
  for(let i=0;i<120;i++){
    const s = rnd(1,2.6).toFixed(1);
    html += `<i class="star" style="left:${rnd(0,100).toFixed(2)}%;top:${rnd(0,74).toFixed(2)}%;width:${s}px;height:${s}px;--t:${rnd(2,6).toFixed(1)}s;animation-delay:${rnd(0,5).toFixed(1)}s;opacity:${rnd(.2,.9).toFixed(2)}"></i>`;
  }
  root.innerHTML = html;
})();

(function buildDust(){
  const root = document.getElementById('dust');
  let html = '';
  for(let i=0;i<18;i++){
    const s = rnd(3,6).toFixed(1);
    html += `<i class="mote" style="left:${rnd(4,96).toFixed(2)}%;width:${s}px;height:${s}px;animation-duration:${rnd(13,26).toFixed(1)}s;animation-delay:-${rnd(0,16).toFixed(1)}s;--dx:${rnd(-60,60).toFixed(0)}px"></i>`;
  }
  root.innerHTML = html;
})();

(function buildRunes(){
  let html = '';
  RUNE_CHARS.forEach((ch,i)=>{
    html += `<span style="--a:${(i/RUNE_CHARS.length*360).toFixed(1)}deg">${ch}</span>`;
  });
  runesEl.innerHTML = html;
})();

/* ================= 尺寸 ================= */
function circleSize(){
  return Math.max(230, Math.min(window.innerWidth * .62, window.innerHeight * .56, 620));
}
function setCircleSize(){
  document.documentElement.style.setProperty('--cs', circleSize() + 'px');
}

/* ================= 构建槽位 ================= */
function buildSlots(){
  slotsRoot.innerHTML = '';
  state.slots = TYPES.map(t=>{
    const el = document.createElement('div');
    el.className = 'slot';
    el.dataset.type = t.id;
    el.title = t.name;
    /* 虚影缩放按容量调整：容量越多缩得越小 */
    const gs = t.cap >= 3 ? .46 : (t.cap === 2 ? .54 : .62);
    el.innerHTML = `<div class="ghost" style="transform:scale(${gs})">${ART[t.id]}</div><span class="count">×${t.cap}</span>`;
    slotsRoot.appendChild(el);
    return { type:t.id, cap:t.cap, el, filled:[], countEl:el.querySelector('.count') };
  });
  layoutSlots();
}

function layoutSlots(){
  const cs = circleSize();
  const R = cs * 0.345;
  const n = state.slots.length;
  /* 起始角偏移半个步长，避免槽位正对顶部标题 */
  const start = -90 + (360/n)/2;
  state.slots.forEach((s,i)=>{
    const a = (start + i * 360/n) * Math.PI / 180;
    s.el.style.left = (Math.cos(a) * R).toFixed(2) + 'px';
    s.el.style.top  = (Math.sin(a) * R).toFixed(2) + 'px';
  });
}

/* ================= 构建物品 ================= */
function buildItems(){
  itemsRoot.innerHTML = '';
  state.items = [];
  TYPES.forEach(t=>{
    for(let i=0;i<t.cap;i++){
      const dom = document.createElement('div');
      dom.className = 'item';
      dom.style.width  = t.w + 'px';
      dom.style.height = t.h + 'px';
      dom.setAttribute('draggable','false');
      dom.style.setProperty('--dur', rnd(3.4,5.4).toFixed(2) + 's');
      dom.style.setProperty('--delay', (-rnd(0,4)).toFixed(2) + 's');
      dom.innerHTML = `<div class="item-inner">${ART[t.id]}</div>`;
      itemsRoot.appendChild(dom);

      const item = { type:t.id, dom, x:0, y:0, placed:false, slot:null, baseZ:1 };
      dom.addEventListener('pointerdown', e=> onDown(e, item));
      state.items.push(item);
    }
  });
  totalEl.textContent = state.items.length;
  stTotalEl.textContent = state.items.length;
}

function setPos(item, x, y){
  item.x = x; item.y = y;
  item.dom.style.left = x + 'px';
  item.dom.style.top  = y + 'px';
}

/* ================= 随机堆叠散落 =================
   完全随机 X/Y，允许互相重叠；每个物品随机旋转角
   和随机 z-index，形成自然的“杂物堆”效果。 */
function scatter(){
  const br = benchEl.getBoundingClientRect();
  const padX = Math.max(34, br.width * .03);
  const padTop = 40, padBottom = 32;
  const minX = br.left + padX,   maxX = br.right  - padX;
  const minY = br.top  + padTop, maxY = br.bottom - padBottom;
  const n = state.items.length;

  state.items.filter(it=>!it.placed).forEach(it=>{
    setPos(it, rnd(minX, maxX), rnd(minY, maxY));
    it.dom.style.setProperty('--r', rnd(-26,26).toFixed(1) + 'deg');
    const z = 1 + Math.floor(Math.random() * n);
    it.dom.style.zIndex = z;
    it.baseZ = z;
  });
}

function saveHomes(){
  state.items.forEach(it=>{
    it.homeX = it.x;
    it.homeY = it.y;
    it.homeR = it.dom.style.getPropertyValue('--r') || '0deg';
  });
}

/* ================= 拖拽（支持重叠堆叠） ================= */
function onDown(e, item){
  if(state.locked || item.placed || state.drag) return;
  e.preventDefault();
  sfx('pick');
  if(!state.startAt) state.startAt = Date.now();

  const off = { x: e.clientX - item.x, y: e.clientY - item.y };
  item.dom.classList.add('dragging');
  item.dom.classList.remove('hint');
  item.dom.style.setProperty('--s', '1.12');
  /* 抓起时清掉之前被青蛙挤开的位移 */
  item.dom.style.setProperty('--jx', '0px');
  item.dom.style.setProperty('--jy', '0px');
  /* 拖拽时置于最顶层，压住所有堆叠物品 */
  item.dom.style.zIndex = 99999;
  state.drag = { item, off, pointerId: e.pointerId };
  stage.classList.add('dragging');

  try{ item.dom.setPointerCapture(e.pointerId); }catch(err){}

  item.dom.addEventListener('pointermove', onMove);
  item.dom.addEventListener('pointerup', onUp);
  item.dom.addEventListener('pointercancel', onUp);
  updateHover();
}

function onMove(e){
  const d = state.drag;
  if(!d) return;
  setPos(d.item, e.clientX - d.off.x, e.clientY - d.off.y);
  updateHover();
}

function onUp(e){
  const d = state.drag;
  if(!d) return;
  const item = d.item;
  item.dom.removeEventListener('pointermove', onMove);
  item.dom.removeEventListener('pointerup', onUp);
  item.dom.removeEventListener('pointercancel', onUp);
  try{ item.dom.releasePointerCapture(d.pointerId); }catch(err){}
  state.drag = null;
  stage.classList.remove('dragging');

  const near = nearestSlot(item.x, item.y);
  state.slots.forEach(s=> s.el.classList.remove('hover'));
  const hit = near.slot && near.dist < near.rw * 0.95 ? near.slot : null;

  if(hit && hit.type === item.type && hit.filled.length < hit.cap){
    restoreZLater(item);
    place(item, hit);
  }else{
    if(hit){
      state.mistakes++;
      hit.el.classList.add('bad');
      setTimeout(()=> hit.el.classList.remove('bad'), 520);
      sfx('bad');
    }
    restoreZLater(item);
    reject(item);
  }
}

/* 拖拽结束后延迟恢复原本的堆叠层级，让飞回/吸附动画保持在最上层 */
function restoreZLater(item){
  setTimeout(()=>{
    if(state.drag && state.drag.item === item) return; /* 已被再次抓起 */
    if(!item.placed) item.dom.style.zIndex = item.baseZ;
  }, 420);
}

function nearestSlot(x, y){
  let best = null, bestD = Infinity, bestW = 0;
  for(const s of state.slots){
    const r = s.el.getBoundingClientRect();
    const cx = r.left + r.width/2, cy = r.top + r.height/2;
    const d = Math.hypot(x - cx, y - cy);
    if(d < bestD){ bestD = d; best = s; bestW = r.width; }
  }
  return { slot: best, dist: bestD, rw: bestW };
}

function updateHover(){
  const d = state.drag;
  if(!d) return;
  const near = nearestSlot(d.item.x, d.item.y);
  const inRange = near.slot && near.dist < near.rw * 0.95;
  state.slots.forEach(s=> s.el.classList.toggle('hover', s === near.slot && inRange));
}

function reject(item){
  const dom = item.dom;
  dom.classList.remove('dragging');
  dom.classList.add('reject');
  dom.style.setProperty('--s', '1');
  void dom.offsetWidth;
  setPos(item, item.homeX, item.homeY);
  dom.style.setProperty('--r', item.homeR);
  setTimeout(()=> dom.classList.remove('reject'), 480);
}

/* ================= 放置 ================= */
function place(item, slot){
  const r = slot.el.getBoundingClientRect();
  const cx = r.left + r.width/2, cy = r.top + r.height/2;
  const idx = slot.filled.length;

  /* 多件物品在槽内排开：2 件左右分，3 件左中右 */
  let off = 0, s = .62;
  if(slot.cap === 2){ s = .5;  off = (idx === 0 ? -1 : 1) * r.width * .16; }
  else if(slot.cap >= 3){ s = .44; off = (idx - 1) * r.width * .19; }

  slot.filled.push(item);
  item.placed = true;
  item.slot = slot;

  const dom = item.dom;
  dom.classList.remove('dragging', 'reject');
  dom.classList.add('placed');
  void dom.offsetWidth;
  dom.style.setProperty('--s', String(s));
  dom.style.setProperty('--r', '0deg');
  setPos(item, cx + off, cy);

  const left = slot.cap - slot.filled.length;
  slot.countEl.textContent = left > 0 ? ('×' + left) : '✓';
  slot.el.classList.add('flash');
  setTimeout(()=> slot.el.classList.remove('flash'), 640);
  if(left === 0) slot.el.classList.add('done');

  state.placed++;
  countEl.textContent = state.placed;
  sfx('place');

  if(state.placed === state.items.length) setTimeout(win, 420);
}

/* ================= 通关结算 ================= */
function win(){
  state.locked = true;
  stage.classList.add('win');
  circleEl.classList.add('win');
  burst();
  sfx('win');

  const sec = state.startAt ? Math.round((Date.now() - state.startAt)/1000) : 0;
  stTimeEl.textContent = fmtTime(sec);
  stErrEl.textContent = state.mistakes;
  stTotalEl.textContent = state.items.length;

  setTimeout(()=> winEl.classList.add('show'), 350);
}

function burst(){
  burstEl.innerHTML = '';
  const n = 54;
  for(let i=0;i<n;i++){
    const el = document.createElement('i');
    const a = (i / n) * 360 + rnd(-6, 6);
    el.style.setProperty('--a', a.toFixed(1) + 'deg');
    el.style.setProperty('--d', rnd(120, 330).toFixed(0) + 'px');
    el.style.animationDelay = rnd(0, .45).toFixed(2) + 's';
    el.style.animationDuration = rnd(1.1, 1.9).toFixed(2) + 's';
    const s = rnd(4, 9).toFixed(0);
    el.style.width = s + 'px'; el.style.height = s + 'px';
    if(i % 3 === 0){ el.style.background = 'radial-gradient(circle,#fff,#c8a4ff 45%,rgba(180,120,255,0) 72%)'; }
    burstEl.appendChild(el);
  }
  setTimeout(()=>{ burstEl.innerHTML = ''; }, 2800);
}

/* ================= 重置 ================= */
function reset(){
  state.locked = false;
  state.placed = 0;
  state.mistakes = 0;
  state.startAt = null;
  countEl.textContent = '0';
  stage.classList.remove('win');
  circleEl.classList.remove('win');
  winEl.classList.remove('show');
  burstEl.innerHTML = '';

  state.slots.forEach(s=>{
    s.filled = [];
    s.el.classList.remove('flash','bad','done','hover');
    s.countEl.textContent = '×' + s.cap;
  });

  state.items.forEach(it=>{
    it.placed = false;
    it.slot = null;
    const dom = it.dom;
    dom.classList.remove('placed','reject','dragging','hint');
    dom.style.setProperty('--s','1');
  });

  layoutSlots();
  scatter();
  saveHomes();
  frogMoveRandom();
  setTimeout(hintFirst, 700);
}

/* 随机提示一个还没归位的物品 */
function hintFirst(){
  const list = state.items.filter(i=>!i.placed);
  const it = list[Math.floor(Math.random()*list.length)];
  if(!it) return;
  it.dom.classList.add('hint');
  setTimeout(()=> it.dom.classList.remove('hint'), 5200);
}

/* ================= 躲避鼠标的青蛙 ================= */
const FLEE_R = 100;               /* 鼠标靠近该距离即触发逃跑 */
const frog = { el:null, x:0, y:0, fleeing:false };
let lastMouse = null;

function buildFrog(){
  const el = document.createElement('div');
  el.className = 'frog';
  el.innerHTML = '<div class="frog-inner">🐸</div>';
  const br = benchEl.getBoundingClientRect();
  const pad = 46;
  /* 先定位再插入 DOM，避免从 (0,0) 飞过来 */
  el.style.left = rnd(br.left+pad, br.right-pad) + 'px';
  el.style.top  = rnd(br.top+pad,  br.bottom-pad) + 'px';
  frog.x = parseFloat(el.style.left);
  frog.y = parseFloat(el.style.top);
  itemsRoot.appendChild(el);
  frog.el = el;
}

function frogMoveRandom(){
  if(!frog.el) return;
  const br = benchEl.getBoundingClientRect();
  const pad = 46;
  frog.x = rnd(br.left+pad, br.right-pad);
  frog.y = rnd(br.top+pad,  br.bottom-pad);
  frog.el.style.left = frog.x + 'px';
  frog.el.style.top  = frog.y + 'px';
}

function onPointerMove(e){
  lastMouse = { x: e.clientX, y: e.clientY };
  if(state.locked || frog.fleeing) return;
  if(Math.hypot(e.clientX - frog.x, e.clientY - frog.y) < FLEE_R) frogFlee();
}

function frogFlee(){
  frog.fleeing = true;
  sfx('frog');
  frog.el.classList.add('hopping');

  const br = benchEl.getBoundingClientRect();
  const pad = 46;
  const minX = br.left+pad, maxX = br.right-pad;
  const minY = br.top+pad,  maxY = br.bottom-pad;

  /* 顺着远离鼠标的方向滑行一段距离 */
  const dx = frog.x - (lastMouse ? lastMouse.x : frog.x);
  const dy = frog.y - (lastMouse ? lastMouse.y : frog.y - 1);
  const len = Math.hypot(dx, dy) || 1;
  const dist = rnd(180, 280);
  let tx = clamp(frog.x + dx/len*dist, minX, maxX);
  let ty = clamp(frog.y + dy/len*dist, minY, maxY);

  /* 保证新位置离鼠标足够远，否则在工作台上随机换一个远点 */
  let tries = 0;
  while(lastMouse && Math.hypot(tx-lastMouse.x, ty-lastMouse.y) < FLEE_R + 60 && tries++ < 30){
    tx = rnd(minX, maxX); ty = rnd(minY, maxY);
  }

  frog.x = tx; frog.y = ty;
  frog.el.style.left = tx + 'px';
  frog.el.style.top  = ty + 'px';

  setTimeout(()=>{
    frog.el.classList.remove('hopping');
    frog.fleeing = false;
    frogSqueeze();
    /* 落地后如果鼠标还贴着脸，接着逃 */
    if(lastMouse && Math.hypot(lastMouse.x - frog.x, lastMouse.y - frog.y) < FLEE_R + 10) frogFlee();
  }, 540);
}

/* 伪物理挤压：青蛙落点附近的散落物品被“挤开” */
function frogSqueeze(){
  const br = benchEl.getBoundingClientRect();
  const pad = 30;
  const R = 95;   /* 碰撞感知半径 */
  state.items.forEach(it=>{
    if(it.placed) return;                            /* 已归位的不参与 */
    if(state.drag && state.drag.item === it) return; /* 正被拖拽的不参与 */
    const dx = it.x - frog.x, dy = it.y - frog.y;
    const d = Math.hypot(dx, dy);
    if(d > R || d < 0.001) return;

    /* 距离越近挤得越远 */
    const push = 12 + (1 - d/R) * 36;
    let jx = dx/d * push, jy = dy/d * push;
    /* 挤开后仍留在工作台范围内 */
    jx = clamp(it.x + jx, br.left+pad, br.right-pad) - it.x;
    jy = clamp(it.y + jy, br.top+pad,  br.bottom-pad) - it.y;
    if(Math.abs(jx) < 1.5 && Math.abs(jy) < 1.5) return;

    const dom = it.dom;
    dom.classList.add('jolt');
    dom.style.setProperty('--jx', jx.toFixed(1) + 'px');
    dom.style.setProperty('--jy', jy.toFixed(1) + 'px');
    setTimeout(()=> dom.classList.remove('jolt'), 520);
  });
}

/* 青蛙闲着没事自己蹦一下 */
setInterval(()=>{
  if(!frog.el || frog.fleeing || state.locked) return;
  if(Math.random() < .55){
    frog.el.classList.add('hopping');
    setTimeout(()=> frog.el.classList.remove('hopping'), 540);
  }
}, 6000);
document.addEventListener('pointermove', onPointerMove);

/* ================= 窗口重排 ================= */
let rzTimer = null;
function onResize(){
  clearTimeout(rzTimer);
  rzTimer = setTimeout(()=>{
    setCircleSize();
    layoutSlots();
    /* 已归位物品重新贴回槽位 */
    state.slots.forEach(s=>{
      s.filled.forEach((it, i)=>{
        const r = s.el.getBoundingClientRect();
        const cx = r.left + r.width/2, cy = r.top + r.height/2;
        let off = 0;
        if(s.cap === 2) off = (i === 0 ? -1 : 1) * r.width * .16;
        else if(s.cap >= 3) off = (i - 1) * r.width * .19;
        it.x = cx + off; it.y = cy;
        it.dom.style.left = it.x + 'px';
        it.dom.style.top  = it.y + 'px';
      });
    });
    /* 未归位物品重新随机堆叠到新尺寸的工作台 */
    if(state.drag) return;
    scatter();
    saveHomes();
    frogMoveRandom();
  }, 180);
}

/* ================= 交互绑定 ================= */
document.getElementById('resetBtn').addEventListener('click', ()=>{
  sfx('pick');
  reset();
});
document.getElementById('againBtn').addEventListener('click', ()=>{
  sfx('pick');
  reset();
});
const soundBtn = document.getElementById('soundBtn');
soundBtn.addEventListener('click', ()=>{
  soundOn = !soundOn;
  soundBtn.textContent = soundOn ? '🔊' : '🔇';
  if(soundOn) sfx('pick');
});

window.addEventListener('resize', onResize);
window.addEventListener('orientationchange', onResize);
window.addEventListener('contextmenu', e=>{
  if(e.target.closest('.item')) e.preventDefault();
});
document.addEventListener('dragstart', e=> e.preventDefault());

/* ================= 启动 ================= */
function init(){
  setCircleSize();
  buildSlots();
  buildItems();
  buildFrog();
  scatter();
  saveHomes();
  setTimeout(()=>{
    scatter();
    saveHomes();
    hintFirst();
  }, 60);
}
init();

})();
</script>
</body>
</html>
