# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

**1.Describe detalladamente cómo funciona este ejemplo.**

El programa  crea dos píxeles uno en la esquina de arriba y otro en la esquina contraria en la parte de abajo y se encienden y apagan con diferentes intervalos de tiempo, uno con 1 seg y otro con 0.5 seg.

**2.¿Cuáles son los estados en el programa?**
tiene dos estados uno es Init que establece el tiempo inicial y enciende o apaga el píxel según su estado inicial, y el otro es WaitTimeout que espera a que pase el intervalo para alternar el estado del píxel y actualizar la pantalla.

**3.¿Cuáles son los eventos/inputs en el programa?**
El paso del tiempo que se mide mediante utime.ticks_ms(), y utime.ticks_diff()   ue hace que cuando pase el intervalo de tiepo definido se apague o se encienda.

**¿Cuáles son las acciones en el programa?**
Crea los pixeles en su posicion inicial y estado inicial que es apagado y crea cada uno con un intervalo distinto, se configuran los pixeles, y se establece el estado de prendido y apagado y luego se muestran los pixeles en su posicion en el microbit usa los tiks para medir el tiempo que pasa cuando está encendido o apagado y cuando pasa el intervalo de tiempo definido lo apaga o lo enciende.

### Actividad 3

**1.Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.**

se dice por que el programa gestiona varios comportamientos al mismo tiempo sin bloquear la ejecucion.

**2.Identifica los estados, eventos y acciones en el programa.**

Estados: STATE_INIT, STATE_HAPPY, STATE_SMILE, STATE_SAD.
Eventos: El tiempo, muestra algo durante cierta cantidad de tiempo, Cuando se presiona el Boton A.
Accines: Son las imagenes que se muestran en el display, o mejor dicho son el resultado de la accion que pasó, ya sea oprimir el botón A, o el paso del tiempo.

**3.Describe y aplica al menos 3 vectores de prueba para el programa. Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario el sistema puede tener un error.**

<img width="614" height="656" alt="image" src="https://github.com/user-attachments/assets/25b852cf-e4f5-4a59-8add-3e5e035f1d84" />



**MicroBit**


```

from microbit import *
import utime

STATE_INIT = 0
STATE_HAPPY = 1
STATE_SMILE = 2
STATE_SAD = 3

HAPPY_INTERVAL = 1500
SMILE_INTERVAL = 1000
SAD_INTERVAL = 2000

current_state = STATE_INIT
start_time = 0
interval = 0

while True:
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        start_time = utime.ticks_ms()
        interval = HAPPY_INTERVAL
        current_state = STATE_HAPPY

    elif current_state == STATE_HAPPY:
        if button_a.was_pressed():
            display.show(Image.SAD)
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD
        elif utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.SMILE)
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE

    elif current_state == STATE_SMILE:
        if button_a.was_pressed():
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
        elif utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.SAD)
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD

    elif current_state == STATE_SAD:
        if button_a.was_pressed():
            display.show(Image.SMILE)
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
        elif utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY

    sleep(50) 


```
