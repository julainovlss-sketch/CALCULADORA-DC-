# CALCULADORA-DC-calculadora/
├── index.html
├── style.css
├── script.js
├── manifest.json (para instalar como app)
├── service-worker.js (modo offline)<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Calculadora Inteligente</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <header>
    <h1>Calculadora Inteligente</h1>
    <button id="toggle-theme">🌙</button>
  </header>

  <main>
    <div class="calculator">
      <input type="text" id="display" readonly />
      <div class="buttons">
        <!-- Botões numéricos e operadores -->
        <button>7</button><button>8</button><button>9</button><button>/</button>
        <button>4</button><button>5</button><button>6</button><button>*</button>
        <button>1</button><button>2</button><button>3</button><button>-</button>
        <button>0</button><button>.</button><button>=</button><button>+</button>
        <button id="clear">C</button>
      </div>
    </div>

    <section id="history">
      <h2>Histórico</h2>
      <ul id="history-list"></ul>
    </section>
  </main>

  <footer>
    <p>Feito por Juliano © 2025</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>body {
  font-family: 'Segoe UI', sans-serif;
  margin: 0;
  background: #f0f0f0;
  color: #333;
  transition: background 0.3s, color 0.3s;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background: #6200ea;
  color: white;
}

.calculator {
  max-width: 300px;
  margin: 2rem auto;
  padding: 1rem;
  background: white;
  border-radius: 10px;
  box-shadow: 0 0 10px #ccc;
}

#display {
  width: 100%;
  height: 40px;
  font-size: 1.5rem;
  margin-bottom: 1rem;
  text-align: right;
  padding: 0.5rem;
}

.buttons button {
  width: 23%;
  margin: 1%;
  height: 50px;
  font-size: 1.2rem;
  cursor: pointer;
}

#history {
  max-width: 300px;
  margin: 2rem auto;
}

.dark-mode {
  background: #121212;
  color: #eee;
}

.dark-mode .calculator {
  background: #1e1e1e;
  box-shadow: none;
}

footer {
  text-align: center;
  padding: 1rem;
  background: #eee;
}const display = document.getElementById('display');
const buttons = document.querySelectorAll('.buttons button');
const historyList = document.getElementById('history-list');
const clearBtn = document.getElementById('clear');
const themeToggle = document.getElementById('toggle-theme');

let history = [];

buttons.forEach(btn => {
  btn.addEventListener('click', () => {
    const value = btn.textContent;
    if (value === '=') {
      try {
        const result = eval(display.value);
        history.push(`${display.value} = ${result}`);
        updateHistory();
        display.value = result;
      } catch {
        display.value = 'Erro';
      }
    } else if (value === 'C') {
      display.value = '';
    } else {
      display.value += value;
    }
  });
});

function updateHistory() {
  historyList.innerHTML = '';
  history.slice(-5).forEach(item => {
    const li = document.createElement('li');
    li.textContent = item;
    historyList.appendChild(li);
  });
}

themeToggle.addEventListener('click', () => {
  document.body.classList.toggle('dark-mode');
});
