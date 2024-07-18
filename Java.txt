const player = document.getElementById('player');
const banana = document.getElementById('banana');
const scoreBoard = document.getElementById('scoreBoard');

let score = 0;
let playerX = window.innerWidth / 2;
let playerY = window.innerHeight / 2;
let bananaX = Math.random() * (window.innerWidth - 30);
let bananaY = Math.random() * (window.innerHeight - 30);

banana.style.left = bananaX + 'px';
banana.style.top = bananaY + 'px';

document.addEventListener('keydown', movePlayer);

function movePlayer(event) {
    switch(event.key) {
        case 'ArrowUp':
            playerY -= 20;
            break;
        case 'ArrowDown':
            playerY += 20;
            break;
        case 'ArrowLeft':
            playerX -= 20;
            break;
        case 'ArrowRight':
            playerX += 20;
            break;
    }

    playerX = Math.max(0, Math.min(window.innerWidth - 50, playerX));
    playerY = Math.max(0, Math.min(window.innerHeight - 50, playerY));

    player.style.left = playerX + 'px';
    player.style.top = playerY + 'px';

    checkCollision();
}

function checkCollision() {
    const playerRect = player.getBoundingClientRect();
    const bananaRect = banana.getBoundingClientRect();

    if (playerRect.left < bananaRect.left + bananaRect.width &&
        playerRect.left + playerRect.width > bananaRect.left &&
        playerRect.top < bananaRect.top + bananaRect.height &&
        playerRect.height + playerRect.top > bananaRect.top) {
        score++;
        scoreBoard.textContent = 'Score: ' + score;
        moveBanana();
    }
}

function moveBanana() {
    bananaX = Math.random() * (window.innerWidth - 30);
    bananaY = Math.random() * (window.innerHeight - 30);
    banana.style.left = bananaX + 'px';
    banana.style.top = bananaY + 'px';