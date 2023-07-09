<!DOCTYPE html>
<html>
<head>
  <title>Rock Paper Scissors</title>
</head>
<body>
  <h1>Rock Paper Scissors</h1>

  <div id="score"></div>
  <div id="result"></div>

  <button id="rock">Rock</button>
  <button id="paper">Paper</button>
  <button id="scissors">Scissors</button>

  <script>
    // Initialize score and selections
    let playerScore = 0;
    let computerScore = 0;

    // DOM elements
    const scoreDisplay = document.getElementById('score');
    const resultDisplay = document.getElementById('result');
    const rockBtn = document.getElementById('rock');
    const paperBtn = document.getElementById('paper');
    const scissorsBtn = document.getElementById('scissors');

    // Event listeners for buttons
    rockBtn.addEventListener('click', () => playRound('rock'));
    paperBtn.addEventListener('click', () => playRound('paper'));
    scissorsBtn.addEventListener('click', () => playRound('scissors'));

    // Play a round
    function playRound(playerSelection) {
      const computerSelection = computerPlay();
      const result = determineWinner(playerSelection, computerSelection);
      updateScore(result);

      // Display result and score
      resultDisplay.textContent = result;
      scoreDisplay.textContent = `Player: ${playerScore} - Computer: ${computerScore}`;

      // Check if a player has won
      if (playerScore === 5 || computerScore === 5) {
        announceWinner();
        resetGame();
      }
    }

    // Generate computer's move
    function computerPlay() {
      const moves = ['rock', 'paper', 'scissors'];
      return moves[Math.floor(Math.random() * 3)];
    }

    // Determine the winner of the round
    function determineWinner(playerSelection, computerSelection) {
      if (playerSelection === computerSelection) {
        return "It's a tie!";
      } else if (
        (playerSelection === 'rock' && computerSelection === 'scissors') ||
        (playerSelection === 'scissors' && computerSelection === 'paper') ||
        (playerSelection === 'paper' && computerSelection === 'rock')
      ) {
        return 'You win!';
      } else {
        return 'Computer wins!';
      }
    }

    // Update the score based on the round result
    function updateScore(result) {
      if (result === 'You win!') {
        playerScore++;
      } else if (result === 'Computer wins!') {
        computerScore++;
      }
    }

    // Announce the winner of the game
    function announceWinner() {
      if (playerScore === 5) {
        resultDisplay.textContent = 'Congratulations! You won the game!';
      } else if (computerScore === 5) {
        resultDisplay.textContent = 'Oops! Computer won the game!';
      }
    }

    // Reset the game after a player wins
    function resetGame() {
      playerScore = 0;
      computerScore = 0;
      scoreDisplay.textContent = '';
    }
  </script>
</body>
</html>
