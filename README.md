# timer_game
A game where you touch the screen and there’s a timer that’s all








<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Touch Timer Game</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    html, body {
      margin: 0;
      height: 100%;
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      background: #111;
      color: white;
      font-family: Arial, sans-serif;
      user-select: none;
      -webkit-user-select: none;
      -ms-user-select: none;
      -moz-user-select: none;
      overflow: hidden;
    }

    #timer {
      font-size: 6em;
      font-weight: bold;
      text-align: center;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      transition: transform 0.5s ease;
      user-select: none;
      -webkit-user-select: none;
      -ms-user-select: none;
      -moz-user-select: none;
      pointer-events: none;
    }

    .zoom {
      transform: translate(-50%, -50%) scale(1.5);
    }
  </style>
</head>
<body>
  <div id="timer">0.00</div>

  <script>
    const timerDisplay = document.getElementById("timer");
    let startTime = 0;
    let elapsed = 0;
    let running = false;
    let interval;
    let resetTimeout;
    let finished = false;

    function startTimer() {
      if (!running && !finished) {
        clearTimeout(resetTimeout);
        running = true;
        timerDisplay.classList.remove("zoom");
        startTime = Date.now() - elapsed;
        interval = setInterval(() => {
          elapsed = Date.now() - startTime;
          timerDisplay.textContent = (elapsed / 1000).toFixed(2);
        }, 10);
      }
    }

    function stopTimer() {
      if (running) {
        running = false;
        finished = true;
        clearInterval(interval);
        timerDisplay.classList.add("zoom");

        resetTimeout = setTimeout(() => {
          elapsed = 0;
          timerDisplay.textContent = "0.00";
          timerDisplay.classList.remove("zoom");
          finished = false;
        }, 5000);
      }
    }

    // Mouse and touch support
    document.body.addEventListener("mousedown", startTimer);
    document.body.addEventListener("mouseup", stopTimer);
    document.body.addEventListener("touchstart", startTimer);
    document.body.addEventListener("touchend", stopTimer);

    // Disable right-click menu and selection
    document.body.addEventListener("contextmenu", e => e.preventDefault());
    document.body.addEventListener("selectstart", e => e.preventDefault());
    document.body.addEventListener("dragstart", e => e.preventDefault());
  </script>
</body>
</html>
