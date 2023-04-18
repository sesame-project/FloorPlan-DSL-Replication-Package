# P6 protocol

recording length: 00:31:53

### Section 1
00:21
Q: Have you worked on the navigation stack of a real or simulated robot?
A: Yes, with both.
Q: What was role in the development process?
A: We develop most of the software. For the simulation we tried to recreate the robot 1:1 with all its elements such as sensors. For indoor navigation I worked mostly with the SLAM algorithm to ensure loop closures. Our goal was to have the autonomous robot to navigate in a way that enable it to explore the environment. 
Q: Were you involved in the simulation development?
A: I was, but not completely on my side. My contribution was to improve the simulator software in some aspects.

02:22
Q: Would you say that the problem of navigation in indoor environments in a solved problem?
A: No
Q: What are the challenges?
A: There are many. The challenges depend on the type of sensors you use. If you only use lasers then autonomous navigation is very challenging, as the 2D laser has limited observability and you can only see objects at a certain level. In one example we had a structure that the laser would not detect that was impossible for the robot to fit. The choice of the sensor is very important. Most algorithms work in 2D, so navigating in a 3D world is challenging.
Q: Can you think of other challenges?
A: Another challenge is about the kind of environments we simulate. For instance we don't simulate dark rooms, as the type of navigation you do is way different. Also communication challenges are interesting, one time I was controlling the robot with a joystick and the commands that were sent are not the ones that were executed. But we don't usually model this. One that might seem trivial is structures on the floor, in one case there was a sharp object in the floor that could harm the robot. There are a lot of aspects of the environment one must consider to navigate well.

### Section 2
06:19
Q: Can you describe with you own words the navigation stack you have worked with?
A: Our navigation stack has a wall-follower task for exploration. We used one of the 2D local navigation components that are available to the community. We used also a mapping component for the SLAM algorithm. 
Q: What were the inputs?
A: The laser mainly, we used three lasers: one in the front, one in the back, and one looking at the floor.

08:08
Q: Would you consider this navigation stack robust against the environment? What do you consider as robust?
A: I would say that as long as it works without us worrying about it. I would not use the word "robust" but the word "practical". Our navigation stack was practical but if by robust you mean that it never fails then it is not robust. 

09:21
Q: What can the navigation stack observe?
A: The changes on the environment, the changes in the position of the robot. If it is based on lasers it receives 2D information.

09:43
Q: What did the robot model entail?
A: It was a 1:1 copy of our robot, with the exact controller, footprint, and the same moves. 
Q: In a standard format like URDF?
A: Indeed.

10:18
Q: Have you ever found bugs that were interesting related to the environmental features?
A: Yes of course. I must say, a good thing to have a 1:1 simulation of the robot in the environment is that you get to catch the bugs before you test in the real world. The bugs we do not find in simulation are not discovered not because the simulation is inaccurate but due to environmental aspects we did not model. We had problems navigating in the dark, and in one time there was a bench and a chair, and it was hard to operate around it. From the cameras you do not know if the information you are receiving is the most recent frame. 

### Section 3
12:13
Q: Can you describe the environment where you have deployed the robot?
A: In a very large industrial-like environment. In this environment there were many stairs, which were challenging for our robot. 

13:06
Q: How dynamic was this environment?
A: It was not that static, there was another robot that our robot was not aware of. Other than that it was fairly static. There was not a lot of human traffic. 
Q: Were these robot autonomous or always controlled by someone?
A: The plan was to run them autonomously, but it was not possible to do so due to some failures with the navigation components and the lasers. One challenge we had was that our mapping component would get confused when the laser encountered curtains, ropes, or strings that are hanging from the ceiling.

14:29
Q: What is the size of this environment?
A: It is an industrial environment, so it was very large with many many rooms. Of course, our test were limited to a zone, that was still very large. Even though it was very large, the SLAM algorithm behaved very good, as the corridors in this environment were so different from other corridors where we have tested the robot. Almost every corridor looks the same, often with not too many features. In this environment there were large but distinct.

16:15
Q: What are the elements that describe this environment?
A: It is not easy to describe as there are many machines around. There were small (but significant) height differences between the corridor and each room, that made it challenging to traverse. It is a large open space with many stairs that lead to different corridors and rooms, with no windows. You have doors and machinery. Also a lot of valves. There are also objects that hang from the roof but if the robot is not tall enough it is not relevant. There were also holes in the floor, so certainly it was a very complex environment. 

19:28
Q: Was there something in this environment that was particularly challenging?
A: Stairs. The robot could loose its balance when going up or down the stairs. The manipulator at the back of the robot could also get stuck in the railing making the robot fall. It is a track robot so it can go up and down the stairs. This was a robot meant for this kind of environment. 

21:39
Q: Was there something that you didn't expect?
A: Yes, the everyday objects I talked about. One time there was a ladder that was slanted on the wall, and for a larger robot it blocked the way. So objects out of place, such as clutter.

23:05
Q: What do you think are problematic areas that you can find in the environment
A: Narrow corridors but it depends on your robotic platform. Our robot was the size of a backpack. Obstacles that are not in the view of the camera.

24:21
Q: What do you think are problematic aspects?
A: The stairs. 

24:50
Q: Do you think a software solution can deal with these challenges or do we need to modify the environment?
A: To some extend both. It depends on your platform. For some robots even if you have a ramp rather than stairs it is still difficult. I would still try the software solution. 3D navigation would probably have helped us deal with our issues.

26:16
Q: What is the impact of the map quality?
A: We had a very nice map quality, we were able to have a pretty nice loop closure.
Q: Do you think a map that is clean than a noisy map?
A: I think the noisy map is better, as that is how the robot detect it. I would assume that the sensors are going to be noisy.

### Section 4
28:00
Q: When beginning development, how do you approach testing? Is it simulation first or real world first?
A: Simulation first. It takes a while until the hardware is ready for deployment. 

28:27
Q: How would you describe the simulated environment?
A: Just a simulated environment that is almost 1:1 with the robot and the environment that is going to be deployed in. 
Q: Not much different from the 3D world and the real world?
A: We don't simulate the environment exactly. We just simulate the walls. The environment is too complicated and it would take us hours to model each detail.

29:22
Q: Have you ever needed to recreate a specific environment or situation in simulation?
A: No, we haven't done so.
Q: And do you think this is challenging?
A: Just time consuming. The environment is very large and modeling is time consuming.

30:08
Q: What environmental features would you like to simulate but it is not possible?
A: I would prefer to have a detail environment in an easy way, or a list of environments that I could use. Depending on the application, I would also like to see the models have either a lot of detail or be very simple. It is time consuming to create environments.

31:46
Q: Do you have any closing remarks?
A: No. 

= End of interview =