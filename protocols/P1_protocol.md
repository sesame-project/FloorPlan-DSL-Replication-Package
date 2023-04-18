# P1 protocol

recording length: 00:47:00

### Section 1
00:32
Q: Have you worked on the navigation stack of a real or simulated robot
A: Yes. With both.
Q: Can you describe your role in the development process?
A: I was tuning the parameters of move base for the real robot for at least 6 months, to improve the robot navigation. By testing them on the real robot, observing the behavior, and modifying the parameters. Most of the problems with the YouBot navigation back then were due to a bad tuning of the parameters, plus some strong non-well understood assumptions made by move base (for example that they consider the robot as a circle). Many years later I also implemented from scratch some components of the navigation stack, such as the local, global planner, and differential drive kinematics, which is about mapping the body velocity to wheel velocity and computing the odometry.

02:31
Q: Would you say that the problem of navigation in indoor environments is a solved problem?
A: It is considered to be solved in the research community, but I would say it is not entirely solved. The main issue to improve is the motion planning problem. The current implementation of many global planners assumes that the robot is a circle, and this is a strong assumption since the orientation is not computed. While this has not been overlooked by the community at the theoretical level there is little to no implementation available around it (there is no solid bridge between move base and OMPL for various reasons). I believe there is plenty of room for improvement. For the localization, we always need to give it a pose estimate so that it can begin localizing, so it is not truly autonomous. While a service call exists to spread the particles in a random uniform distribution all over the map (something which is supposed to solve the problem) in reality it does not solve the (global localization) problem in a reliable manner.

### Section 2
04:35
Q: Can you describe in your own words the navigation stack?
A: First you need to make a map through SLAM, because this is a chicken and egg problem well covered in literature. Once you have a map you receive a goal of where you want to go, and assuming an occupancy grid map approach, you need to solve a global path planning problem typically solved with search algorithms such as A* or Dijkstra. Once you have a global path plan in hand you need to follow it with a local planner. There are several local planners available that are able to provide a solution. Depending on the kinematics of your base you generate the best trajectory that the robot executes next. In Dynamic Window Approach (DWA) you first generate multiple random samples in the robot velocity space (e.g. Vx, Vtheta for a diff drive robot), then forward simulate them for a small amount of time using a robot model, then score the candidate trajectories with different weights, like path or goal bias. Finally you pick the trajectory that scored best and send it to the controller for execution. These is the basic explanation behind move base, however, you also have some mechanisms in case something goes wrong so that you can recover from the situation. For instance one of them is to rotate the base and try to clear the costmaps by gathering more readings from the sensors (typically lidar). Another one is to consider the costmap obstacles as repulsive points in a vector field, and the sum of the repulsive vectors gives you the direction to move to get away from obstacles, this proved to be very effective in practice.

10:11
Q: What were the inputs for the navigation stack?
A: The desired robot pose which is expressed in a global reference frame (typically map or odom frame).
Q: What about sensors?
A: The canonical sensor is the laser scanner. This is the standard for navigation, mapping, localization and obstacle avoidance, I've also worked with depth cameras and simulated sonar sensors. Some robots like the PR2 also tilt a laser scanner periodically to construct a pointcloud. The idea is to use the 3D point cloud to construct an octomap that later on is projected to 2D, so detection of obstacles considers 3D obstacles but in the end the navigation is performed in 2D to keep the computation simple.

12:28
Q: Would you consider the navigation stack is robust against the environment?
A: It depends on your environment. On a simple environment that you control yes, but a challenging environment I would say no. In a real environment, objects that cause problem to the navigation are for example: objects that are located at a different height with respect to the laser scanner. Also, reflective objects such as metal or glass are a problem. Very crowded environments are also troublesome. Also, depending on the shape of the robot, some locations are harder if not impossible to reach. Also worth to mention are the narrow passages which are particularly challenging.

13:44
Q: What can the navigation observe with its sensors?
A: Any material or surface that is made out of carton, wood, plastic, metal (although noisy), and others?. Some materials are less noisy than others. One that I'm unsure about is how the laser would respond to black coloured materials. Like we said before, lidars can only see obstacles on a 2D plane and not even 360 degrees, but rather a more limited FOV, depending on the lidar specs and the place in the base where is mounted. For our robot we had to place 2 lidars at 90 degree FOV and still had a blind zone at the side of the robot.

14:53
Q: What did the model of the platform entailed?
A: Simulation assumes that everything is perfect, which is reflected on the URDF file. This is not true in real life, there are always deviations from the drawings due to manufacturing imperfections which are addressed in a process called calibration. But more important is how you simulate the model, many of the available simulation models are very high level, so they do not simulate the wheel movement but rather they apply a force to the entire robot. Depending on where you apply this force, you can get sometimes weird behaviors; especially when you collide with something. The weird behavior stems from the simplifications made to the motion models, which are implemented like that to simplify the code as well as to speed up the computation and to consume less resources.

18:51
Q: Did you ever find a bug that was interesting that was related to the environmental features?
A: The canonical (on a real robot) one is wheel slippage, there is no perfect friction with the floor. Sometimes there is a different friction coefficient between the floor and the wheel, and depending on the wheel slip you have a mechanical fault. You fix it with some localization algorithms, to make it more robust. Another bug is related to the pose estimate, in one situation we got confused because the rooms where very similar and gave the wrong pose estimate to the robot navigation. The result was the robot colliding with the table in front of him. Last, I insist on the partial observability, the issue is that depending on the environment many times there are small objects (or big table-like objects) which are not visible by the lidar but instead you only see the legs.

