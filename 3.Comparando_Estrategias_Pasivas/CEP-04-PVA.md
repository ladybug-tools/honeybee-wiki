# Ventilación - Ventanas Abiertas

En esta sección se muestra un ejemplo simple sobre cómo indicar la ventilación en un modelo de energía.

**4.00** Este módulo esta insertado dentro del script aquí:

![alt text](https://user-images.githubusercontent.com/44324576/52432381-96222c00-2b0a-11e9-9107-22d6dc01e8b9.png)

**4.01** Haciendo un acercamiento podemos observar que el componente de ventilación ofrece distintas opciones. Modelar ventilación es un proceso complejo pero EnergyPlus cuenta con bastantes simplicaciones que no requieren mucho tiempo de cómputo. El punto clave es que es extremadamente importante asignar correctamente el tipo de ventilación. La ventilación natural que este componente modela es mayormente hecho para modelación de zona separada y en casos donde no existe flujo de aire considerable entre zonas. Específicamente este componente puede modelar algunos tipos comúnes de ventilación natural:

  1. Ventilación de Cara-Única - ventilación impulsada por la diferencia de altura a lo largo de ventanas individuales colocadas sobre una sola cara del edificio.
  2. Ventilación Cruzada - ventilación impulsada por la diferencia de presión a lo largo de las ventanas colocadas en dos caras opuestas del edificio.
  3. Ventilación de Chimenea - ventilación impulsada por efecto chimenea/apilamiento conectado a la zona.
  4. Ventilación por Capucha - ventilación impulsada por flujo de aire a través de una capucha de ventilación conectada a la zona.
  5. Ventilación de Abanico -  ventilación de flujo constante impulsada por un abanico.
  
  ![alt text](https://user-images.githubusercontent.com/44324576/52433831-47769100-2b0e-11e9-90d8-bb75513e89b4.png)

*Tomar en cuenta que cada una de las formas de ventilación funciona como un switch on-off. Esto es particularmente importante en lo relacionado a la dirección de viento debido a que EnergyPlus no hace ajustes de viento bloqueado por el contexto a los alrededores, ni ajusta la cantidad de ventilación basada en la orientación de una ventana con respecto a la dirección del viento.* 

**4.02** Coloque su mouse por encima de la terminal _naturalVentilationType para leer más. Como puede observar, estamos modelando Ventilación de Cara Única, la cual es como abrir una sola ventana para un cuarto. Esta es distinta de la ventilación cruzada, la cual ocurre cuando existe una ventana abierta en dos lados opuestos de un cuarto con brisa pasando a través de ellas. 

![alt text](https://user-images.githubusercontent.com/44324576/52435631-a1795580-2b12-11e9-9fd8-ca989490c835.jpg)
