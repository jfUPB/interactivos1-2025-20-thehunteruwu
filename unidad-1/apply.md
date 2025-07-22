# Unidad 1

## 🛠 Fase: Apply

# Actividad 5

## explica cómo funciona el sistema físico interactivo que acabamos de crear.

### El programa funciona mediante inputs y outputs, lo primero es configurar el microbit, una de las computadoras, a esta le decimos que al presionar un boton (a) presione la tecla A, y mientras que no esté presionada muestre la tecla N.
ahora creamos el programa en p5, lo pirmero es crear el canvas, y configurar la coneccion con el microbit. despues lo que hacemos es crear un rectangulo en el centro, y lo que hacemos basicamente es; Al ejecutar el programa, este limpia todas las entradas, borra toda la informacion, despues le decimos que mientras la tecla N esté presionada pinte el cuadro de verde, recordemos que el sistema muestra la tecla N presionada cuando la tecla A no está presionada. Antes de esto le indicamos al programa que al presionar la tecla A. pinte el rectangulo de rojo, por ende en este caso los imputs del programa serian, conectar el microbit, y lo que pasa al presionar, o no presionar el botón a. Y los ouputs serian conectar el micro bit, limpiar el sistema, pintar el cuadro de verde cuando ninguna tecla esté presionada, y pintar el Rectangulo de rojo cuando la tecla asignada esté presionada.

# Actividad 6
### https://editor.p5js.org/thehunteruwu/sketches/Ny_DbNips
## p5
### Html
```
<!DOCTYPE html>
<html lang="en">
  <head>
    
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.8/lib/p5.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.8/lib/addons/p5.sound.min.js"></script>
    <script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>
    <link rel="stylesheet" type="text/css" href="style.css">
    <meta charset="utf-8" />

  </head>
  <body>
    <main>
    </main>
    <script src="sketch.js"></script>
  </body>
</html>

```
### js
```
let port;
let connectBtn;
let connectionInitialized = false;




function setup() {
  createCanvas(400, 400);
  background(220);

  port = createSerial();

  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);

 
}

function draw() {
  background(220);


  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);

    if (dataRx === "A") {
      x -= 1; 
    } else if (dataRx === "B") {
      x += 1; 
    }
  }

  ellipse(x, y, 50, 50);

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}
```
### .css
```
html, body {
  margin: 0;
  padding: 0;
}
canvas {
  display: block;
}

```
## Micro:Bit

```
from microbit import *

uart.init(baudrate=115200)

while True:

    if button_a.is_pressed():
        uart.write('A')
  

    if button_b.is_pressed():
        uart.write('B')
   

    sleep(100)
```



