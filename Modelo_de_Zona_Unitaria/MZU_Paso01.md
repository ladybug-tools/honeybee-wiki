Paso 01 - Asignar Propiedades a las Zonas
=========================================

El primer paso necesario para correr una simulación es asignar las propiedades por defecto a las zonas que serán analizadas. Esta será también nuestra primera incursión en la interfaz de Grasshopper y Honeybee. Si no estás familiarizado con Grasshopper y Honeybee, dirígete a las secciones introductorias para cubrir los fundamentos básicos.

En este tutorial comenzaremos a dar un vistazo al script completo que crearemos para un Modelo de Zona Unitaria. El paso que estaremos cubriendo se refiere a las zonas resaltadas en rojo en las siguientes figuras. Si estás siguiendo este tutorial en paralelo en tu máquina, asegúrate de echar a volar Honeybee y Ladybug, tal como se describe en la introducción y como puede apreciarse en el extremo izquierdo de la imagen que aparece abajo.

![alt text](https://user-images.githubusercontent.com/44324576/51673655-d5129680-1fce-11e9-9f97-66e6f5418b6d.png)

Al acercarte a la imagen, leyéndola de izquierda a derecha, observa que primero crearemos los componentes que contienen la geometría. Esta geometría es usada para crear zonas con distintas propiedades por defecto. Después, las ventanas son añadidas como objetos pertenecientes a estas zonas.

![alt text](https://user-images.githubusercontent.com/44324576/51674124-1fe0de00-1fd0-11e9-9e4e-7b7ef4f796be.png)

Paso a paso
-----------

**1.00** Primero creamos un componente de geometría y cambiamos su nombre a 'House Zone' (ver **ii.05** si no estás seguro de cómo crear componentes y renombrarlos). Posterioremente, colocaremos en este componente la geometría de zona construida de acuerdo con las instrucciones en el Paso 1.

![alt text](https://user-images.githubusercontent.com/44324576/49189563-1e4bbe80-f36f-11e8-8537-193ce899aa3a.jpg)

Aquí está una imagen de a zona que ha sido cargada en este componente de geometría, superpuesta con el contexto del modelo que representa.

![alt text](https://user-images.githubusercontent.com/44324576/49190883-7df89880-f374-11e8-940b-a95f99c58fad.jpg)

**1.01** El componente 'Honeybee Masses to Zones' convierte la geometría en una zona que puede ser importada en EnergyPlus. Como puede inferirse por el '\_' frente a los conectores 'Masses' y 'createHBZones', los únicos datos de entrada requeridos son las masas de zona y un selectro boleano para lanzar la creación de las zonas. En este caso, solamente tenemos una zona, así que dejaremos el cambio de nombres para otro ejemplo con múltimples zonas.

![alt text](https://user-images.githubusercontent.com/44324576/49189556-1db32800-f36f-11e8-8f03-f982dafb3d43.jpg)

**1.02** Honeybee cuenta con una librería de ajustes por defecto para modelos en EnergyPlus de la que podemos elegir. El componente 'Honeybee bldgPrograms' te permite elegir de una lista de programas genéricos. El componente 'Honeybee_ListZonePrograms' ofrece una lista más detallada de los tipos de espacios dentro de estos programas; cada uno corresponde con un conjunto de ajustes y horarios por defecto para la simulación. El componente 'Honeybee_Item Selector' te permite elegir uno de stos sub-programas para conectarlo 'Masses2Zones' en 'zoneProgram'.

![alt text](https://user-images.githubusercontent.com/44324576/49189557-1db32800-f36f-11e8-8dde-ff6e9af4d48b.jpg)

**1.03** Cuando un selector boleano fijado en 'Verdadero' se conecta en el dato de entrada 'create Honeybee Zones' el componente 'Mass2Zones' busca en la librería de EnergyPlus los ajustes por defecto para un espacio del tipo 'Apartment' dentro de la tipología de edificio 'MidriseApartment' y aplica esos horarios a la geometría de zona asignada al componente. Este es un buen ejemplo de por qué es importante tener el componente 'Honeybee' volando. El componente 'Mass2Zones' no contiene todas estas librerías por si mismo, sino que busca a través de las librerías almacenadas en el componente 'Honeybee' y aplica los ajustes apropiados.

![alt text](https://user-images.githubusercontent.com/44324576/49189558-1db32800-f36f-11e8-9189-50b314eae95b.jpg)

**1.04** Una vez que las zonas fueron creadas, es momento de crear ventanas y asignarlas perteneciendo a esta zona. Esto se hace usando el componente 'Honeybee Add Glazing' (Honeybee-00-Honeybee_addHBGlz).

![alt text](https://user-images.githubusercontent.com/44324576/49189559-1db32800-f36f-11e8-81e2-1f3937621c17.jpg)

**1.05** Crea otro componente de geometría, cambia su nombre a 'House Windows' y carga las siguientes ventanas detro de él. Revisa **0.07** para ver los requerimientos geométricos para modelar ventanas.

![alt text](https://user-images.githubusercontent.com/44324576/51674921-6fc0a480-1fd2-11e9-8834-58054e2c5887.jpg)

**1.06** Enseguida, conecta la geometría de las ventanas en la terminal '\_childSurfaces' del componente 'Honeybee_HBaddglz'. Como puedes ver en las otras terminales de este componente, también es posible especificar una lista de nombres para estas ventas y especificar los detalles constructivos y materiales para Radiance de estas ventanas.

![alt text](https://user-images.githubusercontent.com/44324576/49189560-1e4bbe80-f36f-11e8-9ff4-e52bf5159263.jpg)

Las zonas ahora han sido creadas con los valores por defeto seleccionados y con ventanas. Es momento de pasar al siguiente paso: Asignar Datos Climáticos y Seleccionando Datos de Salida de Simulación.
