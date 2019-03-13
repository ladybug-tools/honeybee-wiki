We will now run through the process of visualizing the output data into an Energy Balance Diagram like the one below. This diagram keeps track of heat moving into and out of the zone. 

![001_energy_balance](https://user-images.githubusercontent.com/44324576/49155416-2c6fef80-f31b-11e8-88c3-f52a9aa72e7b.JPG)
_Energy modeling draws upon the First Law of Thermodynamics, which states that energy can never be created or destroyed. This diagram summarizes the sources of heat entering and leaving the zone. Heat entering the zone might include heat from people, heat from computers/appliances, heat from light bulbs, solar heat through windows, and heat from heating systems like radiators. Heat losses from the zone might be the result of conduction through the envelope, cool air seeping through walls, or deliberate ventilation. Everything above zero is heat entering the zone, and everything below zero is heat leaving the zone. These must always be equal._

Directing your attention toward the final part of the example file script:
![overview_red](https://user-images.githubusercontent.com/44324576/51702111-3f4d2a80-2013-11e9-914b-3d89486dcae1.png)

**4.00** Begin with the result file from Step 3.
![energy balance diagram_0000_step 0](https://user-images.githubusercontent.com/44324576/49261762-d8145f00-f443-11e8-975a-008cede152bb.jpg)

**4.01** The result file is a huge comma separated values document, so we use a Honeybee-10-Honeybee_Read EP Results component to separate out each of the simulation results we are interested in visualizing.
![energy balance diagram_0001_step 1](https://user-images.githubusercontent.com/44324576/49261765-d8145f00-f443-11e8-86a5-7b3ae9944bf7.jpg)

**4.02** You can see that each of these results is a list containing 8767 values. The first seven items in this list are the 0) the key, 1) the location, 2) the data type, 3) the units, 4) the frequency, 5) the start date (Month, Day, Hour), and 6) the end date (Month, Day,Hour). The remaining 8760 items are for each hour of the year. 
![energy balance diagram_0002_step 1_annotated](https://user-images.githubusercontent.com/44324576/49261766-d8145f00-f443-11e8-9266-c71de5ba6e1e.jpg)

**4.03** These hourly results are all compiled in the Honeybee_Construct Energy Balance component.
![energy balance diagram_0003_step 2](https://user-images.githubusercontent.com/44324576/49261768-d8acf580-f443-11e8-8391-aec7d34d67bf.jpg)

**4.04** Which also requires the zones we created in step 2 in order to match these itmes to the zones of interest.
![energy balance diagram_0004_step 3](https://user-images.githubusercontent.com/44324576/49261771-d8acf580-f443-11e8-9cc0-5fc342c1da95.jpg)

**4.05** Althought we have the zones, and we have the overall amount of heat moving in and out of the building, we do not yet have the information necessary to identify the contributions of individual zone surfaces. For this, we need the Honeybee-10-Honeybee_Read EP Surface Results component.
![energy balance diagram_0006_step 4](https://user-images.githubusercontent.com/44324576/49261774-d8acf580-f443-11e8-863d-a4e55aac2d39.jpg)

**4.06** To describe what this component is doing, we are going to use the Param Viewer component (available in the utilities section of the Params tab). Connect one Param Viewer to the FlrNormBalWStorage output of the Honeybee)Construct Energy Balance component. Connect another to the cooling output stream of the Honeybee_Read EP Results component. 

![energy balance diagram_0005_step 4_annotated](https://user-images.githubusercontent.com/44324576/49263166-a69e9200-f449-11e8-88b0-c15e63230cfc.jpg)
_The Param viewer tells us how many lists are contained in a data stream, and how many items are in each list. We can see that the cooling hourly data is a single list of 8676 values. However, the output of the Honeybee_Construct Energy Balance component contains ten lists with 8767 values each. These lists collect all the other lists into a list of lists. These ten lists represent 0) Heating, 1) Solar, 2) Equipment, 3) Lighting, 4) People, 5) Infiltration, 6) Mechanical Ventilation, 7) Opaque Conduction, 8) Cooling, and 9) Storage. Notice these are numbered starting at 0, this is a convention in most coding languages._


