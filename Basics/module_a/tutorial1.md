associated video: https://youtu.be/EU-QaO6xTv4


extremely important. will be going over the basis of how ROS2 works. also docker as well i guess. honestly this was meant to be only tutorial 1 but i think im going to have things  for lab 1 also in here.



---

## 🐳 What is Docker (in plain English)?
Docker is a **tool that makes it easy to package, run, and share applications** in a consistent way, across different machines.

Imagine you’ve got an app that needs:
- Python 3.11
- A specific version of Linux
- Some custom libraries
- A database

If you set that up on your machine, it might work great. But if someone else tries to run it on their laptop or a server — it might not work, because their setup is different.

**Docker solves this.** It puts your app and *everything it needs to run* into one lightweight package, called a **container**. You can send this container to someone else, and it will run *exactly the same* on their machine.

---

## 🧱 How is Docker Different from a Virtual Machine (VM)?

| Feature | Docker (Containers) | Virtual Machines |
|--------|---------------------|------------------|
| **System Overhead** | Very light (shares your OS kernel) | Heavy (each VM runs its own OS) |
| **Startup Time** | Seconds | Minutes |
| **Performance** | Near-native | Slower (more overhead) |
| **Size** | Megabytes | Gigabytes |
| **Isolation** | App-level | Full system-level |
| **Use Case** | Running many small apps, dev/test, microservices | Full OS testing, running different OSes (e.g. Windows on Linux) |

**Analogy:**
- A **VM** is like a full apartment building for one person — has its own walls, plumbing, electricity, etc.
- A **Docker container** is like a room in a shared house — separated from others, but shares some stuff like the plumbing and power with the whole house.

---

## 🚀 Why Use Docker Over VMs?
Here’s why developers and companies love Docker:

### 1. **Lightweight**
You can run **lots of containers** on one machine. VMs eat a lot more memory and CPU.

### 2. **Fast**
Containers start almost instantly. VMs take a while to boot up.

### 3. **Portable**
A Docker container will run the same way on your laptop, your teammate’s laptop, or a cloud server — no "it works on my machine" issues.

### 4. **Easier Dev & Deployment**
You can:
- Spin up an app and its database in one command.
- Use Docker Compose to define multi-service apps.
- Push images to Docker Hub and deploy anywhere.

---

## 🧰 Applications: Running Linux Inside Windows

### 1. **Using Docker to Run Linux Apps on Windows**
Docker lets you run **Linux-based containers on a Windows machine**, thanks to a lightweight virtual machine under the hood (via WSL2 or Hyper-V). So even if your app needs Linux, you don’t need to dual-boot or install Linux manually.

#### Example:
Say you want to:
- Run a Python Flask web server on Ubuntu
- Use PostgreSQL (a Linux-native database)

With Docker, you can:
```bash
docker run -it ubuntu
```
Boom — you're inside an Ubuntu container, running on Windows.

You can even use `docker-compose.yml` to spin up both Flask and Postgres in one go. This is especially useful if you're building something that’ll eventually run on a Linux server (most servers are Linux!).

---
if you have a windows laptop, getting used to working in a docker container is going to be extremely useful. if you are on linux, you are lucky! those guys are just going to be simulating our environment lol.

id reccomend sticking to the docker cli as much as possible to get used to all the wierd quirks, but docker desktop is a great tool(although using it is a crutch, kind of like using git cli vs github desktop)

---
ALRIGHT! LETS LEARN ROS

honestly the ros2 docs are pretty good, its what i used to learn: https://docs.ros.org/en/foxy/index.html
theyve documented things really well there, and im not trying to replace the use of other docs, being able to navigate through docs of other tools really is a good skill to have. ill have an overview, but wont go too in depth.

---

## 🤖 What is ROS 2?

**ROS 2** is an **open-source framework** for building robot software.

It’s not an operating system like Windows or Linux — despite the name — but more like a **collection of tools, libraries, and conventions** that help you write code to control robots.

Think of it like:
> 🧱 LEGO blocks for building robot brains

It helps with things like:
- Moving motors
- Reading sensors
- Talking between different parts of the robot
- Controlling timing
- Communicating across machines

---

## 🧠 Why ROS 2 Exists (vs ROS 1)

ROS 1 was great for prototyping, but it had limitations:
- Not real-time safe
- Not multi-robot friendly
- Harder to use across networks
- Linux-only (mainly Ubuntu)

**ROS 2** fixed a lot of this:
- Built on top of **DDS (Data Distribution Service)**, a professional pub-sub communication standard
- Designed to be:
  - **Real-time**
  - **Multi-platform** (Linux, Windows, Mac)
  - **More secure and reliable**

---

## 🧩 Key Concepts in ROS 2

Let’s go over the **basic building blocks**:

### 1. **Nodes**
- A **node** is like a mini-program that does one thing.
- Example: One node reads a camera; another drives the wheels.

### 2. **Topics**
- Nodes talk to each other using **topics**.
- If Node A is a camera and publishes images on `/camera`, Node B can **subscribe** to `/camera` to process them.

🗣️ *It's like a radio station: one node broadcasts, another listens.*

### 3. **Messages**
- Data sent over topics.
- Pre-defined formats like `geometry_msgs/Twist` (for movement), or custom messages.

### 4. **Services**
- For request/response style communication (like asking a robot arm to move to a certain position).

### 5. **Actions**
- Like services, but for **long-running tasks** (e.g., "walk to this location").

### 6. **Launch Files**
- Used to start up multiple nodes at once, with all their parameters.

---

## 🛠️ ROS 2 in Practice

Here’s what a simple robot system might look like in ROS 2:

```
[Lidar Node] --(laser scan msgs)--> [Navigation Node] --(cmd_vel msgs)--> [Motor Driver Node]
```

Each piece is isolated and reusable. You can swap components without rewriting everything.


---


ok. enough theory, lets get to getting stuff going on your laptop. this is getting into lab1. dont worry, not the answers.


##  Overview
The goal of this lab is to get you familiar with the ROS 2 workflow. You'll have the option to complete the coding segment of this assignment in either Python or C++. However, we highly recommend trying out both since this will be the easiest assignment to get started on a new language, and the workflow in these two languages are slightly different in ROS2 and it's beneficial to understand both.

In this lab, it'll be helpful to read these tutorials if you're stuck:

https://docs.ros.org/en/foxy/Tutorials.html

https://roboticsbackend.com/category/ros2/


## getting setup
### (Native Ubuntu)
Install ROS 2 following the instructions here: https://docs.ros.org/en/foxy/Installation.html.

Next, create a workspace:
```
mkdir -p ~/lab1_ws/src
cd lab1_ws
colcon build
```
### Docker
If you can't have Ubuntu installed natively, install Docker on your system following the instructions here: https://docs.docker.com/get-docker/. The documentation of Docker can be found here.

Next, start a container with a bind mount to your workspace directory on your host system inside this repo by:

```
docker run -it -v <absolute_path_to_this_repo>/lab1_ws/src/:/lab1_ws/src/ --name f1tenth_lab1 ros:foxy
```

This will create a workspace directory on the host at <absolute_path_to_this_repo>/lab1_ws/src. It'll create the container based on the official ROS 2 Foxy image, and give the container a name f1tenth_lab1. You'll then have access to a terminal inside the container.








honestly i dont see the point of just redoing the lab manual. im done writing for now.



