# UdacityHomeServiceRobot

The Home Service Robot has been simulated by executing shell scripts using xterminal which starts launch files that kick off nodes from inside the below packages. The robot will execute two 2D nav goals, and "pickup" a marker from a pickup point and move it to a dropoff point.

The below packages were used to complete the simulation environment of Home Service Robot project:

  1. "turtlebot_simulator"/"turtlebot_gazebo" is used to provide the open source URDF model of the Turtlebot robot and contains Gazebo, a robot simulation environment   with an integrated physics engine.

  2. "slam_gmapping" was used to create the map that the AMCL node uses to localize itself while navigating. This ROS package is based on Grid-based Fast SLAM algorithm to map an environment. Gmapping provides laser based SLAM, meaning that we can feed its node with the robot laser measurements and odometry values and expect it to provide  2D occupancy grid map of the environment. The map gets updated as the robot moves and collect sensory information using its laser range finder sensor.

  3. "turtlebot_navigation" package contains the AMCL package which is used to localize the robot. This package contains a node which performs Adaptive Monte Carlo Localization, which works by figuring out where the robot would need to be on the map in order for its laser scans to make sense. Each possible location is represented by a "particle" and particles with laser scans that do not match well, are removed resulting in a group of particles representing the location of the robot in the map. The Navigation stack takes in information from odometry and sensor streams and outputs velocity commands that allows the robot to perform 2D nav goals, avoiding obstacles and succesfully navigating to the goal.

  4. "pick_objects" package contains the node which is responsible for interfacing with the ROS navigation stack to execute nav goals. It simply selects a pickup pose which is composed of x and y coordinates and a rotational orientation. When this pickup pose is reached, there is a logic to pause for 5 seconds, display a "pickup" message and navigate to the dropoff pose. When the dropoff pose is reached, it displays "dropoff" message.

  5. "add_markers" package contains the node which subscribes to a topic to monitor the goal status and "pickup" and "dropoff" markers accordingly. Based on the incoming messages from the subscription, it will display, move, and hide a blue marker by publishing the marker state for RViz to visualize.
