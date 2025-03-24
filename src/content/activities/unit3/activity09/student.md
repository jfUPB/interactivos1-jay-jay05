micro bit-state inicio: si preciono boton A, debe +1 = [X]
p5  -  X

micro bit-state inicio: si envio boton A, debe +1 = [X]  
p5  -  X

micro bit-state inicio: si preciono boton B, debe -1 = [X]  
p5  -  X

micro bit-state inicio: si preciono boton B, debe -1 = [X]  
p5  -  X

micro bit-state inicio: si accion shake, debe ir a estado armado = [X]  
p5  -  X

micro bit-state inicio: si envio S, debe ir a estado armado = [X]  
p5  -  X

state armado:if time_left != last_time_displayed: update_display(time_left last_time_displayed = time_left debe ir a estado explota = [X]  
p5   -  X

state armado: si realizo la secuancia A B A S, debe ir a estado inicio = [X]  
p5   -  X

state explota: envio L debe ir a estado inicio: [X]  
p5   -  [ ]

state explota: toco pin logo debe ir a estado inicio: [ ] para ver si esta funcionando, lo que hago es poner un display.show(“W”) para ver si el problema es del pin
o si pasa algo con el codigo que no recibe la orden
p5  

#### corrección  
aqui estoy usando la misma tabla de estados que use para la actividad 6 ya que as funcionalidades siguen sinendo las mismas sin embargo le añadí la parte de p5js  
mostrando tambien sus funcionalidades.  
en los primeros intentos tuve mucho problema para que la bomba se pudiera manejar den las dos plataformas simutaneamente asi que tuve que regresarme varias veces  
en este puento.  
luego ya que esto estaba bien, me toco regresarme ortra vez ya que algo que no me estaba fncionando era la parte de reiniciar la bomba con en pin logo o la letra L  
asi que tuve que concentrarme en este punto también y por eso en la tabla al inicio aparece que esta parte del proceso no esta funcionando pero al final si se logro   
arreglar esta parte.  
