Intro VI - Contribuciones a la Wiki de Honeybee
===============================================

Hola y gracias por interesarte en contribuir a la Wiki de Honeybee.

Esta página fue creada para servir como punto de partida para compartir consejos acerca de Markdown, recomendaciones, observaciones acerca de higiene y otras notas importantes para contribuir a la Wiki. Mientrs Alexander Jacobson escribió esta guía, se topó con muchas consideraciones para hacer más esbelto el proceso de creación de tutoriales que son muy valiosas y vale la pena compartir. Esta página debe solucionar algunos de los dolores de cabeza relacionados con la creación de tutoriales para Honeybee.

Tópicos para Contribuir
-----------------------

Si quisieras encargarte de desarrollar un tópico por ti mismo, existe una lista importante pero aún incompleta de tópicos en la tabla de contenidos, marcados como [WIP] o *Work in Progress*.

El Lenguaje de Escritura de Código Markdown
-------------------------------------------

Esta Wiki está escrita en Markdown, un lenguaje ligero de anotación que permite especificar formato para texto en línea. Es fácil de aprender y existen herramientas como Visual Studio Code de Microsoft que facilitan la edición de código y la visualización de resultados simultánea.
<https://code.visualstudio.com/>

Aquí puedes encontrar una *cheatsheet* (i.e. chuleta, acordeón, machete, torpedo, etc...) para Markdown: <https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet>

Es importante notar que al usar MArkdown es necesario distinguir entre algunos caracteres que especifican formato en Markdown y caracteres que de hecho queremos representar en la guía. Por ejemplo, un guion bajo al lado de una palabra indica ítalicas en Markdown. Sin embargo, la convención en Honeybee es usar el guion bajo al frente para indicar datos de entrada necesarios y un guion bajo detrás para indicar datos de entrada opcionales. Esto puede solucionarse al utilizar una diagonal invertida entre dos guiones bajos, lo cual cancela el comando para representar itálicas.

+ Por ejemplo, en Markdown: '\_RADMaterial\_' debe escribirse '\_RADMaterial\_'; de otra manera se mostraría como '_RADMaterial_'.

Formato
-------
Para mantener el formato, utiliza la guía de Modelado de Zona Unitaria como guía de estilo. El punto más importante de mencionar es que todos los pasos deben estar marcados en negritas y claramente numerados de acuerdo a su sección, seguido de un punto decimal, seguido del número de paso. Por ejemplo, **iii.05** se referiría a la introducción III, paso 5. **Esto facilita las referencias a la guía en los foros donde la gente necesita ayuda.**

Creando Archivos de Ejemplo para Grasshopper
--------------------------------------------

1. Crea grupos entiquetados que correspondan a las secciones de la guía. Esto preverá confusiones y hará más fácil para los lectores seguir la guía.
2. Provee por lo menos una imagen de vista general de todo el script, con los diferentes grupos claramente visibles.
3. Siempre usa un selector booleano de arranque en falso para lanzar operaciones largas. También recomendamos crear un grupo individual para cada uno de estos selectores y marcarlo en color **ROJO** para distinguirlo de los selectores que simplemente modifican parámetros.
4. Recomendamos utilizar el componente 'Bifocals', disponible en food-for-rhino, y activar la visualización a 'icons'. De esta manera es posible que los usuarios vean tanto el nombre como el ícono de cada componente, y hace mucho más fácil que puedan localizar componentes no familiares en los menús de Grasshopper o al ejecutar una búsqueda.

Cargando Imágenes
-----------------

Para cargar imágenes en Markdown, simplente crea un nuevo 'issue' en la Wiki y arrastra y suelta una archivo de imagen en la sección de comentarios. Intenta con este link:
<https://github.com/mostaphaRoudsari/honeybee/issues/new>

Entonces, el proceso general para crear imágenes y cargarlas es:

1. Crea el archivo de ejemplo de Grasshopper/Rhino que quieras capturar.
2. Crea una serie de imágenes paso-a-paso corriendo una captura de pantalla en alta resolución en Grasshopper o 'ViewCapturtoFile' en Rhino (los usuarios de Rhino 5 deben intentar con \_ViewCapturetoFile con un guion bajo al inicio).
3. Exporta estas imágenes a una carpeta en tu computadora.
4. Edita estos archivos en photoshop.
5. Arrastra las imágenes editadas a un tópico 'new issue' en GitHub (ver el link más arriba) para cargarla automáticamente a GitHub y crear un segmento de código en Markdown y un URL de imagen para poder insertarlo en cualquier sitio.
6. Pega este segmento de código en Markdown en tu editor de código, como VS Code por ejemplo (o directamente en la Wiki de Honeybee si no te interesa pre-visualizar el código mientras escribes).
7. Pre-visualiza la imagen como aparece entre tu texto formateado en Markdown.
8. Cuando estés satisfecho, ve a la sección de edición de la página correspondiente en la Wiki de Honeybee y pega el código en Markdown.
9. Guarda los cambios en la página.

Este proceso ha sido probado utilizando múltiples escritorios en Windows 10. En el extremo derecho empezamos con el Escritorio 5 con Rhino/Grasshopper, en el Escritorio 4 abrimos Photoshop para editar las imágenes, en el Escritorio 3 ubicamos lado a lado las ventanas de Windows explorer y el nuevo *issue* de Honeybee de manera que fuera posible arrastrar las imágenes, enseguida el Escritorio 2 con Visual Studio Code donde se probaban los segmentos en Markdown generados en el paso anterior y finalmente, el Escritorio 1 mostraba la página de la Wiki de Honeybee donde se cargaba el resultado final.

