# Introduction
This article primarily introduces how to install ROS2 Foxy on the AIB-NW01 Ubuntu 20.04 environment provided by Avalue Technology Inc.

## Set Locale
```bash
# check for UTF-8
locale  

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

# Verify settings
locale  
```

## Setup Sources
```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```

## Add ROS 2 GPG Key with apt
```bash
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

## Add the repository to the sources list
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

## Install ROS 2 Packages
```bash
# Update apt repository caches 
sudo apt update
# ROS Desktop Install (Recommended): ROS, RViz, demos, tutorials
sudo apt install ros-foxy-desktop python3-argcomplete
# ROS-Base Install (Bare Bones): Communication libraries, message packages, command line tools. No GUI tools
sudo apt install ros-foxy-ros-base python3-argcomplete
# Development tools: Compilers and other tools to build ROS packages
sudo apt install ros-dev-tools
```

## Setup ROS2 Foxy Environment
```bash
# Replace ".bash" with your shell if you're not using bash
# Possible values are: setup.bash, setup.sh, setup.zsh
source /opt/ros/foxy/setup.bash
```

## Testing
```bash
# In one terminal
source /opt/ros/foxy/setup.bash
ros2 run demo_nodes_cpp talker

# In another terminal
source /opt/ros/foxy/setup.bash
ros2 run demo_nodes_py listener
```

## Optional Configuration
This way, every time you open a new terminal, the ROS 2 Foxy environment variables (ROS_DISTRO, AMENT_PREFIX_PATH, PATH...etc.) will be automatically loaded.
```bash
echo "source /opt/ros/foxy/setup.bash" >> ~/.bashrc
```

# Reference.
[Ubuntu (Debian) — ROS 2 Documentation: Foxy documentation](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html "Ubuntu (Debian) — ROS 2 Documentation: Foxy documentation")
