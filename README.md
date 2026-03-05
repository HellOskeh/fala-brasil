<!DOCTYPE html>

<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Fala Brasil">
<meta name="theme-color" content="#0a0f1e">
<title>Fala Brasil! 🇧🇷</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&family=Playfair+Display:wght@700;900&display=swap" rel="stylesheet">
<style>
/* ═══════════════════════════════════════
   VARIABLES & RESET
═══════════════════════════════════════ */
:root {
  --g: #009c3b;
  --y: #FFDF00;
  --b: #002776;
  --bg: #080e1f;
  --s1: #0f1a35;
  --s2: #162347;
  --s3: #1e2f5a;
  --text: #f0f4ff;
  --muted: rgba(240,244,255,0.5);
  --gold: #FFD700;
  --red: #e74c3c;
  --green: #2ecc71;
  --r: 16px;
  --transition: cubic-bezier(0.4,0,0.2,1);
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;overflow:hidden;}
body{font-family:'Nunito',sans-serif;background:var(--bg);color:var(--text);max-width:430px;margin:0 auto;position:relative;}

/* ═══════════════════════════════════════
BACKGROUND AMBIENT
═══════════════════════════════════════ */
body::before{
content:’’;position:fixed;inset:0;pointer-events:none;z-index:0;
background:
radial-gradient(ellipse 60% 40% at 15% 10%, rgba(0,156,59,0.12) 0%, transparent 70%),
radial-gradient(ellipse 50% 50% at 85% 85%, rgba(255,223,0,0.07) 0%, transparent 70%),
radial-gradient(ellipse 70% 60% at 50% 50%, rgba(0,39,118,0.3) 0%, transparent 80%);
}

/* ═══════════════════════════════════════
SCREEN SYSTEM
═══════════════════════════════════════ */
.screen{
display:none;position:fixed;inset:0;z-index:10;
background:var(–bg);overflow-y:auto;overflow-x:hidden;
max-width:430px;
}
.screen.active{display:flex;flex-direction:column;}
.screen.slide-in{animation:slideIn .28s var(–transition) both;}
.screen.slide-out{animation:slideOut .28s var(–transition) both;}
.screen.slide-back-in{animation:slideBackIn .28s var(–transition) both;}
@keyframes slideIn{from{transform:translateX(100%);opacity:0.5}to{transform:translateX(0);opacity:1}}
@keyframes slideOut{from{transform:translateX(0)}to{transform:translateX(-40%);opacity:0}}
@keyframes slideBackIn{from{transform:translateX(-40%);opacity:0}to{transform:translateX(0);opacity:1}}
@keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
@keyframes pop{0%{transform:scale(0.85);opacity:0}70%{transform:scale(1.05)}100%{transform:scale(1);opacity:1}}
@keyframes shake{0%,100%{transform:translateX(0)}20%{transform:translateX(-8px)}40%{transform:translateX(8px)}60%{transform:translateX(-5px)}80%{transform:translateX(5px)}}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:0.6}}
@keyframes confettiFall{0%{transform:translateY(-20px) rotate(0deg);opacity:1}100%{transform:translateY(100vh) rotate(720deg);opacity:0}}
@keyframes checkmark{0%{stroke-dashoffset:50}100%{stroke-dashoffset:0}}
@keyframes ringFill{from{stroke-dashoffset:var(–from)}to{stroke-dashoffset:var(–to)}}
@keyframes glow{0%,100%{box-shadow:0 0 20px rgba(255,223,0,0.3)}50%{box-shadow:0 0 40px rgba(255,223,0,0.6)}}

