# Crownclickergame
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Crown Clicker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #000;
      color: #fff;
      padding: 50px;
      margin: 0;
    }

    h1 {
      margin-bottom: 20px;
    }

    #clickButton {
      font-size: 48px;
      padding: 20px 40px;
      margin: 20px;
      background-color: #ffd700;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      transition: transform 0.2s;
    }

    #clickButton:active {
      transform: scale(0.9);
    }

    .upgrade {
      margin: 10px;
      padding: 15px;
      background-color: #444;
      color: #fff;
      border-radius: 8px;
      cursor: pointer;
      border: none;
    }

    .upgrade:disabled {
      background-color: #222;
      cursor: not-allowed;
    }

    footer {
      position: fixed;
      bottom: 5px;
      width: 100%;
      font-size: 10px;
      color: #888;
      text-align: center;
    }

    #leaderboard {
      margin-top: 30px;
      font-size: 18px;
      color: #FFD700;
    }

    #miningMan {
      width: 150px;
      height: 150px;
      background-image: url('https://example.com/mining-man.png');
      background-size: cover;
      display: none;
      position: fixed;
      bottom: 10px;
      left: 50%;
      transform: translateX(-50%);
    }
  </style>
</head>
<body>
  <h1>Crown Clicker</h1>
  <p>Points: <span id="points">0</span></p>
  <button id="clickButton">👑</button>

  <h2>Upgrades</h2>
  <div>
    <button class="upgrade" id="upgrade1">+1 per click (Cost: <span id="cost1">10</span>)</button><br>
    <button class="upgrade" id="upgrade2">+5 per click (Cost: <span id="cost2">100</span>)</button><br>
    <button class="upgrade" id="upgrade3">Double per click (Cost: <span id="cost3">1000</span>)</button><br>
    <button class="upgrade" id="upgrade4">Triple per click (Cost: <span id="cost4">5000</span>)</button><br>
    <button class="upgrade" id="miningUpgrade">Mining Man (Cost: <span id="costMining">10000</span>)</button>
  </div>

  <h3>Leaderboard</h3>
  <div id="leaderboard">
    <p>Top Player: <span id="topPlayer">Player 1</span> - <span id="topScore">0</span> points</p>
  </div>

  <footer>This is a FazzyNet game</footer>

  <div id="miningMan"></div>

  <script>
    let points = 0;
    let pointsPerClick = 1;
    let upgrade1Cost = 10;
    let upgrade2Cost = 100;
    let upgrade3Cost = 1000;
    let upgrade4Cost = 5000;
    let miningUpgradeCost = 10000;
    let autoClickerActive = false;

    // Multiple Players
    let players = [
      { name: "Player 1", score: 0 },
      { name: "Player 2", score: 0 },
      { name: "Player 3", score: 0 },
    ];

    let currentPlayerIndex = 0;

    // Elements
    const pointsDisplay = document.getElementById("points");
    const clickButton = document.getElementById("clickButton");
    const upgrade1 = document.getElementById("upgrade1");
    const upgrade2 = document.getElementById("upgrade2");
    const upgrade3 = document.getElementById("upgrade3");
    const upgrade4 = document.getElementById("upgrade4");
    const miningUpgrade = document.getElementById("miningUpgrade");
    const cost1 = document.getElementById("cost1");
    const cost2 = document.getElementById("cost2");
    const cost3 = document.getElementById("cost3");
    const cost4 = document.getElementById("cost4");
    const costMining = document.getElementById("costMining");
    const leaderboardDisplay = document.getElementById("leaderboard");
    const miningMan = document.getElementById("miningMan");

    // Crown Animation on Click
    clickButton.onclick = () => {
      points += pointsPerClick;
      clickButton.style.transform = "scale(1.1)";
      setTimeout(() => clickButton.style.transform = "scale(1)", 200);
      updateDisplay();
    };

    // Upgrade Functions
    upgrade1.onclick = () => {
      if (points >= upgrade1Cost) {
        points -= upgrade1Cost;
        pointsPerClick += 1;
        upgrade1Cost = Math.floor(upgrade1Cost * 1.5);
        cost1.textContent = upgrade1Cost;
        updateDisplay();
      }
    };

    upgrade2.onclick = () => {
      if (points >= upgrade2Cost) {
        points -= upgrade2Cost;
        pointsPerClick += 5;
        upgrade2Cost = Math.floor(upgrade2Cost * 1.5);
        cost2.textContent = upgrade2Cost;
        updateDisplay();
      }
    };

    upgrade3.onclick = () => {
      if (points >= upgrade3Cost) {
        points -= upgrade3Cost;
        pointsPerClick *= 2;
        upgrade3Cost = Math.floor(upgrade3Cost * 1.5);
        cost3.textContent = upgrade3Cost;
        updateDisplay();
      }
    };

    upgrade4.onclick = () => {
      if (points >= upgrade4Cost) {
        points -= upgrade4Cost;
        pointsPerClick *= 3;
        upgrade4Cost = Math.floor(upgrade4Cost * 1.5);
        cost4.textContent = upgrade4Cost;
        updateDisplay();
      }
    };

    miningUpgrade.onclick = () => {
      if (points >= miningUpgradeCost) {
        points -= miningUpgradeCost;
        miningMan.style.display = "block";
        setTimeout(() => miningMan.style.display = "none", 5000); // Mining man appears for 5 seconds
        miningUpgradeCost = Math.floor(miningUpgradeCost * 1.5);
        costMining.textContent = miningUpgradeCost;
        updateDisplay();
      }
    };

    // Auto-clicker functionality (for future updates)
    setInterval(() => {
      if (autoClickerActive) {
        points += pointsPerClick;
        updateDisplay();
      }
    }, 1000); // Auto-clicks every second

    // Leaderboard update
    function updateDisplay() {
      pointsDisplay.textContent = points;

      // Update current player score
      players[currentPlayerIndex].score = points;

      // Find top player
      let topPlayer = players.reduce((max, player) => (player.score > max.score ? player : max), players[0]);

      leaderboardDisplay.innerHTML = `<p>Top Player: ${topPlayer.name} - ${topPlayer.score} points</p>`;
    }
  </script>
</body>
</html>
