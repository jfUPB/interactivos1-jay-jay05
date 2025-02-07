#### ¿que queria comprobar?  
que pasa si uso el sensor y los botones para generar sonido?  
#### hipotesis  
ya jugue un poco con los botones y tambien investigue sobre el como se usa la bocina y se generan notas musicales asi que quiero juntas estas dos formas de codigo  
#### codigos involucrados  
``` py
from microbit import *
import music
while True: 
 if button_a.is_pressed():
    music.play(['C4'])
 if button_b.is_pressed():
    music.play(['D4'])
 if pin_logo.is_touched():
    music.play(['E4'])
```
#### descripcion de los resultados  
el resultado ffue exitoso ya que logre lo que estaba intentando realizar y es que con cada boton que presioaba, lograba emitir un sonido distinto  
#### analisis  
el codigo dice que si el boton a, es presionado, entonces por las bocinas se emitiira el sonido de DO en la cuarta octava, si es el boton b, se emitira la nota RE  
y si es el sensor, sse emitira la nota MI. el while true verifica si los botones si estan siendo presionados  
#### concluciones  
al principio trate de escribir el codigo desde los ejemplos que se nos dan en la pagina, juntando ambos codigos con las partes que me servian para realizarlo.  
tuve varios problemas con esto ya que me faltaban algunas partes del codigo para hacer que funcione bien, pero luego de investigar un poquito mas y ver bien cada  
codigo, logre que funcionara bien.
