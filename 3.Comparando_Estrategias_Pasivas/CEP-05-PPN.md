# Programa - Purga Nocturna

**5.00** La estrategia final que compararemos en esta guía inicial es la purga nocturna. Al igual que antes, se añadirá como un elemento más a las capas de información encadenada en las zonas de salida de ventilación natural de Honeybee.

![alt text](https://user-images.githubusercontent.com/44324576/52487947-15713780-2bbf-11e9-9a2a-45c631d04174.png)

**5.01** Acercándonos podemos ver que la Purga Nocturna usa exactamente el mismo componente que las Ventanas Abiertas, el componente Honeybee_Set EP Air Flow. Tomar en cuenta que aún así se usará otro tipo de flujo de aire en esta opción. Otra distinción clave es que se asignará un Programa de Horario de Uso, lo cual es una forma de informar a Energy+ que solamente se desea que ocurran estos cambios durante un tiempo específico.

![alt text](https://user-images.githubusercontent.com/44324576/52489139-c4167780-2bc1-11e9-96bb-b142796f297d.png)

**5.02** Para construir este módulo, se debe iniciar con el componente Honeybee_Set EP Air Flow.

![alt text](https://user-images.githubusercontent.com/44324576/52489017-81549f80-2bc1-11e9-8322-7d0d6f8f63cb.jpg)

**5.03** Se especificará la ventilación natural tipo 3.

![alt text](https://user-images.githubusercontent.com/44324576/52489019-81549f80-2bc1-11e9-9ede-1fcc8113f6d6.jpg)

**5.04** Si se coloca el *mouse* por encima de la terminal de ventilación natural se podrá observar que el tipo '3' corresponde a ventilación por abanico. Por lo tanto, esta estrategia asume el flujo de aire es hecho por un ventilador eléctrico. Esta forma de ventilación es más confiable que simplemente abriendo las ventanas, pero hay un costo asociado al uso del ventilador por sí mismo. La simulación evaluará solamente el potencial de ganancia térmica al aplicar esta estrategia, existe además otra capa de complejidad relacionada con la modelación del consumo de electricidad del abanico.

![alt text](https://user-images.githubusercontent.com/44324576/52489783-73a01980-2bc3-11e9-9e9c-626146fb6e9d.jpg)
