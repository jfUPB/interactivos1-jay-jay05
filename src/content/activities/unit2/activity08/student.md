#### como funciona  
Este código usa los píxeles de la pantalla led para que brillen en un tiempo estimado. Este ejemplo lo hace cada 1 segundo y cada 0,5 segundos.  
Lo que hace para definir qué led encender, lo usa como plano cartesiano, seleccionando el led en la posición 0 0 y en la posición 4 4  
Así se escoge el tiempo y el lugar donde el led va a estar prendiendo y apagado, esto generando un patrón.  
En el código se está diciendo un estado inicial del píxel y se le aclara cuando debe prender y cuando apagar dependiendo del intervalo de tiempo que se le pide  
con X y Y se le está diciendo la posición exacta del píxel.   
De los estados puedo ver el WaitTimeOut que es cuando el código espera un intervalo de tiempo, y el Init que guarda el tiempo actual.  
El evento que puedo ver en el código sería cuando se pregunta la posición del píxel en la pantalla, esto se refleja con el uso del plano cartesiano, X y Y.  
la acción que genera el código es encender los pixele en la pantalla de una manera y tiempo establecido, creando un patrón.  

