## Guide Conventions
To help you navigate this guide, there are just a few points of organization to be aware of:

- _Numbering_ In order to make it possible to refer to specific sections in the guide the entries are numbered. Each entry is first numbered by section, followed by a decimal point, followed by the step number. For example, 0.05 would be read section zero, step five. Introductory sections will be numbered with roman numerals, so iv.02 would be the second step of the fourth section.
- _Example Files_ The numbering system above runs parallel to numbering in the example files. Individual steps are not labeled in the example files, but section numbers are mentioned.
- _Distinguishing Example Files_ To avoid confusion note that example files are distinguished from each other using a 3-letter code that abbreviates the topic of the example. HSZ stands for Honeybee Single Zone, HMZ stands for Honeybee Multiple Zone, etc.   
- _Simulation Start Triggers_ Boolean Toggles which execute a large action are placed in a group and colored red. Beware of changing it from false to true because this will trigger the start of a simulation that may take a long time. More on boolean toggles below.

## Hygiene
The flexibility that grasshopper affords is absolutely beautiful, but it can also become a nightmare. Throughout this guide, we have developed conventions and points of hygiene for making code easy to interpret, and therefore easy to use and easy to share with your colleagues/community. The following topics are listed from the most fundamental to the most nuanced. Start reading at the top of the list until you don't understand what we're talking about, then go practice and you can come back to pick up where you left off once you've learned more. Happy coding.

### Write from Left to Right
Whenever possible, we write scripts that read from top left to bottom right. If it is necessary to create more space for inserting a large step into an existing script, hold down alt and left-click to insert more space into the canvas. 

### Interface Shortcuts and Keyboard
Here are a few keyboard shortcuts which come in handy, more available here: https://www.grasshopper3d.com/forum/topics/what-hotkeys-and-shortcuts-are-available-in-grasshopper
- Type '//' for creating a panel
- Hold shift to add multiple wires to the same terminal
- Hold control to remove a wire from a specific terminal

### Common Data-Entry Mistakes
- Panels have two forms of data, strings and multi-line data. If you wish to create a mannually-entered list using a panel, you must change the data-type to Multi-line data. Simply right-click the component and press multi-line data to make this change.
- Don’t press enter in panels, this creates an extra line containing empty data that causes errors for many components.

### Explicit is better than implicit
When creating a script remember that you are telling a story. Make it so that someone else can read it. Don’t internalize values, instead use a panel if you don’t want people to change the value. Use a slider only when you expect someone to change values. 

### Inputs should be entered once 
If you have to enter a value twice in order to change an input, the script will become difficult to use. For example, lets say you want to measure the average number of daylight hours over your analysis period. If your analysis period is an entire year, you would be taking an average over 8760 days. If your analysis period is only a month, you would be taking an average over just 30 days. Write your code so that the length of the period dynamically updates, so that you don't mistakenly calculate an impossibly small monthly average because you didn't update the code to divide by 30 instead of 8760. This can be done automatically using either the original input, or a list-length component. Your code will be very difficult to use if someone must type in multiple values in order to change one input.

### Break the process down into steps
This guide will grouped components into distinct steps. Steps will be labeled and every effort is made to keep the guide in parallel with the example file. All inputs for a process will be located on the left side of a step in the process, and outputs will be located on the right.

### Boolean toggles
Boolean toggles warrant special attention because they are often used to trigger large calculations, with long calculation times. All boolean toggles which trigger a large calculation will be marked with a red group, to distinguish them from boolean toggles which simply change settings. It is also best practice to save files with these heavy-hitting boolean toggles in the false position, so that the simulation does not automatically run the next time the file is opened. Even better, use a false start boolean toggle from Ladybug, which automatically resets to false each time a file is opened.

### Updating, and Honeybee Legacy vs Honeybee Plus
There are two versions of Honeybee at the moment, Honeybee Legacy and Honeybee Plus. The difference lies in the way that each handles data behind the scenes. Honeybee Plus [+] is a re-write of the original Honeybee Legacy that makes it more platform-agnostic, cloud-compatible, scalable and more flexible for development. For most users, the difference will not be apparent but it is an important distinction when trouble-shooting.

As for updating, keep the latest release unless you have a major problem / bug. Limit automatic updating if you can, because it makes it difficult to figure out which version was last functioning properly. Updating is especially problematic when working in large organizations like schools or offices because it creates inconsistencies between users.

### For parametric studies:
Always question the workflow before building it. Know when you are trying to solve a 1D problem versus a 2D problem. Remember that it takes exponentially more time for each dimension of a problem. If you want to estimate the time necessary for a series of calculations, you should take the average of a representative sample of several calculations rather than timing one and multiplying that out.