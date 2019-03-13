Wiki Honeybee Página de Inicio
==============================

Bienvenido al Wiki Oficial de Honeybee, para guías de modelado energético usando Honeybee.

La guía de **Modelado de Zona Unitaria** cubre la creación de geometría apropiada en Rhino, la especificación de datos de entrada y la configuración de un modelo energético, el envío de un modelo energético a un motor de cálculo y la interpretación de resultados de esa simulación. Honeybee utiliza componentes de Ladybug, que es otro plugin *open source* para Grasshopper diseñado para importar, visualizar y analizar gráficamente datos climáticos.

La guía de **Comparación de Estrategias Pasivas** complementa el Modelado de Zona Unitaria, explicando el marco de trabajo que Honeybee emplea para incorporar más niveles de detalle a una simulación. Esta sección enseña cómo estudiar cinco estrategias de diseño comunes y pretende ser un paso intermedio hacia tópicos más avanzados.

En **Tópicos**, el formato de estos tutoriales cambia. En vez de avanzar a través de una serie de instrucciones paso-a-paso, la guía se divide y se enfoca en métodos para referirse a técnicas específicas de modelado y situaciones particulares de diseño. Estas son algunas de las razones para esta transición:

1. Sería imposible para nosotros escibir un solo tutorial secuencial que cumpla las necesidades de cada persona.
2. Los diseñadores buscan frecuentemente métodos para evaluar problemas específicos de diseño, de esta manera la guía puede fungir como un repositorio de métodos / buenas prácticas.
3. Este formato hace mucho más fácil que otros puedan contribuir a la guía.

Vista General del Proceso de Modelado Energético de Honeybee
------------------------------------------------------------

La relación entre Rhino, Grasshopper, Ladybug, Honeybee y los motores de simulación con los que Honeybee se comunica se describe en el diagrama mostrado más abajo. Ladybug es la herramienta más simple de utilizar y provee muchos recursos muy útiles en las fases más tempranas del diseño. Honeybee hace posible involucrarse mucho más a fondo y proveer un análisis más detallado.

