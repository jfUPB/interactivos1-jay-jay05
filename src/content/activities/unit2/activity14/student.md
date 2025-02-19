 #### documentacion 
       
        if button_a.was_pressed() and countdown_time < max_time:
            countdown_time += 1
            utime.sleep(0.2)  
        
        if button_b.was_pressed() and countdown_time > min_time:
            countdown_time -= 1
            utime.sleep(0.2)
            
aqui hay dos ejemplos de vectores con sus resultados esperados y es que dice: con el tiempo ya establecido del contador, si se presiona el boton a, este tiempo  
sube un segundo al contador, y si se presiona el boton b, este tiempo baja un segundo.  

     
        if pin0.is_touched():
            current_state = STATE_INICIO
            countdown_time = 20 
            
este muestra el momento de reiniciar el juego con el touch y que su numero estandar seria 20   

        if time_left == 0:
                  current_state = STATE_EXPLOTA
                  explode()

aca se ve cuando se le da a entender que cuando el contador llegue a 0, este debe hacer la simulacion de exploción  
              

los problemas que tuve con el codigo fue relacionarme bien con los eventos ya que esta era una forma nueva de programar y hacer acciones asi que esta forma era  
realmente nueva para mi
