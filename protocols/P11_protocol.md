# P11 protocol

recording length: 00:42:53

### Section 1
0:33
Q: Have you worked on the navigation stack of a real or simulated robot?
A: I would say I worked with a navigation stack, not on. Navigation is not my field of research.
Q: Can you describe what role you had in the development process?
A: In general, I was doing tests with the navigation stack. My role was to test experimentally the navigation stack and evaluate its impact on components I was developing. Also adapting my components to the specifics of the navigation stack. 

01:52
Q: Would you say that the problem of navigation in indoor environments is a solved problem?
A: Absolutely not, at least at the environments we worked in (a university and a hospital) definetly not, we had lots of challenges.
Q: In general, what are the challenges for the navigation stack?
A: The biggest one we faced was localization, it was unreliable in general. In certain parts it was reliable but in another our tools (which were standards) were not performing well. Issues such reflections affect localization, and then navigation won't perform well. Also sensor choice was difficult, we tried many and none seem to be a perfect solution. We even had localization issues on a small scale, for instance when the environment changes a little bit there will localization problems. This is potentially because we used standard tools, which could possibly not be the best one. Maybe some other algorithm performs better. There were also issues with maps, their size and their type. The navigation itself had issues, for instance incorrect parametrization which leads to estrange behaviors. Maybe it is a solved problem for better constrained environments, but in general no.

### Section 2
06:09
Q: Can you describe in your own words the navigation stack you have worked with?
A: There is mapping, we worked with a traditional map server with some custom map servers. Also, there was a different type of map in another project which added semantics. For localization we used standard tools such as AMCL or variants, and for navigation itself I worked with the standard packages, but also worked with custom algorithms. On the hardware side, I worked with different robots, but most of them were omnidirectional and used a 2D laser scanner. Sometimes it also has 3D Lidar lasers and sometimes we used a RGBD camera. 

09:13
Q: Would you consider the navigation stack robust against the environment?
A: Not fully, depends on the environment. Localization is affected with material reflection, so I would not say that localization in general is robust. The navigation depends on the stack. I would consider robustness (for the navigation) to avoid obstacles that come into view, and even minor changes in the environment. Major changes in the environment is difficult for all software stacks. In the end it depends on what kind of changes in the environment we are talking about.
11:04
A: And as I said, reflection from glass is problematic. From my experience that would break the nav stack that I have worked with. Dynamic obstacles are also a problem, but it really depends. 

11:58
Q: What can the sensors detect?
A: A 2D laser can detect basic geometry information, parallel and perpendicular lines. A 3D lidar is able to detect more, it can detect planes, objects, even people. Then there are cameras that can, with a processing algorithm, detect anything. Depending on the sensor the navigation stack must be adapted to process that information.

14:10
Q: Do you have a model for simulation that captures the real world platform?
A: Yes, a URDF model always is use to represent the robot. 
Q: What does this model entail?
A: Personally I have not written one, but it usually represents the platform at whatever accuracy you require. I have worked with simple models where the robot is modeled with geometric primitives, but I also have worked with a more sophisticated mesh. Most of the time I have worked in simulation, I have worked with a laser. 

15:58
Q: Did you ever find any bugs that were interesting that were related to the environmental features?
A: I can't recall a case at the moment. 

### Section 3
17:12
Q: Can you describe the environment where you have deployed the robot?
A: A university environment, where most of the tests have been performed. Also in a hospital. I can think of other environments but I have not performed lots of test there.
Q: How dynamic are these environments?
A: Very dynamic, in terms of people. The hospital was very dynamic in terms of people and objects that were moved periodically, with vehicles driving around. The university was mostly dynamic in terms of people, with most objects staying in a place. It depends on the environment.
Q: How big were these environments?
A: It depends on your definition of large, but both were quite large. The university had a few hundred meters between corners of the maps, and the hospital was even larger. More than 500 meters, considerably large.

