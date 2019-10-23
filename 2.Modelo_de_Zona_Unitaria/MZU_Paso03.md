Paso 03 - Correr la simulación
=========================================

El siguiente paso del proceso es recolectar la información que hemos ingresado hasta ahora para correr nuestra primera simulación energética. Nos concentraremos en el paso 3, resaltado en rojo más abajo:

![alt text](https://user-images.githubusercontent.com/44324576/51686499-c6d57200-1ff0-11e9-8708-03b5f2cb2583.png)

Al inspeccionarlo de cerca, observamos que en este paso se reciben los datos de salida de los pasos 1 y 2.

![alt text](https://user-images.githubusercontent.com/44324576/49238365-8d252800-f400-11e8-8545-6dc35671295c.png)

**3.00** El componente clave en este proceso es el componente "Honeybee-10-Honeybee_Run Energy Simulation" el cual, recolecta todos los datos de entrada que hemos preparado, completa los campos vacíos con datos por defecto y prepara una serie de instrucciones para el motor de simulación OpenStudio. Este conjunto de instrucciones es guardado en forma de un archivo OSM. Después de haber corrido la simulación, revisaremos cómo se ve un archivo OSM.

![alt text](https://user-images.githubusercontent.com/44324576/49255094-48fb4d00-f42b-11e8-8688-ae2a2edd2151.jpg)

*Nota acerca de las versiones: Es importante no confundir el componente "Honeybee_Export to OpenStudio" con el anterior "Honeybee_Run Energy Simulation". El componente OpenStudio realiza las mismas funciones que el componente anterior y más. El anterior componente ha sido mantenido en las librerías de Honeybee solamente con la finalidad de permitir a los usuarios continuar usando scripts previamente escritos.*

![alt text](https://user-images.githubusercontent.com/44324576/49256977-0fc5db80-f431-11e8-8448-498c69de5edd.png)

*La relación entre el componente OpenStudio y el anterior componente EnergyPlus proviene del desarrollo de Honeybee de manera más general, como se describe en los siguientes diagramsa. OpenStudio funciona como un "hub" o nodo concetrador, entre Honeybee y EnergyPlus, lo que expande el conjunto de funcionalidades y características más allá de aquellas disponibles únicamente en EnergyPlus.

![alt text](https://user-images.githubusercontent.com/44324576/51989233-e5cb7c80-24a6-11e9-8762-4f506e842115.JPG)
![alt text](https://user-images.githubusercontent.com/44324576/51989236-e6fca980-24a6-11e9-83a8-413f623443b3.JPG)

Paso a paso
-----------

**3.01** Lo primero que hay que hacer es conectar el archivo climático EPW del paso 2 al componente "Honeybee_Export to OpenStudio".

![alt text](https://user-images.githubusercontent.com/44324576/49255095-48fb4d00-f42b-11e8-9c1f-9e8a38c34bdf.jpg)

**3.02** A continuación, conectamos las zonas que tienen ventanas del paso 1.

![alt text](https://user-images.githubusercontent.com/44324576/49255096-48fb4d00-f42b-11e8-8616-ee7069e71280.jpg)

**3.03** Conectamos la lista de datos de salida deseados del paso 2.

![alt text](https://user-images.githubusercontent.com/44324576/49255097-48fb4d00-f42b-11e8-81bd-673f3fe42ae1.jpg)

**3.04** Necesitaremos un interruptor de dos posiciones booleano para correr la simulación, pero todavía no debemos cambiarlo a "verdadero". Utilizaremos este mismo interruptor booleano para indicarle a Honeybee que desamos guardar una copia del archivo OSM que contenga los parámetros de nuestra simulación. Debemos notar que este interruptor está conectado a las terminales en el diagrama más abajo:

![alt text](https://user-images.githubusercontent.com/44324576/49255099-48fb4d00-f42b-11e8-8d2d-d30d6dd81454.jpg)

**3.05** Ahora especificaremos un nombre para el archivo de datos de salida de la simulación. Esto hace posible que podamos guardar los datos de salida en lugar de sobreescribir a cada momento. Usaremos un panel para esto y llamaremos a nuestro archivo "LAHouse".

![alt text](https://user-images.githubusercontent.com/44324576/49256165-6bdb3080-f42e-11e8-8689-ef2a619ef127.jpg)

**3.06** Finalmente, cmabiaremos el interruptor booleano para correr la simulación. Esto puede tomar varios minutos, dependiendo de la capacidad de procesamiento de tu computadora u ordenador.

![alt text](https://user-images.githubusercontent.com/44324576/49255100-4993e380-f42b-11e8-8d05-bcab2c6967da.jpg)

**3.07** Como lo prometimos en el paso 1, ahora puedes ver cuáles son el conjunto de instrucciones y ajustes que Honeybee ha enviado a OpenStudio. Estos están contenidos en el archivo OSM, el cuál puedes localizar al conectar un panel al nodo de salida "osmFileAddress".

![alt text](https://user-images.githubusercontent.com/44324576/49258081-7dbfd200-f434-11e8-8833-1bc4e751f845.jpg)

**3.08** A continuación, presentamos una porción del archivo OSM. Es importante notar que Honeybee ha autocompletado muchos de los campos con valores por defecto. Por ejemplo, nosotros no modificamos el periodo de análisis, pero el campo "Begin Month" ha sido definido como 1 (enero), y el campo "End Month" aparece en 12 (diciembre). Si abres este archivo en tu computadora u ordenador, notarás que es bastante largo, pero esto te da una idea del proceso.

![alt text](https://user-images.githubusercontent.com/44324576/49251487-befab680-f421-11e8-8553-f94d9c21fa92.JPG)

No obstante, nuestra preocupación principal es el archivo de resultados, el cual es arrojado como un documento de valores separados coma. Este formato es comunmente empleado en hojas de cálculo y a en la siguiente sección veremos cómo es el proceso de recorrer estos datos para obtener la información que requerimos para hacer un diagrama de balance de calor.
