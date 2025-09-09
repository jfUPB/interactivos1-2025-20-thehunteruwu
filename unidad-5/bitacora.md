
# Evidencias de la unidad 5
## Actividad 1
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



