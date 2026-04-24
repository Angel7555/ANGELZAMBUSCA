<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Buscaminas</title>
<style>
body {
    background: url('imagen.jpg') no-repeat center center fixed;
    background-size: cover;
    color: white;
    font-family: Arial;
    text-align: center;
    overflow: auto;
}

/* lluvia */
.rain {
    position: fixed;
    width: 2px;
    height: 15px;
    background: rgba(255,255,255,0.3);
    animation: fall linear infinite;
}
@keyframes fall {
    to { transform: translateY(100vh); }
}

#game {
    display: grid;
    gap: 2px;
    justify-content: center;
    margin-top: 20px;
}

.cell {
    width: 25px;
    height: 25px;
    background: rgba(128,128,128,0.9);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    font-size: 12px;
}

.revealed { background: #222; }
.mine { background: red; }

#overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.95);
    color: white;
    display: none;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    font-size: 25px;
}

button, select { margin: 5px; }
</style>
</head>
<body>

<h1>☢ Buscaminas ☢</h1>

<div>
Dificultad:
<select id="difficulty">
<option value="easy">Fácil (5x5)</option>
<option value="medium">Medio (10x10)</option>
<option value="hard">Difícil (20x20)</option>
<option value="extreme">Extremo (40x40)</option>
</select>
<br>
Victorias: <span id="wins">0</span> |
Derrotas: <span id="losses">0</span> |
Clicks: <span id="clicks">0</span>
<br>
<button onclick="initGame()">Reiniciar</button>
</div>

<div id="game"></div>

<div id="overlay">
<div id="message"></div>
<button onclick="closeOverlay()">Reiniciar</button>
</div>

<script>
let size = 5;
let mines = 5;
let board = [];
let revealedCount = 0;
let clicks = 0;
let wins = 0;
let losses = 0;
let gameOver = false;

const game = document.getElementById("game");

function initGame() {
    let diff = document.getElementById("difficulty").value;

    if (diff === "easy") { size = 5; mines = 5; }
    else if (diff === "medium") { size = 10; mines = 20; }
    else if (diff === "hard") { size = 20; mines = 60; }
    else if (diff === "extreme") { size = 40; mines = 300; }

    game.style.gridTemplateColumns = `repeat(${size}, 25px)`;

    board = [];
    game.innerHTML = "";
    revealedCount = 0;
    clicks = 0;
    gameOver = false;
    document.getElementById("clicks").textContent = clicks;

    for (let i = 0; i < size * size; i++) {
        let cell = document.createElement("div");
        cell.classList.add("cell");
        cell.onclick = () => reveal(i);
        game.appendChild(cell);
        board.push({ mine: false, revealed: false, count: 0 });
    }

    let placed = 0;
    while (placed < mines) {
        let i = Math.floor(Math.random() * board.length);
        if (!board[i].mine) {
            board[i].mine = true;
            placed++;
        }
    }

    for (let i = 0; i < board.length; i++) {
        if (board[i].mine) continue;
        let neighbors = getNeighbors(i);
        board[i].count = neighbors.filter(n => board[n].mine).length;
    }

    createRain();
}

function getNeighbors(i) {
    let x = i % size;
    let y = Math.floor(i / size);
    let neighbors = [];

    for (let dx = -1; dx <= 1; dx++) {
        for (let dy = -1; dy <= 1; dy++) {
            if (dx === 0 && dy === 0) continue;
            let nx = x + dx;
            let ny = y + dy;
            if (nx >= 0 && nx < size && ny >= 0 && ny < size) {
                neighbors.push(ny * size + nx);
            }
        }
    }
    return neighbors;
}

function reveal(i) {
    if (gameOver) return;

    let cell = game.children[i];
    let tile = board[i];

    if (tile.revealed) return;

    tile.revealed = true;
    clicks++;
    document.getElementById("clicks").textContent = clicks;

    cell.classList.add("revealed");

    if (tile.mine) {
        cell.classList.add("mine");
        endGame(false);
        return;
    }

    revealedCount++;

    if (tile.count > 0) {
        cell.textContent = tile.count;
    } else {
        getNeighbors(i).forEach(n => {
            if (!board[n].revealed) reveal(n);
        });
    }

    if (revealedCount === size * size - mines) {
        endGame(true);
    }
}

function endGame(win) {
    gameOver = true;

    let overlay = document.getElementById("overlay");
    let message = document.getElementById("message");

    overlay.style.display = "flex";

    if (win) {
        wins++;
        document.getElementById("wins").textContent = wins;
        message.innerHTML = "☢☢☢ 🏅🏅 SOBREVIVISTE A MOSCÚ 🏅🏅 ☢☢☢";
    } else {
        losses++;
        document.getElementById("losses").textContent = losses;
        message.innerHTML = "💣💣💣 EXPLOTASTE Y TE COMIÓ LA RADIACIÓN 💣💣💣";
    }
}

function closeOverlay() {
    document.getElementById("overlay").style.display = "none";
    initGame();
}

function createRain() {
    document.querySelectorAll('.rain').forEach(e => e.remove());
    for (let i = 0; i < 120; i++) {
        let drop = document.createElement('div');
        drop.classList.add('rain');
        drop.style.left = Math.random() * 100 + 'vw';
        drop.style.animationDuration = (Math.random() * 1 + 0.5) + 's';
        document.body.appendChild(drop);
    }
}

initGame();
</script>

</body>
</html>
