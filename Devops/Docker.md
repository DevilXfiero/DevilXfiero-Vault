## Motivation for Containers
| Development                                                                                                                       | Deployment                                                                              |
| --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| To get development env setup instead of running multiple commands <br>and configurations in local <br><br>"Run docker compose up" | To deploy the application <br><br>"Run the container images with different configs"<br> |
|                                                                                                                                   |                                                                                         |

A Docker container image is  a lightweight, standalone, executable package of software that includes everything needed to run an application.


Container image - class ( contains config, code)
Container - running instance of image

Open Container Initiative (OCI)
creating open industry standards around container formats and runtimes

Evolution of Virtualization 

1. Bare Metal - Running application on same OS 
2. Virtual Machines - Hypervisor (Combination of Software and hardware used to distribute resources in different pools to create isolated Virtual Machines) 
   Two types - 
   a. Hypervisor above OS (different boot that current OS) VMware
   b. Hypervisor with OS (Virtual Box)
   
3. Containers 
   Container Runtime - Software required to run container images in OS.
   Sharing kernel with host OS compare to VM you have your own kernel and OS
   Desktop Container Platforms - docker, podman
   Container Runtimes - containerd, cri-o

Virtual Machines + Containers
How to manage different containers inside different VMs ? 

Orchestrators - Kubernetes, Nomad, hashicorp
System design to take containers and run, manage and schedule them across multiple nodes (VMs).



### 1️⃣ `docker build`

- Reads `Dockerfile`
- Creates an **image**
- Image = frozen snapshot

### 2️⃣ `docker run`

- Starts a **container**
- Container = running Linux process
    

### 3️⃣ Port mapping

`-p 8000:8000`

Means:

`Laptop:8000 → Container:8000`

### 4️⃣ Why this matters for AI apps

- Tomorrow you’ll add:
    
    - PostgreSQL
    - Vector DB
    - Redis
        
- All will talk via Docker networking
    

---

# 🧪 Common Debug Commands (Memorize These)

docker ps              # running containers
docker ps -a           # all containers 
docker images          # images 
docker logs <id>       # logs 
docker stop <id>       # stop container

---

# 🔐 Small Improvement (Optional but Pro)

Run container in background:

`docker run -d -p 8000:8000 second-brain`

Then:

`docker ps docker logs <container_id>`

Dockerfile defines how a service is built, while docker-compose defines how multiple services are deployed and communicate together. Dockerfile focuses on image creation, docker-compose focuses on runtime orchestration.



Docker allows us to deploy our applications inside "containers", which are kind of like _very_ lightweight virtual machines. Instead of just shipping an application, we can ship an application _and the environment it runs in_.

## Container 
