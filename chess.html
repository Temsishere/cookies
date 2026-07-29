<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Playable Chess Hub</title>
  
  <!-- Chessboard.js CSS -->
  <link rel="stylesheet" href="https://unpkg.com/@chrisoakman/chessboardjs@1.0.0/dist/chessboard-1.0.0.min.css">

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      background-color: #161512;
      color: #bababa;
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    header {
      background-color: #1e1e1e;
      border-bottom: 1px solid #2a2a2a;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .logo {
      font-size: 1.5rem;
      font-weight: bold;
      color: #38bdf8;
      text-decoration: none;
    }

    .container {
      display: flex;
      flex-wrap: wrap;
      gap: 2rem;
      max-width: 1200px;
      margin: 2rem auto;
      padding: 0 1rem;
      flex: 1;
      justify-content: center;
    }

    .board-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.75rem;
    }

    .player-card {
      width: 100%;
      max-width: 560px;
      background-color: #262421;
      padding: 0.75rem 1rem;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .player-info {
      display: flex;
      align-items: center;
      gap: 0.75rem;
      font-weight: 600;
      color: #ffffff;
    }

    .avatar {
      width: 36px;
      height: 36px;
      border-radius: 4px;
      background-color: #38bdf8;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: bold;
      color: #161512;
    }

    .timer {
      background-color: #161512;
      padding: 0.4rem 0.8rem;
      border-radius: 4px;
      font-family: monospace;
      font-size: 1.2rem;
      font-weight: bold;
      color: #ffffff;
    }

    .timer.active {
      background-color: #38bdf8;
      color: #161512;
    }

    #myBoard {
      width: 560px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
      border-radius: 4px;
      overflow: hidden;
    }

    .game-panel {
      width: 360px;
      background-color: #262421;
      border-radius: 8px;
      display: flex;
      flex-direction: column;
      height: 660px;
    }

    .panel-header {
      padding: 1.25rem;
      border-bottom: 1px solid #363431;
      font-size: 1.1rem;
      font-weight: bold;
      color: #ffffff;
    }

    .move-history {
      flex: 1;
      padding: 1rem;
      overflow-y: auto;
      font-family: monospace;
      font-size: 1rem;
    }

    .move-row {
      display: grid;
      grid-template-columns: 40px 1fr 1fr;
      padding: 0.4rem 0.5rem;
      border-radius: 4px;
    }

    .move-row:nth-child(even) {
      background-color: #1e1d1b;
    }

    .move-number {
      color: #7c7a76;
    }

    .panel-actions {
      padding: 1.25rem;
      border-top: 1px solid #363431;
      display: flex;
      flex-direction: column;
      gap: 0.75rem;
    }

    .btn {
      width: 100%;
      padding: 0.8rem;
      border: none;
      border-radius: 6px;
      font-weight: bold;
      font-size: 1rem;
      cursor: pointer;
    }

    .btn-primary {
      background-color: #81b64c;
      color: #ffffff;
    }

    .btn-primary:hover {
      background-color: #a3d168;
    }

    @media (max-width: 960px) {
      #myBoard {
        width: 100%;
        max-width: 400px;
      }
      .game-panel {
        width: 100%;
        max-width: 400px;
        height: 350px;
      }
    }
  </style>
