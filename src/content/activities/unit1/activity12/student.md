#### act 12

- como antes, use el mismo codigo pero remplazando valores, lo comlicado fui hacer que el programa leyera las fotos y las mostrara, por que sin un buen link que supiera leer, pues este no tenia como mostrarlo asi que tuve que subir las imagenes en un programa aparte para luego generar el link y ponerlo en el codigo final. 

 codigo: 
```js
let port;
let connectBtn;
let images = [];
let currentImage = 0;
function preload() {
  images[0] = loadImage("https://i.imgur.com/2OqkHXJ.jpg");
  images[1] = loadImage("https://i.imgur.com/GzgEmve.jpg");
  images[2] = loadImage("https://i.imgur.com/uLy9zk4.jpg");
  images[3] = loadImage("https://i.imgur.com/flgkq68.jpg");
}


function setup() {
  createCanvas(400, 400);
  background(220);

  port = createSerial(); 

  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);
  image(images[currentImage], 50, 50, 300, 300);

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
    currentImage = (currentImage - 1 + 4) % 4;
  } else if (data === 'B') {  
    currentImage = (currentImage + 1) % 4; 
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