/* ═══════════════════════════════════════
TIMER BAR (always on top)
═══════════════════════════════════════ */
#timer-bar{
position:fixed;top:0;left:50%;transform:translateX(-50%);
width:100%;max-width:430px;z-index:999;
display:none;
background:rgba(8,14,31,0.95);backdrop-filter:blur(20px);
border-bottom:1px solid rgba(255,255,255,0.06);
padding:.4rem 1rem;
flex-direction:row;align-items:center;gap:.8rem;
}
#timer-bar.visible{display:flex;}
.timer-track{flex:1;height:5px;background:rgba(255,255,255,0.1);border-radius:999px;overflow:hidden;}
.timer-fill{height:100%;background:linear-gradient(90deg,var(–g),var(–y));border-radius:999px;transition:width 1s linear;}
.timer-fill.warning{background:linear-gradient(90deg,#e74c3c,#f39c12);}
.timer-text{font-size:.78rem;font-weight:800;color:var(–y);min-width:42px;text-align:right;}
.timer-icon{font-size:.9rem;}

/* ═══════════════════════════════════════
BOTTOM NAV
═══════════════════════════════════════ */
#bottom-nav{
position:fixed;bottom:0;left:50%;transform:translateX(-50%);
width:100%;max-width:430px;z-index:998;
display:none;
background:rgba(8,14,31,0.97);backdrop-filter:blur(20px);
border-top:1px solid rgba(255,255,255,0.07);
grid-template-columns:repeat(5,1fr);
padding:.4rem 0 max(.4rem,env(safe-area-inset-bottom));
}
#bottom-nav.visible{display:grid;}
.nb{
display:flex;flex-direction:column;align-items:center;gap:.15rem;
padding:.4rem .2rem;background:none;border:none;
color:var(–muted);cursor:pointer;font-family:‘Nunito’,sans-serif;
transition:color .2s;position:relative;
}
.nb.on{color:var(–y);}
.nb .ni{font-size:1.3rem;}
.nb .nl{font-size:.58rem;font-weight:800;letter-spacing:.03em;}
.nb .badge{
position:absolute;top:.3rem;right:.8rem;
background:var(–red);color:white;
border-radius:999px;padding:.05rem .3rem;
font-size:.55rem;font-weight:900;
}

/* ═══════════════════════════════════════
COMMON COMPONENTS
═══════════════════════════════════════ */
.topbar{
display:flex;align-items:center;gap:.7rem;
padding:.9rem 1rem;
padding-top:calc(.9rem + 35px);
background:rgba(8,14,31,0.8);backdrop-filter:blur(10px);
border-bottom:1px solid rgba(255,255,255,0.06);
position:sticky;top:0;z-index:50;
}
.back-btn{
width:34px;height:34px;border-radius:10px;border:none;
background:rgba(255,255,255,0.09);color:var(–text);
cursor:pointer;font-size:1rem;display:flex;align-items:center;justify-content:center;
flex-shrink:0;transition:background .15s;
}
.back-btn:active{background:rgba(255,255,255,0.18);}
.topbar-title{font-family:‘Playfair Display’,serif;font-size:1.15rem;font-weight:700;}
.topbar-sub{font-size:.7rem;color:var(–muted);}

.btn{
border:none;border-radius:var(–r);cursor:pointer;
font-family:‘Nunito’,sans-serif;font-weight:800;
transition:all .15s var(–transition);
display:flex;align-items:center;justify-content:center;gap:.4rem;
}
.btn:active{transform:scale(0.96);}
.btn-primary{background:var(–b);color:white;padding:.85rem 1.5rem;font-size:.95rem;}
.btn-primary:active{background:#001a5a;}
.btn-green{background:var(–g);color:white;padding:.85rem 1.5rem;font-size:.95rem;}
.btn-yellow{background:var(–y);color:#0a0f1e;padding:.85rem 1.5rem;font-size:.95rem;}
.btn-ghost{background:rgba(255,255,255,0.08);color:var(–text);padding:.75rem 1.2rem;font-size:.88rem;}
.btn-ghost:active{background:rgba(255,255,255,0.15);}
.btn-full{width:100%;border-radius:14px;}
.btn-lg{padding:1rem 2rem;font-size:1rem;border-radius:16px;}

/* ═══════════════════════════════════════
TOAST
═══════════════════════════════════════ */
#toast{
position:fixed;top:50px;left:50%;transform:translateX(-50%) translateY(-20px);
background:rgba(15,26,53,0.97);border:1px solid rgba(255,255,255,0.12);
border-radius:999px;padding:.55rem 1.2rem;
font-size:.84rem;font-weight:700;z-index:2000;
transition:all .25s var(–transition);opacity:0;pointer-events:none;
backdrop-filter:blur(20px);white-space:nowrap;
box-shadow:0 8px 30px rgba(0,0,0,0.5);
}
#toast.show{opacity:1;transform:translateX(-50%) translateY(0);}

/* ═══════════════════════════════════════
XP POPUP
═══════════════════════════════════════ */
.xp-popup{
position:fixed;z-index:3000;pointer-events:none;
font-size:1.1rem;font-weight:900;color:var(–y);
text-shadow:0 2px 8px rgba(0,0,0,0.8);
animation:xpFloat 1.2s ease-out forwards;
}
@keyframes xpFloat{0%{opacity:1;transform:translateY(0) scale(1)}100%{opacity:0;transform:translateY(-60px) scale(1.3)}}

/* ═══════════════════════════════════════
SPLASH SCREEN
═══════════════════════════════════════ */
#splash{
align-items:center;justify-content:center;
text-align:center;padding:2rem 1.5rem;
background:linear-gradient(160deg,#070d1c 0%,#0a1628 40%,#0d2a18 100%);
overflow-y:auto;
}
.splash-flag{
width:100px;height:100px;border-radius:50%;
background:conic-gradient(var(–g) 0deg 180deg,var(–y) 180deg 240deg,var(–b) 240deg 360deg);
display:flex;align-items:center;justify-content:center;
font-size:3rem;margin:0 auto 1.2rem;
box-shadow:0 0 0 3px rgba(255,223,0,0.2),0 0 60px rgba(0,156,59,0.3);
animation:glow 3s ease-in-out infinite;
}
.splash-title{
font-family:‘Playfair Display’,serif;
font-size:3.2rem;font-weight:900;line-height:1;
background:linear-gradient(135deg,#fff 30%,var(–y));
-webkit-background-clip:text;-webkit-text-fill-color:transparent;
margin-bottom:.3rem;
}
.splash-sub{font-size:1rem;color:var(–muted);margin-bottom:2rem;}

.level-list{width:100%;max-width:320px;display:flex;flex-direction:column;gap:.6rem;}
.level-row{
display:flex;align-items:center;gap:.9rem;
background:rgba(255,255,255,0.05);
border:1.5px solid rgba(255,255,255,0.09);
border-radius:14px;padding:.9rem 1rem;
cursor:pointer;transition:all .2s;text-align:left;
}
.level-row:active,.level-row:hover{background:rgba(255,223,0,0.1);border-color:rgba(255,223,0,0.4);}
.lr-emoji{font-size:1.7rem;flex-shrink:0;}
.lr-name{font-size:.92rem;font-weight:900;}
.lr-desc{font-size:.72rem;color:var(–muted);}
.lr-arrow{margin-left:auto;color:var(–muted);font-size:.9rem;}

/* ═══════════════════════════════════════
HOME
═══════════════════════════════════════ */
#home{overflow-y:auto;padding-bottom:70px;}
.home-header{
padding:calc(1.2rem + 35px) 1rem 1rem;
background:linear-gradient(180deg,rgba(0,39,118,0.3) 0%,transparent 100%);
}
.home-greeting{font-size:.82rem;color:var(–muted);font-weight:600;}
.home-name{font-family:‘Playfair Display’,serif;font-size:1.6rem;font-weight:900;line-height:1.2;}
.home-level-badge{
display:inline-flex;align-items:center;gap:.4rem;
background:rgba(255,223,0,0.1);border:1px solid rgba(255,223,0,0.3);
border-radius:999px;padding:.25rem .8rem;
font-size:.75rem;font-weight:800;color:var(–y);
margin-top:.4rem;
}
.xp-bar-wrap{
background:var(–s1);border-radius:14px;padding:.9rem 1rem;
margin:.8rem 1rem 0;border:1px solid rgba(255,255,255,0.06);
}
.xp-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:.5rem;}
.xp-label{font-size:.75rem;color:var(–muted);font-weight:700;}
.xp-val{font-size:.82rem;font-weight:900;color:var(–y);}
.xp-track{height:8px;background:rgba(255,255,255,0.08);border-radius:999px;overflow:hidden;}
.xp-fill{height:100%;background:linear-gradient(90deg,var(–b),var(–g),var(–y));border-radius:999px;transition:width .8s var(–transition);}

.session-banner{
margin:.8rem 1rem 0;
background:linear-gradient(135deg,rgba(0,156,59,0.15),rgba(0,39,118,0.2));
border:1px solid rgba(0,156,59,0.3);border-radius:14px;
padding:.8rem 1rem;display:flex;align-items:center;gap:.8rem;
}
.sb-icon{font-size:1.5rem;}
.sb-text{font-size:.82rem;font-weight:700;line-height:1.4;}
.sb-btn{
margin-left:auto;background:var(–g);color:white;
border:none;border-radius:10px;padding:.4rem .8rem;
font-size:.75rem;font-weight:800;cursor:pointer;white-space:nowrap;
font-family:‘Nunito’,sans-serif;
}

.section-title{
font-size:.7rem;font-weight:900;letter-spacing:.1em;text-transform:uppercase;
color:var(–muted);padding:.9rem 1rem .4rem;
}
.chapter-list{padding:0 1rem;display:flex;flex-direction:column;gap:.6rem;padding-bottom:.5rem;}
.chapter-card{
background:var(–s1);border-radius:14px;padding:1rem;
border:1.5px solid rgba(255,255,255,0.07);
cursor:pointer;transition:all .2s;display:flex;align-items:center;gap:.9rem;
}
.chapter-card:active{transform:scale(0.98);}
.chapter-card.active-ch{border-color:var(–y);background:rgba(255,223,0,0.07);}
.chapter-card.locked{opacity:.45;cursor:not-allowed;}
.chapter-card.done{border-color:rgba(0,156,59,0.4);background:rgba(0,156,59,0.07);}
.ch-icon{width:44px;height:44px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:1.4rem;flex-shrink:0;}
.ch-icon.c0{background:rgba(0,156,59,0.2);}
.ch-icon.c1{background:rgba(0,39,118,0.3);}
.ch-icon.c2{background:rgba(255,165,0,0.2);}
.ch-icon.c3{background:rgba(231,76,60,0.2);}
.ch-icon.c4{background:rgba(155,89,182,0.2);}
.ch-icon.c5{background:rgba(52,152,219,0.2);}
.ch-name{font-size:.9rem;font-weight:800;}
.ch-sub{font-size:.72rem;color:var(–muted);margin-top:.15rem;}
.ch-progress{display:flex;align-items:center;gap:.4rem;margin-top:.5rem;}
.ch-prog-track{flex:1;height:4px;background:rgba(255,255,255,0.08);border-radius:999px;overflow:hidden;}
.ch-prog-fill{height:100%;background:linear-gradient(90deg,var(–g),var(–y));border-radius:999px;transition:width .6s var(–transition);}
.ch-prog-pct{font-size:.65rem;font-weight:700;color:var(–muted);}
.ch-status{margin-left:auto;font-size:.75rem;font-weight:800;flex-shrink:0;}
.ch-status.done{color:var(–g);}
.ch-status.active{color:var(–y);}
.ch-status.locked{color:var(–muted);}

/* ═══════════════════════════════════════
CHAPTER DETAIL
═══════════════════════════════════════ */
#chapter-screen{padding-bottom:80px;}
.module-grid{display:grid;grid-template-columns:1fr 1fr;gap:.7rem;padding:.7rem 1rem;}
.module-tile{
background:var(–s1);border-radius:14px;padding:1.1rem .9rem;
border:1.5px solid rgba(255,255,255,0.07);
cursor:pointer;transition:all .2s;position:relative;overflow:hidden;
}
.module-tile:active{transform:scale(0.96);}
.module-tile.done-tile{border-color:rgba(0,156,59,0.35);}
.module-tile.locked-tile{opacity:.4;cursor:not-allowed;}
.mt-icon{font-size:1.8rem;margin-bottom:.5rem;}
.mt-name{font-size:.85rem;font-weight:800;margin-bottom:.2rem;}
.mt-desc{font-size:.68rem;color:var(–muted);line-height:1.3;}
.mt-xp{
position:absolute;top:.5rem;right:.5rem;
background:rgba(255,223,0,0.15);border:1px solid rgba(255,223,0,0.3);
border-radius:999px;padding:.1rem .45rem;
font-size:.6rem;font-weight:900;color:var(–y);
}
.mt-check{
position:absolute;bottom:.5rem;right:.5rem;
font-size:.85rem;
}

/* ═══════════════════════════════════════
FLASHCARD SCREEN
═══════════════════════════════════════ */
#flashcard-screen{padding-bottom:80px;}
.fc-container{
padding:1rem;display:flex;flex-direction:column;
align-items:center;min-height:calc(100vh - 120px);justify-content:center;
}
.fc-prog-row{width:100%;display:flex;align-items:center;gap:.7rem;margin-bottom:1rem;}
.fc-prog-track{flex:1;height:5px;background:rgba(255,255,255,0.1);border-radius:999px;overflow:hidden;}
.fc-prog-fill{height:100%;background:linear-gradient(90deg,var(–b),var(–g));border-radius:999px;transition:width .4s var(–transition);}
.fc-prog-label{font-size:.75rem;font-weight:800;color:var(–muted);min-width:40px;text-align:right;}

.card-stage{
width:100%;perspective:1200px;
margin-bottom:1.2rem;
}
.card-3d{
width:100%;min-height:210px;
transform-style:preserve-3d;
transition:transform .45s var(–transition);
cursor:pointer;position:relative;
}
.card-3d.flipped{transform:rotateY(180deg);}
.card-face{
position:absolute;inset:0;min-height:210px;
backface-visibility:hidden;border-radius:20px;
display:flex;flex-direction:column;
align-items:center;justify-content:center;
padding:1.5rem;text-align:center;
}
.cf-front{
background:linear-gradient(145deg,var(–s2),var(–s3));
border:1.5px solid rgba(255,255,255,0.1);
box-shadow:0 20px 60px rgba(0,0,0,0.4);
}
.cf-back{
background:linear-gradient(145deg,#0a2e16,#0f4020);
border:1.5px solid rgba(0,156,59,0.3);
box-shadow:0 20px 60px rgba(0,156,59,0.2);
transform:rotateY(180deg);
}
.cf-emoji{font-size:2.2rem;margin-bottom:.5rem;}
.cf-lang{font-size:.65rem;font-weight:800;letter-spacing:.12em;text-transform:uppercase;opacity:.5;margin-bottom:.4rem;}
.cf-word{font-family:‘Playfair Display’,serif;font-size:2.2rem;font-weight:900;line-height:1.1;margin-bottom:.3rem;}
.cf-phonetic{font-size:.82rem;color:rgba(255,255,255,0.55);font-style:italic;margin-top:.2rem;}
.cf-example{font-size:.8rem;color:rgba(255,255,255,0.7);margin-top:.7rem;line-height:1.6;font-style:italic;border-top:1px solid rgba(255,255,255,0.1);padding-top:.7rem;width:100%;}
.cf-tap{font-size:.68rem;opacity:.35;margin-top:.8rem;}

/* Answer buttons */
.answer-row{
display:flex;gap:.7rem;width:100%;
}
.ans-btn{
flex:1;border:none;border-radius:14px;padding:.9rem .5rem;
cursor:pointer;font-family:‘Nunito’,sans-serif;font-weight:800;
font-size:.9rem;transition:all .18s var(–transition);
display:flex;flex-direction:column;align-items:center;gap:.3rem;
}
.ans-btn:active{transform:scale(0.95);}
.ans-no{background:rgba(231,76,60,0.18);color:#ff7675;border:1.5px solid rgba(231,76,60,0.25);}
.ans-no:active{background:rgba(231,76,60,0.35);}
.ans-yes{background:rgba(0,156,59,0.18);color:#55efc4;border:1.5px solid rgba(0,156,59,0.25);}
.ans-yes:active{background:rgba(0,156,59,0.35);}
.ans-icon{font-size:1.4rem;}

/* Swipe indicator */
.swipe-hint{
font-size:.7rem;color:var(–muted);text-align:center;
padding:.4rem;margin-top:.3rem;
}

/* ═══════════════════════════════════════
GRAMMAR SCREEN
═══════════════════════════════════════ */
#grammar-screen{padding-bottom:80px;overflow-y:auto;}
.gram-content{padding:.5rem 1rem 1rem;}
.gram-lesson{
background:var(–s1);border-radius:16px;
border:1.5px solid rgba(255,255,255,0.07);
overflow:hidden;margin-bottom:.7rem;
}
.gram-header{
display:flex;align-items:center;gap:.8rem;
padding:.9rem 1rem;cursor:pointer;
}
.gram-h-icon{font-size:1.4rem;}
.gram-h-title{font-size:.9rem;font-weight:800;flex:1;}
.gram-h-arrow{font-size:.8rem;color:var(–muted);transition:transform .25s;}
.gram-lesson.open .gram-h-arrow{transform:rotate(180deg);}
.gram-body{
max-height:0;overflow:hidden;
transition:max-height .35s var(–transition);
}
.gram-lesson.open .gram-body{max-height:600px;}
.gram-inner{padding:0 1rem 1rem;}
.gram-rule-box{
background:rgba(255,223,0,0.06);border-radius:12px;
border:1px solid rgba(255,223,0,0.12);
padding:.9rem;margin-bottom:.7rem;
font-size:.84rem;line-height:1.8;
}
.gram-rule-box b{color:var(–y);}
.gram-example-box{
border-left:3px solid var(–g);padding-left:.8rem;
font-size:.82rem;color:rgba(255,255,255,0.75);
font-style:italic;line-height:1.7;
}
.gram-done-btn{
width:100%;margin-top:.8rem;padding:.65rem;
background:rgba(0,156,59,0.15);border:1px solid rgba(0,156,59,0.3);
border-radius:10px;color:var(–g);font-family:‘Nunito’,sans-serif;
font-size:.8rem;font-weight:800;cursor:pointer;
display:flex;align-items:center;justify-content:center;gap:.4rem;
}

/* ═══════════════════════════════════════
CONVERSATION SCREEN
═══════════════════════════════════════ */
#conv-screen{padding-bottom:80px;overflow-y:auto;}
.conv-scene-list{padding:.5rem 1rem;display:flex;flex-direction:column;gap:.6rem;}
.scene-card{
background:var(–s1);border-radius:14px;padding:.9rem 1rem;
border:1.5px solid rgba(255,255,255,0.07);
cursor:pointer;transition:all .2s;display:flex;align-items:center;gap:.9rem;
}
.scene-card:active{transform:scale(0.97);}
.scene-card.done{border-color:rgba(0,156,59,0.3);}
.sc-icon{font-size:1.8rem;flex-shrink:0;}
.sc-title{font-size:.88rem;font-weight:800;}
.sc-desc{font-size:.7rem;color:var(–muted);margin-top:.1rem;}
.sc-status{margin-left:auto;font-size:.85rem;}

#conv-play-screen{padding-bottom:80px;overflow-y:auto;}
.chat-area{padding:.8rem 1rem;display:flex;flex-direction:column;gap:.6rem;min-height:200px;}
.chat-msg{display:flex;gap:.5rem;max-width:88%;animation:fadeUp .25s var(–transition) both;}
.chat-msg.user{flex-direction:row-reverse;align-self:flex-end;}
.chat-av{width:30px;height:30px;border-radius:50%;background:var(–s2);display:flex;align-items:center;justify-content:center;font-size:.85rem;flex-shrink:0;margin-top:.1rem;}
.chat-bub{border-radius:14px;padding:.6rem .85rem;font-size:.84rem;line-height:1.55;}
.bot .chat-bub{background:var(–s2);border:1px solid rgba(255,255,255,0.07);border-radius:4px 14px 14px 14px;}
.user .chat-bub{background:var(–b);border-radius:14px 4px 14px 14px;}
.chat-tr{font-size:.7rem;color:var(–muted);margin-top:.2rem;font-style:italic;}

.choice-area{padding:.5rem 1rem 1rem;display:flex;flex-direction:column;gap:.5rem;}
.choice-label{font-size:.68rem;font-weight:900;letter-spacing:.08em;text-transform:uppercase;color:var(–muted);padding:.2rem 0;}
.choice-btn{
background:var(–s1);border:1.5px solid rgba(255,255,255,0.1);
border-radius:13px;padding:.8rem 1rem;
cursor:pointer;font-family:‘Nunito’,sans-serif;
text-align:left;transition:all .18s;
}
.choice-btn:active{transform:scale(0.97);}
.choice-btn.correct{border-color:var(–g)!important;background:rgba(0,156,59,0.18)!important;}
.choice-btn.wrong{border-color:var(–red)!important;background:rgba(231,76,60,0.18)!important;animation:shake .3s;}
.choice-btn.disabled{pointer-events:none;}
.cb-pt{font-size:.88rem;font-weight:800;color:var(–y);}
.cb-fr{font-size:.72rem;color:var(–muted);margin-top:.15rem;}

/* ═══════════════════════════════════════
PRONUNCIATION SCREEN
═══════════════════════════════════════ */
#pronun-screen{padding-bottom:80px;overflow-y:auto;}
.pronun-list{padding:.5rem 1rem;display:flex;flex-direction:column;gap:.7rem;}
.pronun-card{
background:var(–s1);border-radius:16px;padding:1.1rem;
border:1.5px solid rgba(255,255,255,0.07);
}
.pc-phrase{font-family:‘Playfair Display’,serif;font-size:1.3rem;font-weight:700;margin-bottom:.3rem;}
.pc-translation{font-size:.8rem;color:var(–muted);margin-bottom:.8rem;}
.pc-phonetic{
background:rgba(255,223,0,0.07);border-radius:10px;
padding:.5rem .8rem;font-size:.82rem;color:var(–y);
font-style:italic;margin-bottom:.8rem;
}
.pc-controls{display:flex;gap:.6rem;align-items:center;}
.pc-btn{
flex:1;padding:.65rem;border-radius:12px;border:none;
font-family:‘Nunito’,sans-serif;font-size:.8rem;font-weight:800;
cursor:pointer;display:flex;align-items:center;justify-content:center;gap:.4rem;
}
.pc-listen{background:rgba(0,39,118,0.4);color:#7fb3ff;}
.pc-speak{background:rgba(231,76,60,0.2);color:#ff9f9f;}
.pc-speak.recording{background:rgba(231,76,60,0.5);animation:pulse 1s infinite;}
.pc-result{
margin-top:.6rem;border-radius:10px;padding:.6rem .8rem;
font-size:.8rem;font-weight:700;display:none;
}
.pc-result.show{display:block;}
.pc-result.good{background:rgba(0,156,59,0.18);color:#55efc4;}
.pc-result.ok{background:rgba(255,165,0,0.18);color:#f39c12;}
.pc-result.retry{background:rgba(231,76,60,0.18);color:#ff7675;}

/* ═══════════════════════════════════════
QUIZ / TEST SCREEN
═══════════════════════════════════════ */
#quiz-screen{padding-bottom:80px;}
.quiz-container{padding:1rem;}
.quiz-header-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:.8rem;}
.quiz-score-pills{display:flex;gap:.5rem;}
.qsp{
background:var(–s1);border-radius:10px;padding:.4rem .75rem;
font-size:.78rem;font-weight:800;
display:flex;align-items:center;gap:.3rem;
}
.qsp.green{color:var(–g);}
.qsp.red{color:var(–red);}
.qsp.blue{color:#74b9ff;}

.quiz-prog-row{margin-bottom:.8rem;}
.quiz-prog-track{height:6px;background:rgba(255,255,255,0.08);border-radius:999px;overflow:hidden;}
.quiz-prog-fill{height:100%;background:linear-gradient(90deg,var(–b),var(–y));border-radius:999px;transition:width .4s var(–transition);}

.quiz-q-card{
background:var(–s1);border-radius:18px;padding:1.3rem;
border:1.5px solid rgba(255,255,255,0.08);margin-bottom:.9rem;
}
.qq-type{font-size:.65rem;font-weight:900;letter-spacing:.12em;text-transform:uppercase;color:var(–y);margin-bottom:.5rem;}
.qq-question{font-family:‘Playfair Display’,serif;font-size:1.7rem;font-weight:700;line-height:1.2;}
.qq-sub{font-size:.78rem;color:var(–muted);margin-top:.4rem;}
.qq-points{font-size:.72rem;font-weight:800;color:var(–g);margin-top:.4rem;}

.quiz-opts{display:flex;flex-direction:column;gap:.5rem;margin-bottom:.7rem;}
.qo{
background:var(–s1);border:1.5px solid rgba(255,255,255,0.1);
border-radius:13px;padding:.85rem 1rem;
cursor:pointer;font-family:‘Nunito’,sans-serif;
font-size:.88rem;font-weight:700;color:var(–text);
text-align:left;transition:all .18s;
display:flex;align-items:center;gap:.7rem;
}
.qo:active:not(.disabled){transform:scale(0.98);}
.qo:hover:not(.disabled):not(.correct):not(.wrong){border-color:rgba(255,255,255,0.25);}
.qo.correct{border-color:var(–g)!important;background:rgba(0,156,59,0.2)!important;color:#55efc4!important;}
.qo.wrong{border-color:var(–red)!important;background:rgba(231,76,60,0.2)!important;color:#ff7675!important;animation:shake .3s;}
.qo.disabled{pointer-events:none;}
.qo-letter{
width:26px;height:26px;border-radius:8px;
background:rgba(255,255,255,0.08);
display:flex;align-items:center;justify-content:center;
font-size:.75rem;font-weight:900;flex-shrink:0;
}

.quiz-feedback{
border-radius:12px;padding:.8rem 1rem;font-size:.85rem;
font-weight:700;display:none;margin-bottom:.7rem;
}
.quiz-feedback.show{display:block;}
.quiz-feedback.ok{background:rgba(0,156,59,0.18);border:1px solid rgba(0,156,59,0.3);color:#55efc4;}
.quiz-feedback.ko{background:rgba(231,76,60,0.18);border:1px solid rgba(231,76,60,0.3);color:#ff7675;}

/* Test result */
.test-result{
display:none;text-align:center;padding:1.5rem;
}
.test-result.show{display:block;animation:fadeUp .4s var(–transition);}
.tr-circle{
width:120px;height:120px;border-radius:50%;
background:var(–s2);border:3px solid var(–y);
display:flex;flex-direction:column;align-items:center;justify-content:center;
margin:0 auto 1rem;
}
.tr-score{font-family:‘Playfair Display’,serif;font-size:2rem;font-weight:900;color:var(–y);line-height:1;}
.tr-total{font-size:.75rem;color:var(–muted);}
.tr-grade{font-size:2rem;margin-bottom:.5rem;}
.tr-title{font-family:‘Playfair Display’,serif;font-size:1.5rem;font-weight:700;margin-bottom:.4rem;}
.tr-msg{font-size:.85rem;color:var(–muted);margin-bottom:1.5rem;line-height:1.6;}
.tr-breakdown{
background:var(–s1);border-radius:14px;padding:.9rem;
margin-bottom:1.2rem;text-align:left;
}
.trb-row{display:flex;justify-content:space-between;padding:.35rem 0;border-bottom:1px solid rgba(255,255,255,0.05);font-size:.82rem;}
.trb-row:last-child{border-bottom:none;}

/* ═══════════════════════════════════════
STATS / PROFILE SCREEN
═══════════════════════════════════════ */
#stats-screen{padding-bottom:80px;overflow-y:auto;}
.stats-content{padding:.5rem 1rem 1rem;}
.stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:.6rem;margin-bottom:.7rem;}
.stat-card{
background:var(–s1);border-radius:14px;padding:1rem;
border:1px solid rgba(255,255,255,0.06);text-align:center;
}
.sc-val{font-family:‘Playfair Display’,serif;font-size:2rem;font-weight:900;color:var(–y);}
.sc-lbl{font-size:.65rem;font-weight:800;text-transform:uppercase;letter-spacing:.08em;color:var(–muted);margin-top:.2rem;}

.badge-section-title{font-size:.7rem;font-weight:900;letter-spacing:.1em;text-transform:uppercase;color:var(–muted);margin:.5rem 0 .5rem;}
.badge-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:.5rem;}
.badge-item{
background:var(–s1);border-radius:12px;padding:.8rem .5rem;
text-align:center;border:1.5px solid rgba(255,255,255,0.06);
transition:all .2s;
}
.badge-item.unlocked{border-color:rgba(255,223,0,0.3);background:rgba(255,223,0,0.07);}
.badge-item.unlocked:hover{transform:translateY(-2px);}
.bi-icon{font-size:1.6rem;}
.bi-name{font-size:.62rem;font-weight:800;margin-top:.3rem;color:var(–muted);}
.badge-item.unlocked .bi-name{color:var(–y);}
.bi-req{font-size:.55rem;color:var(–muted);margin-top:.1rem;}

/* Scrollbar */
::-webkit-scrollbar{width:3px;}
::-webkit-scrollbar-track{background:transparent;}
::-webkit-scrollbar-thumb{background:rgba(255,255,255,0.15);border-radius:2px;}

/* ═══════════════════════════════════════
CONFETTI CANVAS
═══════════════════════════════════════ */
#confetti-canvas{position:fixed;inset:0;pointer-events:none;z-index:9999;display:none;}
</style>

</head>
<body>

<!-- Timer Bar -->

<div id="timer-bar">
  <span class="timer-icon">⏱️</span>
  <div class="timer-track"><div class="timer-fill" id="timer-fill"></div></div>
  <div class="timer-text" id="timer-text">60:00</div>
</div>

<!-- Toast -->

<div id="toast"></div>

<!-- Confetti -->

<canvas id="confetti-canvas"></canvas>

<!-- ══════════════ SPLASH ══════════════ -->

<div class="screen active" id="splash">
  <div class="splash-flag">🇧🇷</div>
  <h1 class="splash-title">Fala<br>Brasil!</h1>
  <p class="splash-sub">Portugais brésilien · 6 chapitres progressifs</p>
  <p style="font-size:.8rem;color:var(--muted);margin-bottom:1.3rem;">Choisis ton niveau pour commencer</p>
  <div class="level-list">
    <div class="level-row" onclick="startApp('debutant')">
      <span class="lr-emoji">🌱</span>
      <div><div class="lr-name">Débutant</div><div class="lr-desc">Absolument zéro en portugais</div></div>
      <span class="lr-arrow">›</span>
    </div>
    <div class="level-row" onclick="startApp('novice')">
      <span class="lr-emoji">🌿</span>
      <div><div class="lr-name">Novice</div><div class="lr-desc">Je connais quelques mots</div></div>
      <span class="lr-arrow">›</span>
    </div>
    <div class="level-row" onclick="startApp('moyen')">
      <span class="lr-emoji">🌳</span>
      <div><div class="lr-name">Moyen</div><div class="lr-desc">Je me débrouille un peu</div></div>
      <span class="lr-arrow">›</span>
    </div>
    <div class="level-row" onclick="startApp('fort')">
      <span class="lr-emoji">🦅</span>
      <div><div class="lr-name">Fort</div><div class="lr-desc">Je parle couramment</div></div>
      <span class="lr-arrow">›</span>
    </div>
    <div class="level-row" onclick="startApp('avance')">
      <span class="lr-emoji">🏆</span>
      <div><div class="lr-name">Avancé</div><div class="lr-desc">Niveau presque bilingue</div></div>
      <span class="lr-arrow">›</span>
    </div>
  </div>
</div>

<!-- ══════════════ HOME ══════════════ -->

<div class="screen" id="home">
  <div class="home-header">
    <div class="home-greeting" id="home-greeting">Bonjour 👋</div>
    <div class="home-name">Fala Brasil! 🇧🇷</div>
    <div class="home-level-badge" id="home-level-badge">🌱 Débutant</div>
  </div>

  <div class="xp-bar-wrap">
    <div class="xp-row">
      <span class="xp-label">⭐ Progression</span>
      <span class="xp-val" id="home-xp">0 XP</span>
    </div>
    <div class="xp-track"><div class="xp-fill" id="home-xp-fill" style="width:0%"></div></div>
  </div>

  <div class="session-banner" id="session-banner">
    <span class="sb-icon">📅</span>
    <div class="sb-text" id="session-text">Session du jour disponible !<br><small style="color:var(--muted)">1 heure · Mardi</small></div>
    <button class="sb-btn" onclick="startSession()">Commencer →</button>
  </div>

  <div class="section-title">📚 Chapitres</div>
  <div class="chapter-list" id="chapter-list"></div>
</div>

<!-- ══════════════ CHAPTER DETAIL ══════════════ -->

<div class="screen" id="chapter-screen">
  <div class="topbar">
    <button class="back-btn" onclick="navigate('home')">←</button>
    <div>
      <div class="topbar-title" id="ch-screen-title">Chapitre</div>
      <div class="topbar-sub" id="ch-screen-sub">Modules disponibles</div>
    </div>
  </div>
  <div class="module-grid" id="module-grid"></div>
  <div style="padding:0 1rem" id="test-unlock-banner" style="display:none"></div>
</div>

<!-- ══════════════ FLASHCARD SCREEN ══════════════ -->

<div class="screen" id="flashcard-screen">
  <div class="topbar">
    <button class="back-btn" onclick="navigate('chapter-screen')">←</button>
    <div>
      <div class="topbar-title">📚 Vocabulaire</div>
      <div class="topbar-sub" id="fc-chapter-name">Chapitre</div>
    </div>
  </div>
  <div class="fc-container">
    <div class="fc-prog-row">
      <div class="fc-prog-track"><div class="fc-prog-fill" id="fc-prog-fill"></div></div>
      <div class="fc-prog-label" id="fc-prog-label">0/0</div>
    </div>
    <div class="card-stage">
      <div class="card-3d" id="card-3d" onclick="flipCard()">
        <div class="card-face cf-front">
          <div class="cf-emoji" id="cf-emoji">🌟</div>
          <div class="cf-lang">🇫🇷 Français</div>
          <div class="cf-word" id="cf-fr">—</div>
          <div class="cf-tap">Touchez pour voir en portugais</div>
        </div>
        <div class="card-face cf-back">
          <div class="cf-emoji" id="cf-emoji2">🌟</div>
          <div class="cf-lang">🇧🇷 Português</div>
          <div class="cf-word" id="cf-pt">—</div>
          <div class="cf-phonetic" id="cf-phonetic">—</div>
          <div class="cf-example" id="cf-example">—</div>
        </div>
      </div>
    </div>
    <div class="answer-row" id="answer-row" style="display:none">
      <button class="ans-btn ans-no" onclick="answerCard(false)">
        <span class="ans-icon">😕</span>À revoir
      </button>
      <button class="ans-btn ans-yes" onclick="answerCard(true)">
        <span class="ans-icon">✅</span>Je sais !
      </button>
    </div>
    <div class="swipe-hint" id="swipe-hint">Touchez la carte pour la retourner</div>
  </div>
</div>

<!-- ══════════════ GRAMMAR SCREEN ══════════════ -->

<div class="screen" id="grammar-screen">
  <div class="topbar">
    <button class="back-btn" onclick="navigate('chapter-screen')">←</button>
    <div>
      <div class="topbar-title">📐 Grammaire</div>
      <div class="topbar-sub" id="gram-chapter-name">Chapitre</div>
    </div>
  </div>
  <div class="gram-content" id="gram-content"></div>
</div>

<!-- ══════════════ CONVERSATION SCREEN ══════════════ -->

<div class="screen" id="conv-screen">
  <div class="topbar">
    <button class="back-btn" onclick="navigate('chapter-screen')">←</button>
    <div>
      <div class="topbar-title">💬 Conversations</div>
      <div class="topbar-sub" id="conv-chapter-name">Choisir une scène</div>
    </div>
  </div>
  <div class="conv-scene-list" id="conv-scene-list"></div>
</div>

<!-- CONVERSATION PLAY -->

<div class="screen" id="conv-play-screen">
  <div class="topbar">
    <button class="back-btn" onclick="navigate('conv-screen')">←</button>
    <div>
      <div class="topbar-title" id="conv-play-title">Conversation</div>
      <div class="topbar-sub" id="conv-play-sub"></div>
    </div>
  </div>
  <div class="chat-area" id="chat-area"></div>
  <div class="choice-area" id="choice-area"></div>
</div>

<!-- ══════════════ PRONUNCIATION ══════════════ -->

<div class="screen" id="pronun-screen">
  <div class="topbar">
    <button class="back-btn" onclick="navigate('chapter-screen')">←</button>
    <div>
      <div class="topbar-title">🎤 Prononciation</div>
      <div class="topbar-sub" id="pronun-chapter-name">Pratiquer à voix haute</div>
    </div>
  </div>
  <div class="pronun-list" id="pronun-list"></div>
</div>

<!-- ══════════════ QUIZ / TEST ══════════════ -->

<div class="screen" id="quiz-screen">
  <div class="topbar">
    <button class="back-btn" onclick="navigate('chapter-screen')">←</button>
    <div>
      <div class="topbar-title" id="quiz-screen-title">🏆 Test</div>
      <div class="topbar-sub" id="quiz-screen-sub">Noté sur 60 points</div>
    </div>
  </div>
  <div class="quiz-container">
    <div class="quiz-header-row">
      <div class="quiz-score-pills">
        <div class="qsp green">✅ <span id="qs-ok">0</span></div>
        <div class="qsp red">❌ <span id="qs-ko">0</span></div>
        <div class="qsp blue">📝 <span id="qs-left">0</span> rest.</div>
      </div>
      <div style="font-size:.78rem;font-weight:800;color:var(--y)" id="quiz-pts-display">0 pts</div>
    </div>
    <div class="quiz-prog-row">
      <div class="quiz-prog-track"><div class="quiz-prog-fill" id="quiz-prog-fill"></div></div>
    </div>
    <div class="quiz-q-card" id="quiz-q-card">
      <div class="qq-type" id="qq-type">QUESTION</div>
      <div class="qq-question" id="qq-question">Chargement…</div>
      <div class="qq-sub" id="qq-sub"></div>
      <div class="qq-points" id="qq-points"></div>
    </div>
    <div class="quiz-opts" id="quiz-opts"></div>
    <div class="quiz-feedback" id="quiz-feedback"></div>
    <div class="test-result" id="test-result">
      <div class="tr-circle"><div class="tr-score" id="tr-score">0</div><div class="tr-total">/60</div></div>
      <div class="tr-grade" id="tr-grade">🎉</div>
      <div class="tr-title" id="tr-title">Résultat</div>
      <div class="tr-msg" id="tr-msg"></div>
      <div class="tr-breakdown" id="tr-breakdown"></div>
      <button class="btn btn-yellow btn-full btn-lg" onclick="navigate('chapter-screen')">Continuer →</button>
    </div>
  </div>
</div>

<!-- ══════════════ STATS ══════════════ -->

<div class="screen" id="stats-screen">
  <div class="topbar" style="padding-top:calc(.9rem + 35px)">
    <div style="flex:1">
      <div class="topbar-title">📊 Mon profil</div>
      <div class="topbar-sub">Progression & badges</div>
    </div>
  </div>
  <div class="stats-content">
    <div class="stats-grid">
      <div class="stat-card"><div class="sc-val" id="st-xp">0</div><div class="sc-lbl">⭐ Total XP</div></div>
      <div class="stat-card"><div class="sc-val" id="st-streak">0</div><div class="sc-lbl">🔥 Jours suite</div></div>
      <div class="stat-card"><div class="sc-val" id="st-words">0</div><div class="sc-lbl">📚 Mots appris</div></div>
      <div class="stat-card"><div class="sc-val" id="st-tests">—</div><div class="sc-lbl">🏆 Moy. tests</div></div>
    </div>
    <div class="badge-section-title">🏅 Badges débloqués</div>
    <div class="badge-grid" id="badge-grid"></div>
  </div>
</div>

<!-- ══════════════ BOTTOM NAV ══════════════ -->

<nav id="bottom-nav">
  <button class="nb on" onclick="navTo('home',this)" id="nb-home">
    <span class="ni">🏠</span><span class="nl">Accueil</span>
  </button>
  <button class="nb" onclick="navTo('home',this,'chapters')" id="nb-chapters">
    <span class="ni">📖</span><span class="nl">Chapitres</span>
  </button>
  <button class="nb" onclick="navToConv(this)" id="nb-conv">
    <span class="ni">💬</span><span class="nl">Converser</span>
  </button>
  <button class="nb" onclick="navToPronun(this)" id="nb-pronun">
    <span class="ni">🎤</span><span class="nl">Prononcer</span>
  </button>
  <button class="nb" onclick="navTo('stats-screen',this)" id="nb-stats">
    <span class="ni">📊</span><span class="nl">Profil</span>
  </button>
</nav>

<script>
/* ═══════════════════════════════════════════════════════
   DATA — 6 CHAPTERS
═══════════════════════════════════════════════════════ */
const CHAPTERS = [
{
  id:0, name:"Premiers pas", emoji:"🌱", color:"c0",
  desc:"Salutations, chiffres, se présenter",
  vocab:[
    {fr:"Bonjour",pt:"Olá / Bom dia",ph:"[o-LA / bõ JI-a]",ex:"Olá! Como vai? — Bonjour ! Comment ça va ?",em:"👋"},
    {fr:"Bonsoir",pt:"Boa tarde / Boa noite",ph:"[BO-a TAR-ji / NOY-chi]",ex:"Boa noite! — Bonsoir !",em:"🌙"},
    {fr:"Au revoir",pt:"Tchau / Até logo",ph:"[TCHAW / a-TE LO-go]",ex:"Tchau! Até amanhã! — Au revoir ! À demain !",em:"👋"},
    {fr:"Merci",pt:"Obrigado/a",ph:"[o-bri-GA-do]",ex:"Muito obrigado! — Merci beaucoup !",em:"💛"},
    {fr:"S'il vous plaît",pt:"Por favor",ph:"[por fa-VOR]",ex:"Um café, por favor. — Un café, s'il vous plaît.",em:"🙏"},
    {fr:"Oui",pt:"Sim",ph:"[SÎ]",ex:"Sim, eu quero. — Oui, je veux.",em:"✅"},
    {fr:"Non",pt:"Não",ph:"[NÃO]",ex:"Não, obrigado. — Non, merci.",em:"❌"},
    {fr:"Comment t'appelles-tu ?",pt:"Como você se chama?",ph:"[KO-mo vo-SE si SHA-ma]",ex:"Como você se chama? — Sou o Pedro. — Comment tu t'appelles ? — Je suis Pedro.",em:"🙋"},
    {fr:"Je m'appelle…",pt:"Meu nome é…",ph:"[MEU NO-mi E]",ex:"Meu nome é Maria. — Je m'appelle Maria.",em:"😊"},
    {fr:"Enchanté(e)",pt:"Muito prazer!",ph:"[MOOY-to pra-ZER]",ex:"Muito prazer em te conhecer! — Enchanté(e) de te rencontrer !",em:"🤝"},
    {fr:"Un / Une",pt:"Um / Uma",ph:"[ũ / U-ma]",ex:"Uma água, por favor.",em:"1️⃣"},
    {fr:"Deux",pt:"Dois / Duas",ph:"[DOYSS]",ex:"Dois cafés, obrigado.",em:"2️⃣"},
    {fr:"Trois",pt:"Três",ph:"[TRAYSS]",ex:"Três horas da tarde.",em:"3️⃣"},
    {fr:"Dix",pt:"Dez",ph:"[DEZZ]",ex:"Dez reais, por favor.",em:"🔟"},
    {fr:"Cent",pt:"Cem",ph:"[SÊ]",ex:"Cem reais.",em:"💯"},
  ],
  grammar:[
    {
      title:"SER — Être (identité permanente)",emoji:"⚓",
      rule:`<b>Eu sou</b> — Je suis<br><b>Você é</b> — Tu es / Vous êtes<br><b>Ele/Ela é</b> — Il/Elle est<br><b>Nós somos</b> — Nous sommes<br><b>Vocês são</b> — Vous êtes (pluriel)<br><b>Eles/Elas são</b> — Ils/Elles sont`,
      ex:`Eu sou francês. (Je suis français.)<br>Ela é professora. (Elle est professeure.)<br>Nós somos amigos. (Nous sommes amis.)`
    },
    {
      title:"Pronoms personnels sujets",emoji:"👤",
      rule:`<b>Eu</b> — Je<br><b>Você</b> — Tu / Vous (le plus courant au Brésil)<br><b>Ele / Ela</b> — Il / Elle<br><b>Nós</b> — Nous<br><b>Vocês</b> — Vous (pluriel)<br><b>Eles / Elas</b> — Ils / Elles<br><br>⚠️ Au Brésil, <b>você</b> remplace "tu" dans la vie quotidienne.`,
      ex:`Você fala português? (Tu parles portugais ?)<br>Eles moram aqui. (Ils habitent ici.)`
    },
    {
      title:"La négation simple avec NÃO",emoji:"🚫",
      rule:`Mets simplement <b>NÃO</b> avant le verbe :<br><br>→ Eu falo. → Eu <b>não</b> falo.<br>→ Ele é. → Ele <b>não</b> é.<br><br>Aucune autre modification nécessaire !`,
      ex:`Não entendo. (Je ne comprends pas.)<br>Não sou daqui. (Je ne suis pas d'ici.)<br>Ela não é brasileira. (Elle n'est pas brésilienne.)`
    },
  ],
  conversations:[
    {
      title:"Présentation mutuelle",scene:"🤝 Première rencontre",
      steps:[
        {role:"bot",msg:"Oi! Tudo bem? Como você se chama?",tr:"Salut ! Tout va bien ? Comment tu t'appelles ?"},
        {role:"choice",opts:[
          {pt:"Olá! Me chamo Lucas. E você?",fr:"Salut ! Je m'appelle Lucas. Et toi ?",correct:true},
          {pt:"Não gosto de futebol.",fr:"Je n'aime pas le football.",correct:false},
          {pt:"Boa noite!",fr:"Bonne nuit !",correct:false},
        ]},
        {role:"bot",msg:"Prazer, Lucas! Sou a Ana. Você é francês?",tr:"Enchanté, Lucas ! Je suis Ana. Tu es français ?"},
        {role:"choice",opts:[
          {pt:"Sim, sou da França. E você, é brasileira?",fr:"Oui, je viens de France. Et toi, tu es brésilienne ?",correct:true},
          {pt:"Não, obrigado.",fr:"Non, merci.",correct:false},
          {pt:"Onde fica o banheiro?",fr:"Où sont les toilettes ?",correct:false},
        ]},
        {role:"bot",msg:"Sim! Muito prazer em te conhecer!",tr:"Oui ! Enchanté(e) de te connaître !"},
      ]
    },
  ],
  pronunciation:[
    {phrase:"Olá! Tudo bem?",tr:"Salut ! Tout va bien ?",ph:"[o-LA TOO-do bẽ]",tips:"Le 'o' de Olá est accentué. 'Tudo' se prononce 'TUdo'."},
    {phrase:"Muito prazer em te conhecer.",tr:"Enchanté(e) de te connaître.",ph:"[MOOY-to pra-ZER ẽ chi ko-nyeSSER]",tips:"'Muito' = 'MOOY-to'. 'Conhecer' : le 'c' final se prononce comme 'ss'."},
    {phrase:"Como você se chama?",tr:"Comment tu t'appelles ?",ph:"[KO-mo vo-SE si SHA-ma]",tips:"'Você' = 'vo-SE'. Le 'ch' brésilien = 'sh' français."},
    {phrase:"Meu nome é François.",tr:"Je m'appelle François.",ph:"[MEU NO-mi E]",tips:"'Nome' = 'NO-mi'. Le 'e' final se prononce 'i' au Brésil."},
  ],
},{
  id:1, name:"La vie quotidienne", emoji:"🌿", color:"c1",
  desc:"Maison, nourriture, famille, corps humain",
  vocab:[
    {fr:"Eau",pt:"Água",ph:"[A-gwa]",ex:"Um copo de água, por favor.",em:"💧"},
    {fr:"Nourriture",pt:"Comida",ph:"[ko-MI-da]",ex:"A comida está deliciosa!",em:"🍽️"},
    {fr:"Manger",pt:"Comer",ph:"[ko-MER]",ex:"Vamos comer? — On mange ?",em:"🍖"},
    {fr:"Boire",pt:"Beber",ph:"[be-BER]",ex:"Quer beber algo? — Tu veux boire quelque chose ?",em:"🥤"},
    {fr:"Maison",pt:"Casa",ph:"[KA-za]",ex:"Minha casa é sua casa!",em:"🏠"},
    {fr:"Famille",pt:"Família",ph:"[fa-MI-lya]",ex:"Minha família é muito grande.",em:"👨‍👩‍👧"},
    {fr:"Père",pt:"Pai",ph:"[PAI]",ex:"Meu pai é médico.",em:"👨"},
    {fr:"Mère",pt:"Mãe",ph:"[MÃE]",ex:"Minha mãe é professora.",em:"👩"},
    {fr:"Frère",pt:"Irmão",ph:"[ir-MÃO]",ex:"Tenho dois irmãos.",em:"👦"},
    {fr:"Sœur",pt:"Irmã",ph:"[ir-MÃ]",ex:"Minha irmã mora em São Paulo.",em:"👧"},
    {fr:"Ami(e)",pt:"Amigo/a",ph:"[a-MI-go]",ex:"Ele é meu melhor amigo.",em:"🤝"},
    {fr:"Travail",pt:"Trabalho",ph:"[tra-BA-lyo]",ex:"Tenho muito trabalho hoje.",em:"💼"},
    {fr:"École",pt:"Escola",ph:"[esh-KO-la]",ex:"Vou para a escola de ônibus.",em:"🏫"},
    {fr:"Voiture",pt:"Carro",ph:"[KA-rro]",ex:"Meu carro é vermelho.",em:"🚗"},
    {fr:"Téléphone",pt:"Telefone",ph:"[te-le-FO-ni]",ex:"Meu telefone está sem bateria.",em:"📱"},
  ],
  grammar:[
    {
      title:"ESTAR — Être (état temporaire)",emoji:"🌡️",
      rule:`<b>Eu estou</b> — Je suis (temporairement)<br><b>Você está</b> — Tu es<br><b>Ele/Ela está</b> — Il/Elle est<br><b>Nós estamos</b> — Nous sommes<br><b>Vocês estão</b> — Vous êtes<br><b>Eles estão</b> — Ils sont<br><br>💡 <b>SER vs ESTAR</b> : SER = permanent, ESTAR = temporaire`,
      ex:`Estou cansado. (Je suis fatigué → temporaire)<br>Sou alto. (Je suis grand → permanent)<br>A comida está fria. (La nourriture est froide → temporaire)`
    },
    {
      title:"TER — Avoir",emoji:"✋",
      rule:`<b>Eu tenho</b> — J'ai<br><b>Você tem</b> — Tu as<br><b>Ele/Ela tem</b> — Il/Elle a<br><b>Nós temos</b> — Nous avons<br><b>Vocês têm</b> — Vous avez<br><b>Eles têm</b> — Ils ont`,
      ex:`Tenho fome. (J'ai faim.)<br>Você tem irmãos? (Tu as des frères et sœurs ?)<br>Nós temos um carro. (Nous avons une voiture.)`
    },
    {
      title:"Articles : O, A, Um, Uma",emoji:"📝",
      rule:`<b>Définis :</b><br>→ <b>O</b> (masc. sing.) — o carro (la voiture)<br>→ <b>A</b> (fém. sing.) — a casa (la maison)<br>→ <b>Os/As</b> (pluriel) — os carros / as casas<br><br><b>Indéfinis :</b><br>→ <b>Um</b> (masc.) — um carro (une voiture)<br>→ <b>Uma</b> (fém.) — uma casa (une maison)`,
      ex:`O Brasil é lindo! (Le Brésil est magnifique !)<br>Uma cerveja, por favor. (Une bière, s'il vous plaît.)<br>As praias são incríveis. (Les plages sont incroyables.)`
    },
  ],
  conversations:[
    {
      title:"Chez le marchand",scene:"🛒 Au marché",
      steps:[
        {role:"bot",msg:"Bom dia! Posso te ajudar?",tr:"Bonjour ! Je peux t'aider ?"},
        {role:"choice",opts:[
          {pt:"Quanto custa o quilo de manga?",fr:"Combien coûte le kilo de mangue ?",correct:true},
          {pt:"Boa noite!",fr:"Bonne nuit !",correct:false},
          {pt:"Eu moro em Paris.",fr:"J'habite à Paris.",correct:false},
        ]},
        {role:"bot",msg:"A manga está a R$6 o quilo. Quer provar?",tr:"La mangue est à 6 reais le kilo. Vous voulez goûter ?"},
        {role:"choice",opts:[
          {pt:"Sim! Também quero meio quilo de abacaxi.",fr:"Oui ! Je veux aussi un demi-kilo d'ananas.",correct:true},
          {pt:"Não tenho dinheiro.",fr:"Je n'ai pas d'argent.",correct:false},
          {pt:"Estou cansado.",fr:"Je suis fatigué.",correct:false},
        ]},
        {role:"bot",msg:"Ótima escolha! Vai ser R$9,00 no total.",tr:"Excellent choix ! Ça fera 9 reais au total."},
        {role:"choice",opts:[
          {pt:"Pode parcelar no cartão?",fr:"Je peux payer en plusieurs fois par carte ?",correct:true},
          {pt:"Obrigado, tchau!",fr:"Merci, au revoir !",correct:true},
          {pt:"Tenho fome.",fr:"J'ai faim.",correct:false},
        ]},
        {role:"bot",msg:"Claro! Aqui está seu troco. Obrigado!",tr:"Bien sûr ! Voici votre monnaie. Merci !"},
      ]
    },
  ],
  pronunciation:[
    {phrase:"Tenho muita fome agora.",tr:"J'ai très faim maintenant.",ph:"[TE-nyo MOOY-ta FO-mi a-GO-ra]",tips:"'Tenho' : le 'nh' = 'gn' français comme dans 'montagne'."},
    {phrase:"Minha família mora no Rio.",tr:"Ma famille habite à Rio.",ph:"[MI-nya fa-MI-lya MO-ra no RIO]",tips:"'Minha' : 'nh' = son nasal. 'Mora' = habite, vit."},
    {phrase:"A comida está deliciosa!",tr:"La nourriture est délicieuse !",ph:"[a ko-MI-da esh-TA de-li-SYO-za]",tips:"'Está' accentué sur le 'A'. 'Deliciosa' = de-li-SYO-za."},
  ],
},{
  id:2, name:"En ville & voyages", emoji:"🌳", color:"c2",
  desc:"Transport, hôtels, directions, météo",
  vocab:[
    {fr:"Plage",pt:"Praia",ph:"[PRA-ya]",ex:"A praia de Copacabana é linda!",em:"🏖️"},
    {fr:"Hôtel",pt:"Hotel",ph:"[o-TEL]",ex:"O hotel fica perto do centro.",em:"🏨"},
    {fr:"Avion",pt:"Avião",ph:"[a-vi-ÃO]",ex:"O avião parte às 10h.",em:"✈️"},
    {fr:"Bus",pt:"Ônibus",ph:"[O-ni-bus]",ex:"Pego o ônibus todo dia.",em:"🚌"},
    {fr:"Taxi",pt:"Táxi",ph:"[TAK-si]",ex:"Pode chamar um táxi?",em:"🚕"},
    {fr:"À gauche",pt:"À esquerda",ph:"[a esh-KER-da]",ex:"Vire à esquerda no semáforo.",em:"⬅️"},
    {fr:"À droite",pt:"À direita",ph:"[a di-REY-ta]",ex:"O banco fica à direita.",em:"➡️"},
    {fr:"Tout droit",pt:"Em frente / Reto",ph:"[ẽ FRÊN-chi]",ex:"Continue em frente por 200 metros.",em:"⬆️"},
    {fr:"Combien ça coûte ?",pt:"Quanto custa?",ph:"[KWÃN-to KUSH-ta]",ex:"Quanto custa a passagem?",em:"💰"},
    {fr:"Billet",pt:"Passagem / Ingresso",ph:"[pa-SA-jẽ]",ex:"Dois ingressos, por favor.",em:"🎟️"},
    {fr:"Il fait chaud",pt:"Está quente / Faz calor",ph:"[esh-TA KÊN-chi]",ex:"Hoje está muito quente!",em:"☀️"},
    {fr:"Il pleut",pt:"Está chovendo",ph:"[esh-TA sho-VÊN-do]",ex:"Está chovendo muito lá fora.",em:"🌧️"},
    {fr:"Carte / Plan",pt:"Mapa",ph:"[MA-pa]",ex:"Você tem um mapa da cidade?",em:"🗺️"},
    {fr:"Où se trouve… ?",pt:"Onde fica… ?",ph:"[ÕN-ji FI-ka]",ex:"Onde fica o metrô?",em:"❓"},
    {fr:"Aéroport",pt:"Aeroporto",ph:"[a-e-ro-POR-to]",ex:"Como chego ao aeroporto?",em:"🛫"},
  ],
  grammar:[
    {
      title:"Verbes réguliers en -AR au présent",emoji:"🔄",
      rule:`<b>FALAR</b> (parler) :<br>Eu fal<b>o</b> — Você fal<b>a</b> — Ele fal<b>a</b><br>Nós fal<b>amos</b> — Vocês fal<b>am</b> — Eles fal<b>am</b><br><br>Même modèle : morar (habiter), trabalhar (travailler), comprar (acheter), gostar (aimer)`,
      ex:`Eu moro em Paris. (J'habite à Paris.)<br>Ela trabalha muito. (Elle travaille beaucoup.)<br>Nós compramos frutas. (Nous achetons des fruits.)`
    },
    {
      title:"Questions avec mots interrogatifs",emoji:"❓",
      rule:`<b>O que?</b> — Quoi / Qu'est-ce que<br><b>Onde?</b> — Où<br><b>Quando?</b> — Quand<br><b>Como?</b> — Comment<br><b>Por que?</b> — Pourquoi<br><b>Quem?</b> — Qui<br><b>Quanto(s)/Quanta(s)?</b> — Combien`,
      ex:`O que você quer? (Que veux-tu ?)<br>Onde você mora? (Où habites-tu ?)<br>Quando você chega? (Quand arrives-tu ?)<br>Por que você está triste? (Pourquoi es-tu triste ?)`
    },
  ],
  conversations:[
    {
      title:"Dans le taxi",scene:"🚕 Se déplacer",
      steps:[
        {role:"bot",msg:"Boa noite! Para onde você vai?",tr:"Bonsoir ! Vous allez où ?"},
        {role:"choice",opts:[
          {pt:"Para o aeroporto, por favor. Com urgência!",fr:"À l'aéroport, s'il vous plaît. C'est urgent !",correct:true},
          {pt:"Estou com fome.",fr:"J'ai faim.",correct:false},
          {pt:"Bom dia!",fr:"Bonjour !",correct:false},
        ]},
        {role:"bot",msg:"Tudo bem! Vai levar uns 30 minutos. Tem trânsito.",tr:"D'accord ! Ça va prendre 30 minutes. Il y a des embouteillages."},
        {role:"choice",opts:[
          {pt:"Quanto vai custar a corrida?",fr:"Combien va coûter la course ?",correct:true},
          {pt:"Eu não sei.",fr:"Je ne sais pas.",correct:false},
          {pt:"Faz calor hoje.",fr:"Il fait chaud aujourd'hui.",correct:false},
        ]},
        {role:"bot",msg:"Pela autoestrada, R$45. Aceita cartão?",tr:"Par l'autoroute, 45 reais. Vous acceptez la carte ?"},
        {role:"choice",opts:[
          {pt:"Sim, pode ser no débito.",fr:"Oui, en débit ça va.",correct:true},
          {pt:"Não entendo.",fr:"Je ne comprends pas.",correct:false},
          {pt:"Obrigado, tchau.",fr:"Merci, au revoir.",correct:false},
        ]},
        {role:"bot",msg:"Ótimo! Chegamos em 30 minutos. Pode relaxar.",tr:"Parfait ! On arrive dans 30 minutes. Vous pouvez vous détendre."},
      ]
    },
  ],
  pronunciation:[
    {phrase:"Onde fica o metrô mais próximo?",tr:"Où se trouve le métro le plus proche ?",ph:"[ÕN-ji FI-ka o me-TRO mayss PRO-si-mo]",tips:"'Onde' = 'ÕN-ji'. 'Próximo' : accent sur PRO."},
    {phrase:"Quanto custa a passagem de ônibus?",tr:"Combien coûte le billet de bus ?",ph:"[KWÃN-to KUSH-ta a pa-SA-jẽ di O-ni-bus]",tips:"'Quanto' : le 'qu' se prononce 'kw'. 'Custa' = coûte."},
    {phrase:"Está chovendo muito lá fora.",tr:"Il pleut beaucoup dehors.",ph:"[esh-TA sho-VÊN-do MOOY-to LA FO-ra]",tips:"'Chovendo' = 'sho-VÊN-do'. Le 'ch' = 'sh'."},
  ],
},{
  id:3, name:"Émotions & culture", emoji:"🦅", color:"c3",
  desc:"Sentiments, musique, fêtes brésiliennes",
  vocab:[
    {fr:"Heureux/Heureuse",pt:"Feliz",ph:"[fe-LIZZ]",ex:"Estou muito feliz hoje!",em:"😄"},
    {fr:"Triste",pt:"Triste",ph:"[TRISH-chi]",ex:"Por que você está triste?",em:"😢"},
    {fr:"Amour",pt:"Amor",ph:"[a-MOR]",ex:"O amor é lindo!",em:"❤️"},
    {fr:"Saudade",pt:"Saudade",ph:"[saw-DA-ji]",ex:"Tenho saudade do Brasil. (Ce mot n'existe qu'en portugais !)",em:"💙"},
    {fr:"Incroyable",pt:"Incrível",ph:"[in-KRI-vel]",ex:"O show foi incrível!",em:"🤩"},
    {fr:"Musique",pt:"Música",ph:"[MU-zi-ka]",ex:"Adoro a música brasileira!",em:"🎵"},
    {fr:"Fête / Carnaval",pt:"Festa / Carnaval",ph:"[FES-ta / kar-na-VAL]",ex:"O carnaval do Rio é famoso no mundo todo.",em:"🎉"},
    {fr:"Plage",pt:"Praia",ph:"[PRA-ya]",ex:"Adoro ir à praia no verão.",em:"🏖️"},
    {fr:"Foot / Football",pt:"Futebol",ph:"[fu-chi-BOL]",ex:"O futebol é a paixão do Brasil.",em:"⚽"},
    {fr:"Chanter",pt:"Cantar",ph:"[kãn-TAR]",ex:"Ela canta muito bem.",em:"🎤"},
    {fr:"Danser",pt:"Dançar",ph:"[dãn-SAR]",ex:"Vamos dançar samba!",em:"💃"},
    {fr:"Rire",pt:"Rir",ph:"[HIR]",ex:"Ele faz todo mundo rir.",em:"😂"},
    {fr:"Pleurer",pt:"Chorar",ph:"[sho-RAR]",ex:"Não chore! — Ne pleure pas !",em:"😭"},
    {fr:"Rêver",pt:"Sonhar",ph:"[so-NYAR]",ex:"Sonho em visitar o Brasil.",em:"💭"},
    {fr:"Profiter",pt:"Aproveitar",ph:"[a-pro-vey-TAR]",ex:"Aproveita a vida! — Profite de la vie !",em:"🌟"},
  ],
  grammar:[
    {
      title:"Futur proche — IR + infinitif",emoji:"⏩",
      rule:`<b>Vou + infinitif</b> = Je vais…<br><b>Vai + infinitif</b> = Tu vas…<br><b>Vamos + infinitif</b> = Nous allons…<br><br>C'est la forme de futur la plus utilisée au Brésil !<br>Le futur simple est rare dans la conversation.`,
      ex:`Vou viajar para o Rio. (Je vais voyager à Rio.)<br>Vamos comer churrasco! (On va manger un barbecue !)<br>Ela vai estudar amanhã. (Elle va étudier demain.)`
    },
    {
      title:"GOSTAR DE — Aimer (goûts)",emoji:"❤️",
      rule:`<b>Gosto de…</b> = J'aime…<br><b>Não gosto de…</b> = Je n'aime pas…<br><b>Adoro…</b> = J'adore…<br><b>Odeio…</b> = Je déteste…<br><br>⚠️ Toujours suivi de <b>DE</b> ! (différent du français)`,
      ex:`Gosto muito de samba. (J'aime beaucoup le samba.)<br>Não gosto de frio. (Je n'aime pas le froid.)<br>Adoro a culinária brasileira! (J'adore la cuisine brésilienne !)`
    },
    {
      title:"Accord des adjectifs (genre & nombre)",emoji:"🎨",
      rule:`Les adjectifs s'accordent avec le nom :<br><b>Masculin sing. :</b> bonito / feliz<br><b>Féminin sing. :</b> bonit<b>a</b> / feliz<br><b>Masculin plur. :</b> bonit<b>os</b> / feliz<b>es</b><br><b>Féminin plur. :</b> bonit<b>as</b> / feliz<b>es</b><br><br>L'adjectif se place généralement <b>après</b> le nom.`,
      ex:`Um menino bonito. (Un beau garçon.)<br>Uma menina bonita. (Une belle fille.)<br>Músicas lindas. (De belles musiques.)`
    },
  ],
  conversations:[
    {
      title:"Au concert",scene:"🎵 Parler de musique",
      steps:[
        {role:"bot",msg:"Uau! Você gostou do show?",tr:"Wow ! Tu as aimé le concert ?"},
        {role:"choice",opts:[
          {pt:"Adorei! Foi incrível demais!",fr:"J'ai adoré ! C'était vraiment incroyable !",correct:true},
          {pt:"Não entendo música.",fr:"Je ne comprends pas la musique.",correct:false},
          {pt:"Estou com sono.",fr:"J'ai sommeil.",correct:false},
        ]},
        {role:"bot",msg:"Eu também! Você gosta de samba ou prefere axé?",tr:"Moi aussi ! Tu préfères le samba ou l'axé ?"},
        {role:"choice",opts:[
          {pt:"Adoro samba! Mas não sei dançar muito bem.",fr:"J'adore le samba ! Mais je ne sais pas très bien danser.",correct:true},
          {pt:"Não gosto de música.",fr:"Je n'aime pas la musique.",correct:false},
          {pt:"Tenho que ir.",fr:"Je dois y aller.",correct:false},
        ]},
        {role:"bot",msg:"Vou te ensinar! Dançar samba é fácil!",tr:"Je vais t'apprendre ! Danser le samba c'est facile !"},
      ]
    },
  ],
  pronunciation:[
    {phrase:"Tenho muita saudade do Brasil.",tr:"J'ai beaucoup de saudade du Brésil.",ph:"[TE-nyo MOOY-ta saw-DA-ji do bra-ZIL]",tips:"'Saudade' est unique au portugais. 'Tenho' : le 'nh' est nasal."},
    {phrase:"Vamos dançar até de manhã!",tr:"On danse jusqu'au matin !",ph:"[VA-mos dãn-SAR a-TE ji ma-NYÃ]",tips:"'Dançar' : le 'ç' = 'ss'. 'Manhã' : son nasal final."},
    {phrase:"O carnaval do Rio é incrível!",tr:"Le carnaval de Rio est incroyable !",ph:"[o kar-na-VAL do HIO e in-KRI-vel]",tips:"'Rio' : le 'R' brésilien ressemble à 'H'. 'Incrível' : accent sur KRI."},
  ],
},{
  id:4, name:"Santé & shopping", emoji:"💊", color:"c4",
  desc:"Corps humain, médecin, magasins, vêtements",
  vocab:[
    {fr:"Médecin",pt:"Médico",ph:"[ME-ji-ko]",ex:"Preciso ver um médico.",em:"👨‍⚕️"},
    {fr:"Hôpital",pt:"Hospital",ph:"[os-pi-TAL]",ex:"Onde fica o hospital mais próximo?",em:"🏥"},
    {fr:"J'ai mal à…",pt:"Estou com dor de…",ph:"[esh-TOW kõ DOR ji]",ex:"Estou com dor de cabeça. (J'ai mal à la tête.)",em:"🤕"},
    {fr:"Tête",pt:"Cabeça",ph:"[ka-BE-sa]",ex:"Minha cabeça está doendo.",em:"🧠"},
    {fr:"Ventre / Estomac",pt:"Estômago / Barriga",ph:"[esh-TO-ma-go]",ex:"Estou com dor de barriga.",em:"🤢"},
    {fr:"Fièvre",pt:"Febre",ph:"[FE-bri]",ex:"Estou com febre alta.",em:"🌡️"},
    {fr:"Médicament",pt:"Remédio",ph:"[he-ME-jyo]",ex:"Preciso de um remédio.",em:"💊"},
    {fr:"Magasin",pt:"Loja",ph:"[LO-ja]",ex:"Essa loja tem bons preços.",em:"🏪"},
    {fr:"Cher / Chère",pt:"Caro/a",ph:"[KA-ro]",ex:"Isso está muito caro!",em:"💸"},
    {fr:"Pas cher",pt:"Barato/a",ph:"[ba-RA-to]",ex:"Que barato! — Pas cher du tout !",em:"💰"},
    {fr:"Taille / Pointure",pt:"Tamanho / Número",ph:"[ta-MA-nyo]",ex:"Qual é o seu tamanho?",em:"📏"},
    {fr:"Essayer",pt:"Experimentar / Provar",ph:"[es-pe-ri-mẽn-TAR]",ex:"Posso experimentar esse vestido?",em:"👗"},
    {fr:"Couleur",pt:"Cor",ph:"[KOR]",ex:"Tem em outra cor?",em:"🎨"},
    {fr:"Payer",pt:"Pagar",ph:"[pa-GAR]",ex:"Onde pago?",em:"💳"},
    {fr:"Caisse",pt:"Caixa",ph:"[KAY-sha]",ex:"A caixa fica no fundo.",em:"🏧"},
  ],
  grammar:[
    {
      title:"Passé récent — acabar de + infinitif",emoji:"⏮️",
      rule:`<b>Acabei de…</b> = Je viens de…<br><b>Você acabou de…</b> = Tu viens de…<br><br>Exprime une action qui vient de se terminer, équivalent du "venir de" français.`,
      ex:`Acabei de comer. (Je viens de manger.)<br>Ela acabou de chegar. (Elle vient d'arriver.)<br>Acabamos de ver o médico. (Nous venons de voir le médecin.)`
    },
    {
      title:"Comparatifs : plus / moins / aussi",emoji:"⚖️",
      rule:`<b>mais … do que</b> = plus … que<br><b>menos … do que</b> = moins … que<br><b>tão … quanto</b> = aussi … que<br><br>Supérlatif : <b>o/a mais</b> = le/la plus`,
      ex:`Isso é mais caro do que aquilo. (C'est plus cher que ça.)<br>Ela é menos alta do que eu. (Elle est moins grande que moi.)<br>O Rio é o mais bonito! (Rio est le plus beau !)`
    },
  ],
  conversations:[
    {
      title:"Chez le médecin",scene:"🏥 Consultation médicale",
      steps:[
        {role:"bot",msg:"Bom dia! O que está sentindo?",tr:"Bonjour ! Qu'est-ce que vous ressentez ?"},
        {role:"choice",opts:[
          {pt:"Estou com muita dor de cabeça e febre.",fr:"J'ai très mal à la tête et de la fièvre.",correct:true},
          {pt:"Estou com fome.",fr:"J'ai faim.",correct:false},
          {pt:"Quero comprar remédio.",fr:"Je veux acheter des médicaments.",correct:false},
        ]},
        {role:"bot",msg:"Há quanto tempo está assim?",tr:"Depuis combien de temps vous êtes comme ça ?"},
        {role:"choice",opts:[
          {pt:"Desde ontem à noite. É muito forte.",fr:"Depuis hier soir. C'est très fort.",correct:true},
          {pt:"Não sei.",fr:"Je ne sais pas.",correct:false},
          {pt:"Estou bem, obrigado.",fr:"Je vais bien, merci.",correct:false},
        ]},
        {role:"bot",msg:"Vou te receitar um remédio. Tome de 8 em 8 horas.",tr:"Je vais vous prescrire un médicament. Prenez-le toutes les 8 heures."},
      ]
    },
  ],
  pronunciation:[
    {phrase:"Estou com dor de cabeça.",tr:"J'ai mal à la tête.",ph:"[esh-TOW kõ DOR ji ka-BE-sa]",tips:"'Estou' : le 'ou' final = son fermé. 'Cabeça' : le 'ç' = 'ss'."},
    {phrase:"Isso é mais barato do que aquele.",tr:"C'est moins cher que celui-là.",ph:"[I-so E mayss ba-RA-to do ki a-KE-li]",tips:"'Aquele' = celui-là. Le 'e' final en 'i'."},
    {phrase:"Posso experimentar esse vestido?",tr:"Je peux essayer cette robe ?",ph:"[PO-so esh-pe-ri-mẽn-TAR E-si vesh-TI-do]",tips:"'Experimentar' : long mais régulier. 'Vestido' = vêtement/robe."},
  ],
},{
  id:5, name:"Maîtrise avancée", emoji:"🏆", color:"c5",
  desc:"Subjonctif, expressions idiomatiques, argot brésilien",
  vocab:[
    {fr:"Ça c'est cool ! (argot)",pt:"Que maneiro! / Legal!",ph:"[ki ma-NEY-ro / le-GAL]",ex:"Que maneiro esse lugar! — Cet endroit est trop cool !",em:"😎"},
    {fr:"Mec / Pote (argot)",pt:"Cara / Mano",ph:"[KA-ra / MA-no]",ex:"E aí, cara? — Quoi de neuf, mec ?",em:"🤙"},
    {fr:"C'est vrai ? (argot)",pt:"Sério? / É mesmo?",ph:"[SE-ryo / E MEZ-mo]",ex:"Você ganhou na loteria? Sério?!",em:"😱"},
    {fr:"Pas de souci",pt:"Tranquilo / Sem problema",ph:"[trãn-KI-lo]",ex:"Pode me ajudar? — Tranquilo! — Tu peux m'aider ? — Pas de souci !",em:"😌"},
    {fr:"Travailler dur",pt:"Dar o sangue",ph:"[DAR o SÃN-gi]",ex:"Dei o sangue nesse projeto. — J'ai tout donné pour ce projet.",em:"💪"},
    {fr:"Avoir de la chance",pt:"Ter sorte",ph:"[TER SOR-chi]",ex:"Você tem muita sorte! — Tu as beaucoup de chance !",em:"🍀"},
    {fr:"N'en plus pouvoir",pt:"Estar de saco cheio",ph:"[de SA-ko SHEY-o]",ex:"Estou de saco cheio do trabalho. (Expression familière)",em:"😤"},
    {fr:"Tomber amoureux",pt:"Se apaixonar",ph:"[si a-pay-sho-NAR]",ex:"Me apaixonei pelo Brasil!",em:"😍"},
    {fr:"Se débrouiller",pt:"Se virar",ph:"[si vi-RAR]",ex:"Não se preocupe, vou me virar.",em:"🤸"},
    {fr:"Valoir la peine",pt:"Valer a pena",ph:"[va-LER a PE-na]",ex:"Vale muito a pena aprender português!",em:"✨"},
    {fr:"Parler sans s'arrêter",pt:"Falar pelos cotovelos",ph:"[fa-LAR PE-los ko-to-VE-los]",ex:"Ela fala pelos cotovelos! — Elle parle sans s'arrêter !",em:"🗣️"},
    {fr:"Être dans la lune",pt:"Estar no mundo da lua",ph:"[no MUN-do da LU-a]",ex:"Você está no mundo da lua hoje!",em:"🌙"},
    {fr:"Coûter les yeux de la tête",pt:"Custar os olhos da cara",ph:"[KUSH-tar os O-lyos da KA-ra]",ex:"Esse celular custa os olhos da cara!",em:"💰"},
    {fr:"Être stressé(e)",pt:"Estar estressado/a",ph:"[esh-tre-SA-do]",ex:"Estou muito estressado com o trabalho.",em:"😰"},
    {fr:"Avoir le cafard",pt:"Estar na fossa",ph:"[esh-TAR na FO-sa]",ex:"Estou na fossa hoje. — J'ai le cafard aujourd'hui.",em:"😔"},
  ],
  grammar:[
    {
      title:"Subjonctif présent — cas courants",emoji:"🌀",
      rule:`Le subjonctif brésilien (presente do subjuntivo) s'utilise :<br>→ <b>Quero que você venha.</b> (Je veux que tu viennes.)<br>→ <b>Espero que esteja bem.</b> (J'espère que ça va.)<br>→ <b>Tomara que chova!</b> (Pourvu qu'il pleuve !)<br><br>Formation : base du présent + terminaison opposée (-AR → -e, -ER/-IR → -a)`,
      ex:`Espero que você fique bem. (J'espère que tu vas bien.)<br>É importante que você estude. (Il est important que tu étudies.)`
    },
    {
      title:"Voix passive et se passivo",emoji:"🔄",
      rule:`<b>Se passivo</b> : utilisé quand le sujet est indéfini :<br>→ <b>Fala-se português aqui.</b> (On parle portugais ici.)<br>→ <b>Vende-se apartamento.</b> (À vendre : appartement.)<br><br>Voix passive complète :<br>→ <b>O bolo foi comido.</b> (Le gâteau a été mangé.)<br>→ <b>A porta foi aberta.</b> (La porte a été ouverte.)`,
      ex:`Aluga-se quarto. (Chambre à louer.)<br>O jogo foi cancelado. (Le match a été annulé.)`
    },
    {
      title:"Discours indirect & connecteurs",emoji:"🔗",
      rule:`<b>Discours indirect :</b><br>→ Ele disse <b>que</b> estava cansado. (Il a dit qu'il était fatigué.)<br><br><b>Connecteurs essentiels :</b><br><b>portanto</b> = donc / par conséquent<br><b>porém / mas</b> = mais / cependant<br><b>além disso</b> = de plus / en outre<br><b>por isso</b> = c'est pourquoi`,
      ex:`Estou cansado, portanto vou dormir. (Je suis fatigué, donc je vais dormir.)<br>Gosto de viajar, mas não tenho dinheiro. (J'aime voyager, mais je n'ai pas d'argent.)`
    },
  ],
  conversations:[
    {
      title:"Soirée entre amis",scene:"🍹 Entre copains brésiliens",
      steps:[
        {role:"bot",msg:"E aí, cara! Tudo bem? Faz tempo que não te vejo!",tr:"Quoi de neuf, mec ! Tout va bien ? Ça fait longtemps que je t'ai pas vu !"},
        {role:"choice",opts:[
          {pt:"Cara, que saudade! Tudo ótimo, e você?",fr:"Oh, que la nostalgie ! Tout super, et toi ?",correct:true},
          {pt:"Bom dia.",fr:"Bonjour.",correct:false},
          {pt:"Não entendo.",fr:"Je ne comprends pas.",correct:false},
        ]},
        {role:"bot",msg:"Tranquilo! Vamos pedir uma rodada de caipirinha?",tr:"Tranquille ! On commande une tournée de caïpirinha ?"},
        {role:"choice",opts:[
          {pt:"Com certeza! Você sabe que adoro caipirinha!",fr:"Absolument ! Tu sais que j'adore la caïpirinha !",correct:true},
          {pt:"Não gosto de bebida.",fr:"Je n'aime pas les boissons.",correct:false},
          {pt:"Estou com fome.",fr:"J'ai faim.",correct:false},
        ]},
        {role:"bot",msg:"Haha! Que bom! Então, me conta, o que você tem feito?",tr:"Haha ! Super ! Allez, raconte-moi, qu'est-ce que tu as fait ?"},
        {role:"choice",opts:[
          {pt:"Cara, dei o sangue no trabalho esse mês. Estou exausto!",fr:"Mec, j'ai tout donné au boulot ce mois-ci. Je suis épuisé !",correct:true},
          {pt:"Nada. Estou bem.",fr:"Rien. Je vais bien.",correct:false},
          {pt:"Preciso ir.",fr:"Je dois y aller.",correct:false},
        ]},
        {role:"bot",msg:"Nossa! Você precisa relaxar. Vale a pena descansar!",tr:"Waouh ! Tu as besoin de te détendre. Ça vaut la peine de se reposer !"},
      ]
    },
  ],
  pronunciation:[
    {phrase:"Que maneiro esse lugar, cara!",tr:"Cet endroit est trop cool, mec !",ph:"[ki ma-NEY-ro E-si lu-GAR KA-ra]",tips:"'Maneiro' est de l'argot brésilien. 'Cara' = mec, copain."},
    {phrase:"Vale muito a pena aprender português!",tr:"Ça vaut vraiment la peine d'apprendre le portugais !",ph:"[VA-li MOOY-to a PE-na a-prẽn-DER por-tu-GESH]",tips:"'Vale' = vaut. 'Pena' ici = la peine. 'Português' : accent sur GESH."},
    {phrase:"Espero que você esteja bem.",tr:"J'espère que tu vas bien.",ph:"[esh-PE-ro ki vo-SE esh-TE-ja bẽ]",tips:"'Esteja' = subjonctif d'ESTAR. Son 'esh-TE-ja'."},
  ],
},
];

/* ═══════════════════════════════════════════════════════
   BADGES
═══════════════════════════════════════════════════════ */
const BADGES = [
  {id:"first_word",name:"Premier mot",emoji:"🌱",desc:"1 mot appris",req:"1 mot",check:s=>s.words>=1},
  {id:"w10",name:"Vocabulaire",emoji:"📚",desc:"10 mots appris",req:"10 mots",check:s=>s.words>=10},
  {id:"w50",name:"Polyglotte",emoji:"🗣️",desc:"50 mots appris",req:"50 mots",check:s=>s.words>=50},
  {id:"xp100",name:"100 XP",emoji:"⭐",desc:"100 XP gagnés",req:"100 XP",check:s=>s.xp>=100},
  {id:"xp500",name:"500 XP",emoji:"💫",desc:"500 XP gagnés",req:"500 XP",check:s=>s.xp>=500},
  {id:"xp1000",name:"Maître",emoji:"🏆",desc:"1000 XP gagnés",req:"1000 XP",check:s=>s.xp>=1000},
  {id:"first_test",name:"Testeur",emoji:"📝",desc:"1er test passé",req:"1 test",check:s=>s.tests>=1},
  {id:"perfect",name:"Parfait",emoji:"💎",desc:"Test 60/60",req:"60/60",check:s=>s.perfect>=1},
  {id:"streak3",name:"Régulier",emoji:"🔥",desc:"3 jours suite",req:"3 jours",check:s=>s.streak>=3},
  {id:"streak7",name:"Assidu",emoji:"🌟",desc:"7 jours suite",req:"7 jours",check:s=>s.streak>=7},
  {id:"ch1",name:"Chapitre 1",emoji:"🌿",desc:"Chap. 1 terminé",req:"Ch.1",check:s=>s.chDone&&s.chDone[0]},
  {id:"ch3",name:"Niveau 3",emoji:"🌳",desc:"3 chapitres finis",req:"3 ch.",check:s=>s.chDone&&Object.values(s.chDone).filter(Boolean).length>=3},
  {id:"ch6",name:"Expert",emoji:"🦅",desc:"Tous chapitres !",req:"6 ch.",check:s=>s.chDone&&Object.values(s.chDone).filter(Boolean).length>=6},
  {id:"conv1",name:"Conversant",emoji:"💬",desc:"1re conversation",req:"1 conv",check:s=>s.conv>=1},
  {id:"pronun5",name:"Phonéticien",emoji:"🎤",desc:"5 prononciations",req:"5 pron.",check:s=>s.pronun>=5},
];

/* ═══════════════════════════════════════════════════════
   STATE MANAGEMENT
═══════════════════════════════════════════════════════ */
let S = {
  level:'debutant', xp:0, streak:0,
  words:0, tests:0, perfect:0, conv:0, pronun:0,
  knownWords:{}, gramRead:{}, testScores:{},
  chDone:{}, chProgress:{},
  lastSession:null, sessionDays:{},
  badges:[],
};

function save(){ try{ localStorage.setItem('fb_v3',JSON.stringify(S)); }catch(e){} }
function load(){ try{ const d=localStorage.getItem('fb_v3'); if(d) S=Object.assign(S,JSON.parse(d)); }catch(e){} }

function addXP(pts, x, y){
  S.xp += pts;
  if(x && y){
    const el = document.createElement('div');
    el.className = 'xp-popup';
    el.textContent = `+${pts} XP`;
    el.style.cssText = `left:${x-20}px;top:${y-10}px;`;
    document.body.appendChild(el);
    setTimeout(()=>el.remove(),1200);
  }
  checkBadges();
  save();
}

function checkBadges(){
  let newBadge = false;
  BADGES.forEach(b=>{
    if(!S.badges.includes(b.id) && b.check(S)){
      S.badges.push(b.id);
      newBadge = true;
      setTimeout(()=>toast(`🏅 Badge débloqué : ${b.emoji} ${b.name} !`), 400);
    }
  });
  if(newBadge) save();
}

/* ═══════════════════════════════════════════════════════
   NAVIGATION
═══════════════════════════════════════════════════════ */
let currentScreen = 'splash';
let currentChapter = 0;
let navStack = [];

function navigate(to, back=false){
  const from = document.querySelector('.screen.active');
  const toEl = document.getElementById(to);
  if(!toEl) return;
  if(from) from.classList.remove('active');
  toEl.classList.remove('slide-in','slide-out','slide-back-in');
  void toEl.offsetWidth;
  toEl.classList.add(back?'slide-back-in':'slide-in');
  toEl.classList.add('active');
  currentScreen = to;
  initScreen(to);
}

function initScreen(id){
  if(id==='home') renderHome();
  if(id==='stats-screen') renderStats();
}

function navTo(id, btn, sub){
  document.querySelectorAll('.nb').forEach(b=>b.classList.remove('on'));
  btn.classList.add('on');
  navigate(id);
}

function navToConv(btn){
  document.querySelectorAll('.nb').forEach(b=>b.classList.remove('on'));
  btn.classList.add('on');
  const ch = CHAPTERS[currentChapter];
  document.getElementById('conv-chapter-name').textContent = ch.name;
  renderConvList(ch);
  navigate('conv-screen');
}

function navToPronun(btn){
  document.querySelectorAll('.nb').forEach(b=>b.classList.remove('on'));
  btn.classList.add('on');
  const ch = CHAPTERS[currentChapter];
  document.getElementById('pronun-chapter-name').textContent = ch.name;
  renderPronun(ch);
  navigate('pronun-screen');
}

/* ═══════════════════════════════════════════════════════
   TIMER (1 hour session)
═══════════════════════════════════════════════════════ */
let timerInterval = null;
let timerSeconds = 3600;

function startTimer(){
  timerSeconds = 3600;
  document.getElementById('timer-bar').classList.add('visible');
  clearInterval(timerInterval);
  timerInterval = setInterval(()=>{
    timerSeconds--;
    const m = Math.floor(timerSeconds/60);
    const s = timerSeconds%60;
    document.getElementById('timer-text').textContent = `${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
    const pct = (timerSeconds/3600)*100;
    const fill = document.getElementById('timer-fill');
    fill.style.width = pct+'%';
    if(timerSeconds <= 300) fill.classList.add('warning');
    if(timerSeconds <= 0){
      clearInterval(timerInterval);
      toast('⏰ Heure de session terminée ! Super travail !');
    }
  },1000);
}

function stopTimer(){
  clearInterval(timerInterval);
  document.getElementById('timer-bar').classList.remove('visible');
}

/* ═══════════════════════════════════════════════════════
   TOAST
═══════════════════════════════════════════════════════ */
let toastTimer = null;
function toast(msg){
  const el = document.getElementById('toast');
  el.textContent = msg;
  el.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(()=>el.classList.remove('show'),2800);
}

/* ═══════════════════════════════════════════════════════
   CONFETTI
═══════════════════════════════════════════════════════ */
function launchConfetti(){
  const canvas = document.getElementById('confetti-canvas');
  canvas.style.display = 'block';
  const ctx = canvas.getContext('2d');
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  const particles = Array.from({length:80},()=>({
    x:Math.random()*canvas.width,y:-20,
    vx:(Math.random()-0.5)*4,vy:Math.random()*4+2,
    color:['#009c3b','#FFDF00','#002776','#ff6b6b','#48dbfb'][Math.floor(Math.random()*5)],
    size:Math.random()*8+4,rot:Math.random()*360,
    vrot:(Math.random()-0.5)*8,
  }));
  let frame=0;
  function draw(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    particles.forEach(p=>{
      ctx.save();
      ctx.translate(p.x,p.y);
      ctx.rotate(p.rot*Math.PI/180);
      ctx.fillStyle=p.color;
      ctx.fillRect(-p.size/2,-p.size/2,p.size,p.size/2);
      ctx.restore();
      p.x+=p.vx;p.y+=p.vy;p.rot+=p.vrot;p.vy+=0.05;
    });
    frame++;
    if(frame<120) requestAnimationFrame(draw);
    else{ ctx.clearRect(0,0,canvas.width,canvas.height); canvas.style.display='none'; }
  }
  draw();
}

/* ═══════════════════════════════════════════════════════
   SPLASH & START
═══════════════════════════════════════════════════════ */
function startApp(level){
  load();
  if(!S.level||S.level!==level) S.level = level;
  save();
  document.getElementById('bottom-nav').classList.add('visible');
  navigate('home');
  updateGreeting();
}

function updateGreeting(){
  const h = new Date().getHours();
  const g = h<12?'Bonjour':h<18?'Bon après-midi':'Bonsoir';
  const el = document.getElementById('home-greeting');
  if(el) el.textContent = g+' 👋';
}

/* ═══════════════════════════════════════════════════════
   HOME
═══════════════════════════════════════════════════════ */
const LEVEL_NAMES = {debutant:'🌱 Débutant',novice:'🌿 Novice',moyen:'🌳 Moyen',fort:'🦅 Fort',avance:'🏆 Avancé'};
const XP_LEVELS = [0,100,300,600,1000,1500,2200,3000];

function renderHome(){
  updateGreeting();
  document.getElementById('home-level-badge').textContent = LEVEL_NAMES[S.level]||'🌱 Débutant';
  document.getElementById('home-xp').textContent = S.xp+' XP';
  // XP bar
  let lvl=0;
  while(lvl<XP_LEVELS.length-1 && S.xp>=XP_LEVELS[lvl+1]) lvl++;
  const cur=XP_LEVELS[lvl], next=XP_LEVELS[lvl+1]||XP_LEVELS[lvl]+500;
  const pct=Math.min(100,Math.round((S.xp-cur)/(next-cur)*100));
  document.getElementById('home-xp-fill').style.width=pct+'%';
  // Session
  const days={2:'Mardi',3:'Mercredi',4:'Jeudi',6:'Samedi'};
  const today=new Date().getDay();
  const sessText = document.getElementById('session-text');
  if(days[today]){
    sessText.innerHTML = `Session du jour disponible !<br><small style="color:var(--muted)">1 heure · ${days[today]}</small>`;
  } else {
    sessText.innerHTML = `Pas de session aujourd'hui 😊<br><small style="color:var(--muted)">Prochaine : Mardi</small>`;
    document.querySelector('.sb-btn').style.display='none';
  }
  // Chapters
  renderChapterList();
}

function renderChapterList(){
  const list = document.getElementById('chapter-list');
  list.innerHTML='';
  CHAPTERS.forEach((ch,i)=>{
    const prog = getChapterProgress(i);
    const isDone = S.chDone && S.chDone[i];
    const isActive = i<=getMaxUnlockedChapter();
    const div = document.createElement('div');
    div.className='chapter-card'+(isDone?' done':isActive?' active-ch':' locked');
    div.innerHTML=`
      <div class="ch-icon ${ch.color}">${ch.emoji}</div>
      <div style="flex:1;min-width:0">
        <div class="ch-name">Ch.${i+1} — ${ch.name}</div>
        <div class="ch-sub">${ch.desc}</div>
        <div class="ch-progress">
          <div class="ch-prog-track"><div class="ch-prog-fill" style="width:${prog}%"></div></div>
          <div class="ch-prog-pct">${prog}%</div>
        </div>
      </div>
      <div class="ch-status ${isDone?'done':isActive?'active':'locked'}">${isDone?'✅':isActive?'▶':'🔒'}</div>`;
    if(isActive) div.onclick=()=>openChapter(i);
    list.appendChild(div);
  });
}

function getMaxUnlockedChapter(){
  let max=0;
  CHAPTERS.forEach((ch,i)=>{
    if(S.chDone&&S.chDone[i]) max=i+1;
  });
  return Math.min(max, CHAPTERS.length-1);
}

function getChapterProgress(chIdx){
  const ch = CHAPTERS[chIdx];
  let done=0, total=0;
  ch.vocab.forEach((_,i)=>{ total++; if(S.knownWords&&S.knownWords[`${chIdx}_${i}`]) done++; });
  ch.grammar.forEach((_,i)=>{ total++; if(S.gramRead&&S.gramRead[`${chIdx}_${i}`]) done++; });
  ch.conversations.forEach((_,i)=>{ total++; if(S.conv>0) done+=0.5; });
  return total>0?Math.min(100,Math.round(done/total*100)):0;
}

function startSession(){
  startTimer();
  openChapter(currentChapter);
  toast('🚀 Session démarrée ! 1 heure de portugais !');
  // Mark session day
  const days={2:'Mar',3:'Mer',4:'Jeu',6:'Sam'};
  const today=new Date().getDay();
  if(days[today]){
    if(!S.sessionDays) S.sessionDays={};
    const key = new Date().toDateString();
    if(!S.sessionDays[key]){ S.sessionDays[key]=true; S.streak++; save(); }
  }
}

/* ═══════════════════════════════════════════════════════
   CHAPTER SCREEN
═══════════════════════════════════════════════════════ */
function openChapter(idx){
  currentChapter = idx;
  const ch = CHAPTERS[idx];
  document.getElementById('ch-screen-title').textContent = `${ch.emoji} Ch.${idx+1} — ${ch.name}`;
  document.getElementById('ch-screen-sub').textContent = ch.desc;
  renderModuleGrid(ch, idx);
  navigate('chapter-screen');
}

function renderModuleGrid(ch, idx){
  const grid = document.getElementById('module-grid');
  grid.innerHTML='';
  const prog = getChapterProgress(idx);
  const testScore = S.testScores&&S.testScores[idx];
  const testUnlocked = prog >= 70;

  const modules = [
    {id:'vocab',icon:'📚',name:'Vocabulaire',desc:`${ch.vocab.length} mots à apprendre`,xp:'+10 XP/mot',fn:()=>openVocab(ch,idx),done:false},
    {id:'gram',icon:'📐',name:'Grammaire',desc:`${ch.grammar.length} règles essentielles`,xp:'+15 XP/règle',fn:()=>openGrammar(ch,idx),done:false},
    {id:'conv',icon:'💬',name:'Conversations',desc:`${ch.conversations.length} dialogue(s) interactif(s)`,xp:'+20 XP/conv',fn:()=>openConvChapter(ch,idx),done:false},
    {id:'pronun',icon:'🎤',name:'Prononciation',desc:`${ch.pronunciation.length} phrases à pratiquer`,xp:'+5 XP/phrase',fn:()=>openPronunChapter(ch,idx),done:false},
    {id:'test',icon:'📝',name:'Test du chapitre',desc:testScore!=null?`Score obtenu : ${testScore}/60`:'Noté sur 60 pts — Débloqué à 70%',xp:testScore!=null?`${testScore}/60`:'Jusqu\'à +60 XP',fn:()=>openTest(idx),done:testScore!=null,locked:!testUnlocked},
  ];

  modules.forEach(m=>{
    const tile = document.createElement('div');
    tile.className = 'module-tile'+(m.done?' done-tile':m.locked?' locked-tile':'');
    if(m.id==='test') tile.style.gridColumn='span 2';
    tile.innerHTML=`
      <div class="mt-xp">${m.xp}</div>
      <div class="mt-icon">${m.icon}</div>
      <div class="mt-name">${m.name}</div>
      <div class="mt-desc">${m.desc}</div>
      ${m.done?'<div class="mt-check">✅</div>':''}
      ${m.locked?'<div class="mt-check">🔒</div>':''}`;
    if(!m.locked) tile.onclick=m.fn;
    grid.appendChild(tile);
  });
}

/* ═══════════════════════════════════════════════════════
   FLASHCARDS
═══════════════════════════════════════════════════════ */
let fc = { words:[], idx:0, flipped:false, chIdx:0 };
let touchStartX=0, touchStartY=0;

function openVocab(ch, chIdx){
  fc.words = ch.vocab;
  fc.idx = 0;
  fc.flipped = false;
  fc.chIdx = chIdx;
  document.getElementById('fc-chapter-name').textContent = `${ch.emoji} ${ch.name}`;
  loadFlashcard();
  navigate('flashcard-screen');

  // Touch/swipe
  const card = document.getElementById('card-3d');
  card.removeEventListener('touchstart',onTouchStart);
  card.removeEventListener('touchend',onTouchEnd);
  card.addEventListener('touchstart',onTouchStart,{passive:true});
  card.addEventListener('touchend',onTouchEnd,{passive:true});
}

function onTouchStart(e){ touchStartX=e.touches[0].clientX; touchStartY=e.touches[0].clientY; }
function onTouchEnd(e){
  const dx=e.changedTouches[0].clientX-touchStartX;
  const dy=Math.abs(e.changedTouches[0].clientY-touchStartY);
  if(dy>50||Math.abs(dx)<40) return;
  if(!fc.flipped){ flipCard(); return; }
  if(dx<-40) answerCard(false);
  else if(dx>40) answerCard(true);
}

function loadFlashcard(){
  const w = fc.words[fc.idx];
  fc.flipped = false;
  const card = document.getElementById('card-3d');
  card.classList.remove('flipped');

  document.getElementById('cf-emoji').textContent = w.em;
  document.getElementById('cf-emoji2').textContent = w.em;
  document.getElementById('cf-fr').textContent = w.fr;
  document.getElementById('cf-pt').textContent = w.pt;
  document.getElementById('cf-phonetic').textContent = w.ph;
  document.getElementById('cf-example').textContent = w.ex;

  const pct = (fc.idx/fc.words.length)*100;
  document.getElementById('fc-prog-fill').style.width=pct+'%';
  document.getElementById('fc-prog-label').textContent=`${fc.idx}/${fc.words.length}`;

  document.getElementById('answer-row').style.display='none';
  document.getElementById('swipe-hint').textContent='Touchez la carte pour la retourner';
}

function flipCard(){
  fc.flipped = true;
  document.getElementById('card-3d').classList.add('flipped');
  document.getElementById('answer-row').style.display='flex';
  document.getElementById('swipe-hint').textContent='← Pas sûr(e)  ·  Je sais ! →';
}

function answerCard(known, event){
  const key=`${fc.chIdx}_${fc.idx}`;
  if(known){
    if(!S.knownWords[key]){ S.knownWords[key]=true; S.words++; addXP(10); }
  } else {
    delete S.knownWords[key];
  }
  save();

  // Animate out
  const card = document.getElementById('card-3d');
  card.style.transition='transform .2s, opacity .2s';
  card.style.transform = known ? 'translateX(80px) rotate(8deg)' : 'translateX(-80px) rotate(-8deg)';
  card.style.opacity='0';

  setTimeout(()=>{
    card.style.transition='none';
    card.style.transform='';
    card.style.opacity='1';
    fc.idx++;
    if(fc.idx >= fc.words.length){
      allCardsFinished();
    } else {
      loadFlashcard();
      setTimeout(()=>{ card.style.transition=''; },50);
    }
  },200);
}

function allCardsFinished(){
  const knownCount = fc.words.filter((_,i)=>S.knownWords[`${fc.chIdx}_${i}`]).length;
  toast(`🎉 Vocabulaire terminé ! ${knownCount}/${fc.words.length} mots maîtrisés`);
  if(knownCount === fc.words.length) launchConfetti();
  setTimeout(()=>navigate('chapter-screen',true),800);
}

/* ═══════════════════════════════════════════════════════
   GRAMMAR
═══════════════════════════════════════════════════════ */
function openGrammar(ch, chIdx){
  document.getElementById('gram-chapter-name').textContent = `${ch.emoji} ${ch.name}`;
  renderGrammarContent(ch, chIdx);
  navigate('grammar-screen');
}

function renderGrammarContent(ch, chIdx){
  const content = document.getElementById('gram-content');
  content.innerHTML='';
  ch.grammar.forEach((g,i)=>{
    const done = S.gramRead&&S.gramRead[`${chIdx}_${i}`];
    const div = document.createElement('div');
    div.className='gram-lesson'+(done?' done-tile':'');
    div.innerHTML=`
      <div class="gram-header" onclick="toggleGram(this.parentElement,${chIdx},${i})">
        <span class="gram-h-icon">${g.emoji}</span>
        <div>
          <div class="gram-h-title">${g.title}</div>
          ${done?'<div style="font-size:.65rem;color:var(--g);font-weight:700;">✅ Lu</div>':''}
        </div>
        <span class="gram-h-arrow">▾</span>
      </div>
      <div class="gram-body">
        <div class="gram-inner">
          <div class="gram-rule-box">${g.rule}</div>
          <div class="gram-example-box">📌 ${g.ex}</div>
          <button class="gram-done-btn" onclick="markGramDone(${chIdx},${i},this)">
            ${done?'✅ Déjà lu !':'✅ Marquer comme lu (+15 XP)'}
          </button>
        </div>
      </div>`;
    content.appendChild(div);
  });
}

function toggleGram(card){
  const wasOpen = card.classList.contains('open');
  document.querySelectorAll('.gram-lesson').forEach(c=>c.classList.remove('open'));
  if(!wasOpen) card.classList.add('open');
}

function markGramDone(chIdx, gIdx, btn){
  const key=`${chIdx}_${gIdx}`;
  if(!S.gramRead) S.gramRead={};
  if(!S.gramRead[key]){
    S.gramRead[key]=true;
    addXP(15);
    toast('📐 Règle mémorisée ! +15 XP');
  }
  btn.textContent='✅ Déjà lu !';
  save();
}

/* ═══════════════════════════════════════════════════════
   CONVERSATIONS
═══════════════════════════════════════════════════════ */
let convState = { ch:null, sceneIdx:0, step:0, chIdx:0 };

function openConvChapter(ch, chIdx){
  convState.chIdx = chIdx;
  document.getElementById('conv-chapter-name').textContent = `${ch.emoji} ${ch.name}`;
  renderConvList(ch);
  navigate('conv-screen');
}

function renderConvList(ch){
  const list = document.getElementById('conv-scene-list');
  list.innerHTML='';
  ch.conversations.forEach((c,i)=>{
    const card = document.createElement('div');
    card.className='scene-card';
    card.innerHTML=`
      <span class="sc-icon">${c.scene.split(' ')[0]}</span>
      <div><div class="sc-title">${c.title}</div><div class="sc-desc">${c.scene}</div></div>
      <span class="sc-status">›</span>`;
    card.onclick=()=>startConv(ch, i);
    list.appendChild(card);
  });
}

function startConv(ch, sceneIdx){
  const scene = ch.conversations[sceneIdx];
  convState.ch = ch;
  convState.sceneIdx = sceneIdx;
  convState.step = 0;

  document.getElementById('conv-play-title').textContent = scene.title;
  document.getElementById('conv-play-sub').textContent = scene.scene;
  document.getElementById('chat-area').innerHTML='';
  document.getElementById('choice-area').innerHTML='';

  navigate('conv-play-screen');
  setTimeout(()=>runConvStep(scene),300);
}

function runConvStep(scene){
  if(convState.step >= scene.steps.length){
    convDone();
    return;
  }
  const step = scene.steps[convState.step];
  if(step.role==='bot'){
    addChatMsg('bot','🤖',step.msg,step.tr);
    convState.step++;
    setTimeout(()=>runConvStep(scene),700);
  } else {
    showChoices(step.opts, scene);
  }
}

function addChatMsg(role, avatar, msg, tr){
  const area = document.getElementById('chat-area');
  const div = document.createElement('div');
  div.className=`chat-msg ${role}`;
  div.innerHTML=`
    <div class="chat-av">${avatar}</div>
    <div>
      <div class="chat-bub">${msg}</div>
      ${tr?`<div class="chat-tr">${tr}</div>`:''}
    </div>`;
  area.appendChild(div);
  area.scrollTop=area.scrollHeight;
}

function showChoices(opts, scene){
  const area = document.getElementById('choice-area');
  area.innerHTML=`<div class="choice-label">Que répondre ?</div>`;
  opts.forEach(opt=>{
    const btn = document.createElement('button');
    btn.className='choice-btn';
    btn.innerHTML=`<div class="cb-pt">${opt.pt}</div><div class="cb-fr">${opt.fr}</div>`;
    btn.onclick=()=>{
      // Disable all
      area.querySelectorAll('.choice-btn').forEach(b=>b.classList.add('disabled'));
      btn.classList.add(opt.correct?'correct':'wrong');
      if(opt.correct){ addXP(5); addChatMsg('user','😊',opt.pt,opt.fr); }
      else toast('❌ Essaie une autre réponse !');
      if(opt.correct){
        convState.step++;
        setTimeout(()=>{ area.innerHTML=''; runConvStep(scene); },500);
      } else {
        setTimeout(()=>{ btn.classList.remove('wrong','disabled'); area.querySelectorAll('.choice-btn').forEach(b=>b.classList.remove('disabled')); }, 800);
      }
    };
    area.appendChild(btn);
  });
}

function convDone(){
  S.conv++;
  addXP(20);
  save();
  document.getElementById('choice-area').innerHTML=`
    <button class="btn btn-green btn-full" style="margin:.5rem 0" onclick="navigate('conv-screen',true)">
      🎉 Conversation terminée ! Retour →
    </button>`;
  toast('💬 Conversation réussie ! +20 XP');
}

/* ═══════════════════════════════════════════════════════
   PRONUNCIATION
═══════════════════════════════════════════════════════ */
function openPronunChapter(ch, chIdx){
  document.getElementById('pronun-chapter-name').textContent = `${ch.emoji} ${ch.name}`;
  renderPronun(ch);
  navigate('pronun-screen');
}

function renderPronun(ch){
  const list = document.getElementById('pronun-list');
  list.innerHTML='';
  ch.pronunciation.forEach((p,i)=>{
    const card = document.createElement('div');
    card.className='pronun-card';
    card.innerHTML=`
      <div class="pc-phrase">${p.phrase}</div>
      <div class="pc-translation">${p.tr}</div>
      <div class="pc-phonetic">🔊 ${p.ph}</div>
      <div style="font-size:.76rem;color:var(--muted);margin-bottom:.7rem;line-height:1.5">💡 ${p.tips}</div>
      <div class="pc-controls">
        <button class="pc-btn pc-listen" onclick="listenPhrase('${p.phrase.replace(/'/g,"\\'")}',this)">🔊 Écouter</button>
        <button class="pc-btn pc-speak" onclick="speakMode(this,'${p.phrase.replace(/'/g,"\\'")}',${i})">🎤 Prononcer</button>
      </div>
      <div class="pc-result" id="pcr-${i}"></div>`;
    list.appendChild(card);
  });
}

function listenPhrase(text, btn){
  if('speechSynthesis' in window){
    const u = new SpeechSynthesisUtterance(text);
    u.lang='pt-BR'; u.rate=0.85;
    // Find Brazilian voice if available
    const voices = speechSynthesis.getVoices();
    const brVoice = voices.find(v=>v.lang==='pt-BR')||voices.find(v=>v.lang.startsWith('pt'));
    if(brVoice) u.voice=brVoice;
    speechSynthesis.speak(u);
    btn.textContent='🔊 En cours…';
    u.onend=()=>{ btn.textContent='🔊 Écouter'; };
  } else {
    toast('🔊 Synthèse vocale non disponible sur ce navigateur.');
  }
}

function speakMode(btn, expectedText, cardIdx){
  if(!('webkitSpeechRecognition' in window||'SpeechRecognition' in window)){
    // Simulate for demonstration
    btn.classList.add('recording');
    btn.textContent='🎤 Enregistrement…';
    setTimeout(()=>{
      btn.classList.remove('recording');
      btn.textContent='🎤 Prononcer';
      const results=['good','ok','retry'];
      const r=results[Math.floor(Math.random()*2)];
      showPronunResult(cardIdx, r, expectedText);
      S.pronun++;
      addXP(5);
      save();
    },2000);
    return;
  }
  const SR=window.SpeechRecognition||window.webkitSpeechRecognition;
  const rec=new SR();
  rec.lang='pt-BR'; rec.continuous=false; rec.interimResults=false;
  btn.classList.add('recording'); btn.textContent='🎤 Parle maintenant…';
  rec.start();
  rec.onresult=(e)=>{
    const said=e.results[0][0].transcript.toLowerCase().trim();
    const exp=expectedText.toLowerCase().trim();
    const conf=e.results[0][0].confidence;
    let res='retry';
    if(said===exp||conf>0.85) res='good';
    else if(conf>0.6||levenshtein(said,exp)<4) res='ok';
    showPronunResult(cardIdx, res, expectedText);
    S.pronun++;
    addXP(5); save();
  };
  rec.onerror=()=>{
    toast('🎤 Impossible d\'accéder au micro. Essaie dans Safari.');
  };
  rec.onend=()=>{ btn.classList.remove('recording'); btn.textContent='🎤 Prononcer'; };
}

function showPronunResult(idx, result, phrase){
  const el=document.getElementById(`pcr-${idx}`);
  el.classList.add('show');
  if(result==='good'){ el.className='pc-result show good'; el.textContent='🏆 Excellent ! Prononciation parfaite !'; toast('🎤 Parfait ! +5 XP'); }
  else if(result==='ok'){ el.className='pc-result show ok'; el.textContent='👍 Bien ! Quelques petites améliorations possibles.'; toast('🎤 Bien ! +5 XP'); }
  else { el.className='pc-result show retry'; el.textContent='🔄 Réessaie en articulant mieux. Écoute d\'abord.'; }
}

function levenshtein(a,b){
  const m=[];
  for(let i=0;i<=b.length;i++) m[i]=[i];
  for(let j=0;j<=a.length;j++) m[0][j]=j;
  for(let i=1;i<=b.length;i++) for(let j=1;j<=a.length;j++)
    m[i][j]=b[i-1]===a[j-1]?m[i-1][j-1]:Math.min(m[i-1][j-1]+1,m[i][j-1]+1,m[i-1][j]+1);
  return m[b.length][a.length];
}

/* ═══════════════════════════════════════════════════════
   TEST / QUIZ
═══════════════════════════════════════════════════════ */
let quiz = { questions:[], idx:0, correct:0, wrong:0, pts:0, answered:false, chIdx:0 };

function openTest(chIdx){
  quiz.chIdx = chIdx;
  const ch = CHAPTERS[chIdx];
  document.getElementById('quiz-screen-title').textContent = `📝 Test — ${ch.name}`;
  document.getElementById('quiz-screen-sub').textContent = `Chapitre ${chIdx+1} · Noté sur 60 pts`;
  buildTest(ch, chIdx);
  navigate('quiz-screen');
}

function buildTest(ch, chIdx){
  const allWords = ch.vocab;
  const questions = [];

  // 10 questions vocab FR→PT (3 pts chacune = 30 pts)
  const vocabSample = shuffle(allWords).slice(0,10);
  vocabSample.forEach(w=>{
    const wrong = shuffle(allWords.filter(x=>x.pt!==w.pt)).slice(0,3);
    questions.push({
      type:'FR → PT',typeLabel:'VOCABULAIRE',
      q:w.fr, sub:'Traduis en portugais',
      correct:w.pt, pts:3,
      opts:shuffle([w.pt,...wrong.map(x=>x.pt)])
    });
  });

  // 5 questions PT→FR (3 pts = 15 pts)
  const ptSample = shuffle(allWords).slice(0,5);
  ptSample.forEach(w=>{
    const wrong = shuffle(allWords.filter(x=>x.fr!==w.fr)).slice(0,3);
    questions.push({
      type:'PT → FR',typeLabel:'COMPRÉHENSION',
      q:w.pt, sub:'Traduis en français',
      correct:w.fr, pts:3,
      opts:shuffle([w.fr,...wrong.map(x=>x.fr)])
    });
  });

  // 5 questions grammaire (3 pts = 15 pts)
  ch.grammar.forEach((g,i)=>{
    if(i>=5) return;
    const gramQ = buildGramQuestion(g, i, ch);
    if(gramQ) questions.push({...gramQ, pts:3});
  });

  quiz.questions = shuffle(questions).slice(0,20); // Max 20 questions, chacune 3pts = 60 max
  quiz.idx=0; quiz.correct=0; quiz.wrong=0; quiz.pts=0; quiz.answered=false;

  document.getElementById('test-result').classList.remove('show');
  document.getElementById('quiz-q-card').style.display='';
  document.getElementById('quiz-opts').style.display='';
  document.getElementById('quiz-feedback').style.display='none';

  updateQuizScorebar();
  loadQuizQuestion();
}

function buildGramQuestion(g, idx, ch){
  // Extract examples and create fill-in questions
  const examples = g.ex.split('<br>');
  if(!examples.length) return null;
  const ex = examples[0].split('(')[0].trim();
  const words = ex.split(' ').filter(w=>w.length>3);
  if(!words.length) return null;

  // Simple: which translation fits?
  return {
    type:'GRAMMAIRE',typeLabel:'GRAMMAIRE',
    q:`${g.emoji} ${g.title}`,
    sub:'Quelle phrase est grammaticalement correcte ?',
    correct:ex,
    opts:shuffle([ex, ex.replace(/não/g,'sim'), ex.replace(/é/g,'está')||ex+'?', ex.split(' ').reverse().join(' ')]).slice(0,4).map((o,i)=>i===0?ex:o),
  };
}

function loadQuizQuestion(){
  if(quiz.idx>=quiz.questions.length){ showTestResult(); return; }
  quiz.answered=false;
  const q=quiz.questions[quiz.idx];

  document.getElementById('qq-type').textContent=q.typeLabel||q.type;
  document.getElementById('qq-question').textContent=q.q;
  document.getElementById('qq-sub').textContent=q.sub;
  document.getElementById('qq-points').textContent=`Valeur : ${q.pts} point(s)`;
  document.getElementById('quiz-feedback').classList.remove('show','ok','ko');
  document.getElementById('quiz-feedback').style.display='';

  const pct=(quiz.idx/quiz.questions.length)*100;
  document.getElementById('quiz-prog-fill').style.width=pct+'%';

  const opts = document.getElementById('quiz-opts');
  opts.innerHTML='';
  const letters=['A','B','C','D'];
  (q.opts||[]).slice(0,4).forEach((o,i)=>{
    const btn=document.createElement('button');
    btn.className='qo';
    btn.innerHTML=`<span class="qo-letter">${letters[i]}</span>${o}`;
    btn.onclick=()=>checkAnswer(o,q,btn);
    opts.appendChild(btn);
  });
}

function checkAnswer(chosen, q, btn){
  if(quiz.answered) return;
  quiz.answered=true;
  const ok=chosen===q.correct;
  document.querySelectorAll('.qo').forEach(b=>{
    b.classList.add('disabled');
    if(b.textContent.slice(1)===q.correct) b.classList.add('correct');
    else if(b===btn&&!ok) b.classList.add('wrong');
  });
  const fb=document.getElementById('quiz-feedback');
  if(ok){
    quiz.correct++; quiz.pts+=q.pts;
    fb.className='quiz-feedback show ok';
    fb.textContent=`✅ Correct ! +${q.pts} pts`;
    addXP(q.pts);
  } else {
    quiz.wrong++;
    fb.className='quiz-feedback show ko';
    fb.textContent=`❌ Réponse : ${q.correct}`;
  }
  fb.style.display='block';
  updateQuizScorebar();
  quiz.idx++;
  setTimeout(()=>{ fb.classList.remove('show'); fb.style.display='none'; loadQuizQuestion(); },1400);
}

function updateQuizScorebar(){
  document.getElementById('qs-ok').textContent=quiz.correct;
  document.getElementById('qs-ko').textContent=quiz.wrong;
  document.getElementById('qs-left').textContent=Math.max(0,quiz.questions.length-quiz.idx);
  document.getElementById('quiz-pts-display').textContent=quiz.pts+' pts';
}

function showTestResult(){
  document.getElementById('quiz-q-card').style.display='none';
  document.getElementById('quiz-opts').style.display='none';
  document.getElementById('quiz-feedback').style.display='none';
  document.getElementById('quiz-prog-fill').style.width='100%';

  // Scale to 60
  const maxPossible = quiz.questions.reduce((a,q)=>a+q.pts,0)||60;
  const score60 = Math.min(60, Math.round(quiz.pts/maxPossible*60));
  const pct = score60/60;

  let grade,emoji,title,msg;
  if(pct>=0.95){grade='A+';emoji='🏆';title='Exceptionnel !';msg='Score parfait ! Tu maîtrises totalement ce chapitre. Continue avec le suivant !';}
  else if(pct>=0.83){grade='A';emoji='🌟';title='Excellent !';msg='Très belle maîtrise du chapitre. Quelques petits points à revoir.';}
  else if(pct>=0.70){grade='B';emoji='😊';title='Bien !';msg='Bon travail ! Revois les points que tu as manqués avant de continuer.';}
  else if(pct>=0.55){grade='C';emoji='💪';title='Passable';msg='Tu passes, mais il faut revoir ce chapitre. Les bases sont là !';}
  else {grade='D';emoji='📚';title='À revoir';msg='Revois le vocabulaire et la grammaire avant de repasser le test.';}

  document.getElementById('tr-score').textContent=score60;
  document.getElementById('tr-grade').textContent=emoji;
  document.getElementById('tr-title').textContent=`${title} — Note : ${grade}`;
  document.getElementById('tr-msg').textContent=msg;

  // Breakdown
  const bd=document.getElementById('tr-breakdown');
  bd.innerHTML=`
    <div style="font-size:.72rem;font-weight:900;letter-spacing:.08em;text-transform:uppercase;color:var(--muted);margin-bottom:.5rem;">Détail</div>
    <div class="trb-row"><span>✅ Bonnes réponses</span><span style="color:var(--g);font-weight:800">${quiz.correct} / ${quiz.questions.length}</span></div>
    <div class="trb-row"><span>❌ Mauvaises réponses</span><span style="color:var(--red);font-weight:800">${quiz.wrong}</span></div>
    <div class="trb-row"><span>⭐ Score final</span><span style="color:var(--y);font-weight:900">${score60} / 60</span></div>
    <div class="trb-row"><span>📊 Pourcentage</span><span style="font-weight:800">${Math.round(pct*100)}%</span></div>`;

  document.getElementById('test-result').classList.add('show');

  // Save
  if(!S.testScores) S.testScores={};
  const prev=S.testScores[quiz.chIdx];
  if(prev==null||score60>prev){ S.testScores[quiz.chIdx]=score60; }
  S.tests++;
  if(score60===60) S.perfect++;
  addXP(score60);
  save();

  // Unlock next chapter if score >= 35/60
  if(score60>=35){
    if(!S.chDone) S.chDone={};
    S.chDone[quiz.chIdx]=true;
    save();
    if(quiz.chIdx<CHAPTERS.length-1) toast(`🎉 Chapitre ${quiz.chIdx+1} terminé ! Chapitre ${quiz.chIdx+2} débloqué !`);
    launchConfetti();
  }
}

function shuffle(arr){ return [...arr].sort(()=>Math.random()-.5); }

/* ═══════════════════════════════════════════════════════
   STATS
═══════════════════════════════════════════════════════ */
function renderStats(){
  document.getElementById('st-xp').textContent=S.xp;
  document.getElementById('st-streak').textContent=S.streak||0;
  document.getElementById('st-words').textContent=S.words||0;
  const scores=Object.values(S.testScores||{});
  document.getElementById('st-tests').textContent=scores.length?Math.round(scores.reduce((a,b)=>a+b,0)/scores.length)+'/60':'—';

  const grid=document.getElementById('badge-grid');
  grid.innerHTML='';
  BADGES.forEach(b=>{
    const unlocked=S.badges&&S.badges.includes(b.id);
    const div=document.createElement('div');
    div.className='badge-item'+(unlocked?' unlocked':'');
    div.innerHTML=`<div class="bi-icon">${unlocked?b.emoji:'🔒'}</div><div class="bi-name">${b.name}</div><div class="bi-req">${b.req}</div>`;
    grid.appendChild(div);
  });
}

/* ═══════════════════════════════════════════════════════
   PWA SERVICE WORKER
═══════════════════════════════════════════════════════ */
if('serviceWorker' in navigator){
  const sw=`const C='fb4';self.addEventListener('install',e=>e.waitUntil(caches.open(C).then(c=>c.addAll(['./','/']))));self.addEventListener('fetch',e=>e.respondWith(caches.match(e.request).then(r=>r||fetch(e.request).catch(()=>new Response('',{status:200})))));`;
  const blob=new Blob([sw],{type:'application/javascript'});
  navigator.serviceWorker.register(URL.createObjectURL(blob)).catch(()=>{});
}

/* ═══════════════════════════════════════════════════════
   BOOT
═══════════════════════════════════════════════════════ */
load();
if(S.level&&S.xp>0){
  document.getElementById('bottom-nav').classList.add('visible');
  navigate('home');
}
// Pre-load voices
if('speechSynthesis' in window) speechSynthesis.getVoices();
</script>

</body>
</html>
