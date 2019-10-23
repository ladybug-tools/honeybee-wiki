Paso 03 - Correr la simulación
=========================================

El siguiente paso del proceso es recolectar la información que hemos ingresado hasta ahora para correr nuestra primera simulación energética. Nos concentraremos en el paso 3, resaltado en rojo más abajo:

![alt text](https://user-images.githubusercontent.com/44324576/51686499-c6d57200-1ff0-11e9-8708-03b5f2cb2583.png)

Al inspeccionarlo de cerca, observamos que en este paso se reciben los datos de salida de los pasos 1 y 2.

![alt text](https://user-images.githubusercontent.com/44324576/49238365-8d252800-f400-11e8-8545-6dc35671295c.png)

**3.00** El componente clave en este proceso es el componente "Honeybee-10-Honeybee_Run Energy Simulation" el cual, recolecta todos los datos de entrada que hemos preparado, completa los campos vacíos con datos por defecto y prepara una serie de instrucciones para el motor de simulación OpenStudio. Este conjunto de instrucciones es guardado en forma de un archivo OSM. Después de haber corrido la simulación, revisaremos cómo se ve un archivo OSM.

![alt text](https://user-images.githubusercontent.com/44324576/49255094-48fb4d00-f42b-11e8-8688-ae2a2edd2151.jpg)

