Paso 0 - Modelando la Geometría de la Zona
==========================================

El motor de cálculo EnergyPlus posee convenciones preestablecidas para la creación de la geometría de una zona. Esta sección muestra cómo caracterizan una casa unifamiliar utilizando una sola zona, así como la manera de describir la misma casa usando un método más elaborado empleando múltiples zonas. La primera sección se enfoca en crear la geometría de la zona, seguida de notas adicionales que son requeridas para crear modelos con múltiples zonas.

**0.01** Aquí está el proyecto de ejemplo que analizaremos:

![alt text](https://user-images.githubusercontent.com/44324576/48569753-de162600-e902-11e8-9be4-cc85de7eee54.jpg)

**0.02** En un modelo energético simplificado, la casa entera puede ser tratada como una zona unitaria:

![alt text](https://user-images.githubusercontent.com/44324576/48569892-38af8200-e903-11e8-8f9e-eed633a5f163.jpg)

**0.03** Un modelo más elaborado definiría cada cuarto como una zona independiente:

![alt text](https://user-images.githubusercontent.com/44324576/48569893-39e0af00-e903-11e8-8f5c-1916fd4197d7.jpg)

**0.04** Las zonas adyacentes deben ser coplanares.

![alt text](https://user-images.githubusercontent.com/44324576/48576313-7bc62100-e914-11e8-9b86-43e400a65c90.jpg)

**0.05** Cada zona debe ser una forma en 3D completamente cerrada.

![alt text](https://user-images.githubusercontent.com/44324576/48571288-c5a80a80-e906-11e8-9341-3ceb166c3f79.jpg)

**0.06** Cada superficie de cada zona se modela como un plano, el cual puede ser posteriormente nombrado y caracterizado con propiedades específicas.

![alt text](https://user-images.githubusercontent.com/44324576/48571833-27b53f80-e908-11e8-82b0-4592fae18767.jpg)

**0.07** Las ventanas y puertas son representadas como superficies. Serán asignadas como "pertenecientes" a una de las superficies de la zona y deberán ser coplanares con esta superficie. Las ventanas y las puertas no deberán compartir vértices o lados con la geometría de la zona.

![alt text](https://user-images.githubusercontent.com/44324576/48570921-c68c6c80-e905-11e8-8a0b-786f44afddfb.jpg)

Requerimientos para Análisis con Zonas Múltiples
------------------------------------------------

**0.08** Las zonas adyacentes deberán tener idénticas áreas. Esto crea un problema para tres superficies en nuestro ejemplo. En la imagen mostrada abajo, identifica 1) un muro de la zona 5 es compartido con la zona 1 y con la zona 2, 2) un muro de la zona 3 es compartido con la zona 5 y con la zona 4, 3) un muro en la zona 5 es compartido con la zona 6 y con la zona 7.

![alt text](https://user-images.githubusercontent.com/44324576/48578327-a23a8b00-e919-11e8-987e-8231ff0f23f9.jpg)

**00.09** Es importante que las superficies que toquen más de una zona sean divididas en la intersección con cada zona. De otra manera, existirá un error de alineación en el cálculo del área de superficie para el calor saliendo de las zonas 1 y 2 versus el calor que llega a la zona 5.

![alt text](https://user-images.githubusercontent.com/44324576/48577773-4a4f5480-e918-11e8-9614-fd894bf00c0f.jpg)

*Nota:* El componente Honeybee | 0 Honeybee | Solve Adjacencies está diseñado para ajustar la geometría de la zona para hacer esto automáticamente. La siguiente sección *Asignando Propiedades a las Zonas* explica este componente en mayor detalle.

**00.10** Esto puede solucionarse dibujando una poli-línea alrededor de la base de la zona 5, incluyendo un punto de control extra en la unión de las zonas 1 y 2, y posteriormente extruyendo esa poli-línea como un sólido.

![alt text](https://user-images.githubusercontent.com/44324576/49099463-cda26b80-f271-11e8-85de-ce351ff72259.jpg)

**00.11** Al describir la geometría de las superficies de un edificio en EnergyPlus, todas las superficies son tratadas como un plano simple sin espesor. Esto crea algunas complicaciones acerca de dónde debe modelarse la superficie 2D en relación con el muro 3D. La documentación de EnergyPlus sugiere utilizar las dimensiones exteriores para las soperficies exteriores y las dimensiones a centro de muro para la geometría interipr. Esto genera geometría completamente conectada con una apropiada cantidad de área de piso, volumen de zona y masa térmica. Observa la relación entre la línea roja representado xonas y las líneas negras representando muros en el siguiente diagrama:

![alt text](https://user-images.githubusercontent.com/44324576/51616959-7c3df200-1f2b-11e9-932d-867f4afe6587.jpg)

*Nota que el espesor de los materiales asignados a las superficies del edificio solamente es utilizado para el cálculo de la conducción de calor y de masa térmica. Para la mayoria de los edificios, la diferencia es pequeña y podrá usarse las dimensiones que sean más convenientes. Si así se desea, el volumen de la zona y el área de piso pueden ser sobreescritos en el objeto de zona directamente. Para edificios con muros realmente gruesos, como por ejemplo edificios antiguos de piedra o ladrillo, se recomienda utilizar dimensiones a centro de muro para todas las superficies (interiores y exteriores) a manera que el edificio tenga la cantidad correcta de masa térmica.

**00.12** Al crear geometría extruyendo curvas cerradas en Rhino, asegúrate al 100% de que no existan orillas traslapándose. Esto resultará en errores, como zonas con áreas imposiblemente grandes para su volumen. Los cálculos de transferencia de calor dependen del área de las superficies, así que esto creará errores en el análisis.

![alt text](https://user-images.githubusercontent.com/44324576/48574730-3b64a400-e910-11e8-8a96-03959e2668c3.jpg)

**00.13** Las zonas también pueden ser representadas por geometría curvada. Sin embargo, las curvas serán simplificadas en superficies planas y cada superficie adicional incrementa el número de cálculos que EnergyPlus debe realizar para describir el comportamiento térmico de la zona. Se recomienda que simplifiques la geometría curvada con geometría segmentada con áreas equivalentes, como se muestra en el siguiente diagrama:

![alt text](https://user-images.githubusercontent.com/44324576/51614761-a345f500-1f26-11e9-9c02-80a9f96d70d0.jpg)

**00.14** El modelado de atrios (como la zona en azul en la imagen más abajo) en EnergyPlus es extremadamente complejo. Esto será abordado como un tópico más adelante.

![alt text](https://user-images.githubusercontent.com/44324576/48573942-26871100-e90e-11e8-8b5e-b6bc956db10c.jpg)

Una de las razones por las cuales es difícil modelar este tipo de espacios es porque la temperatura varía grandemente entre la zona superior y la de la base, mientras que EnergyPlus asume que cada zona se encuentra en una sola temperatura unifirme (más acerca de esto en la sección Intro IV.

![alt text](https://user-images.githubusercontent.com/44324576/48573943-27b83e00-e90e-11e8-919c-aa03bb6f75f0.jpg)

Una suposición inmediata sería modelar este tipo de atrios como un conjunto de zonas apiladas, pero esto crea problemas adicionales:

1. Hasta Enero de 2019 EnergyPlus no puede considerar intercambios de calor multi direccionales en un solo paso de tiempo. Esto significa que es muy difícil representar el calor movíendose en múltiples corrientes a través de múltiples zonas, este tipo de análisis requeriría cálculos computacionales de dinámica de fluidos (CFD).

2. Apilar zonas crea problemas relacionados con la manera en que la luz solar y el calor radiante son manejados, debido a que los muros y pisos serán tratados como superficies que interfieren con la radiación que llega a cada espacio.

Basta decir que el modelado de atrios es un tópico avanzado que requiere un gran cuidado y atención, dependiendo de la cuestión específica que uno esté tratando de analizar.
