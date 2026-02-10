# RoboticsCrashCourse_week4_Simulation
Here is the English version of your README draft. I have kept the structure professional and suitable for a GitHub repository.

## 🔦 Webots Light Chasing Experiment: Master & Dog Simulation
This project is an autonomous robot collaboration experiment based on the Webots simulation environment.

It simulates a dynamic "Dark Night Tracking" scenario:

master.py: use it to be the controller of The Master (Bait): An autonomous mobile unit holding a light source that roams the environment while actively avoiding obstacles.

dog.py: use it to be the controller ofThe Dog (Tracker): A vision-based tracking unit that uses a differential light intensity algorithm to lock onto the Master's position, while fusing near-field obstacle avoidance logic to prevent collisions.

## 🤖 System Roles
1. The Master (Light Bait)
Core Function: Acts as a dynamic Mobile Beacon in the environment.

Hardware Configuration:

Equipped with an omnidirectional LED array.

Mounts a PointLight on the turretSlot to simulate physical light attenuation and support shadow casting.

Motion Logic:

Based on a variation of the Braitenberg Vehicle algorithm.

Accelerates in open areas and generates repulsive forces using sensor differentials to smoothly steer away when obstacles are detected.

2. The Dog (Visual Tracker)
Core Function: Locates and tracks a dynamic light source within a complex, obstacle-filled environment.

Hardware Configuration:

8x Light Sensors: Used to perceive light intensity gradients.

8x Distance Sensors: Used for near-field obstacle avoidance.

Control Algorithm:

Weighted Sensor Fusion: Vector synthesis of "Light Attraction Force" and "Obstacle Repulsion Force".

State Machine: Includes four states: Search, Chase, Avoid, and Unstuck.

## 🧠 Algorithm Principle
The tracker's core steering logic is based on the following formula:

Python

Final Steering Command = (Light Coefficient * Light Diff) + (Avoidance Coefficient * Obstacle Diff)

Final_Steering = (K_chase * Light_Diff) + (K_avoid * Obstacle_Diff)

Long-Range Tracking: When the surroundings are clear, Obstacle_Diff is 0. The robot is guided entirely by light gradients, executing P-Control (Proportional Control) to steer towards the brightest point.

Close-Range Avoidance: When close to a wall, distance sensor readings spike. The avoidance repulsion Obstacle_Diff increases rapidly, overriding the chasing command and forcing the robot to push away from the wall.

Deadlock Detection: If the robot gets stuck in a corner or a collision occurs (Front_Dist > Threshold), a forced reverse timer is triggered, executing a "Reverse & Turn" maneuver to escape.

🛠️ Simulation Setup
To ensure the light sensors function correctly, this project relies on a Dark Environment setting:

WorldInfo: It is recommended to adjust basicTimeStep to match the controller's refresh rate.

Lighting:

BackgroundLight: luminosity must be set to 0 or a very low value (e.g., 0).
<img width="367" height="386" alt="image" src="https://github.com/user-attachments/assets/2f466ef1-ca7f-4891-a9f2-5f977aee3050" />

DirectionalLight: Recommended to remove or disable to eliminate ambient interference light.

Master Robot: A PointLight node must be added to the turretSlot with castShadows set to TRUE to ensure walls correctly block lig<img width="348" height="96" alt="image" src="https://github.com/user-attachments/assets/02047a5f-56c6-4ba3-9302-d63ca8f61ae2" />
ht (preventing X-ray tracking).


##📝 Future Plans (To-Do)
[ ] Swarm Intelligence: Introduce multiple "Dogs" tracking a single "Master" simultaneously, adding swarm avoidance and formation keeping algorithms.

[ ] Air-Ground Co-op: Add a Mavic 2 Pro UAV model as an aerial tracker to implement light tracking in 3D dimensions.


