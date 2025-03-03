```py
from microbit import *
import utime
import music

isEvent = False
eventData = ""

def tareaBomba():
    global isEvent,eventData

    if isEvent == True:
        isEvent = False
        if eventData == "A":
            display.show(eventData)
    

def tareaEventos():
    global isEvent,eventData

    if button_a.was_pressed():
        isEvent = True
        eventData = "A"

    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord("A"):
                isEvent = True
                eventData = "A"
    
while True:
    tareaBomba()
    tareaEventos()
```
