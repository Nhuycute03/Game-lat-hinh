# Game-lat-hinh
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Game Lật Hình</title>
  <style>
    body {
      font-family: Arial;
      background: #f0f0f0;
      text-align: center;
      padding-top: 30px;
    }
    h1 { color: #333; }
    .game-board {
      width: 360px;
      margin: auto;
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }
    .card {
      width: 80px;
      height: 80px;
      background: #666;
      border-radius: 8px;
      cursor: pointer;
      color: white;
      font-size: 36px;
      line-height: 80px;
      user-select: none;
    }
    .matched {
      background: #2ecc71;
      cursor: default;
    }
  </style>
</head>
<body>
  <h1>Game Lật Hình</h1>
  <div class="game-board" id="board"></div>

  <script>
    const emojis = ['🍎', '🍌', '🍇', '🍉'];
    let cards = [...emojis, ...emojis].sort(() => 0.5 - Math.random());

    const board = document.getElementById('board');
    let flipped = [];
    let lock = false;

    cards.forEach((emoji, i) => {
      const card = document.createElement('div');
      card.className = 'card';
      card.dataset.emoji = emoji;
      card.dataset.index = i;
      card.innerText = '';
      card.onclick = () => {
        if (lock || card.classList.contains('matched') || flipped.includes(card)) return;
        card.innerText = card.dataset.emoji;
        flipped.push(card);
        if (flipped.length === 2) {
          lock = true;
          setTimeout(() => {
            if (flipped[0].dataset.emoji === flipped[1].dataset.emoji) {
              flipped[0].classList.add('matched');
              flipped[1].classList.add('matched');
            } else {
              flipped[0].innerText = '';
              flipped[1].innerText = '';
            }
            flipped = [];
            lock = false;
          }, 800);
        }
      };
      board.appendChild(card);
    });
  </script>
</body>
</html>
