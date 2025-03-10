#### codigo python 
```py
from microbit import *
import utime
import music

STATE_INICIO = 0
STATE_ARMADO = 1
STATE_EXPLOTA = 2

countdown_time = 20
min_time = 10
max_time = 60
current_state = STATE_INICIO

seq_passWord = ["A", "B", "A", "S"]
seq_user = []

start_time = 0
last_time_displayed = -1
event_occurred = False
event = ""

def update_display(time_left):
    display.show(str(time_left))

def explode():
    music.play(music.BA_DING)

def tareaEventos():
    global event_occurred, event
    if button_a.was_pressed():
        event = 'A'
        event_occurred = True

    if button_b.was_pressed():
        event = 'B'
        event_occurred = True

    if accelerometer.was_gesture("shake"):
        event = 'S'
        event_occurred = True

    if uart.any():
        message = uart.read()
        if message:
            message = message.decode('utf-8').strip()
            if message:
                event = message
                event_occurred = True

def tareaBomba():
    global current_state, start_time, seq_user, countdown_time, last_time_displayed, event_occurred, event

    if current_state == STATE_INICIO:
        update_display(countdown_time)

        if event_occurred:
            if event == 'A' and countdown_time < max_time:
                countdown_time += 1
                update_display(countdown_time)
            elif event == 'B' and countdown_time > min_time:
                countdown_time -= 1
                update_display(countdown_time)
            elif event == 'S':
                start_time = utime.ticks_ms()
                seq_user = []
                current_state = STATE_ARMADO

            event_occurred = False  # Consumir el evento

    elif current_state == STATE_ARMADO:
        time_left = max(0, countdown_time - (utime.ticks_diff(utime.ticks_ms(), start_time) // 1000))

        if time_left != last_time_displayed:
            update_display(time_left)
            last_time_displayed = time_left

        if time_left == 0:
            explode()
            display.show("BOOM!")
            current_state = STATE_EXPLOTA

        if event_occurred:
            if event == 'A':
                seq_user.append("A")
            elif event == 'B':
                seq_user.append("B")
            elif event == 'S':
                seq_user.append("S")
                if seq_user == seq_passWord:
                    current_state = STATE_INICIO
                    countdown_time = 20
                    update_display(countdown_time)
                    music.play(music.BADDY)
                else:
                    seq_user = []

            event_occurred = False  # Consumir el evento

    elif current_state == STATE_EXPLOTA:
        explode()
        if pin_logo.is_touched() or event == 'T':
            current_state = STATE_INICIO
            countdown_time = 20
            update_display(countdown_time)
        while True:
            if uart.any():
                message = uart.read()
                if message:
                    message = message.decode('utf-8').strip()
                    if message == 'T':
                        current_state = STATE_INICIO
                        countdown_time = 20
                        update_display(countdown_time)

while True:
    tareaEventos()
    tareaBomba()

```

#### codigo html
```html
<!DOCTYPE html>
<html>
<head>
    <title>Micro:bit Control</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js"></script>
    <script src="https://unpkg.com/@serialport/browser"></script>
    <script src="sketch.js"></script>
</head>
<body>
    <button id="connect">Connect</button>
    <button id="sendA">Send A</button>
    <button id="sendB">Send B</button>
    <button id="sendS">Send S</button>
    <button id="sendT">Send T</button> <!-- Botón Send T -->
</body>
</html>


```


#### codigo sketch
```js
let port;
let writer;
let encoder = new TextEncoder();

function setup() {
    noCanvas();

    document.getElementById('connect').addEventListener('click', async () => {
        try {
            port = await navigator.serial.requestPort();
            await port.open({ baudRate: 9600 });
            writer = port.writable.getWriter();
        } catch (error) {
            console.log('Error connecting to the serial port: ', error);
        }
    });

    document.getElementById('sendA').addEventListener('click', () => {
        sendData('A');
    });

    document.getElementById('sendB').addEventListener('click', () => {
        sendData('B');
    });

    document.getElementById('sendS').addEventListener('click', () => {
        sendData('S');
    });

    document.getElementById('sendT').addEventListener('click', () => { // Agregar evento Send T
        sendData('T');
    });
}

async function sendData(data) {
    if (writer) {
        await writer.write(encoder.encode(data));
        console.log(`Sent: ${data}`); // Mensaje de consola
    } else {
        console.log('Writer not available');
    }
}

```
