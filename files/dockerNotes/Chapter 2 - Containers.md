#dockerNotes 

### **Quick Navigation**
- [[#VM's vs Containers]]
- [[#Images]]
- [[#Run a Container]]
- [[#Stop a Container]]
- [[#Multiple Containers]]
- 

---

**Container** = A standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.

### VM's vs Containers:
**Virtual Machines:**
- Slow 
- Virtualizes Hardware
**Containers:
- Fast
- Virtualizes OS

Note: Both containers and vm's have good isolation. Each container feels like it has its own operating and filesystem. In reality, a lot of resources are being shared, but they're being shared securely through `namespaces`.

![[Pasted image 20250920092406.png]]

### Images

**Image:** A read-only definition of a container
**Container:** An instance of a virtualized read-write environment

A container is basically an image that's **actively running**. In other words, you boot up a container _from_ an image. You can create multiple separate containers all from the same image (it's _kinda_ like the relationship between classes and objects).

Note: For servers people split the same image into separate containers 

### Run a Container

`docker run`

**Example:**

```bash
docker run -d -p hostport:containerport namespace/name:tag
```
- `-d`: Run in detached mode (doesn't block your terminal)
- `-p`: Publish a container's port to the host (forwarding)
- `hostport`: The port on your local machine
- `containerport`: The port inside the container
- `namespace/name`: The name of the image (usually in the format `username/repo`)
- `tag`: The version of the image (often the `latest`)

**Running containers:**

```bash
docker ps
```

- This checks what containers are running

One one of the columns you should see something similar to this:
```bash
PORTS
0.0.0.0:8965->80/tcp
```

- This is saying that port `8965` on your local "host" machine is being forwarded to port `80` on the running container. Port `80` is conventionally used for HTTP web traffic. Navigate to `http://localhost:8965` and you should see a webpage served from the container!

### Stop a Container

**There are two primary ways:**

- `docker stop <CONTAINER_ID>`: This stops the container by issuing a `SIGTERM` signal to the container. You'll typically want to use `docker stop <CONTAINER_ID>`.

- `docker kill <CONTAINER_ID>`: This stops the container by issuing a `SIGKILL` signal to the container. This is a more forceful way to stop a container, and should be used as a last resort.

Remember: use `docker ps` this will show your running container ID's

**Restarting != Killing->Starting

A common misconception by developers.

Killing and starting: Resets the state of the entire machine to the entire image.

Restarting: Will keep the state of the machine.

### Multiple Containers

Remember, Docker containers are very lightweight. It's normal to run many containers on a single host machine.

Each container is in it's own isolated environment.
Multiple containers of an image are running separate instances.

We have to use different host ports for different containers because two processes can't bind to the same port on the OS.
Example:
```bash
docker run -d -p 8965:80 docker/getting-started
docker run -d -p 8966:80 docker/getting-started
docker run -d -p 8967:80 docker/getting-started
docker run -d -p 8968:80 docker/getting-started
docker run -d -p 8969:80 docker/getting-started
```
