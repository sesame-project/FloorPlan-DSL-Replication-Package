# P13 protocol

recording length: 00:31:32

### Section 1
00:23
Q: Have you worked on the navigation stack of a real or simulated robot?
A: Yes, in both.
Q: Can you describe your role?
A: I've been a researcher and a developer. 
Q: Did you develop components?
A: Yes, at one time I developed a mapping approach for navigation. At the moment I integrate components.

01:23
Q: Would you say that the problem of navigation in indoor environments is a solved problem?
A: No.
Q: What are the challenges?
A: For me, the main challenge is that the navigation focuses on the spatial information of the environment through spatial representations, we ignore the semantics of what we see in the environment. It is necessary for more human-like navigation in indoor environments.

### Section 2
02:18
Q: Can you describe in your own words the navigation stack?
A: It's the software component that is involved in moving the robot around the environment. As a software developer, it's the set of components that allow you to navigate around.
Q: What are those components?
A: The mapping, a representation of the environment; a planner, which happens at different levels but gives you a plan; and the control, which executes the plan. You can also have recovery components. These are the four main components

03:25
Q: Which sensor did you use?
A: LiDAR is the most common, also RGBD camera for semantic understanding. LiDAR is more for spatial understanding. In addition you have odometry, and IMU to improve estimates.

04:08
Q: Would you say the navigation stack is robust against the environment?
A: If you refer that it will work in any environment, no. It depends a lot on the environment. For instance, a very large area where the robot cannot see any features, it is very difficult to navigate. In a very small environment with many features that are static, it is a solved problem.
Q: What would you consider as robust?
A: That is plug-and-play, it works in any environment.
Q: What would make a stack robust against the environment?
A: I feel that is not possible to have one solution for all environments. We need different solution and strategies for different environment. A single solution is not possible.

06:22
Q: What can the navigation stack observe?
A: It has to perceive all the obstacles, which it does right now. We should perceive the semantics, for example humans in the environment. With this we can make better decisions.
Q: Which objects can the robot perceive?
A: Right now it should be able to detect most objects, the problem is to determine how to incorporate that into the navigation stack.

07:40
Q: What did the simulation model for the robot platform entail?
A: Just the kinematics of the robot
Q: What else do you simulate to simulate the robot?
A: For me just the components require to make sure everything is integrated. I don't simulate the dynamics. 

08:40
Q: Have you ever found bugs that were interesting or surprising related to the environmental features?
A: You always have issues when you go to the real environment which you can't simulate. 

### Section 3
09:59
Q: Can you describe the environment where you deployed the robot?
A: Hospital, universities and homes.
Q: What were these like? 
A: Hospitals had lots of hallways and rooms. The university is very diverse with lots of hallways, with a lot of glass walls which are hard for LiDAR systems to detect, and also metal walls instead of concrete walls. Home environments were the best environments to navigate around since they were small and statics.
Q: And did you have many features in the hospitals?
A: No, just long hallways.

11:54
Q: How dynamic were these spaces?
A: The hospital were dynamic, but not due to people but due to movable objects. Apart from that it was very static. The universities are way more dynamic.
Q: How does the dynamic aspect affect robustness?
A: It affects them negatively. Current navigation stacks are not very good handling dynamic obstacles.
Q: What were the size of these environments?
A: The hospital was large, but the space you navigate is limited.

14:04
Q: Was there something in the environment that was particularly challenging?
A: Non-smooth surfaces, ramps or stairs can cause problems. People can cause problems as well, because they don't know how react to the robot so they get in the way.

15:44
Q: Was there ever something in the environment you did not expect
A: Not that I can recall

16:13
Q: What do you think are problematic areas? 
A: Areas that have glass or metal, large areas without features, and the top floor where the robot can't see that it can fall down. 

18:00
Q: Which aspects of the environment do you think can cause problems to the navigation stack? You have mentioned already dynamic objects, reflective materials, what else?
A: I would say not knowing what the dynamic objects are.
Q: What type of dynamic objects are out there?
A: Mostly humans.

19:41
Q: Do you think a software solution can deal with these challenges? Or do you need to modify the environment?
A: Most of the time you can't modify the environment, but in general we can of course improve the software components.
Q: Is the solution comes only from software? Or do you need to improve hardware as well?
A: You can improve the hardware as well. Better sensors help, and better computation can help. 

21:07
Q: What do you think is the impact of the map quality in the performance of the system?
Q: You mean in how much agrees with the current environment?
A: yes
A: I think it plays a huge role, it depends a lot on the map. If you can't localize you can't navigate.
Q: Is a noisy map better than a hand-drawn map?
A: Noise works better if it was created with the same sensor. 

### Section 4
22:39
Q: How do you approach testing?
A: Simulation first, only when I have everything running in simulation I got to the real world.
Q: And you have an idea of how your real world platform looks like before you start simulating?
A: Yes. 
Q: You craft the URDF file and setup the simulation
A: correct.

23:45
Q: How would you describe the simulated environment?
A: We try to replicate the real environment, but is very limited. We have only a static world with the walls and objects that make the environment.

24:20
Q: What elements do you think you need to describe the environment?
A: I think it depends on your task. The environment will look different for each task, it depends on what you want to do. But if you want to test navigation the current offer in simulators is enough. 

25:48
Q: What is the difference between the real world and the simulated environment?
A: The simulation is too perfect, and it is relevant for perception applications, you can't test perception applications because they are very different. Also, modeling a person is very difficult.

27:34
Q: Have you every tried to recreate the real world in simulation?
A: I try to recreate something close to the real world.
Q: Is it challenging?
A: It is a huge challenge, but my main goal is to just test the integration.

28:17
Q: What is your reference to recreate a new environment?
A: I use the occupancy grid of the environment, and based on that I build walls. Depending on the use case I add objects.
Q: What type of objects do you add?
A: Depends on the use case, one example was a robot that works in a cafe so we added tables and chairs. 

29:15
Q: What environmental features would you like to simulate but it is not possible?
A: It would be nice to simulate everything that is interesting. I could not simulate people for the case application, because the task depending on the pose of the people. I had a problem that I could not see until I moved away from simulation that was related to the person detection, since I could not detect humans I could not detect the problem.

31:21
Q: Any closing remarks?
A: Not really. 

== end of interview ==