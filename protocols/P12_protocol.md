# P12 protocol

recording length: 00:49:01

### Section 1

00:18
Q: Have you worked with the navigation stack of a real or simulated robot?
A: Yes.
Q: Can you describe your role in the development process?
A: My role was mostly to integrate and test. I was not a core developer for algorithms, but to bring together the components and test. 
Q: What sort of components did you integrate?
A: Mostly trajectory management, also perception. 

01:30
Q: Would you say that the problem of indoor navigation is a solved problem?
A: No. It is solved for certain cases, when a couple of assumptions hold. It works reasonable well is static environments with constant lighting conditions, constant material properties, and control of what objects and persons are moving around. These conditions allows the robot to perform well, but I general it is not a solved problem. When dynamic come into play, i.e. everything that makes the map to change significantly, this can lead to localization and navigation failures. 

### Section 2
03:20
Q: Can you describe in your own words the navigation stack.
A: Referring to robots that navigate in indoor scenarios, the navigation stack is a layered software stack that has high level component such as path planning (which can be geometry or topologically based), local navigation that uses sensor data to form a grid that helps determine if a desired motion might lead to collisions, and controllers that control the actuators to execute a motion plan. In addition, a localization component that gives you the pose of the robot with respect to the map of the environment

05:14
Q: What type of sensors are the input for the navigation stack?
A: There are different types. One of them are 2D laser scanners, it can also work with 3D laser scanners, and can also work with cameras. But the industry's best practice is 2D laser scanners.

05:54
Q: Would you consider the navigation stack robust against the environment?
A: I would say yes, since it has a lot redundancy. We have different sensors of different modalities that can sense multiple things. For localization we are able to use 2D SLAM and 3D SLAM. Everything can still fail, but redundancy brings a lot robustness.

06:50
Q: What do you consider as robust?
A: When the robot is able to achieve a task. If the task is to move from pose A to pose B, it should be able to finish the task, even if the solution is not optional. For instance, it could recalculate its path several times, but it finished successfully. So the success rate of the navigation stack is a measure for robustness. 

07:45
Q: What can the navigation stack perceive?
A: Different types of objects, like walls or doors. It can also see more challenging objects such as small objects and overhang objects. Small objects are objects that are below the 2D plane of the laser scanner, hence we have 3D cameras. Same for overhang objects such as large tables. Another category are objects that are difficult to perceived due to its material material. This include objects with very high or low reflectivity, or translucent like glass. But these objects are mostly static.

09:14
Q: Do you have a model for the robot platform for simulation?
A: Yes, we have one for two simulators. 
Q: What does it entail?
A: All the kinematic aspects of the platform, all the actuators (which movements can be simplified in simulation), and all the sensors. Several types of sensors can be simulated and recreate closely the behaviour of the real world, we can simulate 2D and 3D lidar, 3D cameras, RGB cameras, etc.

10:13
Q: How you ever found any bugs that were related to the environmental features?
A: There are inaccuracies in the simulation of the robot that is noticeable in the perception module, because the level and pattern of noise is difficult to recreate. This is a gap between the real world and simulation.

### Section 3
11:49
Q: Can you describe the environment where you have deployed the robot?
A: We have deployed it in environments with a variety of small to medium sized rooms connected with corridors, including very long corridors and open halls, so it is a very informed type of environment for testing. Also we have done test in different floors and basements for large similar buildings. This latter one was the most challenging. We have also deployed robots in industrial environments with large halls with sections where machinery is grouped together. And finally, a confined space where we do endurance tests.

13:21
Q: How dynamic would you say are the environments?
A: That depends, the most dynamic space was the basement of one of the buildings. In this basement there were movable containers that were parked near the walls of a hallway, so throughout the day every time you map the result is completely different. 
14:21
More dynamic than containers are persons, and the more dynamic environment we observed was the entry area of a building. It is different dynamic than the previous situation. In particular, a problem was groups waiting for an elevator.

14:56
Q: How would you say the dynamic aspect affected the robustness?
A: The person doesn't really affect the robustness, but it affects the performance. So a robot may take more time to complete the task but it will achieve it. There is more of a problem of robustness the case of the basement. The changes of the position of the containers was so extreme that the localization component was not able to localize the robot or calculate an incorrect pose. At any time a third of the room was covered by something, which makes each map significantly different. 
16:48
At this point we had no redundancy in the navigation stack, and this was the reason we started to develop it.