### Section 3
20:30
Q: Can you describe the environment where you have deployed the robot?
A: We have deployed it in a laboratory environment, where we had platforms made out of aluminum and plastic with different heights. There were no people walking around (during a specific situation), but our robot was able to navigate between people even without a social layer. Another environment was a home-like environment, there were narrow passages that were challenging. The narrow passage I would say is one of the most challenging areas for robots to navigate through. In another project we conducted experiments in a retirement house real environment at a slow speed, in case of problems we could manually override the robot with teleoperation.

Q: How dynamic were these spaces?
A: I would say not much. Extremely crowded environments can get you lost very quickly because you only see a lot of human feet around. There was one time when multiple robots were placed in the same area, and this was more dynamic, the robot coped well to our surprise. There are two points of view of dynamics: obstacles and people. Obstacles that are not known to the robot at the time of mapping are also considered dynamic obstacles. Unknown obstacles were part of the robot's environment, and we had to deal with them regularly, the robot was almost always able to do it without problems. We did not dealt with people that much. By the way: something to consider, depending on the position of the lidar, sometimes you would not even see the complete foot of the person but rather form the ankle and up, so basically a pair of cylinders, so you would obviously collide with the metatarsal or phalanges.

24:06
Q: Which elements do you think you need in order to describe the environment?
A: Platforms were the main element, maybe some machinery, like a conveyor belt or a rotating table. Tape was another element, which we had to detect to avoid crossing it. This was not detectable by the laser, but instead we used a rgb camera mounted on the robot arm. Sometimes an object can become an obstacle (e.g. if dropped by the robot gripper), and if the object is very small then it cannot be seen by the robot lidar and can potentially become a hazard to the wheels.

26:25
Q: Was there something in this environment that was challenging?
A: Detecting the tape was challenging. Another issue was with the swedish wheels of the robot which generated lots of vibration. We were careful in building the robot mechanical additions robustly, e.g by 3D printing supports for the laser scanners later on attached via screws, such that the vibrations didn’t became an issue.

28:13
Q: Was there something in the environment you did not expect?
A: In one situation I would say no (apart from objects accidentally dropped to the floor by the robot), in general the environments we worked on were controlled and static, even if they did change the layout of the space. Sometimes the platform material changed but it didn't caused much trouble. In another situation we had to perform a following people task, where you are pushed to uncontrolled environment with many people. The main problem is that the laser scanner does not have full observability. For that we added more sensors, but even then is hard to get full observability, we still had a lot of blind spots.

30:52
Q: What type of areas do you think are problematic?
A: I would say go to 3D poses in the environment, talking about 3D navigation. Motion planning in 3D is more challenging. The robot footprint shape is also important, if it's close to a circle then is ok, but the more different to a circle the more challenging it becomes to the navigation stack.

32:49
Q: Can a software solution deal with these challenges?
A: Yes definitely. What needs to be done is to develop a motion planner that takes into account the orientation of the robot base. Additionally you could incrementally build some memory of the environment potential collisions around you. Move base to some degree does this with the costmaps.

33:15
Q: What do you think is the impact of the map quality on the performance of the robot?
A: The quality of the map mainly depends on the map resolution configurable parameter, it does have an impact because it determines how close you can get to the objects or walls, but at the spend of computation, this is: is more expensive for the PC to work with a higher map resolution.
Q: Would a map that is noisy perform better than a "perfect" map?
A: I think the map taken by the robot will perform better. Hand drawing can be tricky because you need to consider the slice of the world the robot can see. On the other hand a map taken by the robot which is later on edited by an expert user would be best, in fact we were doing exactly that in one situation.

### Section 4
36:50
Q: How do you approach testing? Simulation first or real-world first?
A: I like to work with the real world better. The simulation is not that accurate, or not accurate enough to represent most situations. Most of the effort was directed towards the real robot. However, due to the COVID-19 pandemic, we decided to invest more time to make the simulation better. I now work mostly with the simulated robot.

39:13
Q: How would you describe the simulated environment?
A: The simulated environment is a list of (sdf/urdf) models that are imported by the simulator, the models typically consist of visual, collision, inertia properties. CAD models can provide with the geometry and collision, for other properties the inertia tensor needs to be expressed, alongside the mass, etc. Apart from this list of models, you have general simulation properties such as gravity, friction, wind, etc. Another important aspect is the rendering, it is important for simulation of the perception modules. For my application low graphics is enough however nowadays photorealistic rendering can be useful to generate synthetic training data that is then later on transferred to the real system with ML techniques such as domain randomization.

42:35
Q: Have you ever recreated the real-world in simulation?
A: We did it once with one specific environment.
Q: Did you find it challenging?
A: Not really, just time-consuming.

43:10
Q: What environmental features would you like to simulate but are not currently possible?
A: Movement of plants, although not needed. The main thing that I would like to simulate is a person walking around the environment. I've seen some examples but I'm not sure how easy it is to use. I would like to be able to just give some navigation goals (like you do for the robot) to the human, and for the actor to move to the spot in a realistic way. Maybe also use multiple humans in one environment. Another thing would be to be able to simulate humas in a better way to be able e.g to hand over tools to him, etc. This would greatly help to try HRI algorithms in the simulator.

45:03
Q: Any closing remarks?
A: I've missed something about the hardware, I forgot to mentioned the IMU (inertial measurement unit) that is used by components to help localization. Also, in another robot we had two ultra-wide band modules available in the robot base to serve a sort-of indoor GPS system. With two UWB sensors you can compute the robot orientation. Additionally we also tried WiFi localization as part of a course exercise. These sensors can potentially be inputs for navigation, even a RGB camera alone could be used with visual slam and visual odometry approaches, however I have never worked with such approaches.

== end of interview ==