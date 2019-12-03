Las elecciones de materiales tienen un gran impacto en el rendimiento energético. Esta sección ilustrará como Honeybee maneja los materiales modelando ventanas de alto rendimiento.

**1.01** Here is an overview of all the modules we will add throughout the chapter on Passive Techniques. This is baseed directly upon the single-zone model we created before. The original elements appear in light grey groups below, and new elements appear in yellow.

![gh_000_overview](https://user-images.githubusercontent.com/44324576/52227404-b6a27a00-28af-11e9-8839-6854e4e642e5.png)

**1.02** Zooming in, you can see that we will create a construction for a high performance window, and connect it to the Honeybee_addHBGlz component. This will replace the default assumption about glazing with our specifications for a high-performance window.

![gh_001_passive 1](https://user-images.githubusercontent.com/44324576/52228338-6b3d9b00-28b2-11e9-8cea-4fc05f449fbb.png)

**1.03** Zooming in further, we will now walk through the process of creating a high-performance window construction. 
![gh_002_passive 1](https://user-images.githubusercontent.com/44324576/52228340-6c6ec800-28b2-11e9-9b8c-02ada07437d0.png)

**1.04** Start with the Honeybee_EnergyPlus Construction component. An Energy Plus Construction could be a single material in a single layer (i.e. solid concrete) or it could be an entire material stack (i.e. a stud-wall with gypsum on either side and insulation inside). The important thing is that you can only have one construction per zone surface. In this case we are making a window, and we have already specified the surfaces we intend to use (notice the 'House Windows' component in the image from step **1.02**).
![gh_02_hpwindow_0000_01](https://user-images.githubusercontent.com/44324576/52409824-e41d3c80-2ad6-11e9-993a-b7d7f5910c4b.jpg)
_Note you can add additional layers to an EP construction by zooming into the component in Grasshopper until you see black-and-white plus/minus signs next to the terminals, as in the image below:_

![add layers](https://user-images.githubusercontent.com/44324576/52410725-89391480-2ad9-11e9-9e8e-34057df18d72.JPG)


**1.05** Now we need to add layers of material to this construction. Honeybee contains a variety of components for specifying materials (see tab 06 | Energy | Materials) that can be attached as layers to an EP Construction. The simplest way to model a window is to use the EnergyPlus Window Material, which is intended to describe an entire window assembly. This makes it easy to plug in values from manufacturers which describe an entire window rather than a specific material.
![gh_02_hpwindow_0001_02](https://user-images.githubusercontent.com/44324576/52409825-e41d3c80-2ad6-11e9-80c7-7ce489dc8662.jpg)

_Here is a preview of Honeybee Materials Menu:_ 
![hp windows materials](https://user-images.githubusercontent.com/44324576/52495175-32623680-2bd0-11e9-95ae-c3eafbb3b9d8.JPG)


**1.06** Assign the U-Value as 2, Solar Heat Gain Coefficient as 0.25, and Visible Transmittance of the window as 0.55. The U-Value is a measure of insulation, the Solar Heat Gain Coefficient is a measure of how much solar energy enters the glass, and Visible Transmittance is a measure of how much visible light enters the window. 

_Note the distinction between **Transmittance**, which is the measured ratio of light at normal incidence, versus **transmissivity**, which is the ratio of the total light that passes through the glass. We're not using Radiance here, but Radiance glazing parameters require transmissivity and glazing manufacturers often quote transmittance._
![gh_02_hpwindow_0002_03](https://user-images.githubusercontent.com/44324576/52409826-e4b5d300-2ad6-11e9-80fd-553f3f038ad3.jpg)

**1.07** Now we can connect this construction to the Honeybee_AddHBGlz component to assign the material to the windows we modeled. ![gh_001_passive 1](https://user-images.githubusercontent.com/44324576/52228338-6b3d9b00-28b2-11e9-8cea-4fc05f449fbb.png)

**1.08** Re-run the Simulation by clicking the false start toggle and examine the Energy Balance Diagram. As you can see below, when we compare the Energy Balance Diagram of the house with and without the high performance window, it significantly reduces solar heat gain.
![001_nostrategyvshighperformancewindow](https://user-images.githubusercontent.com/44324576/52350919-e2496f80-2a29-11e9-9614-7e161f37bb3c.gif)

