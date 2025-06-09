### 2. Managing Multiple Containers

Once I had the basics down, I wanted to try spinning up **multiple containers at once** — this helped me see how Docker handles networking, ports, and naming across instances. I also got more comfortable starting, stopping, and removing containers from the command line.

This phase was all about **exploring Docker’s multi-container behavior manually**, before getting into orchestration tools like Compose.


I wanted to experiment with running multiple instances of the `httpd` container.

* I ran 3 instances of `httpd`:  

  ```bash
  docker run -d -p 8081:80 --name web1 httpd:2.4.62

  docker run -d -p 8082:80 --name web2 httpd:2.4.62
  
  docker run -d -p 8083:80 --name web3 httpd:2.4.62
  ```
  I saw three container IDs printed out, confirming they started successfully.

* Then, I listed all running containers:

  ```bash
  docker ps
  ```

* Note: If you don't specify a name for your container, docker will assign a quirky name, typically an adjective plus a famous scientist or hacker’s name (j/k).

* I stopped all containers one by one:

  ```bash
  docker stop web1
  docker stop web1
  docker stop web2
  ```
 
  Docker confirmed each container was stopped by printing their names.

* For a quicker way to stop all containers at once, you can run:

  `bash
  docker stop $(docker ps -aq)
  `
  This command stopped every container Docker knew about by listing all container IDs (`docker ps -aq`) and passing them to `docker stop`.


* To remove all deleted containers in one go use:

  ```bash
  docker rm $(docker ps -aq)
  ```
  Docker listed the IDs or names of all the containers it removed.

---

### 3. Interactive Mode & Image Management

I also explored interactive mode and how to manage Docker images.

* To get a feel for interactive mode, I ran the `alpine` container interactively and listed the contents of its root directory:

  ```bash
  docker run -it alpine ls /
  ```
  This showed me the directory listing inside the container’s root.

* I listed all the Docker images on my system:

  ```bash
  docker images
  ```
  I saw a table with image names, tags, IDs, creation dates, and sizes.

* To clean up, I deleted the `alpine` and `nginx` images (after pulling `nginx` if I didn’t have it already):

  ```bash
  docker rmi alpine nginx
  ```
  Docker confirmed the images were removed.

* Finally, to delete all images locally, I ran:

  ```bash
  docker rmi $(docker images -aq)
  ```
  This command removed all images on my machine by listing all image IDs and deleting them. I made sure to use this carefully since it deletes everything!


### Useful Commands:
```bash
docker run -d -p 8081:80 --name web1 httpd:2.4.62    (example)
docker stop web1                                     (stop a container)
docker rm web1                                       (remove a container)
docker stop $(docker ps -aq)                         (stop all containers)
docker rm $(docker ps -aq)                           (remove all containers)
docker run -it alpine ls /                           (example: interactive alpine shell)
docker exec -it web1 bash                            (access running container)
docker images                                        (list all images)
docker rmi alpine nginx                              (example: remove specific images)
docker rmi $(docker images -aq)                      (remove all images)
```
