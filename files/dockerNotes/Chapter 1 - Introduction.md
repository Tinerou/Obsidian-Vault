#dockerNotes

### **Quick Navigation**

- [[#What is Docker?]]
- [[#3 Parts of Docker]]
- [[#Docker Hub]]

---
### What is Docker?

Docker is the big name in "containerization". The big idea behind Docker and other container technologies is that they allow us to package our programs _with an environment_ and ship the whole thing. Most real world programs don't work in isolation, they need:

- Files from disk
- Environment variables
- Installed dependencies
- Specific permissions

Docker allows us to deploy our applications inside "containers", which are kind of like ***very*** lightweight virtual machines.

Instead of just shipping an application, we can ship an application and the environment it runs in.

### 3 Parts of Docker

1. The "**Docker Server**" or "**Docker Daemon**". Background process that listens to requests from the desktop app and executes them. If this isn't running nothing else will work.
2. The "**Docker Desktop**" GUI. Starting the GUI should start the server.
3. The **Docker CLI**. Recommended to use the GUI to visualize what's going on, but executing through the command line.

### Docker Hub

**Docker Hub** is the official cloud service for storing and sharing docker image.

There are alternatives. For example:

- AWS ECR
- GCP Container Registry
- Azure Container Registry
---