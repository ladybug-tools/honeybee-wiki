Assigning Zone Default Properties is the first of several steps necessary for running a simulation. This will also be our entry into Grasshopper and the Honeybee interface. If you are completely unfamiliar with Grasshopper and Honeybee, refer to the Intro sections which cover the basics. 

This is an overview of the entire script we will create for a Single Zone Energy Model. This step on Assigning Zone Default Properties covers the portion highlighted in red. If you are following along, be certain that you let Honeybee and Ladybug fly, as covered in Intro III and as visible at the very left of the diagram below.  
![s03_00_overview](https://user-images.githubusercontent.com/44324576/51673655-d5129680-1fce-11e9-9f97-66e6f5418b6d.png)
Zooming in and reading from left to right, observe that first we will create components that contain the geometry. The geometry is then used to create zones with a default set of properties. Then, the windows are added as children to those zones.
![s03_00_overview_zoom](https://user-images.githubusercontent.com/44324576/51674124-1fe0de00-1fd0-11e9-9e4e-7b7ef4f796be.png)

 ### Step-by-step

**1.00** First we create a geometry component, and rename it House Zone (refer to **ii.05** if you are unsure how to create components and rename them). We then place the zone geometry constructed according to the guidelines in Step 1 into this component. 
![s03_10_assign default zones__0000_step 1](https://user-images.githubusercontent.com/44324576/49189563-1e4bbe80-f36f-11e8-8537-193ce899aa3a.jpg)

Here is an image of the zone which is loaded into this Geometry component, overlayed on top of the model context it represents.
![005_single zone_overlay](https://user-images.githubusercontent.com/44324576/49190883-7df89880-f374-11e8-940b-a95f99c58fad.jpg)


**1.01** The Honeybee Masses to Zones component converts the zone geometry into a zone which can be imported into Energy+. As is apparent from the '__' in front of zone Masses and createHBZones, the only two required inputs for this are the zone masses and a boolean toggle to trigger the creation. 
We only have one zone in this case, so we will save zone naming for a later example with multiple zones.

![s03_10_assign default zones__0001_step 2](https://user-images.githubusercontent.com/44324576/49189556-1db32800-f36f-11e8-8f03-f982dafb3d43.jpg)

**1.02** Honeybee has a library of default settings for Energy+ models that we can choose from. The Honeybee bldgPrograms component allows you to choose from a list of very generic programs. The Honeybee_ListZonePrograms offers a more detailed list of room types within each of these programs, that each correspond to a set of default settings and schedules for simulation. The Honeybee_Item Selector allows you to choose one of these sub-programs to connect to the Masses2Zones input for zoneProgram.
![s03_10_assign default zones__0002_step 3](https://user-images.githubusercontent.com/44324576/49189557-1db32800-f36f-11e8-8dde-ff6e9af4d48b.jpg)

**1.03** When a boolean toggle set to True is connected to the create Honeybee Zones input, the Mass2Zones component searches the Energy+ library of default settings for a room type of 'Apartment' within the Building Type of 'MidriseApartment' and applies those schedules to the zone geometry attached to the component. This is a good example of why it is important to have the Honeybee component flying. The Mass2Zones component does not contain all of these default libraries itself, it searches through libraries contained in the Honeybee component and applies the appropriate settings.

![s03_10_assign default zones__0003_step 4](https://user-images.githubusercontent.com/44324576/49189558-1db32800-f36f-11e8-9189-50b314eae95b.jpg)

**1.04** Once zones are created, apply windows as children to the zone. This is done using the Honeybee Add Glazing component (Honeybee-00-Honeybee_addHBGlz). 
![s03_10_assign default zones__0004_step 5](https://user-images.githubusercontent.com/44324576/49189559-1db32800-f36f-11e8-81e2-1f3937621c17.jpg)

**1.05** Create another Geometry component, rename it House Windows and load the following windows into the component. Review **0.07** for geometric requirements for modeling windows.
![005_single zone_windows overlay](https://user-images.githubusercontent.com/44324576/51674921-6fc0a480-1fd2-11e9-8834-58054e2c5887.jpg)


**1.06** Then connect the House Windows geometry to the _childSurfacese input terminal of the Honeybee_HBaddglz component. As you can see from the other terminals on this component, it is also possible to provide a list of names for these windows and to provide construction details and Radiance Materials for the windows. 
![s03_10_assign default zones__0005_step 6](https://user-images.githubusercontent.com/44324576/49189560-1e4bbe80-f36f-11e8-9ff4-e52bf5159263.jpg)


The zones have now been created with default settings and windows. It is time to move on to Step 4. Assigning Climate Data and Selecting Simulation Output.