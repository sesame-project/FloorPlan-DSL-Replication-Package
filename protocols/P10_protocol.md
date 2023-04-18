# P10 protocol

recording length: 00:38:04

### Section 1

00:17
Q: Have you worked on the navigation stack of a real or simulated robot?
A: Yes, on a real robot
Q: Can you describe your role in the development process?
A: The industralization and programming of the robot. By industralization, I mean that the robot is integrated into the production cell. By industralization role I mean that I worked in programming the processes that the robot performs whithin the production cell. 

01:27
Q: Would you say the problem of indoor environments is a solved problem?
A: No, there are a lot of issues. First of all, in a production cell that is encaged the robot will only have problems in the area that the robot can perceive and interact with. Some of the stations have collaborating robots outside the cages and must take into acount humans in the environment. Also, for mobile robots that navigate without an external guide, there are problems in staying in the planned paths and avoid crashes.  

### Section 2
03:50
Q: Can you describe in you own words the navigation stack you have worked with? What are the components?
A: The componets are the robots within the production cell, the controller of the robots, and controllers for the production cell which can interact with a human interface. 
Q: What about software components?
A: Mapping, Planning, and Control

05:19
Q: What are the inputs for the navigation stack?
A: The inputs are generally the goal coordinates of each stage of the process for the navigation.
Q: What about sensors?
A: We have different source of contact sensors in the grippers, also force sensors to determine if there is a cell or not. Positioning sensors to determine if the robot is in a specific area. 
Q: Does the robot perceive the environment?
A: Yes, with cameras. We have different camera systems for quality control and give information if the position of objects are incorrect. 

08:55
Q: Would you consider this navigation stack robust against the environment?
A: Yes, as it is in a cage and the process is flexible but static after configuration. 
Q: This is a very controlled environment?
A: Yes
Q: What would consider as robust?
A: That it is repateable every time, and that it can deal with external circumstances such as variations in the position of the cells in such as way that these circumstances don't affect the performance of the robot. 

11:35
Q: What can the navigation observe from the environment?
A: There are different sensors mounted on the head. For instance preassure. The sensors interact with cell to determine how much preassure its applied, the position of the cell, and where the cell is placed down. It determines if a surface is free to place down objects. There are many interactions between robots and the environment and humans. 

15:30
Q: What did the model of the robot entail?
A: For the simulated robot we simulated the different grippers in the specific areas of the production cell. 

16:39
Q: Did you ever found any bugs that were interesting related to the environmental features? 
A: Most of the issues where caused by interacting with the different sensors and its interfacees. Also its communication. There were many issues that only came up in the real world. 

### Section 3
18:48
Q: Can you describe the environment where you deployed the mobile robot?
A: The environment was a factory environment, with many safety features. We have some specific conditions for the temperature and the humidity, which are relevant for measurements in the production cell.

20:42
Q: How dynamic is the space? 
A: It is very dynamic, the production cells are flexible and change in between production cycles of products. 

22:49
Q: Does the dynamic aspect affect the robustness of the robot?
A: We are doing a lot of changes and set up within the production cell, and it does affect the robustness a bit. We try to change the production cell not more than once a day. 

24:40
Q: How big is this environment?
A: Quite large.

24:56
Q: Which elements do you need to describe this environment?
A: Within the factory we have walls, windows, big doors (from 2m to 1m). Withing production cell there are cages with many doors to bring in/out equipment.

26:43
Q: Is there something in the environment that is particularly challenging?
A: For the two robots there is only a challenge with external materials. 

27:34
Q: Which aspects of the environment can cause problem with the navigation stack you are familiar with?
A: The tooling can caused many issues as well as the provided materials for production.

28:38
Q: Can a software solution deal with the challenges? Or do you have to modify the environment?
A: We have tried to modify the environment in a way of the materials that are provided. For instance, a pre-sort of the materials before they enter the production cell. 

### Section 4

29:55
Q: How do you approach testing? Simulation first or real world first?
A: At the moment is real-world first. But we have alredy started working in a new project where we are approaching simulation first. We try to perform the process in the simulation first and then just perform tweaks in the real environment.

31:49
Q: How can you describe the simulation environment?
A: Just 3D models in the environment, with all the tooling and equipment that was not available at the time in place. And then we perfomed all the process steps. 

33:15
Q: What is the difference between the real environment and the simulated environment?
A: The difference we were not that detailed when performing the process in comparison to real life. After building up the complete tooling and preaccepted the design from suppliers, we realized of some issues that we were not aware during the simulation phase. We were not aware of the table size or the size of other things. 

34:26
Q: Have you ever needed to recreate a specific scenario in simulation?
A: Not yet. But it is a goal. 

34:43
Q: Would you find this challenging?
A: Of course, time consuming mostly. 

35:15
Q: What environmental features would you like to simulate but currently it is not possible?
A: We are not simulating the cooperation between different robots, becuase we have robots from different vendors. To simulate the cooperation of these multiple robots is very challenging. 

37:20
Q: Do you have any closing remarks?
A: No. 

== end of interview ==