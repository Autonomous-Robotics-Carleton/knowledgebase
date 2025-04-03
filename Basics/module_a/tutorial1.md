associated video: https://youtu.be/EU-QaO6xTv4


extremely important. will be going over the basis of how ROS2 works. also docker as well i guess.

For those who arent familiar with what docker is, you are going to learn :)

[200~Absolutely — let’s break it down simply.

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

