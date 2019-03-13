We will now illustrate how you can use the model to explore potential design strategies.

**5.00** This will require three changes to the script we completed in Section 4. The changes are highlighted in yellow below:

**You can download a version with the changes on** [Hydra](http://hydrashare.github.io/hydra/viewer?owner=alexandermatthias&fork=hydra&id=SingleZoneModel_01_IteratingToImprove&slide=0&scale=1&offset=0,0). 
![06_iterating through designs](https://user-images.githubusercontent.com/44324576/51693280-f2f7ef80-1ffe-11e9-8163-9c24766b27bb.png)

**5.01** The very first thing we will do is apply a high and low bound to the graph, so that our results are drawn on the same y-axis and are therefore comparable to one another. Connect two panels to the Ladybug_Legend Parameters component containing .03 and -.03 as shown below:
![06_iterating through designs_change 3](https://user-images.githubusercontent.com/44324576/51693629-a19c3000-1fff-11e9-99e5-87b550ac6a8f.png)

**5.02** You might imagine that the Energy Balance Diagram describes the work done by mechanical systems, but it is actually broader than that. It describes all heat moving in and out of the zone. To illustrate this point we will change the zone to being unconditioned, which results in an Energy Balance Diagram that describes the house with the air conditioning and heating systems switched off. In the Grasshopper script, this is achieved by connecting an additional false boolean toggle to the Mass2Zones component:
![06_iterating through designs_change 1](https://user-images.githubusercontent.com/44324576/51693630-a234c680-1fff-11e9-953d-cf23f87a2afc.png)

**5.03** If all the boolean toggles which are grouped red (indicating that they trigger a calculation) are still set to True, then the changes made in **5.01** and **5.02** should automatically re-run the simulation. You should now see the following Energy Balance Diagram in the Rhino modeling space:
![06_unconditioned without shading](https://user-images.githubusercontent.com/44324576/51693915-17080080-2000-11e9-9219-fd8c2399a44a.jpg)

**5.04** Compare this to our first Energy Balance Diagram (below). The tallies for monthly cooling and monthly heating are gone.
![06_without shading](https://user-images.githubusercontent.com/44324576/51693917-17080080-2000-11e9-8aa8-84d234d4dd35.jpg)

**5.05**  We can also see that the component of heat gains to the zone is still dominated by the sun, so next we will account for context which shades the house to our model. Recall our original model:
![context with north](https://user-images.githubusercontent.com/44324576/51699509-322d3d00-200d-11e9-9622-3538afae3643.jpg)


For sake of simplicity, we will ignore the effect of the attic space in the roof. These are the elements we will add to the shading component: two trees to the south, an extension of the roof to the south, and the car port entrance on the northern side. 
![005_single zone_shade overlay](https://user-images.githubusercontent.com/44324576/51695123-98f92900-2002-11e9-964b-a786602a1ecf.jpg)

**5.06** In the grasshopper script, this is achieved by creating a geometry component, placing the geometry from **5.05** in that component, and connecting it to a Honeybee EP Context Surfaces component, which then is connected to the Honeybee_Export To OpenStudio component. See the central group highlighted in yellow below:
![06_iterating through designs](https://user-images.githubusercontent.com/44324576/51693280-f2f7ef80-1ffe-11e9-8163-9c24766b27bb.png)
Here is a zoomed-in view that is more legible.:
![06_iterating through designs_change 2_v2](https://user-images.githubusercontent.com/44324576/51695389-394f4d80-2003-11e9-90b2-6034cfd00a39.png)

**5.06** You can now see that the solar contribution to heating is dramatically reduced.
![06_unconditioned with shading](https://user-images.githubusercontent.com/44324576/51693914-17080080-2000-11e9-8e2b-576d578dc05b.jpg)

This concludes the section on iterating to adjust the results of our initial single-zone model. You have now begun to make comparisons between different design options using an Energy Balance Diagram. 