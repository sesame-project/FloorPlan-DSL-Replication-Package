# P2 protocol

recording length: 00:42:40

### Section 1
00:22
Q: Have you worked on the navigation stack of a real or simulated robot before?
A: Yes. With both.
Q: Can you describe your role in the development process?
A: My role was integrating all the components involved in the navigation process. This included the sensor drivers, the SLAM algorithms, navigation action servers, job scheduling, and user interface. So really the full pipeline from the user's command to the robot execution. I also was responsible of developing some of these components.
Q: Were these components developed by you or were they already available?
A: Most of them were available, we focused on using what was out there.

02:09
Q: Would you say that the problem of navigation in indoor environments is a solved problem?
A: I would not say that is solved completely, there are unexpected situations that can occur. I have not seen an approach that is prepared to deal will 100% of possible situations, there is still a lot to improve with the navigation stacks that I have used.
Q: What kind of situations do you think are troublesome?
A: A Laser scanner that is in an environment with glass walls. It is common in spaces such as offices and universities. These element create artifacts in the readings of the lasers due to the refraction of the material, so they are not perceived correctly as solid objects. You also don't sense them as "free spaces", you perceive them as obstacles that are not there. But this situation is present only for laser scanners. 
04:28
A: After the mapping process, if the environment changes and the robot is not actively mapping all the time, over time this introduces enough differences that the map that the robot has does not represent the environment anymore. 
05:16
Q: Is that very common? that the mapping process is performed once?
A: It's more common to map occasionally, not just once but also not constantly. Probably after significant changes to the environment are made. 

### Section 2
06:24
Q: Can you describe in your own words the navigation stack?
A: From the base you have a robot that has sensor and wheel actuators. The robot sends the sensor information to a localization module, possible a SLAM algorithm, with sensor fusion or Kalman filter beforehand. When the sensor information reaches the SLAM module, you get localization for the robot. With a localize robot you can finish the loop by giving a goal position for the robot to move. There is a module that is able to read the robot's position and produce the velocity commands to reach the desired position. Overall this is what makes a navigation stack. 

08:09
Q: Would you consider the navigation stack robust against the environment?
A: Probably not complete robust, since the structure is very basic. It would be more robust if you have multiple SLAM algorithms (such as a backup SLAM module) for when the sensors are not good enough. There is room for improvement. With some higher level information, such as semantic information, can make the navigation more robust. 

09:16
Q: What would you consider as robust?
A: I would say that a navigation stack that uses semantic information would lead to more robust behavior, even if this introduces more processing. In addition, using sensors can increase robustness.

10:08
Q: How would you measure robustness?
A: I would measure it by trying challenging scenarios, maybe introducing different test. Create a simple environment for a test, such as a static environment, and make it more complex by adding dynamic obstacles. Then we evaluate if the navigation stack can successfully complete its tasks. Then your qualitative measure of robustness would be knowing if the navigation stack can complete its task in a challenging environment.

11:34
Q: What can the navigation stack observe?
A: I would say the most important thing is the robot position. The navigation stack is observing the robot position through the sensors. 
Q: What could you say that the robot can perceive?
A: That would depend on what sensors are you using. But mainly distances: an odometry sensor is able to perceive the distance the robot has moved, a laser scanner reads the distances to solid objects, a camera can perceive the distances to landmarks. So in general the robot can perceive distances and landmarks.
Q: What makes a landmark distinct? For a laser scanner.
A: The shape of the object being sensed. One thing that I have seen for a different part of the navigation stack is shape detection. You can use the shape as a reference, you can say that a landmark is a shape with a certain size. For cameras you can use the uniqueness of an object as the landmark, you can also use bitmap patterns as landmarks, and even visual odometry; but mainly pattern matching.

15:34
Q: What did the robot model in simulation entailed?
A: What we normally used in simulation was a differential robot, it has simulated motors with odometry readings, it had also virtual laser scanners. That was mostly it, the simulated robot could operate in a 3D environment. 

16:14
Q: Have you found bugs that were related to the environmental features?
A: Yes. The situation about the glass is one. Something similar happens with partially translucent panels such as Plexiglas, those also generated artifacts. It meant that in the map there were obstacles that were not there, not even following the shape of the glass.
Q: Was this because the panel was reflecting the laser beam or because the panel let the laser through?
A: My guess is a little bit of both. I was able to see through them but I also got some obstacles around them.

