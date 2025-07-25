# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

#### ¿Qué es un sistema físico interactivo?
Es un sistema que funciona mediante inputs y outputs, mediante los inputs generas una orden, y el output genera un resultado, todo esto usando medios tecnologicos.

#### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

Siempre me gustó el tema de los visuales en la musica, ahora me gustaria explorar ese tema junto con poder hacer interactivos esos visuales, o un sistema de visuales que se generen automaticamente.

### Actividad 02

#### ¿Qué es el diseño y el arte generativos?

El diseño y el arte generativo, lo interpreto como un producto, un programa, osea un conjunto de reglas que haces para crear algo, la cuestion está en que estas reglas tienen que estár hechas para que el programa sea autonomo, osea que, yo le doy la orden de lo que quiero pero el programa debe darme un resultado unico, dieferente, basicamente  se crea un sistema automatizado donde yo le digo que quiero algo que cumpla ciertas caracteristicas, pero no le digo cual va a ser el resultado final, por ende el programa tiene un grado de independencia.

#### La diferenecia entre el arte y el diseño, 

Es que el arte esta hecho para expresar las ideas del artista, las ideas del que crea el programa. en cambio el diseño está para satisfacer a un cliente, a alguien más, está para cumplir con las ideas de otro.

### Actividad 03
<img width="545" height="894" alt="image" src="https://github.com/user-attachments/assets/b7465cb2-dfe1-439d-afba-d138a1c83be9" />.

Presiona los botones A y B del micro:bit.

<img width="406" height="397" alt="image" src="https://github.com/user-attachments/assets/ec54e74a-b438-46db-b14d-3573597a81a4" />.

<img width="401" height="390" alt="image" src="https://github.com/user-attachments/assets/b9260e2b-363a-40e3-a622-cfc5fcc3169c" />.

Sacude el micro:bit. ¿Qué pasa?

<img width="389" height="393" alt="image" src="https://github.com/user-attachments/assets/b2bfd105-def7-4472-88e5-84c5968e8ad7" />.

Presiona el botón Send Love. ¿Qué pasa?
pone un corazon y una carita feliz

### Actividad 04
Escribe el enlace a tu programa en el editor de p5.js.  
https://editor.p5js.org/thehunteruwu/sketches/F64bFZk83

index.html

``` html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Patrones Visuales Aleatorios</title>
  <link rel="stylesheet" href="style.css">
  <!-- Cargar la librería p5.js -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
  <script src="sketch.js" defer></script>
</head>
<body>
  <main>

  </main>
</body>
</html>
 ```
Sketch.js

``` js
function setup() {
  createCanvas(800, 800);
  noStroke();
  frameRate(12); 
}

function draw() {
  background(20, 20, 30, 50);
  let t = frameCount * 0.05;
  let numShapes = int(random(5, 20));

  for (let i = 0; i < numShapes; i++) {
    let angle = random(TWO_PI);
    let radius = random(50, 250);
    let x = width / 2 + radius * cos(angle + t);
    let y = height / 2 + radius * sin(angle - t);

    let size = random(10, 80);
    let r = 100 + 155 * sin(t + i);
    let g = 100 + 155 * sin(t + i * 2);
    let b = 100 + 155 * cos(t + i * 3);

    fill(r, g, b, 150);
    ellipse(x, y, size, size);
  }
}
```
style.js

``` js
body {
  margin: 0;
  padding: 0;
  background-color: #111;
  color: white;
  font-family: 'Arial', sans-serif;
  text-align: center;
}

main {
  padding-top: 20px;
}

canvas {
  display: block;
  margin: 0 auto;
  border: 2px solid white;
}
```

<img width="1106" height="750" alt="image" src="https://github.com/user-attachments/assets/c704fa87-1377-4a9d-b244-e256cbe3f893" />

<img width="688" height="664" alt="image" src="https://github.com/user-attachments/assets/55d6fdc2-eb9a-4b33-8c71-16a2037d605b" />
<img width="660" height="668" alt="image" src="https://github.com/user-attachments/assets/56893e51-2cbe-4416-85f7-3cc6ed0823ea" />
