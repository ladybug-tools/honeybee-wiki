Las elecciones de materiales tienen un gran impacto en el rendimiento energético. Esta sección ilustrará como Honeybee maneja los materiales modelando ventanas de alto rendimiento.

**1.01** Aquí una descripción general de todos los módulos que agregaremos a lo largo del capítulo sobre Técnicas Pasivas. Se basa directamente en el modelo de zona única que creamos antes. A continuación, los elementos originales aparecen en grupos de color gris y los elementos nuevos aparecen en amarillo.

![gh_000_overview](https://user-images.githubusercontent.com/44324576/52227404-b6a27a00-28af-11e9-8839-6854e4e642e5.png)

**1.02** Acercándonos, puedes ver que crearemos una construcción para una ventana de alto rendimiento, y la conectaremos al componente Honeybee_addHBGlz. Esto reemplazará la suposición por defecto sobre el acristalamiento con nuestras especificaciones para una ventana de alto rendimiento. 

![gh_001_passive 1](https://user-images.githubusercontent.com/44324576/52228338-6b3d9b00-28b2-11e9-8cea-4fc05f449fbb.png)

**1.03** Acercándonos aún más, ahora veremos el proceso de creación de una construcción de ventanas de alto rendimiento. 
![gh_002_passive 1](https://user-images.githubusercontent.com/44324576/52228340-6c6ec800-28b2-11e9-9b8c-02ada07437d0.png)

**1.04** Comenzamos con el componente de construcción Honeybee_EnergyPlus. Una construcción Energy Plus podría ser un solo material en una sola capa (es decir, hormigón sólido) o podría ser un material compuesto (es decir, una estructura de montantes con yeso y aislamiento en el interior). Lo importante es que solo puede tener una construcción por superficie de zona. En este caso, estamos creando una ventana y ya hemos especificado las superficies que pretendemos usar (observe el componente 'House Windows' en la imagen del paso **1.02**).
![gh_02_hpwindow_0000_01](https://user-images.githubusercontent.com/44324576/52409824-e41d3c80-2ad6-11e9-993a-b7d7f5910c4b.jpg)
_Observa que puedes agregar capas adicionales a una construcción EP haciendo zoom en el componente en Grasshopper hasta que veas los signos más / menos en blanco y negro al lado de los terminales, como en la imagen a continuación:_

![add layers](https://user-images.githubusercontent.com/44324576/52410725-89391480-2ad9-11e9-9e8e-34057df18d72.JPG)


**1.05** Ahora necesitamos agregar capas de material a esta construcción. Honeybee contiene una variedad de componentes para especificar materiales (ver pestaña 06 | Energía | Materiales) que se pueden añadir como capas a una Construcción EP. La forma más sencilla de modelar una ventana es usar el Material de Ventana de EnergyPlus, que está destinado a describir un conjunto de ventana completo. Esto facilita la conexión de valores de fabricantes que describen una ventana completa en lugar de un material específico.
![gh_02_hpwindow_0001_02](https://user-images.githubusercontent.com/44324576/52409825-e41d3c80-2ad6-11e9-80c7-7ce489dc8662.jpg)

_Aquí hay una vista previa del Menú de Materiales de Honeybee:_ 
![hp windows materials](https://user-images.githubusercontent.com/44324576/52495175-32623680-2bd0-11e9-95ae-c3eafbb3b9d8.JPG)


**1.06** Asigne el valor U como 2, el Coeficiente de Ganancia de Calor Solar como 0.25 y la Transmitancia Visible de la ventana como 0.55. El valor U es una medida de aislamiento, el Coeficiente de Ganancia de Calor Solar es una medida de cuánta energía solar pasa a través del vidrio, y la Transmitancia Visible es una medida de cuánta luz visible pasa a través de la ventana.

_Observe la distinción entre **Transmitancia**, que es la relación de medida de la luz con una incidencia normal, frente a **transmisividad**, que es la relación de la luz total que pasa a través del cristal. No estamos usando Radiance aquí, pero los parámetros de acristalamiento de Radiance requiren transmisividad y los fabricantes de acristalamientos suelen citar la transmitancia._
![gh_02_hpwindow_0002_03](https://user-images.githubusercontent.com/44324576/52409826-e4b5d300-2ad6-11e9-80fd-553f3f038ad3.jpg)

**1.07** Ahora podemos conectar esta construcción al componente Honeybee_AddHBGlz para asignar el material a las ventanas que modelamos. ![gh_001_passive 1](https://user-images.githubusercontent.com/44324576/52228338-6b3d9b00-28b2-11e9-8cea-4fc05f449fbb.png)

**1.08** Vuelva a ejecutar la simulación haciendo clic en el botón de inicio falso y examine el Diagrama de Equilibrio de Energía. Como puede ver a continuación, cuando comparamos el Diagrama de Equilibrio de Energía de la casa con y sin la ventana de alto rendimiento, reduce significativamente la ganancia de calor solar.
![001_nostrategyvshighperformancewindow](https://user-images.githubusercontent.com/44324576/52350919-e2496f80-2a29-11e9-9614-7e161f37bb3c.gif)

