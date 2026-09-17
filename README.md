# 🐢 ROS2 Practice Nodes

## What Is It?
A set of small ROS2 nodes written in Python (using `rclpy`) that demonstrate the core building blocks of a robotics application: creating a node, running code on a timer, publishing commands, and subscribing to sensor data. Together they control and monitor a simulated turtle robot using the built-in `turtlesim` simulator.

## Technologies Involved
- **Python** — the language all three nodes are written in
- **ROS2 (rclpy)** — the Robot Operating System framework's Python client library, used to create nodes, timers, publishers, and subscribers
- **turtlesim** — ROS2's built-in turtle simulator, used here as a simple robot to control and read data from
- **geometry_msgs / turtlesim.msg** — the standard message types used to send velocity commands (`Twist`) and read the turtle's position (`Pose`)

## Features
- **`my_first_node.py`** — a basic ROS2 node that logs a "Hello" message once per second, with an increasing counter, to demonstrate node setup and timers
- **`draw_circle.py`** — continuously publishes velocity commands that drive the simulated turtle in a circle, by combining constant forward and turning speed
- **`pose_subscriber.py`** — listens to the turtle's live position and logs its (x, y) coordinates in real time as it moves

## Process
Each file is a standalone ROS2 node, but they all follow the same underlying pattern:
1. **Set up** — `rclpy.init()` starts up the ROS2 Python client library
2. **Create the node** — each node is its own Python class that inherits from ROS2's `Node`, giving it access to logging, timers, publishers, and subscribers
3. **Do the actual work** — via either a **timer callback** (runs on a schedule, used in `my_first_node` and `draw_circle` to repeatedly log or publish) or a **subscription callback** (runs automatically whenever new data arrives, used in `pose_subscriber` to react to the turtle's position)
4. **Spin** — `rclpy.spin(node)` keeps the node alive and listening/publishing until it's stopped
5. **Shut down** — `rclpy.shutdown()` cleanly closes the ROS2 connection

## What I Learned
- The core ROS2 concepts: nodes, topics, publishers, and subscribers, and how they communicate with each other
- How to use `rclpy` to create a node, and how to use timers vs. subscription callbacks
- How to work with ROS2 message types (`Twist` for velocity, `Pose` for position)
- How a simulated robot (`turtlesim`) can be controlled and monitored the same way a real robot would be

## How It Can Be Improved
- Combine the publisher and subscriber into a single closed-loop node — e.g., stop the turtle once it returns to its starting position
- Make the circle's speed and radius adjustable via ROS2 parameters instead of hardcoded values
- Add more drawing patterns beyond a circle (square, spiral, figure-eight)
- Package the nodes properly with a `setup.py` and `package.xml` so they can be run with `ros2 run` instead of directly with Python
- Add a launch file to start `turtlesim` and all the nodes together with one command
- Visualize the turtle's path traveled over time, not just its live position

## Running the Project
1. Install ROS2 (e.g. Humble or a later distribution) and source it in your terminal.
2. Install/launch the turtle simulator:
   ```
   ros2 run turtlesim turtlesim_node
   ```
3. In a separate terminal (with ROS2 sourced), run any of the nodes directly:
   ```
   python3 my_first_node.py
   python3 draw_circle.py
   python3 pose_subscriber.py
   ```
   (Note: fix the missing `main()` guard mentioned above for `draw_circle.py` and `pose_subscriber.py` first, or they won't do anything when run this way.)

## Picture of the flowchart
<img src="https://raw.githubusercontent.com/matafn09/ROS2-Publisher-and-Subscriber/main/Rqt_graph for my robot (1).png" width="600" alt="Publisher Demo">
