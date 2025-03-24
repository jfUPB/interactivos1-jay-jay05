
#### codigo py
```py
from microbit import *

uart.init(baudrate=115200)

while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(100)
    if button_b.is_pressed():
        uart.write('B')
        sleep(100)
    if accelerometer.is_gesture("shake"):
        uart.write('S')
        sleep(100)
    if pin_logo.is_touched():
        uart.write('L')  # Comando para reiniciar la bomba
        sleep(100)

```

#### codigo p5js
```js
let port;
let writer;
let encoder = new TextEncoder();

let STATE_INICIO = 0;
let STATE_ARMADO = 1;
let STATE_EXPLOTA = 2;

let countdown_time = 20;
let min_time = 10;
let max_time = 60;
let current_state = STATE_INICIO;

let seq_passWord = ["A", "B", "A", "S"];
let seq_user = [];

let start_time = 0;
let last_time_displayed = -1;
let event_occurred = false;
let event = "";

let displayValue = countdown_time;
function setup() {
  createCanvas(400, 200);
  port = createSerial();

  let connectBtn = createButton('Connect to Micro:bit');
  connectBtn.position(10, 10);
  connectBtn.mousePressed(() => {
    if (!port.opened()) {
      port.open('MicroPython', 115200);
    } else {
      port.close();
    }
  });

  let buttonA = createButton('Send A');
  buttonA.position(10, 50);
  buttonA.mousePressed(() => {
    sendCommand('A');
  });

  let buttonB = createButton('Send B');
  buttonB.position(80, 50);
  buttonB.mousePressed(() => {
    sendCommand('B');
  });

  let buttonS = createButton('Send S');
  buttonS.position(150, 50);
  buttonS.mousePressed(() => {
    sendCommand('S');
  });

  let buttonL = createButton('Reset Bomb (Send L)');
  buttonL.position(220, 50);
  buttonL.mousePressed(() => {
    sendCommand('L');
    resetBomb(); // Reinicia la bomba en la interfaz
  });
}

function draw() {
  background(220);
  textAlign(CENTER, CENTER);
  textSize(32);
  text(displayValue, width / 2, height / 2);

  tareaBomba();

  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);
    if (dataRx) {
      tareaEventos(dataRx);
      if (dataRx === 'L') {
        resetBomb(); // Reinicia la bomba cuando el Micro:bit envía "L"
      }
    }
  }
}

function resetBomb() {
  current_state = STATE_INICIO;
  countdown_time = 20;
  displayValue = countdown_time;
  seq_user = [];
  console.log("Bomba reiniciada");
}


function tareaEventos(receivedEvent) {
  event = receivedEvent;
  event_occurred = true;
}

function tareaBomba() {
  if (current_state === STATE_INICIO) {
    if (event_occurred) {
      if (event === 'A' && countdown_time < max_time) {
        countdown_time++;
      } else if (event === 'B' && countdown_time > min_time) {
        countdown_time--;
      } else if (event === 'S') {
        start_time = millis();
        seq_user = [];
        current_state = STATE_ARMADO;
      }
      event_occurred = false;
    }
    displayValue = countdown_time;
  } else if (current_state === STATE_ARMADO) {
    let time_left = max(0, countdown_time - Math.floor((millis() - start_time) / 1000));

    if (time_left !== last_time_displayed) {
      displayValue = time_left;
      last_time_displayed = time_left;
    }

    if (time_left === 0) {
      current_state = STATE_EXPLOTA;
      displayValue = "BOOM!";
    }

    if (event_occurred) {
      if (event === 'A' || event === 'B' || event === 'S') {
        seq_user.push(event);
        if (seq_user.join("") === seq_passWord.join("")) {
          current_state = STATE_INICIO;
          countdown_time = 20;
        } else if (seq_user.length > seq_passWord.length) {
          seq_user = [];
        }
      }
      event_occurred = false;
    }
  } else if (current_state === STATE_EXPLOTA) {
    explode();
  }
}

function explode() {
  background(255, 0, 0);
  text("BOOM!", width / 2, height / 2);
}

```
