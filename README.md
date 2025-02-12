# ROS Noetic and ROS 2 Humble Installation Guide

This guide provides step-by-step instructions for installing **ROS Noetic** and **ROS 2 Humble** on Ubuntu. Both ROS Noetic and ROS 2 Humble are popular frameworks for building robotics applications, each serving different needs. ROS Noetic is the latest version of the ROS 1 series, while ROS 2 Humble is a newer, more robust version designed to improve upon the ROS 1 architecture.

## Prerequisites

Before you begin, make sure your system meets the following requirements:
- **Ubuntu 20.04 or later** (This guide assumes you're using Ubuntu 20.04 LTS)
- A **64-bit** architecture.
- A **ROS compatible computer** (Ideally a laptop or desktop with at least 4GB of RAM)

You’ll need to have `sudo` privileges and an internet connection for downloading the packages.

## Table of Contents

1. [Install ROS Noetic](#install-ros-noetic)
2. [Install ROS 2 Humble](#install-ros-2-humble)
3. [Post-installation Steps](#post-installation-steps)
4. [Verification](#verification)
5. [Resources and Links](#resources-and-links)

---

## Install ROS Noetic

### Step 1: Setup Your Sources

First, update your system and add the ROS package repository.

```bash
sudo apt update
sudo apt install curl gnupg2 lsb-release
```

Now, add the ROS repository to your system.

```bash
curl -sSL http://packages.ros.org/ros.key | sudo apt-key add -
```

Then, add the ROS repository.

```bash
echo "deb [arch=amd64] http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/ros-latest.list
```

### Step 2: Install ROS Noetic

Update your system’s package list and install ROS Noetic.

```bash
sudo apt update
sudo apt install ros-noetic-desktop-full
```

This will install the full ROS Noetic desktop version, including tools such as RViz, Gazebo, and the ROS command-line interface.

### Step 3: Initialize rosdep

ROS uses `rosdep` to install system dependencies for source code. Initialize it with:

```bash
sudo rosdep init
rosdep update
```

### Step 4: Set Up Your ROS Environment

You need to set up your environment for ROS by adding it to your `.bashrc` file:

```bash
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

### Step 5: Install Dependencies

Some additional ROS dependencies are required to work with ROS packages and workspaces:

```bash
sudo apt install python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```

---

## Install ROS 2 Humble

### Step 1: Setup Your Sources

Similar to ROS Noetic, you'll need to add the ROS 2 Humble repository.

```bash
sudo apt update
sudo apt install curl gnupg2 lsb-release
```

Download and add the ROS 2 repository:

```bash
curl -sSL https://packages.ros.org/ros2/ubuntu/ros2.asc | sudo apt-key add -
```

Then, add the ROS 2 repository.

```bash
echo "deb [arch=amd64] https://packages.ros.org/ros2/ubuntu $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/ros2-latest.list
```

### Step 2: Install ROS 2 Humble

Update your system and install ROS 2 Humble.

```bash
sudo apt update
sudo apt install ros-humble-desktop
```

The `ros-humble-desktop` package includes the common tools you need for a ROS 2 installation, such as RViz, Gazebo, and more.

### Step 3: Set Up Your ROS 2 Environment

For ROS 2, you will also need to source the ROS 2 environment in your `.bashrc`.

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

### Step 4: Install Dependencies

ROS 2 uses some Python dependencies, so install them via pip:

```bash
sudo apt install python3-colcon-common-extensions
```

---

## Post-installation Steps

### Step 1: Install Development Tools (Optional)

If you're planning to develop ROS 1 or ROS 2 packages, you can install additional development tools.

For ROS Noetic:
```bash
sudo apt install python3-catkin-tools
```

For ROS 2 Humble:
```bash
sudo apt install python3-colcon-common-extensions
```

### Step 2: Create a Workspace

For both ROS 1 and ROS 2, you can create a workspace to store your projects.

#### ROS Noetic:
Create the workspace and build it:

```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws
catkin_make
```

#### ROS 2 Humble:
Create the workspace and build it:

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
colcon build
```

### Step 3: Source the Workspace

Once you have created your workspace, remember to source it every time you open a new terminal.

#### ROS Noetic:
```bash
source ~/catkin_ws/devel/setup.bash
```

#### ROS 2 Humble:
```bash
source ~/ros2_ws/install/setup.bash
```

---

## Verification

### ROS Noetic

Verify the ROS Noetic installation by running:

```bash
roscore
```

If everything is installed correctly, the `roscore` command should start the ROS master node.

### ROS 2 Humble

Verify the ROS 2 Humble installation by running:

```bash
ros2 run demo_nodes_cpp talker
```

This should start a demo ROS 2 node publishing messages.

---

## Troubleshooting

- **"Command not found" errors**: Ensure you've properly sourced your ROS environment (`source /opt/ros/noetic/setup.bash` or `source /opt/ros/humble/setup.bash`).
- **Dependency issues**: If you encounter errors with missing dependencies, use `rosdep` to resolve them for ROS Noetic (`rosdep install --from-paths src --ignore-src -r -y`) or ROS 2 (`rosdep update && rosdep install --from-paths src --ignore-src -y`).

---

## Resources and Links

- [ROS 2 Humble Installation Guide](https://docs.ros.org/en/humble/Installation.html)
- [ROS Installation Guide (ROS 1)](http://wiki.ros.org/ROS/Installation)
- [Video Guide: How to Install ROS](https://www.youtube.com/watch?v=IOwlnpWPuj0)
- [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads)

---

## Conclusion

This guide should have helped you install ROS Noetic and ROS 2 Humble on your Ubuntu system
