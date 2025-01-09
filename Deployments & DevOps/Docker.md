
> Note - The basis of Docker is covered in [[Actionable Docker]].

---
## Containers 

In Docker, **containers** are **lightweight, standalone, and executable software** units that include everything needed to run an application: **code, runtime, libraries, and dependencies**. Containers ensure that an application behaves consistently regardless of the environment in which it runs.

They can be thought of as isolated environments or sandboxes for running applications.

#### How Docker Containers Work

1. **Built from Images**:
    - A container is created from a **Docker image**, which is a lightweight, immutable blueprint that includes application code, dependencies, and configuration.
2. **Shared Kernel**:
    - Containers use the host system's OS kernel, which allows them to be lightweight while maintaining isolation.
3. **Namespaces and Control Groups (cgroups)**:
    - Docker uses Linux features like namespaces for isolation and control groups for resource allocation.

>Control groups, often abbreviated as **cgroups**, are a Linux kernel feature that allows you to limit, prioritize, isolate, and monitor system resources (such as CPU, memory, disk I/O, and network) used by processes. They are particularly important in containerization platforms like Docker, where resource control is essential.

1. `Docker Engine` - Docker Engine is an open-source `containerization` technology that allows developers to package applications into `container`
2. `Docker CLI` - The command line interface lets you talk to the `docker engine` and lets you start/stop/list containers.
3. `Docker registry` - The `docker registry` is how Docker makes money.It is similar to `github`, but it lets you push `images` rather than `sourcecode`

---

### Images vs Containers 

**Docker Image** - 
A Docker image is a lightweight, standalone, executable package that includes everything needed to run a piece of software, including the code, a runtime, libraries, environment variables, and config files.

**Docker Container** - 
A container is a running instance of an image. It encapsulates the application or service and its dependencies, running in an isolated environment.

---

![[Pasted image 20250107193450.png]]


---

## DockerFile 

A Dockerfile is a text document that contains all the commands a user could call on the command line to create an image.

A dockerfile has 2 parts
1. Base image
2. Bunch of commands that you run on the base image (to install dependencies like Node.js)

```dockerfile

FROM node:20

WORKDIR /app

COPY . .

RUN npm install
RUN npx prisma generate
RUN npm run build

EXPOSE 3000

CMD ["node", "dist/index.js"]

```

The command `COPY . . `

1. Source (.)- The first . represents the current directory on the host machine (where the Dockerfile is located or the docker build command is run).It specifies what to copy.
2. Destination (.)- The second . represents the current working directory inside the Docker image (set by WORKDIR, or by default /).
### Common commands

- `WORKDIR`: Sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY` instructions that follow it.
- `RUN`: Executes any commands in a new layer on top of the current image and commits the results.
- `CMD`: Provides defaults for executing a container. There can only be one CMD instruction in a Dockerfile.
- `EXPOSE`: Informs Docker that the container listens on the specified network ports at runtime.
- `ENV`: Sets the environment variable.
- `COPY`: Allow files from the Docker host to be added to the Docker image

---

### Building Images 

```bash
docker build -t [repository_name]:[tag] .
```

The `-t` flag assigns a **repository name** and **tag** to the image being built. The syntax is:

- `repository_name`: The name of the Docker image.
- `tag`: (Optional) The version of the image (default is `latest` if omitted).
- `.`: Specifies the build context, typically the current directory.

---

## Layers in Docker 

In Docker, layers are a fundamental part of the image architecture that allows Docker to be efficient, fast, and portable. A Docker image is essentially built up from a series of layers, each representing a set of differences from the previous layer.

### How Layers Are Created
 
1. **Base Image**:
    - The first layer in a Docker image is usually a base image (e.g., `ubuntu`, `alpine`, `node`).
    - This layer contains the minimal operating system files or runtime environment required for the application.
    
2. **Instructions in Dockerfile**: Each instruction in the Dockerfile creates a new layer. Common instructions include:
    - **`RUN`**: Executes commands in the shell and creates a new layer with the resulting filesystem changes.
    - **`COPY`/`ADD`**: Adds files from the build context or URL into the image, creating a new layer.
    - **`ENV`**: Sets environment variables in a new layer.
    - **`CMD`/`ENTRYPOINT`**: Sets up the default command for the container but doesn’t create a new filesystem layer.
    
3. **Union File System**: Docker uses a union filesystem (e.g., OverlayFS) to stack layers and present them as a single coherent filesystem to the container. The layers are read-only, with the top layer being writable for container runtime changes.

---

#### Layer Optimization and Caching

Docker caches each layer during the build process. If a layer hasn’t changed, Docker reuses the cached version to speed up builds.

> Note- Place frequently changing instructions (e.g., `COPY`) at the end of the Dockerfile to maximize caching.

>Docker layers are shared across images. If two Dockerfiles use the same base image or `RUN` commands, Docker reuses the cached layers.

---

### Layers During Runtime

When a container runs:

1. **Read-Only Layers**: The image layers remain read-only.
2. **Writable Layer**: Docker adds a thin, writable layer (the "container layer") on top of the image layers. Changes made during container runtime (e.g., writing files) happen in this layer.

When the container is deleted, its writable layer is also removed, leaving the original image layers intact.

---

##  Optimizing Dockerfile

> Note - 💡 If a layer changes, all subsequent layers also change.

```dockerfile

FROM node:20

WORKDIR /usr/src/app

COPY package* .
COPY ./prisma .
    
RUN npm install
RUN npx prisma generate

