#### class  
las ventajas que se tienen al usar class es para poder delimitar cada semaforo como objetos diferentes uno de el otro pero que sigan en el mismo codig trabajando de  
manera individual.  

```py
from microbit import *
import utime

class Semaforo:
    def __init__(self, x, tiempos):
        self.x = x
        self.tiempos = tiempos
        self.estado = "rojo"
        self.inicio = utime.ticks_ms()

    def actualizar(self):
        tiempo_actual = utime.ticks_diff(utime.ticks_ms(), self.inicio)
        if self.estado == "rojo" and tiempo_actual >= self.tiempos["rojo"]:
            self.inicio = utime.ticks_ms()
            self.estado = "amarillo"
        elif self.estado == "amarillo" and tiempo_actual >= self.tiempos["amarillo"]:
            self.inicio = utime.ticks_ms()
            self.estado = "verde"
        elif self.estado == "verde" and tiempo_actual >= self.tiempos["verde"]:
            self.inicio = utime.ticks_ms()
            self.estado = "rojo"
        self.mostrar()

    def mostrar(self):
        display.clear()
        if self.estado == "rojo":
            for y in range(2):
                display.set_pixel(self.x, y, 9)
        elif self.estado == "amarillo":
            display.set_pixel(self.x, 2, 9)
        elif self.estado == "verde":
            for y in range(3, 5):
                display.set_pixel(self.x, y, 9)
                

semaforo1 = Semaforo(0, {"rojo": 5000, "amarillo": 2000, "verde": 3000})
semaforo2 = Semaforo(2, {"rojo": 3000, "amarillo": 1000, "verde": 2000})
semaforo3 = Semaforo(4, {"rojo": 4000, "amarillo": 3000, "verde": 2000})

while True:
    semaforo1.actualizar()
    semaforo2.actualizar()
    semaforo3.actualizar()
   

```
