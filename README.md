# ISAAC SIM Tutorial for Unitree A1
## 1. Install Omniverse Launcher
- Follow the instruction in [2.Basic Isaac Sim Installation](https://docs.omniverse.nvidia.com/app_isaacsim/app_isaacsim/install_basic.html)
- For **Unitree A1**, install **the latest Isaac Sim** beta version 2022 in Omniverse Launcher.
- This setup requires NVIDIA graphic card from **RTX 2070** and **ROS noetic version**
- root_dir is ```~/.local/share/ov/pkg/isaac_sim-2022.1.0```

## 2. Put ```a1_custom.py``` in ```root_dir/standalone_examples/api/omni.isaac.quadruped/```
- ```a1_custom.py``` refers to  
  1) ```a1_direct_ros1_standalone.py``` - You can control A1 by directly control every 12 joints of A1. 
  2) ```a1_standalone.py``` - You can control A1 by pressing NUM keypad.


## 3. Come back to ```root_dir``` and run 
```
roscore
```
and in another terminal, run
```
./python.sh standalone_examples/api/omni.isaac.quadruped/a1_custom.py
```

## (To be updated) 4. To control A1 in simulator, run 
```
rostopic pub -r 1 isaac_a1/joint_torque_cmd sensor_msgs/JointState -- '{header: {seq: 0, stamp: now, frame_id: "value"}, name: ['name'], position: [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], velocity: [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], effort: [10, 0, 1, 10, 10, 10, 10, 10, 10, 10, 10, 10]}'
```
- The custom message will be made for simplicity 
- ```a1_custom.py``` subscibes the topic whose type requires above values (header, position, velocity, effort)
- Not all but the first three values of *effort* will be used for the advance of A1 in 'x, y, rotate' direction.  
- For example, in the above command the A1 will move with 10 Nm in x direction which is 'forward' and 1 Nm in 'anti-clockwise rotation'.

## TODO
- [ ] Make the Robot default state to be in a sitting state (as real).
- [ ] Check the input args of Isaac Sim A1 and Unitree A1 - velocity vs effort.
