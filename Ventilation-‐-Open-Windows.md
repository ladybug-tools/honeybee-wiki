In this section we will provide a simple example of how to indicate ventilation in an energy model. 

**4.00** This module is inserted into the script here:

![gh_04_overview_open windows](https://user-images.githubusercontent.com/44324576/52432381-96222c00-2b0a-11e9-9107-22d6dc01e8b9.png)

**4.01** Zooming in, we can see that the ventilation component offers quite a few options. Modeling ventilation is complex, but EnergyPlus has many simplifications that do not require much computation time. The trade-off here is that it is **extremely important that you assign the correct type of ventilation**. The natural ventilation that this component models is mostly meant for single zones and cases where there is not much airflow between zones. Specifically, this component can model a few common types of natural ventilation:

1. Single-sided Ventilation - ventilation driven by the height difference across individual windows on a single side of a building.
2. Cross Ventilation - ventilation driven by the pressure difference across windows on two opposite sides of a building.
3. Chimney Ventilation - ventilation driven by a chimney/stack that is attached to a zone.
4. Cowl Ventilation - ventilation driven by wind through a cowl attached to a zone.
5. Fan-driven Ventilation - ventilation at a constant flow rate driven by a fan.

![gh_04_open windows](https://user-images.githubusercontent.com/44324576/52433831-47769100-2b0e-11e9-90d8-bb75513e89b4.png)

_Note that each of these forms of ventilation work more like an on-off switch. This is particularly important to understand in relationship to wind direction because EnergyPlus does not make adjustments for wind blocked by surrounding context, nor does it adjust the amount of ventilation based upon how directly a window faces the wind._

**4.02** Hover your mouse above the _naturalVentilationType terminal to read more. As you can see, we are modeling single-sided ventilation, which is like opening a single window for one room. This is distinct from cross-ventilation which is when there is a window open on both sides of a room with a breeze passing through.
![006_openwindows_read](https://user-images.githubusercontent.com/44324576/52435631-a1795580-2b12-11e9-9fd8-ca989490c835.jpg)

**4.03** When we compare the Energy Balance Diagrams, we can see that opening the windows has almost no effect on the amount of energy entering the building. This is more of a commentary on the usefulness of Energy Balance Diagrams than it is on the effectiveness of natural ventilation. Natural ventilation does not prevent solar energy from entering the zone, it just removes the heat once it is already there. The impact of natural ventilation therefore appears as a change in the balance of energy leaving the zone, in the lower-half of the energy balance diagram. 
![004_open-windows](https://user-images.githubusercontent.com/44324576/52435462-3465c000-2b12-11e9-98e4-19c909b93399.gif)

_Note the energy removed from the zone by ventilation appears as 'storage'.This is because we have not yet connected the natural ventilation to the Honeybee_Construct Energy Balance component in our original Single Zone Model, see the component in green below:_
![006_openwindows_connectnatventenergy](https://user-images.githubusercontent.com/44324576/52437574-852be780-2b17-11e9-9432-f299c91472c9.jpg)

 
**4.04** The graph of exterior temperatures tells us when this natural ventilation is actually ocurring. For this, we use Ladybug to visualize the implications of the min/max temperature inputs from step **4.01**. Below is a graph of all hours of the year. The days run horizontally, and each vertical strip of color represents 24 hours. The graph below shows how temperatures fluctuate through January and December.
![rh_006_openwindows_diagram](https://user-images.githubusercontent.com/44324576/52436054-89560600-2b13-11e9-8087-304579af9e2b.jpg)


**4.05** The following chart is identical to the one above, except that it shows the entire year. The first image shows all hours of the year, colored by temperature. The second image shows only those hours for which the exterior temperature is above 12C, and the final image shows only those hours for which there is a potential for natural ventilation based upon this criteria. 
![005_temperatures-demo](https://user-images.githubusercontent.com/44324576/52436707-3f6e1f80-2b15-11e9-8004-bf9d1a382078.gif)

**4.06** This graph can be created with components from Ladybug. Pay special attention to the conditional statement input for a Ladybug_3D Chart, and you can create an all-black graph by dropping two black swatches into the customColors input of the Ladybug_Legend Parameters component. More examples of customizing data visualizations can be found here: http://hydrashare.github.io/hydra/viewer?owner=mostaphaRoudsari&fork=hydra_1&id=Customize_weather_data_visualization_with_3D_Chart&slide=0&scale=1&offset=0,0
![gh_04 temperature graph](https://user-images.githubusercontent.com/44324576/52436944-e783e880-2b15-11e9-8cc5-8ea4f309681c.png)

_Note that we have hidden the wires to this component in the overview diagram, for sake of making the diagrams in this guide more legible. To hide wires, simply right-click the terminal and select 'Hidden' from the drop-down_
![hidden wires](https://user-images.githubusercontent.com/44324576/52437724-e2279d80-2b17-11e9-9204-3482033d707a.JPG)

**4.07** Finally, we want to actually evaluate these strategies in terms of their impact on the comfort of the space inside. To do this, we will need to use the adaptive comfort model and graph the results. This is located near the end of our definition:
![gh_000_overview_final](https://user-images.githubusercontent.com/44324576/52441180-52d2b800-2b20-11e9-85a7-2654e114c562.png)

**4.08** Zooming in, we can see that the Ladybug_Adaptive Comfort component requires several sources of data. The drybulb temperature and mean radiant temperatures are outputs from our simulation. It also requires the outdoor temperature, because as we explained in the introductory section on comfort models, adaptive comfort is based upon occupant's recent experience, and therefore a record of outdoor temperatures is also necessary for this calculation.

![gh_adaptive comfort](https://user-images.githubusercontent.com/44324576/52441428-cecd0000-2b20-11e9-9c28-60dd9e8ea861.png)

**4.09** Here are two resulting graphs, which compare an initial scenario without any strategies, to a scenario with natural ventilation only.
![07_comfort-graph_2-stratgies-gif](https://user-images.githubusercontent.com/44324576/52441922-418aab00-2b22-11e9-858f-c2ad86d5598e.gif)