![alt text](https://user-images.githubusercontent.com/44324576/51753145-60685680-20b9-11e9-8526-299586429511.png "Proceso de modelado con Honeybee")

Honeybee y Ladybug son ambos necesarios para seguir esta guía, pero no es necesario leer las guías sobre Ladybug antes de proceder. Los fundamentos necesarios acerca de Ladybug serán aquí cubiertos. Si estás solamente interesado en análisis geométrico, Ladybug puede ser soficiente. Por ejemplo, Ladybug puede calcular la dirección de la luz del sol en cualquier momento específico, e incluso el número de horas de luz solar directa impactando un objeto a lo largo del año. Sin embargo, Honeybee es necesario para cualquier cosa que tenga que ver con materiales, como el rastreo de trayectorias para la iluminación natural difusa, tomar en cuenta las ganancias de calor resultante en un espacio, simular variaciones térmicas o estimar los consumos energéticos anuales de un edificio.

![alt text](https://user-images.githubusercontent.com/44324576/49177299-298df280-f34d-11e8-9f48-40bc1bac363c.jpg "Relaciones entre Honeybee y motores de cálculo")

Es importante dejar en claro una distinción: Honeybee en realidad no ejecuta simulaciones. Honeybee es una interfaz que crea instrucciones para que otros programas de software ('motores de cálculo') corran las simulaciones. Hasta noviembre de 2018 Honeybee posee interfaces con cinco motores de cálculo:

1. Radiance para simular iluminación en un punto específico del tiempo
2. Daysim (que utiliza Radiance) para iluminación a lo largo del tiempo
3. EnergyPlus para simulaciones de balances térmicos y modelación de consumos energéticos 
4. OpenStudio para la integración de Radiance y EnergyPlus
5. Therm para simular la conducción de calor y evaluar riesgos de condensación en modelos de construcciones

Para mayor información, es posible consultar la sección *Our Story* en el [website de Ladybug](https://www.ladybug.tools/about.html).

Motor de Cálculo EnergyPlus
---------------------------

Este tutorial tratará primordialmente con el tercer motor de cálculo, EnergyPlus. Técnicamente, estaremos empleando OpenStudio para enviar la simulación a través de EnergyPlus, pero lo importante es comprender que EnergyPlus crea un modelo energético que rastrea el movimiento del calor hacia y desde el edificio. El motor de cálculo EnergyPlus es una inmensa colección de trabajo realizado por **múltiples colaboradores alrededor del mundo y es coordinado por el Departamento de Energía de los Estados Unidos.**

Zonas Térmicas
--------------

Al trabajar en un modelo energético, los edificios son descritos utilizando zonas tridimensionales creadas en un entorno gráfico. Cada zona representa un espacio térmicamente distinto. Por lo tanto, un edificio puede ser tratado como una sola zona térmica, o puede ser estudiado más a detalle al descomponerlo y caracterizar cada espacio interior como una zona térmica independiente. Honeybee incluye herramientas para crear estas zonas a partir de geometría tridimensional modelada en Rhino. Cada zona es modelada como una forma 3D, delimitada por múltiples superficies que encierran un volumen; Honeybee asigna propiedades físicas para cada una de estas superficies. Las ventanas y puertas son tratadas como sub-elementos que 'pertenecen' a una superficie específica dentro de una zona.

Las zonas son la únidad básica de análisis. Para rastrear el calor que se desplaza desde y hacia cada zona, a través de un periodo de tiempo (i.e. un año completo), la simulación correrá en pasos de tiempo (i.e. intervalos de 10 minutos). A medida que una simulación va siendo ejecutada, características específicas serán calculadas y asignadas para cada uno de estos pasos de tiempo. Por ejemplo, es posible referirse a los datos climáticos para simular las condiciones en el exterior de una zona, como la temperatura hora-por-hora del aire exterior. También podemos simular condiciones en el interior de la zona, empleando datos de entrada como horarios de ocupación o de utilización de equipamiento. Es posible también especificar cómo el equipamiento responderá a estas condiciones interiores y exteriores, por ejemplo especificando temperaturas de consigna interiores.

Cálculos de Simulación
----------------------

Una vez que hemos empleado Honeybee para introducir toda la información que deseamos considerar, indicaremos a Honeybee que es momento de 'correr' nuestra simulación. En este punto, Honeybee manda los datos de entrada arriba descritos como un conjunto de instrucciones para OpenStudio, que a su vez envía estas instrucciones al motor de cálculo EnergyPlus. El motor de cálculo recorrerá entonces cada paso de tiempo a través del periodo de análisis especificado y regresará datos de salida de vuelta para Honeybee. Honeybee incluye herramientas para analizar estos resultados. Por ejemplo, es posible extraer métricas específicas, visualizar el balance térmico en cada zona, comparar zonas entre sí y agregar resultados de múltiples zonas.

Analizando los Resultados
-------------------------

A medida que analizamos los resultados, evaluaremos si éstos son razonables e identificaremos cuáles factores contribuyen más al uso de energía de nuestro edificio. Una vez que la simulación y el análisis han sido completados, estableceremos un ciclo completo de retroalimentación por medio del cual podemos empezar a alterar el diseño y evaluar el impacto de estas modificaciones en el desempeño.

¿Por Qué Crear un Modelo Energético en Primer Lugar?
----------------------------------------------------

1. Para informar el diseño
2. Anticipar el uso de energía
3. Respardar con argumentos convincentes ideas de diseño
4. Desarrollar una intuición constructiva
5. Realizar análisis de sensitividad
6. Calcular periodos de retorno de inversión para medidas de conservación de energía (MCEs)
7. Cumplir con códigos y normatividad de edificación
8. Validar el cumplimiento con certificaciones de terceros, como LEED, BREAM o DGNB

Esta guía es suficiente para cumplir con los primeros cinco objetivos, pero los detalles específicos para calcular periodos de retorno de inversión y para crear modelos de validación normativa, se encuentran fuera del alcance de este tutorial.

¿Qué Resultados Puedo Esperar?
------------------------------

Depende. Existen múltiples métricas que pueden ser extraídas de una simulación energética, cada una refiriéndose a aspectos específicos del desempeño energético de un edificio.

![alt text](https://user-images.githubusercontent.com/44324576/51490305-2e01e500-1dab-11e9-924c-90c3c64b662b.png "The World of Metrics")

El resultado más frecuentemente utilizado es el Diagrama de Balance de Energía, el cual representa la energía moviéndose desde y hacia el edificio. Esto es fundamental para la Primera Ley de la Termodinámica, la cual establece que la energía no puede ser creada ni destruida. El calor que se desplaza en un edificio puede incluir el calor generado por las personas, calor disipado por equipo de cómputo o de procesos, calor proveniente de bombillas incandescentes, calor solar a través de las ventanas y calor proveniente de sistemas de climatización artificial. Las pérdidas de calor pueden ser resultado de la conducción a través de la envolvente, aire frío filtrándose por las paredes o siendo inyectado por sistemas de ventilación. Todos estos mecanismos de transmisión de calor son contabilizados en un diagrama de balance:

![alt text](https://user-images.githubusercontent.com/44324576/49155416-2c6fef80-f31b-11e8-88c3-f52a9aa72e7b.JPG "Energy Balances")

Nota Acerca de la Iluminación Natural
-------------------------------------

Las simulaciones energéticas basadas en EnergyPlus toman en cuenta la geometría específica de un edificio, así como el movimiento aparente del sol. No obstante, si estás interesado en simulaciones de iluminación natural que arrojen niveles específicos de iluminación interior, entonces es necesario buscar otras opciones. Este tipo de simulaciones pueden ser ejecutadas utilizando Honeybee, pero para llevarlas a cabo es necesario utilizar el motor de cálculo Radiance, el cual no está incluido en esta guía. Existen planes para desarrollar una guía wiki para iluminación natural, pero hasta Enero de 2019, ésta aún no ha sido desarrollada.