### Section 3
18:38
Q: Can you describe in your own words where you would deploy the robot?
A: Most of them have been office environments, where you had not a lot of variations in altitude of the floor. So for the most part no ramps or stairs were present. The floor was carpeted or with normal title, and we didn't have trouble with them. Most of the walls were solid, and the most narrow corridor was at most 2 meters, so a person could walk (with the robot on the corridor). The doors would be 80cm wide. 
20:03
An offices tends to have a lot of chairs and tables, which can be problematic because depending on where the sensors are mounted you could only sense the bottom part of them. So the space that the chair occupies is not completely detected. You just need to be aware about this.
20:49
We also deployed robots in industrial spaces, and there the setting was an industrial warehouse with many racks. The main challenge was that many of the features were repeated, so multiple halls would look the same, and that induced some ambiguity, there weren't many unique features to match with. The obstacles were easier to detect because they were larger.

22:09
Q: How dynamic were these spaces?
A: I would say in the case of the industrial environment it was quite dynamic. There were workers that constantly moved things around, so it change constantly. In the case of the office there wasn't a lot of change. When we would test we had the space reserved. But for real applications I would expect the environment to be dynamic.

23:02
Q: How does this dynamic aspect affect the robustness of the navigation stack?
A: It mainly affects the localization, up to a certain degree. The more the environment changes the more likely you are to have a drift in the SLAM algorithm. At least, our navigation stack was quite good with obstacle avoidance.

23:55
Q: Were these environments very large?
A: At least the industrial one was quite large, but I can't recall a number, but there were at least 50 rows of shelves.

24:33
Q: Which elements do you thing form together this environment?
A: Shelf and boxes, people, forklifts and machines. Mainly to classes: static and dynamic objects. The most dynamic would be people and forklifts moving around, but boxes are also dynamic their position would change day to day.

26:05
Q: Was there something in this environment that was particularly challenging?
A: Yes, the fact that the rows most of the time looked the same. That was the main challenge in that environment just because it was really uniform. 

26:50
Q: Do you have a map that you could share?
A: Yes.
28:38
A: This is an example of a map that we normally use. This is a map of an industrial area, as you can see there are a lot of laser beams that travel far, because the place was quite large, but we were interested in a specific area.
30:00
Q: Is the gray area between the white areas shelves?
A: Not all the time, the reason that is gray is that the robot can detect only the out most surface of the object, it doesn't know what's beyond a box.
31:35
A: This was probably a shelf, but were able to see like the columns of the shelf. As part of our navigation stack we had the opportunity to mark certain areas as areas to avoid.

32:25
Q: Was this something you could expect?
A: It was expected. We know that the sensor has a fixed height, so we can only detect what is at that height.

33:03
Q: What do you think are problematic areas for a navigation stack?
A: I would side, besides the problem with similar corridors, there is a problem when environments are too dynamic.
Q: And do you think a software solution can deal with these challenges?
A: I think so, yes. You have to do a lot of tests but it can be done.

34:38
Q: Do you think that the quality of this map will affect the performance?
A: Yes, if you are not able to capture some important features, or if you have a drift during mapping resulting in a warped map, it will affect the localization for sure. You have to ensure that the map is as close as reality as you can make it.
Q: And do you think a map that is too perfect can be troublesome?
A: If it's perfect, probably. A map generated by the robot will have noise, but the noise comes from the sensors the robot uses to localize itself as well. A noisy map will work better than a map made out of a CAD model. A map generated by the robot will give me more confidence.

### Section 4
36:42
Q: How do you approach testing? Is it simulation first or real world first?
A: Simulation first. We have our simulator set-up made so that we can switch between the simulated robot and the real robot. Particularly for the configuring SLAM algorithms.

37:43
Q: How would describe the simulated environment?
A: Ours is pretty simple, just a set of walls. 
38:38
A: This is our layout for simulation, the map we generated by the simulated robot, so as expected there is some noise. We have some halls, some narrow corridors, some objects. Everything is static, and the walls are completely vertical. So the robot sense the actual boundary.

39:35
Q: How different is this environment from the real world?
A: I would say the main difference is that we don't have dynamic objects in the simulation, and the we have very defined boundaries, so chairs are a represented as the couple area they take. 

40:20
Q: Did you find challenging to create this simulation world?
A: Not at all, we just drew it and extruded it.

40:42
Q: Were you basing it from a real environment?
A: No, this was completely fiction. We just said we needed some halls, some rooms, some obstacles in the middle. And said let's try it like that.

41:15 
Q: What environmental features would you like to simulate but currently is not possible?
A: Dynamic obstacles should be possible, but everything I would like to have is possible. 

42:04
Q: Any closing remarks?
A: No.

== end of interview ==