# Introduction to Energy Simulation in Honeybee

This is a walk-through of creating energy models using Honeybee. It covers creating suitable geometry in Rhino, specifying the input properties and settings necessary for running an energy model, sending the energy model to a simulation engine, and interpreting the results of that simulation. 

## Overview of Honeybee Energy Modeling Workflow
![000_honeybee relation to other engines](https://user-images.githubusercontent.com/44324576/49177299-298df280-f34d-11e8-9f48-40bc1bac363c.jpg)

It's important to make one distinction clear: Honeybee does not actually run simulations.  Honeybee is an interface that creates instructions for other software programs ('engines') to run simulations. As of Nov 2018 Honeybee has interfaces to five analysis engines: 1. Radiance for point-in-time lighting, 2. Daysim for lighting over time, 3. Energy+ for energy and resource consumption, 4. Open Studio for integration of Radiance and Energy+, and 5. Therm for conduction through construction models and condensation risk. For more information see Our Story on Ladybug.tools website (https://www.ladybug.tools/about.html).

This tutorial will deal primarily with the third engine, Energy +. Technically, we will be using Open Studio to send a simulation through Energy+, but the important thing to understand is that Energy+ creates an energy model that tracks the movement of heat in and out of 3D zones. Each zone represents a thermally distinct space. So, a building can be treated as a single zone, or it can be studied in more detail by treating each room as a separate zone. Honeybee has tools for creating these zones from geometry modeled in Rhino. Each zone is modeled as a closed 3D shape, and Honeybee has tools for assigning thickness and material properties to each surface of a zone. Windows and doors are treated as sub-elements which 'belong' to a particular surface of a zone.

These zones are the unit of analysis. To track the heat moving in and out of each zone over a period of time (i.e. an entire year), the simulation will run in time-steps (i.e. 10-minute intervals). As we set up the simulation, we will assign characteristics to each of these time steps. For example, we can refer to climate data for simulating conditions outside the zone, like outdoor hourly air temperature. We can also simulate conditions inside the zone using inputs like occupancy schedules or equipment schedules. We will also specify how equipment will respond to these interior and exterior conditions, by for example specifying thermostat set points.

Once we have used Honeybee to enter all the information we want to consider, we will instruct Honeybee to 'run' the simulation. At this point, Honeybee sends the inputs described above as a set of instructions to Open Studio, which forwards instructions to the Energy+ simulation engine. The simulation engine will then run through each time-step of the specified period, and and return the raw output calculations to Honeybee. Honeybee has tools to analyze these results. For example it can retreive specific metrics, visualize the energy balance of each zone, compare zones to each other, and aggregate results from several zones.

As we analyze these results, we will check them for reasonableness, and identify which factors are contributing most to the energy use of the building. Once the simulation and analysis are complete, we have established one complete feedback loop through which we can begin to alter to the design and test the impact of modificaitons on performance.

## Common reasons for energy modeling include:
1. Informing design 
2. Forecasting energy use
3. Creating convincing arguments for design ideas
4. Building design intuition
5. Sensitivity analysis
6. Calculating payback periods for energy conservation measures (ECMs)
7. Code compliance
8. LEED BREAM or DGNB compliance

This guide is sufficient for the first five goals, but the nuances necessary to calculate payback periods and create code-compliant models are beyond the scope of this tutorial. 

## What results can I expect? 
Energy modeling uses the first law of Thermodynamics, which states that Energy can never be created or destroyed, to track energy moving in and out of a building. Heat entering the building might include heat from people, heat from computers/appliances, heat from light bulbs, solar heat through windows, and heat from heating systems like radiators. Heat losses might be the result of conduction through the envelope, cool air seeping through walls, and through deliberate ventilation. These are tallied in a balance sheet:

![001_energy_balance](https://user-images.githubusercontent.com/44324576/49155416-2c6fef80-f31b-11e8-88c3-f52a9aa72e7b.JPG)

## What assumptions is this based on?
, the conduction through the walls, solar gains through the windows, occupancy schedules of people, energy consumption from lighting, operation schedules of internal equipment, and the resource consumption of heating, ventilation and air-conditioning (HVAC) equipment. The simulation accounts for your specific geometry and the movement of the sun, but it does not provide levels of lighting inside the space. For daylighting simulations, refer to our guide to Honeybee for Daylighting. 

Section about thermal comfort and flawed measures. 

The specific metrics returned are as follows:


<img src="https://user-images.githubusercontent.com/44324576/49518217-67839d00-f89e-11e8-9b63-e16b5618a9af.png" width="100" height="100" />


QUESTION: Are these assumptions accurate? What are all the metrics we can get out of these simulations? Ask Mostapha for help creating a list of all metrics.