20:24
Q: Which elements do you think you need in order to describe these environments?
A: You need to describe the elements you want to be robust against. You don't want to describe all aspects, but you want to describe the walls, certain features that can help you with localization, particularly in environments that change often. You want to describe parts of the environment where you know there is some invariance. Any modeling has to consider this. 
Q: Which elements do you think are relevant to your application
A: Considering the hospital, you want to have a model of geometric entities (walls, doors) but also some model of the dynamic elements. If you want to help you localization you can model distinct parts of the environments, you do this naturally as a human.

23:36
Q: Was there something in the environment that was particularly challenging?
A: The university had glass doors, and was the cause of most of the issues. In the hospital there was a lot of metal, which causes misreadings of the laser lidar. There we also needed to use a elevator, which has lots of challenges. Also, narrow corridors are challenging, but it is very environment dependent.

25:09
Q: Do you have a map that you think it's interesting?
A: I don't think there are interesting but I can show you one. 
= we moved to another question until the interviewee found the map =

27:03
Q: Was there something in the environment you did not expect that was troublesome?
A: I guess in the university nothing, but in the hospital until we got used to the environment, everything was unexpected. We had to study the way people moved, the way doors open/close, and dynamic elements. You have to see in the environment how the people work in it. There were several things we had to learn. 

== back to the map == 
A: In this context we navigated from a delivery area through a huge corridor to another area with narrow corridors and an elevator. We had challenges in areas with lots of metal objects. The corridor changed constantly because items were placed in it. And in the narrow corridors it was difficult to move because the robot's footprint was almost the same size as the corridor, so movement was tricky. Turning into the elevator was also difficult. 

30:40
Q: What do you think are problematic areas?
A: Narrow passages/corridors where the robot doesn't have a lot of space to move around. The types of materials in the environment (specially reflective such as metal and glass). In certain environments doors can be challenging as well because they open and close constantly.

31:51
Q: Do you think a software solution can deal with these challenges?
A: I suppose that modifying the environment would make things easier, but it depends on the application if its acceptable. If it's not acceptable a software solution can also deal with the issues but it's trickier. Changing the environment can make localization easier, but if you have to deal with the issues on software you need to take many aspects into account. It can be done, but it is harder and requires a combination of models and algorithms.

33:39
Q: What do you think is the impact of the map quality in the performance?
A: Huge impact, specially when you use a 2D laser. With an occupancy grid the map quality can make or break the navigation, even small changes in the environment can cause failures. 

### Section 4
34:45
Q: When beginning development, how do you approach testing? Simulation first or real-world first?
A: For me it's really real-world. For several reasons, first using/setting up a simulation takes a lot of time, you have to make sure that what you want to test it's representative of the real world. For me it is not worth it most of the time.  But in the context of navigation simulations are more helpful than for other applications. 

36:28
Q: How would you describe the environment for the simulation? What is different between the real and simulated world.
A: A least with the test we performed in simulation did not include glass materials, it is usally a simplified version of the environment. You place walls, normal walls, even when you have glass walls in the real environments. Also dynamic obstacles are not added to the simulation, so it's really simplified.

37:30
Q: Have you ever tried to recreate a specific environment in simulation?
A: Yes, smaller parts of one of the environments. But described in a geometric aspects mostly, so the walls. 
Q: Was this challenging?
A: Not really, once you do it a couple of times you are aware of what you have to take into account and get used to the tools to do it. it is also easy to set up dynamic elements to the environment. In the geometric level it is not challenging.

38:52
Q: What is your reference for the geometric level?
A: For geometric information is the floorplant, to have the dimensions right. But we don't develop high fidelity versions of the environment. 

40:09
Q: What environmental features would you like to simulate but it is currently not possible?
A: The environment itself it is not that interesting on its own. Ignoring materials, you can introduce dynamic obstacles, not just random movement but modeling realistic behavior. Doors that open/close. So movement that is grounded in the real world. That would be good to have. You test in the real world because it is exposed to dynamic elements that are hard to simulate.

42:24
Q: Any closing remarks?
A: Not really. 

== end of interview ==