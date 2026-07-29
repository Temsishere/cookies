<!DOCTYPE html>
<html>
<head>
<title>Dinosaur Runner</title>

<style>
body{
    margin:0;
    background:#222;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
    font-family:Arial;
}

canvas{
    background:white;
    border:3px solid black;
}
</style>

</head>

<body>

<canvas id="game" width="900" height="300"></canvas>

<script>

const canvas=document.getElementById("game");
const ctx=canvas.getContext("2d");

let gravity=0.7;
let score=0;
let gameOver=false;
let speed=6;

let keys={};

document.addEventListener("keydown",e=>{

    keys[e.code]=true;

    if(e.code==="Space" && gameOver){
        restart();
    }

});

document.addEventListener("keyup",e=>{
    keys[e.code]=false;
});


let dino={

    x:80,
    y:220,

    width:40,
    height:50,

    dy:0,

    jumping:false

};


let obstacles=[];


let clouds=[];

for(let i=0;i<5;i++){

    clouds.push({

        x:Math.random()*900,
        y:40+Math.random()*80

    });

}



function spawnObstacle(){

    let type=Math.random();

    obstacles.push({

        x:900,

        y:type>0.8?150:220,

        width:type>0.8?45:25,

        height:type>0.8?40:50,

        bird:type>0.8

    });

}



function jump(){

    if(!dino.jumping){

        dino.dy=-13;
        dino.jumping=true;

    }

}



function update(){

    if(gameOver)return;


    if(keys["Space"])
        jump();



    // gravity

    dino.dy+=gravity;
    dino.y+=dino.dy;



    if(dino.y>=220){

        dino.y=220;
        dino.dy=0;
        dino.jumping=false;

    }



    // obstacles

    for(let i=obstacles.length-1;i>=0;i--){

        let o=obstacles[i];

        o.x-=speed;


        if(o.x+o.width<0){

            obstacles.splice(i,1);
            score++;

        }



        if(

            dino.x < o.x+o.width &&
            dino.x+dino.width > o.x &&
            dino.y < o.y+o.height &&
            dino.y+dino.height > o.y

        ){

            gameOver=true;

        }

    }



    if(Math.random()<0.015)
        spawnObstacle();



    // clouds

    clouds.forEach(c=>{

        c.x-=1;

        if(c.x<-50)
            c.x=950;

    });



    speed+=0.001;

}



function draw(){

    ctx.clearRect(0,0,900,300);


    // sky

    ctx.fillStyle="#dff6ff";
    ctx.fillRect(0,0,900,300);



    // clouds

    ctx.fillStyle="white";

    clouds.forEach(c=>{

        ctx.beginPath();

        ctx.arc(c.x,c.y,20,0,Math.PI*2);

        ctx.fill();

    });



    // ground

    ctx.fillStyle="#555";

    ctx.fillRect(0,270,900,30);



    // dino

    ctx.fillStyle="#333";

    ctx.fillRect(
        dino.x,
        dino.y,
        dino.width,
        dino.height
    );


    // eye

    ctx.fillStyle="white";

    ctx.fillRect(
        dino.x+25,
        dino.y+10,
        8,
        8
    );



    // obstacles

    obstacles.forEach(o=>{


        ctx.fillStyle=o.bird?"#e74c3c":"#228B22";


        ctx.fillRect(
            o.x,
            o.y,
            o.width,
            o.height
        );


    });



    // score

    ctx.fillStyle="black";

    ctx.font="25px Arial";

    ctx.fillText(
        "Score: "+score,
        20,
        40
    );



    if(gameOver){

        ctx.fillStyle="rgba(0,0,0,.5)";
        ctx.fillRect(0,0,900,300);


        ctx.fillStyle="white";

        ctx.font="40px Arial";

        ctx.fillText(
            "GAME OVER",
            320,
            130
        );


        ctx.font="20px Arial";

        ctx.fillText(
            "Press SPACE to restart",
            330,
            170
        );

    }

}



function restart(){

    score=0;
    speed=6;

    obstacles=[];

    dino.y=220;
    dino.dy=0;

    gameOver=false;

}



function loop(){

    update();
    draw();

    requestAnimationFrame(loop);

}


loop();

</script>

</body>
</html>
