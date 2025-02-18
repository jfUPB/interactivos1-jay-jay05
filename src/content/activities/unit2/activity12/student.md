#### codigo: 
``` py
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

def update_display(time_left):
    display.show(str(time_left))

def explode():
    music.play(music.BA_DING)

start_time = 0
last_time_displayed = -1 

while True:
    if current_state == STATE_INICIO:
        update_display(countdown_time)
        
        if button_a.was_pressed() and countdown_time < max_time:
            countdown_time += 1
            utime.sleep(0.2)  
        
        if button_b.was_pressed() and countdown_time > min_time:
            countdown_time -= 1
            utime.sleep(0.2)

        if accelerometer.is_gesture('shake'):
            current_state = STATE_ARMADO
            start_time = utime.ticks_ms()
        
        if pin0.is_touched():
            current_state = STATE_INICIO
            countdown_time = 20 

    elif current_state == STATE_ARMADO:
        time_left = max(0, countdown_time - (utime.ticks_diff(utime.ticks_ms(), start_time) // 1000))
        
        if time_left != last_time_displayed:
            update_display(time_left)
            last_time_displayed = time_left
        
        if time_left == 0:
            current_state = STATE_EXPLOTA
            explode()
        
    elif current_state == STATE_EXPLOTA:
        display.show("BOOM!")
        while not pin0.is_touched():
            pass  
        current_state = STATE_INICIO
        countdown_time = 20 

    utime.sleep(0.1)
    
```

#### video:  
**https://drive.google.com/file/d/1jevfiDzPU05xBI4x45OR9x7Y3k-E-Vqx/view?usp=sharing**:
 
