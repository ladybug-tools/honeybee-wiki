Ahora mostraremos cómo es posible usar nuestro modelo para explorar estrategias de diseño adicionales.

**5.00** Para esto, necesitaremos modificar el script que completamos en la sección 4. Los cambios se muestran resaltados en amarillo en las ilustraciones siguientes:

**Es posible descargar una versión con estos cambios en** [Hydra](http://hydrashare.github.io/hydra/viewer?owner=alexandermatthias&fork=hydra&id=SingleZoneModel_01_IteratingToImprove&slide=0&scale=1&offset=0,0)

![alt text](https://user-images.githubusercontent.com/44324576/51693280-f2f7ef80-1ffe-11e9-8163-9c24766b27bb.png)

**5.01** Lo primero que haremos será aplicar límites inferiores y superiores al gráfico, de manera que nuestros resultados sean dibujados en el mismo eje y y por lo tanto, que sean comparables entre sí. Debemos conectar dos paneles al componente "Ladybug_Legend Parameters" con los valores 0.03 y -0.03, como se muestra a continuación.

![alt text](https://user-images.githubusercontent.com/44324576/51693629-a19c3000-1fff-11e9-99e5-87b550ac6a8f.png)

**5.02** Podríamos imaginar que el diagrama de balance de calor describe el trabajo realizado por los sitemas mecánicos, pero en realidad es más que eso. Se trata de una descripción del calor moviéndose hacia y desde la zona. Para ilustrar este punto, cambiaremos la condición de la zona para que esté no-acondicionada, lo que resulta en un diagrama de balance de calor que describe la casa con los sistemas de aire acondicionado y calefacción apagados. En el script de Grasshopper esto se consigue conectando un selector booleano de falso arranque el compoente "Mass2Zones":

![alt text](https://user-images.githubusercontent.com/44324576/51693630-a234c680-1fff-11e9-953d-cf23f87a2afc.png)

**5.03** Si todos los selectores booleanos que están agrupados en rojo (lo que indica que sirven para lanzar un cálculo) están todavía en la posición "True", entonces los cambios hechos en **5.01** y **5.02** deberán causar que la simulación vuelva a lanzarse automáticamente. Ahora deberás poder apreciar el siguiente diagrama en el espacio de modelación de Rhino.

![alt text](https://user-images.githubusercontent.com/44324576/51693915-17080080-2000-11e9-9219-fd8c2399a44a.jpg)

**5.04** Al comparar esto con el diagrama de balance de energía anterior (ver más abajo) observamos que los valores correspondientes para el enfriamiento y la calefacción mensuales se han ido.

![alt text](https://user-images.githubusercontent.com/44324576/51693917-17080080-2000-11e9-8aa8-84d234d4dd35.jpg)

**5.05** Tambiénn podemos observar que las aportaciones de calor a la zona térmica continúan dominadas por las cargas solares, así que a continuación vamos a agregar el contexto que sombrea nuestro edificio. Recordando nuestro modelo original:

![alt text](https://user-images.githubusercontent.com/44324576/51699509-322d3d00-200d-11e9-9622-3538afae3643.jpg)

Con el fin de mantener la simplicidad, ignoraremos por el momento el efecto del espacio del ático en el techo. Estos son los elemtos que agregremos al componente de sombreado: dos árboles al sur, una extensión del techo hacia el sur y la entrada con cochera del lado norte.

![alt text](https://user-images.githubusercontent.com/44324576/51695123-98f92900-2002-11e9-964b-a786602a1ecf.jpg)

**5.06** en el script de grasshopper, esto se realiza al crear un componente de geometría y asignándole a éste la geometría mostrada anteriormente, enlazando con el componente "Honeybee EP Context Surfaces", el cual a su vez es conectado al componente "Honeybee_Export To OpenStudio. Esto puede verse en el componente realtado en amarillo a continuación:

![alt text](https://user-images.githubusercontent.com/44324576/51693280-f2f7ef80-1ffe-11e9-8163-9c24766b27bb.png)

Aquí está una acercamiento para hacer más legible esta imagen:

![alt text](https://user-images.githubusercontent.com/44324576/51695389-394f4d80-2003-11e9-90b2-6034cfd00a39.png)

**5.06** Ahora podemos apreciar que la contribución solar para la calefacción ha sido dramáticamente reducida.

![alt text](https://user-images.githubusercontent.com/44324576/51693914-17080080-2000-11e9-8e2b-576d578dc05b.jpg)

Esto concluye la sección acerca de iterar para ajustar los resultados de nuestro modelo de zona unitaria original. Ahora hemos comenzado a hacer comparaciones entre diferentes alternativas de diseño usando el diagrama de balance de calor.
