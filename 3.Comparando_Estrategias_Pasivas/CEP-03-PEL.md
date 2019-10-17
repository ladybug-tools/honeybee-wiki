# Equipos - Iluminación

A pesar de ser una pequeña sección del Diagrama de Balance de Energía en este modelo, se cubrirá un ejemplo básico de cómo asignar cargas en la zona. Esto incluye las cargas específicas de la zona, tal como equipo por unidad de área, tasa de infiltración por unidad de área, densidad de iluminación, número de personas por unidad de área, ventilación por unidad de área, ventilación por persona, y recirculación de aire por unidad de área. En este caso, mostraremos como cambiar toda la iluminación a Lámparas LED al ajustar la densidad de iluminación por unidad de área.

3.00 Regresando al diagrama, insertaremos el módulo siguiente inmediatamente después del módulo de ventanas eficientes del script anterior, tal como se indicó en el grupo amarillo apuntado desde abajo por una flecha amarilla. 

![alt text](https://user-images.githubusercontent.com/44324576/52429288-0c6f6000-2b04-11e9-93bb-e4151cecef01.png)


3.01 Haciendo un acercamiento podemos ver que el módulo Passive 3_Lighting Level simplemente continua donde el módulo Passive 1_High Performance Windows concluye. Cada elemento de análisis sucesivo añade una capa de enriquecimiento a las Zonas de Honeybee de los elementos anteriores. Este sistema en cadena facilita la configuración y re-configuración de los archivos de simulación con diferentes estrategias. 

![alt text](https://user-images.githubusercontent.com/44324576/52429470-6b34d980-2b04-11e9-93b3-f113a7584a31.png)


3.02 Asignar la densidad de iluminación es relativamente simple, solo se requiere conectar el panel con valor a 5.9 a la terminal lightingDensityPerArea. Como se puede leer del componente por sí mismo, este valor es medido en W/m2 y los valores típicos oscilan entre 3 W/m2 para Lámparas LED eficientes, a 15 W/m2 para bombillas incandescentes.

![alt text](https://user-images.githubusercontent.com/44324576/52430239-f367ae80-2b05-11e9-83dc-b768cfd81401.png)