16:56
Q: What would you say are the elements that form this environment?
A: Walls; Doors, specially if they can be open or close. In particular if these are two double doors next to each other. Everything related to containers, crowds of persons, and smaller objects. This include tables and chairs that can be placed in corridors. Also, there could be a situation where you have a room with many tables and chairs that is difficult to navigate. And furniture can be troublesome since everyday they can be in different configurations. 
19:06
One of the most extreme cases was a kiosk with a magazine stand, which was hard to perceived with a laser scanner. But the kiosk had operation hours, and depending on the time the kiosk can be outside or inside. Another aspect is anything that can loose the mechanical stability of the robot, such as stairs. Glass is uncommon, but it is interesting to see the effect. Everything that is narrow is also interesting, a narrow travel path can determine if a test is successful or not, it can be the width of a door or the shape of a corridor. 
21:29
Features in the corridor can be problematic, one case was a container that was hanged to the wall so it was difficult to perceive, as it also had a reflective material. The worst possible case is a long corridor without features, as it introduces ambiguity on the position. 

23:00 
Q: Do you have a map that you can show?
A: Yes. As you can see, these is the very long corridor I was talking about. There is a ramp that is not visible in the map, and it has the effect that it elongates the map for a small amount. The corridor is not completely feature-less, but some parts have very few features. Also, due to some renovations, even the walls were not fixed.
Q: I notice the corridor is a bit curve, is this a drift problem?
A: Indeed. We asked for architectural drawings but these were not available. You can also see that there is no loop closures, there is no chance for the algorithm to handle that. As long as you stick to the map, the curvature is not really a problem.
30:00
Q: Is there anything on this map that you think is problematic?
A: The containers that constantly occlude the wall.


32:00
Q: Can you think of another areas that can be problematic?
A: Everything that has a long feature-less corridor for the localization, and anything that has a narrow passage for the navigation. You can have paths with door of multiple widths, some might be easier than others. This is because there are safety margins.

33:13
Q: Do you think a software solution can deal with these challenges?
A: To some degree it can be solved by software. But you also need to think on your hardware for redundancy and placement of sensors. From the perception side, you can try to perceive static features. You may also try to go for other localization strategies to deal with these issues. 

35:00
Q: What is the impact of the quality of the map for the performance of the system?
A: There is an impact, if there is a discrepancy between what you see in the real world and the map this will degrade the performance. It really depends on the situation. To see the effect you need to see the entire system. For applications where you really rely on the map, the task will degrade.

Q: And what about a map that is too perfect? 
A: For my experience, something that comes from an architectural drawing will perform worse that a map obtained by the sensors. Because this is what the robot sees, you want it to look like it looks to the robot. If you start from an architectural drawing, many things don't look the same. There are irregularities that can be even considered features. And sometimes architectural drawing are really inaccurate. It is also more effort to create a map from an architectural drawing, it might be easier with BIM. 

### Section 4   
39:25
Q: How do you approach testing? Is it simulation first or real world fist?
A: There is no direct answer, it mostly depend on the availability of hardware. But must of the time it is a co-development. For example, we went to an environment to create the map, we cleaned the map, and create a simulation environment. Both activities go hand by hand.

41:25
Q: How would you describe the simulated environment?
A: They are based on a occupancy grid, so the map has a lot of artifacts, but it is nice enough for testing. It has allowed us to replicate some situations, even though it is not optically nice. We had one case where we had a floorplan and we built a rough replica of that environment, and then on the simulator we were able to add some furniture. If we build this environment without seeing the real-world first, then we would focus on what is stable. i.e. the walls, and then dynamic object such as doors can be later added.

43:59
Q: Have you ever tried to replicate a specific situation in simulation?
A: Not me but colleagues, they were trying to trigger a weird behavior.

44:21
Q: What environmental features would you like to simulate?
A: Human-like looking persons, and realistic looking "loads" (containers). Other than this, better physics. And some aspects to simulate our application-specific behaviours. and better lighting.

46:00
Q: Do you have any closing remarks?
A: It is important to note that creating new environments are difficult to create. It should be possible to reduce the amount of time required to have an environment ready to simulate. It would be nice to also have variations of the environment. The easier it is to specify and obtain these environments, the better. It would also be nice if we don't need to specify every aspect, so we could say "we would like some clutter in this room" and get a room with a number of tables.

== end of interview == 