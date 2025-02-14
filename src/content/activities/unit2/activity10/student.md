1) el programa logra hecer varias cosas al mismo tiempo porque hace uso de los estados, estos para que algo suceda de manera ciclica y cada vez que se acaba el ciclo, este vuelve a empezar desde el inicio,
sin embargo para lograr que otra cosa pase se debe hacer un estado donde el cicli esta funcionando esternamente pero si pasa un condicional cualquiera que se quiera que pase, ahi es donde la respuesta
del micro:bit cambia. como asi? en los estados se esta diciendo que si la condicion de presionar el boton a, se cumple, pues este muestra la cara anterior a la que se estaba mostrando, esto se hace de modo
de condicion que si o si debe cumplirse para que se realice la accion, de lo contrario, el ciclo seguira en su orden natural. esto de los estados permite que el codigo trabaje varias cosas al tiempo.
#### vectores:  
1) si estoy en el estado happy y preciono el boton a, este pasa al estado sad: funciona  
2) si estoy en el estado happy y pasa el tiempo establecido, pasa al estado smile: funciona  
3) si esta en el estado smile y se presiona el boton a, pasa al estado happy: funciona
4) si esta en el estado smile y se espera el intervalo de tiempo de este, pasa al estado sad: funciona
5) si esta en el estado sad y se preciona el boton a, pasa al estado smile: funciona
6) si esta en el estado de sad y pasa el intervalo de tiempo establecido, pasa a happy: funciona

