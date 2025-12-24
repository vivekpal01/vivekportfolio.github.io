<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Neon Hacker Portfolio</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
:root{
  --bg:#05060a;
  --neon:#00ff9c;
}
*{margin:0;padding:0;box-sizing:border-box;font-family:Courier New,monospace}
body{
  background:black;
  color:#e5e7eb;
  overflow:hidden;
}

/* MATRIX CANVAS */
canvas{
  position:fixed;
  inset:0;
  z-index:-2;
}

/* TERMINAL INTRO */
#terminal{
  position:fixed;
  inset:0;
  background:black;
  color:var(--neon);
  padding:20px;
  font-size:14px;
  z-index:10;
}
#terminal span{display:block}

/* CURSOR */
.cursor{
  width:18px;height:18px;
  border:2px solid var(--neon);
  border-radius:50%;
  position:fixed;
  pointer-events:none;
  transform:translate(-50%,-50%);
  box-shadow:0 0 15px var(--neon);
  z-index:9;
}

/* MAIN */
main{
  opacity:0;
  transition:opacity 1s ease;
}
header{
  text-align:center;
  padding:90px 20px 60px;
}
.avatar{
  width:140px;height:140px;border-radius:50%;
  background:url("https://i.imgur.com/8Km9tLL.png") center/cover;
  margin:0 auto 25px;
  box-shadow:0 0 30px var(--neon);
  animation:float 4s ease-in-out infinite;
}
h1{
  color:var(--neon);
  text-shadow:0 0 20px var(--neon);
}
section{
  max-width:1000px;
  margin:auto;
  padding:40px 20px;
}
.card{
  background:#0b1020;
  padding:25px;
  margin-bottom:20px;
  border:1px solid rgba(0,255,156,.3);
  transition:.3s;
}
.card:hover{
  box-shadow:0 0 25px var(--neon);
}

/* ANIMS */
@keyframes float{
  50%{transform:translateY(-10px)}
}
</style>
</head>

<body>

<canvas id="matrix"></canvas>
<div class="cursor"></div>

<div id="terminal"></div>

<main id="site">
<header>
  <div class="avatar"></div>
  <h1>YOUR NAME</h1>
  <p>HACKER MODE ONLINE</p>
</header>

<section>
  <div class="card">About: Neon hacker portfolio</div>
  <div class="card">Projects: Interactive demos</div>
  <div class="card">Skills: HTML CSS JS</div>
  <div class="card">Contact: you@domain.com</div>
</section>
</main>

<audio id="hoverSound" src="https://assets.mixkit.co/sfx/preview/mixkit-tech-click-1140.mp3"></audio>

<script>
/* MATRIX RAIN */
const c=document.getElementById("matrix"),ctx=c.getContext("2d");
c.width=innerWidth;c.height=innerHeight;
const letters="01ABCDEFGHIJKLMNOPQRSTUVWXYZ";
const font=16,cols=c.width/font;
const drops=Array(cols).fill(1);
setInterval(()=>{
 ctx.fillStyle="rgba(0,0,0,.05)";
 ctx.fillRect(0,0,c.width,c.height);
 ctx.fillStyle="#00ff9c";
 ctx.font=font+"px monospace";
 drops.forEach((y,i)=>{
   const t=letters[Math.random()*letters.length|0];
   ctx.fillText(t,i*font,y*font);
   if(y*font>c.height&&Math.random()>.975)drops[i]=0;
   drops[i]++;
 });
},50);

/* TERMINAL INTRO */
const lines=[
 "Initializing system...",
 "Loading modules...",
 "Injecting UI...",
 "Access granted."
];
let i=0;
const term=document.getElementById("terminal");
const type=setInterval(()=>{
 if(i<lines.length){
  const s=document.createElement("span");
  s.textContent=lines[i++];
  term.appendChild(s);
 }else{
  clearInterval(type);
  setTimeout(()=>{
    term.style.display="none";
    document.getElementById("site").style.opacity=1;
  },800);
 }
},600);

/* CURSOR FOLLOW */
const cursor=document.querySelector(".cursor");
document.addEventListener("mousemove",e=>{
 cursor.style.left=e.clientX+"px";
 cursor.style.top=e.clientY+"px";
});

/* SOUND ON HOVER */
const snd=document.getElementById("hoverSound");
document.querySelectorAll(".card").forEach(c=>{
 c.addEventListener("mouseenter",()=>{
   snd.currentTime=0;
   snd.play();
 });
});
</script>

</body>
</html>
