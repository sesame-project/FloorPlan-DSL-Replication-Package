# P9 protocol

recording length: 00:36:27 & 00:29:47

### Section 1
04:49
Q: Have you worked on the navigation stack of a real or simulated robot?
A: Yes
Q: Can you describe your role?
A: I worked on a project regarding in multi-robot navigation in narrow environments, I worked on the path planning of a robotic fleet. LAter on I worked for a project about intralogistic in hospital environments, we work on the high level planning aspect of path planning, no motion planning. I was also involved in the navigation component of some robots, were I developed high level path planning.

Q: How long have you worked with the navigation stack?
A: I would say three years on one project (at a high level), and nother 3 years in another porject.

06:58
Q: Have you performed navigation test in the real world?
A: Yes.

### Section 2
07:16
Q: Can you describe with your own words the navigation stack of one of the robots you have worked with?
A: There were several layers, I worked in the planning part, that consisted in choosing the order of the places the robot would visit to achieve its tasks. The goal was to go to location A to pick up and item, take it to point B, and go to point C. The environment was very dynamic and multi-level, the robot had to use elevators to move between floors. The highlevel layer would need to decompose into smaller middle level path plans. The middle level path were decomposing the goal into smaller sub goals, and the environmental representation used in the project was made so that the plan had incorporated traffic rules, it was important for MRS since you need to coordinate to avoid collisions.
09:55
At the lower level there was a need to follow a trajectory. The interesting bit is that the robot needs to be able to reconfigure its kinnematic chain as it can pick up carts which changes the movement constraints. 

11:17
Q: What would be the inputs and outputs of the navigation stack?
A: there was a component that included semantic information in the occupancy grid, and topological subdivisions. As inputs we had the original occupancy grid, the environment representation (with semantics), the tasks (location to pick up and deliver), we had a task planner, the state of the robot, and the current location. As outputs we had feedback about when the robot reached a specific position to track progress, we also had feedback about attempts (e.g. to reach a location), and a final feedback on whether or not the nav stack was able to reach the goal.

15:10
Q: Would you consider the navigation stack as robust?
A: Yes, at least on the environment where we tested
Q: What do you consider robust?
A: Robust means that it was possible to conduct many tests without failures, so the failure-rate was low and it was possible to conduct tests for longs periods of time without failures. I must say that there were many iterations to reach this point. It also required changes to the environment model on top of iterations of software. 
16:39
Q: What makes the stack robust?
A: This was part of the software stack developed through the project but wasn't exclusive to navigation. There was a mechanism to escalate failures from lower level components to higher level components. If you had a failure on the sensor, then the component that depended on it would get notified, for instance localization, and the recovery action was performed. If it didn't worked, it would get scalated to the next level. 

19:35
Q: What can the navigation stack observe?
A: It depends on the type of sensor and where they are positioned. One robot had one laser scanner at the bottom, maybe at 30cm from the ground, it also had a camera at 1,4m off the ground. For navigation we used the laser information, and it gives you information that can only be seen at that height. So for a table it only sees the legs of the table, it doesn't see the surface. To prevent crashes, we would modify the occupancy grid. In the environment model there were subdivisions, and part of the semantic information was regarding forbidden areas. For example: stairs, and certain doors. But we didn't use this to deal with obstacles. 
22:45
A: Other thing, sometimes navigation is solved on a 2D level, depending on the height of the sensor sometimes objects are detected. The wall gets detected fine, but we had trashcans attached to the walls that were not detected because they were too high. So the robot assumes that the space is free. We also can use point clounds to detect them, but they are more computationally expensive, you have to deal with much more data. Even then, you still have blind spots. For the navigation you choose a solution that is particular to the environment or application. 

26:00
Q: Do you have a model for simulation that captures the real world platform?
A: Yes, the model for simulation was always slightly simplified. 
Q: What did it entail?
A: Simpler than the physical platform, it was used to test navigation. We had the physical footprint of the robot, the wheels, the kinematic model, the laser scanner, and the normal camera. The simulation model was not able to capture all details.

