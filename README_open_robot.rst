.. Copyright 2016 The Cartographer Authors

.. Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

..      http://www.apache.org/licenses/LICENSE-2.0

.. Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.

===============================
Cartographer ROS for open-robot
===============================


Purpose
=======

`Cartographer`_ is a system that provides real-time simultaneous localization
and mapping (`SLAM`_) in 2D and 3D across multiple platforms and sensor
configurations. This project provides Cartographer's ROS integration for open-robot.

.. _Cartographer: https://github.com/googlecartographer/cartographer
.. _SLAM: https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping

Building & Installation
=======================


We recommend using `wstool <http://wiki.ros.org/wstool>`_ and `rosdep
<http://wiki.ros.org/rosdep>`_. For faster builds, we also recommend using
`Ninja <https://ninja-build.org>`_.

  .. code-block:: bash

    # Install wstool and rosdep.
    sudo apt-get update
    sudo apt-get install -y python-wstool python-rosdep ninja-build

    # Create a new workspace in 'catkin_ws'.
    mkdir catkin_ws
    cd catkin_ws
    wstool init src
    
    # Clone cartographer_ros
    cd src
    git clone https://github.com/open-robot/cartographer_ros.git

    # Merge the cartographer_ros.rosinstall file and fetch code for dependencies.
    cd ../
    wstool merge -t src ./src/cartographer_ros/cartographer_ros.rosinstall
    wstool update -t src

    # Install deb dependencies.
    rosdep update
    rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y

    # Build and install.
    catkin_make_isolated --install --use-ninja
    source install_isolated/setup.bash

How to run
==========

  .. code-block:: bash

    # Start open-robot 
    roslaunch robot_bringup demo_start.launch
    
    # Start Cartographer_ros
    roslaunch cartographer_ros demo_open_robot.launch 
    
    # Start rviz in a remote computer to watch the building map
    About how to run ROS across multiple machines: http://wiki.ros.org/ROS/Tutorials/MultipleMachines
