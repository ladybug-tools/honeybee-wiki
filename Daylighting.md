Daylighting Outline

# Honeybee Versions 
- Distinction between Honeybee Legacy and Honeybee Plus
- This guide is written for version 0.0.64, using Honeybee Plus components.

This is a tutorial for daylighting simulations using Radiance. 

Radiance is a lighting simulation engine originally developed by Greg Ward and verified by an international scientific community.  There are essentially four elements to defining the inputs for a Radiance simulation:
If you categorize the "Radiance Inputs" according to geometry, scene parameters, light sources, rendering parameters and view parameters, that will cover all bases.

1. Geometry 
2. Scene Parameters
3. Light Sources
4. Rendering Parameters
5. View Parameters

Radiance uses reverse ray-tracing. Ray-tracing would mean that the simulation starts with the Sun / Sky calculates every possible ray of light until some of them reach our camera or sensor points. Reverse ray-tracing is much more efficient, because it starts with our camera or sensors and then 'hunts' for the light that can reach them.

 In the spirit of reverse ray-tracing, the guide will begin with defining the geometry and materials. These determine how light bounces around our building, and how much light is absorbed / reflected at each bounce. Then, the guide will cover different sky and sun models which generate light. Then, we will cover the settings that affect the quality of reverse ray-tracing. Finally, we conclude with types of simulations and formats for results. 


### Geometry for Daylighting
This section will show how to assign geometry for Daylighting. First we will import geometry from Rhino into Grasshopper, and then cover how to use that geometry to create Honeybee Surfaces. This step is important because Honeybee Surfaces make it possible to assign material information to the surfaces. This is a necessary for a daylight simulation using Radiance.

**00.00** The first step is to model geometry in Rhino. As you model, keep in mind that the geometry will need to be separated into groups by material. Model the geometry on different layers, label the layers, and it can be helpful to avoid the use of spaces in the layer names.

If you are still early in the design process and still undecided about materials, create a set of layers that distinguishes between:
- Surrounding vegetation
- Surrounding context which is hard surface 
- Floors
- Walls
- Ceilings
- Windows / Glass 

_Note: The reason for this set of distinctions is that vegetation and dark or rough surfaces absorb more light than light smooth surfaces. It is also clearly important to distinguish between opaque and transparent materials. Much more detail follows in the section on Radiance materials._ 

