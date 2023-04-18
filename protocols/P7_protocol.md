# P7 protocol

recording length: 00:33:36

### Section 1
00:21
Q: Have you worked on the navigation stack of a real or simulated robot?
A: Yes.
Q: Can you describe your role in the development process?
A: I designed and developed the architecture for the navigation stack and I developed many of its components. Although this was for aerial robots.
Q: What were the components for?
A: Localization, trajectory planning, control, communication, state machines.

01:11
Q: Would you say the problem of navigation in indoor environments is a solved problem?
A: No
Q: What are the challenges?
A: If the environment is static then you can say is the navigation stack is "alright", but when there are dynamic objects/entities there are still many unsolved challenges. The robot are not able to fully understand the environment. It also depends on the sensor, using a 3D lidar is in a more advanced state than using cameras. There are many robots out there using 3D lidar for navigating indoors, but based on only on cameras is more challenging.

### Section 2
02:33
Q: Can you describe in your own words the navigation stack?
A: In general the navigation stack is set of components for localization, plan, and drive the robot to a localization. 
Q: What about the navigation stack you developed?
A: For the navigation stack I developed (which was for aero applications) we had a multi-layer approach with multiple systems, you had feature extraction, situational awareness, control, planning, execution, supervision, communication and interaction.

04:03
Q: What were the inputs/sensors the robot used to perceive the environment?
A: It was a generic approach with generic inputs and outputs, and we developed specific components. We were mostly focusing on vision sensors, including RGBD cameras. Since it was for aerial robots, other sensors that come in drone autopilots were also included, such as IMU, magnetometer, etc. 

4:46
Q: Is the navigation stack robust against the environment?
A: Not really, if the environment was very dynamic and unstructured of course the system would not work
Q: What would be your definition of robust?
A: For me it is that is able to perform the task even in different situations that are beyond of what it has tested and designed for. So new environments and situations with different objects and conditions. 

05:58
Q: What can the navigation stack observe?
A: It should perceive the environment and build an understanding of the situation, at multiple levels of abstraction. So not only understand the geometry of the environment but also semantics and relationship information. 
Q: And how is it currently?
A: Currently we understand quite well the space geometrically, and work have been done for semantic understanding. But more complex semantical information as well as topological information are required for a more deep understanding of the environment.

07:44
Q: What did the model of the robot entail?
A: I have worked with aerial robot, and it is hard to have a good model, for many conditions that are hard to simulate (ground effect, wall effect, ...). For ground robots you can have a more detailed model that is more accurate that can be exploited in the state estimation and simulation. 

08:53
Q: Did you ever found any bugs that were interesting related to the environmental features? 
A: Situational awareness is environment dependent. The environment were we deployed some drones had metallic structures, and they cause problems with the magnetometer, it goes crazy, so the drone can no longer locate itself in the environment. 
Q: What is the magnetometer for?
A: It measures the magnetic field of the earth and it is essential for estimating the orientation of the drone. 

### Section 3
11:37
Q: Can you describe the environment where you deployed the mobile robot?
A: For drones we deployed it in bigger indoor environments, we even deployed them in basketball arenas. With ground robots we went to construction sites. It is challenging because it is often dirty and unstructured. 

12:42
Q: For the ground robots, how dynamic were these places?
A: We tried to make them quite static, but we still tried to incorporate a way to perceive dynamic obstacles and people and avoid collisions, but our focus was on static environments
Q: How big were these environments?
A: The size of a family house.

13:49
Q: Which elements do you need to describe this environment?
A: For the construction site it was interesting because there were not many things, as it is still under construction, so we used the structure of the house like the walls, the columns, bricks on the floor and tools, but mainly the structure.

14:36
Q: Was there something in the environment that was particularly challenging?
A: The robot had lidar, and the most challenging part were windows. Lidars cannot see windows so we had to be careful.
Q: What was the effect of the windows? 
A: Depends on the stage of the construction, sometimes the window didn't have the glass pane installed, and sometimes it had. But the laser beam of the lidar sensor goes through glass so it can not get detected. It was dangerous because the robot does not detect it.

