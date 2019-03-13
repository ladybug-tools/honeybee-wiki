The EnergyPlus simulation engine has existing established conventions for creating zone geometry. This section shows how to describe a single-family house using a single zone, and how to describe the same house with a more nuanced multiple zone method. The first section focuses on creating zone geometry, followed by additional notes which are required reading for creating multiple-zone models.

**0.01** Here is the example project we will analyze:
![00_axo](https://user-images.githubusercontent.com/44324576/48569753-de162600-e902-11e8-9be4-cc85de7eee54.jpg)

**0.02** In a simplified energy model, the entire house can be treated as a single zone:
![005_single zone_overlay](https://user-images.githubusercontent.com/44324576/48569892-38af8200-e903-11e8-8f9e-eed633a5f163.jpg)

**0.03** A more nuanced energy model would treat each room as a separate zone:
![006_multi zone_overlay](https://user-images.githubusercontent.com/44324576/48569893-39e0af00-e903-11e8-8f5c-1916fd4197d7.jpg)

**0.04** Neighboring zones must be co-planar.
![006_multi zone_coplanar](https://user-images.githubusercontent.com/44324576/48576313-7bc62100-e914-11e8-9b86-43e400a65c90.jpg)

**0.05** Each zone must be a closed 3D shape.
![010_closed shape thickness](https://user-images.githubusercontent.com/44324576/48571288-c5a80a80-e906-11e8-9341-3ceb166c3f79.jpg)

**0.06** Each surface of the zone is modeled as a flat plane, which will later be labeled with names and assigned properties.
![011_labels](https://user-images.githubusercontent.com/44324576/48571833-27b53f80-e908-11e8-82b0-4592fae18767.jpg)

**0.07** Windows and doors are represented as surfaces. They will be assigned as "belonging" to one of the zone surfaces, and should be co-planar with the associated zone surface. Windows and doors should not share corners or edges with the zone geometry.
![012_boundary](https://user-images.githubusercontent.com/44324576/48570921-c68c6c80-e905-11e8-8a0b-786f44afddfb.jpg)




## Requirements for Multiple-Zone Analysis:
**0.08** Neighboring zones must also have identical surface areas. This creates a problem for three areas of our example. In the image below, examine 1) the wall of zone 5 shared with zone 1 and zone 2, 2) the wall of zone 3 shared with zone 5 and zone 4, 3) the wall of zone 5 shared with zone 6 and zone 7.
![09_parallelintro](https://user-images.githubusercontent.com/44324576/48578327-a23a8b00-e919-11e8-987e-8231ff0f23f9.jpg)

**0.09** It is important that surfaces touching more than one zone are split at each zone junction. Otherwise, there is a mis-match in the surface area calculation for heat leaving zone 1 and zone 2 versus heat arriving in zone 5.
![08_parallel](https://user-images.githubusercontent.com/44324576/48577773-4a4f5480-e918-11e8-9614-fd894bf00c0f.jpg)
_Note_  The Honeybee | 0 Honeybee | Solve Adjacencies component is designed to do adjust zone geometry to do this automatically. More detail on how to use this component in the following section, Assigning Properties to Zones.

**0.10** This can be solved by drawing a 2D polyline around the base of zone 5 which has an extra anchor point at the junction between zones 1 and 2, and then extruding that polyline as a solid.
![09_extra control point_edit](https://user-images.githubusercontent.com/44324576/49099463-cda26b80-f271-11e8-85de-ce351ff72259.jpg)

**0.11** When describing the geometry of building surfaces in EnergyPlus, all surfaces are a thin plane without any thickness. This creates some complication about where the 2D surface should be modeled in relationship to the 3D wall. EnergyPlus's documentation suggests using the outside dimensions for exterior surfaces, and centerline dimensions for interior surfaces. This produces fully connected geometry with an appropriate amount of floor area, zone volume, and thermal mass. See the relationship between the red line representing zones and the black lines representing walls in the diagram below:
 ![006_zone borders](https://user-images.githubusercontent.com/44324576/51616959-7c3df200-1f2b-11e9-932d-867f4afe6587.jpg)
 _Note that the thickness property of the materials which are assigned to the
building surface are only used for heat conduction and thermal mass calculations. For most buildings, the difference is small, and the user may use whatever dimensions are most convenient. If desired, zone volume and floor area may be overridden by entering values in the Zone object. For buildings with very thick walls, such as centuries-old masonry buildings, it is recommended that centerline dimensions be used for all surfaces (exterior and interior) so that the model will have the correct amount of thermal mass._ 

**0.12** When creating geometry by extruding closed curves in Rhino, be absolutely certain that there are not any self-overlapping edges. This will result in errors, like zones with an impossibly large surface areas for their volume. Heat-transfer calculations rely on surface area, so this will create errors in the analysis. 
![014_cleanliness](https://user-images.githubusercontent.com/44324576/48574730-3b64a400-e910-11e8-8a96-03959e2668c3.jpg)


**0.13** Zones can be represented by curved geometry as well. However, the curves are simplified into flat surfaces and each additional zone surface increases the number of calculations EnergyPlus must make in order to describe the overall zone behavior. It is recommended that you simplify curved geometry with faceted geometry of a comparable surface area, as in the following diagram. 
![006_curved geometry](https://user-images.githubusercontent.com/44324576/51614761-a345f500-1f26-11e9-9c02-80a9f96d70d0.jpg)

**0.14** Modelling atriums (like the blue one below) in EnergyPlus is an extremely nuanced exercise. This will be treated as a topic of its own later. 

![013_atrium](https://user-images.githubusercontent.com/44324576/48573942-26871100-e90e-11e8-8b5e-b6bc956db10c.jpg)
One reason it is diffuclt to model stories of multiple height is because the temperature varies greatly from the top of the zone to the bottom, whereas EnergyPlus assumes that each zone is a single uniform temperature (more on this issue in Intro IV - Energy Modeling Assumptions). 

![013_doubleheight_cut](https://user-images.githubusercontent.com/44324576/48573943-27b83e00-e90e-11e8-919c-aa03bb6f75f0.jpg)
The immediate temptation may be to model the atrium as a stack of several zones, but this creates two further problems:

1.  As of January 2019 EnergyPlus cannot account for multi-directional heat exchange in a single time step. In layman's terms, this means that heat moving with air currents is difficult to represent with multiple zones, and this would require a simulation that uses computational fluid dynamics to solve. 
2. That stacking several zones creates has to do with the way that sunlight and radiation are handled, because the walls and floors of the stacked zones will be treated as surfaces that interefere with sunlight and radiation reaching the space.

Suffice to say that modeling ateriums is an advanced topic that requires nuanced care and attention to the exact questions one is trying to answer.



