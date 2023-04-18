# P14 protocol

recording length: 00:47:36

### Section 1
00:20
Q: Have you worked in the navigation stack of a real or simulated robot?
A: Yes. In both.
Q: Can you describe your role in the development process?
A: I've worked in many stages of the project, but mainly integration. We used existing techniques for navigation, so we configure the navigation modules but also the simulation. We also wrote new modules for local and global planning.
Q: Are the components you used are the defacto standards?
A: Mostly modules that exist on the community, but we also developed our own. The reason was the existing shortcoming for the current modules, but we wanted to develop components that were a better fit for our application.

02:17
Q: Would you say that the problem of robot navigation in indoor environments is a solved problem?
A: No. 
Q: What are the challenges?
A: If you want to navigate you need to include planning and localization, in the high and low level. Most of the current modules rely in accurate localization, and use geometric representation to know where the robot is located. You plan a global path, and then try to stick on that plan with the use of local planners. So everything is very rigid. This is different in how we as human move around the environment. We think in terms on which directions we are going to move. This method is widely use, but it require very high localization that is hard to obtain, and once you have it you then have to try to stay in a rigid path where the robot will run into issues. 

### Section 2
05:07
Q: Can you describe in your own words the navigation stack you have worked with?
A: I've worked with the "classical" navigation stack, the most widely used. Where you have a map of the environment (grid map), you try to localize yourself in it, and then try to design a path from point A to point B by following a set of poses. You have a local planner that based on the position of the robot in the path, it will determine the velocity commands so that the robot follows through with its plan. In another navigation stack I've worked with we tried to rely less on the accuracy. Also, the environment was divided into sections with semantics. This semantic map allowed us to do planning in the topological level, instead of planning on the occupancy grid. Another layer is in charge of executing the plan, and this one only has to keep track of the local environment. It is important to keep in mind the footprint of the robot when planning to make sure that the movements are safe for the robot to execute, i.e. avoid obstacles. In cases where we didn't have a map, but a goal, with use a combination of methods to steer the robot, such as potential fields. 

10:44
Q: What were the input of the navigation stack?
A: If we talk about sensors, we used 2D lasers for building the grid map. For obstacles we read the values of the laser to determine whether the robot could collide with obstacles. This is different from other frameworks use costmaps.

12:14
Q: Would you consider this navigation stack robust against the environment?
A: Not completely. We were trying to make the navigation stack robust with semantic information. If you are in a hallway with a room, you notice there is a room with an open door, there is uncertainty that a person could come out of the room. This uncertainty requires semantic information to deal with it. A simple action is to slow down and try to see if something is coming. This type of actions are missing in the navigation stack.

14:01
Q: What can the navigation stack perceive?
A: Sometimes there are perception modules in the navigation stack, in our case it was simple. We perceived whether or not there was an object in the plane of the laser scanner. But we didn't try to know exactly what was in front the scanner (a person, a wall, an object). We worked only with lasers, but cameras allow you to do more. 

15:31
Q: What did the model of the platform entailed? 
A: We are interested in the kinematics of the vehicles, so we were not interested in the dynamics. It was important to simulate the kinematics of the robot and the environment. 
17:15
A: We simulate sensors, and we are not interested in simulating the wheels, but more interested in how the robot would move. So the most important part was the movement constraints at the platform level. Regarding the sensors, we only simulated the laser. 
18:24
For simulation that I have worked on in the industry, there were simulations that were more complete. We tried to simulate as close as possible the real robot. But the specifics of what to simulate depends on the requirements of the project.

18:54
Q: Can you think of bugs that were related to the environmental features?
A: Yes. The environment is the source of all faults, specially the dynamic features of the environment. Localization errors due to dynamic objects is very problematic. Perception components should keep track of the objects in the environment to make the localization more robust.

### Section 3
20:50
Q: Can you describe the environment where you have deployed the robot? 
A: Yes, one of the environments was a hospital, which was very structured and rich in semantics. We also worked on robots that are deployed in warehouse type of environments. There are similar structures with large hallways that break into smaller hallways. But if you want to use a laser to measure the environment, there are more distinct features in the hospital than in the warehouse. In the warehouse it was also challenging since the racks have objects that change overtime.