Crear Series de Imágenes Paso-a-Paso Usando Grasshopper y Photoshop
-------------------------------------------------------------------

Una vez que hayas creado un archivo de Grasshopper que quieras usar en un tutorial como una serie de imágenes paso a paso, ve al menú de Grasshopper, en achivo selecciona exportar como imágen en alta resolución. Esto creará una imágen de alta resolución de todo el lienzo. Entonces, abre este archivo en Photoshop y recorta la imagen como consideres necesario. Entonces, duplica la capa, crea una máscara completamente negra y pinta en blanco las máscaras de capa para 'revelar' el primer paso en la imagen de alta resolución. Duplica la primera capa y repite el proceso para mostrar el segundo paso de tu tutorial. Repite según sea necesario para abarcar todos los pasos del tutorial. Cuando esta serie de capas esté completa, puedes exportarlas todas ellas al mismo tiempo accediendo al menú en 'File / Scripts / Export Layers to Files'.

Capturando la Actividad del Lienzo de Grasshopper
-------------------------------------------------

En la creación de las primeras guías de esta Wiki fue utilizado Windows Screen Capture para registrar la actividad en el lienzo, como la información que se revela al pasar el cursor por encima de un componente, o al hacer clic derecho en una terminal, etc. Existe una opción para añadir un retraso a la captura, lo que te permite capturar los menús de clic derecho. También es posible seleccionar capturas rectangulares o de ventana completa para facilmente alinear los tamaños y escalas de imágenes entre si.

Editando la Tabla de Contenidos
-------------------------------

Pulsa el icono del lápiz arriba de la tabla de contenidos para editarla. Cada entrada muestra el texto en paréntesis (), seguido por el nombre de la página entre corchetes []. Si simplemente escribes una nueva línea, con un nuevo nombre de página entre [corchetes] GitHub automáticamente creará una página con ese nombre. Para crear una nueva página en la tabla de contenidos que incluya un guion corto, es necesario utilizar el caracter '‐' en su lugar. Esto es necesario porque Gollum (el entorno de fondo que muestra la página de GitHub) utiliza guiones en los nombres de archivos para representar espacios, así que asume que los guiones son generalmente espacios. Este método alternativo fue realizado usando el caracter de unicode ‐ (Hyphen or U+2010) en lugar de - (Hyphen-Minus or U+002D). La solución simplemente es copiar y pegar este caracter: ‐

Marcando Páginas Incompletas
----------------------------

+ Cuando trabajes en una página o sección que esté en un estado muy rudimentario todavía, debes marcarla ya sea con [WIP], para trabajo en proceso, o simplemente excluirla de la tabla de contenidos. Aparecerá en la sección 'pages' antes de la tabla de contenidos, lo que la hace públicamente accesible para que otros editores continúen el trabajo, pero solamente quienes estén buscando activamente esta página podrán encontrarla.
+ Si hay algún problema con una página existente, aquí hay un método para crear un ícono de exclamación. Usa esto para indicar que hay un problema con esta área de la guía y provee notas acerca de tus dudas en **negritas**. 

<img src="https://user-images.githubusercontent.com/44324576/49518217-67839d00-f89e-11e8-9b63-e16b5618a9af.png" width="50" height="50" />


Dando Crédito a Contribuidores
------------------------------

```
 _Contributors_:
 <a href="https://github.com/alexandermatthias" title="Alexander Matthias Jacobson"><img 
 src="https://github.com/alexandermatthias.png" height="24"></a>
 #
 
```

Es posible dar crédito a los contribuidores de esta Wiki con el segmento de código mostrado justo arriba (el cual, por supesto, deberá se editado para vincular el perfil de GitHub del contribuidor en vez del de Alexander). Para tutoriales más largos, el crédito puede ser dado en la página de inicio, para **Tópicos** el crédito puede ser dado en la parte superior de cada página.

Creando Figuras Directamente desde Rhino
----------------------------------------

Todas las imágenes en esta guía han sido tomadas como capturas de pantalla directamente desde Rhino 6. Aquí están las notas para crear estas figuras:

+ Usa el ajuste de previsualización 'arctic'
+ Escribe 'LinetypeDisplay' en la línea de comandos de Rhino para encenderlo.
+ Escribe 'SetLineTypeScale' en la línea de comandos de Rhino y captura 250.
+ Deberás ser ahora capaz de editar tipos de línea y escalas en las capas de Rhino.
+ Es una buena práctica crear una vista con nombre para cada archivo que exportes, de manera que si necesitas volver a editar el archivo sea fácil crear un duplicado.
+ Tienes la opción de espécificar el color de cada objeto por color de objeto o color de material. Ambas opciones te permitirán hacer objetos semitransparentes al cambiar la transparencia del material. Esto puede lograrse al personalizar el modo de visualización en 'Options / Display Modes'.
+ Para empezar a dibujar para un nuevo paso duplica la capa y los objetos. Esto puede hacerse haciendo clic derecho en el menu de capas y seleccionando 'duplicate layer and objects', después renombrando la capa con el número del paso. Esto es más fácil que volver y editar las figuras.
+ Hemos exportado imágenes en 1000x600 pixeles para mantener los archivos pequeños. Esto puede hacerse usando 'viewcapturetofile'.
+ 'Dot' puede ser muy útil para crear etiquetas en Rhino.
+ Escribe 'Options' en la línea de comandos de Rhino, desplázate a 'Display Modes' en el fondo, crea uno nuevo y cambia los siguientes datos: 1) cambia el color de fondo a blanco. 2) Bajo 'Objects' ve a 'Curves' y fija el diámetro a 1 pixel.
