```py
from microbit import *
import music

uart.init(baudrate=115200)

while True:
    if uart.any():
        data = uart.read()
        if data:
            data = data.decode('utf-8').strip()
            if data == 'love':
                display.show(Image.HEART)
                sleep(2000)
                display.clear()
        sleep(100)

```

```js
let port;
let connectBtn, sendLoveBtn;

function setup() {
    noCanvas();
    connectBtn = select('#connectBtn');
    sendLoveBtn = select('#sendLoveBtn');

    connectBtn.mousePressed(connectBtnClick);
    sendLoveBtn.mousePressed(sendLoveBtnClick);

    updateConnectBtn();
}

function updateConnectBtn() {
    connectBtn.html(port && port.opened ? 'Disconnect' : 'Connect to micro:bit');
}

async function connectBtnClick() {
    try {
        if (!port || !port.opened) {
            port = await navigator.serial.requestPort();
            await port.open({ baudRate: 115200 });
        } else {
            await port.close();
            port = null;
        }
        updateConnectBtn();
        console.log(port ? 'Connected to Micro:bit' : 'Disconnected from Micro:bit');
    } catch (err) {
        console.error('Error with serial port:', err);
    }
}

async function sendLoveBtnClick() {
    if (port?.writable) {
        const writer = port.writable.getWriter();
        await writer.write(new TextEncoder().encode('love\n'));
        writer.releaseLock();
        console.log('Sent love to Micro:bit');
    } else {
        console.error('Port is not open. Cannot send data.');
    }
}

```
