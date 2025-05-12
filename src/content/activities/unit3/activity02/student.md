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


seq_passWord = ["A", "B", "A", "S"]
seq_user = []

def update_display(time_left):
    display.show(str(time_left))

def explode():
    music.play(music.BA_DING)

start_time = 0
last_time_displayed = -1

update_display(countdown_time)

while True:
    if current_state == STATE_INICIO:

        if button_a.was_pressed() and countdown_time < max_time:
            countdown_time += 1
            update_display(countdown_time)

        if button_b.was_pressed() and countdown_time > min_time:
            countdown_time -= 1
            update_display(countdown_time)

        if accelerometer.was_gesture('shake'):
            start_time = utime.ticks_ms()
            seq_user = []
            current_state = STATE_ARMADO

    elif current_state == STATE_ARMADO:
        time_left = max(0, countdown_time - (utime.ticks_diff(utime.ticks_ms(), start_time) // 1000))

        if time_left != last_time_displayed:
            update_display(time_left)
            last_time_displayed = time_left

        if time_left == 0:
            explode()
            display.show("BOOM!")
            current_state = STATE_EXPLOTA
        
        if button_a.was_pressed():
            seq_user.append("A")
        if button_b.was_pressed():
            seq_user.append("B")
        if accelerometer.was_gesture('shake'):
            seq_user.append("S")
            if seq_user == seq_passWord:
                current_state = STATE_INICIO
                countdown_time = 20
                update_display(countdown_time)
                music.play(music.BADDY)
            else:
                seq_user = []

    elif current_state == STATE_EXPLOTA:
        if pin_logo.is_touched():
            current_state = STATE_INICIO
            countdown_time = 20
            update_display(countdown_time)

```

#### explicación   
lo que hice con la ayuda del profe fue, agregar otra accion mas que seria la secuencia y al momento de que el codigo perciva que la secuencia fue realizada, el estado inmediato al que se va la bomba es otra vez a armado  
como si volviera al inicio, al momento de hacer esto, la bomba produce un sonido, avisando que fue armada.  
