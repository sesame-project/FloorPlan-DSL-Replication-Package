# P5 protocol

recording length: 00:43:06

### Section 1
00:26
Q: Have you worked in the navigation stack of a real or simulated robot?
A: Yes
Q: Can you describe your role in the development process?
A: One role was developing the simulation environments, where we tested navigation algorithms. Another was developing a map representation for indoor environments, the goal was to add semantic labels to environmental features, to inform special behaviors of the robot. 

01:22
Q: Would you say that the problem of navigation in indoor environments in a solved problem?
A: Definitely not, even though there are multiple libraries available there are several corner cases in distinct environments with distinct platforms. 
Q: What would you say are the challenges?
A: Navigation stacks nowadays are successful in moving the robot from point A to point B. But one of the main challenges is produce sociable acceptable behaviors in robots that operate in human-inhabited environments, such as hospitals, when navigating. Unpredictable behavior in robots lowers the trust in robots that must operate in this environments, causing annoyance and dangerous situations. Another challenge is the safety of the robot in certain scenarios, since robots have limited perception. They can cause harm to itself or to other elements of the environment. 

### Section 2
04:15
Q: Can you describe in your own words the navigation stack of the robots you have worked with?
04:40
A: I have worked primarily with robots with laser scanners as inputs to a mapping software using open source software. They can generate 2D or 3D maps (such as occupancy grids or 3D point clouds). A localization component uses the maps with the laser data to localize the robot. The output for this component would be a 2D or 3D pose of the robot. Another component is a path planning software that returns a global path plan in your map, and a local path planning component helps you navigate in the local environment. 

06:34
Q: Would you consider this navigation stack robust against the environment?
A: To a certain extend yes, but not fully
Q: What do you consider as robust?
A: For instance, for a robot that is about a meter tall with a laser scanner not so far from the ground, a generated occupancy grid map will not detect overhanging structures (e.g. long tables). This are obstacles that the robot cannot perceive, making their deployment in the environment unsafe. This problem cannot be solved with a single laser scanner, it is a corner case. You have to think of way that allow the robot to avoid this types of obstacles/areas.
08:29
A: On the yes side, it depends on the robot that you have and the capabilities it has. If a robot has a 3D Lidar mounted then it can 3D collisions check. Certain problems can be solved with the right software and hardware capabilities. It depends on the map representation and the capabilities of the environment

09:45
Q: How would you measure robustness?
A: We don't have a single measure of robustness, we can have different degrees of robustness categories. We can have robustness in safety, task completion. For the previous example, we can quantify it by counting the times the robot collide with an object that is undetectable. Another scenario is passing through narrow doors, this is often difficult for the robot with a high chance of failure. 

11:47
Q: What can the navigation stack observe?
A: The can perceive whether a region is space is occupied or not. You don't know if the perceived obstacle is a wall or a door. All they have is whether a certain space if occupied or free. With this information the robot can plan whether it can reach a certain space. Success in reaching the goal is not guaranteed, e.g. narrow spaces are difficult to deal with. You can add semantic information to specific regions of the occupancy grid to add information on unsafe regions. That can help the robot in reaching its goal.

13:35
Q: Do you have a model in simulation that captures the real world platform?
A: Yes. We have one model using of the most common description frameworks. In addition, we have model on a 3D engine and physics simulator that is not tailored to robotics, so it is missing a lot of sensors. 
Q: What does the model entail?
A: It is composed of meshes for representing the robot, also a model for the collision boxes, the transformation between the different components (from the wheels to the base), sensors (meshes and plugins). 

16:17
Q: Did you perform test in the real world?
A: Sometimes yes
Q: Did you find bugs that were related to the environmental features?
A: In my personal experience, no. But colleagues had problem with differences in the behavior of the sensors between the real world and the simulated. The real sensor had more noise. Also, in one scenario we replaced one sensor with another, since their performance was different the localization component was not able to localize the robot, failing the scenario.

