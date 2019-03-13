**5.00** The final strategy we will compare in this initial guide is night-flushing. Just as before, it will daisy-chain to add another layer of information on the Honeybee zones output from natural ventilation. Located here:
![gh_05_overview_nightflush](https://user-images.githubusercontent.com/44324576/52487947-15713780-2bbf-11e9-9a2a-45c631d04174.png)

**5.01** Zooming in, we can see that Night Flushing actually uses the exact same component as Open The Windows did, the Honeybee_SEt EP Air Flow component. Note, however that we are using a different type of airflow here. Another key distinction is that we will be assigning a schedule, which is a way of informing Energy+ that we only want these changes to occur at specific times.
![gh_05_zoom_nightflush](https://user-images.githubusercontent.com/44324576/52489139-c4167780-2bc1-11e9-96bb-b142796f297d.png)

**5.02** To build this module up, start with the Honeybee_Set EP Air Flow component. 
![nightflush__0000_01](https://user-images.githubusercontent.com/44324576/52489017-81549f80-2bc1-11e9-8322-7d0d6f8f63cb.jpg)

**5.03** We will specify natural ventilation type 3. 
![nightflush__0001_02](https://user-images.githubusercontent.com/44324576/52489019-81549f80-2bc1-11e9-9ede-1fcc8113f6d6.jpg)

**5.04** If you hover your mouse over the natural ventilation type terminal, you can see that '3' corresponds to fan driven ventilation. So, this strategy assumes that there will be an electric fan which drives the air flow. This is much more reliable than simply opening the windows, but there is also a cost for running the fan itself. This simulation will only evaluate the potential thermal gains of this strategy, there is another layer of complexity involved with modeling the electricity consumed by the fan itself.
![nightflush__0001_02a](https://user-images.githubusercontent.com/44324576/52489783-73a01980-2bc3-11e9-9e9c-626146fb6e9d.jpg)

**5.05** The next step is to tell Energy + when we would like to turn on the fan. This requires a schedule. There are several different types of schedules in Honeybee, which are useful for annual, seasonal, weekly and daily behavior. In this case we will create a custom schedule that repeats the exact same daily routine year-round, and we will use it to modify the size of the window opening through which fan air blows. For now, start with the Honeybee_Constant Schedule component.
![nightflush__0002_03](https://user-images.githubusercontent.com/44324576/52489020-81ed3600-2bc1-11e9-9027-adee45d27454.jpg)

**5.06** The next step is to assign a value representing the size of the opening for airflow at each hour of the day. This is done using a Gene Pool component.
![nightflush__0003_04](https://user-images.githubusercontent.com/44324576/52490045-25d7e100-2bc4-11e9-973d-14b2fa31f0a0.jpg)

**5.07** When you first drag a Gene Pool component onto the canvas, it will only have 9 values. You must edit the gene pool by right-clicking on it and tapping 'edit'. 
![nightflush__0003_04a](https://user-images.githubusercontent.com/44324576/52489416-86feb500-2bc2-11e9-8376-c38e9e6b0ce2.jpg)

**5.08** This brings up a small menu like the one below, where you can change the number of genes to 24, and set the minimum and maximum values to 0 and 1, respectively. 
![nightflush__0003_04b](https://user-images.githubusercontent.com/44324576/52489417-86feb500-2bc2-11e9-8515-01e73ffbff50.jpg)

**5.09** Finally, we assign a name to the schedule. Do not use spaces in the name. This is important because Schedules are handled differently than many other forms of data in Grasshopper. They are actually saved as a text file, called an IDF file, and then the name of that file is passed on through Grasshopper. This is why you see the 'schedIFText' output.  
![nightflush__0004_05](https://user-images.githubusercontent.com/44324576/52489023-81ed3600-2bc1-11e9-9d28-b5e2c7168992.jpg)

**5.10** You can see that Grasshopper is only passing the name of the IDF file by connecting a pannel to the schedule output.
![nightflush__0005_06](https://user-images.githubusercontent.com/44324576/52489024-81ed3600-2bc1-11e9-82a7-92b2bbda53af.jpg)

**5.11** Finally, we will specify the size of the windows which is operable for night-flushing. We write 1 for demonstration purposes here, which assumes that the entire window area is open. In reality, this would mean a window on a a hinged door that can swing fully open, as opposed to a sliding window which cannot ever have more than 50% of its area open. 
![nightflush__0006_end](https://user-images.githubusercontent.com/44324576/52489025-81ed3600-2bc1-11e9-8781-8c948a26dbcc.jpg)

**5.12** Here is the resulting Energy Balance Diagram. Note that almost all of the cooling is attributed to natural ventilation now.
![008_night flush](https://user-images.githubusercontent.com/44324576/52487702-764c4000-2bbe-11e9-825a-b94dcb93cb4f.jpg)

**5.13** Revisiting the comfort graph we created in step 4 on natural ventilation, we have now added the impact of night-flushing on the comfort generally. You can see that we have greatly reduced the number of hours for which it is too hot, but the house is also now too cold to be comfortable for a significant part of the year. 
![06_comfort-graph_gif](https://user-images.githubusercontent.com/44324576/52487737-95e36880-2bbe-11e9-8f0d-b4f8883b2a92.gif)


This concludes the section on comparing passive approaches. This section is intended to provide an intermediate step between single-zone modeling and advanced multi-zone modeling. You should now be familiar with the following processes:
- Adding and removing layers of information/simulation instructions to Honeybe Zones. 
- Specifying context shading
- Changing the performance specifications of windows
- Changing equipment loads specific to a Honeybee Zone
- Introducing natural ventilation into a zone
- Creating and assigning equipment schedules

