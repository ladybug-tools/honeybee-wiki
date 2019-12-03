There are several ways of modeling shade in Honeybee. For static elements, the easiest is to simply model the geometry and load it into a Honeybee EP Context Surfaces component.

**2.00 - Review** The first is to simply draw context geometry, as we did when we added trees and shading elements to the Single Zone Model:
![005_single zone_shade overlay](https://user-images.githubusercontent.com/44324576/52411432-17ae9580-2adc-11e9-9cc8-1f8f78b200c5.jpg)

We will plug the shading component into our existing definition here:
![gh_03_overview_shade](https://user-images.githubusercontent.com/44324576/52431819-47c05d80-2b09-11e9-8d26-08c140421d9c.png)

**2.01** Zooming in, we can see that this is the exact same module we created at the end of the Single Zone Model. 
![gh_03_shade](https://user-images.githubusercontent.com/44324576/52420174-d1fcc780-2af1-11e9-9689-ffb93bd7f946.png)
_Note these steps are explained more fully here: https://github.com/mostaphaRoudsari/honeybee/wiki/Iterating-to-improve-design_

**2.02** Once we run the simulations and compare the resulting Energy Balance Diagrams, we can compare the effectiveness of shading the house versus replacing the windows with high performance glass.
![002_high-perf-window-vs-shading](https://user-images.githubusercontent.com/44324576/52420820-1472d400-2af3-11e9-8909-704d701f6b40.gif)


**2.03** Why is this the case? Using Ladybug's Skydome component, it is possible to visualize where in the sky this solar radiation originates. It provides us a diagrm like the one below. This diagram is to be read as a sphere projected flat in plan. It subdivides the sky into 145 areas, and measures the overal amount of solar radiation originating from each area of the sky dome. 
![003_contextshadingskydome_legend](https://user-images.githubusercontent.com/44324576/52426104-a5e74380-2afd-11e9-98d5-1cf0292000a4.jpg)
_A full explanation of the Ladybug_skyDome component is beyond the scope of this tutorial, but you can download an example file on Hydra._

**Download example file on** [Hydra](http://hydrashare.github.io/hydra/viewer?owner=alexandermatthias&fork=hydra&id=ComparingPassiveStrategies_01_SkyDome&slide=0&scale=1&offset=0,0).

**2.04** Here is an axonometric view of the same diagram, which is easier to read spatially.
![003_contextshadingskydome](https://user-images.githubusercontent.com/44324576/52426407-358cf200-2afe-11e9-82fe-3ce4d4781fd5.jpg)


 **2.05** If we overlay this diagram on our model, we can see that the canopy protecting the eastern side of the house is fairly effective, but the south and west sides of the house are left unprotected. This is the primary reason that high performance windows are more effective than shading in the analysis above. We can also see that some of the most intense sunlight arrives from an altitude that is too acute to be shaded by the trees.  
![003_contextshadingskydome_edit](https://user-images.githubusercontent.com/44324576/52424173-bb5a6e80-2af9-11e9-9460-a73456b6994a.jpg)

