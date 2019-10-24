# Programa - Purga Nocturna

**5.00** La estrategia final que compararemos en esta guía inicial es la purga nocturna. Al igual que antes, se añadirá como un elemento más a las capas de información encadenada en las zonas de salida de ventilación natural de Honeybee.

![alt text](https://user-images.githubusercontent.com/44324576/52487947-15713780-2bbf-11e9-9a2a-45c631d04174.png)

**5.01** Acercándonos podemos ver que la Purga Nocturna usa exactamente el mismo componente que las Ventanas Abiertas, el componente Honeybee_Set EP Air Flow. Tomar en cuenta que aún así se usará otro tipo de flujo de aire en esta opción. Otra distinción clave es que se asignará un Programa de Horario de Uso, lo cual es una forma de informar a Energy+ que solamente se desea que ocurran estos cambios durante un tiempo específico.

![alt text](https://user-images.githubusercontent.com/44324576/52489139-c4167780-2bc1-11e9-96bb-b142796f297d.png)

**5.02** Para construir este módulo se debe iniciar con el componente Honeybee_Set EP Air Flow.

![alt text](https://user-images.githubusercontent.com/44324576/52489017-81549f80-2bc1-11e9-8322-7d0d6f8f63cb.jpg)

**5.03** Se especificará la ventilación natural tipo 3.

![alt text](https://user-images.githubusercontent.com/44324576/52489019-81549f80-2bc1-11e9-9ede-1fcc8113f6d6.jpg)

**5.04** Si se coloca el *mouse* por encima de la terminal de ventilación natural se podrá observar que el tipo '3' corresponde a ventilación de abanico. Por lo tanto, esta estrategia asume el flujo de aire es hecho por un ventilador eléctrico. Esta forma de ventilación es más confiable que simplemente abriendo las ventanas, pero hay un costo asociado al uso del ventilador por sí mismo. La simulación evaluará solamente el potencial de ganancia térmica al aplicar esta estrategia pero existe además otra capa de complejidad relacionada con la modelación del consumo de electricidad del abanico.

![alt text](https://user-images.githubusercontent.com/44324576/52489783-73a01980-2bc3-11e9-9e9c-626146fb6e9d.jpg)

**5.05** El siguiente paso es declarar en Energy+ cuando queremos encender el ventilador, esto requiere un programa de uso horario. Existen diferentes tipos de agendas en Honeybee, las cuales son útiles de forma anual, estacional, semanal y diaria. En este caso crearemos un programa personalizado que se repite exactamente igual diariamente durante todo el año y lo usaremos para modificar el tamaño de las aperturas de las ventanas por las que el aire soplará. Por ahora, se iniciará con el componente Honeybee_Constant Schedule.

![alt text](https://user-images.githubusercontent.com/44324576/52489020-81ed3600-2bc1-11e9-9027-adee45d27454.jpg)

**5.06** El siguiente paso es asignar el valor que representa el tamaño de la apertura del flujo de aire en cada hora del día. Esto es hecho usando el componente Gene Pool.

![alt text](https://user-images.githubusercontent.com/44324576/52490045-25d7e100-2bc4-11e9-973d-14b2fa31f0a0.jpg)

**5.07** Cuando se arrastra por primera vez el componente Gene Pool en el *canvas* se mostrarán solamente 9 valores. Deberá editar el componente Gene Pool haciendo click derecho sobre él y seleccionando 'edit'.

![alt text](https://user-images.githubusercontent.com/44324576/52489416-86feb500-2bc2-11e9-8376-c38e9e6b0ce2.jpg)

**5.08** Esto desplegará un menu de opciones como el mostrado debajo, donde podrá cambiar los números de genes a 24 y declarar valores mínimo y máximo de 0 y 1 respectivamente.

![alt text](https://user-images.githubusercontent.com/44324576/52489417-86feb500-2bc2-11e9-8515-01e73ffbff50.jpg)