22:53
Q: How dynamic were these spaces?
A: Very dynamic, in the warehouse the content of the racks changed all the time. You have people and vehicles moving around. Hospitals similarly has lots of people moving around, with even employees moving objects around. 

23:44
Q: Which elements do you think you need to form the environment?
A: The stable features, the ones that I can rely to localize myself. For instance pillars, which you know they are static. Then you have semi static features, such as carts and boxes, which can be static when you detect them but move in the future. Then you have dynamic obstacles that always move. 

26:30
Q: What would you say it's an aspect of the environment that was particularly challenging?
A: One of them is dynamic obstacles, which can include doors. But on the physical part, the unevenness in the floor can be problematic for robots relying on LiDAR. Reflective materials such as glass and metal can also be troublesome, and you "measure" objects that don't exist.

29:14
Q: Was there something in the environment you did not expect? 
A: There was one situation when we visited a space that was complete chaos. They sorted and moved metal parts around, and even you as a person would get lost inside the space. It was really dynamic with lots of hard-to-perceive objects. We ended up asking to move to a more structured place.

31:00
Q: What type of areas do you think are problematic?
A: Areas that change a lot. Delivery areas a problematic for instance. If you are in such an area, you need to build new information and connect it to the only information you have. 

33:10
Q: Can you think of aspects that can cause problems to the navigation stack?
A: Light, specially when you are using cameras. Also changes in the friction coefficient of the floor. And areas that change a lot. 

34:30
Q: Do you think a software solution can deal with these problems?
A: Certainly yes. I think if you can sense the environment and attach meaning to those measurements, you can distinct what were the changes that occurred so you can rely more on the static elements of the environment. You can also add hardware for redundancy, add beacons for localization, and reduce light sources. But this approach is costly and not reliable.

37:22
Q: What do you think is the impact of the map quality in the performance of the system?
A: The impact will depend on how robust the navigation stack is. If it relies too much on the grid map and the quality will impact the performance. The map is only one of the inputs to the internal model of the environment. For the current navigation solutions it does have an impact.

38:25
Q: Do you think a map that is too perfect will have a better or worse performance than a noisy map?
A: Depends on the navigation stack. For the classical navigation stack then it's better to work with a noisy map obtained from the sensors. If you attach semantic information to the map then you won't need a high accuracy map. 

### Section 4   
39:42
Q: How do you approach testing? Simulation first or real-world first?
A: Simulation first. But you don't want to stay to much in simulation. You want to workout most of the things in simulation. In an application where the robot must have contact with the environment then it might be better to quickly move to the real robot. Physical interactions with the objects is very difficult to model and simulate.

41:20
Q: How would you describe the simulated environment.
A: You try to simulate the target environment to develop the high-level behavior of the robot, for instance move it to a certain place, and you try to make a simulation environment that is similar to the real world. Also, continuous integration tests try to recreate small situations for small automated test. 

42:58
Q: What is different between the real world and the simulated environment?
A: Mostly in the simulated environment you start with a very static simulation. Where you include mostly the static elements of the environments, since dynamic objects are very hard to simulate. For simulating humans, there is a complex interaction between a person and a robot system that is hard to model.

44:00
Q: Have you ever tried to recreate a specific situation of the real world?
A: Yes. Sometimes you try to recreate simplified real-world situations. 
44:32
Q: Did you find it challenging?
A: It is challenging if you want to make the environment as close as possible to the real world, but what you do is to simulate a simple environment.

45:05
Q: What environmental features would you like to simulate but are not currently possible?
A: Doors are challenging, specifically their behavior (open, close). Also interactions with people, so what happens when two people want to cross the same door and there is only space of one of them. Currently with open source simulators we don't have good models for simulating humans.

46:11
Q: Any closing remarks?
A: To summarize, we as research community we should strive for new navigation concepts that are robust to the huge uncertainty that you have in real dynamic environments. Where your environment changes constantly and you need to keep track of all changes to the environment and rely on different kinds of sensors. We still have a long way to go.

== end of interview ==