En este codigo hay varias formas de entrada y salida  
usa los botones para mostrar dos textos distintos.  
usa el sensor para mostrar la derecha y la izquierda marcado como R y L   
usa el sensor de cuando se mueve todo el micro:bit y muestra una imagen de una cara   
y usa el sensor de sonido para mostrar una imagen de cara feliz  


```py
from microbit import *

while True:
    if button_a.is_pressed():
        display.show('UPB')
    if button_b.is_pressed():
        display.show('FUBA')
    if accelerometer.get_x() > 200:
        display.show("R") 
        sleep(1000)
        display.clear()

    elif accelerometer.get_x() < -200:
        display.show("L")
        sleep(1000)
        display.clear()
    if  accelerometer.was_gesture('shake'):
        display.show(Image.SURPRISED)
        sleep(1000)
        display.clear()
    if microphone.sound_level() > 50:
        display.show(Image.HAPPY)
        sleep(1000)
        display.clear()
    sleep(100)
```
    