COPY . .

EXPOSE 3000

CMD ["node", "dist/index.js", ]

```

1. We first copy over only the things that `npm install` and `npx prisma generate` need
2. Then we run these script.
3. Then we copy over the rest of the source code

This is because the dependencies in the project rarely change in comparison to the source code. Hence caching the dependencies which in turn  caches more layers for efficient build times.

---

## Networks

In Docker, **networks** enable communication between containers, the host machine, and external networks. Docker provides a built-in networking system to isolate and connect containers securely and efficiently.

Creating a Network and attaching containers to it - 
 ``` bash
docker build -t image_tag .
docker network create my_custom_network
docker run -d -p 3000:3000 --name backend --network my_custom_network image_tag
docker run -d -v volume_database:/data/db --name mongo --network my_custom_network -p 27017:27017 mongo
```

![[Pasted image 20250109134023.png]]

---

### Types of Docker Networks

Docker supports several network types, each suited for specific use cases:

1. **Bridge Network (Default)**:
    - Used for standalone containers running on a single host.
    - Containers on the same bridge network can communicate with each other directly.
    - By default, containers in the bridge network are isolated from the host and external networks unless explicitly exposed.

2. **Host Network**:
	- Shares the host's networking namespace.
	- Containers using the host network have direct access to the host's network interfaces and can bind to the host's IP address.
	- The ports which are opened on container are automatically to the port on the host machine hence no port mapping is required. (This can lead to port conflicts.)

	   `docker run --network host my_container`

3. **Overlay Network**:
	- Used in Docker Swarm or Kubernetes environments.
	- Enables communication between containers on different hosts by creating a virtual distributed network.
	- Requires a key-value store like `etcd` or `consul` to manage network state.

4. **None Network**:
	- Completely disables networking for the container.
	- The container has no access to external networks or other containers.

5. **Macvlan Network**:
	- Assigns a unique MAC address to the container, making it appear as a physical device on the network.
	- Containers can communicate directly with the host network and external systems.

---

## Volumes 

In Docker, **volumes** are a mechanism to persist data generated and used by containers. They allow you to store and share data between the container and the host or across multiple containers, ensuring that data remains available even after the container is deleted or stopped.

### Key Features of Docker Volumes

1. **Data Persistence**:
    - Volumes ensure that the data persists beyond the lifecycle of the container.
2. **Sharing Data**:
    - Volumes can be shared among multiple containers to enable shared access to the same data.

**Creating a Volume**

```bash
docker volume create volume_database
docker run -v volume_database:/data/db -p 27017:27017 mongo
```

---

### Scenario 1: New Volume Mounted on a New Container

- **Container Path**: Empty (no data).
- **Volume**: New, empty volume.
#### What Happens:
- No data copying occurs because both the container path and the volume are empty.
- Any subsequent writes to the container path are directly written to the volume.
#### Result:
- The volume becomes the data store.
- Data is written directly to the volume.
---
### Scenario 2: Empty Volume Mounted to a Container with Existing Data

- **Container Path**: Contains data (e.g., `file1.txt`, `file2.txt`).
- **Volume**: New, empty volume.
#### What Happens:
- Docker copies the existing data from the container path to the volume **on initialization**.
- The container then works directly with the volume's data going forward.
- The original container folder data is effectively replaced by the volume.
#### Result:
- Data is **copied from the container** to the volume.
- All subsequent writes and reads are performed on the volume.
---
### Scenario 3: Non-Empty Volume Mounted to a Container with Existing Data

- **Container Path**: Contains data (e.g., `file3.txt`).
- **Volume**: Non-empty volume (e.g., contains `fileA.txt`, `fileB.txt`).
#### What Happens:
- The volume's contents **overwrite** the container path.
- The original container data (`file3.txt`) is **not copied** to the volume; it is effectively **lost** unless it was backed up.
- The container now sees and interacts only with the data from the volume (`fileA.txt`, `fileB.txt`).
#### Result:
- The container's original data is ignored (not copied to the volume).
- All subsequent writes and reads are performed on the volume.


>Note - If the volume already contains data then volume data takes precedence over the data already present in the container. Though the data inside the container is not deleted but remains their , it only takes takes lower precedence over the volume data.

---

### How Containers Can Share the Same Port Number in a Docker Network:

1. **Container-Level Networking:**
    - Inside a Docker network, each container has its own isolated network stack, including its own internal IP address.

2. **No Conflict Between Containers in a Network:**
	- Since containers have unique internal IPs within a network, they can all bind to the same port (e.g., port `80`) without conflict.

> Note - **You cannot map multiple containers to the same host port.** For example, if `container1` maps `80` to `8080` on the host (`-p 8080:80`), you cannot map  `container2` to the same host port (`8080`) since it would conflict with `container1`.

---

# Docker-Compose 

Docker Compose is a tool designed to help you define and run multi-container Docker applications. With Compose, you use a YAML file to configure your application's services, networks, and volumes. Then, with a single command, you can create and start all the services from your configuration.


```yaml
version: '3.8'
services:
  mongodb:
    image: mongo
    container_name: mongodb
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db

  backend22:
    image: backend
    container_name: backend_app
    depends_on:
      - mongodb
    ports:
      - "3000:3000"
    environment:
      MONGO_URL: "mongodb://mongodb:27017"

volumes:
  mongodb_data:

```

Running the docker-compose.yaml file 

```bash

docker-compose up

//To stop everyting including volumes.
docker-compose down --volumes
 
```

---

