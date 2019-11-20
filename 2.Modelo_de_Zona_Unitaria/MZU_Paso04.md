Paso 04 - Visualizar los resultados
=========================================

Ahora recorreremos el proceso de visualización de datos en un diagrama de balance de calior como el que se muestra a continuación. Este diagrama analiza cómo el calor entra y sale de una zona de nuestro edificio. 

![alt text](https://user-images.githubusercontent.com/44324576/49155416-2c6fef80-f31b-11e8-88c3-f52a9aa72e7b.JPG)

*Las simulaciones energéticas obedecen la Primera Ley de la Termodinámica, la cual establece que la energía no puede ser creada ni destruida. Este diagrama resume las fuentes de calor entrando y saliendo de una zona. El calor que entra en una zona puede incluir el emitido por los ocupantes, por computadoras o electrodomésticos, por luminarios, el calor solar entrando por las ventanas y el calor  de los sistemas de calefacción como radiadores. Las pérdidas de calor de una zona pueden ser el resultado de la conducción a través del envolvente, aire frío colándose entre los muros, o ventilación deliberada. Todo lo que se observa sobre el nivel del cero es calor entrando a la zona, todo lo que está debajo de este nivel es calor saliendo de la zona. Estos valores siempre deben ser iguales.*

Paso a paso
-----------

Dirijamos nuestra atención ahora a la parte final del script del archivo de ejemplo:

![alt text](https://user-images.githubusercontent.com/44324576/51702111-3f4d2a80-2013-11e9-914b-3d89486dcae1.png)

**4.00** Empecemos con el archivo resultado del paso 3.

![alt text](https://user-images.githubusercontent.com/44324576/49261762-d8145f00-f443-11e8-975a-008cede152bb.jpg)

**4.01** El archivo de resultados es un enorme documento de valores separados por comas, así que usamos el componente "Honeybee-10Honeybee_Read EP Results" para separar cada uno de los resultados de la simulación que nos interesa analizar.

![alt text](https://user-images.githubusercontent.com/44324576/49261765-d8145f00-f443-11e8-86a5-7b3ae9944bf7.jpg)

**4.02** Podemos observar que cada uno de estos resultados contiene 8767 valores. Las primeras 7 posiciones de esta línea son 0)la clave, 1)la ubicación, 2)el tipo de datos, 3)las unidades, 4)la frecuencia, 5)la fecha inicial (mes, día, hora) y 6) la fecha final (Mes, Día, Hora). Las restantes 8760 posiciones corresponden a cada hora del año.

![alt text](https://user-images.githubusercontent.com/44324576/49261766-d8145f00-f443-11e8-9266-c71de5ba6e1e.jpg)

**4.03** Estos resultados horarios son compilados en el componente "Honeybee_Construct Energy Balance".

![alt text](https://user-images.githubusercontent.com/44324576/49261768-d8acf580-f443-11e8-8391-aec7d34d67bf.jpg)

**4.04**  Este componente también requiere que sean conectadas las zonas que creamos en el paso 2 para asociar los resultados a las zonas de interés.

![alt text](https://user-images.githubusercontent.com/44324576/49261771-d8acf580-f443-11e8-9cc0-5fc342c1da95.jpg)

**4.05** Aunque ya tenemos las zonas y la cantidad de calor entrando y saliendo del edificio, todavía no tenemos la información necesaria para identificar las contribuciones de cada una de las superficies de cada zona. Para esto, necesitamos el componente "Honeybee-10-Honeybee_Read EP Surface Results".

![alt text](https://user-images.githubusercontent.com/44324576/49261774-d8acf580-f443-11e8-863d-a4e55aac2d39.jpg)

**4.06** Para describir lo que este componente está haciendo, utilizaremos el componente "Param Viewer" (disponible en la sección "utilities" de la pestaña "Param"). Enseguida, conectamos un componente "Param Viewer" al nodo de salida "FlrNormBalWStorage" del componente "Construct Energy Balance". Igualmente, conectamos otro al nodo de salida "cooling" del componente "Honeybee_Read EP Result".

![alt text](https://user-images.githubusercontent.com/44324576/49263166-a69e9200-f449-11e8-88b0-c15e63230cfc.jpg)

*El componente "Param Viewer" nos indica cuántas listas están contenidas en los datos de salida, y cuántos objetos hay en cada lista. Podemos apreciar que los datos horarios de refrigeración (cooling) es una sola lista de 8767. No obstante, la salida del componente "Honeybee_Construct Energy Balance" contiene 10 listas con 8767 valores cada una. Estas listas colectan todas las otras listas en una lista de listas. Estas 10 listas representan 0)calefacción, 1)solar, 2)equipos, 3)iluminación, 4)ocupantes, 5)infiltración, 6)ventilación mecánica, 7)conducción por elementos opacos, 8)enfriamiento y 9)almacenamiento de calor. Es necesario notar que la numeración inicia en 0 debido a que esta es la convención en la mayoría de los lenguajes de programación.*

