This brief introduction to Grasshopper will provide you with an understanding of how Grasshopper is different from Rhino, and how to work with lists of data that create geometry. This example uses two lists of points to create a series of lines.

Grasshopper is a visual scripting language, it exists as a plugin for Rhino 5.0 and it is built in to Rhino 6.0. Grasshopper creates geometry in Rhino exactly the same way that Rhino's interface creates geometry, except that Grasshopper uses lists of inputs instead of information entered by hand. For example, to define a line between two points in Rhino, you would type 'line' into Rhino's command line, and then provide two points. 
![202_grasshopper](https://user-images.githubusercontent.com/44324576/49101914-afd80500-f277-11e8-94aa-1774b9f9ae24.jpg)

**ii.00** To create the same line between two points in Grasshopper, you would create two lists of points in Grasshopper, place one point in each list, and then connect these lists with a 'line' component.
![205_grasshopper_interface](https://user-images.githubusercontent.com/44324576/49102500-46f18c80-f279-11e8-826f-ef1b23d084b1.png)

**ii.01** To create this definition from scratch, you will need to install Grasshopper. Then type 'Grasshopper' into the command line of Rhino to start Grasshopper. 
![206_grasshopper_cmd_line](https://user-images.githubusercontent.com/44324576/49103686-53c3af80-f27c-11e8-98b5-6d59251de1be.JPG)

**ii.02** This will activate the Grasshopper interface. The tabs at the top (Params, Maths, Sets, Vector, Curve, etc.), contain components that can be dragged into the beige gridded area below called the 'canvas'. Components are the building blocks for scripts, think of components like narrow-minded workers which can only do one extremely specific task. Grasshopper's tabs organize the available components according to the type of task they perform.
![207_grasshopper_cmd_line](https://user-images.githubusercontent.com/44324576/49116780-f68d2580-f29e-11e8-9e16-06e0622e8fcd.JPG)

**ii.03** Parameter components perform the task of accepting input from the designer, think of them like empty buckets that can be filled with information. To create a point parameter component, go to the Params tab, and look in the Geometry section for a component marked with an 'x' that displays 'Point' when you hover over it. Click and drag a point component onto the canvas. This will be the start of our line.
![208_grasshopper_cmd_line](https://user-images.githubusercontent.com/44324576/49116976-9185ff80-f29f-11e8-8135-317e1668c38f.JPG)

_Note on Appearance: Your components may have icons intead of 'Pt'. To change this go to Grasshopper's Display menu (top, middle) and select Draw Icons. Also, unless you have installed a plugin called Bifocals, the label that reads 'Point' above the point component will not be visible. We use Bifocals throughout this guide so that you can always see the name of the component type. If you would like to install Bifocals, it is available [here](https://www.food4rhino.com/app/bifocals)._


**ii.04** Repeat this step to create a second point parameter, for the end-point of the line.
![209_grasshopper](https://user-images.githubusercontent.com/44324576/49116783-f725bc00-f29e-11e8-90a8-48d6bf10e9e0.JPG)

**ii.05** Rename the first point by right-clicking on the point component in the canvas and typing 'Start Point' (without the quotation marks) in the first entry field. It is best practice to retain the parameter type in the name of the component, as in 'Start Point' or 'End Point', rather than simply 'Start', or 'End'. This is because components only accept specific types of data as input, and it's important to keep these data types seperate. A container for points can not accept curves, or surfaces, or boxes as input.
![210_grasshopper](https://user-images.githubusercontent.com/44324576/49116787-f7be5280-f29e-11e8-9964-2f000631d239.JPG)

**ii.06** The next step is to fill our Start Point 'bucket' with a point. Return to Rhino, draw two points, and then deselect everything by pressing ESC.
![212_grasshopper](https://user-images.githubusercontent.com/44324576/49103695-558d7300-f27c-11e8-8a17-c7c33cbd6baf.JPG)
_Note: Every piece of geometry in Rhino is created with a unique ID, visible in the Rhino properties tab under 'Details...'_

**ii.07** Then, open the Grasshopper canvas and right-click the middle of the Start Point component. Select 'Set One Point'.
![211_grasshopper](https://user-images.githubusercontent.com/44324576/49116788-f856e900-f29e-11e8-8693-37a53400b0e8.JPG)

**ii.08** This will bring up the Rhino interface, where you select one of the points you just drew. Grasshopper points appear as a red 'x' in Rhino by default.
![211a_rhino](https://user-images.githubusercontent.com/44324576/49116789-f856e900-f29e-11e8-847c-d3ff4850338c.JPG)
_Note 1: If a point in Rhino was already selected at the time you clicked 'Set One Point', Rhino may automatically choose that point and instantly return you to the Grasshopper canvas. Either way, the Start Point component should turn from orange to grey, indicating it is properly collecting data._

**ii.09** Next, repeat these steps for the End Point. Re-name the second point component to 'End Point'.
![213_grasshopper](https://user-images.githubusercontent.com/44324576/49116791-f9881600-f29e-11e8-8b84-a2a50190bffc.JPG)

**ii.10** ... and assign the second point from Rhino by right-clicking and pressing Set One Point.
![214_grasshopper](https://user-images.githubusercontent.com/44324576/49116792-fa20ac80-f29e-11e8-9bc8-a833fec793bf.JPG)

**ii.11** This will bring up the Rhino interface again. Select the second point you drew.
![215_rhino](https://user-images.githubusercontent.com/44324576/49116794-fa20ac80-f29e-11e8-8e23-d3aee454652e.JPG)

**ii.12** Connecting the two points will require a new type of component. Navigate to Grasshopper's Curve tab, go to the Primitive section, and drag a line component onto the canvnas.
![216a_grasshopper](https://user-images.githubusercontent.com/44324576/49117443-f8f07f00-f2a0-11e8-84bf-38ad6e431809.JPG)

**ii.13** Grasshopper always computes from left to right. The left side of components are for inputs, the right side is the resulting output. Connect the output of Start Point to the input of the Line Component marked A. This is done with a left-click and drag from the round knob of one component to the round knob of the opposite one. You can make the connection in either direction.
![217_grasshopper](https://user-images.githubusercontent.com/44324576/49116796-fab94300-f29e-11e8-8822-b7793b1fe592.JPG)

**ii.14** Make the second connection between the End Point and the Line component.
![218_grasshopper](https://user-images.githubusercontent.com/44324576/49116797-fab94300-f29e-11e8-91a6-302beaa6a4d6.JPG)

**ii.15** A red line should now appear between the two points in Rhino. This is only a preview, you will not be able to select the line in Rhino. Note also that this line has not been recorded in Rhino and it will disappear when Grasshopper is closed. The reason for this behavior is to keep Grasshopper running fast, if all the geometry generated had to be recorded into Rhino the script would run very slowly._
![219_grasshopper](https://user-images.githubusercontent.com/44324576/49116800-fab94300-f29e-11e8-8a79-568a0be092f5.JPG)

**ii.16** Thus far, we have simply reproduced a line in Rhino as a line in Grasshopper. However, this script for creating a line between two points can be modified to create multiple lines between multiple points. Draw six additional points in Rhino.
![220_grasshopper](https://user-images.githubusercontent.com/44324576/49116801-fb51d980-f29e-11e8-965a-cc3efcbd5cda.JPG)

**ii.17** Return to the Start Point component, right-click and select Set Multiple Points.
![221_grasshopper](https://user-images.githubusercontent.com/44324576/49116803-fbea7000-f29e-11e8-933b-e6dd6c0bee68.JPG)

**ii.18** Select the three points near the initial start point, and the initial start point itself. You may see a blue helper arrow, this shows the sequence of point selection. Observe that there is now a red line between each of these points, and our original end point.
![222_rhino](https://user-images.githubusercontent.com/44324576/49116806-fbea7000-f29e-11e8-9aff-7ad1f2a198fd.JPG)

**ii.19** This is because or initial Start Point 'bucket' now contains four points. We can view this list using the Panel Component, located in Grasshoppers Params tab, in the Input section. Drag a Panel onto the canvas.
![222a_rhino](https://user-images.githubusercontent.com/44324576/49118422-68b43900-f2a4-11e8-8f49-39c94158ae6a.JPG)

**ii.20** Connecting the output of our Start Point 'bucket' to the new Panel component displays the list of points contained in the Start Point component. We can see it contains four referenced points, numbered 0-3. A second panel shows that the End Point component contains just one referenced point.
![223_grasshopper](https://user-images.githubusercontent.com/44324576/49116808-fc830680-f29e-11e8-95b8-8308ef2e8896.JPG)

**ii.21** If we Set Multiple Points to the End Point component, we can see that the sequence in which the points were assigned is important for matching the Start Points to the End Points.
![225_rhino](https://user-images.githubusercontent.com/44324576/49116810-fc830680-f29e-11e8-9905-bfde408e5b32.JPG)

**ii.22** Now there are four points in the Start Point component, and four points in the End Point component.
![224_grasshopper](https://user-images.githubusercontent.com/44324576/49116809-fc830680-f29e-11e8-872f-381fa05c79d6.JPG)

**ii.23** Observe that this results in four lines from the Line component.
![226_grasshopper](https://user-images.githubusercontent.com/44324576/49116811-fd1b9d00-f29e-11e8-9273-7df137475017.JPG)

**ii.24** If we want to transfer these four lines back into Rhino, go to the Grasshopper Canvas, right-click on the Line component, and select Bake. This will record the lines by creating four line objects in the active layer of Rhino.
![227_grasshopper](https://user-images.githubusercontent.com/44324576/49119770-065e3700-f2aa-11e8-9c0f-d1388198ab2b.JPG)

**ii.25** The grasshopper preview can be turned on and off using these controls. The half green icon is particularly useful, because it will preview only comonents you have selected in the Grasshopper canvas. This is a good tool for checking that you referenced the geometry you intended to, and for quickly identifying problems or unexpected behavior.
![228_grasshopper preview jpg](https://user-images.githubusercontent.com/44324576/49161164-92af3f00-f328-11e8-82cd-22c3ce11826e.png)



This concludes the introduction to Grasshopper. You should now be familiar with the following:
1. How to create a simple Grasshopper script
2. How to reference geometry from Rhino in Grasshopper (ii.07)
3. The idea of working with lists (ii.20)
4. Grasshopper computes from left to right (ii.13)
5. How to bake geometry from Grasshopper into Rhino (ii.24)
6. Checking referenced geometry using Grasshopper's preview tools (ii.25)