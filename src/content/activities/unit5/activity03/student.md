#### diferencias  
el primer codigo usa las comas para dividir los datos, asi es como se verifica que se reciben los datos exactos.   
en el codigo dos, se usa otra variable para leer los bytes, especificando exactamente que son los 6 bytes a enviar esto hace una estructura mas precisa.  

al reproducir el codigo, lo que sucede es que aparece como si se estuviera enviando datos seguidos uno tras otro sin parar, esto creo que sucede porque como dice, no se estan enviando los datos correctos, esta funcionando solo sin que yo le envíe los datos.  
las diferencis que tienen los codigos comparado con el ultimo que ya tiene el funcionamiento con datos binarios es que se hace mas simple pero con mas funcionalidades, cambia la parte de las posiciones,  
con el dataview hace que se permite leer los 6 datos exactos requeridos y el mismo codigo lo convierte en los valores.  
