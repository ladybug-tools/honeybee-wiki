# Ventilación - Ventanas Abiertas

En esta sección se muestra un ejemplo simple sobre cómo indicar la ventilación en un modelo de energía.

**4.00** Este módulo esta insertado dentro del script aquí:

![alt text](https://user-images.githubusercontent.com/44324576/52432381-96222c00-2b0a-11e9-9107-22d6dc01e8b9.png)

**4.01** Haciendo un acercamiento podemos observar que el componente de ventilación ofrece distintas opciones. Modelar ventilación es un proceso complejo pero EnergyPlus cuenta con diversas simplificaciones que no requieren mucho tiempo de cómputo. El punto clave es que es extremadamente importante asignar correctamente el tipo de ventilación. La ventilación natural que este componente modela es mayormente hecho para modelación de Zona Separada y en casos donde no existe flujo de aire considerable entre zonas. Específicamente este componente puede modelar algunos tipos comúnes de ventilación natural:

  1. Ventilación de Cara-Única - ventilación impulsada por la diferencia de altura a lo largo de ventanas individuales colocadas sobre una sola cara del edificio.
  2. Ventilación Cruzada - ventilación impulsada por la diferencia de presión a lo largo de las ventanas colocadas en dos caras opuestas del edificio.
  3. Ventilación de Chimenea - ventilación impulsada por efecto chimenea/apilamiento conectado a la zona.
  4. Ventilación por Capucha - ventilación impulsada por flujo de aire a través de una capucha de ventilación conectada a la zona.
  5. Ventilación de Abanico -  ventilación de flujo constante impulsada por un abanico.
  
  ![alt text](https://user-images.githubusercontent.com/44324576/52433831-47769100-2b0e-11e9-90d8-bb75513e89b4.png)

*Tomar en cuenta que cada una de las formas de ventilación funciona como un switch on-off. Esto es particularmente importante con relación a la dirección de vient, debido a que EnergyPlus no hace ajustes del viento bloqueado por el contexto en los alrededores, ni ajusta la cantidad de ventilación basada en la orientación de una ventana con respecto a la dirección del viento.* 

**4.02** Coloque su mouse por encima de la terminal _naturalVentilationType para leer más. Como puede observar, estamos modelando Ventilación de Cara Única, lo cual consiste en abrir una sola ventana para un cuarto. Esta es distinta de la ventilación cruzada, la cual ocurre cuando existe una ventana abierta en dos lados opuestos de un cuarto con brisa pasando a través de ellas. 

![alt text](https://user-images.githubusercontent.com/44324576/52435631-a1795580-2b12-11e9-9fd8-ca989490c835.jpg)

**4.03** Al comparar los Diagramas de Balance de Energía podemos observar que el efecto de abrir las ventanas es aparentemente nulo en la cantidad de energía que entra en el edificio. Este es un comentario que esta relacionado más con la utilidad de usar Diagramas de Balance de Energía que con la efectividad del uso de ventilación natural. La ventilación natural no previene a la energía solar de entrar en la zona, esta solamente retira el calor una vez que está ahí. Por lo tanto, el impacto de la ventilación natural aparece como el cambio del balance de la energía saliendo de la zona, en la mitad inferior del diagrama de balance de energía.

![alt text](https://user-images.githubusercontent.com/44324576/52435462-3465c000-2b12-11e9-98e4-19c909b93399.gif)

*Tomar en cuenta que la energía removida de la zona por ventilación aparece como 'storage'. Esto es debido a que no se ha conectado aún la ventilación natural con el componente Honeybee_Construct Energy Balance del Modelo de Zona Separada original, ver debajo el componente en verde:*

![alt text](https://user-images.githubusercontent.com/44324576/52437574-852be780-2b17-11e9-9432-f299c91472c9.jpg)

**4.04** La gráfica de temperaturas exteriores nos indica cuando la ventilación natural está realmente occurriendo. Para esto se puede utilizar Ladybug en la visualización de las implicaciones al introducir temperaturas min/max visto en el paso **4.01**. Debajo se presenta una gráfica con todas las horas anuales. Los días aparecen en el eje horizontal y cada sección vertical representa 24 horas. La gráfica muestra la fluctuación de temperaturas en Enero y Diciembre.

![alt text](https://user-images.githubusercontent.com/44324576/52436054-89560600-2b13-11e9-8087-304579af9e2b.jpg)

**4.05** La siguiente gráfica es idéntica a la presentada arriba, con la excepción que esta muestra el año completo. En la primer imagen están todas las horas del año con gradiente de colores basado en las temperaturas. La segunda imagen expone solamente las horas en las que la temperatura exterior está por encima de 12°C, y en la imagen final aparecen solamente las horas en las que existe un potencial uso de ventilación natural basados en este criterio.

![alt text](https://user-images.githubusercontent.com/44324576/52436707-3f6e1f80-2b15-11e9-8004-bf9d1a382078.gif)

**4.06** Esta gráfica puede ser creada usando los componentes de Ladybug. Prestar atención especial al enunciado condicional de entrada para la gráfica Ladybug_3D y podrá crear igualmente una gráfica de gradiente en negro al conectar con dos *black swatches* en la entrada customColors del componente Ladybug_Legend Parameters. Más ejemplos sobre personalización en la visualización de datos pueden encontrarse aquí:http://hydrashare.github.io/hydra/viewer?owner=mostaphaRoudsari&fork=hydra_1&id=Customize_weather_data_visualization_with_3D_Chart&slide=0&scale=1&offset=0,0

![alt text](https://user-images.githubusercontent.com/44324576/52436944-e783e880-2b15-11e9-8cc5-8ea4f309681c.png)

*Tomar en cuenta que se han ocultado las conexiones de estos componentes en la vista general del diagrama, por limpieza y legibilidad. Para esto simplemente se hace click derecho en la terminal y seleccionar 'Hidden' de la lista desplegable*.

![alt text](https://user-images.githubusercontent.com/44324576/52437724-e2279d80-2b17-11e9-9204-3482033d707a.JPG)

**4.07** Finalmente queremos evaluar realmente estas estrategias en términos de su impacto en el confort del espacio interior. Para hacer esto necesitaremos usar el modelo de confort adaptativo y graficar los resultados. Esto se encuentra localizado cerca del final de la definición:

![alt text](https://user-images.githubusercontent.com/44324576/52441180-52d2b800-2b20-11e9-85a7-2654e114c562.png)

**4.08** Acercándonos podemos observar que el componente Ladybug_Adaptive Comfort requiere de diversas fuentes de datos. La temperatura de bulbo seco y la temperatura media radiante son resultados de nuestra simulación. También se requiere la temperatura exterior debido a que, como se explicó en la sección introductoria de los modelos de confort, el confort adaptativo está basado en la experiencia inmediata de los ocupantes y por lo tanto para su cálculo es necesario de un registro de la temperatura exterior.

![alt text](https://user-images.githubusercontent.com/44324576/52441428-cecd0000-2b20-11e9-9c28-60dd9e8ea861.png)

**4.09** Aquí se muestran dos gráficos con resultados, los cuáles comparan un escenario inicial sin aplicar ninguna de las estrategias con un escenario aplicando solamente ventilación natural.

![alt text](https://user-images.githubusercontent.com/44324576/52441922-418aab00-2b22-11e9-858f-c2ad86d5598e.gif)


