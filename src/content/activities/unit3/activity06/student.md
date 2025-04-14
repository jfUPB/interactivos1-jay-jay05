#### vectores de prueba 
state inicio: si preciono boton A, debe +1 = [X]  
state inicio: si envio boton A, debe +1 = [X]  
state inicio: si preciono boton B, debe -1 = [X]  
state inicio: si preciono boton B, debe -1 = [X]  
state inicio: si accion shake, debe ir a estado armado = [X]  
state inicio: si envio S, debe ir a estado armado = [X]  
state armado:if time_left != last_time_displayed:  update_display(time_left  last_time_displayed = time_left debe ir a estado explota = [X]  
state armado: si realizo la secuancia A B A S, debe ir a estado inicio = [X]  
state explota: envio T debe ir a estado inicio:  [X]  
state explota: toco pin logo debe ir a estado inicio:  [ ]  para ver si esta funcionando, lo que hago es poner un display.show("W") para ver si el problema es del pin   
o si pasa algo con el codigo que no recibe la orden 