**4.07** To visualize the data on a monthly basis instead of a daily basis, we will use the Ladybug_Average Data component to make the conversion.
![energy balance diagram_0007_step 5](https://user-images.githubusercontent.com/44324576/49261775-d9458c00-f443-11e8-8595-23a481ea0037.jpg)

**4.08** Observe that each of the lists that once contained 8767 values now contain just 19 values each. (7 for information about the data + 12 for each month of the year)
![energy balance diagram_0008_step 5_annotated](https://user-images.githubusercontent.com/44324576/49261776-d9458c00-f443-11e8-9854-808b08799e80.jpg)

**4.09** Finally, we have the data in the right format for a monthly bar chart. Drag a Ladybug_Monthly Bar Chart component onto the canvas.
![energy balance diagram_0009_step 6](https://user-images.githubusercontent.com/44324576/49261778-db0f4f80-f443-11e8-85a7-5c23426152b2.jpg)

**4.10** Use a boolean toggle in the True position to stack the values on the chart.
![energy balance diagram_0010_step 7](https://user-images.githubusercontent.com/44324576/49261780-dba7e600-f443-11e8-97c4-a5a47859f3c8.jpg)

**4.11** Use a Panel to label the Y Axis with 'Energy Intensity (kWh/m2)'.
![energy balance diagram_0011_step 8](https://user-images.githubusercontent.com/44324576/49261782-dcd91300-f443-11e8-8a6e-919ae8e2ebdc.jpg)

**4.12** Use another Panel to set the base point of the chart to (70,0,0).
![energy balance diagram_0012_step 9](https://user-images.githubusercontent.com/44324576/49261783-dcd91300-f443-11e8-8a86-082c5c429e30.jpg)

**4.13** Finally, we will adjust the color of the chart using a Ladybug_Legend Parameters component.
![energy balance diagram_0013_step 10](https://user-images.githubusercontent.com/44324576/49261784-dd71a980-f443-11e8-96b5-0518d14ca523.jpg)

**4.14** We'll take item 19 of the Ladybug Gradient library, which has been designed for Energy Balance visualizations.
![energy balance diagram_0014_step 11](https://user-images.githubusercontent.com/44324576/49261785-dd71a980-f443-11e8-8240-763c8213bf08.jpg)

**4.15** Rhino's modeling space should now contain an Energy Balance Chart. 
![energy balance diagram](https://user-images.githubusercontent.com/44324576/49264216-b0c28f80-f44d-11e8-9cfd-f0d9a04d6e02.jpg)
This represents a simulation of a very simple box model, as pictured below. We have not yet accounted for context. 
![005_single zone](https://user-images.githubusercontent.com/44324576/51697197-8c2b0400-2007-11e9-9128-c2c75db22a02.jpg)


**4.16** As a demonstration, try disconnecting the wire highlighted in red below. This will remove the surface calculations from the Energy Balance Diagram. In layman's terms, this is removing the component of the calculation that accounts for the heat conducted through each individual surface of the zone, meaning that all the heat which the simulation expects to be conducted through the wall now appears as simply being stored in the material.
![energy balance diagram_0014_step 12_storage](https://user-images.githubusercontent.com/44324576/49264180-883a9580-f44d-11e8-8198-640cb9f03d64.jpg)

**4.17** Observe that the storage component of the Energy Balance Diagram is significant now. This storage component refers to energy stored in the building's mass. If you have input all of the terms of your Energy Balance into the Honeybee_Construct Energy Balance component, the storage term should be very small compared to the other terms. This storage term is a good way of checking whether all of your energy balance terms are accounted for.

![energy balance diagram_storage](https://user-images.githubusercontent.com/44324576/49264238-c9cb4080-f44d-11e8-9461-aa8ab38956fc.jpg)

This concludes the section on creating a single-zone energy model. 

You should now feel comfortable with the following:
1. Creating Honeybee Zones with Windows
2. Inputting climate data with Ladybug
3. Specifying desired outputs for OpenStudio 
4. The role of an OSM file as Honeybee communicates with OpenStudio
4. How to read the data the result file produces
5. How to convert hourly data to monthly averaged data
6. How to create an Energy Balance diagram
