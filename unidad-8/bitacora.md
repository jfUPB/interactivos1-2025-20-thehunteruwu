
# Evidencias de la unidad 8


## Seek: Investigación

### Actividad 01

**Link repo**

https://github.com/thehunteruwu/Visuales_jazz_final


**Link Video**
https://youtube.com/shorts/CDG3orDWeNs?si=pQyp9GNUQI6Ro9n8

<img width="734" height="408" alt="image" src="https://github.com/user-attachments/assets/21b794fd-02ea-4cb9-b204-b11a8fd930a0" />


<img width="758" height="454" alt="image" src="https://github.com/user-attachments/assets/71823318-a5a5-40ba-bb97-427e0c68f93d" />


<img width="699" height="461" alt="image" src="https://github.com/user-attachments/assets/cb672f1b-d3bb-4742-84f7-09cbf99d8239" />


<img width="542" height="222" alt="image" src="https://github.com/user-attachments/assets/1aa89dfd-4e0c-45be-9dfb-1eb9247dc5d7" />

La app fucniona de la siguiente manera, primero creamos una app movil y una desktop, en la desktop se reproduce una cancion y muestra los visuales, los visuales estan basadosen rattatuille y lalaland, en la app movil lo que hace es que cambia el estilo del visual, desde la interfaz del desktop aparecen los botones para limpiar el canvas, reproducir, la musica y conectar el micro:bit, el codigo del microbit fue hecho con ia, lo que hace es que al oprimir el boton "a" el pincel queda en estado true, y para evidenciar que está funcionando en el display del microbit aparece una nota musical, despues con el sensor del microbit toma las coordenadas x, y, y pinta en esas coordenadas, el codigo tambien está hecho para que los colores cambien según una paleta de colores que yo le proporcione.

todo el codigo fue hecho con ia, sin embargo yo le proporcione la estructura del codigo los componentes como los visuales los colores la musica.

# 📡 Cómo Funciona el Sistema

## 🎯 Resumen Simple

Este proyecto conecta 3 cosas:
1. **micro:bit** - Para dibujar moviendo el dispositivo
2. **Pantalla (Desktop)** - Donde se ven las manchas de colores
3. **Móvil** - Para cambiar el estilo de las manchas

```
        micro:bit                    Pantalla                    Móvil
           │                            │                          │
           │─── Cable USB ─────────────▶│                          │
           │    (envía X, Y)            │                          │
           │                            │◀─── Internet ───────────│
           │                            │    (cambia estilo)       │
           │                            │                          │
```

## 🔄 Cómo se Comunican

### 1️⃣ micro:bit → Pantalla (Cable USB)

**¿Qué hace?**
- Presionas el botón A → Se activa el pincel 🎵
- Mueves el micro:bit → Envía la posición X, Y
- La pantalla recibe los datos y dibuja manchas

**Flujo:**
```
micro:bit                      Pantalla
────────                       ────────

Presionar Botón A
    │
    ▼
Activar pincel 🎵
    │
    ▼
Leer movimiento
X: 50, Y: 75
    │
    ▼
Enviar por USB ──────────────▶ Recibir posición
"50,75"                            │
                                   ▼
                              Dibujar mancha
                              en (50, 75)
```

### 2️⃣ Móvil → Pantalla (Internet)

**¿Qué hace?**
- Tocas un botón en el móvil (ej: "Explosiones 💥")
- El servidor recibe el cambio
- Todas las pantallas conectadas cambian al nuevo estilo

**Flujo:**
```
Móvil                 Servidor              Pantalla
─────                 ────────              ────────

Tocar "Explosiones"
     │
     ▼
Enviar cambio ──────▶ Recibir
                           │
                           ▼
                      Avisar a todos ────▶ Cambiar estilo
                                          a "Explosiones"
```

### 3️⃣ Música → Colores (Automático)

**¿Qué hace?**
- La música suena en la pantalla
- Cuando hay graves fuertes (beats) → Cambia de color
- Los colores rotan: Púrpura oscuro → Púrpura → Amarillo

**Flujo:**
```
Música                    Pantalla
──────                    ────────

"City of Stars"
     │
     ▼
Analizar sonido
     │
     ▼
¿Hay graves fuertes? ────▶ SÍ → Cambiar al siguiente color
     │                         Púrpura → Amarillo → Púrpura
     ▼
Aplicar color a las manchas
```

## 🎨 Los 4 Estilos

Puedes elegir cómo se ven las manchas desde el móvil:

| Estilo | Nombre | ¿Cómo se ve? |
|--------|--------|--------------|
| ⚪ | Manchas Circulares | Círculos suaves con degradado |
| 💫 | Manchas Dispersas | Muchas gotas pequeñas alrededor |
| 🖌️ | Pinceladas Orgánicas | Líneas curvas como pintura |
| 💥 | Explosiones de Color | Rayos que salen desde el centro |

## 🎨 Paleta de Colores

Los colores cambian automáticamente con la música:

- 🟣 **Púrpura muy oscuro** - Música suave
- 🟣 **Púrpura oscuro** - Música media
- 🟣 **Púrpura** - Música fuerte
- 🟡 **Amarillo** - Beats intensos

## 🔌 Conexiones

```
                    ┌──────────────┐
                    │  micro:bit   │
                    │   (Botón A)  │
                    └──────┬───────┘
                           │
                      Cable USB
                           │
                           ▼
              ┌────────────────────────┐
              │  Pantalla (Desktop)    │
              │  - Recibe movimientos  │
              │  - Reproduce música    │
              │  - Dibuja manchas      │
              └─────────┬──────────────┘
                        │
                   Internet
                   (Servidor)
                        │
                        ▼
              ┌────────────────────────┐
              │  Móvil (Smartphone)    │
              │  - 4 botones           │
              │  - Ver estado          │
              └────────────────────────┘
```


1. **Conectas el micro:bit** al PC con USB
2. **Abres la pantalla** en el navegador (Desktop)
3. **Abres el móvil** en tu teléfono
4. **Presionas botón A** en el micro:bit → Aparece 🎵
5. **Mueves el micro:bit** → Se dibuja en la pantalla
6. **Tocas botones en el móvil** → Cambia el estilo
7. **La música suena** → Los colores cambian solos


**AutoEvaluacion**

Actividad 1: 5

la estructura está completa y está explicada detalladamente, tiene las referencias utilizadas.

Actividad 2: 5

La app es completamente funcional, integré todos los elementos requeridos, y la app sigue la estructura planteada.