### Section 3
18:14
Q: Can you describe in your own words the environment where you would deploy the robot?
A: Most of the time the experiments that I performed were on a public infrastructure building. I have also worked on a simulated hospital, with multiple rooms and doorways of different sizes. 
Q: How dynamic would you say it's this place?
A: Not dynamic. Nothing would change. But in another project some colleagues of mine had trouble in an environment that would change occasionally.

21:26
Q: Which concepts do you think you need in order to describe this environment?
A: The main critical elements are: doors (narrow), furniture (and different types of furniture), walls, and low hanging structures, such as stairs.

23:20
Q: What do you mean by "walls as long as they are visible"?
A: A corridor that is completely made of glass, then 2D, 3D, and even cameras will not detect the walls. If the robot cannot see the features then it will collide with them. In addition, if you have a piece of furniture that is next to a wall, the furniture will be mapped as a wall. For some furniture it doesn't matter, but tables and chairs can move and can cause issues. 

24:50
Q: Was there something in the environment that was particularly challenging?
A: Mostly narrow corridors. 

25:48
Q: Do you have an interesting map that could be problematic to a robot?
A: I can show you some of the things that I have talked about. 
27:34
A: Here are four scenarios, and we have talked about three of them (glass corridors, narrow doors, overhangs/low hanging structures). 
28:29
A: In this scenario, if you map a room with an elevation change, the robot may not be able to detect this elevation change. So when it tries to reach a point in the raised platform, it will fail. With some semantic information you can tell the robot the location of a ramp, so that it successfully navigates in this scenario.

29:56
Q: Was there anything you didn't expect in the environment that caused trouble for the robot?
A: glass corridors, narrow doors, overhangs/low hanging structures, height differences. 

30:41
Q: What do you think are problematic areas for the robot?
A: It depends, for a robot that is passing by tight corners, it might happen that the robot cannot see a human around the corner. With enough velocity, it might not be possible to slow down when the human is detected to avoid collision. Another challenge is when a robot is trying to get into an elevator. The problem is the reflective property of the elevator frame, which causes incorrect readings for the laser scanners. So the robot cannot enter the elevator.

33:22
Q: Would you say a software solution can deal with these issues?
A: I'm in favor of avoiding modifying the environment. Software solutions are possible through different techniques, such as adding sensors or adding semantic information to the space representations.

35:05
Q: What is the impact of map quality in the performance of the system? What would you say is map quality?
A: One metric to measure the map quality is to see how many tasks can it complete with it. How useful it is to solve certain kind of tasks.
Q: Would you say that a map that is too perfect is troublesome for the robot?
37:01
A: The map that is perfect would cause worse performance. In some cases, such as a very long corridor without features, the noisy map will perform slightly better.

### Section 4   
37:58
Q: How do you approach testing? Simulation or real world first?
A: Ideally it should be simulation fist, but in our case was the other way around. By the time I joined we had a real platform that was already working. We wanted to see how changes in the environment affected the robot, and that is why we moved to simulation.

39:00
Q: What would you say are the biggest differences between the simulated world and the real environment?
A: I can't think of any right now.

39:36
Q: Have you ever tried to recreate a specific environment of the real world in simulation?
A: Yes, but not photo realistically.
Q: Did you find this challenging?
A: A 3D non-textured model would not be that difficult. For walls and doors only it would be easy. If you add objects in the environment and dynamic actors, it might be more difficult.

40:29
Q: What would be your starting point?
A: It still would be to get the fixed elements of the environment place (walls, doors, static furniture), and then I would add furniture that it can move. So a starting point would be a grid map/floor plan, and then work from that. 

41:45
Q: Which environmental features would you like to simulate?
A: Lighting is one of the main issues if you wanna use VSLAM map, model of human agents are difficult in our standard simulator. I also wanted to model doors that open and close. It is interesting to simulate if the robot can get through certain doors.

42:42
Q: Any closing remarks?
A: No.

== end of interview ==