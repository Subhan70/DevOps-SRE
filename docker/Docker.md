Docker : Docker is a platform used to create, run and manage the containers 

1.What is virtualization
2. What docker is solving ?

#Physical Server: Is nothing but the server which we bought (Eg: Cpu 16 cores, Ram: 64GB, Storage : 1TB)
- on top of it we install ubuntu or windows as per our requirment. [if installed O S uses 2gb, 4cores and 256gb], then remaining will be left unused 
- we are paying the money for the complete server, and unused space which we are wasting the resource 
- the companies don't want to waste this resource 
--------------------------------------------------------
##Virtualization was implemented.
 - Lets say if we have 3 applications: DB, frontend and UI/Backend
 - For 3 applications we buy 3 servers, then it is huge cost and also we may not use all the resources on the server.
 -  Virtualization comes in picture, We use install the required OS on one physical server, on the left over space avaibale in server 

Virtualization: is the process of creating multiple virtual computers (Virtual Machines) on a single physical server.
                
             Physical Server
      CPU 16 Core | RAM 64 GB | Disk 1 TB
                     │
                Hypervisor
      ┌────────┬────────┬
      VM1      VM2      VM3
    Ubuntu    Windows   CentOS
    Frontend   DB       Backend
  eg: Think of an Appartment, in this each flat has its own bedroom, watersuply, electricty, living room, Kitchen - Same as Each VM has its own RAM, CPU, Memory 

-------------------------------
Hypervysor: is the software that creates and manages the VM 
 eg: VM ware ESX, Microsoft Hyper-V, Oracle virtual Desktop
-------------------------------------
Docker : A platform for building, shipping, and running applications in containers.

Docker Image: A Docker Image is a lightweight, standalone and executable software package that includes everything needed to run an application: the code, a runtime, system tools, libraries and settings.
 - A read-only blueprint that contains everything needed to run an application.
Docker Container: A running instance of an Docker image
------------------------
**Docker Networking**
Networking allows containers to communicate with each other and with the host system. Containers run isolated from the host system and need a way to communicate with each other and with the host system.

By default, Docker provides two network drivers for you, the bridge and the overlay drivers.
docker network ls
eg output 
 NETWORK ID          NAME                DRIVER
xxxxxxxxxxxx        none                null
xxxxxxxxxxxx        host                host
xxxxxxxxxxxx        bridge              bridge

Bridge Networking : The default network mode in Docker. It creates a private network between the host and containers, allowing containers to communicate with each other and with the host system.

If we want to secure your containers and isolate them from the default bridge network we can also create our own bridge network, by using below command:
 docker network create -d bridge my_bridge

after creating the network if we list the network by docker network ls , the example output as below 
 docker network ls

NETWORK ID          NAME                DRIVER
xxxxxxxxxxxx        bridge              bridge
xxxxxxxxxxxx        my_bridge           bridge
xxxxxxxxxxxx        none                null
xxxxxxxxxxxx        host                host

-> This new network can be attached to the containers, when you run these containers, by below command 
docker run -d --net=my_bridge --name db training/postgres (update the repository and image and network name accordingly)
This way, you can run multiple containers on a single host platform where one container is attached to the default network and the other is attached to the my_bridge network. These containers are completely isolated with their private networks and cannot talk to each other.
-> However, you can at any point of time, attach the first container to my_bridge network and enable communication
 docker network connect my_bridge web

----------------
**Host Networking** : 
This mode allows containers to share the host system's network stack, providing direct access to the host system's network.

To attach a host network to a Docker container, you can use the --network="host" option when running a docker run command. When you use this option, the container has access to the host's network stack, and shares the host's network namespace. This means that the container will use the same IP address and network configuration as the host.

Here's an example of how to run a Docker container with the host network:

docker run --network="host" <image_name> <command>

Keep in mind that when we use the host network, the container is less isolated from the host system, and has access to all of the host's network resources. This can be a security risk, so use the host network with caution.

-------------------------
**Overlay Networking**
This mode enables communication between containers across multiple Docker host machines, allowing containers to be connected to a single network even when they are running on different hosts.

-----------------
**Docker Volumes** : containers will get destroyed sometimes, when they got crashed at that point, if we stored our data on the container, then it is difficult to bring the data back, so to overcome this we have a solution called volumes 

There are 2 different ways how docker solves this problem.
1. Volumes
2. Bind Directory on a host as a Mount

1.Volumes

-> Volumes aims to solve the same problem by providing a way to store data on the host file system, separate from the container's file system, so that the data can persist even if the container is deleted and recreated.

-> Volumes can be created and managed using the docker volume command. You can create a new volume using the following

command:
"docker volume create <volume_name>"
-> Once a volume is created, you can mount it to a container using the -v or --mount option when running a docker run command.

For example:
"docker run -it -v <volume_name>:/data <image_name> /bin/bash"

-> This command will mount the volume <volume_name> to the /data directory in the container. Any data written to the /data directory inside the container will be persisted in the volume on the host file system.

2. Bind Directory on a host as a Mount : Bind mounts also aims to solve the same problem but in a complete different way.

-> Using this way, user can mount a directory from the host file system into a container. Bind mounts have the same behavior as volumes, but are specified using a host path instead of a volume name.

-> For example : "docker run -it -v <host_path>:<container_path> <image_name> /bin/bash"

-------------------------------------------
Key Differences between Volumes and Bind Directory on a host as a Mount

-> Volumes are managed, created, mounted and deleted using the Docker API. However, Volumes are more flexible than bind mounts, as they can be managed and backed up separately from the host file system, and can be moved between containers and hosts.

-> In a nutshell, Bind Directory on a host as a Mount are appropriate for simple use cases where you need to mount a directory from the host file system into a container, while volumes are better suited for more complex use cases where you need more control over the data being persisted in the container.