28:27
Q: Did you found any bugs that were interested related to the environmental features?
A: Yes. we were testing mostly in two real world environments. One was the target environment, and another was very controlled. The scale was very different, but the both of them were large. So we saw different behaviors in both. one example is that tThe out-of-the-box ROS planner can't deal with long distances. The other one is the dynamic aspect of the target environment, which changed everytime we went there. This made localization break, as the occupancy grid is static and made from information captured at a certain height. The environment changed from hour to hour. There was no way to capture this dynamic aspect. The environment model developed for the project was based on the floorplan of the building, but they were too "perfect": no noise and sometimes different from the real world. 

== end of recording 1 ==

### Section 3
00:02
Q: From the perspective of the navigation stack, can you describe the indoor environment?
A: It was a huge space. There was an extremly long hallway. 
Q: Did this space had many obstacles?
A: Yes, there were many containers and carts that get moved around. There were also tools to moved stuff around, and parked next to the wall. The parking poition for these would change every hour. There were also humans moving around the environment but these were not that troublesome. Also, the state of doors changes the paths you can follow. There are times were there are multitudes of people that are crowded in a certain area. 
06:17
Q: Can you think of other environmental aspects that are challenging?
A: The problem with the hallway was that the changes made it difficult to localize, because features do not match. We had issues localizing in places where everything looks the same, because the error accumulates very fast. Open spaces are also troublesome for a similar reason, there aren't many features to localize oneself with. We also had obstacle detection problems with the mirrors of the elevators.
10:00
At one point in the target environment had a thin metal strip for decoration that the sensors could not detect. And also the common glass walls or dividers. 

10:54
Q: Where these unexpected?
A: Glass walls problems are known, the metal strip was a surprise, and the dynamic of the environment was also a surprise. We did not expect that level of change. The elevetor problem we sort of knew. 

11:57
Q: Can you think of other aspects that can be problematic?
A: Light, depends on the sensor but navigating with too litle light is problematic. If you rely on communication for completing the task, then this can also be a problem depending on the network. 

14:05
Q: What is the impact of the map quality in the perfomance of the system?
A: It is tightly coupled, very noisy map can affect negatively the performance. There might be areas that the robot cannot go through because it thinks there is an obstacle. It is also important for localization. Too perfect does not reflect reality, so it might not be able to localize. Very perfect maps tends to increse the map between plan and execution, you can find a plan in the perfect map but when executing you can find that is not possible. 

15:47
Q: Out of the two maps here which one is better?
A: I think the noisy map. In my opinion, you have some noise but it is color coded in grey so that it can be changed online. 
Q: How would you measure map quality?
A: I'm not sure if there is a metric to do that at the moment. When mapping you have an idea of the error that the robot perceived, that could be useful. Another way is by looking at the performance of the robot, if its good enough it will perform good.

### Section 4
19:10
Q: When beginning development, how did you approach testing? real world or simulation first?
A: By parts, because of the location we did not test often in the target environment. We would test more in a control environment but in the real world. We introduced simulation after, because you need to create the simulation environment which is not easy. It is also not easy when the environment is very large. You can also use the occupancy grid to generate the environment, but you need a really good map without noise. This however will not take into account the material of the wall, and will assume that the wall/material of the wall looks the same for all. We had the simulation but it was scaled down. The simualtion was too perfect with flat walls. We had a simulation environment for the controlled environment first, we didn't have all the data to model the target environment. 
23:37
There was also inclination in the target environment, and when we built the map it taking into account the inclination. 

24:43
Q: Would recreating the target environment be a challenge?
A: Yes, would by having the information it would be easier to start. We would have at least a basic version of the environment, maybe with some assumptions such as flat walls. But at least the basic structure of the building would be there, and this alone would be helpful. 

25:45
Q: Did you ever try to recrate a problem in simulation?
A: It depends on whether or not creating the simulation was going to add a long term benefit. In most cases the answer was not. It required too much effort. Testing in simulation were too small in comparison with test in the real world. In the real world you get to see the real reaction.
27:00
It would have been nice to test some things in simulation. Investing time for creating the simulation must bring a lot of benefit to the project. It would have been useful because we needed to test more was the MRS aspect. 
28:50
"Either you make it work in simulation or you make it work in the real world"
If we had the resources, simualtion could have been useful at an early and later stage of the project.

== end of interview ==