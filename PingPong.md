<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Neon Ping Pong</title>

<style>
body{
    margin:0;
    overflow:hidden;
    background:#111;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
    font-family:Arial,Helvetica,sans-serif;
}

canvas{
    background:#000;
    border:4px solid #00ffee;
    box-shadow:0 0 30px #00ffee;
}

#instructions{
    position:absolute;
    top:20px;
    color:white;
    text-align:center;
    width:100%;
    font-size:18px;
}
</style>
</head>
<body>

<div id="instructions">
W/S or ↑/↓ to Move &nbsp; | &nbsp; First to 10 Wins
</div>

<canvas id="game" width="900" height="500"></canvas>

<script>

const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

const WIDTH = canvas.width;
const HEIGHT = canvas.height;

const paddleWidth = 15;
const paddleHeight = 110;

let player = {
    x:25,
    y:HEIGHT/2-paddleHeight/2,
    score:0
};

let ai = {
    x:WIDTH-40,
    y:HEIGHT/2-paddleHeight/2,
    score:0
};

let ball = {
    x:WIDTH/2,
    y:HEIGHT/2,
    radius:10,
    vx:6,
    vy:4,
    speed:6
};

const keys = {};

document.addEventListener("keydown",e=>keys[e.key]=true);
document.addEventListener("keyup",e=>keys[e.key]=false);

function resetBall(){

    ball.x=WIDTH/2;
    ball.y=HEIGHT/2;

    ball.speed=6;

    let angle=(Math.random()*Math.PI/2)-(Math.PI/4);

    let dir=Math.random()>0.5?1:-1;

    ball.vx=Math.cos(angle)*ball.speed*dir;
    ball.vy=Math.sin(angle)*ball.speed;
}

function drawCenter(){

    ctx.strokeStyle="#444";
    ctx.setLineDash([12,18]);

    ctx.beginPath();
    ctx.moveTo(WIDTH/2,0);
    ctx.lineTo(WIDTH/2,HEIGHT);
    ctx.stroke();

    ctx.setLineDash([]);
}

function draw(){

    ctx.clearRect(0,0,WIDTH,HEIGHT);

    drawCenter();

    // paddles
    ctx.fillStyle="#00ffee";

    ctx.fillRect(player.x,player.y,paddleWidth,paddleHeight);
    ctx.fillRect(ai.x,ai.y,paddleWidth,paddleHeight);

    // ball
    ctx.beginPath();
    ctx.arc(ball.x,ball.y,ball.radius,0,Math.PI*2);
    ctx.fillStyle="#ffffff";
    ctx.fill();

    // score
    ctx.fillStyle="white";
    ctx.font="48px Arial";
    ctx.fillText(player.score,WIDTH/2-90,60);
    ctx.fillText(ai.score,WIDTH/2+60,60);
}

function update(){

    // PLAYER
    if(keys["w"]||keys["W"])
        player.y-=8;

    if(keys["s"]||keys["S"])
        player.y+=8;

    if(keys["ArrowUp"])
        player.y-=8;

    if(keys["ArrowDown"])
        player.y+=8;

    player.y=Math.max(0,Math.min(HEIGHT-paddleHeight,player.y));

    // AI

    let target=ball.y-paddleHeight/2+ball.radius;

    ai.y+=(target-ai.y)*0.09;

    ai.y=Math.max(0,Math.min(HEIGHT-paddleHeight,ai.y));

    // Ball movement

    ball.x+=ball.vx;
    ball.y+=ball.vy;

    // Wall collision

    if(ball.y-ball.radius<0 || ball.y+ball.radius>HEIGHT){
        ball.vy*=-1;
    }

    // Paddle collision function

    function collide(p){

        return ball.x-ball.radius<p.x+paddleWidth &&
               ball.x+ball.radius>p.x &&
               ball.y>p.y &&
               ball.y<p.y+paddleHeight;
    }

    // Player collision

    if(collide(player) && ball.vx<0){

        let hit=(ball.y-(player.y+paddleHeight/2))/(paddleHeight/2);

        let angle=hit*Math.PI/3;

        ball.speed+=0.35;

        ball.vx=Math.cos(angle)*ball.speed;
        ball.vy=Math.sin(angle)*ball.speed;
    }

    // AI collision

    if(collide(ai) && ball.vx>0){

        let hit=(ball.y-(ai.y+paddleHeight/2))/(paddleHeight/2);

        let angle=hit*Math.PI/3;

        ball.speed+=0.35;

        ball.vx=-Math.cos(angle)*ball.speed;
        ball.vy=Math.sin(angle)*ball.speed;
    }

    // Score

    if(ball.x<0){

        ai.score++;
        resetBall();
    }

    if(ball.x>WIDTH){

        player.score++;
        resetBall();
    }

    if(player.score===10){

        alert("You Win!");
        player.score=0;
        ai.score=0;
        resetBall();
    }

    if(ai.score===10){

        alert("Computer Wins!");
        player.score=0;
        ai.score=0;
        resetBall();
    }

}

function loop(){

    update();
    draw();

    requestAnimationFrame(loop);

}

resetBall();
loop();

</script>

</body>
</html>
