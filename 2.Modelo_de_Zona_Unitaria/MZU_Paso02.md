Paso 02 - Preparar la simulación
=========================================

A continuación, procederemos al segundo paso de la creación de un modelo de zona unitaria en HoneyBee, la preparación de la simulación, mostrado en rojo más abajo.

![alt text](https://user-images.githubusercontent.com/44324576/51675610-751eee80-1fd4-11e9-8349-1eb30ab5cc8a.png)

Aquí podemos ver cómo se relaciona con la sección previa acerca de la creación de zonas de HoneyBee, así como con el siguiente paso acerca de cómo correr la simulación.

![alt text](https://user-images.githubusercontent.com/44324576/49234839-1afd1500-f3f9-11e8-8e09-13b003d2fe75.png)

*Es importante hacer notar que para evitar crear un tutorial separado para el antiguo componente independiente de EnergyPlus, técnicamente estaremos corriendo la simulación empleando el motor de cálculo OpenStudio, el cual es un software superior multi-plataforma que permite combiran las simulaciones de iluminación basadas en Radiance con las simulaciones energéticas de EnergyPlus. Por el momento y para los propósitos de este turorial, simplemente ignoraremos las funciones de Radiance dentro de este componente.

Paso a paso
-----------

**2.00** El primer paso es cargar los datos climáticos, al igual que la vez anterior, arrastrando a nuestro lienzo el componente "Ladybug-0-Ladybug Open EPW and STAT Weather Files".

![alt text](https://user-images.githubusercontent.com/44324576/49236199-e8085080-f3fb-11e8-80c3-c862a69887b2.jpg)

**2.01** A continuación, creamos un panel (escribiendo //, o arrastrando hacia el lienzo el componente desde la primer pestaña "params") e introduciomos el URL que contiene la ubicación de los datos climáticos que deseamos utilizar, en este caso utilizaremos la localidad de Van Nuys, California:
https://www.energyplus.net/weather-download/north_and_central_america_wmo_region_4/USA/CA/USA_CA_Van.Nuys.AP.722886_TMY3/all

![alt text](https://user-images.githubusercontent.com/44324576/49236206-eb9bd780-f3fb-11e8-8092-fd86ed3d5049.jpg)

**2.02** Ahora craremos una lista con los datos de salida que deseamos obtener de la simulación cuando se haya completado. Es importante hacer notar qut casi todos estos datos de salida son simulados, aunque no completemos este paso. No obstante, guardar los resultados toma tiempo, y HoneyBee fue desarrollado para dar a los usuarios tanto control como sea posible sobre los tiempos de cálculo.

Arrastra un comppoonente "Honeybee-10-Honeybee_Generate EP Output" al lienzo. Este componente nos proporciona la lista de datos de salida que nos gustaría obtener de los datos de la simulación en OpenStudio. Honeybee usa un indicador booleano para indicar si se queiere solicitar o no estos datos. "TRUE" significa sí y "FALSE" significa que no. Es posible indicar esto conectando un indicador de dos posiciones para cambiar entre falso y verdadero, o simplemente escribir 'true' o 'false' en un panel y conectarlo.

![alt text](https://user-images.githubusercontent.com/44324576/49236209-eccd0480-f3fb-11e8-80e0-461e95f5b30f.jpg)

*Es importante notar que la lista de tipos de datos disponibles en el componente "Honeybee_Generate EP Output" solamente incluye los datos de salida más comunmente utilizados. La lista completa de datos de salida disponibles en OpenStudio puede ser consultada aquí: https://bigladdersoftware.com/epx/docs/8-3/input-output-reference/index.html. Alternativamente, el componente "Honeybee-10-Honeybee_Read Results Dictionary" puede proporcionar una lista de todos los datos de salida una vez que una simulación haya sido ejecutada.

La preparación inicial con los datos climaticos y la solicitud de los datos de salida ahora está completa, procedamos ahora a correr nuestra simulación.