**4.07** Para visualizar los datos de manera mensual, utilizaremos el componente "Ladybug_Average data" para hacer la conversión:

![alt text](https://user-images.githubusercontent.com/44324576/49261775-d9458c00-f443-11e8-8595-23a481ea0037.jpg)

**4.08** Debemos observar que cada una de las listas que antes contenía 8767 valores ahora contiene solamente 19 valores (7 para la información sobre los datos y 12 para cada mes del año).

![alt text](https://user-images.githubusercontent.com/44324576/49261776-d9458c00-f443-11e8-9854-808b08799e80.jpg)

**4.09** Finalmente, tenemos todos los datos en el formato correcto para un gráfico de barras mensuales. Ahora, arrastramos un componente "Ladybug_Monthly Bar Chart" al lienzo.

![alt text](https://user-images.githubusercontent.com/44324576/49261778-db0f4f80-f443-11e8-85a7-5c23426152b2.jpg)

**4.10** Usamos un seleccionador booleano en la posición "True" para compilar los datos en el gráfico.

![alt text](https://user-images.githubusercontent.com/44324576/49261780-dba7e600-f443-11e8-97c4-a5a47859f3c8.jpg)

**4.11** Usamos un panel para etiquetar el eje Y con "Energy Intensity (kWh/m2)".

![alt text](https://user-images.githubusercontent.com/44324576/49261782-dcd91300-f443-11e8-8a6e-919ae8e2ebdc.jpg)

**4.12** Usamos otro panel para definir el punto base del gráfico en (70,0,0).

![alt text](https://user-images.githubusercontent.com/44324576/49261783-dcd91300-f443-11e8-8a86-082c5c429e30.jpg)

**4.13** Finalmente, ajustamos el color del gráfico usando un componente "Ladybug_Legend Parameters".

![alt text](https://user-images.githubusercontent.com/44324576/49261784-dd71a980-f443-11e8-96b5-0518d14ca523.jpg)

**4.14** Tomamos el elemento 19 de la librería de gradientes de Ladybug, el cual ha sido diseñado para visualizaciones de balances energéticos.

![alt text](https://user-images.githubusercontent.com/44324576/49261785-dd71a980-f443-11e8-8240-763c8213bf08.jpg)

**4.15** El espacio de modelado de Rhino ahora deberá contener el gráfico de balance de calor.

![alt text](https://user-images.githubusercontent.com/44324576/49264216-b0c28f80-f44d-11e8-9cfd-f0d9a04d6e02.jpg)

Esto representa la simulación de un modelo sumamente sencillo, como se muestra debajo. Aún no hemos definido el contexto.

![alt text](https://user-images.githubusercontent.com/44324576/51697197-8c2b0400-2007-11e9-9128-c2c75db22a02.jpg)

**4.16** A manera de desmostración, intenta desconectar el cable resaltado abajo. Esto removerá los cálculos de superficie del diagrama del balance de calor. De manera sencilla, esto equivale a remover el componente de la simulación que considera el calor conducido a través de cada superficie en la zona, lo que significa que todo el calor que la simulación esera que sea conducido a través de los muros ahora aparece como si estuviera siendo almacenado en el material.

![alt text](https://user-images.githubusercontent.com/44324576/49264180-883a9580-f44d-11e8-8198-640cb9f03d64.jpg)

**4.17** Observemos que el componente de almacenamiento en el diagrama del balance de calor es significativamente más grande ahora. El componente de almacenamiento se refiere a la energía almacenada en la masa del edificio. Si hemos llenado todos los términos del balance de calor en el componente "Honeybee_Construct Energy Balance", el almacenamiento ubiese sido muy pequeño comparado con los otros términos. Este valor de almacenamiento es una buena manera de revisar que todos los términos en tu balance de calor hayan sido considerados.

![alt text](https://user-images.githubusercontent.com/44324576/49264238-c9cb4080-f44d-11e8-9461-aa8ab38956fc.jpg)

Esto concluye la sección sobre la creación del modelo de zona unitaria.

Ahora deberás estar familiarizado con los conceptos siguientes:

...1. Crear zonas con ventanas en Honeybee
...2. Añadir datos climáticos con Ladybug
...3. Especificar los datos de salida deseados para OpenStudio
...4. El rol del archivo OSM en la comunicación entre Honeybee y OpenStudio
...5. Leer los datos producidos por el archivo de resultados
...6. Cómo convertir datos horarios en datos mensuales promedio
...7. Cómo crear un diagrama de balance de calor