16:11
Q: Was there something in the environment you did not expect?
A: We were expecting the walls and the columns, we even had the plans for the construction. But there was water...

16:41
Q: What do you think are problematic areas? 
A: There are many challenging, windows and mirror are challenging if you are using lidar or cameras. Depending on the material it can also affect your sensor, such as metal with the magnetometer. For a very dark material it can absorb the lidar beam. Another challenge are dynamic obstacles, and understanding the environment. i.e. understanding that a piece of furniture is not fixed but also that it does not move often. Interacting with objects such as doors and chairs is also challenging. 

18:35
Q: In terms of the spatial aspect, what do you think is problematic?
A: Depends on your sensor, a narrow corridor can be challenging for a lidar sensor, as the robot may not be able to localize itself in a corridor that looks the same. Specially if the environment does not have any texture, you will get lost even with vision based navigation. It can also be problematic for the lidar sensor to detect features in environments that are too large (e.g. a desert). If the robot is big, a narrow area is challenging. Steps are also hard to detect if the camera/laser is not pointing at the floor. It really depends on your sensor configuration, you need the right sensor for the right environment.

20:30
Q: Which aspects of the environment can cause problems to the navigation stack?
A: It depends on the sensors, for lidar sensor glass or dark materials are challenging. Obstacles and stairs that are not in the field of view can also be dangerous, including small objects such as nails. Water can also be a problem, and we had some in the construction site.

22:05
Q: Can a software solution deal with these challenges?
A: To deal with these challenges you need to build a deeper understanding of the environment. If there is a window, but the robot cannot see it but it knows about it, even if you can't perceive it you can estimate it. There is also work to be done in sensor fusion. The lidar might not work in an instance, but a camera will, or vice versa.

23:37
Q: What is the impact of the map quality in the performance of the system?
A: I think it is essential for the performance, I consider it part of the situational awareness. You can plan and execute the tasks better with a better map. 
Q: How would you measure the map quality?
A: For me the map is more than the geometry, it should incorporate semantic, dynamic, and topological relationships, and of course its hard to measure the quality. You can measure the geometric quality with certain proposed metrics, but the semantics it is harder to measure.

25:15
Q: If you build the map from the construction plan with work better than a noisy map obtained from the sensors?
A: The plans are only plans and may differ from the reality, so we don't use it blindly. The idea is to have a prior that we can adapt with the real measurements. And on top we can add the semantics and topological information to the map to increase the situational awareness.

### Section 4
26:51
Q: How do you approach testing?
A: Depends, but normally we first try to develop in a simulator. In some cases this is very difficult, and depends on the purpose. For visual slam, a realistic simulator is very challenging and is better to work with the real system. For lidar it is easier to work with simulation. If you are working in trajectory planning and control maybe simulation makes more sense.

28:28
Q: How would describe the simulated environment?
A: It depends on what we are testing, simulation is very generic. For VSLAM you need a photo realistic environment, for lidar you may not need so much detail but you need to provide some detail for features. For control you may not even need a realistic simulator. For trajectory planning it doesn't have to be realistic. So it depends.

29:49
Q: What would you say is the different with the real environment?
A: The simulation is always simpler, unless you spend a lot of time in making the details. For trajectory planning you may even create more challenging environments such as labyrinths. It depends on what you are simulating.

30:48
Q: Have you ever recreate an environment in simulation?
A: Yes. But we know we are simplifying it.
Q: But is it challenging?
A: It depends on the purpose, for a simulator you first need to know why you are doing it for. For some purposes, you may not need a realistic environment, but to test the situational awareness you need a very accurate environment. 

31:56
Q: What environmental features would you like to simulate but it is currently not possible?
A: For me the most challenging to simulate is realism. It is hard to obtain realistic measurements from the simulated sensors that are similar to those obtained by the real robot. I don't think that nowadays is possible, and it is something that has to be dealt with.
Q: Is this only for cameras or for other sensors as well?
A: Cameras are the most challenging, but this applies to other sensors such as lidar. We once recreate an environment and created a robot model with the sensors for simulation, and the simulated sensors produced way different measurements. The measurements were not the same as the ones for the real environment. 

33:22
Q: Any closing remarks?
A: No.

== end of interview ==