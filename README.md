<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Weverson | Developer</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Poppins,sans-serif;
}

body{
    background:#070b18;
    overflow:hidden;
    color:white;
}

canvas{
    position:fixed;
    inset:0;
    z-index:-1;
}

.container{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
}

.card{

    width:900px;
    max-width:90%;
    padding:50px;

    border-radius:30px;

    backdrop-filter:blur(20px);
    background:rgba(255,255,255,.05);

    border:1px solid rgba(255,255,255,.1);

    box-shadow:
    0 0 50px #00aaff33,
    0 0 150px #0055ff22;

    transition:.3s;

}

.card:hover{

transform:translateY(-10px);

box-shadow:
0 0 70px #00bfff55,
0 0 200px #0066ff44;

}

h1{

font-size:60px;
margin-bottom:10px;

background:linear-gradient(90deg,#00c6ff,#7b2fff);

-webkit-background-clip:text;
-webkit-text-fill-color:transparent;

}

.typing{

font-size:23px;
height:35px;
margin-bottom:35px;

color:#8dd8ff;

}

.skills{

display:grid;
grid-template-columns:repeat(4,1fr);
gap:20px;

margin-top:30px;

}

.skill{

padding:25px;

border-radius:20px;

background:rgba(255,255,255,.04);

text-align:center;

transition:.3s;

cursor:pointer;

}

.skill:hover{

transform:translateY(-10px) scale(1.05);

background:rgba(0,170,255,.18);

}

.skill img{

width:70px;

margin-bottom:15px;

}

.social{

margin-top:40px;

display:flex;

gap:20px;

}

.social a{

text-decoration:none;

color:white;

padding:12px 28px;

border-radius:50px;

background:linear-gradient(90deg,#00c6ff,#0055ff);

transition:.3s;

}

.social a:hover{

transform:scale(1.08);

}

.glow{

position:absolute;

width:600px;
height:600px;

background:#008cff;

filter:blur(180px);

opacity:.18;

border-radius:50%;

animation:move 10s infinite alternate;

}

@keyframes move{

0%{

transform:translate(-150px,-120px);

}

100%{

transform:translate(400px,150px);

}

}

@media(max-width:850px){

.skills{

grid-template-columns:repeat(2,1fr);

}

h1{

font-size:42px;

}

}

</style>

</head>

<body>

<div class="glow"></div>

<canvas id="stars"></canvas>

<div class="container">

<div class="card">

<h1>Weverson</h1>

<div class="typing"></div>

<p>
Apaixonado por tecnologia e desenvolvimento de software.
<br><br>
💻 HTML • CSS • JavaScript • Python
</p>

<div class="skills">

<div class="skill">
<img src="https://skillicons.dev/icons?i=html">
<h3>HTML</h3>
</div>

<div class="skill">
<img src="https://skillicons.dev/icons?i=css">
<h3>CSS</h3>
</div>

<div class="skill">
<img src="https://skillicons.dev/icons?i=javascript">
<h3>JavaScript</h3>
</div>

<div class="skill">
<img src="https://skillicons.dev/icons?i=python">
<h3>Python</h3>
</div>

</div>

<div class="social">

<a href="https://github.com/SEUUSUARIO">GitHub</a>

<a href="#">Projetos</a>

</div>

</div>

</div>

<script>

const text=[
"Front-End Developer",
"HTML • CSS • JavaScript",
"Python Developer",
"Always Learning 🚀"
];

let line=0;
let char=0;
let erase=false;

const typing=document.querySelector(".typing");

function type(){

if(!erase){

typing.innerHTML=text[line].slice(0,char++);

if(char>text[line].length){

erase=true;

setTimeout(type,1500);

return;

}

}else{

typing.innerHTML=text[line].slice(0,char--);

if(char<0){

erase=false;

line=(line+1)%text.length;

}

}

setTimeout(type,erase?40:80);

}

type();

const canvas=document.getElementById("stars");

const ctx=canvas.getContext("2d");

function resize(){

canvas.width=innerWidth;

canvas.height=innerHeight;

}

resize();

addEventListener("resize",resize);

const stars=[];

for(let i=0;i<180;i++){

stars.push({

x:Math.random()*canvas.width,

y:Math.random()*canvas.height,

r:Math.random()*2,

v:Math.random()*0.5+0.2

});

}

function animate(){

ctx.clearRect(0,0,canvas.width,canvas.height);

ctx.fillStyle="white";

stars.forEach(s=>{

ctx.beginPath();

ctx.arc(s.x,s.y,s.r,0,Math.PI*2);

ctx.fill();

s.y+=s.v;

if(s.y>canvas.height){

s.y=0;

s.x=Math.random()*canvas.width;

}

});

requestAnimationFrame(animate);

}

animate();

document.querySelectorAll(".skill").forEach(card=>{

card.addEventListener("mousemove",e=>{

const rect=card.getBoundingClientRect();

const x=e.clientX-rect.left;

const y=e.clientY-rect.top;

const rotateY=((x-rect.width/2)/8);

const rotateX=((rect.height/2-y)/8);

card.style.transform=`perspective(700px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.08)`;

});

card.addEventListener("mouseleave",()=>{

card.style.transform="perspective(700px) rotateX(0) rotateY(0)";

});

});

</script>

</body>
</html>
