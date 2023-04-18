# P8 protocol

recording length: 00:45:56

### Section 1
00:26
Q: Have you worked on the navigation stack of a real or simulated robot?
A: Yes. With both.
Q: Can you describe your role in the development process?
A: I was the tester. I tested plugins for the mapping, and the local and global planners.
Q: What did these tests consist of?
A: My goal was to integrate the platform and the navigation stack, so my tests had that objective. Another of my projects was regarding robot collisions, so a lot of tests also focused on that. The test were performed to optimize parameters and try to make the stack work.

1:40
Q: Would you say that the problem of robot navigation in indoor environments is a solved problem?
A: I don't think so, I think this is still an active research topic. The current state works, but it is not completely solved.  
Q: What are the challenges?
A: The most popular navigation stacks are based on static maps. If you change the position of objects in the environment it is very challenging to detect what is an obstacle. In the case of a table, a 2D laser scanner will detect the four legs, and not the surface it can collide with. This type of obstacles are hard to detect when the environment changes constantly. 

== Interview interrupted by internet problems ==

6:07
A: In addition, when there are humans in the environment, there is a limitation in the robot's performance for safety. The robot has to move slower and think better of its movements. 
Q: So depending on the application can you consider the navigation problem completed?
A: It depends quite a lot. For an application in a warehouse where the map does not change that often, you can consider the problem solved. But for more dynamic environments you cannot call the problem solved. 

### Section 2
07:52
Q: Can you describe in your own words the navigation stack?
A: There are four components: One is the mapping, the localization component, the global planner, and the local planner. The global planner is in charge of planning the path between two locations in the space that avoids the known obstacles in the map, the local planner is in charge of handling the errors of the map and dynamic obstacles, and try to prune the global path. These are the four basic components.
9:00
Q: Would you say that this navigation stack is robust against the environment?
A: It depends, for static environments is robust. But the robot has problems when the map does not reflect the reality, i.e. when the environment is dynamic. It is hard to say if something is robust because it depends on many factors, but specially the application.
Q: What would you consider as robust?
A: In general, To get a robust navigation stack one would introduce intelligence to the navigation stack. The default version of the navigation stack has limitations. 
Q: How would you measure robustness?
A: It's tricky, it depends on the goal of the project. There is no general definition of robustness, it depends on the application and the task, on how you define the optimal behavior. It's complex. What I can say, is that safety should be included in the measure of robustness, but it is hard to measure.

14:08
Q: What can the navigation the navigation stack perceive?
A: It depends on the perception system. With a 2D lidar you will perceive a single height. A depth camera will perceive a 3D world. A 3D lidar will have a wide spectrum. If you have cameras, you can have a good idea of what's in front of them, but you won't have idea of what is in the back. To have a proper perception system is to have a 360 degrees perception, but this is expensive to achieve computationally and economically.

15:48
Q: What did the model of the robot in simulation entail
A: In general just the kinematics, sometimes the shape of the robot. But it is very hard to attach the dynamics of the real robot. For the navigation perspective at least.

16:55
Q: When you were testing, did you find any bugs that were related to the environmental features
A: The only one that I found interesting is that you only detect some parts of the tables, so it is difficult to detect completely. Also, sometimes the planner cannot decide on a path so the robot starts shaking. 
Q: Was this because the space that it had to go through was very narrow?
A: Sometimes yes, sometimes no. Sometimes the space is quite wide, there are no obstacles, so its gets stuck because it doesn't know where to go
Q: Is this because it cannot localize itself? since everything is far away? Or is it because there are multiple paths to the destination?
A: Three different things: the global path may not be optimal, if everything is free then the robot will try to move too fast and it will impact the localization, and also the localization tend to fails.

