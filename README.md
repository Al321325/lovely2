<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Valentine Love for Raghad</title>
<style>
body {
    margin: 0;
    padding: 0;
    height: 100vh;
    background: radial-gradient(circle at bottom, #1a001a, #330033);
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    font-family: 'Poppins', sans-serif;
    text-align: center;
}

/* Center Heart */
.heart {
    width: 200px;
    height: 200px;
    background: linear-gradient(45deg, #ff1e56, #ff66a3);
    position: relative;
    transform: rotate(-45deg);
    animation: glow 1s infinite alternate, beat 1s infinite ease-in-out;
    cursor: pointer;
    z-index: 10;
    box-shadow: 0 0 40px #ff1e56;
    border-radius: 20px;
    transition: all 0.5s ease;
}
.heart.active {
    transform: rotate(-45deg) scale(1.5);
    box-shadow: 0 0 80px #ff1e56, 0 0 160px #ff66a3;
}
.heart:before, .heart:after {
    content: "";
    width: 200px;
    height: 200px;
    background: linear-gradient(45deg, #ff1e56, #ff66a3);
    border-radius: 50%;
    position: absolute;
}
.heart:before { top: -100px; left: 0; }
.heart:after { left: 100px; top: 0; }
@keyframes beat {
    0%, 100% { transform: rotate(-45deg) scale(1); }
    50% { transform: rotate(-45deg) scale(1.3); }
}
@keyframes glow {
    0% { box-shadow: 0 0 20px #ff1e56, 0 0 40px #ff66a3; }
    100% { box-shadow: 0 0 40px #ff1e56, 0 0 80px #ff66a3; }
}

/* Message */
.message {
    position: absolute;
    bottom: 50px;
    color: #ff99cc;
    font-size: 32px;
    font-weight: bold;
    min-height: 50px;
    opacity: 0;
    transition: opacity 1s ease;
}
.message.show {
    opacity: 1;
}
.message .raghad {
    color: #fff176;
    font-weight: bold;
    text-shadow: 0 0 20px #fff176;
    animation: appear 1s ease forwards;
}

/* Fireworks Hearts */
.firework-heart {
    position: absolute;
    width: 20px;
    height: 20px;
    background: #ff3366;
    transform: rotate(-45deg);
    border-radius: 20px;
    animation: explode 0.8s forwards;
}

/* Rain Hearts */
.rain-heart {
    position: absolute;
    width: 15px;
    height: 15px;
    background: #ff6699;
    transform: rotate(-45deg);
    border-radius: 20px;
    animation: fall linear infinite;
    opacity: 0.8;
}
.rain-heart.intense {
    animation-duration: 1s !important;
}
@keyframes fall {
    0% { transform: translateY(-50px); opacity:0.8; }
    100% { transform: translateY(100vh); opacity:0; }
}
@keyframes explode {
    0% { transform: scale(0) translate(0,0); opacity:1; }
    100% { transform: scale(1.5) translate(var(--x), var(--y)); opacity:0; }
}

/* Sparkles */
.sparkle {
    position: absolute;
    width: 6px;
    height: 6px;
    background: #fff;
    border-radius: 50%;
    opacity: 0.8;
    animation: sparkleAnim 2s infinite;
}
@keyframes sparkleAnim {
    0%,100% { transform: translateY(0) scale(1); opacity:0.7; }
    50% { transform: translateY(-15px) scale(1.5); opacity:1; }
}

/* Raghad appear animation */
@keyframes appear {
    0% { opacity: 0; transform: scale(0.5) rotate(-10deg); }
    100% { opacity: 1; transform: scale(1) rotate(0deg); }
}
</style>
</head>
<body>

<div class="heart" id="heart"></div>
<div class="message" id="message"></div>

<div id="fireworkContainer"></div>
<div id="rainContainer"></div>
<div id="sparkleContainer"></div>

<script>
// Generate rain hearts continuously
function createRain() {
    const rain = document.getElementById('rainContainer');
    setInterval(()=>{
        const heart = document.createElement('div');
        heart.className = 'rain-heart';
        heart.style.left = Math.random()*100 + 'vw';
        heart.style.animationDuration = (2+Math.random()*2)+'s';
        rain.appendChild(heart);
        setTimeout(()=>heart.remove(),5000);
    },100);
}
createRain();

// Generate floating sparkles
function createSparkles() {
    const container = document.getElementById('sparkleContainer');
    for(let i=0;i<50;i++){
        const s = document.createElement('div');
        s.className='sparkle';
        s.style.left= 50 + Math.random()*100 -50 + 'vw';
        s.style.top= 50 + Math.random()*100 -50 + 'vh';
        s.style.animationDuration=(1+Math.random()*2)+'s';
        container.appendChild(s);
    }
}
createSparkles();

// Heart click event
const heart = document.getElementById('heart');
const message = document.getElementById('message');
const fireworkContainer = document.getElementById('fireworkContainer');
const rainContainer = document.getElementById('rainContainer');

heart.addEventListener('click', ()=>{
    // Heart pulses bigger and glows
    heart.classList.add('active');
    setTimeout(()=>heart.classList.remove('active'),1500);

    // Show message
    message.classList.add('show');
    typeWriter("I love you so much Raghad❤️", message);

    // Explode firework hearts
    explodeFirework();

    // Intensify rain hearts
    const rains = rainContainer.querySelectorAll('.rain-heart');
    rains.forEach(r => r.classList.add('intense'));
    setTimeout(()=>rains.forEach(r => r.classList.remove('intense')),1500);

    // Add extra sparkles around heart
    createExtraSparkles();
});

// Typewriter effect
function typeWriter(text, element) {
    element.innerHTML = '';
    const span = document.createElement('span');
    element.appendChild(span);
    let i=0;
    function type() {
        if(i<text.length){
            span.innerHTML+=text.charAt(i);
            i++;
            setTimeout(type,50);
        }
    }
    type();
}

// Firework hearts explosion
function explodeFirework() {
    for(let i=0;i<40;i++){
        const h = document.createElement('div');
        h.className='firework-heart';
        let angle = Math.random()*360;
        let distance = Math.random()*250 +50;
        h.style.setProperty('--x', distance*Math.cos(angle*Math.PI/180)+'px');
        h.style.setProperty('--y', distance*Math.sin(angle*Math.PI/180)+'px');
        h.style.left='50%';
        h.style.top='50%';
        fireworkContainer.appendChild(h);
        setTimeout(()=>h.remove(),1000);
    }
}

// Extra sparkles for heart click
function createExtraSparkles() {
    const container = document.getElementById('sparkleContainer');
    for(let i=0;i<20;i++){
        const s = document.createElement('div');
        s.className='sparkle';
        s.style.left= 50 + Math.random()*60 -30 + 'vw';
        s.style.top= 50 + Math.random()*60 -30 + 'vh';
        s.style.animationDuration=(0.5+Math.random()*1.5)+'s';
        container.appendChild(s);
        setTimeout(()=>s.remove(),1500);
    }
}
</script>

</body>
</html>
