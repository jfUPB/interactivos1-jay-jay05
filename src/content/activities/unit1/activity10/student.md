#### codigo 
- lo que hice fue partir desde el mismo codigo anerio modificando que ahora ya no mestre un circulo sino un cuadrado y que dependiendo del boton que se usa,
- muestra un color distinto

```js
let port;
let connectBtn;
let squareColor;

function setup() {
  createCanvas(400, 400);
  background(220);


  port = createSerial();


  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);
  let sendBtn = createButton('Send Love');
  sendBtn.position(220, 300);
  sendBtn.mousePressed(sendBtnClick);


  squareColor = color(255);
}

function draw() {
 
  background(220);
  fill(squareColor);
  rect(width / 2 - 50, height / 2 - 50, 100, 100);

 
  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);
    processMicrobitData(dataRx); 
  }

 
  if (!port.opened()) {
    connectBtn.html('Connect to micro:bit');
  } else {
    connectBtn.html('Disconnect');
  }
}

function processMicrobitData(data) {
  if (data === 'A') {
    squareColor = color(255, 0, 0);
  } else if (data === 'B') {
    squareColor = color(255, 255, 0); 
  } else {
    squareColor = color(0, 255, 0);
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open('MicroPython', 115200);
  } else {
    port.close();
  }
}
```

function sendBtnClick() {
  port.write('h');
}
