#### micro:bit:  
#### entradas:  
botones: dispositivo de entrada común  
sensores: la pantalla de leds aparte de ser una salida de luz, tambien funciona como una entrada de sensores. sensor de luz  
pines: sirven como entrada para elementos externos como sensores o niveladores 
logo tactil: el micri:bit nuevo ya cuenta con un boton extra tipo sensor que es otro tipo de entrada. el sensor sirve para arrastrar tambien  
microfono: el micro:bit cuenta con un microfono que hace uso como una eentrada por voz  

#### salidas:  
leds: dispositivo de salida que emite luz  
pantalla: pantalla con 25 leds que emite luz  
pines: también sirven para elementos externos de salida como luces led, bocinas, etc.  
bocina: micro:bit tambien cuenta con una bocina que sirve como salida de sonido  

#### Micropython  
#### ejemplo 1
``` py
from microbit import *

while True:
    if button_a.is_pressed():
        display.show(Image.HAPPY)
    if button_b.is_pressed():
        display.show(Image.SAD)
```
este codigo muestra como de entrada se dice que se usa el boton ya sea el a o el b, si uno de estos se presiona, de manera de salida, en la pantalla saldra una  
configuracion en fforma de carita feliz y lo mismo con el otro boton pero esta ve mostrara una cara triste.  
usa entrada de botones y salida de luz  

#### ejemplo 2   

``` py
from microbit import *

while True:
    if button_a.is_pressed():
        display.show(Image.HAPPY)
    if button_b.is_pressed():
        display.show(Image.SAD)
    if button_a.is_pressed()and button_b.is_pressed():
        display.show(Image.HEART)
    if pin_logo.is_touched():
        display.show(Image.SCISSORS)

```
este es el mismo codigo que el anterior pero con un agregaddo que es usando el pin logo, osea el sensor  
usa entrada de sensor y salida de luz  

#### ejemplo  3  

``` py
from microbit import *
import music


for x in range(2):
    music.play(['C4:4', 'D4', 'E4', 'C4'])

for x in range(2):
    music.play(['E4:4', 'F4', 'G4:8'])
```  
este codigo hace uso de la bocina emitiendo las notas que se le pide   
este codigo usa como entrada el codigo enviado y como salida usa la bocina

