#### Consolidación de lo aprendido  
#### ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?  
function setup() {
  createCanvas(windowWidth, windowHeight);
  background(255);

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}
estariamo hablando de esta parte del codigo donde se conecta la plataforma de p5.js con python para asi mismo, conectarlo con el micro bit. esta parte, concidero yo  
es una de las mas importamtes del codigo ya que sin esta, no tendriamos como hacer que funcione en su totalidad.  
#### ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?  
- eso es porque las comas hacen el trabajo de separar los valores, indicar que son distintos y se deben enviar por separado, para evitar la sobre carga de los datos
enviados.
#### ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?  
esto es importante porque ayuda a la plataforma a entender cuando se acaba la información. como esta programación siempre esta enviando datos en una velocidad muy alta  
asi que por esto es que es necesario indicarle cuando debe parar.  
#### ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?  
ya he aprendido bastante que el uso y trabajo de las maquinas de estado es fundamental en trabajos como este. esto importa porque, como hemos hablado en trabajos  
anteriores, esta manera de programar es importante porque es el que cuida que podamos realizar varias ordenes al mismo tiempo sin que el sistema se colapse por la  
cantidad de informacion o porque al no tener los estado, nada funcionaria porque no tendria una separacion o solo se podria hacer una funcion por codigo.  
#### ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?  
data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)  
al hacer uso de: \n. esta es la manera en que se le da fin al mensaje, este para que finalice y no siga enviando más datos.  
#### ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?  
cuando se habla de ASCII se da a entender que los datos que se envian al micro bit, se hacen de una forma codificada, donde a una letra tiene un valor asignado y al  
momento de escribir el codigo, ya no se hace necesario usar los numeros como tal y solo se usa su letra designada.  
#### ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
esto es importante para que el programa sepa si hay datos que leer o no. si este intenta leer datos cuando no hay, esto puede generar un error, la maquina es la que  
dice si hay espacio disponible para los datos y si estos pueden leerse.  
#### if (port.availableBytes() > 0) {     let data = port.readUntil("\n");¿Qué pasa si esto no se hace?
el programa prodria tener problemas y no mostraria la informacion pedida, esto porque si no se se verifica si hay datos o no, el programa poria estar leyendo datos  
nulos. este auda como una seguridad para saber que los datos estan listos.  
#### ¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?  
encuentro que una forma para remplazarlo es usando esta funcion: trim() que lo que hace es eliminar cualquier espacio en blanco.  
#### Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías?  
para esto, la funcion que sirve seria: split().  
#### Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?  
esto es importante, ya que de por si ya se necesitan muchos numeros en los datos a enviar, esto es para que el programa pueda identificar sin tanto problema.  
#### Si el micro:bit tiene los siguientes datos xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial?  

#### ¿Qué aprendiste nuevo del micro:bit que no sabías antes?
me he dado cuanta que este aparato tiene una infinidad de funcionalidades para trabajar y explorar formas distintas de programar. de que existen muchas formas de  
explorar de una manera mas practica y rapida antes de realizarlo en una escala mas grande.   
#### ¿Qué aprendiste nuevo de p5.js que no sabías antes?
de p5 aprendi casi todo lo que no sabia, todas las funcionalidades que este tiene, que no solo es programacion numerica o estandar sino que incluye muchas cosas  
por ejemplo todos los ejemplos visuales y artisticos que se pueden crear con este


