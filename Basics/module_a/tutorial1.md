# F1TENTH Tutorial T01: Docker and ROS 2

Welcome to your first F1TENTH tutorial! This version includes embedded good coding habits, checklists, documentation links, upcoming visual demos, and now also outlines clear learning objectives, troubleshooting tips, and ROS 2 graph visualization guidance to support you as a beginner. This guide is built for first-year university students and assumes minimal experience with software development. It introduces two powerful tools used in robotics development: [Docker](https://docs.docker.com/) and [ROS 2](https://docs.ros.org/en/rolling/). You'll learn core concepts, how to apply them, and gain hands-on experience along the way.

> ✅ **Good Habit Reminder**: Always look up official docs before using a command you're unfamiliar with. Bookmark [Docker](https://docs.docker.com/get-started/) and [ROS 2](https://docs.ros.org/en/rolling/) now!

---

## 1. Introduction to Docker for Robotics

🎯 **Learning Objectives**

* Understand what Docker is and why it's useful in robotics
* Identify key Docker concepts (images, containers, Dockerfiles)
* Learn the benefits of using Docker for reproducibility and isolation

### What is Docker?

Imagine your laptop is a kitchen. Docker is like having a bunch of meal kits — everything you need to cook a specific meal (or run a software project) is packed neatly together. No missing ingredients, no mess.

Docker allows you to package an application and all its dependencies into a **container**. This container can run on any computer with Docker installed, regardless of the operating system.

> 📘 Learn more: [Docker Overview](https://docs.docker.com/get-started/overview/)

### Why Use Docker in Robotics?

* ✅ **Reproducibility**: Everyone on your team runs the same setup.
* ✅ **Isolation**: No conflicts between projects.
* ✅ **Portability**: Move between laptops, labs, or robots with no reinstallation.

### Core Docker Concepts (with Visual Aid)

```
+--------------------------+
|         Image           | <-- Recipe for your container (like a blueprint)
+--------------------------+
|         Dockerfile      | <-- Instructions to build the image
+--------------------------+
|         Container        | <-- A running instance of the image
+--------------------------+
```

> 📘 Learn more: [Docker Images vs Containers](https://docs.docker.com/get-started/)

### ✅ Good Habits Checklist

* [ ] Use `Dockerfile` instead of installing software manually
* [ ] Document what each command does using comments
* [ ] Never hardcode credentials in Dockerfiles
* [ ] Always mount volumes to avoid losing work

🎥 **Coming Soon:** Visual terminal demo — *docker build and run*

---

## 2. Getting Hands-On with Docker

> 🎥 Visual: `docker run` in action *(Insert terminal recording GIF)*

### Installation

* [Install Docker for your OS](https://docs.docker.com/get-docker/)

### Core Commands

```bash
# Download an existing image from Docker Hub
docker pull ubuntu

# Build a custom image from a Dockerfile
docker build -t my_image .

# Run an interactive container
docker run -it my_image

# List running containers
docker ps

# Stop a container
docker stop <container-id>

# Remove a container
docker rm <container-id>
```

> 📘 Learn more: [Docker CLI Reference](https://docs.docker.com/engine/reference/commandline/docker/)

### ✅ Good Habits Checklist

* [ ] Use `--rm` to clean up containers automatically when testing
* [ ] Clean up regularly using `docker system prune`
* [ ] Use `--name` to identify containers more easily

---

## 3. ROS 2: Your Robot's Operating System

🎯 **Learning Objectives**

* Grasp what ROS 2 is and how it enables modular robotics software
* Understand key components like nodes, topics, and services
* Know how data flows between different parts of a robotic system

### What is ROS 2?

ROS 2 (Robot Operating System 2) is a framework that helps different parts of a robot — like sensors, motors, and control systems — talk to each other.

You can think of a robot as a team of people:

* **Sensors** = the eyes and ears
* **Motors** = the arms and legs
* **Control Code** = the brain
  ROS 2 is the language they use to coordinate.

> 📘 Learn more: [ROS 2 Overview](https://docs.ros.org/en/rolling/index.html)

### Key ROS 2 Concepts (with Diagram)

```
+-------------+         +-------------+         +-------------+
|  Sensor     |-------> |   Node A    |-------> |  Motor Cmd  |
| (Camera)    | Topic   | (Talker)    | Topic   | (Listener)  |
+-------------+         +-------------+         +-------------+
```

| Concept    | Description                                                |
| ---------- | ---------------------------------------------------------- |
| Node       | A small program that performs one task                     |
| Topic      | A stream of data (like sensor readings)                    |
| Publisher  | A node that sends messages                                 |
| Subscriber | A node that receives messages                              |
| Service    | A request/response system between nodes                    |
| Action     | A long-running task with feedback (e.g. driving to a goal) |
| Parameter  | A tunable value inside a node                              |

> 📘 Learn more: [Nodes, Topics, Services in ROS 2](https://docs.ros.org/en/rolling/Concepts.html)

### ✅ Good Habits Checklist

* [ ] Use launch files to manage nodes
* [ ] Keep node logic modular and reusable
* [ ] Use `ros2 topic list` and `ros2 topic echo` to debug
* [ ] Comment your node scripts generously

🎥 **Coming Soon:** Visual: Talker and listener node in action

---

## 4. ROS 2 Workspaces and Package Structure

🎯 **Learning Objectives**

* Understand the structure of a ROS 2 workspace
* Learn how to create and build packages inside a workspace
* Build good workspace habits to avoid conflicts and confusion

### What is a Workspace?

A workspace is a directory where you develop and organize your ROS 2 projects.

### Directory Layout

```bash
ros2_ws/        # Your main workspace
├── src/        # Source code of your packages
├── install/    # Install folder created by the build system
├── build/      # Temporary build files
├── log/        # Log files from the build
```

> 📘 Learn more: [Creating a ROS 2 Workspace](https://docs.ros.org/en/rolling/Tutorials/Beginner-Client-Libraries/Creating-A-Workspace/Creating-A-Workspace.html)

### ✅ Good Habits Checklist

* [ ] Use one workspace per project to avoid clutter
* [ ] Rebuild regularly (`colcon build`) after changes
* [ ] Run `colcon clean` if packages act unexpectedly
* [ ] Never add workspace sourcing to `.bashrc`

🎥 **Coming Soon:** Visual: Workspace build from scratch

---

## 5. Creating and Understanding a ROS 2 Package

🎯 **Learning Objectives**

* Learn to create a basic ROS 2 Python package
* Understand the purpose of files like `package.xml` and `setup.py`
* Write and run a simple ROS 2 node

### Creating a Python Package

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_python my_package --dependencies rclpy std_msgs
```

> 📘 Learn more: [Creating ROS 2 Python Packages](https://docs.ros.org/en/rolling/Tutorials/Beginner-Client-Libraries/Writing-A-Simple-Py-Publisher-And-Subscriber.html)

### ✅ Good Habits Checklist

* [ ] Use clear package and node names
* [ ] Create separate files for publishers and subscribers
* [ ] Use `entry_points` in `setup.py` for CLI access
* [ ] Update `package.xml` with real descriptions

🎥 **Coming Soon:** Visual: File structure breakdown + node run

---

## 6. Building and Running Inside Docker

### Sample Dockerfile

```Dockerfile
FROM ros:humble
RUN apt update && apt install -y python3-colcon-common-extensions
WORKDIR /ros2_ws
COPY . /ros2_ws
RUN . /opt/ros/humble/setup.sh && colcon build
CMD ["bash"]
```

> 📘 Learn more: [Dockerizing ROS 2 Projects](https://docs.ros.org/en/rolling/How-To-Guides/Docker.html)

### ✅ Good Habits Checklist

* [ ] Add a `.dockerignore` file to keep images small
* [ ] Re-tag and version your Docker builds
* [ ] Push only working builds to Docker Hub

🎥 **Coming Soon:** Visual: Docker build + colcon run demo

---

## 7. Final Assignment

### Objective

* Build a containerized ROS 2 workspace
* Create a simple publisher node
* Launch it using Python
* Push your container to Docker Hub
* Submit via GitHub Classroom

> ✅ **Track your changes:** Keep a `CHANGELOG.md` file from the start

---

## 8. Common Mistakes and Pro Tips

| Mistake                         | Fix                                            |
| ------------------------------- | ---------------------------------------------- |
| Not sourcing the setup script   | Run `source install/setup.bash`                |
| Permissions issue on volume     | Add `--user $(id -u):$(id -g)` to `docker run` |
| Dependencies missing in package | Add to `package.xml` and `setup.py`            |

✅ Use `tmux` to keep sessions alive
✅ Use volumes to persist work
✅ Don’t put ROS source commands in `.bashrc` — see [why here](https://docs.ros.org/en/rolling/How-To-Guides/Overriding-Environment-Variables.html)

---

## 9. Resources and What’s Next

### 🔄 Troubleshooting Common ROS 2 Issues

> 🛠️ **Colcon build fails with missing dependencies**
> Check your `package.xml` and `setup.py` to ensure all dependencies are listed. Use `rosdep install --from-paths src --ignore-src -r -y` to auto-install missing ones.

> 🛠️ **Can't find installed packages**
> Make sure to `source install/setup.bash` after building. Never skip this step.

> 🛠️ **Docker can't access local folder**
> Ensure you're using absolute paths with `-v` or `--mount`, and check permissions.

---

### 🧠 Visualize ROS 2 Graph

Run this command to generate a visual diagram of how your nodes and topics are connected:

```bash
rqt_graph
```

Or use:

```bash
ros2 run tf2_tools view_frames
```

This produces an image like the one below that shows your full ROS 2 computation graph.

📷 *(Insert SVG or screenshot of ROS graph visualization here)*

---

### Learn More

* [Official ROS 2 Tutorials](https://docs.ros.org/en/rolling/Tutorials.html)
* [Docker Curriculum](https://docker-curriculum.com/)
* [RoboticsBackend ROS 2 Tutorials](https://roboticsbackend.com/)

### Coming Up

* Writing custom messages and services
* Simulating environments with Gazebo
* Connecting ROS 2 nodes over a network

---

Congratulations! 🎉 You now know how to:

* Use Docker to run isolated robotics environments
* Build ROS 2 packages from scratch
* Launch and test simple nodes
* Submit your containerized project professionally

