We now proceed to HoneyBee Single Zone Step 2. Simulation Setup, highlighted in red below. 
![s03_00_ overview step 3](https://user-images.githubusercontent.com/44324576/51675610-751eee80-1fd4-11e9-8349-1eb30ab5cc8a.png)

Here you can see how it relates to the previous section on creating Honeybee Zones, and the next step on running the simulation.  
![s04_00_climate data_cropped](https://user-images.githubusercontent.com/44324576/49234839-1afd1500-f3f9-11e8-8e09-13b003d2fe75.png)
_Note that in order to avoid creating a separate tutorial for the out-dated Energy+ only component we will technically be running the simulation using the OpenStudio Engine, which is a superior cross-platform software capable of combining Radiance-based lighting simulations with Engery+ energy simulations. We will simply ignore the Radiance capabilities of the engine for this demonstration._

**2.00** The first step is to bring in climate data, exactly in Step 2.30. Drag a Ladybug-0-Ladybug Open EPW and STAT Weather Files component onto the canvas.

![s04_simulation setup_0000_step 0](https://user-images.githubusercontent.com/44324576/49236199-e8085080-f3fb-11e8-80c3-c862a69887b2.jpg)

**2.01** Create a panel (by typing //, or by dragging it onto the canvas from the first Params tab) Enter the URL containing the location of the weather data you would like to use, in this case we will use Van Nuys California: https://www.energyplus.net/weather-download/north_and_central_america_wmo_region_4/USA/CA/USA_CA_Van.Nuys.AP.722886_TMY3/all
![s04_simulation setup_0001_step 1](https://user-images.githubusercontent.com/44324576/49236206-eb9bd780-f3fb-11e8-8092-fd86ed3d5049.jpg)

**2.02** We will now create a list of the outputs that we would like to retrieve from the simulation once it is complete. Note that almost all of these outputs are simulated whether or not we complete this step. Recording the results takes time though, and Honeybee has been developed to give users as much control over calculation times as possible. 

Drag a Honeybee-10-Honeybee_Generate EP Output component onto the canvas. This component supplies the list of outputs we would like to request from the OpenStudio simulation. Honeybee uses a boolean data-type to indicate 'yes' I want to request this data or 'no' I do not want to request this data. 'True' means yes and 'false' means no. You can use a boolean toggle to create a 'true' or 'false', or you can create a panel and simply type 'true' or 'false' (without quotations).
![s04_simulation setup_0002_step 2](https://user-images.githubusercontent.com/44324576/49236209-eccd0480-f3fb-11e8-80e0-461e95f5b30f.jpg)
_Note that the list of available data types on Honeybee_Generate EP Output only includes the most commonly requested outputs. For a complete list of all available outputs through OpenStudio, look here: https://bigladdersoftware.com/epx/docs/8-3/input-output-reference/index.html. Alternatively, the Honeybee-10-Honeybee_Read Results Dictionary component can provide you with a list of all outputs after a simulation has been run._ 

The initial setup of providing local climate data and rquestiong specific outputs is now complete, lets proceed to running the simulation.