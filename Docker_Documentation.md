# Docker Documentation 
Elias Lind

---

## Table of contents
- [Docker Documentation](#docker-documentation)
  - [Table of contents](#table-of-contents)
  - [List of common syntax](#list-of-common-syntax)
      - [Start Docker](#start-docker)
      - [**Run Docker Container**](#run-docker-container)
  - [Docker Compose](#docker-compose)
      - [Services](#services)
      - [Image](#image)
      - [Ports](#ports)


---

## List of common syntax
This is to be used with Powershell.

---

#### Start Docker
> 


#### **Run Docker Container**
> A common command for creating a container. 
***Docker run -d -t [image name]***

Docker containers


Docker exec -it

---

## Docker Compose

#### Services
Defines the name of the underlying services that will compose and run, as soon as the Compose-file runs. 
> Services:
>> website:
>> kalilinux:

The names under Services can be completely custom; but keep this relevant. 

#### Image
Bases the services on an image - creating containers within the services, within the Docker-Compose-file.
> Services:
>> website:
>>> image: nginx:latest

#### Ports
Defines which ports the service will use. 
> Services:
>> website:
>>> image: nginx:latest
>>> ports: 
>>>> -- "8080:80"
