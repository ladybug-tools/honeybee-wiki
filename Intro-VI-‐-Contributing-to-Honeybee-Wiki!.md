Hello and thanks for your interest in contributing to the HoneyBee Wiki!

This page is intended to serve as a home for sharing Markdown tips, work-arounds, points of hygiene, and other important notes for contributing to this wiki itself. As Alexander Jacobson wrote this guide, he came accross many considerations for streamlining the process of creating tutorials that are worth sharing. This page should take some of the pain out of creating future tutorials for Honeybee.

### Topics to contribute
If you would like to take on a topic of your own, there is a list of important but still incomplete topics in the table of contents, all marked with [WIP] for Work In Progress.

### The Markdown Coding Language
This wiki is written in Markdown, a lightweight markup language that makes it possible to specify formatting. It is easy to learn, and there are free tools like Visual Studio Code from Microsoft which make it easy to edit the raw code and preview the results simultaneously. https://code.visualstudio.com/ 

Here is a cheatsheet on Markdown: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

Note that our use of Markdown makes makes it necessary to distinguish between some characters that specify Markdown formatting and characters we actually intend to display in the guide. For example, an underscore (_) on either side of a word or phrase indicates italics in Markdown. However, the convention in Honeybee is to use the underscore in front to indicate necessary inputs and an underscore behind to indicate optional inputs. This can be overcome using a backslash in between the two underscores, which cancels the command to display italics. 
- For example, in Markdown: '\_RADMaterial\_' must be written '\\\_RADMaterial\\_\', otherwise it will display as '_RADMaterial_'

### Formatting
As for maintaining formatting, use the the Single Zone Model as a style and formatting guide. The most important point to mention here is that all steps should be marked in bold and clearly numbered by section number, followed by a decimal point, followed by step number. For example, **iii.05** would refer to introduction III, step 5. **This will make it easy to refer to the guide on the forums when people need help!**


### When creating example grasshopper files
1. Create clearly labeled groups that correspond to the sections of the guide. This will prevent confusion and makes it easy for readers of the guide to follow-along.
2. Provide at least one overview image of the entire script, with the distinct groups clearly visible.
3. Always use a False-start Boolean Toggle for triggering large operations. We also recommend creating an individual group for each of these toggles, and coloring that group **RED** to distinguish these toggles from boolean toggles which simply specify settings.
4. We recommend using the bi-focals component, available on food for rhino, and setting the display of components to 'icons'. This makes it possible for users to both see the name and the icon for each component, and makes it much easier for them to locate unfamiliar components in the grasshopper menus or by searching.

### Uploading Images
To upload images in markdown, simply create a new issue on the wiki and drag-and-drop an image file into the issue comment section. Try this link: https://github.com/mostaphaRoudsari/honeybee/issues/new

