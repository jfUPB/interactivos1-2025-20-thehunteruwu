# Unidad 1

## 🤔 Fase: Reflect
### Actividad 07
#### Autoevaluación
#### Parte 1: recuperación de conocimiento (Retrieval Practice)
 *1.Basándote en los ejemplos que vimos de sistemas físicos interactivos al iniciar el curso, describe las tres características que definen a un sistema físico interactivo.*
R/ Es un programa, un conjunto de reglas, que mediante inputs(ordenes que le entrego al programa) genera un output(el resultado de la orden que le dí).
 *2.Explica el modelo input-process-output de Patrick Hübner usando como ejemplo el sistema que construiste con micro:bit y p5.js en la Actividad 06. ¿Cuál fue el input, cuál fue el proceso y cuál fue el output?*
R/ Primero hay que configurar el microbit que es una de las computadoras, y para que la configuramos?, configuramos los botones, ponemos que al oprimir un botón presione cierta tecla, en este caso el input seria presinar el boton, y el output seria en la consola cuando nos muestra la tecla que presionamos, pero esto solo es la configuracion de la computadora, despues creamos el programa que es el que realmente nos muestra el output, en el programa creamos una bolita, que cuando detecte la tecla a se mueve a la izquierda, y cuando detecta la tecla b, se mueve a la derecha. Entonces el intput en este caso seria oprimir los botones, y el output seria el movimiento de la bolita.
*3.¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?*
la funcion de la linea uart.write('A') es mandar al computador conectado con el microbit la letra A, en este caso al oprimir el boton a, manda la letra A al computador, y en p5.js la funcion que se encarga de escuchar la orden es dataRx, que lee lo que se ingresa.
