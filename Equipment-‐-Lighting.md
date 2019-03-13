Although it is a very small portion of the Energy Balance Diagram in this model, we will still cover a basic example of how to assign zone loads. These include loads which are specific to the zone, such as equipment per unit area, infiltration rate per unit area, lighting density, number of people per unit area, ventilation per unit area, ventilation per person, and recirculated air per unit area. In this case, we will show how to change all of the lights over to LED Blulbs by adjusting the lighting density per unit area. 

**3.00** Returning to our overview diagram, we will insert the next module immediately after the high performance windows module from the previous script, as indicated in the yellow group with a black arrow pointing to it below:
![gh_03_overview_daisychain](https://user-images.githubusercontent.com/44324576/52429288-0c6f6000-2b04-11e9-93bb-e4151cecef01.png)

**3.01** Zooming in, we can see that the Passive 3_Lighting Level module simply picks up where the 'Passive 1_High Performance Windows' left off. Each successive element of analysis adds a layer of nuance to Honeybee Zones from the previous element. This system of 'daisy-chaining' makes it easy to configure and re-configure simulation files with different strategies.
![gh_03_lighting](https://user-images.githubusercontent.com/44324576/52429470-6b34d980-2b04-11e9-93b3-f113a7584a31.png)

**3.02** Assigning the lighting density itself is quite simple, just connect a panel with 5.9 to the terminal for lightingDensityPerArea. As you can read in the component itself, this value is measured in W/m2 and typical values rante from 3 W/m2 for efficient LED bulbs, to 15 W/m2 for incandescents. 
![gh_03_equipmentschedule](https://user-images.githubusercontent.com/44324576/52430239-f367ae80-2b05-11e9-83dc-b768cfd81401.png)

**3.03** Comparing this to the previous Energy Balance Diagram we can see the impact of installing more efficient lighting fixtures.
![003_1 2-vs-1 2 3](https://user-images.githubusercontent.com/44324576/52430996-9a007f00-2b07-11e9-8b7a-aca29ff9e91f.gif)