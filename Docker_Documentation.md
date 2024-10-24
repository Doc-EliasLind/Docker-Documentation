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
      - [Restart](#restart)


---

## List of common syntax
This is to be used with Powershell, Visual Studio Code & Docker Desktop. 

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
>>>> - "8080:80"

#### Restart
Specifies whether or not the service can restart after composing services. 

> Services:
>> website:
>>> image:  nginx:latest
>>> ports:
>>>> - "8081:80"
>>>restart: always

---

SQL Injection Testing with DVWA and SQLNinja
To perform SQL Injection testing on a Dockerized environment, the following tools and steps are used:

Environment Setup:
Use Docker Compose to create two containers:

DVWA: A vulnerable web application running on a PHP/MySQL stack.
Kali Linux: A penetration testing environment containing security tools, including SQLNinja.
Network Configuration:
Both containers must be attached to the same Docker network to facilitate communication between the penetration testing container (Kali Linux) and the target application (DVWA). This can be configured within the docker-compose.yml file.

SQLNinja Configuration:
The SQLNinja configuration file (sqlninja.conf) should be modified to target the DVWA login page or any vulnerable endpoint. The key configuration parameters include:

Target URL (target) and vulnerable parameter.
HTTP request method (GET or POST).
SQL injection point specified by __SQL2INJECT__ in the HTTP request.
Example configuration snippet:


>ini
>--httprequest_start--
>GET http://172.18.0.3/login.php?id=1'__SQL2INJECT__ HTTP/1.1
>Host: 172.18.0.3
>User-Agent: Mozilla/5.0
>--httprequest_end--
>Wordlist-based Attack:
>For brute-force attacks, a custom wordlist can be created (e.g., wordlist.txt). This file should be placed in the appropriate directory (e.g., /etc/wordlist.txt), and SQLNinja can be run with the -w flag to specify the wordlist:


>bash
>sudo sqlninja -m b -f /etc/sqlninja.conf -w /etc/wordlist.txt
>Burp Suite Integration:
>Burp Suite can be used to intercept and modify HTTP requests. By capturing requests sent to the DVWA instance, the SQL injection vector can be identified and refined before being used with SQLNinja.

Testing Outcome:
SQLNinja and Burp Suite enable extraction of database information and testing for vulnerabilities. This process highlights the interaction between Docker containers for security testing within isolated environments.

This process integrates Docker Compose, container networking, and security testing into a practical workflow for SQL injection vulnerability assessments in web applications.