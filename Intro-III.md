Intro III - La Interfaz de Honeybee
===================================

Esta sección cubrirá cómo construir un script muy sencillo de Honeybee desde cero. Comenzaremos con una breve introducción a la interfaz de Honeybee, continuaremos con la creación de una definición básica de Honeybee y finalmente, concluiremos con una lista de convenciones usadas en los scripts de Honeybee- Esta sección te permitirá empezar a expandir de manera independiente tu conocimiento al recorrer la librería de componentes.

La Interfaz de Honeybee
-----------------------

La interfaz de Honeybee organiza los componentes por cada tipo de simulación. La sección 00 es primordialmente par definir la geometría de las zonas en una simulación energética.

![alt text](https://user-images.githubusercontent.com/44324576/49173594-77522d00-f344-11e8-8b38-1faf1714ac00.png)

Las secciones 02-04 son para cálculos de iluminación natural. No utilizaresmos estos componentes en este turorial.

![alt text](https://user-images.githubusercontent.com/44324576/49173589-76b99680-f344-11e8-84e5-aa729d9f1dc8.png)

Las secciones 05-10 son para modelado energético en EnergyPlus. Nos enfocaremos en este tipo de componentes en este tutorial.

![alt text](https://user-images.githubusercontent.com/44324576/49173915-47575980-f345-11e8-8abd-4b181702c279.png)

Los componentes de la sección 11 se emplean para realizar simulaciones en THERM. No utilizaremos estos componentes en este tutorial.

![alt text](https://user-images.githubusercontent.com/44324576/49173595-77522d00-f344-11e8-8b87-9fe09ec4bec0.png)

Los componentes de la sección 12 sirven para actualizar Honeybee y los componentes de la sección 13 son experimentales o están en desarrollo.

![alt text](https://user-images.githubusercontent.com/44324576/49173592-77522d00-f344-11e8-8928-abd3b9476adf.png)

A manera de ejemplo sobre cómo funcionan estos grupos de componentes, consideremos el tutorial en simulaciones energéticas para zona unitaria en EnergyPlus. Este tutorial solamente utiliza componentes de la sección 00, las secciones de energía 05, 06, 07, 08, 09, 10 y la sección de actualización 12. No se utilizan componentes de las secciones 02-04 de iluminación natural, o de la sección 11 de THERM.

![alt text](https://user-images.githubusercontent.com/44324576/49173591-76b99680-f344-11e8-8a88-550f37222797.png)

Ubicando Componentes en Honeybee
--------------------------------

Para ayudarte a localizar componentes, comenzaremos refiriéndonos a ellos usando el nombre de la pestaña de Grasshopper, el nombre o número de la sección y el nombre del componente. Por ejemplo: 'Honeybee|04 Energy Material|Honeybee_EnergyPlus Window Material' significaría que debes buscar en la pestaña 'Honeybee', en la sección 04 que se emplea para especificar materiales en las simulaciones energéticas y finalmente, deberías buscar el nombre 'Honeybee_EnergyPlus Window Material'. También es posible hacer doble clic en el lienzo y escribir 'EnergyPlus Window Material' (sin comillas) y seleccionar de la lista dinámica que aparece.

Si encuentras un componente que no reconoces, hay un par de cosas que puedes hacer:

+ Puedes mover el ratón sobre el ícono en el centro del componente para ver el nombre del componente.

+ Si el componente está fuera de Ladybug y Honeybee, puedes también presionar y sostener ctrl + alt al mismo tiempo para activar el modo informativo. Esto te muestra la ubicación en el menú de los componentes que ya se encuentran en el lienzo. Desafortunadamente, para Ladybug y Honeybee, esto solamente indicará hacia un componente Python.

+ Un método alternativo para componentes dentro de Ladybug y Honeybee es hacer doble clic en el ícono del componente de Ladybug o Honeybee, lo que abrirá el código en su interior. Posteriormente, debes desplazarte hasta encontrar la línea que empieza con 'ghenv.Component.SubCategory =' la cual deberá estar seguida por algo parecido a '07|Energy|Schedule'. Esto funciona de la misma manera que la dirección anterior, así que en este caso sabemos que el componente está ubicado en la pestaña 7 bajo 'Energy' y que se llama Honeybee_Schedule.

+ Si prefieres ver nombres en vez de íconos, también es posible acceder a la pestaña 'Display' en la barra de menú de Grasshopper y modificar la opción 'Display Icons', de manera que se desplegará el nombre del componente en vez del ícono.

+ También es posible hacer doble clic en el lienzo de Grasshopper y empezar a teclear el nombre de un componente para buscar en todas las pestañas de Grasshopper. Todos los componentes de Honeybee y Ladybug incicial ya sea con 'Honeybee' o 'Ladybug', de manera que empezando con alguna de esas palabras clave es una forma de buscar solo dentro de nuestros plugins.

+ Otra herramienta muy útil es el componente 'Bifocals', el cual crea una etiqueta encima de cada componente de manera que sea posible para ti ver tanto el ícono de un componente como su nombre. El componente 'Bifocals' está disponible en <https://www.food4rhino.com/app/bifocals>.

Creando una Definición de Honeybee
----------------------------------

**iii.00** El primer paso para crear cualquier script de Honeybee es *siempre* colocar el componente Honeybee_Honeybee en el lienzo. Esto es importante porque este component contiene múltiples librerías internas que son necesarias para el funcionamiento de casi todos los demás componentes de Honeybee. A diferencia de casi todos los scripts en Grasshopper, no es necesario conectar un cable entre el componente Honeybee_Honeybee y otros componentes; las librerías se activan simplemente al colocarlo en el lienzo. Este componente se localiza en la pestaña '0 Honeybee|Honeybee' y a la acción de colocar este componente en el lienzo se le conoce como 'echar a volar Honeybee'.

![alt text](https://user-images.githubusercontent.com/44324576/49170763-2d197d80-f33d-11e8-96fb-ca46f7fa79df.png)

**iii.01** Muchos componentes de Honeybee funcionan conjuntamente con componentes de Ladybug, así que *casi siempre* es necesario echar también a volar Ladybug. Puedes encontrar el componente Ladybug_Ladybug en la pestaña Ladybug, en la sección 0.

![alt text](https://user-images.githubusercontent.com/44324576/49170767-2db21400-f33d-11e8-8269-ddf02cd3f166.png)

**iii.02** El siguiente paso crucial antes de empezar a crear una simulación es asegurarse que contamos con datos climáticos adecuados en los que se basará nuestra simulación. Para esto requerimos de una conexión a internet. Para empezar, encuentra la sección 0 de Ladybug y arrastra el component 'Open EPD and STAT Weather File' al lienzo.

![alt text](https://user-images.githubusercontent.com/44324576/49170768-2db21400-f33d-11e8-993e-66d13f1727ab.png)

**iii.03** Este componente descargará automáticamente los datos climáticos desde el internet a partir de una URL proporcionada por el usuario. Utilizaremos un componente panel para ingresar la dirección buscada.

![alt text](https://user-images.githubusercontent.com/44324576/49170769-2db21400-f33d-11e8-8461-b6c947b936a5.JPG)

**iii.04** Haz doble clic en el componente panel y pega la siguiente URL, sin espacios antes o después:

+ <https://www.energyplus.net/weather-download/north_and_central_america_wmo_region_4/USA/CA/USA_CA_Van.Nuys.AP.722886_TMY3/all>

Es importante evitar presionar ENTER después de ingresar el texto en el componente panel, ya que Grasshopper interpreta ENTER como la creación de un segunto ítem en la lista de datos dentro del panel. Para aclaraciones sobre listas de datos, consulta el paso 2.20.

Estos datos provienen del Departamento de Energía de los Estados Unidos y corresponden al aeropuerto de Van Nuys, California. Al pasar el cursor sobre este componente es posible obtener más detalles sobre cómo encontrar más datos para otras ubicaciones. De igual manera pueden encontrarse y descargarse directamente del siguiente link: <https://www.energyplus.net/weather>.

El siguiente link contiene información sobre el origen y la generación de estos datos: <https://energyplus.net/weather/sources>.

![alt text](https://user-images.githubusercontent.com/44324576/49170770-2e4aaa80-f33d-11e8-9a83-fa2d5160dc66.JPG)

*Consejo sobre paneles: Utilizaremos paneles para ingresar información frecuentemente. En vez de arrastrar un panel al lienzo cada vez, simplemente haz doble clic en el lienzo y escribe '//' seguido de los datos que quieras introducir en el panel.

**iii.05** Conecta el panel que contiene la URL del archivo de datos climáticos deseados al puerto de entrada 'weatherFileURL' del componente 'Open EPW and STAT Weather Files'. Notarás que el componente 'Open EPW and STAT Weather files' habrá cambiado de naranja a gris, indicando que ha obtenido los datos climáticos sin errores.

![alt text](https://user-images.githubusercontent.com/44324576/49170772-2ee34100-f33d-11e8-8a8f-07541ecf2991.JPG)

**iii.06** Si conectas un panel a la salida 'epwFile' del componente'Open EPW and STAT Weather files' y pasas el cursor por encima del texto 'epwFile', verás que Ladybug ha descargado el archivo EPW y lo ha guardado en tu disco local. La ubicación por defecto es: c:\ladybug.

![alt text](https://user-images.githubusercontent.com/44324576/49170771-2e4aaa80-f33d-11e8-86b7-4748521bbbbf.JPG)

**iii.07** Estos datos climáticos pueden ahora ser usados para múltiples simulaciones. Concluiremos este tutorial demostrando cómo explorar los datos que acabas de importar. Empecemos arrastranto un componente 'Ladybug_Import EPW" hasta el lienzo.

![alt text](https://user-images.githubusercontent.com/44324576/51679914-8c63d900-1fe0-11e9-8200-027a9ceb0b81.JPG)

**iii.08** Posteriormente, conecta los datos que acabamos de descargar a este componente. Esto nos permitirá recorrer los distintos tipos de datos contenidos en el archivo inicialmente importado.

![alt text](https://user-images.githubusercontent.com/44324576/51679917-8cfc6f80-1fe0-11e9-9c08-a4357165722e.JPG)

**iii.09** El componente 'Ladybug_Import EPW' deberá cambiar ahora de naranja a gris, indicando que los datos climáticos fueron recopilados sin errores.

![alt text](https://user-images.githubusercontent.com/44324576/51679916-8cfc6f80-1fe0-11e9-9364-74698dc7f7e0.JPG)

**iii.10** Ahora podemos acceder a los distintos tipos de datos contenidos en el archivo EPW, conectemos paneles a los primeros cuatro datos de salida y demos un vistazo más cercano a la información ahora disponible.

![alt text](https://user-images.githubusercontent.com/44324576/51679915-8c63d900-1fe0-11e9-8f5f-a1c743b7b68d.png

**iii.11** El puerto de salida 'readMe!' provee valiosa información acerca de si el componente funcionó correctamente. Esto es particularmente importante si el componete se vuelve naranja, lo que inidica que hubo un error.

![alt text](https://user-images.githubusercontent.com/44324576/51680591-73f4be00-1fe2-11e9-9106-c303cea225c9.jpg)

*Nota cómo desconectando la dirección URL que hemos ingresado antes afecta estos datos de sallida.

![alt text](https://user-images.githubusercontent.com/44324576/51680758-ea91bb80-1fe2-11e9-8ed5-eb3d7d461fdf.jpg)

**iii.12** La latitud proveerá la latitud en la que los datos fueron recopilados. Esto es extremadamente importante para confirmar la precisión de la geometría solar.

![alt text](https://user-images.githubusercontent.com/44324576/51680593-7525eb00-1fe2-11e9-865d-83531de1f298.jpg)

**iii.13** El siguiente dato de salida provee más información acerca de la ubicación como el nombre de la localidad, latitud, longitud, zona horaria y elevación. La zona horaria es expresada por el número de horas de direfencia desde Greenwich, Reino Unido. Los valores positivos significan este, los valores negativos el oeste. La elevación está en metros sobre el nivel del mar.

![alt text](https://user-images.githubusercontent.com/44324576/51680594-75be8180-1fe2-11e9-97e2-668a53e7c247.jpg)

**iii.14** Todos los datos de salida siguientes contienen datos horarios. Observemos la temperatura de bulbo seco como ejemplo.

Las primeras siete entradas contienen información acerca de los datos, mientras que los siguientes 8760 valores representan una serie de datos para cada una de las horas de un año. La convención para listas en Grasshopper indica que se empiece a numerar en 0, así que una lista de 7 elementos leerá valores desde la posición 0 hasta la 6.

+ El valor 0 es una clave
+ El valor 1 es el nombre de la ubicación
+ El valor 2 es el tipo de datos
+ El valor 3 son las unidades de los datos
+ El valor 4 es la frecuencia a a que fue registrado
+ Los valores 5 y 6 representan el periodo de tiempo sobre el que los datos fueron recopilados. El formato utilizado es mes del año, día del mes y hora del día. Así que podemos ver que estos datos fueron recopilados a partir del primero de enero a la primer hora del día entre 00:00-01:00, hasta el 31 de diciembre en lahora 24 del día, entre las 23:00-00;00

![alt text](https://user-images.githubusercontent.com/44324576/51680596-76efae80-1fe2-11e9-822d-16c10510109e.jpg)

**iii.15** Intenta desplazarte por los 8760 valores arrastrando la barra de desplazamiento color amarillo oscuro (marcada con un gran punto rojo más abajo)

![alt text](https://user-images.githubusercontent.com/44324576/51680597-78b97200-1fe2-11e9-8e26-925981b8416e.jpg)

**iii.16** Finalmente, arrastraremos el componente 'Ladybug_Sunpath' hasta el lienzo para explicar algunas importantes convenciones y para mostrarte cómo puedes usar la interfaz de Ladybug y Honeybee para conocer sobre los componentes disponibles. El componente de trayectoria solar muestra el movimiento del sol a lo largo de un año completo.

![alt text](https://user-images.githubusercontent.com/44324576/51682324-6ee63d80-1fe7-11e9-9421-faf5311f8ceb.JPG

**iii.17** Observa que algunos de los nombres de los datos de entrada para el componente de trayectoria solar son precedidos por un guión bajo, mientras que otros incluyen uno después. Esta es una convención adoptada por Ladybug y Honeybee para distinguir los inputs obligatorios de los opcionales. Si un dato de entrada obligatorio es dejado vacío, el componente no se ejecutará. Nota que aunque el componente de trayectoria solar está en el lienzo, nada aparece en el entorno de modelado en Rhino.

![alt text](https://user-images.githubusercontent.com/44324576/51682973-0ac47900-1fe9-11e9-8d89-cdfbcb40ddef.png)

**iii.18** Una vez que conectamos el dato de salida de la ubicación, desde el componente 'Ladybug_Import EPW' al dato de entrada de ubicación del componente 'Ladybug_SunPath', existe suficiente información para que el componente 'Ladybug_SunPath' se ejecute.

![alt text](https://user-images.githubusercontent.com/44324576/51682979-0c8e3c80-1fe9-11e9-927a-ec5cb6b29399.png)

**iii.19** Ahora deberías ver algo parecido a la siguiente ilustración dentro del entorno de modelado de Rhino. Toma en cuenta que la escala por defecto de este diagrama es de 400 unidades de Rhino, y que será colocado en las coordenadas 0,0,0 por lo que será necesario aplicar un zoom para apreciarlo completamente.

![alt text](https://user-images.githubusercontent.com/44324576/51682958-fed8b700-1fe8-11e9-9389-639f119addbb.jpg)

**iii.20** Podrías haber notado que hay muchos datos de entrada que son precedidos por un guión bajo, pero que aun así se dejan vacíos. De cualquier manera, el componente es ejecutado. Esto sucede porque muchos datos de entrada pueden asumir de manera razonable valores por defecto. No tendría ningún sentido asumir una ubicación por default para la trayectoria solar, ya que la geometría depende enteramente de la latitud de la ubicación del estudio. Sin embargo, uno podría asumir que el periodo de análisis por defecto es un año completo.

**iii.21** Mueve el cursor sobre las distintas áreas del componente para aprender más acerca de los dato de entrada requeridos, suposiciones de cálculo, formatos para la entrada de datos y en ocasiones, inlcuso referncias para publicacioes de investigación en las cuales se basan los cálculos de los componentes.

Esto es lo que observarás al momento de pasar tu cursor sobre los datos de entrada de la ubicación:

![alt text](https://user-images.githubusercontent.com/44324576/51683837-0e58ff80-1feb-11e9-9f9b-449f71302681.JPG)

Esto es lo que verás al pasar tu cursor sobre el centro del componente de trayectoria solar, lo cual aplica dera todo el componente.

![alt text](https://user-images.githubusercontent.com/44324576/51683839-0ef19600-1feb-11e9-8f07-85cdd3627f9d.JPG)

Finalmente, al pasar el cursor sobre uno de los datos de salida:

![alt text](https://user-images.githubusercontent.com/44324576/51683838-0e58ff80-1feb-11e9-9f23-e094a8718f46.JPG)


**iii-22** También es importante mencionar a secuencia con las que los componentes son ejecutados en el lienzo de Grassopper. Los componetes de Grasshopper usualmente son ejecutados en la secuencia con la que fueron colocados y conectados entre si en el lienzo. Así que los componentes mas ordinarios correrían en la siguiente secuecncia;

![alt text](https://user-images.githubusercontent.com/44324576/53178720-b6fe7d00-35f2-11e9-8179-ebfa9c356bcf.png)

Sin embargo, los componentes 'Ladybug_Ladybug' y 'Honeybee_Honeybee *siempre* son ejecutados al principio. Esto es bueno, porque significa que los datos, las funciones y las librerías contenidas en esos dos componentes siempre están accesibles para todos los que se ekjecuten posteriormente. Esto es verdad incluso si un cable *no está conectado*. De esta manera, el veradero orden de cálculo es el siguiente:

![alt text](https://user-images.githubusercontent.com/44324576/53178724-b82faa00-35f2-11e9-8761-0f7477b18c63.png)

Esto nos permite cerrar el círculo hasta la explicación ii.00 más arriba. Usualmente, tienes que conectar un cable entre dos componentes para poder transferir datos entre ellos. Este no es el caso en Honeybee. La librería se hizo disponible porque el componente 'Honeybee_Honeybee' fue ejecutado primero y esto hace posible que se ejecuten múltiples funciones en segundo plano.

A medida que aprendas más acerca de Honeybee, llegarás a comprender algunas de las ventajas de escribir código de esta manera. Por ejemplo, esto facilita crear una librería estándar de materiales de Radiance que puede ser accesada por múltiples definiciones en Grasshopper.

***

Esto concluye la sección de fundamentos de Honeybee. Ahora debes estar familiarizado con:

1. El layout de la interfaz Ladybug y Honeybee
2. La importancia de echar a volar Ladybug y Honeybee
3. Introducir información en un componente panel
4. Descargar datos climáticos
5. Importar datos climáticos
6. Examinar los datos importados
7. La convención de *antes* y *después* para datos de entrada necesarios vs óptimos
8. Aprender acerca de componentes, y datos de entrada y de salida al pasar el cursor por encima de elllos
