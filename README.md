# rover_arm_urdf

URDF description of the Team Interplanetar rover's robotic arm, exported from the SOLIDWORKS model and packaged for ROS 2. It is the base for the arm's MoveIt 2 inverse-kinematics setup and the operators' arm control GUI.

## The arm

| Joint | Type | Notes |
|---|---|---|
| `base_joint` | revolute | base yaw |
| `shoulder_joint` | revolute | |
| `elbow_joint` | revolute | |
| `wrist_joint` | revolute | |
| `roller_joint` | revolute | wrist roll |
| `gripper_joint1`, `gripper_joint2` | prismatic | parallel gripper fingers |

Meshes for every link are in `arm_sim/meshes/` (STL), joint limits are in `arm_sim/urdf/arm_sim.urdf`.

## Package layout

```
arm_sim/
├── urdf/arm_sim.urdf          # robot description
├── meshes/*.STL               # link meshes from SOLIDWORKS
├── launch/display.launch.py   # RViz2 + joint sliders
├── rviz/display.rviz
└── config/                    # joint names for controllers
```

## Run

Tested with ROS 2 (Humble/Jazzy).

```bash
cd ~/ros2_ws/src
git clone https://github.com/abulhasnat-abdullah/rover_arm_urdf.git
cd ~/ros2_ws
rosdep install --from-paths src --ignore-src -y
colcon build --packages-select arm_sim
source install/setup.bash
ros2 launch arm_sim display.launch.py
```

RViz2 opens with the arm, and the `joint_state_publisher_gui` window lets you move each joint to check limits and kinematics.

## Related

- [Mars-Rover-Simulation](https://github.com/abulhasnat-abdullah/Mars-Rover-Simulation): the rover's Gazebo workspace
- [arm_visualizer](https://github.com/abulhasnat-abdullah/arm_visualizer): a Tkinter/Matplotlib view of arm joints and workspace
