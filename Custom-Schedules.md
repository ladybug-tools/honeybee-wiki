_Contributors_:
<a href="https://github.com/alexandermatthias" title="Alexander Matthias Jacobson"><img src="https://github.com/alexandermatthias.png" height="24"></a>
# 

Welcome to the **Topics** page on Schedules! 

This page discusses various methods for creating schedules in Honeybee. We will use the first example file below, but there the other two are also helpful. Chris Mackey's example of how to assign schedules (including those which have holidays) is a particularly important complement to the material here.

**Download the example file this tutorial uses for** [Schedules Types on Hydra](http://hydrashare.github.io/hydra/viewer?owner=alexandermatthias&fork=hydra&id=AdvancedEnergyModeling_00_ScheduleTypes&slide=0&scale=2.297396709994071&offset=-786.871104611404,-484.0506037693506)

**Download** [Chris Mackey's example for assigning schedules on Hydra](http://hydrashare.github.io/hydra/viewer?owner=chriswmackey&fork=hydra_2&id=Creating_Custom_Schedules&slide=0&scale=1&offset=0,0)

**Download** [Antonello Di Nuzio's example for Schedule Creation on Hydra](http://hydrashare.github.io/hydra/viewer?owner=AntonelloDN&fork=hydra&id=Honeybee_Schedules_Creation&slide=0&scale=1&offset=11.524914040484845,-22.842574579106923)

## Schedules Overview

Schedules are lists of data that indicate settings which change from time-step to time-step over the course of the simulation. For example, the temperature set point for an heating system, the the number of occupants in a space at a given hour, or the activity level of those occupants. 

There are several types of data entered into schedules for Energy+, here are the most typical:
- **Fractional** schedules are a value between 0 and 1. These are usually multiplied by a maximum load value to calculate the simulated load at a given point in time. 
- **On/Off** indicates whether a piece of equipment is either on or off. 
- **Temperature** is usually used for temperature setpoints on heating or cooling equipment. 
- **Activity Level** represents the total heat gain per person measured in watts / person. This includes convective, radiant, and latent heat gain.

Schedules work hand-in-hand with loads. Loads are usually defined as a maximum value for each zone, and then this maximum is reduced to its expected level at any given hour by multiplying a fractional schedule. For example, if the maximum occupancy of a room is 20 people, but it is only occupied by 4 people at 8AM on a Tuesday, then a fractional schedule would read 0.2 at 8AM on Tuesdays in order to indicate that there are .02 * 20 max occupants = 4 people in the zone at that time. 

Honeybee has an extremely flexible system for defining schedules. 
## Daily Schedules
A **daily schedule** is simply a list of 24 values representing the hours of the day. By itself, it cannot yet be used to run a simulation, but daily schedules are building blocks for weekly and annual schedules which can be used for EnergyPlus simulations. The Honeybee_Daily Schedule component works in tandem with the Galapagos Gene Pool component to quickly create this list of 24 values. Simply connect the Gene Pool component, connect a button, and then press the button. This makes it very easy to customize and read daily schedules. Several useful presets can be entered using panels or number sliders, as in the image below.
![00_type_single day_crop](https://user-images.githubusercontent.com/44324576/52800948-1dc4e900-307d-11e9-8f62-dd9675df1918.png)

It is possible to graphically verify that a daily schedule (which is just a list of 24 values) is correct by plugging it into the Ladybug_3D Chart component:
![00_type_single day](https://user-images.githubusercontent.com/44324576/52793417-f9154500-306d-11e9-8753-d90d09d5be19.png)
It will appear as a single strip of color to the left of the legend.  
![00_single day](https://user-images.githubusercontent.com/44324576/52793420-fa467200-306d-11e9-9aae-820fb19b8c75.jpg)

## Constant Schedules
**Constant schedules** can create a very simple annual schedule that repeats the same day for the entire year. Connect a Gene Pool to the Honeybee_Constant Schedule component to achieve this.
![00_type_constant_24](https://user-images.githubusercontent.com/44324576/52793550-45608500-306e-11e9-8a11-760a4ea73887.png)
Constant Schedules are a different form of data than Daily Schedules. When you create a Constant Schedule, you are actually creating an IDF file that can be passed to an EnergyPlus simuluation. So, whenever you connect a Constant Schedule to another component, you are actually just passing the name of the IDF file containing the schedule (try connecting a panel to the schedule output to confirm this for yourself). This creates an extra step when we want to graph the schedule, because it's first necessary to convert this IDF file into a series of values that can be read by the Ladybug_3D Chart component. This is accomplished using the Honeybee_Convert EnergyPlus Schedule to Values component, as below: 
![visualize a schedule](https://user-images.githubusercontent.com/44324576/52795712-a12d0d00-3072-11e9-83f1-aa2aad2201e1.png) 
Observe that this results in a graph that repeats the same day for the entire year:
![types__0002_02_constant day jpg](https://user-images.githubusercontent.com/44324576/52794073-6d041d00-306f-11e9-8a42-3f0a19c293ef.jpg)

**Constant Schedules** can also be defined with a single value instead of a Gene Pool. In this case we use a panel with 0.1: ![00_type_constant](https://user-images.githubusercontent.com/44324576/52793424-fb779f00-306d-11e9-8ece-bcbd01ab4c69.png)
Which results in a schedule that uses the exact same value of 0.1 for all hours of the year.
![types__0000_01_constant value jpg](https://user-images.githubusercontent.com/44324576/52793426-fca8cc00-306d-11e9-9747-443805b47515.jpg)

## Annual Schedules
 **Annual Schedules** are more nuanced, and make it possible to specify separate lists of 24 values for each day of the week. This representative week is then repeated for all 52 weeks in a year. Further, annual schedules also make it possible to specify distinct daily schedules for holidays. An EPW file makes it especially easy to specify holidays, as it will automatically read national holidays for the location the data was recorded. 
 
 In the script below, you can see there are two Gene Pool components, one for weekends, one for weekdays. Further, you can see we have assigned a single value for all hours of a holiday. This is for demonstration purposes to distinguish between holidays and weekends on the graph below. In reality holidays would probably have a schedule similar to a Saturday or Sunday. You can also see that the EPW component is plugged into the Honeybee_Convert Schedule to Values component:
![02_type_annual](https://user-images.githubusercontent.com/44324576/52795203-9b82f780-3071-11e9-835f-3c57e58b1148.png)
This results in a graph of 52 weeks (orange indicates higher occupancy on weekdays vs weekends), and 8 holidays (which appear as eight vertical blue stripes.)
![types__0001_02_annual jpg](https://user-images.githubusercontent.com/44324576/52795201-99209d80-3071-11e9-8a85-5bb593101158.jpg)

**_IMPORTANT NOTE:_** The Annual Schedules component does not actually contain the dates of holidays! It only contains the daily schedule to run in the case that holidays are assigned! In other words, it can specify that there will not be anyone in the office on a holiday like Christmas, but it doesn't know that Christmas falls on the 25th of December. 

In order to actually run holidays in a simulation, you must assign them using the Honeybee_EnergyPlus Simulation Parameters component. This is done from the Honeybee_Convert EnergyPlus Schedules to Values component, which reads the holidays from and EPW file and converts them to a list of dates in the right format. See the image below: 
![ensure holidays are accounted for](https://user-images.githubusercontent.com/44324576/52798201-bc4e4b80-3077-11e9-8896-2d0c0e5049d4.png)

## Seasonal Schedules
**Seasonal schedules** make it possible to switch between several constant or annual schedules over a given analysis period. The script below shows how it is possible to specify transparency levels of foliage between winter time and summer time. To do this, it uses four constant schedules. One which is a base that is repeated for all periods of year not otherwise specified. One for Jan 1st until the end of Spring when trees have sprouted leaves, a second schedule for the summer through the fall when trees lose their leaves, and a third for the beginning of winter through Dec 31st. Notice that each schedule is paired with a Ladybug_Analysis Period component ![04_type_seasonal](https://user-images.githubusercontent.com/44324576/52793579-53160a80-306e-11e9-84c1-73fc638e2ec2.png)
For demonstration periods, we have made a distinction between the two winter periods, so they appear as blue and yellow below. In reality they would have the same value.
![types__0003_04_seasonal jpg](https://user-images.githubusercontent.com/44324576/52793584-54dfce00-306e-11e9-8075-fd663982711a.jpg)
Note also that the Annual Schedule component has a secondary weekly output for the purpose of making seasonal schedules.
![03_type_weekly](https://user-images.githubusercontent.com/44324576/52793570-501b1a00-306e-11e9-97d7-a242f7ce3cf9.png)
These can also be graphically verified, using the Ladybug_3D Chart component.
![03_single week](https://user-images.githubusercontent.com/44324576/52793574-51e4dd80-306e-11e9-8f7e-1b04dbfd6473.jpg)

## Searching the EnergyPlus library of schedules

There is already a library of 1912 schedules in the EnergyPlus Library. You can search and brows through these using the Honeybee_Call From EP Schedule Library component: 
![search library](https://user-images.githubusercontent.com/44324576/52799714-b312ae00-307a-11e9-8750-b1a6928a9ca9.png)

For example, you could conduct a search for hospital as follows:
![search library_hospital](https://user-images.githubusercontent.com/44324576/52800321-cd00c080-307b-11e9-9135-2e3fc55edcb4.png)

Searching for 'hospital' yields the following list of schedules:


- HOSPITAL CRITICAL CLGSETP
- HOSPITAL CRITICAL CLGSETP DEFAULT SCHEDULE
- HOSPITAL CRITICAL CLGSETP SUMMER DESIGN DAY
- HOSPITAL CRITICAL CLGSETP WINTER DESIGN DAY
- HOSPITAL CRITICAL EQUIP
- HOSPITAL CRITICAL EQUIP DEFAULT SCHEDULE
- HOSPITAL CRITICAL EQUIP RULE 1 DAY SCHEDULE
- HOSPITAL CRITICAL EQUIP RULE 2 DAY SCHEDULE
- HOSPITAL CRITICAL EQUIP SUMMER DESIGN DAY
- HOSPITAL CRITICAL EQUIP WINTER DESIGN DAY
- HOSPITAL CRITICAL HTGSETP
- HOSPITAL CRITICAL HTGSETP DEFAULT SCHEDULE
- HOSPITAL CRITICAL HTGSETP SUMMER DESIGN DAY
- HOSPITAL CRITICAL HTGSETP WINTER DESIGN DAY
- HOSPITAL CRITICAL LIGHT
- HOSPITAL CRITICAL LIGHT DEFAULT SCHEDULE
- HOSPITAL CRITICAL LIGHT RULE 1 DAY SCHEDULE
- HOSPITAL CRITICAL LIGHT RULE 2 DAY SCHEDULE
- HOSPITAL CRITICAL LIGHT SUMMER DESIGN DAY
- HOSPITAL CRITICAL LIGHT WINTER DESIGN DAY
- HOSPITAL CRITICAL OCC
- HOSPITAL CRITICAL OCC DEFAULT SCHEDULE
- HOSPITAL CRITICAL OCC RULE 1 DAY SCHEDULE
- HOSPITAL CRITICAL OCC RULE 2 DAY SCHEDULE
- HOSPITAL CRITICAL OCC SUMMER DESIGN DAY
- HOSPITAL CRITICAL OCC WINTER DESIGN DAY

You can read more about these schedules and the abbreviations on EnergyPlus' website, but here are a few helpful leads:
    
- **EQUIP** - Equipment. A value between 0 and 1 representing the portion of the total equipment running at a given point in time. This amount is specified using the Honeybee_Set EnergyPlus Zone Loads component.
- **CLGSETP** - cooling set point. A temperature. When the zone is above the temperature the cooling system to turn on, when it is below this temperature the cooling system will turn off.
- **HTGSETP** - heating set point. A temperature. When the zone is above this temperature the heating system will turn off, and when the zone is below this temperature, the heating system will turn on.
- **OCC** - occupancy. A value between 0 and 1 representing the the portion of total occupancy at a given point in time. The full occupancy is specified using the Honeybee_Set EnergyPlus Zone Loads component.
- **LIGHT** - lighting. A value between 0 and 1 representing the portion of the total lighting load assigned using the Honeybee_Set EnergyPlus Zone Loads component.
- **INFIL** - infiltration. A value between 0 and 1 representing the portion of infiltration rate specified in the Honeybee_Set EnergyPlus Zone Loads component.
- **ACTIVITY** - activity. A value measured in watts / person the average activity level per occupant. (The overall number of occupants is specified as a multiple of the occupancy schedule, and the number specified in the Honeybee_set Energy Plus Zone Loads component.)  

The table below provides typical values. 

_Note that the right column is measured in watts per person, the central column is watts per meter squared (area), and the right hand column is in met._

![metabolic rates 1](https://user-images.githubusercontent.com/44324576/52800431-05a09a00-307c-11e9-8632-cb7fc944d73d.JPG)
![metabolic rates 2](https://user-images.githubusercontent.com/44324576/52800433-06d1c700-307c-11e9-9e9e-f867255f8a45.JPG)




## Typical Problems on Schedules
- Dont make analysis periods that run 'around' the turn of a year. If you would like to define an analysis period which runs from October until May (as in the example above) you should define three periods. One from Jan 1st-May, one from May - October, and one from October-Dec 31st. 
- Be very careful not to create multiple schedules with duplicate names. Remember, you are not passing the actual schedule to the simulation, you are passing the _name_ of the IDF file containing the schedule. 
- Best practice is to use a name which describes both the object it is applied to and the length of time you expect. For example tree01_jan_apr refers to tree number 1, January through April. This makes it easy to troubleshoot if you get unexpected results.
- If you change the name of a schedule, it will not update until you recompute entire grasshopper canvas.
- To check the values of a schedule, you can also connect a panel to the Honeybee_Convert EnergyPlus Schedule to Values component and scroll through the resulting values. 
- Holidays will not be accounted for in a simulation unless you have both specified a schedule to run on holidays (by default this is the same as Sunday) and added a list of Holidays to the Honeybee_EnergyPlus Simulation Parameters component. 
- EPW files contain a list of national holidays, see notes on Annual Schedules above for parsing this list. 