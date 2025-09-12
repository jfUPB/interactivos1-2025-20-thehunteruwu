
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

**¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?**

Formato binario:

Más rápido y eficiente (menos datos).

Difícil de leer y requiere decodificación precisa.

Formato texto ASCII:

Fácil de leer y depurar.

Más lento y usa más ancho de banda.

**Ahora te voy a proponer un experimento que te permitirá ver mejor los datos. Cambia el código del micro:bit por este:**

```.py
# Imports go at the top
from microbit import *
import struct
uart.init(115200)
display.set_pixel(0,0,9)

while True:
    if accelerometer.was_gesture('shake'):
        xValue = accelerometer.get_x()
        yValue = accelerometer.get_y()
        aState = button_a.is_pressed()
        bState = button_b.is_pressed()
        data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
        uart.write(data)
```

<img width="975" height="211" alt="image" src="https://github.com/user-attachments/assets/820a19d9-5492-4f35-bd9b-5f6119817364" />

**Captura el resultado del experimento. ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?**


Se están usando los siguientes tipos de datos:

2h: dos enteros cortos (16 bits cada uno = 2 bytes cada uno) → 2 × 2 = 4 bytes

2B: dos enteros sin signo de 1 byte cada uno → 2 × 1 = 2 bytes

Total: 4 + 2 = 6 bytes por mensaje

**¿Cómo se relaciona esto con el formato '>2h2B'?**

Este formato le dice a struct.pack() cómo convertir los datos a binario:

/>: big-endian (orden de bytes de más significativo a menos significativo)

2h: empaqueta dos valores enteros tipo short (2 bytes cada uno)

2B: empaqueta dos valores tipo unsigned char (1 byte cada uno)

**¿Qué significa cada uno de los bytes que se envían?**

Los 6 bytes enviados representan:

Bytes 0-1: Valor entero de aceleración en X (puede ir de aprox. -2048 a +2048)

Bytes 2-3: Valor entero de aceleración en Y

Byte 4: Estado del botón A:

0 si no está presionado

1 si está presionado

Byte 5: Estado del botón B (igual que el A)

**Recuerda de la unidad anterior que es posible enviar números positivos y negativos para los valores de xValue y yValue. ¿Cómo se verían esos números en el formato '>2h2B'?**

En struct.pack, los valores h (short) se codifican en complemento a dos con 16 bits.

Números positivos (por ejemplo, 500) se codifican como de costumbre:

500 = 0x01F4 → se codifica como: 01 F4

Números negativos (por ejemplo, -300):

-300 en binario complemento a dos de 16 bits = 0xFED4 → se codifica como: FE D4

**Ejemplo:**

```.py
xValue = -500
yValue = -1000
aState = 0
bState = 1

```

Resultado en bytes:

```.py
struct.pack('>2h2B', -500, -1000, 0, 1)
# → b'\xfe\x0c\xfc\x18\x00\x01'

```


| Byte index | Valor   | Significado           |
| ---------- | ------- | --------------------- |
| 0-1        | `FE 0C` | `-500` (x)            |
| 2-3        | `FC 18` | `-1000` (y)           |
| 4          | `00`    | botón A no presionado |
| 5          | `01`    | botón B presionado    |


**Ahora realiza el siguiente experimento para comparar el envío de datos en ASCII y en binario.**
```.py
# Imports go at the top
from microbit import *
import struct
uart.init(115200)
display.set_pixel(0,0,9)

while True:
    if accelerometer.was_gesture('shake'):
        xValue = accelerometer.get_x()
        yValue = accelerometer.get_y()
        aState = button_a.is_pressed()
        bState = button_b.is_pressed()
        data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
        uart.write(data)
        uart.write("ASCII:\n")
        data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
        uart.write(data)
```
**Captura el resultado del experimento. ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?**


<img width="988" height="277" alt="image" src="https://github.com/user-attachments/assets/c1b66b61-99d1-4315-ba90-58daba2174bf" />


**Diferencias entre datos en ASCII y en binario**

| Aspecto                      | Datos en binario                                           | Datos en ASCII                                                                     |
| ---------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **Representación**           | Datos empaquetados en bytes crudos                         | Datos convertidos a texto legible                                                  |
| **Tamaño del mensaje**       | Compacto (6 bytes en este caso)                            | Más largo (varios bytes, depende de la longitud numérica + comas + salto de línea) |
| **Facilidad de lectura**     | No legible para humanos                                    | Legible para humanos                                                               |
| **Procesamiento**            | Necesita decodificación con `struct` u otro método binario | Puede ser parseado como texto, fácil con split y conversiones                      |
| **Velocidad de transmisión** | Más eficiente, menos bytes a enviar                        | Menos eficiente, más bytes transmitidos                                            |


**Ventajas y desventajas de usar formato binario**

**Ventajas:**

Menor tamaño de datos: Los valores numéricos ocupan el tamaño mínimo necesario (ej. 2 bytes para un entero corto).

Transmisión rápida: Menos bytes → menos tiempo en enviar.

Menor uso de ancho de banda: Importante en conexiones lentas o con limitaciones.

Exactitud y precisión: No hay ambigüedad en la representación, no hay que convertir números a texto y luego volver a números.

**Desventajas:**

Difícil de leer: Para un humano no es interpretable sin herramientas específicas.

Necesita procesamiento especial: En el receptor hay que saber exactamente cómo decodificar (estructura y orden de bytes).

Mayor posibilidad de errores sutiles: Si se desincroniza el flujo de datos, puede perderse la referencia a qué byte corresponde a qué dato.


**Ventajas y desventajas de usar formato ASCII (texto)**
 
**Ventajas:**

Legible para humanos: Fácil de visualizar y entender al instante.

Fácil de depurar: Puedes leer datos con un simple terminal serial.

Flexible: El receptor puede interpretar la cadena fácilmente con funciones comunes de texto (split, parse).

No requiere conocimiento exacto de la estructura binaria.

**Desventajas:**

Tamaño más grande: Los números se convierten en caracteres, por ejemplo, el número -300 se transmite como 4 bytes ('-', '3', '0', '0'), más la coma y salto de línea.

Más lento para transmitir: Más bytes → más tiempo y mayor consumo de energía.

Parsing más costoso: Convertir de texto a números implica overhead computacional.

Posibilidad de errores en formato: Si la cadena no está bien formateada, puede haber problemas para parsear.


