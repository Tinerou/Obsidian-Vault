#dockerNotes 

### **Quick Navigation**

- [[#What are Volumes?]]

---

### What are Volumes?
By default, Docker containers, don't retain any state from past containers. For example, if I:
1. Start a container from an image
2. Make some changes to the filesystem (like installing a new package) in that container
3. Stop the container
4. Start a new container from the same image
5. The new container does not have the changes I made in step 2.

Note: That if I restarted the stopped container, it will have the changes I made. 
restart != killing->starting

Docker does have ways to support "persistent state" through *storage volumes*.

**Storage Volumes:** A filesystem that lives outside of the container, but can be accessed by the container.

```bash
docker volume create <volume>
# Creates volume
docker volume ls
# Check volume
docker volume inspect <volume>
# See where the volume is on your local machine
```

To practice this I used Ghost. An open-source blogging software, kind of like Wordpress:
```bash
docker volume create ghost-vol
docker volume ls
docker volume inspect ghost-vol
docker pull ghost
# Pull the Ghost image from Docker Hub
docker run -d -e NODE_ENV=development -e url=http://localhost:3001 -p 3001:2368 -v ghost-vol:/var/lib/ghost ghost
# Run the Ghost image in a new container
```
- `-d` runs the image in detached mode to avoid blocking the terminal.
- `-e NODE_ENV=development` sets an [environment variable](https://en.wikipedia.org/wiki/Environment_variable) within the container. This tells Ghost to run in "development" mode (rather than "production", for instance)
- `-e url=http://localhost:3001` sets another environment variable, this one tells Ghost that we want to be able to access Ghost via a URL on our host machine.
- We've used `-p` before. `-p 3001:2368` does some [port-forwarding](https://en.wikipedia.org/wiki/Port_forwarding) between the container and our host machine.
- `-v ghost-vol:/var/lib/ghost` mounts the `ghost-vol` volume that we created before to the `/var/lib/ghost` path in the container. Ghost will use the `/var/lib/ghost` directory to persist stateful data (files) between runs.
- Navigate to `http://localhost:3001/` in your browser, you should see your new Ghost CMS!