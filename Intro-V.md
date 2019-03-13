Intro V - Convenciones e Higiene para Escritura de Código
======================================================

Convenciones de la Guía
-----------------------

Para ayudarte a navegar esta guía, hay algunos puntos acerca de su misma organización que debes tener presentes:

+ *Numeración* De manera que sea posible referirse a secciones específicas de la guía, cada entrada ha sido numerada. Cada entrada está numerada primero por sección, seguido de un punto decimal, seguido por el número de paso. Por ejemplo, 0.05 debe leerse como sección cero, paso cinco. Las secciones introductorias estarán numeradas con números romanos, así que iv.02 sería el segundo paso de la cuarta sección.
+ *Archivos de ejemplo* El sistema de numeración arriba mencionado corre en paralelo a la numeración en los archivos de ejemplo. Los pasos individuales no están marcados en los archivos de ejemplo, pero sí se mencionan los números de sección.
+ *Diferenciando archivos de ejemplo* Para evitar confusiones debe notarse que los archivos de ejemnplo se diferencian entre si usando un código de tres letras que abrevia el tópico del ejemplo. HSZ quiere decir *Honeybee Single Zone*, HMZ quiere decir *Honeybee Multiple Zone*, etc.
+ *Detonadores de inicio de simulación* Los selectores booleanos que ejecutan una acción importante están ubicados en grupos y marcados con color rojo. Hay que prestar atención a no cambiar su estado, ya que esto lanzará la simulación y en ocasiones éstas pueden tomar mucho tiempo.

Higiene
-------

La flexibilidad que permite Grasshopper es absolutamente hermosa, pero también puede convertirse en una pesadilla. A lo largo de esta guía, hemos desarrollado convenciones y puntos de higiene para que el código sea fácil de interpretar y que sea, por lo tanto, fácil de usar y compartir con tus colegas o comunidad. Los siguientes tópicos son enlistados desde el más fundamental hasta el más detallado. Comienza leyendo desde arriba de la lista hasta que no entiendas de qué estamos hablando, después ve y practica y podrás regresar a donde te quedaste cuando hayas aprendido más. Feliz código.

Escribe de Izquierda a Derecha
------------------------------

Siempre que es posible, escribimos scripts que se leen desde arriba a la izquierda hasta el fondo a la derecha. Si es necesario crear más espacio para insertar un paso muy grande en un script existente, mantén presionado 'alt' y da clic izquierdo para agregar más espacio en el lienzo.

Atajos de Interfaz y Teclado
----------------------------

Aquí están algunos atajos que pueden ser muy útiles, puedes encontrar más en:
<https://www.grasshopper3d.com/forum/topics/what-hotkeys-and-shortcuts-are-available-in-grasshopper>

+ Escribe '//' para crear un panel
+ Mantén presionado 'shift' para agregar múltiples cables a la misma terminal
+ Mantén presionado 'ctrl' para eliminar un cable de una terminal en específico

Errores Comunes en la Captura de Datos
--------------------------------------

+ Los paneles tienen dos formas de datos, strings y datos de líneas múltiples. Si deseas crear una lista manualmente usando un panel, debes cambiar el tipo de datos a datos de líneas múltiples. Simplemente haz clic derecho en el componente y presiona 'multi-line data' para hacer el cambio.
+ No presiones 'enter' en los paneles, esto crea una línea extra que contiene datos vacíos que pueden causar errores en algunos componentes.

Explícito es Mejor que Implícito
--------------------------------

Al crear un script recuerda que estás contando una historia. Créalo de manera que alguien más pueda leerlo. No internalices valores, en vez de esto utiliza un panel si no deseas que las personas cambien el valor. Usa un slider solamente cuando esperes que alguien modifique valores.

Los Datos de Entrada Deben Capturarse Solo una Vez
--------------------------------------------------

Si debes capturar un valor dos veces para cambiar un dato de entrada, tu script será difícil de usar. Por ejemplo, digamos que quieres medir el número promedio de días con iluminación natural en tu periodo de análisis. Si tu periodo de análisis es de un año completo, estarías realizando un promedio por 8760 días. Si tu periodo de análisis es de un mes solamente, estarías haciendo un promedio a lo largo de 30 días. Escribe tu código de manera que el periodo de análisis se actualice automáticamente, de manera que no calcules por error un promedio mensual extremadamente pequeño debido a que olvidaste actualizar el código para dividir entre 30 en lugar de 8760. Esto puede hacerse automáticamente usando ya sea los datos de entrada originales o un componente del tamaño de la lista. Tu código será muy difícil de usar si alguien debe teclear múltiples valores para poder cambiar solamente un parámetro.

Descompone el Proceso en Pasos
------------------------------

Esta guía agrupará componentes en distintos pasos. Los pasos serán etiquetados y haremos todo lo posible por mantener la guía en paralelo con su archivo de ejemplo correspondiente. Todos los datos de entrada para cada proceso estarán localizados a la izquierda de cada paso en el proceso y los datos de salida estarán ubicados a la derecha.

Selectores Booleanos
--------------------

Los selectores booleanos requieren particular atención ya que son frecuentemente utilizados para lanzar simulaciones complejas, con largos tiempos de cómputo. Todos los selectores booleanos que detonan largas simulaciones estarán marcados con un grupo de color rojo, para distinguirlos de selectores que simplemente cambian parámetros de simulación. También es una buena práctica guardar aquellos archivos que tengan selectores booleanos siempre en la posición 'falso', de manera que no se lance la simulación al abrir el archivo. Todavía mejor, puedes utilizar un selector booleando de falso arranque, disponible en Ladybug, el cual se reinicia a falso cada vez que un archivo es abierto.

Actualizando y Honeybee Legacy vs Honeybee Plus
-----------------------------------------------

Actualmente existen dos versiones de Honeybee, Honeybee Legacy y Honeybee Plus. La diferencia radica en la manera en que cada una maneja los datos tras bambalinas. Honeybee Plus [+] es una re-escritura de Honeybee Legacy, que los hace más agnóstico en términos de plataforma, compatible con la nube, escalable y más flexible al desarrollo. Para la mayoría de los usuarios, la diferencia no será aparente pero es una importante distinción al momento de hacer *trouble shooting*.

En cuanto a las actualizaciones, mantente usando la versión más actualizada a menos que tengas un problema/bug de considerable gravedad. Limita las actualizaciones automáticas de ser posible, ya que esto hace difícil distinguir qué versión es la que funcionó correctamente de manera más reciente. Las actualizaciones son especialmente problemáticas al trabajar en grandes organizaciones como escuelas y oficinas ya que crean inconsitencias entre los usuarios.

Para Estudios Paramétricos:
---------------------------

Siempre cuestiona el flujo de trabajo antes de construirlo. Determina cuándo estás resolviendo un problema 1D comparado con uno 2D. Recuerda que toma exponencialmente más tiempo para cada dimensión de un problema. si deseas estimar el tiempo necesario para una serie de cálculos, deberás tomar el promedio de una muestra representativa de varias simulaciones en vez de tomar una sola y multiplicarla.
