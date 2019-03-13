_Contributors_:
<a href="https://github.com/alexandermatthias" title="Alexander Matthias Jacobson"><img src="https://github.com/alexandermatthias.png" height="24"></a>
# 

# Honeybee Wiki Home

Welcome to the Official Honeybee Wiki, for guides to energy modeling using Honeybee. 

The **Single Zone Model** guide covers creating suitable geometry in Rhino, specifying inputs and settings for an energy model, sending the energy model to a simulation engine, and interpreting the results of that simulation. Honeybee uses components from Ladybug, which is another open-source plugin for Grasshopper designed for importing climate data, visualizing the data, and performing geometric analysis. 

The **Comparing Passive Strategies** guide builds upon the the Single Zone Model, to explain the framework Honeybee uses for adding more layers of nuance to your simulation. This section shows how to study five common design strategies and it is intended as an intermediate step to more advanced topics.

In **Topics**, the format of these tutorials changes. Instead of walking through a sequential set of step-by-step instructions, the guide branches out to address methods for addressing specific modeling techniques / design issues. There are several reasons for this transition:
1. It would be impossible for us to write a single sequential tutorial that meets everyone's needs. 
2. Designers are often looking for methods of evaluating a specific design problem, and this way the guide can act as a repository of methods / best-practices.
3. This format makes it much easier for others to contribute to the guide.

## Overview of Honeybee Energy Modeling Workflow

The relationship between Rhino, Grasshopper, Ladybug, Honeybee and the simulation engines Honeybee communicates with is described in the diagram below. Ladybug is the simpler tool to use, and it provides many tools valuable to the early design phases. Honeybee makes it possible to delve much deeper and provide more nuanced analysis.

![depth of analysis](https://user-images.githubusercontent.com/44324576/51753145-60685680-20b9-11e9-8526-299586429511.png)


Both Honeybee and Ladybug are necessary for following this guide, but it is not necessary to read the guides on Ladybug before proceeding. Minimum knowledge of Ladybug is covered here. 
If you are only interested in geometric analysis, Ladybug may be sufficient. For example, Ladybug can calculate the direction of sunlight at any given time, and even the number of hours of direct sunlight shining on a given piece of geometry over a year. However, Honeybee is necessary for anything that requires accounting for materials, like raytracing calculations of diffuse daylight, accounting for the resulting heat gains, simulating temperatures, or estimating total energy consumption.

![000_honeybee relation to other engines](https://user-images.githubusercontent.com/44324576/49177299-298df280-f34d-11e8-9f48-40bc1bac363c.jpg)

It's important to make one distinction clear: Honeybee does not actually run simulations.  Honeybee is an interface that creates instructions for other software programs ('engines') to run simulations.
As of Nov 2018 Honeybee has interfaces to five analysis engines: 
1. Radiance for point-in-time lighting
2. Daysim (which uses Radiance) for lighting over time
3. EnergyPlus for heat, electrical and fuel resource modeling
4. OpenStudio for integration of Radiance and EnergyPlus
5. Therm for conduction through construction models and condensation risk

For more information see Our Story on Ladybug.tools website (https://www.ladybug.tools/about.html).

### EnergyPlus Simulation Engine
This tutorial will deal primarily with the third engine, EnergyPlus. Technically, we will be using OpenStudio to send a simulation through EnergyPlus, but the important thing to understand is that EnergyPlus creates an energy model that tracks the movement of heat in and out of a building. The EnergyPlus simulation engine is an immense collection of work by 

### Thermal Zones

Buildings are described using 3D zones. Each zone represents a thermally distinct space. So, a building can be treated as a single zone, or it can be studied in more detail by treating each room as a separate zone. Honeybee has tools for creating these zones from geometry modeled in Rhino. Each zone is modeled as a closed 3D shape, and Honeybee has tools for assigning thickness and material properties to each surface of a zone. Windows and doors are treated as sub-elements which 'belong' to a particular surface of a zone.

Zones are the unit of analysis. To track the heat moving in and out of each zone over a period of time (i.e. an entire year), the simulation will run in time-steps (i.e. 10-minute intervals). As we set up the simulation, we will assign characteristics to each of these time steps. For example, we can refer to climate data for simulating conditions outside the zone, like outdoor hourly air temperature. We can also simulate conditions inside the zone using inputs like occupancy schedules or equipment schedules. We will also specify how equipment will respond to these interior and exterior conditions, by for example specifying thermostat set points.

### Simulation Calculations
Once we have used Honeybee to enter all the information we want to consider, we will instruct Honeybee to 'run' the simulation. At this point, Honeybee sends the inputs described above as a set of instructions to OpenStudio, which forwards instructions to the EnergyPlus simulation engine. The simulation engine will then run through each time-step of the specified period, and and return the raw output calculations to Honeybee. Honeybee has tools to analyze these results. For example it can retrieve specific metrics, visualize the energy balance of each zone, compare zones to each other, and aggregate results from several zones.

### Analyzing Results
As we analyze these results, we will check them for reasonableness, and identify which factors are contributing most to the energy use of the building. Once the simulation and analysis are complete, we have established one complete feedback loop through which we can begin to alter the design and test the impact of modifications on performance.

### Why create an energy model at all?
1. Informing design 
2. Forecasting energy use
3. Creating convincing arguments for design ideas
4. Building design intuition
5. Sensitivity analysis
6. Calculating payback periods for energy conservation measures (ECMs)
7. Code compliance
8. LEED BREAM or DGNB compliance

This guide is sufficient for the first five goals, but the nuances necessary to calculate payback periods and create code-compliant models are beyond the scope of this tutorial. 

### What results can I expect? 
It depends. There are many metrics that can be drawn from energy simulations, each targeted at assessing a particular aspect of the building's performance.

![list of metrics](https://user-images.githubusercontent.com/44324576/51490305-2e01e500-1dab-11e9-924c-90c3c64b662b.png)

The most frequently used result is the Energy Balance Diagram, which tracks energy moving into and out of a building. This is fundamental to the first law of Thermodynamics, which states that Energy can never be created or destroyed. Heat entering the building might include heat from people, heat from computers/appliances, heat from light bulbs, solar heat through windows, and heat from heating systems like radiators. Heat losses might be the result of conduction through the envelope, cool air seeping through walls, and through deliberate ventilation. These are tallied in a balance sheet:

![001_energy_balance](https://user-images.githubusercontent.com/44324576/49155416-2c6fef80-f31b-11e8-88c3-f52a9aa72e7b.JPG)

### Note on daylighting
EnergyPlus based simulations do account for specific geometry, and for the movement of
the sun. However, if you are interested in daylighting simulations that return specific
lighting levels then you are in the wrong place. These simulations can also be run using
Honeybee, however those calculations require the Radiance ray-tracing engine and are not
covered in this guide. There are plans for a wiki guide to daylighting, but as of Jan
2019 it has not yet been written.
