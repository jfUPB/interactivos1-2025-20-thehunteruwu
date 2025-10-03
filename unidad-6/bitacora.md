
# Evidencias de la unidad 6
**¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?**

Instaló Node.js que me permite ejecutar código JavaScript fuera del navegador, principalmente en el servidor.

**¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?**

<img width="567" height="84" alt="image" src="https://github.com/user-attachments/assets/e207fc6a-0648-448e-88c3-e5af6ea41993" />

está corriendo el archivo server.js

**Describe lo que ves inicialmente en page1 y page2 en tu navegador.**

Son dons circulos que están conectados por una linea, y al mover las ventanas en diferentes coordenadas de la pantalla, la pocicion de la linea cambia, porque estos circulos siguen conectados.


**¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?**

<img width="975" height="292" alt="image" src="https://github.com/user-attachments/assets/66aaafe8-9781-4d1a-b190-b7b05a15b830" />


**Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?**

Son dons circulos que están conectados por una linea, y al mover las ventanas en diferentes coordenadas de la pantalla, la pocicion de la linea cambia, porque estos circulos siguen conectados.

<img width="522" height="410" alt="image" src="https://github.com/user-attachments/assets/cbcb4367-2843-41ce-9482-d137c66b3e5e" />


## Seek: Investigación

### Actividad 02

**Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.**

Si se corta la información seguiria en los dispositivos, sin embargo no podria interactuar con el resto de dispositivos, ni enviar nuevos datos desde el mio ni descargarlos.

**¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?**

cuando tanqueo el carro, pido gasolina y me entregan la gasolina, yo seria el cliente y ellos el servidor.

**Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?**



https://www.youtube.com/watch?v=dQw4w9WgXcQ:

Protocolo: https://

Dominio: www.youtube.com

Ruta: /watch?v=dQw4w9WgXcQ

 **¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.youtube.com) sin una ruta específica?**


El navegador accede a la ruta raíz (/) y carga la página principal del sitio.

 **¿Qué “página por defecto” crees que te envía el servidor?**

Normalmente, el servidor envía una página por defecto como index.html, o una ruta equivalente configurada como la página de inicio


**¿Qué similitudes encuentras?**

Ambos protocolos transmiten datos entre dispositivos.

En ambos casos, hay una especie de emisor y receptor.

Usan una estructura de mensajes (aunque HTTP es mucho más detallado).

Ambos pueden funcionar de forma secuencial: se envía un mensaje, se recibe una respuesta.

**¿Qué diferencias clave ves?**

| Característica           | HTTP                                        | Protocolos Seriales (ej. UART con micro:bit) |
| ------------------------ | ------------------------------------------- | -------------------------------------------- |
| **Complejidad**          | Mucho más complejo (usa texto estructurado) | Muy simple (envío directo de bytes)          |
| **Formato**              | Usa encabezados, métodos (GET, POST), etc.  | Solo datos planos (bytes/caracteres)         |
| **Medio de transmisión** | Redes (TCP/IP, Internet)                    | Cable físico (USB, pines TX/RX)              |
| **Dirección y ruta**     | Usa URLs para indicar recursos              | No hay rutas, solo conexión punto a punto    |
| **Aplicación**           | Web, APIs, navegación                       | Comunicación entre dispositivos o sensores   |


**¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?**

Porque HTTP trabaja en entornos más grandes y variables como Internet, donde:

Se necesita saber qué recurso se está pidiendo (URL).

Es importante indicar el tipo de solicitud (ver, enviar, actualizar, etc.).

Hay que incluir metadatos (idioma, formato, autenticación, etc.).

Puede haber muchos clientes y servidores diferentes, por lo que se requiere un estándar universal.

En cambio, en el micro:bit, solo hay comunicación directa y simple, por lo que no es necesario todo ese nivel de estructura.



**Piensa en una página web simple, como un formulario de login.**

**¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?**

**¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?**

**¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?**

**¿Qué parte crees que es HTML?**

Los campos de texto para usuario y contraseña

El botón de "Iniciar sesión"

La estructura general del formulario (etiquetas, títulos, etc.)

HTML define el contenido y estructura de la página.

**¿Qué parte es CSS?**

El color del botón

El tipo y tamaño de letra

La alineación y espaciado del formulario

Los bordes, sombras o estilos visuales en general

CSS se encarga del diseño y apariencia visual.

**¿Qué parte es JavaScript?**

La validación de que escribiste algo antes de enviar

Mostrar un mensaje de “contraseña incorrecta” sin recargar la página

Hacer que el formulario se envíe al servidor y maneje la respuesta

JavaScript controla la interactividad y comportamiento dinámico de la página.

**Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.**

**¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?**

**¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?**

**Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.**

El bucle draw() en p5.js se ejecuta 60 veces por segundo (por defecto), actualizando constantemente la pantalla, aunque nada haya cambiado.
En cambio, en las interfaces web modernas, el modelo basado en eventos (como click, submit, keydown, etc.) espera a que el usuario haga algo antes de reaccionar.

**¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?**

Más eficiente: No consume recursos si no hay interacción.

Menor uso del CPU: No hay un ciclo constante de redibujado.

Mejor rendimiento en dispositivos móviles: Ahorra batería y procesamiento.

Más claro para el desarrollo: Solo se escribe código que responde a acciones específicas del usuario.

**¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?**

No, sería muy ineficiente. Redibujar toda la página constantemente sin necesidad consume mucha memoria y CPU, lo cual puede hacer que el sitio sea lento, especialmente en dispositivos con pocos recursos.

**¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?**

Ventajas para los desarrolladores:

Un solo lenguaje para todo el desarrollo:
No necesitas aprender un lenguaje para el servidor (como PHP o Python) y otro para el navegador. Todo se hace con JavaScript.

Reutilización de código:
Puedes compartir funciones entre el cliente y el servidor (por ejemplo, validaciones de formularios o formatos de fecha).

Mayor productividad:
Los equipos pueden trabajar más rápido y entender mejor el código porque todo está en el mismo lenguaje.

Facilita el desarrollo full-stack:
Un mismo desarrollador puede trabajar tanto en el front-end como en el back-end sin cambiar de lenguaje.

Mejor integración con herramientas modernas:
Muchos frameworks y librerías modernas (como React, Next.js, Express, etc.) funcionan muy bien juntos porque usan JavaScript.





