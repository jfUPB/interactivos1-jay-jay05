#### tabla comparativa  
https://drive.google.com/file/d/1o8L75pyZwRS7MNudm2EpukTwXroKjeYo/view?usp=sharing  
- ¿Por qué fue necesario introducir framing en el protocolo binario?  
- ¿Cómo funciona el framing?  
el framing en el protocolo binario, hace un trabajo parecido al que hace {n/} en el ASCII, esto para separar la linea de codigo de los datos, dandole inicio o fin a esta linea
esto para que el codigo tenga entendido que ese es el inicio o fin del la linea. esto es necesari ya que en la modalidad de binario, los datos se envian en una secuencia seguida
por lo que se necesita dar a entender su inicio y fin. si este no estuviera, el receptor no sabria cuando inicia o acaba una linea.
- el caracter de sincronización s como una alarma que avisa que elgo importante esta por suceder, identifica el inicio de un paquete de datos.
- el checksum sirve como una forma de detectar errores, revisa la integridad de un grupo de datos dentificando si estos tienen algun problema.
- En la función readSerialData() del programa en p5.js:
- ¿Qué hace la función concat? ¿Por qué?
la funcion concat lo que hacees unir dos arreglos, serialBuffer ya tiene datos y newData son los nuevos bytes, concat une las dos variables sin eliminar nada de ninguno de ellos
esto es para cuando los datos a veces no es envian en un grupo completo, los va acumulando hasta donde sea necesario y luego elimina lo que ya no sirve.
- En la función readSerialData() tenemos un bucle que recorre el buffer solo si este tiene 8 o más bytes ¿Por qué?
esto sirve para guardar en un paquete que los bytes necesarios son 8, este espera hasata completar todos los datos para seguir, este solo lee el mensaje cuando el paquete de bytes
esta completo.
- En el código anterior qué significa 0xaa?
esta es una forma de lenguaje binario para representar el numero 170 decimal. es el numero de forma binaria. se usa para marcaar el inicio de un mensaje.
- En el código anterior qué hace la función shift y la instrucción continue? ¿Por qué?
estos hacen la funcion de bucle para revisar datos. shift se pone  ahi para buscar el cmienzo correcto del paquete, si no es, este simplemente se elimina hasta encontrarlo.
continue, este salta al siguiente siclo del bucle sin ejecutar lo que sigue del codigo, este bucle se hace hasta completar los datos necesarios, si es asi, ya el codigo puede seguir
el curso.
- break lo que hace es que detiene el bucle, espera a que lleguen mas datos para poder seguir, esto es porque en el codigo se estan pidiendo 8 datos asi que hasta que esten completos
los 8 datos, el codigo no va a seguir.
- slice, el codigo tiene 8 datos, pero si en algun momento llego a necesitar algunos de estos datos sin dañar los demas, por ejemplo si necesito solo 2 o 3, se hace uso de slice para
separar solo los datos necesarios sin dañar los otros.
- splice sirve para modificar el arreglo original, puede servir para usar el arreglo modificado en el sigiente conjunto de bytes.
- A la siguiente parte del código se le conoce como programación funcional ¿Cómo opera la función reduce?
la funcion reduce es un mtodo de java script para reducir o acumular todos los elementos de un arreglo en un solo datos. dataBytes es el arreglo de numeros y con acc se empiezan a acumular los datos.
- la comparacion de el checksum calculado y el checksum recibido sirve como verificación de los datos, ya que como habia dicho antes, el checksum lo que hace es revisar si hay algun tipo de error antes de enviar los datos o seguir el codigo, en otras palabras, se recolectan los datos en las dos partes, lo que hacen estos dos es compararse y ver si todos los datos son iguales. si los checksums no coinciden ahi es cuando se imprime un error en la consola.  esto para poder encontrar errores en el codigo y poder corregirlo.
- En el código anterior qué hace la instrucción continue? ¿Por qué?
por lo  que me quedo entendido de la explicacion anterior de continue, este la funcion que tiene es, repetir el bucle de codigo hasta que la condicion pedidaa, se cumpla por completo, hasta que eso suceda, este bucle seguira dando vueltas en la misma parte y cuando ya este completa, el codigo seguira su curso. esto seria para revisar si hay errores den esta parte.
- Qué es un DataView? ¿Para qué se usa?
dataview te sirve para leer los diferentes tipos de datos de forma mas sencilla, te permite leer y escribir en el mismo buffer usando distintos tipos de datos.
- ¿Por qué es necesario hacer estas conversiones y no simplemente se toman tal cual los datos del buffer?
 son necesarias para interpretar correctamente los datos binarios que vienen del buffer. com los datos del buffer estan escitos de forma cruda, para poder entenderlos de mejor manera, es necesario convertir los datos a una manera mass entendible. En resumen, estas conversiones son necesarias para transformar el flujo de datos binarios del buffer en información útil y comprensible (coordenadas y estados de botones) que pueda ser utilizada en el programa.  