So, the overall process for making images, and uploading them is:
1. Set up the example Grasshopper/Rhino file you'd like to capture. 
2. create a step-by-step series of images by running a high-res image capture from grasshopper, or 'ViewCapturetoFile' in Rhino (note that Rhino 5 users may want to try _ViewCapturetoFile with an underscore in front).
3. export these images to a folder on your computer
4. Edit these files in photoshop
4. Drag the edited images into a 'new issue' topic on Github (see link above) to automatically upload them to Github and create a piece of markdown code and internet link to the image that can be inserted anywhere.
5. Paste this markdown code into your code-editor, like VS Code for example (or directly into the HoneyBee Wiki if you don't care about previewing the result while writing code)
6. Preview the image as it appears among your text formatted in markdown. 
7. Once you're satisfied, then go to edit the HoneyBee Wiki page, and paste the markdown code in.
8. Save the page.

I managed this process by using multiple desktops in Windows 10. At the very far right I had Desktop 5 with rhino/grasshopper, then Desktop 4 with photoshop for editing the output, followed by Desktop 3 with side-by-side windows explorer and honeybee New Issue so I could drag the images to a new issue, followed by Desktop 2 with Visual Studio Code where I could test the markdown snippets generated and preview the output, and finally Desktop 1 with the HoneyBee Wiki page I was editing to upload the result.

### To create step-by-step series of images using Grasshopper and Photoshop
Once you have created a Grasshopper file you would like to use in the tutorial as a step-by-step series of images, go to the grasshopper menu, go to file, and export a high-res image. This will create a hi-res image of the entire canvas. Then, take this file into Photoshop and crop the image as you see fit. Then, you can duplicate the layer, create an entirely black mask and paint with white in the layer masks to 'reveal' the first step of the high-res image. Duplicate that first layer (which shows the first step of your tutorial) and continue painting white in the layer mask to reveal the second step. Duplicate the layer again, and reveal up to the third step, and so-on. When this series of layers is complete, you can export all of them at once by going to the menu under File / Scripts / Export Layers to Files. 

### Capturing Grasshopper Canvas activity
I used windows screen capture to capture grasshopper canvas activity, like information revealed when 'hovering' over a component, or by right-clicking on a terminal, etc. There is an option for setting a delay on the capture, which allows you to capture right-click menus. It is also possible to choose rectangular or full-window captures so that you can easily match the size and scale of images to each other. 

### Editing the table of contents
Tap the icon of a pencil above the table of contents to edit it. Each entry has the text displayed in parenthesis (), followed by the name of the page itself in brackets []. If you simply type a new line, with a new page name in [brackets] GitHub will automatically create a page with that name for you. To create a new page in the table of contents which includes a hyphen, it is necessary to use the unicode character '‐' instead of a standard hyphen. This is necessary because Gollum (the background environment displaying Github's web page) uses dashes in filenames on the filesystem to represent spaces (you should see 'a-b-c-d-e-f.md' on yours), so it assumes that dashes are really spaces. I worked around this using the unicode character ‐ (Hyphen or U+2010) as opposed to the - (Hyphen-Minus or U+002D). The solution is to simply copy paste this character: ‐

### Marking Incomplete Pages
- When working on a page or section which is in a very rough-state, either mark it with [WIP] for work in progress, or simply exclude it from the Table of Contents. It will show up in the 'pages' section above the table of contents, which makes it publicly accessible for other editors to pick up where you left off, but only those who are actively looking for the page will come across it.

- If there is a problem on an existing page, here is a method for creating an exclamation icon. Use this to indicate that there is a problem with this area of the guide, and provide notes about your doubt in **bold**. 
\<img src="https://user-images.githubusercontent.com/44324576/49518217-67839d00-f89e-11e8-9b63-e16b5618a9af.png" width="50" height="50" />
 <img src="https://user-images.githubusercontent.com/44324576/49518217-67839d00-f89e-11e8-9b63-e16b5618a9af.png" width="50" height="50" />

### Crediting Contributors
     _Contributors_:
     <a href="https://github.com/alexandermatthias" title="Alexander Matthias Jacobson"><img 
     src="https://github.com/alexandermatthias.png" height="24"></a>
     # 
Contributors to the wiki can be credited with the above snippet of code (which should of course be edited to link to the contributor's github profile instead of Alexander's). For longer tutorials, the credit can be placed on the home page, for **Topics** the credit can be placed at the top of each page.

### Creating Drawings Directly from Rhino
All the images in this guide have been screen-printed directly from Rhino 6. Here are notes on creating the drawings themselves:
- Use the 'arctic' preview setting 
- Type 'LinetypeDisplay' into Rhino's command line and turn it on. 
- Type 'SetLineTypeScale' into Rhino's command line and enter 250. 
- You should now be able to edit line types and scales under Rhino Layers. 
- Best practice is to create a named view for each file you export, so that if you need to come back an edit the file it is easy to create a duplicate.
- You have the option of specifying object color by object color or by rendering material. Both will allow you to make objects semi-transparent by changing the transparency of the rendering material. This can be achieved by customizing the display mode, under Options / Display Modes 
- To start a drawing for a new step duplicate the layer and objects. This can be done by right-clicking the layer in the layer menu and click 'duplicate layer and objects', and then re-naming the layer with the step number. This way it is easy to go back and edit drawings.  
- I have been exporting images at 1000x600 pixels to keep files small. This can be done using 'viewcapturetofile'
- 'Dot' can be helpful for labeling in Rhino.
- Type 'Options' in Rhino command line, scroll to 'Display Modes' on the bottom, create a new one, and change the following inputs: 1) Change the Background color to white. 2) Under 'Objects' go to 'Curves' and set the diameter to 1 pixel. 