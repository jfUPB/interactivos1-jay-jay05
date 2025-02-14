#### codigo
la manera en la que el circulo se mueve es hacio¿endo que el boton a mueve el circulo hacia la derecha unicamente y el boton b mueve el circulo unicamente
a la izquierda con cada vez que se presiona. se hace de una manera tipo plano carteciano donde si se quiere mover a la derecha se le suve el valor en X o si
hacia la isquierda pues este disminuye el valor en X. 

```js
let port;
let connectBtn;
let circleX;

function setup() {
  createCanvas(400, 400);
  background(220);


  port = createSerial();


  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);

 
  circleX = width / 2;
}

function draw() {

  background(220);
  fill(100, 150, 255);
  ellipse(circleX, height / 2, 50, 50);


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
    circleX = max(25, circleX - 10);
  } else if (data === 'B') {
    circleX = min(width - 25, circleX + 10);
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
