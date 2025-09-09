
# Evidencias de la unidad 5
### Actividad 1
**Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?**

El micro:bit envia 4 valores xValue, yValue, aState, bState, 

| Dato     | Descripción                                         | Tipo     |
| -------- | --------------------------------------------------- | -------- |
| `xValue` | Valor del eje X del acelerómetro                    | Entero   |
| `yValue` | Valor del eje Y del acelerómetro                    | Entero   |
| `aState` | `True` si el botón A está presionado, `False` si no | Booleano |
| `bState` | `True` si el botón B está presionado, `False` si no | Booleano |

**¿Cómo es la estructura del protocolo ASCII usado?**

Estructura general de cada mensaje enviado por el Micro:bit:

xValue,yValue,aState,bState\n

xValue: Número entero (puede ser negativo)

yValue: Número entero (puede ser negativo)

aState: True o False (en texto, no booleanos reales)

bState: True o False

\n: Carácter de nueva línea (ASCII 10)

Ejemplo:

-512,970,False,True\n

| Carácter | ASCII decimal |
| -------- | ------------- |
| `-`      | 45            |
| `5`      | 53            |
| `1`      | 49            |
| `2`      | 50            |
| `,`      | 44            |
| ...      | ...           |
| `\n`     | 10            |

**Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.**

```.js

if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    } else {
      print("No se están recibiendo 4 datos del micro:bit");
    }
  }
}

```

| Línea de código                     | ¿Qué hace?                                                                         |
| ----------------------------------- | ---------------------------------------------------------------------------------- |
| `port.availableBytes()`             | Verifica si hay datos nuevos en el puerto serial.                                  |
| `port.readUntil("\n")`              | Lee una línea completa hasta el salto de línea (`\n`).                             |
| `data.trim()`                       | Elimina espacios y saltos de línea al principio/final.                             |
| `data.split(",")`                   | Divide la línea CSV en 4 partes: `[x, y, a, b]`.                                   |
| `int(values[0]) + windowWidth / 2`  | Convierte el valor X del acelerómetro en una coordenada horizontal de la pantalla. |
| `int(values[1]) + windowHeight / 2` | Hace lo mismo con el valor Y para la coordenada vertical.                          |
| `toLowerCase() === "true"`          | Convierte el texto `"True"` o `"False"` en valores booleanos reales.               |
| `updateButtonStates(...)`           | Llama una función que gestiona los eventos de botón.                               |

**¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?**

En la función updateButtonStates(...):

Se compara el estado actual con el anterior.

Si A pasa de false → true, se detecta "A pressed".

Si B pasa de true → false, se detecta "B released".

## Seek: Investigación 

### Actividad 02

**Caso de estudio: micro:bit**
Vamos a transformar el caso de estudio de la unidad anterior para que ahora la comunicación entre el micro:bit y p5.js
se realice mediante un protocolo binario.
Primero analizaremos el código del micro:bit y en la siguiente actividad veremos cómo leer los datos en p5.js.


```.py
# Imports go at the top
from microbit import *
import struct
uart.init(115200)
display.set_pixel(0,0,9)

while True:
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed()
    bState = button_b.is_pressed()
    data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
    uart.write(data)
    sleep(100) # Envia datos a 10 Hz

```
**¿Pero cómo se ven esos datos binarios?**
<img width="972" height="194" alt="image" src="https://github.com/user-attachments/assets/56a7e2fa-a4af-4de3-a529-8c0a730ad017" />

**¿Por qué se ve este resultado?**

Esto se ve así porque ya pasamos de ASCII a binario, por ende toca cambiar el metodo de visualizacion a HEX.

<img width="952" height="159" alt="image" src="https://github.com/user-attachments/assets/fd27c9b1-989a-4b4a-93c0-eeac9f00609f" />

**¿Lo que ves ¿Cómo está relacionado con esta línea de código?**

```.py
data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
```

esta linea de codigo empaqueta los valores en un formato binario
'>2h2B' indica cómo empaquetar los datos:

/>: usa orden de bytes big-endian.

2h: dos números enteros de 2 bytes cada uno (xValue y yValue).

2B: dos números enteros de 1 byte cada uno (los estados aState y bState convertidos a enteros 0 o 1).

