

Hay varias formas de modelar la sombra en Honeybee. Para elementos estáticos, lo más fácil es simplemente modelar la geometría y cargarla en un Componente Context Surfaces EP de Honeybee.

**2.00 - Revisión** El primero es simplemente dibujar geometría, como lo hicimos cuando agregamos árboles y elementos de sombreado al Modelo de Zona Única:
![005_single zone_shade overlay](https://user-images.githubusercontent.com/44324576/52411432-17ae9580-2adc-11e9-9cc8-1f8f78b200c5.jpg)

Conectaremos el componente de sombreado a nuestra definición existente aquí:
![gh_03_overview_shade](https://user-images.githubusercontent.com/44324576/52431819-47c05d80-2b09-11e9-8d26-08c140421d9c.png)

**2.01** Al acercarnos, podemos ver que este es exactamente el mismo módulo que creamos al final del Modelo de Zona Única.  
![gh_03_shade](https://user-images.githubusercontent.com/44324576/52420174-d1fcc780-2af1-11e9-9689-ffb93bd7f946.png)
_Observe que estos pasos se explican más detalladamente aquí: https://github.com/mostaphaRoudsari/honeybee/wiki/Iterating-to-improve-design_

**2.02** Una vez que ejecutemos las simulaciones y comparemos los Diagramas de Balance de Energía resultantes, podemos comparar la efectividad de sombrear la casa frente a reemplazar las ventanas con vidrio de alto rendimiento.
![002_high-perf-window-vs-shading](https://user-images.githubusercontent.com/44324576/52420820-1472d400-2af3-11e9-8909-704d701f6b40.gif)


**2.03** ¿Por qué es este el caso? Usando el componente Skydome de Ladybug, es posible visualizar en qué parte del cielo se origina esta radiación solar. Nos proporciona un diagrama como el de abajo. Este diagrama debe leerse como una esfera proyectada plana en el plano. Subdivide el cielo en 145 áreas y mide la cantidad general de radiación solar que se origina en cada área de la cúpula del cielo. 
![003_contextshadingskydome_legend](https://user-images.githubusercontent.com/44324576/52426104-a5e74380-2afd-11e9-98d5-1cf0292000a4.jpg)
_Una explicación completa del componente Ladybug_skyDome esta más allá de este tutorial, pero tu puedes descargar una archivo ejemplo en Hydra._

**Descargue el archivo ejemplo en** [Hydra](http://hydrashare.github.io/hydra/viewer?owner=alexandermatthias&fork=hydra&id=ComparingPassiveStrategies_01_SkyDome&slide=0&scale=1&offset=0,0).

**2.04** Aquí hay una vista axonométrica del mismo diagrama, que es más fácil de leer espacialmente.
![003_contextshadingskydome](https://user-images.githubusercontent.com/44324576/52426407-358cf200-2afe-11e9-82fe-3ce4d4781fd5.jpg)


 **2.05** Si superponemos este diagrama en nuestro modelo, podemos ver que el alero que protege el lado este de la casa es bastante efectivo, pero los lados sur y oeste de la casa quedan sin protección. Esta es la razón principal por la que las ventanas de alto rendimiento son más efectivas que el sombreado en el análisis anterior. También podemos ver que parte de la luz solar más intensa llega desde una altitud que es demasiado aguda para ser sombreada por los árboles.  
![003_contextshadingskydome_edit](https://user-images.githubusercontent.com/44324576/52424173-bb5a6e80-2af9-11e9-9460-a73456b6994a.jpg)

