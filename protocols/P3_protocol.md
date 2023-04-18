# P3 protocol

recording length: 00:43:36

### Section 1
00:34
Q: Have you worked with the navigation stack of a real or simulated robot?
A: Yes. with both.
Q: can you describe your role?
A: For simulation: developed the simulation package for a company I worked for. The package was develop for ROS 1 and was comprised of controllers and configurations. Also worlds and plugins for Gazebo. Currently, we are working in creating the simulation package for ROS 2. In the real wold, I worked in the migration of the navigation components from ROS 1 to ROS 2, including the development of behaviors.

04:16
Q: Would you say that the problem of simulation in indoor environments is solved?
A: Not at the moment. It depends on various aspects. One of them is that cost of the navigation components. Higher cost sensors lead to better performance overall. A lot of work have to be done in the software and hardware to reach a point where the problem of navigation can be considered solved, but problems will still exist.

### Section 2
08:14
Q: Can you describe in your own words the navigation stack? 
A: I have worked with software stacks for ROS 1 and ROS 2. ROS 1 has deficiencies in local planners, and its de facto software stack was inflexible. ROS 2 planners has more flexibility thanks to the behavior trees. But the problems with planners persist. An improper planner makes the robot lose one degree of freedom. 

11:26
Both navigation stacks work on a cost maps, where the environment is modeled with different sets of cost around the environment. Some planners/controller do not [unintelligible] all the costmap information as part of the planning. There is still work to be done for the planner to be complete.  

12:34
Q: What would be the inputs for this navigation stack? what would be the sensors?
A: For 2D navigation, 2D LiDAR. The output would be velocity and position. 

13:45
Q: Would you consider this navigation stack robust against the environment? 
A: Depends on the environment, in an industrial environment where nothing can be harmed or damaged, we can work on the velocity level. i.e. it is robust. In public spaces (such as hospitals) it is not robust. It takes a lot of time for the robot to navigate. It is also not safe, unless safety controllers are added.

15:11
Q: What can the navigation stack observe?
A: Sensor data, velocity and position. 
Q: But what can the sensor observe?
A: With ML techniques you can observe aspects of the environment. But without processing there is nothing you can "observe" i.e. figure out what you are seeing.

16:36
Q: Did you have a simulation model that captured the real-world platform? 
A: Simulation cannot capture the real world 100%. One of the deficiencies is in simulating friction, which is a non-linear property of the system. Other physical phenomena such as damping and springs are not fully modeled. 


18:16
We tried to simulate the wheels, the grippers, tasks, as close as possible. There are also no scanners stops for the simulation models out there. 

19:28
Q: During testing in the real world, did you find any bugs that were surprising or interesting? 
A: We always had issues when laser scanners hit something transparent (glass), reflective or bright. In particular, sunlight that came from a skylight would get reflected on the walls. 

21:42
The sunlight causes problems since the laser cannot detect the wall when it is reflecting a lot of light. 

### Section 3
22:22
Q: Can you describe the environment where you would deploy the robot?
A: Industrial spaces, mostly in manufacturing. 
Q: How dynamic would these spaces be? 
A: The environment should not be dynamic, the more stable the better. 
Q: What is the size of the environment
A: It can be a large environment, with laser scanners the robot could get "kidnapped" but that is unlikely to happen

24:23
Q: If you were to describe this environment, what would be the elements that would be present?
A: Machines, racks, desks, flat surfaces (important for 2D navigation).
26:04
A: Walls, door, pillars, seats.

26:47
Q: In the environment, was there something that was particularly challenging?
A: (On top of skylights that let in a lot of sunlight), non-flat surfaces (like inclines). 

28:14
Q: Do you have an occupancy you could show? 
A: Yes. This is a basic environment with an interesting problem. 
30:25
A: It is a simple environment without too many complexities. You can see a small doorway around 800mm [sic]. The footprint of the robot allows it to go through the doorway, but you need to be aligned in order to ensure no collisions. 

32:36
Q: Would you say these problems where unexpected?
A: They were expected once the use case was clear. 

33:03
Q: What other problematic areas can you find in the environment?
A: The map was generated with an algorithm. But a part of the environment was not actually mapped correctly due to incorrect parameters for the algorithm. Without proper parameters some elements of the environment can be not included in the map. For instance, an undetected edge can be the cause of a collision in the future. Building the correct map is a challenge. 

35:14
Q: Can a software solution deal with these challenges? 
A: Yes, modifying the environment is often not possible. a

35:48
Q: What is the impact of the map quality in the performance of the system.
A: It is very important. Some procedures require a lot of accuracy, such as a docking procedure. 
Q: Is it troublesome that a map is too perfect?
A: Depends on the environment where you are using it, in a dynamic environment you don't need a perfect map. 
Q: How would you measure map quality?
A: It depends. For instance in the map shown the edges are not well formed. The quality of the map depends on the quality of the sensors.

### Section 4
38:30
Q: When beginning development, how do you approach testing? 
A: For our case test have already been carried out in the real world, as well as deployment. The simulation package was more for inference testing. 

39:30
Q: How would describe the simulated environment when you compare it to the real world?
A: It was mostly the same. I made a replica of the real world environment so that I could save time and resources using the simulation.
Q: And to which level of detail did you model the environment?
A: To the level where windows where place, but sunglight issues were not possible to replicate. All of the walls were replicated. 
Q: So the robot could see more or less the same readings in the simulation?
A: Yes. And to add: some physical properties of the surface varied in simulation. 

41:18
Q: Did you find it challenging to recreate the environment?
A: Not really, all the tools are available, at least for Gazebo.
Q: What was your starting point?
A: Just the workspace that I saw. 

42:08
Q: What environmental features would you like to simulate?
A: Friction, damping, springs. Also sunlight.

43:04
Q: Any closing remarks?
A: No.

== end of interview ==