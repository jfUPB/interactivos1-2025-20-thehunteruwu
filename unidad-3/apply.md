# Unidad 3


## 🛠 Fase: Apply

### Actividad 6

``` py
let state = "CONFIG";
let count = 20;
let lastTick = 0;
let password = ["A", "B", "A"];
let keyInput = [];

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(64);
}

function draw() {
  background(30);
  fill(255);

  if (state === "CONFIG") {
    textSize(20);
    text("Configura con A/B, arma con S", width / 2, 50);
    textSize(64);
    text(count, width / 2, height / 2);
  }
  
  else if (state === "ARMED") {
    textSize(20);
    text("Introduce clave (A,B,A)", width / 2, 50);
    textSize(64);
    text(count, width / 2, height / 2);

    // Tick cada segundo
    if (millis() - lastTick > 1000) {
      lastTick = millis();
      count--;
      if (count <= 0) {
        state = "EXPLODED";
      }
    }
  }

  else if (state === "EXPLODED") {
    textSize(64);
    text("💀", width / 2, height / 2);
    textSize(20);
    text("Presiona T para reiniciar", width / 2, height - 40);
  }
}

function keyPressed() {
  if (state === "CONFIG") {
    if (key === "A") {
      count = min(count + 1, 60);
    } else if (key === "B") {
      count = max(10, count - 1);
    } else if (key === "S") {
      state = "ARMED";
      lastTick = millis();
    }
  }
  
  else if (state === "ARMED") {
    if (key === "A" || key === "B") {
      keyInput.push(key);
      if (keyInput.length === password.length) {
        if (arraysEqual(keyInput, password)) {
          state = "CONFIG";
          count = 20;
        }
        keyInput = []; // reset input
      }
    }
  }
  
  else if (state === "EXPLODED") {
    if (key === "T") {
      state = "CONFIG";
      count = 20;
      keyInput = [];
    }
  }
}

function arraysEqual(a, b) {
  if (a.length !== b.length) return false;
  for (let i = 0; i < a.length; i++) {
    if (a[i] !== b[i]) return false;
  }
  return true;
}
```
