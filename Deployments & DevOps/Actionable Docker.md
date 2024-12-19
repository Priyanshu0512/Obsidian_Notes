---

---
### What is Docker?

Docker is an open-source platform that uses **containerization** to package applications and their dependencies into lightweight, portable, and isolated environments called **containers**. These containers ensure that applications run consistently across different environments.

---
### Why is Docker Used?

1. **Portability**: Containers work on any system with Docker installed.
2. **Efficiency**: Lightweight and faster than virtual machines.
3. **Dependency Management**: Packages all dependencies, avoiding environment conflicts.
4. **Isolation**: Each container is independent, ensuring security and stability.
5. **Scalability**: Easily scale applications horizontally.
6. **DevOps Integration**: Enhances CI/CD pipelines for faster development and deployment.

---
## Docker Hub

Docker registries are similar to version control repositories for code, such as GitHub or GitLab, but instead of code, they store Docker images. Docker images are the blueprints for creating Docker containers, which include the application and all of its dependencies.
Docker Hub is the default registry for Docker and is analogous to GitHub in the context of Docker images. It's a cloud-based repository where users can sign up for an account, push their custom images, pull images published by others, and work with automated build workflows.

- **Version Control and Collaboration**: Just as GitHub allows developers to store, version, and collaborate on code, Docker Hub provides similar functionalities for Docker images. Users can keep track of different versions of their images, collaborate with team members, and integrate with continuous integration/continuous deployment (CI/CD) pipelines.
- **Public and Private Repositories**: Both platforms offer the ability to have public repositories, where anyone can access and use the resources, and private repositories, which are restricted to authorized users.
- **Automated Builds**: Docker Hub can automatically build images from source code in a repository when changes are made, similar to how CI/CD systems work with GitHub to automate the testing and deployment of code.

---
## Common Commands 

- `docker run <image-name>` - Downloads and builds the image.
- `docker ps` - This shows you all the containers that are currently running, providing details such as container ID, image used, command executed, creation time, status, and ports.
- `docker kill <container_id>` - Terminates the mentioned container.

> Note - While running docker run command the image will run in its own environment on the default port number which is different from the actual port number on the client. To direct the request from the port on the client machine to the port on which the image is running in its own environment Port mapping needs to be done.

- Adding a port mapping: By using `docker run -p 27017:27017 mongo` , you map the default MongoDB port (27017) from the container to the host.
- `-d` - The detached flag which run the docker image in the background in the detached mode.

- Mongo 
```bash
docker run -d -p 27017:27017 mongo
```

- Postgres 
```bash
docker run -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:5432 postgres
```

>This command runs a PostgreSQL container with a specified environment variable (-e) setting the default user's password to "mysecretpassword".


``` bash
 docker exec -it 36e25dc981fb /bin/bash
```
 
1. `docker exec`: Runs a command inside an already running Docker container.
2. **`-it`**:
    - `-i`: Interactive mode (keeps STDIN open).
    - `-t`: Allocates a pseudo-TTY (terminal).
3. **`36e25dc981fb`**: The container's ID (or name) where the command will be executed.
4. **`/bin/bash`**: Starts a Bash shell inside the container.

--- 
### TTY-shell

- A **TTY Shell** is a text-based shell running within a terminal session, allowing you to execute commands interactively.
- Modern systems emulate TTYs as **virtual terminals**. Ex - `bash` , `zsh`  or `zs` etc.

---
### Pseudo - TTY Shell

-  A **PTY** is a software-based terminal (emulated TTY). It bridges a process (e.g., a shell like Bash) with a terminal emulator.
- Docker uses a PTY to provide interactive terminal support for commands like `docker exec`.
- When you use the `-t` option with Docker commands (e.g., `docker exec -it`), Docker allocates a **pseudo-TTY** for the container.

---

### Running psql inside the container 

```bash
psql -h localhost -d postgres -U postgres
```

- **`-h localhost`**:
    - Specifies the **host** where the database server is running.
    - `localhost` means the database server is on the same machine as the client.
- **`-d postgres`**:
    - Specifies the **database name** to connect to.
    - In this case, it connects to the `postgres` database (the default database created during PostgreSQL installation).
- **`-U postgres`**:
    - Specifies the **username** for the database connection.
    - Here, the username is `postgres`, which is the default superuser in PostgreSQL.

---
