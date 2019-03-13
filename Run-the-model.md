
The next step of the process is collecting the information we have entered thus far to run our first energy simulation. We focus on Step 3, highlighted in red below:
![s03_00_ overview](https://user-images.githubusercontent.com/44324576/51686499-c6d57200-1ff0-11e9-8708-03b5f2cb2583.png)


Zooming in, observe that we will connect outputs from both Step 1 and Step 2.
![s04_00_connection to open studio_crop](https://user-images.githubusercontent.com/44324576/49238365-8d252800-f400-11e8-8545-6dc35671295c.png)



**3.00** The key component for this process is the Honeybee-10-Honeybee_Run Energy Simulation component, which collects all the inputs we prepared, fills in the blanks with default values, and prepares a set of instructions for the OpenStudio simulation engine. This set of instructions is saved in the form of an OSM file. After we have run the simulation, we will show you what an OSM file looks like.
![05_00_run simulation_cropped_0000_step 1](https://user-images.githubusercontent.com/44324576/49255094-48fb4d00-f42b-11e8-8688-ae2a2edd2151.jpg)

_Note on versions: Do not confuse the Honeybee_Export to OpenStudio with the out-dated Honeybee_Run Energy Simulation component! The OpenStudio component does everything the old component does and more. We retain the old component in the Honeybee library only for the sake of allowing users to continue using scripts that are already written_
![05_verions](https://user-images.githubusercontent.com/44324576/49256977-0fc5db80-f431-11e8-8448-498c69de5edd.png)
_The relationship between the OpenStudio component and the old EnergyPlus only component is related to the development of Honeybee more generally, as described in the following two diagrams. OpenStudio acts as a hub between Honeybee and EnergyPlus, which expands the set of functions and features from those available in EnergyPlus alone._
![software evolution 02](https://user-images.githubusercontent.com/44324576/51989233-e5cb7c80-24a6-11e9-8762-4f506e842115.JPG)
![software evolution 01](https://user-images.githubusercontent.com/44324576/51989236-e6fca980-24a6-11e9-83a8-413f623443b3.JPG)


**3.01** Connect the EPW Weather File from Step 2 to the Honeybee_Export to OpenStudio component.
![05_00_run simulation_cropped_0001_step 2](https://user-images.githubusercontent.com/44324576/49255095-48fb4d00-f42b-11e8-9c1f-9e8a38c34bdf.jpg)

**3.02** Connect the Zones that have Windows as 'children' from Step 1.
![05_00_run simulation_cropped_0002_step 3](https://user-images.githubusercontent.com/44324576/49255096-48fb4d00-f42b-11e8-8616-ee7069e71280.jpg)

**3.03** Connect the list of desired simulation outputs from Step 2.
![05_00_run simulation_cropped_0003_step 4](https://user-images.githubusercontent.com/44324576/49255097-48fb4d00-f42b-11e8-81bd-673f3fe42ae1.jpg)

**3.04** We will need a boolean toggle to run the simulation, but don't change it to True just yet! We will use the same boolean toggle to tell Honeybee that we'd like to save a copy of the OSM file that contains all the settings for our simulation. Note that it is connected to two terminals in the diagram below:
![05_00_run simulation_cropped_0004_step 5](https://user-images.githubusercontent.com/44324576/49255099-48fb4d00-f42b-11e8-8d2d-d30d6dd81454.jpg)

**3.05** We will also specify a name for the simulation output file. This makes it possible to save the output instead of over-writing it each time. Use a panel to do this. We name the file LAHouse.
![05_00_run simulation_cropped_0004_step 5 5](https://user-images.githubusercontent.com/44324576/49256165-6bdb3080-f42e-11e8-8689-ef2a619ef127.jpg)

**3.06** Finally, change the boolean toggle to True to run the simulation. This may take several minutes, depending on the processing power of your computer.
![05_00_run simulation_cropped_0005_step 6](https://user-images.githubusercontent.com/44324576/49255100-4993e380-f42b-11e8-8d05-bcab2c6967da.jpg)

**3.07** As we promised in step one, you can now view the actual set of instructions and settings Honeybee sent to OpenStudio. These are contained in the OSM file, which you can find by connecting a panel to the osmFileAddress output.
![05_00_run simulation_cropped_0005_step 7 osm](https://user-images.githubusercontent.com/44324576/49258081-7dbfd200-f434-11e8-8833-1bc4e751f845.jpg)


**3.08** Here is a portion of the OSM file. Note that Honeybee has filled in many of the default settings. For example, we have not yet set an analysis period, but the Begin Month of the simulation is 1 (January), and the End Month is 12 (December). If you open the file on your computer, you will see it is quite long, but this gives you an idea of this process.
![osm file sample](https://user-images.githubusercontent.com/44324576/49251487-befab680-f421-11e8-8553-f94d9c21fa92.JPG)

Our main concern, however is the resultFile, which comes in the form of a .csv document, or comma separated values document. This format is commonly used for Excel spreadsheets, and next we will go through the process of parsing this spreadsheet to get the information we need to create an Energy Balance diagram in Step 4.