</head>
<body>

  <header>
    <a href="#" class="logo">ChessHub</a>
  </header>

  <div class="container">
    <div class="board-container">
      
      <!-- Black Player -->
      <div class="player-card">
        <div class="player-info">
          <div class="avatar">B</div>
          <span>Black Player</span>
        </div>
        <div id="black-timer" class="timer">05:00</div>
      </div>

      <!-- Chessboard Container -->
      <div id="myBoard"></div>

      <!-- White Player -->
      <div class="player-card">
        <div class="player-info">
          <div class="avatar" style="background-color: #81b64c;">W</div>
          <span>White Player</span>
        </div>
        <div id="white-timer" class="timer active">05:00</div>
      </div>

    </div>

    <!-- Game Control Panel -->
    <div class="game-panel">
      <div class="panel-header" id="status">White to move</div>
      <div class="move-history" id="move-history"></div>
      <div class="panel-actions">
        <button class="btn btn-primary" onclick="resetGame()">Restart Game</button>
      </div>
    </div>
  </div>

  <!-- Dependencies: jQuery, Chess.js (rules), Chessboard.js (UI) -->
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/chess.js/0.10.3/chess.min.js"></script>
  <script src="https://unpkg.com/@chrisoakman/chessboardjs@1.0.0/dist/chessboard-1.0.0.min.js"></script>

  <script>
    let board = null;
    let game = new Chess();
    
    // Timer Variables (5 minutes each = 300 seconds)
    let whiteTime = 300;
    let blackTime = 300;
    let timerInterval = null;
    let gameStarted = false;

    function formatTime(seconds) {
      let min = Math.floor(seconds / 60);
      let sec = seconds % 60;
      return `${min.toString().padStart(2, '0')}:${sec.toString().padStart(2, '0')}`;
    }

    function startTimer() {
      if (timerInterval) clearInterval(timerInterval);
      
      timerInterval = setInterval(() => {
        if (!gameStarted || game.game_over()) return;

        if (game.turn() === 'w') {
          whiteTime--;
          $('#white-timer').text(formatTime(whiteTime));
          if (whiteTime <= 0) handleTimeOut('Black');
        } else {
          blackTime--;
          $('#black-timer').text(formatTime(blackTime));
          if (blackTime <= 0) handleTimeOut('White');
        }
      }, 1000);
    }

    function handleTimeOut(winner) {
      clearInterval(timerInterval);
      $('#status').text(`Game Over! ${winner} wins on time.`);
    }

    function updateTimerHighlight() {
      if (game.turn() === 'w') {
        $('#white-timer').addClass('active');
        $('#black-timer').removeClass('active');
      } else {
        $('#black-timer').addClass('active');
        $('#white-timer').removeClass('active');
      }
    }

    function onDragStart(source, piece, position, orientation) {
      if (game.game_over()) return false;

      // Only allow picking up pieces for the player whose turn it is
      if ((game.turn() === 'w' && piece.search(/^b/) !== -1) ||
          (game.turn() === 'b' && piece.search(/^w/) !== -1)) {
        return false;
      }
    }

    function onDrop(source, target) {
      // See if the move is legal according to chess rules
      let move = game.move({
        from: source,
        to: target,
        promotion: 'q' // Auto promote to Queen for simplicity
      });

      // Illegal move
      if (move === null) return 'snapback';

      // Start clock on first move
      if (!gameStarted) {
        gameStarted = true;
        startTimer();
      }

      updateStatus();
      updateMoveHistory();
      updateTimerHighlight();
    }

    function onSnapEnd() {
      board.position(game.fen());
    }

    function updateStatus() {
      let status = '';
      let moveColor = game.turn() === 'b' ? 'Black' : 'White';

      if (game.in_checkmate()) {
        status = `Game over, ${moveColor} is in checkmate.`;
        clearInterval(timerInterval);
      } else if (game.in_draw()) {
        status = 'Game over, drawn position.';
        clearInterval(timerInterval);
      } else {
        status = `${moveColor} to move`;
        if (game.in_check()) {
          status += `, ${moveColor} is in check!`;
        }
      }

      $('#status').text(status);
    }

    function updateMoveHistory() {
      let history = game.history();
      let html = '';

      for (let i = 0; i < history.length; i += 2) {
        let moveNum = (i / 2) + 1;
        let whiteMove = history[i] || '';
        let blackMove = history[i + 1] || '';

        html += `
          <div class="move-row">
            <span class="move-number">${moveNum}.</span>
            <span>${whiteMove}</span>
            <span>${blackMove}</span>
          </div>
        `;
      }

      $('#move-history').html(html);
      $('#move-history').scrollTop($('#move-history')[0].scrollHeight);
    }

    function resetGame() {
      game.reset();
      board.start();
      whiteTime = 300;
      blackTime = 300;
      gameStarted = false;
      clearInterval(timerInterval);

      $('#white-timer').text(formatTime(whiteTime)).addClass('active');
      $('#black-timer').text(formatTime(blackTime)).removeClass('active');
      $('#move-history').empty();
      $('#status').text('White to move');
    }

    // Initialize Chessboard
    board = Chessboard('myBoard', {
      draggable: true,
      position: 'start',
      onDragStart: onDragStart,
      onDrop: onDrop,
      onSnapEnd: onSnapEnd,
      pieceTheme: 'https://chessboardjs.com/img/chesspieces/wikipedia/{piece}.png'
    });

    $(window).resize(board.resize);
  </script>
</body>
</html>
