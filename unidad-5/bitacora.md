
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
