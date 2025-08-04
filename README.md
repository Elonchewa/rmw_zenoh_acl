# rmw_zenoh_acl
I am trying to connect a Jetson Orin Nano and an intel NUC both running Ubuntu 22.04 and ROS2 Humble.
The Orin has zenoh version: Version: 0.1.4-1jammy.20250719.075632
The Nuc has zenoh version: Version: 0.1.4-1jammy.20250719.010153

The two devices are connected through ethernet/usb connector. The ethernet connection being on the Orin side and the usb connection being on the nuc side.

The nuc connects to the orin on the interface enx000ec6a4097b and has an ip 192.168.10.1/24

The Orin connects to the Nuc on the interface enP8p1s0 and has an ip 192.168.10.2/24

Note: In this repo Rob1 stands for the nuc and Rob2 stands for the Orin. 


The two devices have their corresponding zenoh router configuration files (I've posted the configs for both in this repo). The environment variable ZENOH_ROUTER_CONFIG_URI is set on both; however, the session config is in default settings for both (I do not have ZENOH_SESSION_CONFIG files for either).

Background:
* Before I used the access_control part of the configs, my goal was just for the two devices to send all their topics with each other. However, at times I would have lots of topics being published/subscribed to and the data for all topics would stop sending (I'm assuming this is due to bandwidth issues). So I decided to limit the topics that send their data across the routers. I only need a few topics to be shared between them.

Current:
* After I included the access_control part of the config,When the routers are started on both machines through `ros2 run rmw_zenoh_cpp rmw_zenohd`, the router logs a message that the interface specified in the access_control `did not match any configured ACL subject. Default permission Allow will be applied on all messages`. Which means I am back to state I was in before I configured the ACL settings.
* When I run `ros2 topic list` I can see all the topics from one device listed on the other.

I'm not sure if this issue is due to networking or due to limitations of zenoh on humble. 


Details on Versions:
* ORIN Zenoh version:
  
* Package: ros-humble-rmw-zenoh-cpp
Version: 0.1.4-1jammy.20250719.075632
Priority: optional
Section: misc
Maintainer: Yadunund <yadunund@openrobotics.org>
Installed-Size: 554 kB
Depends: libc6 (>= 2.34), libgcc-s1 (>= 3.3.1), libstdc++6 (>= 12), ros-humble-fastcdr, ros-humble-ament-index-cpp, ros-humble-rcpputils, ros-humble-rcutils, ros-humble-rmw, ros-humble-rosidl-typesupport-fastrtps-c, ros-humble-rosidl-typesupport-fastrtps-cpp, ros-humble-tracetools, ros-humble-zenoh-cpp-vendor, ros-humble-ros-workspace
Download-Size: 171 kB
APT-Manual-Installed: yes
APT-Sources: http://packages.ros.org/ros2/ubuntu jammy/main arm64 Packages

* NUC zenoh version:

* Package: ros-humble-rmw-zenoh-cpp
Version: 0.1.4-1jammy.20250719.010153
Priority: optional
Section: misc
Maintainer: Yadunund <yadunund@openrobotics.org>
Installed-Size: 611 kB
Depends: libc6 (>= 2.34), libgcc-s1 (>= 3.3.1), libstdc++6 (>= 12), ros-humble-fastcdr, ros-humble-ament-index-cpp, ros-humble-rcpputils, ros-humble-rcutils, ros-humble-rmw, ros-humble-rosidl-typesupport-fastrtps-c, ros-humble-rosidl-typesupport-fastrtps-cpp, ros-humble-tracetools, ros-humble-zenoh-cpp-vendor, ros-humble-ros-workspace
Download-Size: 183 kB
APT-Manual-Installed: yes
APT-Sources: http://packages.ros.org/ros2/ubuntu jammy/main amd64 Packages
