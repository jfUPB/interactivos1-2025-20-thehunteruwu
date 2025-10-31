
# Evidencias de la unidad 7

## Actividad 2

**Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?**

Dev Tunnels es una herramienta que permite exponer una aplicación que corre localmente a internet mediante una URL.

**Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.**

Es una función que se ejecuta cada vez que el usuario mueve el dedo por la pantalla en dispositivos móviles.

La variable threshold se usa para evitar enviar demasiados eventos insignificantes o muy pequeños. Por ejemplo:

Si el dedo se mueve solo 1 píxel, eso puede generar un evento touchMoved(), pero es tan pequeño que no vale la pena enviarlo.

Entonces, con un threshold (por ejemplo, 5 píxeles), solo se ejecuta cierta lógica cuando el movimiento del dedo supera ese valor.

**Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?**

| **Característica**               | **Dev Tunnels**                                         | **IP Local**                                       |
| -------------------------------- | ------------------------------------------------------- | -------------------------------------------------- |
| **Acceso desde fuera de la red** | ✔️ Sí, permite acceso desde cualquier red               | ❌ No, solo dentro de la misma red local            |
| **Facilidad de configuración**   | ✔️ Fácil, solo necesitas iniciar el túnel               | ⚠️ Puede requerir configurar firewalls o puertos   |
| **Estabilidad/Velocidad**        | ⚠️ Puede tener algo de latencia por el túnel            | ✔️ Muy rápida y estable en red local               |
| **Seguridad**                    | ✔️ Conexiones cifradas                                  | ⚠️ Depende de la red local, puede ser menos segura |
| **URL persistente**              | ❌ No, cambia cada vez (a menos que pagues por una fija) | ✔️ La IP local no cambia si estás en la misma red  |

<img width="609" height="465" alt="image" src="https://github.com/user-attachments/assets/db25c174-ebb9-4b50-a6bc-cac30fb03a60" />


<img width="352" height="763" alt="image" src="https://github.com/user-attachments/assets/33d60667-5fe4-4827-8338-d0fc37df96eb" />

## Actividad 03

**¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …)**

express.static('public') permite servir archivos estáticos (como HTML, CSS, JS, imágenes, etc.) de forma automática desde una carpeta específica (por ejemplo, public). No necesitas definir rutas para cada archivo, ya que Express se encarga de buscarlos y entregarlos directamente al navegador. Es muy práctico y eficiente cuando se trata de mostrar contenido del frontend que no cambia dinámicamente.

app.get('/ruta', ...) se usa cuando necesitas definir rutas específicas y personalizadas. Te permite tener control total sobre qué datos o archivos se envían como respuesta. Es ideal para manejar peticiones dinámicas, APIs, lógica del servidor o para enviar archivos bajo ciertas condiciones.


**Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?**

En el cliente móvil (HTML + JS), normalmente se captura el movimiento del dedo con una función como touchMoved() (por ejemplo, en p5.js) o con eventos como touchmove en JavaScript.

Dentro de esa función, se emite un evento a través de Socket.IO al servidor:

```.js
socket.emit('message', { x: touchX, y: touchY });
```
Evento enviado: 'message'

Contenido del mensaje: posición táctil { x, y }

Destino: el servidor

**¿Qué evento lo recibe el servidor?**

En el servidor Node.js, se tiene el siguiente código:

```.js
socket.on('message', (message) => {
    console.log('Received message =>', message);
    socket.broadcast.emit('message', message);
});


```

Evento que escucha: 'message'

Qué hace:

Imprime el mensaje en la terminal del servidor.

Luego lo reenvía a otros clientes usando socket.broadcast.emit.


**¿Qué hace el servidor con el mensaje?**

El servidor actúa como intermediario:

Recibe el mensaje táctil de un cliente móvil.

No lo guarda ni lo procesa (en este caso).

Lo transmite a todos los demás clientes conectados, excepto al que lo envió.

Esto evita que el mismo móvil reciba su propio mensaje de vuelta.

**¿Qué evento lo envía el servidor al escritorio?**

El servidor usa:

```.js
socket.broadcast.emit('message', message);


```
Esto reenvía el evento 'message' a todos los demás clientes, incluyendo el escritorio si está conectado, pero no al móvil que lo envió.

En el cliente de escritorio, se escucha ese evento así:

```.js
socket.on('message', (data) => {
    // Usar data.x y data.y para mover algo, por ejemplo
});


```


**Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?**

Los otros escritorios sí lo reciben.

El móvil no, porque él ya tiene la información local (por ejemplo, su propia posición táctil) y no necesita recibir su propio mensaje.

Este método envía el mensaje a todos los clientes conectados, excepto al socket que originó el mensaje (en este caso, el móvil).

**¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?**

Confirmación de nuevas conexiones

Ver mensajes recibidos desde los clientes

Detección de desconexiones

## Actividad 04
```
[1] Usuario toca en el móvil (x=120, y=250)
        |
        | touchMoved() detecta movimiento
        V
📱 MÓVIL
--------------------------------------------------
socket.emit('message', { x:120, y:250, type:'touch' })
        |
        |  ➡️ Envío del mensaje al servidor
        V
🌐 SERVIDOR (Node.js + Socket.IO)
--------------------------------------------------
socket.on('message', data) → recibe: { x:120, y:250, type:'touch' }
        |
        |  ➡️ Reenvía a todos los clientes menos al emisor
        V
socket.broadcast.emit('message', { x:120, y:250, type:'touch' })
        |
        |  
        |  📤 ENVÍO A TODOS LOS CLIENTES CONECTADOS (excepto móvil)
        V
🖥️ ESCRITORIO
--------------------------------------------------
socket.on('message', data)
→ Verifica que data.type === 'touch'
→ Actualiza posición del círculo:
   circleX = 120;
   circleY = 250;

🎯 CÍRCULO ROJO SE MUEVE A ESA POSICIÓN EN PANTALLA
```
## Apply: Aplicación

<img width="1255" height="818" alt="image" src="https://github.com/user-attachments/assets/f4cfdca4-0bf6-423b-bf5a-b6bcb8b6b08b" />

<img width="784" height="930" alt="image" src="https://github.com/user-attachments/assets/3983aaa6-0f67-4b7a-8730-89f5b5d6b778" />


https://github.com/thehunteruwu/visuales


Auto Evaluación: 5

Actividad 1: 5

Actividad 2: 5

Actividad 3: 5

Actividad 4: 5

Actividad 5: 5
