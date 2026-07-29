<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Rohen Clicker Site</title>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: "Segoe UI", sans-serif;
    }

    body {
        min-height: 100vh;
        background: linear-gradient(120deg, #6a00ff, #00d4ff, #00ff9d);
        background-size: 300% 300%;
        animation: gradientShift 12s ease infinite;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding-bottom: 200px;
    }

    @keyframes gradientShift {
        0% { background-position: 0% 50%; }
        50% { background-position: 100% 50%; }
        100% { background-position: 0% 50%; }
    }

    /* Waving chroma title */
    .title {
        font-size: 3rem;
        font-weight: 900;
        margin-top: 20px;
        background: linear-gradient(90deg, red, orange, yellow, green, cyan, blue, purple);
        background-size: 400% 400%;
        -webkit-background-clip: text;
        color: transparent;
        animation: chromaWave 6s linear infinite, wave 2s ease-in-out infinite;
        text-shadow: 0 0 20px rgba(255,255,255,0.4);
    }

    @keyframes chromaWave {
        0% { background-position: 0% 50%; }
        50% { background-position: 100% 50%; }
        100% { background-position: 0% 50%; }
    }

    @keyframes wave {
        0%, 100% { transform: translateY(0); }
        50% { transform: translateY(-10px); }
    }

    .card {
        width: 450px;
        padding: 40px;
        border-radius: 20px;
        backdrop-filter: blur(20px);
        background: rgba(255, 255, 255, 0.15);
        box-shadow: 0 0 40px rgba(0,0,0,0.2);
        text-align: center;
        color: white;
        animation: fadeIn 1.5s ease;
        margin-top: 40px;
    }

    @keyframes fadeIn {
        from { opacity: 0; transform: translateY(20px); }
        to { opacity: 1; transform: translateY(0); }
    }

    h1 {
        font-size: 2.5rem;
        margin-bottom: 10px;
        text-shadow: 0 0 10px rgba(255,255,255,0.5);
    }

    p {
        font-size: 1.1rem;
        margin-bottom: 30px;
        opacity: 0.9;
    }

    .btn {
        display: inline-block;
        padding: 12px 30px;
        border-radius: 30px;
        background: rgba(255,255,255,0.2);
        color: white;
        text-decoration: none;
        font-size: 1.1rem;
        transition: 0.3s;
        border: 2px solid rgba(255,255,255,0.4);
    }

    .btn:hover {
        background: white;
        color: #6a00ff;
        box-shadow: 0 0 20px white;
    }

    /* Clicker Section */
    .clicker-container {
        margin-top: 40px;
        text-align: center;
        color: white;
    }

    .clicker-title {
        font-size: 2rem;
        margin-bottom: 15px;
        text-shadow: 0 0 10px rgba(255,255,255,0.5);
    }

    .spawn-btn {
        padding: 15px 40px;
        font-size: 1.3rem;
        border-radius: 30px;
        border: 2px solid rgba(255,255,255,0.5);
        background: rgba(255,255,255,0.2);
        color: white;
        cursor: pointer;
        transition: 0.3s;
    }

    .spawn-btn:hover {
        background: white;
        color: #6a00ff;
        box-shadow: 0 0 20px white;
    }

    .score {
        margin-top: 20px;
        font-size: 1.5rem;
    }

    /* Floating head animation */
    .floating-head {
        position: absolute;
        width: 80px;
        height: 80px;
        border-radius: 50%;
        animation: floatUp 1.2s ease-out forwards;
        pointer-events: none;
    }

    @keyframes floatUp {
        0% { opacity: 1; transform: translateY(0) scale(1); }
        100% { opacity: 0; transform: translateY(-120px) scale(1.2); }
    }

    #spawnArea {
        position: relative;
        width: 100%;
        height: 300px;
        margin-top: 20px;
    }
</style>
</head>
<body>

<div class="title">SKCUS NEHOR</div>

<div class="card">
    <h1>Welcome</h1>
    <p>This is a clean, animated, futuristic website built with pure HTML and CSS.</p>
    <a class="btn" href="#">Explore More</a>
</div>

<!-- Rohen Clicker Section -->
<div class="clicker-container">
    <h2 class="clicker-title">Rohen Clicker</h2>

    <button id="clickButton" class="spawn-btn">Click Me</button>

    <div class="score">Clicks: <span id="scoreCount">0</span></div>

    <div id="spawnArea"></div>
</div>

<script>
    const clickButton = document.getElementById("clickButton");
    const scoreCount = document.getElementById("scoreCount");
    const spawnArea = document.getElementById("spawnArea");

    let score = 0;

    clickButton.addEventListener("click", () => {
        score++;
        scoreCount.textContent = score;

        // Create floating head
        const head = document.createElement("img");
        head.src = "images/IMG_6400.jpg";  // Your GitHub image
        head.classList.add("floating-head");

        // Random horizontal position
        const x = Math.random() * (spawnArea.clientWidth - 80);
        head.style.left = x + "px";
        head.style.bottom = "0px";

        spawnArea.appendChild(head);

        // Remove after animation
        setTimeout(() => head.remove(), 1200);
    });
</script>

</body>
</html>
