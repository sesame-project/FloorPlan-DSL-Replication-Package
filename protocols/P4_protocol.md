# P4 protocol

recording length: 00:51:43

### Section 1
00:33
Q: Have you worked on the navigation stack of a real or simulated robot? 
A: yes

00:45
Q: Can you describe your role in the development process? 
A: Motion planning development. But also the entire pipeline. Slightly higher level. 

01:21
Q: Would you say that the problem of navigation in indoor environments is a solved problem? 
A: With "extreme" assumptions yes, but in general no.

01:39
Q: What are the challenges remaining? 
A: Dynamic environments. Mostly obstacles in motion, such as humans. Especially in small environments, such as small rooms. Certain software stacks cannot handle the dynamics well, as they constantly re-plan their path to avoid obstacles; this has the effect that the robot does not move (or very small movements). Another challenge is configurability, most approaches rely on one solution that is applied everywhere instead of a solution that is tailored to a specific problem. Special environments also present challenges for localization, such as malls where stores use glass as fronts. Localization is fundamental for navigation, if the localization is off by a few tenth of a centimeter the motion planning might have unwanted behavior (wiggle, rotations).

06:10
Q: What can make localization difficult? On top of glass walls. 
A: Clutter (like furniture) after mapping. The robot will see the furniture and will be able to avoid it, but the localization module will be confused. Dynamic obstacles cause the same problem, or adds to the problem. Also faulty odometry.

### Section 2
07:54
Q: Can you describe in your own words the navigation stack?
A: The components depend on the task (e.g. follow humans or pick and place). 
Q: But what about a particular case?
A: Localization based on distance sensors (2D/3D lidar), Map module (before navigating), planning (at a global level, unlike grid based planning, something more abstract), motion planning and control (for short durations).

10:24
Q: Would you consider the navigation stack as robust against the environment?
A: Depends on the implementation. 
Q: But what is depends on?
A: The assumptions. If the environment suits best for the assumptions then it will work, with a correct implementation and tests. But if the environment changes and the assumptions don't hold, then the navigation stack won't hold either. 
Q: Which assumptions are we talking about? 
A: For instance, if the environment has glass walls or not. Or if the floor is flat, or if there are stairs in the environment. Or the size of the environment. But it depends on the designer. 

13:50
Q: What can the navigation stack observe at the low-level?
A: Ranges and intensities. Lidar sees distances, how far the object is and how reflective is. Same with 3D lidar, and RGB depth cameras. Wheels with odometry/encoders. Sensors that look at the floor and tries to localize using the pattern. GPS in big environments, specially those that are indoor but has outdoor challenges (weather conditions). Wi-Fi strength/beacons used for triangulation.  

17:15
Q: Do you have a model for simulation that captures the real-world platform? 
A: Up to a certain extend.
Q: What does it entail?
A: For an omnidirectional platform, we bypass controller-level details. We can say that the robot slides through the floor. Friction is not relevant in simulation. It depends on what you want to simulate. Setting up a simulation that is as-close-as-possible to the real world is rare, simulation has an intention. 

19:49
Q: Did you find ant bugs that were surprising? Related to environmental features.
A: Yes. Reflectivity. For instance, the door frames of a building that are made of metal. This had an effect in the distance calculations, and a door frame that in reality has a gap of 80cms, it has a perceived gap of 20cms. Thus, the robot perceives an open door as closed. Sunlight is also interesting in the way it is perceived by sensors. The robot thinks the sunlight is an obstacle, because it is perceived by the IR sensor.

### Section 3
23:40
Q: Could you describe the environments where you would deploy the robot? 
A: Ideally it would be a warehouse. Sunlight is not a problem since the light source is artificial. No humans since it's completely automated. Extremely flat floor. With markers for better localization. 

25:36
Q: Can you think of the elements that form this environment
A: Walls, ceiling, robots, pallets. Things that the robot can interact with but it has knowledge about it beforehand/a priori. 

26:28
Q: Is there something that is particularly challenging?
A: Sunlight problem, and glass doors/windows, uneven floor (with bumbs or cement), very wide/open areas where the range of the laser sensor is insufficient.
Q: How uneven must the floor be to cause problems?
A: Few centimeters every two meters in height difference. In a conical shape. You would need suspension.

30:00
Q: Do you map that you think is interesting that you can share? 
A: Yes. This is a very clean map that was generated automatically from another format of a map (semantic map). Walls are very clean with no noise. The map representation does not care about glass walls. It assumes that everything can be seen by a sensor. 

33:34
Q: Is there anything in the map that you think is problematic?
A: The glass corridor, the railings (which are not in the map, as the sensor is not at the same height), stairs (going up not a problem, the robot can detect it). Walls where there should not be walls (i.e. where doors are also considered as walls)

36:16
Q: Which aspects of the environment can cause problems to the navigation stacks you are familiar with?
A: Sunlight, glass walls, uneven floor, humans (specially when there are many).

37:32
Q: Do you think software can deal with these problems or do you have to change the environment?
A: I think is possible, but it depends on the project. But modifying the environment is often not an option.

39:34
Q: What is the impact of the map quality on the performance of the system?
A: It depends on what the assumptions are. If the map is very close to what the robot will see and the parameters are correctly tuned then the performance will be good.
Q: But what if we have a perfect map? 
A: It partially depends on map and partially depends on localization algorithm and it's parameters.

### Section 4
41:11
Q: How do you approach testing?
A: It depends on what the hardware can do, what the deadline is, and how much time it takes to setup the simulation. 

42:27
Q: What was the hardest part of setting-up the simulation?
A: For navigation is was fairly simple. 

43:35
Q: How would you describe the simulated environment? How different was it from the real world?
A: Sunlight was not possible to simulate. Nor reflection of materials. It impacted the way simulated sensors performed. Uneven surfaces are not really interesting for navigation task that I was working on, but it is a problem to simulate. Simulators can't "weight" a floor. The floor is completely flat, and you don't need a ceiling. The sensor readings are different than the real world, even with added noise, specifically for convex corners. Also, RGBD cameras' cloud points are not reproducible, a wavy pattern is present in real sensor but not in simulation, which can mess the readings. 

48:27
Q: Have you ever needed to recreate the real-world in simulation?
A: Yes. 
Q: Any challenges?
A: There was a ramp we wanted to create, but the simulator didn't like it. We had to tweak the weight of the ramp for it to stay still. The physics would not allow it. We didn't try to recreate glass walls. 

50:18
Q: Do you have any closing remarks?
A: No. 

= End of interview =