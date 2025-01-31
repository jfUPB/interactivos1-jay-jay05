#### act 12

- como antes, use el mismo codigo pero remplazando valores, lo comlicado fui hacer que el programa leyera las fotos y las mostrara, por que sin un buen link que supiera leer, pues este no tenia como mostrarlo asi que tuve que subir las imagenes en un programa aparte para luego generar el link y ponerlo en el codigo final. 

 codigo: 
```js
let port;
let connectBtn;
let selectedShape = ""; // Almacena la figura seleccionada

function setup() {
    createCanvas(400, 400);
    background(220);
    
    // Configurar la conexión serial
    port = createSerial();

    // Botón para conectar al micro:bit
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(20, 350);
    connectBtn.mousePressed(connectBtnClick);

    // Botones para elegir la figura
    let circleBtn = createButton('Círculo');
    circleBtn.position(20, 50);
    circleBtn.mousePressed(() => sendShape('C'));

    let triangleBtn = createButton('Triángulo');
    triangleBtn.position(100, 50);
    triangleBtn.mousePressed(() => sendShape('T'));

    let squareBtn = createButton('Cuadrado');
    squareBtn.position(200, 50);
    squareBtn.mousePressed(() => sendShape('S'));

    let heartBtn = createButton('Corazón');
    heartBtn.position(300, 50);
    heartBtn.mousePressed(() => sendShape('H'));
}

function draw() {
    background(220);

    // Dibujar la figura seleccionada en la pantalla
    fill('black');
    noStroke();

    if (selectedShape === 'C') {
        ellipse(width / 2, height / 2, 100, 100);
    } else if (selectedShape === 'T') {
        triangle(width / 2, height / 2 - 50, width / 2 - 50, height / 2 + 50, width / 2 + 50, height / 2 + 50);
    } else if (selectedShape === 'S') {
        rectMode(CENTER);
        rect(width / 2, height / 2, 100, 100);
    } else if (selectedShape === 'H') {
        drawHeart(width / 2, height / 2, 50);
    }
}

// Función para enviar la figura seleccionada al micro:bit
function sendShape(shape) {
    if (port.opened()) {
        port.write(shape); // Enviar la letra correspondiente
        selectedShape = shape; // Cambiar la figura en pantalla
    }
}

// Función para conectar/desconectar el micro:bit
function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

// Función para dibujar un corazón
function drawHeart(x, y, size) {
    beginShape();
    vertex(x, y + size / 4);
    bezierVertex(x - size, y - size / 2, x - size, y - size, x, y - size / 2);
    bezierVertex(x + size, y - size, x + size, y - size / 2, x, y + size / 4);
    endShape(CLOSE);
}

```

``py
from microbit import *

# Inicializa la comunicación UART con el computador
uart.init(baudrate=115200)

while True:
    if uart.any():  # Verifica si hay datos disponibles
        data = uart.read(1)  # Lee un byte
        if data:  # Asegura que data no sea None
            shape = data.decode()  # Decodifica el carácter recibido
            
            if shape == 'C':  # Círculo
                display.show(Image("00900:09990:99999:09990:00900"))
            elif shape == 'T':  # Triángulo
                display.show(Image("00900:09990:00900:00900:00900"))
            elif shape == 'S':  # Cuadrado
                display.show(Image("00000:09990:09090:09990:00000"))
            elif shape == 'H':  # Corazón
                display.show(Image.HEART)


``
