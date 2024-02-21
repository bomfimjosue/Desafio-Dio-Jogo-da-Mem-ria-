# Desafio-Dio-Jogo-da-Mem-ria-
Jogo da Memória 
<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Jogo da Memória Emoji</title>
<style>
  /* Estilização básica */
  body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }
  .memory-game {
    display: grid;
    grid-template-columns: repeat(4, 100px);
    gap: 10px;
  }
  .memory-card {
    width: 100px;
    height: 100px;
    background: #f2f2f2;
    border: 1px solid #000;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 50px;
    cursor: pointer;
  }
</style>
</head>
<body>
<div class="memory-game">
  <!-- Adicione as cartas aqui -->
</div>
<script>
</script>
</body>
</html>
document.addEventListener('DOMContentLoaded', () => {
  const memoryGame = document.querySelector('.memory-game');
  const emojis = ['😀', '😃', '😄', '😁', '😆', '😅', '😂', '🤣', '😊', '😇'];
  let hasFlippedCard = false;
  let firstCard, secondCard;
  const emojiPairs = [...emojis, ...emojis];
  const shuffle = array => {
  for (let i = array.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
};
  shuffle(emojiPairs);
  const createCard = emoji => {
  const card = document.createElement('div');
  const emojiSpan = document.createElement('span');
  emojiSpan.textContent = emoji;
  card.classList.add('memory-card');
  card.dataset.emoji = emoji;
  card.appendChild(emojiSpan);
  card.addEventListener('click', flipCard);
  memoryGame.appendChild(card);
};
  emojiPairs.forEach(emoji => {
    createCard(emoji);
  });
  function flipCard() {
    this.classList.add('flip');
    if (!hasFlippedCard) {
      hasFlippedCard = true;
      firstCard = this;
      return;
    }
    secondCard = this;
    checkForMatch();
  }
  const checkForMatch = () => {
    let isMatch = firstCard.dataset.emoji === secondCard.dataset.emoji;
    isMatch ? disableCards() : unflipCards();
  };
  const disableCards = () => {
    firstCard.removeEventListener('click', flipCard);
    secondCard.removeEventListener('click', flipCard);
    resetBoard();
  };
  const unflipCards = () => {
    setTimeout(() => {
      firstCard.classList.remove('flip');
      secondCard.classList.remove('flip');
      resetBoard();
    }, 1500);
  };
  const resetBoard = () => {
    [hasFlippedCard, firstCard, secondCard] = [false, null, null];
  };
});
.flip {
  transform: rotateY(180deg);
}
.memory-card::before {
  content: attr(data-emoji);
}                     .memory-card {
  transition: transform 0.5s;
  transform-style: preserve-3d;
}            .memory-card {
  transition: transform 0.5s, box-shadow 0.5s;
}
.memory-card.flip {
  transform: rotateY(180deg);                  box-shadow: 0 5px 15px rgba(0,0,0,0.5);
}
.memory-card::before, .memory-card::after {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
}
.memory-card::before {
  content: attr(data-emoji);
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f2f2f2;
}
.memory-card::after {
  content: '';
  background: #000;
  transform: rotateY(180deg);
}          
let moves = 0;
const movesCounter = document.querySelector('.moves-counter');
function incrementMoves() {
  moves++;
  movesCounter.textContent = `Movimentos: ${moves}`;
}                
let time = 0;
let timer;

const timerDisplay = document.createElement('div');
timerDisplay.classList.add('timer');
document.body.insertBefore(timerDisplay, document.body.firstChild);
// Inicie o temporizador quando o primeiro cartão for virado
function flipCard() {
  if (!hasFlippedCard) {
    hasFlippedCard = true;
    firstCard = this;
    startTimer(); // Inicia o temporizador
    return;
  }
  // Restante da função flipCard...
}

// Pare o temporizador quando o jogo terminar
const checkEndOfGame = () => {
  const allFlipped = [...document.querySelectorAll('.memory-card')]
    .every(card => card.classList.contains('flip'));
  if (allFlipped) {
    stopTimer(); // Para o temporizador
    alert('Parabéns, você encontrou todos os pares!');
  }
};

function startTimer() {
  timer = setInterval(() => {
    time++;
    timerDisplay.textContent = `Tempo: ${time} segundos`;
  }, 1000);
}

function stopTimer() {
  clearInterval(timer);
}

let time = 0;
const timerDisplay = document.querySelector('.timer');
let moves = 0;
const movesCounter = document.createElement('div');
movesCounter.classList.add('moves-counter');
document.body.insertBefore(movesCounter, document.body.firstChild);

function incrementMoves() {
  moves++;
  movesCounter.textContent = `Movimentos: ${moves}`;
}

// Lembre-se de chamar incrementMoves dentro da função flipCard

function startTimer() {
  setInterval(() => 
const checkEndOfGame = () => {
  const allFlipped = [...document.querySelectorAll('.memory-card')]
    .every(card => card.classList.contains('flip'));
  if (allFlipped) {
    alert('Parabéns, você encontrou todos os pares!');
  }
};                
const disableCards = () => {
  firstCard.removeEventListener('click', flipCard);
  secondCard.removeEventListener('click', flipCard);
  resetBoard();
  checkEndOfGame();
