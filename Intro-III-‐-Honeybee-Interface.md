This section will cover how to build a very simple Honeybee script from scratch. It will start with a breif introduction to the Honeybee Interface, continue to create a basic Honeybee definition, and finally conclude with a list of conventions used in Honeybee scripts. This section should allow you to begin independently expanding your knowledge by browsing through the library of components.

## Honeybee Interface

The Honeybee interface arranges components by simulation type. 
Section 00 is primarily for defining zone geometry in energy simulations.
![s03_09_interface_honeybee primary components](https://user-images.githubusercontent.com/44324576/49173594-77522d00-f344-11e8-8b38-1faf1714ac00.png)

Section 02-04 are for daylighting. We will not use them in this tutorial.
![s03_09_interface_daylight](https://user-images.githubusercontent.com/44324576/49173589-76b99680-f344-11e8-84e5-aa729d9f1dc8.png)

Seciton 05-10 are for energy modeling in Energy+. They are the focus of this tutorial. 
![s03_09_interface_energy only](https://user-images.githubusercontent.com/44324576/49173915-47575980-f345-11e8-8abd-4b181702c279.png)

Section 11 components are for conduction simulations in THERM. We will not use them in this tutorial.
![s03_09_interface_therm](https://user-images.githubusercontent.com/44324576/49173595-77522d00-f344-11e8-8b87-9fe09ec4bec0.png)

Section 12 components update Honeybee, and Section 13 components are experimental or under development.
![s03_09_interface_export and under development](https://user-images.githubusercontent.com/44324576/49173592-77522d00-f344-11e8-8928-abd3b9476adf.png)

As an example of how these groupings work, take the current tutorial on single-zone energy simulations through Energy+. It only uses components from Primary Section 00, the Energy Sections 05, 06, 07, 08, 09, 10, and Update Section 12. It does not use any components from sections 02-04 on daylighting, or Section 11 on THERM.
![s03_09_interface_energy simulation](https://user-images.githubusercontent.com/44324576/49173591-76b99680-f344-11e8-8a88-550f37222797.png)

### Locating Components in Honeybee
To help you locate components, we will start by referring to them using the Grasshopper tab name, section name or number, and component name. For example HoneyBee | 04 Energy Material | Honeybee_Energy Plus Window Material would mean that you need to look in the Honeybee tab, under section 04 which is for specifying materials in energy simulations, and you would look for the name Honeybee_Energy Plus Window Material. You can also simply double-click in the canvas and type 'Energy Plus Window Material' (without the quotation marks), and select from the dynamic search list. 

If you encounter a component you do not recognize, there are a couple things you can do: 
- You can hover the mouse over the icon in the middle of the component to see the name of the component.
- If the component is outside Ladybug and Honeybee, you can also hold ctrl + alt at the same time to engage info mode. This shows the menu location of components already on the canvas. Unfortunately, for Ladybug and Honeybee, this will only point to the Python component. 
- A work-around for components within Ladybug and Honeybee is to double-click on a Ladybug or Honeybee component's icon itself, which will open the code inside. Scroll down to look for a line that starts with "ghenv.Component.SubCategory =" which will be followed with something like "07 | Energy | Schedule". This functions the same way as the address above, so in this case we know that the component is located in tab 7 on Energy, and is called Honeybee_Schedule.
- If you prefer to see names instead of icons, you can also enter the Display tab in Grasshopper's menu bar, and toggle Display Icons on or off, as this will display the name of the component instead of the icon.
- You can also double-click in the Grasshopper canvas and begin typing the name of a component to search through all of Grasshoppers Tabs. All Honeybee and Ladybug components start with either 'Honeybee' or 'Ladybug', so starting with one of those keywords is a way to search only within our plugins.
- Another helpful tool is the bifocals component, which creates a label above each component so that it is possible for you to see both the icon and the name of each component. The bifocals component is available on https://www.food4rhino.com/app/bifocals

## Creating a Honeybee Definition

**iii.00** The first step for creating any Honeybee script is _always_ to place the Honeybee component on the grasshopper canvas. This is important because this component contains several internal libraries that are necessary for nearly all other Honeybee components to function. Unlike most grasshopper scripts, it is not necessary to connect a wire between the Honeybee component and other components, simply placing it in the Grasshopper canvas activates the libraries. It is located on the 0 Honeybee | Honeybee tab, and dragging the Honeybee component onto the canvas is known as 'letting Honeybee fly'.
![s03_01_honeybee](https://user-images.githubusercontent.com/44324576/49170763-2d197d80-f33d-11e8-96fb-ca46f7fa79df.png)

**iii.01** Many Honeybee components work in tandem with Ladybug components, so we will _almost always_ need to let Ladybug fly too. Find the Ladybug Tab and look in Section 0 for the Ladybug component, and drag it onto the canvas.
![s03_02_ladybug](https://user-images.githubusercontent.com/44324576/49170767-2db21400-f33d-11e8-8269-ddf02cd3f166.png)

**iii.02** The next crucial step before we begin creating a simulation is to be sure that we have climate data upon which the simulation will be based. This requires an internet connection. To get started, find Ladybug Section 0 and drag Ladybug's Open EPW and STAT Weather File component to the canvas.
![s03_03_ladybug data](https://user-images.githubusercontent.com/44324576/49170768-2db21400-f33d-11e8-993e-66d13f1727ab.png)

**iii.03** This component will automatically downloas climate data from the internet once we provide it with a URL internet address. We will use a panel component to type the address into, so drag a panel onto the Grashopper canvas. 
![s03_04_panel](https://user-images.githubusercontent.com/44324576/49170769-2db21400-f33d-11e8-8461-b6c947b936a5.JPG)

**iii.04** Double-click the panel component and paste the following URL link inside, without spaces before or after. It is also important not to press ENTER after entering text into a panel component, because Grasshopper interprets ENTER as creating a second item in the panel's list of data. For clarification on lists of data, see Step 2.20.
- https://www.energyplus.net/weather-download/north_and_central_america_wmo_region_4/USA/CA/USA_CA_Van.Nuys.AP.722886_TMY3/all

This data is from the US Department of Energy, collected at the airport in Van Nuys, California. Hovering over the component provides more detail on finding weather data for other locations, or you can browse for weather data files and download them from the US Department of Energy here: https://www.energyplus.net/weather, and read about the data itself here: https://energyplus.net/weather/sources. 

![s03_04_panel_full](https://user-images.githubusercontent.com/44324576/49170770-2e4aaa80-f33d-11e8-9a83-fa2d5160dc66.JPG)
_Tip on panels: We will use panels to enter information frequently. Rather than dragging a panel into the canvas each time, simply double-click on the canvas and type '//' followed by the data you wish to enter into the panel._

 **iii.05** Connect the panel containing the weather file URL to the _weatherFileURL input of the Open EPW and STAT Weather Files component. You should notice that the Open EWP and STAT Weather Files component has turned from orange to grey, indicating that it has collected data without errors. 
![s03_06_panel_connected](https://user-images.githubusercontent.com/44324576/49170772-2ee34100-f33d-11e8-8a8f-07541ecf2991.JPG)

**iii.06** If you connect a panel to the epwFile output of Open EPW and STAT Weather Files component, and hover over the 'epwFile' text, you will see that Ladybug has downloaded an EPW file and saved it on your local drive. The default location is here: c:\ladybug\
![s03_06_panel_confirm](https://user-images.githubusercontent.com/44324576/49170771-2e4aaa80-f33d-11e8-86b7-4748521bbbbf.JPG)

**iii.07** This weather data can now be used for any number of simulations. We will wrap up this tutorial by showing how to explore the data that you've just imported. Start by pulling a Ladybug_Import EPW component onto the canvas. 
![intro iii-import epw_location](https://user-images.githubusercontent.com/44324576/51679914-8c63d900-1fe0-11e9-8200-027a9ceb0b81.JPG)

**iii.08** Then connect the data we imported before to this component. This will allow us to parse through many different types of data contained in the initial file we imported.

![intro iii-import epw_connect](https://user-images.githubusercontent.com/44324576/51679917-8cfc6f80-1fe0-11e9-9c08-a4357165722e.JPG)

**iii.09** The Ladybug_Import EPW component should now change from orange to grey, indicating data was collected without errors. 
![intro iii-import epw](https://user-images.githubusercontent.com/44324576/51679916-8cfc6f80-1fe0-11e9-9364-74698dc7f7e0.JPG)

**iii.10** We now have access to many types of data contained in the EPW File, lets connect panels to the first four inputs and take a closer look at the information that is now available to us. 
![intro iii_basic script](https://user-images.githubusercontent.com/44324576/51679915-8c63d900-1fe0-11e9-8f5f-a1c743b7b68d.png)

**iii.11** The readme output provides useful information on whether the component worked correctly. This is particularly important if the component is orange, which indicates that there was an error. 
![intro iii_panels_0004_02](https://user-images.githubusercontent.com/44324576/51680591-73f4be00-1fe2-11e9-9106-c303cea225c9.jpg)
_Note how disconnecting the URL address we entered earlier affects this ouput:_
![intro iii_panels_0004_02_error](https://user-images.githubusercontent.com/44324576/51680758-ea91bb80-1fe2-11e9-8ed5-eb3d7d461fdf.jpg)

**iii.12** The latitude will provide the latitude at which the data was collected. This is extremely important for confirming that accuracy of solar geometry. 
![intro iii_panels_0003_03](https://user-images.githubusercontent.com/44324576/51680593-7525eb00-1fe2-11e9-865d-83531de1f298.jpg)

**iii.13** The next output provides more information bout the location such as the name of the location, latitude, longitude, timezone, and elevation. The timezone is expressed by the number of hours difference from Greenwhich, UK. Positive values are east, negative values are west. The elevation is in meters.
![intro iii_panels_0002_04](https://user-images.githubusercontent.com/44324576/51680594-75be8180-1fe2-11e9-97e2-668a53e7c247.jpg)

**iii.14** All the following outputs contain hourly data. Lets take dry bulb temperature as an example. 

The first seven entries contain information about the data, and the following 8760 values contain data points for each hour of the year. The convention for lists in Grasshopper is to start numbering at 0, so a list with 7 values will read values 0 through 6. 
- Value 0 is a key 
- Value 1 is the name of the location
- Value 2 is the type of data
- Value 3 is the units of that data
- Value 4 is the frequency at which it was recorded
- Values 5 and 6 represent a time span over which the data was collected. The format here is (month of the year, day of the month, hour of the day). So we can see this data was collected from January 1st on the first hour of the day between 00:00-01:00 until December 31st on the 24th hour of the day, from 23:00-00:00. 

![intro iii_panels_0001_05](https://user-images.githubusercontent.com/44324576/51680596-76efae80-1fe2-11e9-822d-16c10510109e.jpg)

**iii.15** Try scrolling through all 8760 values by dragging the dark yellow scroll-bar (marked by a red dot below).
![intro iii_panels_0000_05a](https://user-images.githubusercontent.com/44324576/51680597-78b97200-1fe2-11e9-8e26-925981b8416e.jpg)

**iii.16** Finally, we will drag a Ladybug_Sunpath component onto the canvas to explain a few important conventions and to show how you can use the Ladybug and Honeybee interface to learn about the components available to you. The sunpath component creates geometry that shows the movement of the sun over the course of an entire year.
![intro iii_sunpath](https://user-images.githubusercontent.com/44324576/51682324-6ee63d80-1fe7-11e9-9421-faf5311f8ceb.JPG)

**iii.17** Observe that some of the inputs for the sunpath component are preceded by an underscore, and others have a trailing underscore. For example, the first input terminal is labelled 'north_', whereas the second is labeled '_location'. This is a convention used throughout Ladybug and Honeybee to distinguish necessary inputs from optional inputs. If a necessary input is left empty, the component will not run. Notice that even though the sunpath component is on the Grasshopper canvas, nothing appears in Rhino's modeling space. 
![intro iii_basic script_plus sunpath](https://user-images.githubusercontent.com/44324576/51682973-0ac47900-1fe9-11e9-8d89-cdfbcb40ddef.png)

**iii.18** Once we connect the location output of the Ladybug_Import EPW component to the location input of the Ladybug_SunPath component, there is enough information for the Ladybug_SunPath component to run.
![intro iii_basic script_plus sunpath_connected](https://user-images.githubusercontent.com/44324576/51682979-0c8e3c80-1fe9-11e9-927a-ec5cb6b29399.png)

**iii.19** You should now see something like this in your Rhino modelling space. Be aware that the default scale of this diagram is 400 Rhino units wide, and it will be located at 0,0,0 so you may need to zoom in or out to see it.
![sunpath](https://user-images.githubusercontent.com/44324576/51682958-fed8b700-1fe8-11e9-9389-639f119addbb.jpg)

**iii.20** You may have noticed that there are many inputs which are preceded by an underscore, but still left empty. Yet, the component still runs. This is because many inputs can assume a sensible default value. It would be meaningless to assume a default location for the sun's path because the geometry depends entirely upon the latitude of the location of study. However, one could assume that the default period of analysis is an entire year.

**iii.21** Hover your mouse over different areas of the component to learn more about required inputs, default assumptions, formats for inputting data, and sometimes even references for research papers upon which the components calculations are based. 

Here is what you will see when hovering over the location input:
![intro iii_learning 2](https://user-images.githubusercontent.com/44324576/51683837-0e58ff80-1feb-11e9-9f9b-449f71302681.JPG)
Here is what you will see when hovering over the center of the sunpath component, which applies to the entire component:
![intro iii_learning 1](https://user-images.githubusercontent.com/44324576/51683839-0ef19600-1feb-11e9-8f07-85cdd3627f9d.JPG)
Finally, hovering over one of the outputs:
![intro iii_learning 3](https://user-images.githubusercontent.com/44324576/51683838-0e58ff80-1feb-11e9-9f23-e094a8718f46.JPG)

**iii.22** The sequence in which components run on Grasshopper canvas is also important to mention. Grasshopper components usually run in the sequence that they are placed and connected to each other on the canvas. So ordinarily components would run in the following sequence:
![intro iii_sequence of calculations_normal](https://user-images.githubusercontent.com/44324576/53178720-b6fe7d00-35f2-11e9-8179-ebfa9c356bcf.png)

However, the Ladybug_Ladybug and Honeybee_Honeybee components _always_ run first. This is good, because it means that data, functions, and libraries contained in those two components are made accessible to all the others that run afterwards. This is true _even if a wire is not connected_. So, the true order of calculation is below:
![intro iii_sequence of calculations_hb and lb](https://user-images.githubusercontent.com/44324576/53178724-b82faa00-35f2-11e9-8761-0f7477b18c63.png)

This brings us full circle to the explanation in **ii.00** above. Usually, you have to connect a wire between two components in order to transfer data from one to another. This is not the case here. The library is made available because the Honeybee_Honeybee component runs first, and this makes it possible for it to perform many functions "in the background."

As you learn more about Honeybee, you will come to understand some of the advantages of writing the code this way. For example, it makes it easy to create a standard library of Radiance Materials that can be accessed from multiple grasshopper definitions.

#

This concludes the Honeybee Basics section. You should now be familiar with the following:
1. The layout of the Ladybug and Honeybee interface
2. The importance of letting Honeybee and Ladybug fly 
3. Entering information in a panel component
4. Downloading climate data
5. Importing climate data
6. Examining imported data
6. The _before or after_ convention for necessary vs optional inputs
7. Learning about components, inputs and outputs by hovering over them
