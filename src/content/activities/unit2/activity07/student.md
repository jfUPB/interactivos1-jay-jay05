con este codigo lo que hago es que dependiendo del boton que estoy presionando, el micro:bit emite un sonido, ya sea DO, RE, MI o  FA  
usa los botones, el sensor y el movimiento.  

``` py

from microbit import *
import music
while True:
    if button_a.is_pressed():
        music.play(['C4:2'])
    if button_b.is_pressed():
        music.play(['D4:2'])
    if pin_logo.is_touched():
        music.play(['E4:2'])
    if  accelerometer.was_gesture('shake'):
        music.play(['F4:2'])
        sleep(1000)
        display.clear()

```