### Section 3
20:22  
Q: Could you describe in your own words the environment where you would deploy the robot?
A: One of them was an industrial set up with small obstacles and narrow spaces, the challenge was to try not to collide with any obstacles. Another environment that I worked with had a familiar house environment, with lots of furniture. Another environment was a warehouse environment that was very static. Some of these environments are more structure than others, and also more dynamics than other.
22:42
Q: How dynamic were these spaces?
A: Some were really dynamic since they had lots of people coming in and out of rooms and moving around. Some were really structured without people or moving furniture. The warehouse was very static but the workers had predictable behavior. But all these spaces had their static parts. For instance, for the home environment I had to manually set every furniture to a known position to make the localization component work. 
24:16
Q: How big were these environments?
A: Some not that big, between 30 to 40 squared meters. In particular the warehouse was quite large.

24:45
Q: What elements do you think are needed to describe this environment?
A: The most important things are the obstacles. This is because the robot should know what is a movable object and what is a wall, but this is a challenge. What is usually part of the map is the walls, the kitchen cabinets, the refrigerator, it all depend if it's considered static. For instance, you have to map the doors open. 

26:45
Q: Was there something in this environment that you found particularly challenging?
A: The chairs, since the localization maps everything in 2D, it only detects the legs and the robot will try to go through the chair. This is the same issue with the table. For the warehouse, the reflectiveness of the material caused problems with our Time-of-flight cameras, it would detect a wall nears the sensor as if it was several meters away. Sometimes the problem is not in the environment but in the characteristics of the sensors.

28:20
Q: Do you have a map that you could show?
A: No.

29:26
Q: Was there something in the environment you didn't expect when you began testing?
A: Yes, the robot had trouble with bumps and cables in the floor. The robot would not detect a bump/cable, and it would shake enough that it would affect the localization and planner. Sometimes the driver crashes when it came across a bump at high speed.
Q: Were these bumps between door frames? Or were there irregularities on the floor?
A: Sometimes the bumps were in the door, but the map assumes that it is very flat. These bumps are common, and you have to be careful. When mapping you would have to filter this and maybe assign a cost to these areas. Maybe even limit the speed when you are nearby a bumb. 

32:43
Q: Which aspects of the environment can cause problem to the navigation stack?
A: I would say environments with many things (crowded) are problematic. When you start moving furniture then you can also have a lot of problems. You need to take them into account. An while it is not an aspect of the environment itself, the sensor set up of the robot is important to deals with these issues. In a hospital environment, the incorrect setup can be considered unsafe.
Q: What do you mean by incorrect setup?
A: You need a smart selection of sensors (their type and their location in the robot platform), and a good set of parameters for algorithms. For instance, you can have a camera pointing up or down. 

35:50
Q: Do you think a software solution can deal with these challenges?
A: I would say a software solution is possible, there are cases where the environment cannot be changed. But the solution doesn't have to be just software, maybe you can also optimize the hardware. In the case of robotics, you have to always think of more than one system to think of a proper solution.

37:10
Q: What do you think is the impact of the map quality in the performance of the system?
A: There is a big impact, but in my experience the resolution of the map doesn't matter. 
38:21
A: I don't think there is a perfect a map, I would say the map should be accurate in its representation. 

### Section 4
39:28
Q: When beginning development, how do you approach testing?
A: Simulation first. Always. Specially when you are trying to optimize controllers, if it is not working on simulation it is not going to work in the real world.
Q: What types of environments do you use to perform tests in simulation?
A: There are plenty open-source simulated houses which you can use to see the performance of all the components of the navigation stack.

40:37
Q: How would you describe the simulated environment?
A: In terms of testing, it is enough to have a simulation that recreates the real world. In terms of localization, simulation is not accurate because you cannot simulate the sensor noise. Since the sensor readings is tightly coupled with the results of the localization, then you have to test it in the real world. And in terms of the local planner, the simulation is just an approximation. 

41:44
Q: How different is the real world from the simulation?
A: The bumps are not present in simulation, for instance.  

42:46
Q: Have you tried to recreate a specific situation in simulation?
A: Yes I have tried. I tried to simulate collisions for instance. 

43:33
Q: What environmental features would you like to simulate but it is not currently possible?
A: I would say everything is possible but you need a lot of time to make sure that it works. 

45:15
Q: Do you have any closing remarks?
A: The current navigation stack is the most stable one that is available to the community, and in general it is not optimal but it is a good start.

== end of interview ==