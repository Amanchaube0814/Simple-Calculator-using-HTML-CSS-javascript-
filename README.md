# Simple-Calculator-using-HTML-CSS-javascript

HTML

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Basic Calculator</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div class="calculator">
    <input type="text" id="display" readonly />
    <div class="buttons">
      <button onclick="clearDisplay()">C</button>
      <button onclick="append('/')">÷</button>
      <button onclick="append('*')">×</button>
      <button onclick="backspace()">←</button>

      <button onclick="append('7')">7</button>
      <button onclick="append('8')">8</button>
      <button onclick="append('9')">9</button>
      <button onclick="append('-')">−</button>

      <button onclick="append('4')">4</button>
      <button onclick="append('5')">5</button>
      <button onclick="append('6')">6</button>
      <button onclick="append('+')">+</button>

      <button onclick="append('1')">1</button>
      <button onclick="append('2')">2</button>
      <button onclick="append('3')">3</button>
      <button onclick="calculate()">=</button>

      <button onclick="append('0')" class="zero">0</button>
      <button onclick="append('.')">.</button>
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>


CSS

body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: #f4f4f4;
  font-family: 'Segoe UI', sans-serif;
}

.calculator {
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 10px 25px rgba(0,0,0,0.1);
  overflow: hidden;
  width: 320px;
}

#display {
  width: 100%;
  padding: 1rem;
  font-size: 2rem;
  border: none;
  text-align: right;
  background: #222;
  color: #fff;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}

button {
  font-size: 1.5rem;
  padding: 1rem;
  border: 1px solid #ccc;
  background: #f9f9f9;
  cursor: pointer;
  transition: background 0.3s;
}

button:hover {
  background: #e0e0e0;
}

button.zero {
  grid-column: span 2;
}

button:active {
  background: #d4d4d4;
}


JS

const display = document.getElementById("display");

function append(char) {
  display.value += char;
}

function clearDisplay() {
  display.value = "";
}

function backspace() {
  display.value = display.value.slice(0, -1);
}

function calculate() {
  try {
    display.value = eval(display.value.replace(/÷/g, '/').replace(/×/g, '*'));
  } catch {
    display.value = "Error";
  }
}

// Bonus: Keyboard support
document.addEventListener("keydown", (e) => {
  const key = e.key;
  if ("0123456789+-*/.".includes(key)) {
    append(key);
  } else if (key === "Enter") {
    calculate();
  } else if (key === "Backspace") {
    backspace();
  } else if (key.toLowerCase() === "c") {
    clearDisplay();
  }
});
