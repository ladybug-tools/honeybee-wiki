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

**5.08** Esto desplegará un menú de opciones como el mostrado debajo, donde podrá cambiar los números de genes a 24 y declarar valores mínimo y máximo de 0 y 1 respectivamente.

![alt text](https://user-images.githubusercontent.com/44324576/52489417-86feb500-2bc2-11e9-8515-01e73ffbff50.jpg)

**5.09** Finalmente asignaremos el nombre del Programa. No se deben utilizar espacios en el nombre, esto es importante debido a que los Programas de Horario de Uso son manejadas de forma distinta de muchos otros tipos de datos en Grasshopper. Estos son guardados como archivos de texto, llamados archivos IDF, para ser usados a través de Grasshopper posteriormente. Por esta razón es que se observa la salida 'schedIFText'.

![alt text](https://user-images.githubusercontent.com/44324576/52489023-81ed3600-2bc1-11e9-9d28-b5e2c7168992.jpg)

**5.10** Se puede observar que Grasshopper únicamente traslada el nombre del archivo IDF al conectarse un panel a la salida *schedule*.

![alt text](https://user-images.githubusercontent.com/44324576/52489024-81ed3600-2bc1-11e9-82a7-92b2bbda53af.jpg)

**5.11** Finalmente especificaremos el tamaño de las ventanas operables para la purga nocturna. Escribimos '1' con fines demostrativos, lo cual asume que el área de la ventana se abre completamente. En realidad esto representaría una ventana con bisagras que pueda girarse y abrirse completamente, opuesta a una ventana corrediza la cual no puede tener más del 50% de su área abierta.

![alt text](https://user-images.githubusercontent.com/44324576/52489025-81ed3600-2bc1-11e9-8781-8c948a26dbcc.jpg)

**5.12** Aquí se muestra el Diagrama de Balance de Energía resultante. Se puede notar que ahora todo el enfriamiento es atribuido a ventilación natural.

![alt text](https://user-images.githubusercontent.com/44324576/52487702-764c4000-2bbe-11e9-825a-b94dcb93cb4f.jpg)

**5.13** Revisitando la gráfica de confort creada en el paso 4 de la sección ventilación natural, hemos añadido ahora el impacto de la purga nocturna en el confort general. Se puede observar que se han disminuido considerablemente el número de horas en las que el inmueble esta muy caliente, pero ahora igualmente está muy frío para ser confortable durante una parte significativa del año.

![alt text](https://user-images.githubusercontent.com/44324576/52487737-95e36880-2bbe-11e9-8f0d-b4f8883b2a92.gif)

Esto concluye la sección comparativa de las estrategias pasivas. Esta sección tiene la intención de proveer un paso intermedio entre la modelación de Zona Unitaria y la modelación Avanzada de Multi-Zonas. Hasta este punto deberán estar familiarizados con los siguientes procesos:

  * Añadir y remover capas de información/simulación a las Zonas de Honeybee.
  * Especificar contexto de sombreado.
  * Cambiar el desempeño de las especificaciones de ventanas.
  * Cambiar las cargas de equipos específicas de una Zona de Honeybee.
  * Introducir ventilación natural dentro de la zona.
  * Crear y asignar programas de horario de uso de equipos.
  
  











