#### que info esta enviando  
el micro bit le esta enviando datos a la pagina. esta encendiendo una luz led dando a entender que esta funcionando.  
tiene la lectura de X y de Y  y cn¿on el boton A y B. siempre se esta enviando datos de false continuamente, si se presiona  
algun boton, ya sea A o B, la info enviada cambia de false a true. el A cambia el eje X y el B cambia el eje Y.  
xValue y yValue son los valores que aparecen.  aState y bState son los botones.  
sin la linea de sleep(100) se dañaria el codigo porque ahora no se reflejan los datos, esto puede ser porque los datos se estan  
enviando a una velocidad tan rapida que no se visualiza.  tambie hace que el micro bit no consuma demasiados recursos y se   
mueva mas eficiente.  
las comas hacen de delimitadores que separan los valores. el salto de linea se hace con el \n, para  
informar que los datos de esa linea ya acabaron y va  ala siguiente linea.  
al momento de inclinar el micro bit hacia cualquier lado, el valo cambia dependiendo de que lado sea usando un plano carteciano como  
base. si lo inclino hacia la izquierda o abajo, los datos salen negativos y i lo inclino hacia la derecha o arriba, los valores  
salen positivos.  
si en vez de poner is_pressed ponemos was_pressed, lo que pasaria es que el sistema veria como si siempre se estuviera presionando  
por lo que no se mostraria cuando no esta presionado.  
si los datos de value cambiaran a 969 y 652, lo que pasaria es que ya no se enviaria datos como true o false sino que se enviarian  
datos de numeros 
