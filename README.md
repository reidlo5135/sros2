## sros2

### install libssl-dev
```bash
sudo apt update && sudo apt install libssl-dev
```

### install RIT Connext DDS
```bash
```

### install RMW Connext CPP
```bash
sudo apt-get install ros-<distro>-rmw-connext-cpp
```

### Run Demo

- create workspace
```bash
mkdir -p sros2_ws/src
```

- Generate key store
```bash
cd ~/sros2_ws
ros2 security create_keystore demo_keys
```

- Generate keys and certificates for the talker and listener nodes
```bash
ros2 security create_key demo_keys /talker_listener/talker
ros2 security create_key demo_keys /talker_listener/listener
```

- Define the SROS2 environment variables
```bash
export ROS_SECURITY_KEYSTORE=~/sros2_ws/demo_keys
export ROS_SECURITY_ENABLE=true
export ROS_SECURITY_STRATEGY=Enforce
```

- export RMW
```bash
export RMW_IMPLEMENTATION=rmw_fastrtps_cpp
export RMW_IMPLEMENTATION=rmw_connext_cpp
```

- Run node
```bash
ros2 run demo_nodes_cpp talker --ros-args --enclave /talker_listener/talker
ros2 run demo_nodes_py listener --ros-args --enclave /talker_listener/listener
```
