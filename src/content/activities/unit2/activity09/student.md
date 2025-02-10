#### primer codigo de intento 
``` py
from microbit import *
import utime

def show_traffic_light(color):
    if color == "red":
        for x in range(5):
            for y in range(2):  # Primeras dos filas
                display.set_pixel(x, y, 9)
    elif color == "yellow":
        for x in range(5):
            display.set_pixel(x, 2, 9)  # Fila 3
    elif color == "green":
        for x in range(5):
            for y in range(3, 5):  # Filas 4 y 5
                display.set_pixel(x, y, 9)

while True:
    show_traffic_light("red")
    utime.sleep(15)  # Rojo durante 15 segundos
    display.clear()
    show_traffic_light("yellow")
    utime.sleep(5)  # Amarillo durante 5 segundos
    display.clear()
    show_traffic_light("green")
    utime.sleep(10)  # Verde durante 10 segundos
    display.clear()
```

#### codigo final con los eventos 

``` py

from microbit import *
import utime

def show_traffic_light(color):
    display.clear()
    if color == "red":
        for x in range(5):
            for y in range(2):  # Primeras dos filas
                display.set_pixel(x, y, 9)
    elif color == "yellow":
        for x in range(5):
            display.set_pixel(x, 2, 9)  # Fila 3
    elif color == "green":
        for x in range(5):
            for y in range(3, 5):  # Filas 4 y 5
                display.set_pixel(x, y, 9)


# Init values
state = "st_red"
startTime = utime.ticks_ms()
timeInRed = 1000
timeInYellow = 500
timeInGreen = 2000
show_traffic_light("red")

while True:

    if state == "st_red":
        if utime.ticks_diff(utime.ticks_ms(),startTime) >= timeInRed:
            startTime = utime.ticks_ms()
            show_traffic_light("yellow")
            state = "st_yellow"
    elif state == "st_yellow":
        if utime.ticks_diff(utime.ticks_ms(),startTime) >= timeInYellow:
            startTime = utime.ticks_ms()
            show_traffic_light("green")
            state = "st_green"
    elif state == "st_green":
        if utime.ticks_diff(utime.ticks_ms(),startTime) >= timeInGreen:
            startTime = utime.ticks_ms()
            show_traffic_light("red")
            state = "st_red"
```