**00.00** For this tutorial, we will be modeling an office space facing a courtyard between two buildings in Copenhagen. This view from Google Maps is captured from south looking directly north. 
![njialsgade 17_view from south](https://user-images.githubusercontent.com/44324576/53183512-c635f880-35fb-11e9-8967-b39668da2b97.png)

**00.00** Here is the Rhino model we will use, the room of interest is marked in red:
![01_geometry](https://user-images.githubusercontent.com/44324576/53188708-45c8c500-3606-11e9-8769-8bbf38923deb.jpg)

**00.00** When modeling your geometry, it's important that you do not have duplicate surfaces, especially if these surfaces have different materials. This will cause errors during ray-tracing and can invalidate your results. 

**00.00** The more complex the geometry is, the longer the calculation time will be. So it is good to simplify the geometry to a minimum number of surfaces. Here is the initial model:
![02_geometry simplify](https://user-images.githubusercontent.com/44324576/53190511-0d2aea80-360a-11e9-8cec-b7752e6c2d44.jpg)

**00.00** Here is a simplified version that eliminates details around windows that will not have any impact upon the room we are interested in:
![03_geometry simplified](https://user-images.githubusercontent.com/44324576/53190621-44010080-360a-11e9-9bfe-a24e7c5585d4.jpg)


**00.00** One word of caution here is that the geometry around the window openings can have quite a big impact on the resuts of your simulation, so be precise in these areas. We include window frames.
![04_zoom](https://user-images.githubusercontent.com/44324576/53191151-60516d00-360b-11e9-88e6-fcbff741e989.jpg)

**00.00** The next step is to separate the geometry by material. If you have decided on materials for you design, then you can separate the geometry accordingly. For this example, we will use generic materials. Our test case is in Denmark, so we will divide our geometry according to the Danish standards for Daylight Factor simulations, which can be found [here](http://bygningsreglementet.dk/Historisk/BR18_Version1/Tekniske-bestemmelser/18/Vejledninger/Generel_vejledning/Dagslys) and are summarized as follows:

| Surface  |Reflectance   | Color | Color Chart RGB |
|:----------|:------------|:----------|:----------|
|Ceiling   | 0.7 | <img src="https://user-images.githubusercontent.com/44324576/53250343-7ec27180-36ba-11e9-9fe2-c3d336795b5d.jpg" width="24">| 216,216,216|
|Window frames       |    0.7|<img src="https://user-images.githubusercontent.com/44324576/53250343-7ec27180-36ba-11e9-9fe2-c3d336795b5d.jpg" width="24">|216,216,216|
|Interior wall| 0.5|<img src="https://user-images.githubusercontent.com/44324576/53250342-7ec27180-36ba-11e9-9c39-41d1b31d5f7c.jpg" width="24">|186,186,186| 
|Floors              |    0.2|<img src="https://user-images.githubusercontent.com/44324576/53250341-7ec27180-36ba-11e9-834c-16b0d4d611e5.jpg" width="24">| 122,122,122|
|Surrounding buildings|   0.2|<img src="https://user-images.githubusercontent.com/44324576/53250341-7ec27180-36ba-11e9-834c-16b0d4d611e5.jpg" width="24">|122,122,122|
|Glass surfaces      |    0.15|<img src="https://user-images.githubusercontent.com/44324576/53250479-c6e19400-36ba-11e9-9a19-ff5916641a94.jpg" width="24">|107,107,107|
|Surrounding vegetation|  0.1|<img src="https://user-images.githubusercontent.com/44324576/53250460-b6c9b480-36ba-11e9-9537-36bc8ec7b948.jpg" width="24">|89,89,89|

_Note: The colors in the chart above come from Axel Jacobs Colour Picker, not the Danish regulations themselves. See **00.00** below for more detail on Radiance Colors_



**00.00** Applying this to the Rhino model yields a new layer structure:

![07_layer structure](https://user-images.githubusercontent.com/44324576/53255918-f1d1e500-36c6-11e9-9c3f-5e449fa64e10.jpg)

**00.00** and the following model:
![05_materials](https://user-images.githubusercontent.com/44324576/53255631-4d4fa300-36c6-11e9-9731-0c25c25fed03.jpg)

**00.00** Note also that the context buildings material has also been applied to the two surrounding buildings:
![06_zoomout](https://user-images.githubusercontent.com/44324576/53255634-4e80d000-36c6-11e9-8bb0-716be525cd49.jpg)

_The colors in the Rhino model are from Axel Jacob's Color picker, see **00.00** below. It can also be helpful ot label the layer structure with the layer name and Radiance Material value if known._

**00.00** Now that we have created the geometry we need in Rhino, it is time to bring it into Grasshopper. The Pipeline component can be useful for picking up geometry from layers in Rhino, because it avoids the need to right clicking and re-assigning geometry to a Geometry component each time you make a change. The Pipeline component is available in Grasshopper's Params tab. 
![08_pipeline](https://user-images.githubusercontent.com/44324576/53257352-30b56a00-36ca-11e9-9875-ccf53bd83bdd.JPG)


**00.00** It is necessary to specify the layer name, and double-click on the BREP filter (green icon below) in order for Pipeline to start picking up geometry:
![09_pipeline](https://user-images.githubusercontent.com/44324576/53256877-33638f80-36c9-11e9-936d-b8009bb52f97.png)
_Note that there is a danger of Pipeline excluding some geometry based upon it's type. There can be a distinction between BREPs (boundary representations) and Extrusions (a curve extruded into a surface)._ 
- _Best practice is to visually confirm that Grasshopper is previewing all the geometry you intend to use._ 
- _Even better, check the number of objects output from Pipeline against the number of objects selected when you 'Select objects in Layer' through Rhino's Layers Panel._ 
- _Another solution to this is to download [Human](https://www.food4rhino.com/app/human) and use their Dynamic Pipeline component, as below_
![10_dynamicpipeline](https://user-images.githubusercontent.com/44324576/53256872-3199cc00-36c9-11e9-813b-e2eab2995a25.png)

**00.00** Although the geometry pipelines can be much faster, we will use a simple geometry component for this example in order to maximize compatibility and minimize the potential for errors.
![geometry component](https://user-images.githubusercontent.com/44324576/53299916-249fe880-3841-11e9-8034-6c51160368e2.png)


**00.00** Now that the geometry is referenced in Grasshopper, we need to convert it into Honeybee Surfaces. There are primarily two differences between Honeybee Surfaces and Rhino Surfaces: 
1. **Honeybee Surfaces contain a lot more information about material and thermal properties.** Honeybee Surfaces can be assigned separate materials for Radiance simulations versus EnergyPlus simulations, each surface can be assigned a name, and several other properties within energy modeling.
2. **Honeybee Surfaces cannot be curved.** The Honeybee_CreateHBSrfs component automatically converts curved geometry into flat planes. This can result in a very large number of surfaces, which will create long simulation times. See the tutorial for Single Zone Model step **0.13** for more detail. 
 
The conversion is accomplished by dragging a Honeybee_Create Honeybee Surfaces component onto the canvas, and connecting your geometry to the \_geometry input terminal.

![12_honeybeesrf](https://user-images.githubusercontent.com/44324576/53258576-411b1400-36cd-11e9-9f7e-157bce61ae12.png)

**00.00** Duplicate this step for each type of material you intend to use.

![11_honeybeesrf](https://user-images.githubusercontent.com/44324576/53258580-424c4100-36cd-11e9-85bc-200393d700e6.png)

You have now created a set of Honeybee Surfaces! Proceed to the next step to learn how to create Radiance Materials, and assign them to these surfaces!

# Scene Parameters



## Reading a Radiance Material Definition

Radiance Materials are defined by a simple text file in a very specific format. This format looks like this:

    #
    # ceiling_standard
    #
    void plastic ceiling_standard

    0 
    0 
    5 0.700 0.700 0.700 0.000 0.000



Here are some notes on how to interpret this format:


    #
    # ceiling_standard
    #

These first three lines are optional, we include them here only because you may find them in some libraries of Radiance Materials. These lines are always preceded by a pound sign (#) and they just label the name of the material for someone reading the file.

    void plastic ceiling_standard

This line contains information about the material type and name. 

**void** - 'void' is simply a place-holder for a modifier. If you see 'void' it means that a modifier could be placed here, but is not currently applied. Modifiers might be patterns or image-based textures that affect the brightness of a material. Modifiers is an advanced topic, we don't cover it further in this tutorial.

**material type** - 'void' is followed by a space, and then the type of the material. In this case the type is 'plastic' which just means opaque (it is not literally plastic).  There are twelve basic types of Radiance material, but the most commonly used five types are:'plastic', 'metal', 'trans', 'glass', and 'BSDF'. More detail on these follows later.

**material name** - The material type is followed by another space, and then the name of the material. In this case the name is 'ceiling_standard'.

_Note: It's important not to include spaces in the names. This is because Radiance uses a space to separate between types of data. If we had named our material 'ceiling standard', with a space ( ) instead of an underscore ( \_ ), Radiance would think that the name of our material ended after 'ceiling' and it would understand there to be a fourth data entry-field: as in (1) 'void' (2) plastic (3) ceiling (4) standard. This is why spaces in material names will cause errors!_

    0 
    
**Optional Material Property** - This zero indicates a specialized material property, zero means there is no data here.

    0
**Optional Material Property** - This second line with a zero _also_ indicates a second specialized material property, and zero again means there is no data here.

    5 0.100 0.200 0.300 0.40 0.500
**Material Property Definitions** - The '5' indicates a material property, and it should be followed by five values each separated by a space. These five values are Red value (0.100), Green value (0.200), Blue value (0.300), Specularity (0.40), and Roughness (0.500).

> 
>

**Line Break** - This last line must also be followed by a line-break. In Grasshopper, you would insert this by pressing 'enter' in the panel. This is important for Radiance to parse through files with multiple materials, especially on macs.

_Note that the last two values (Specularity and Roughness) are switched when compared to the values on a Honeybee_Radiance Opaque Material component! This is important to know when you start writing your own materials, otherwise you will be switching the values you assign for roughness and specularity._

![14_radiance opaque material](https://user-images.githubusercontent.com/44324576/53300197-2a4afd80-3844-11e9-84f2-d62c766040db.png)


## Material Types
**00.00** Here are the descriptions of the different material types from the [Radiance Users Manual](http://radsite.lbl.gov/radiance/refer/usman2.pdf), with a few links to material libraries:

- **Honeybeee_Radiance Opaque Material** is appropriate for all opaque materials which are not metallic. Plastic is a material with uncolored highlights. It is defined by a red green and blue reflectance value, a specularity value and by a roughness value. A positive roughness value will display highlights (uncolored by the materials modifier) but not show any reflections from other objects.

    List of common Radiance Materials: https://github.com/tbleicher/su2rad/blob/master/su2rad/su2radlib/ray/materials.rad

    List of Radiance materials: www.lighting-materials.com

   

-  **Honeybee_Radiance Metal Material** The metal material is similar to plastic except that its highlights are modified by the material color.

 The following chart provides an overview of how Reflectance, Specularity and Roughness affect light bouncing off of opaque and metal objects. As you can see, specularity of metals is typically between 0.9 and 1.0, specularity for opaque objects is usually between 0.0 and 0.1, and roughness is usually between 0 and 0.2.

![material properties](https://user-images.githubusercontent.com/44324576/53883280-d5b03b00-4018-11e9-82b2-fc8bdc35baac.jpg)




-  **Honeybee_Radiance Glass Material** 
The glass type in Radiance only produces one reflected ray and one transmitted ray through a single thin surface. In this way internal reflections are avoided. The glass type has a standard refractive index of 1.52 and all
that is needed to be defined is the transmission at normal incidence.

_Note that there is a distinction between **transmittance** and **transmissivity**. Transmittance is the measured ratio of light at normal incidence, whereas transmissivity is the ratio of the total light that passes through the glass. The Radiance glazing parameters require transmissivity, but glazing manufacturers often quote transmittance.

To compute transmissivity (tn) from transmittance (Tn) use: tn=(sqrt(0.8402528435+.0072522239xTnxTn)-.9166530661/.0036261119/Tn

 [International Glazing Database from Lawrence Berkeley National Laboratories:](https://windows.lbl.gov/software/igdb)

-  **Honeybee_Radiance Trans Material** 
The trans material is basically a translucent plastic. It takes the same parameters as plastic as well as transmission factor and a transmitted specularity value. The transmission factor is the fraction of penetrating light that travels through the material. The fraction of transmitted light that is not 15 diffusely scattered is the specular transmitted value. This material is infinitely thin and will modify the color of the scattered light.

    Complex Glazing Database of translucent materials from Lawrence Berkeley National Laboratories: https://windows.lbl.gov/software/CGDB/

- **Honeybee_Radiance BSDF Material** 
 for Bidirectional Scattering Distribution Function that offer the possibility of estimating the light-scattering effect of complex geometries. This would be appropriate for simulating louvers or complex shading systems. Radiance treats BSDFs like specific plastic materials that get accurate specular distributions from either procedurally defined functions or from data files. This is also considered an advanced topic and it is beyond the scope of this tutorial.

https://en.wikipedia.org/wiki/Bidirectional_scattering_distribution_function

-  **Mirror** 
Note that it is also possible to have a Radiance material of type 'mirror', but Honeybee does not have a component to specify such materials, so these must be specified using another method. This is considered an advanced topic, but the introductory description from Radiance's User Manual follows:

    "The mirror material is used to produce secondary source reflections. It can only be used on planar surfaces ( eg rings and polygons ) and is defined by red, green and blue reflectance values. An optional string argument may be included in the primitive to specify a different material to be used for shading non-source rays."


## Radiance Material Names 

**00.00** There are several important things to remember when naming materials: 

1. Only use ASCI II characters (See right-hand column of the chart from wikipedia below). These are the only characters Radiance can accept. There is a chart of ASCI II characters below.
2. Don't use spaces in the name of Radiance materials. Radiance uses the space character to seprate data types, so this will cause errors.
3. Include a description of the material you're using. Rather than simply 'wall' use 'internal_wall', so that later down the line you will be able to see if you accidentally assigned a material intended for internal walls to the exterior.
4. It is a good idea to include the values you are using in the name of your material. For example, if a material is only named 'interior_wall', it's not easy to see what values are assigned, whereas 'internal_wall_0.7' clearly indicates which values are associated with that name.
5. Capitalization matters, don't capitalize the first letter of a material name. 

Here is a chart of ASCI II characters from Wikipedia. use the right hand column only:

 ![asciii_cropped](https://user-images.githubusercontent.com/44324576/52949946-0a1bca00-337e-11e9-8394-b9e2f23031a4.png)



# Defining Radiance Materials - 4 Methods

There are four ways to define a Radiance material in Honeybee, all of which use the Honeybee_createHBSrfs component. Method 3 is the most error-proof and is recommended for beginners. However, we recommend reading about all four methods because they build on one another:
1. Provide the name of a Radiance Material that is in the Radiance Material Library
2. Write the Radiance Material definition (as in the code from step **00.00** above) into a Grasshopper panel
3. Use one of Honeybee's components to define the material value-by-value (These components include: Honeybee_Radiance Glass Material, Honeybeee_Radiance Opaque Material, Honeybee_Radiance Metal Material, Honeybee_Radiance BSDF Material, Honeybee_Radiance Trans Material, etc.)
4. Specify the surface type and apply a default value for that type.

_Note: Don't confuse the\_RADMaterial\_ with the \_EPConstruction\_ input. Both inputs are used for defining materials, but \_RAD materials\_ is for daylighting simulations whereas the \_EPConstruction\_ input is used for energy simulations. See either step **1.01** of [Single Zone Model - Assign Properties to Zones](https://github.com/mostaphaRoudsari/honeybee/wiki/Assign-Properties-to-Zones) or step **1.04** of [Comparing Passive Strategies - High Performance Window](https://github.com/mostaphaRoudsari/honeybee/wiki/Materials-%E2%80%90-High-Performance-Window) for more on EnergyPlus Materials._


# Method 1 - Radiance Material Library 



**00.00** The basic idea of this method is to store a list of materials in a text file that will serve as a Radiance Material Library. Then, we use the name of the material from the library to assign materials to particular surfaces. The default Radiance Material Library can be accessed using the Honeybee_Call from Radiance Library component.


![radmedthod1__0002_01](https://user-images.githubusercontent.com/44324576/53342535-76fb0b00-390e-11e9-8c81-1c7b4c8d4563.jpg)



**00.00** Observe that the output of this component contains nine materials, labeled by type. If you import a larger library, or create a longer list, you can also enter keywords to search for materials. Try 'exterior' or 'interior' as search terms to test this. 

![radmedthod1__0001_02](https://user-images.githubusercontent.com/44324576/53342538-7793a180-390e-11e9-9e0a-aea738aacb80.jpg)

**00.00** Now, just enter the name of one of the materials in the library, and connect it to the \_RADMaterial input terminal on the Honeybee Surfaces you'd like to apply the material to. 

![radmedthod1__0000_02](https://user-images.githubusercontent.com/44324576/53342542-7b272880-390e-11e9-90c3-b72c9fb74cab.jpg)

**00.00** The way that Honeybee accesses the Radiance Material Library is different from the way that most Grasshopper components access data. Usually, you have to connect a wire between two components in order to transfer data from one to another. This is not the case here. The call from library component is reading a list of names from a file. The library is made available because the Honeybee_Honeybee component is running in the background. 

_Note The following explanation overlaps with **iii.00** and **iii.22** in [Intro III - Honeybee Interface](Intro-III-‐-Honeybee-Interface)._

Grasshopper components usually run in the sequence that they are placed and connected to each other on the canvas. So ordinarily components would run in the following sequence:
![intro iii_sequence of calculations_normal](https://user-images.githubusercontent.com/44324576/53178720-b6fe7d00-35f2-11e9-8179-ebfa9c356bcf.png)

However, the Ladybug_Ladybug and Honeybee_Honeybee components _always_ run first. This is good, because it means that data, functions, and libraries contained in those two components are made accessible to all the others that run afterwards. This is true _even if a wire is not connected_. So, the true order of calculation is below:
![intro iii_sequence of calculations_hb and lb](https://user-images.githubusercontent.com/44324576/53178724-b82faa00-35f2-11e9-8761-0f7477b18c63.png)

**00.00** This method of accessing data makes it possible for you to create your own Radiance Material Libraries. This is done using the Honeybee_Add to Radiance Library component.
![radaddtolib__0000_01](https://user-images.githubusercontent.com/44324576/53343241-2dabbb00-3910-11e9-9c17-f7ec7a5b38f5.jpg)


**00.00** We now connect a panel, that we have typed a Radiance Material definition into. The Honeybee_Add to Radiance Library component adds this material to a central text file containing a list of Radiance materials.
![radaddtolib__0001_02](https://user-images.githubusercontent.com/44324576/53343242-2e445180-3910-11e9-9998-70e63a20e2be.jpg)


**00.00** The process of actually writing the file is controlled by a boolean toggle. Change it from False to True, to add the material definition to the library.
![radaddtolib__0002_03](https://user-images.githubusercontent.com/44324576/53343243-2e445180-3910-11e9-9ee2-1de773053125.jpg)

_Note The values stored in this file will not be updated if you do not change the boolean toggle to False, and then to True again. Alternatively, you can middle-mouse click and choose Recompute Canvas when the boolean toggle is in the True position._ 


**00.00** You have the option of writing at text file that is used only for this document, or for all documents you open in Honeybee. By connecting a boolean toggle with True to the addToHoneybeeLib\_ input terminal, you specify that this material should be added to the general Honeybee Materials Library:

![16_radmaterial_addtogloballib](https://user-images.githubusercontent.com/44324576/53346731-e7f2f080-3917-11e9-89d7-5cdd246043a0.png)


This means that instead of editing a variable saved only in this Grasshopper Document, we are editing a text file which is a file saved here by default: C:\ladybug\HoneybeeRadMaterials.mat.

![16_library location](https://user-images.githubusercontent.com/44324576/53343901-b545f980-3911-11e9-8846-6ecf64a0a365.JPG)

**00.00** Now we have a problem. There is a mistake in our material name! We wrote Interiore instead of Interior, but we didn't notice until after we'd added it to the global Honeybee Radiance Material Library. This means that every time we open a Grasshopper document, this mistake will appear. Fortunatley, we can just open this library, edit it's contents, and then save it again using Notepad. 

![library edit](https://user-images.githubusercontent.com/44324576/53347008-82533400-3918-11e9-89fb-e78807a67162.JPG)

Changes to:

![library edit_02](https://user-images.githubusercontent.com/44324576/53347226-ee359c80-3918-11e9-95c3-67ba34e8fbfd.JPG)

...and don't forget to save your changes.

![library edit_03](https://user-images.githubusercontent.com/44324576/53347218-eb3aac00-3918-11e9-911e-d1de39b9c148.JPG)


**00.00** Whether you choose to save to the document library or the general library, it is important that all of your materials have unique names. Otherwise, Honeybee and Radiance will not be able to distinguish among the materials you specify. If you examine the inputs on the HoneybeeAdd To Radiance Library component, you'll see that there is an option for over-writing materials of the same name. Use a boolean toggle to indicate your choice.


# Method 2. Text-based Radiance Materials


**00.00** As discussed above in step **00.00**, Radiance materials are simply a short text file. So, one method of defining a material is to simply type up a Radiance material definition using a Grasshopper panel component. This panel can then be connected to the \_RADMaterial_ input of a Honeybee_createHBSrfs component. The format for the Radiance Material definition is described above, this can be typed into a panel in Grasshopper:

![17_radmaterialmethod2](https://user-images.githubusercontent.com/44324576/53348694-d4e21f80-391b-11e9-8859-dd91d0baec15.png)


_IMPORTANT: If you try this method, here are several common mistakes to avoid:_
1. _The sequence of the material properties in the line starting with 5 is Red, Green, Blue, Specularity, Roughness. In the Honeybee component these properties appear in a different order, so be sure that you are not switching the last tow by entering data as: Red, Green, Blue, Roughness, Specularity._
2. _Be sure to press 'enter' at the end of the the last line to insert a line-break, as explained above in step **00.00**). See Image below:_

![method 2 panel edit](https://user-images.githubusercontent.com/44324576/53348955-59cd3900-391c-11e9-929b-0078d7dc4916.JPG)

3. _Be sure that the panel is a string and not Multiline Data. Multi-line text produces an index of line numbers that causes errors when reading Radiance materials. You can make this change by right-clicking on the panel and un-selecting Multline data. See image below:_

![multi-line data problem](https://user-images.githubusercontent.com/44324576/53348314-18885980-391b-11e9-8762-0e0623b4b503.JPG)



# Method 3. - Honeybee Radiance Materials Components

**00.00** Honeybee also has several components for defining Radiance materials, which can be found in Honebee's 01 | Daylight Materials tab. Using these components is good for beginners because it will avoid problems in formatting the text correctly. Below is a collection of all the components Honeybee has for creating Radiance materials. The Glass and Opaque materials at left are the most common:

![radmaterialmethod3_components](https://user-images.githubusercontent.com/44324576/53350577-a6feda00-391f-11e9-842d-2d0ed1b3294b.png)

**00.00** Use a panel to fill in the properties you would like to specify, as in the example below.

![radmaterialmethod3_component_example](https://user-images.githubusercontent.com/44324576/53352224-b03d7600-3922-11e9-9a70-fc71e526e5b6.png)
_Note: We are using the concatenate component for creating a material name which includes the RGB values. Doing so makes the script more transparent for others to read, and easier to error-check if you get unexpected results. Concatenate just means to combine pieces of text, called'strings', together into a single string. Below, you can see we have concatenated 'interior_ceiling\_' and the value, '0.5', to create a single string 'interior_ceiling_0.5'. You can also plug the output from concatenate directly into the \_materialName input, without using a panel_

**00.00** In the Honeybee | 01 | Daylight Materials tab, you will also see a series of components called **Honeybee_Radiance "..." By Color**. These offer the option of using an input color instead of specifying three individual RGB values. See the following example:

**PROBLEM** - I am expecting to see 0.5 for the Radiance reflectance value with a color of 144,144,144 from Axel Jacobs' color picker, but I get 5.65
![color problem](https://user-images.githubusercontent.com/44324576/53355182-c51d0800-3928-11e9-8018-4021cfb15ca9.png)

**00.00** Be aware that Radiance reflectance values are on a scale of 0-1, where zero is black and 1 is white. RGB values, by contrast, are on a scale of 0-255, where 0 is black and 255 is white. 

It might seem that you could simply multiply 255 by .7 to get a representative RGB value, but the relationship **is not linear**. This has to do with the way that our eyes perceive color, and subsequently the way that colors are mapped for computer displays. 

Here is a graph with Radiance reflectance values on the horizontal axis, and RGB values on the vertical axis:

![grey scale graph](https://user-images.githubusercontent.com/44324576/53254318-6c990100-36c3-11e9-8a2f-f5adaab5a751.jpg)


| Surface  |Reflectance   | Color | Color Chart RGB |
|:----------|:------------|:----------|:----------|
|Ceiling   | 0.7 | <img src="https://user-images.githubusercontent.com/44324576/53250343-7ec27180-36ba-11e9-9fe2-c3d336795b5d.jpg" width="24">| 216,216,216|
|Window frames       |    0.7|<img src="https://user-images.githubusercontent.com/44324576/53250343-7ec27180-36ba-11e9-9fe2-c3d336795b5d.jpg" width="24">|216,216,216|
|Interior wall| 0.5|<img src="https://user-images.githubusercontent.com/44324576/53250342-7ec27180-36ba-11e9-9c39-41d1b31d5f7c.jpg" width="24">|186,186,186| 
|Floors              |    0.2|<img src="https://user-images.githubusercontent.com/44324576/53250341-7ec27180-36ba-11e9-834c-16b0d4d611e5.jpg" width="24">| 144,144,144|
|Surrounding buildings|   0.2|<img src="https://user-images.githubusercontent.com/44324576/53250341-7ec27180-36ba-11e9-834c-16b0d4d611e5.jpg" width="24">|144,144,144|
|Glass surfaces      |    0.15|<img src="https://user-images.githubusercontent.com/44324576/53250479-c6e19400-36ba-11e9-9a19-ff5916641a94.jpg" width="24">|107,107,107|
|Surrounding vegetation|  0.1|<img src="https://user-images.githubusercontent.com/44324576/53250460-b6c9b480-36ba-11e9-9537-36bc8ec7b948.jpg" width="24">|89,89,89|

_To demonstrate this point, we compare the two grey values. At left is a 0.7 Radiance material, which has an RGB value of (216,216,216). At right is the grey produced by simply multiplying 255 by 0.7 ( 255 * 0.7 =  178 ) with an RGB value of (178,178,178):_

![colourpicker__0004_0 7preview png](https://user-images.githubusercontent.com/44324576/53251285-97338b80-36bc-11e9-9c18-2c982e2eed9a.jpg)
![178grey](https://user-images.githubusercontent.com/44324576/53251273-93076e00-36bc-11e9-9841-c9d13c30cb2a.png)

**00.00** Fortunately, Axel Jacobs has created a [Colour Picker for Radiance Materials](http://www.jaloxa.eu/resources/radiance/colour_picker.shtml) that can be helpful for selecting Radiance colors.

![colour picker_screenshot](https://user-images.githubusercontent.com/44324576/52973054-1e32ec00-33bd-11e9-81a6-549f48b453b1.png)

**00.00** Singapore University for Technology and Design also has a tool for selecting Radiance Materials:
http://spectraldb.com/

# Method 4. Specifying Radiance Material by Surface Type

**00.00** This final method allows you to assing Radiance materials based upon the Honeybee Surface type. This can be achieved by creating a panel, filling it with the number associated with each type above, and connecting it to the srfType_ input of the Honeybee_createHBSrfs component. See below:

![method 4_group](https://user-images.githubusercontent.com/44324576/53356274-55f4e300-392b-11e9-9e50-2657d7528bf4.png)

Hover the mouse over the input terminal to check the available types. They are as follows: 
- 0- 'WALL'
- 0.5- 'UndergroundWall'
- 1- 'ROOF'
- 1.5- 'UndergroundCeiling'
- 2- 'FLOOR'
- 2.25- 'UndergroundSlab'
- 2.5- 'SlabOnGrade'
- 2.75- 'ExposedFloor'
- 3- 'CEILING'
- 4- 'AIRWALL'
- 5- 'WINDOW'
- 6- 'SHADING'

**00.00** You can set the material by type using the Honeybee_Set Radiance Materials component. Here is an example for setting the window material as a custom glass material:
![method 4](https://user-images.githubusercontent.com/44324576/53356171-175f2880-392b-11e9-92d2-61c58a9eca47.png)


This concludes the section on creating Radiance Materials! Next up we will cover different models for the sky. 

# Rendering Parameters 

## Direct Parameters
-dc
-dt
-dj

## Ambient Parameters
-ab
-ad
-ar
-as etc) , 

## Specular Parameters
-st
-ss
## Rays Parameters
-lw
-lr
## View Parameters
-vp
-vd
-vt in rpict

Sarith: Out of these, the majority of the users won't (or rather do not) set params for direct, specular and ray since for most architectural purposes we assume diffusing surfaces and the direct light source in the scene is usually just the sun. There are several view params (like -vp , -vd etc), but the only one worth talking about within the context of Honeybee are the view type (-vt in rpict) as the rest are automatically set for the user through the Rhino viewport.

# Daylight Simulation Recipes 

There are a bunch of different metrics one can use for Daylight simulation: 

- Illuminance [Example on Hydra](http://hydrashare.github.io/hydra/viewer?owner=mostaphaRoudsari&fork=hydra_1&id=Honeybee_Grid-based_Daylight_Simulation_Example_I&slide=0&scale=1.741101126592249&offset=-750.5417638130868,19.547200651655217)
- Daylight Factor 
- Annual Dyalight Metrics [Example on Hydra](http://hydrashare.github.io/hydra/viewer?owner=mostaphaRoudsari&fork=hydra_1&id=Honeybee_Annual_Daylight_Simulation_Example&slide=0&scale=1&offset=0,0)
    - Daylight Autonomy (DA)
    - Continuous Daylight Autonomy (cDA)
    - Spatial Daylight Autonomy (sDA)
    - Useful Daylight Illuminance (UDI)
    - Annual Sun Exposure (ASE) [Example on Hydra](http://hydrashare.github.io/hydra/viewer?owner=chriswmackey&fork=hydra_2&id=Estimate_Glare_Potential_Over_a_Year&slide=0&scale=1&offset=0,0)
- Image-basd Glare Analysis
- Daylight Glare Probability (DGP)

| Honeybee Recipe or Ladybug Component  |Daylight Metric   | Example File | Rating System |
|:------------------|:------------|:----------|:----------|
|Honeybee_Annual Daylight Simulation | Daylight Autonomy (DA)
| | Continuous Daylight Autonomy (cDA)
| | Spatial Daylight Autonomy (sDA) | | LEED
| | Useful Daylight Illuminance (UDI)
|Honeybee_Daylight Factor Simulation | Daylight Factor (DF) || BREAM, DGNB
|Honeybee_Grid Based Simulation | Point-in-Time Illuminance ||LEED|
|Honeybee_Image Based Simulation  | Image-based Glare Analysis
|| Daylight Glare Probability (DGP)
|| Daylight Glare Index (DGI)
|| Visual Comfort Probability (VCP) 
|| Unified Glare Index (UGI) / Unified Glare Rating (UGR)
|| CIE Glare Index (CGI)
|Honeybee_Vertical Sky Component |
|Ladybug_Radiation Analysis| Direct Solar Radiation| 
|Ladybug_Sunlight Hours Analysis|Hours of Sunlight| |DGNB
||Annual Sunlight Exposure (ASE)||LEED
||Uniformity Ratio ||BREAM
||Average Daylit Illuminance ||BREAM


There are several other Ladybug components which can analyse solar geometry, render sky domes, and analyse shading:

| Ladybug Component  |Output   | 
|:------------------|:------------|
|Ladybug_Sun Path|Solar Geometry
|Ladybug_Solar Fan| Unobstructed Solar Fan 
|Ladybug_Solar Fan Basic| Unobstructed Solar Fan
|Ladybug_Solar Envelope| Solar Obstruction Envelope
|Ladybug_Solar Envelope Basic| Solar Obstruction Envelope
|Ladybug_Sky Dome| Tregenza or Reinhart Sky Dome|
|Ladybug_Radiation Calla Dome| Sky Dome For Evaluating Radiation
|Ladybug_Design Day Sky Model| Sky Dome for HVAC sizing
|Ladybug_Shading Mask| Sky Dome obstructed by context
|Ladybug_Sunrise Sunset| Sunrise and Sunset Times
|Ladybug_Radiation Rose| Direction of Solar Radiation


[Daylight Simulation Technical Literature](https://github.com/ladybug-tools/honeybee/wiki/Daylight-Simulation-Technical-Literature)

[Differences between Honeybee Legacy and Honeybee Plus](https://github.com/ladybug-tools/honeybee/wiki/Daylight-simulation-with-Honeybee%5B-%5D-vs-Honeybee-Legacy)

[Review Article on Daylight Metrics](https://www.maxpierson.me/2012/05/19/an-overview-of-daylighting-metrics-with-examples/)

- Radiance Material Library
- Opaque Materials
- Transparent / Translucent Materials
- Sky
    - 
- Radiance Inputs
     - AD - Ambient Divisions
     - AB - Ambient Bounces
     - BSDF - 
     - OCTREE
     - 
 - Types of Simulation 
    - Daylight Factor
    - Illumination Level 
    - % of time 
    - UDI Useful Daylight Illumination
    - Glare


# Sky Models 
Modeling diffuse light coming from the sky is more nuanced than modeling direct light from the sun. The sun is like a spotlight, with a single point as its source that creates very crisp shadows. The sky is like a blanket of light, which is diffuse and spread out, with some areas generating more light than others. To handle this complexity, Radiance has Sky Models.

**00.00** Think of a Sky Model like a semi-spherical dome around the geometry used for daylight simulation. When the project is in the northern hemisphere, the dome will be brightest on the southern side, where the sun is. See the image below:


![sky dome concept](https://user-images.githubusercontent.com/44324576/53658252-8a80db80-3c58-11e9-9751-17a1f4ea9558.png)



![total radiation](https://user-images.githubusercontent.com/44324576/53657510-a5525080-3c56-11e9-9204-91b3e1768c09.jpg)
![diffuse radiation](https://user-images.githubusercontent.com/44324576/53657508-a5525080-3c56-11e9-92e6-e2f2eb2512a3.jpg)
![direct radiation](https://user-images.githubusercontent.com/44324576/53657509-a5525080-3c56-11e9-9b78-f1b4d0ddfb40.jpg)


- Honeybee_Generate Climate Based Sky
- Honeybee_Generate Cumulative Sky
- Honeybee_Generate Standard CIE Sky
- Honeybee_Generate Average Sky
- Honeybee_Generate Custom Sky
- Honeybee_Generate Dark Sky
- Honeybee_Generate Sky with Certain Illuminance Level



### Climate Base Sky

![climate based sky](https://user-images.githubusercontent.com/44324576/53646390-5ea32d00-3c3b-11e9-8665-84d78e902f4b.png)

![cie sky](https://user-images.githubusercontent.com/44324576/53648169-872d2600-3c3f-11e9-9ff6-7f3acc742a0a.png)

![cumulative sky](https://user-images.githubusercontent.com/44324576/53649336-33700c00-3c42-11e9-83ea-7fff02436060.png)
![average sky](https://user-images.githubusercontent.com/44324576/53649353-37039300-3c42-11e9-9b43-d18876126e3d.png)
![illuminance_100](https://user-images.githubusercontent.com/44324576/53649847-6cf54700-3c43-11e9-9fba-82c4dbe1f633.png)
![night time](https://user-images.githubusercontent.com/44324576/53649851-6e267400-3c43-11e9-8fb4-a68bf8a861f0.png)


![average-climate-annual-animation](https://user-images.githubusercontent.com/44324576/53654565-4e487d80-3c4e-11e9-8e62-5db49ef68247.gif)


![average-climate-animated-day](https://user-images.githubusercontent.com/44324576/53655780-7dacb980-3c51-11e9-8cb9-1db051d1dc26.gif)


![calla dome](https://user-images.githubusercontent.com/44324576/53659134-08de7d00-3c5b-11e9-880d-f0245f0f8f9d.jpg)

![tergenza vs reinhart](https://user-images.githubusercontent.com/44324576/53659442-dda85d80-3c5b-11e9-9563-e74ecaf0e639.jpg)

![ladybug perez color sky_june20_12](https://user-images.githubusercontent.com/44324576/53660502-501a3d00-3c5e-11e9-966e-05fe4c543259.jpg)


- Ladybug_Radiation Calla Dome
- Ladybug_Generate Cumulative Sky Matrix
- Ladybug_Colored Sky Visualizer (Perez Sky)
- Ladybug_Design Day Sky Model

Ladybug Solar Fan: https://www.cca.qc.ca/en/events/63353/the-natural-forces-laboratory-ralph-knowles-and-the-instrumentalized-studio
