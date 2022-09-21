# UdacityHomeServiceRobot

The Home Service Robot has been simulated by executing shell scripts using xterminal which starts launch files that kick off nodes from inside the below packages. The robot will execute two 2D nav goals, and "pickup" a marker from a pickup point and move it to a dropoff point.

The below packages were used to complete the simulation environment of Home Service Robot project:

  1. "turtlebot_simulator"/"turtlebot_gazebo" is used to provide the open source URDF model of the Turtlebot robot and contains Gazebo, a robot simulation environment   with an integrated physics engine.

  2. "slam_gmapping" was used to create the map that the AMCL node uses to localize itself while navigating. The heart of this package is a laser-based Simultaneous    Localization and Mapping ROS node. The node is capable of mapping an unknown environment while at the same time updating its own estimate of where the robot is in the map.

  3. "turtlebot_navigation" package contains the AMCL package which is used to localize the robot. This package contains a node which performs Adaptive Monte Carlo Localization, which is a type of particle filter localization. This navigation package allows the robot to perform 2D nav goals, avoiding obstacles and succesfully navigating to the goal.

  4. "pick_objects" package contains the node which is responsible for interfacing with the ROS navigation stack to execute nav goals. It simply selects a goal pose which is composed of x and y coordinates and a rotational orientation. When this goal is reached, there is logic to pause for 5 seconds and return to the origin pose.

  5. "add_markers" package contains the node which subscribes to a topic to monitor the goal status and "pickup" and "dropoff" markers accordingly. Based on the incoming messages from the subscription, it will display, move, and hide a green marker by publishing the marker state for RViz to visualize.
