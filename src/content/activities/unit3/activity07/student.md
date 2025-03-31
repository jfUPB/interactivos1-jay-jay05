#### codigo funcional de p5
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
    tareaEventos('A');
  });

  document.getElementById('sendB').addEventListener('click', () => {
    sendData('B');
    tareaEventos('B');
  });

  document.getElementById('sendS').addEventListener('click', () => {
    sendData('S');
    tareaEventos('S');
  });

  document.getElementById('sendT').addEventListener('click', () => {
    sendData('T');
    tareaEventos('T');
  });
}

async function sendData(data) {
  if (writer) {
    await writer.write(encoder.encode(data));
    console.log(`Sent: ${data}`);
  } else {
    console.log('Writer not available');
  }
}

function draw() {
  background(220);
  tareaBomba();

  textAlign(CENTER, CENTER);
  textSize(32);
  text(displayValue, width / 2, height / 2);
}

function update_display(time_left) {
  displayValue = time_left;
  console.log("Display:", displayValue);
}

function explode() {
  console.log("BOOM!");
}

function tareaEventos(receivedEvent) {
  event = receivedEvent;
  event_occurred = true;
}

function tareaBomba() {
  if (current_state === STATE_INICIO) {
    update_display(countdown_time);

    if (event_occurred) {
      if (event === 'A' && countdown_time < max_time) {
        countdown_time += 1;
        update_display(countdown_time);
      } else if (event === 'B' && countdown_time > min_time) {
        countdown_time -= 1;
        update_display(countdown_time);
      } else if (event === 'S') {
        start_time = millis();
        seq_user = [];
        current_state = STATE_ARMADO;
      }

      event_occurred = false;
    }
  } else if (current_state === STATE_ARMADO) {
    let time_left = max(0, countdown_time - Math.floor((millis() - start_time) / 1000));

    if (time_left !== last_time_displayed) {
      update_display(time_left);
      last_time_displayed = time_left;
    }

    if (time_left === 0) {
      explode();
      displayValue = "BOOM!";
      current_state = STATE_EXPLOTA;
    }

    if (event_occurred) {
      if (event === 'A') {
        seq_user.push("A");
      } else if (event === 'B') {
        seq_user.push("B");
      } else if (event === 'S') {
        seq_user.push("S");
        if (seq_user.join("") === seq_passWord.join("")) {
          current_state = STATE_INICIO;
          countdown_time = 20;
          update_display(countdown_time);
          console.log("BADDY");
        } else {
          seq_user = [];
        }
      }

      event_occurred = false;
    }
  } else if (current_state === STATE_EXPLOTA) {
    explode();
    if (event === 'T') {
      current_state = STATE_INICIO;
      countdown_time = 20;
      update_display(countdown_time);
    }
  }
}
```
#### codigo arreglado:  
https://editor.p5js.org/juanitaduque/full/A0QTJSL2t  
