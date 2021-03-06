# DockerCMS Restful API
A container management system (DockerCMS) using a restful API that manages containers, images, services and stacks by defining several routes for each task.

#### DockerCMS Restful API Video Demo

- Click on the image below to play the video.

[![Video](http://img.youtube.com/vi/5am1bRk3_lU/0.jpg)](https://youtu.be/5am1bRk3_lU)

### Available API endpoints:

| **Method**       | **Endpoint**      | **About**      |
| -------------  | ------------- |:-------------:|
| GET| /containers | List all containers |
| GET| /containers?state=running  | List running containers (only)  |
| GET| /containers/id  | Dump specific container logs |
| GET| /containers/id/logs | List all containers |
| GET| /services  | List all service  |
| GET| /nodes  | List all nodes in the swarm  |
| GET| /images  | List all images |
| POST| /images | Create a new image |
| POST| /containers | Create a new container |
| PATCH| /containers/id | Change a container's state  |
| PATCH| /images/id | Change a specific image's attributes |
| DELETE| /containers/<id> | Delete a specific container |
| DELETE| /images/id | Delete all containers (including running)  |
| DELETE| /images/id | Delete a specific image  |
| DELETE| /images/id | Delete all images |
  
### How to Run

1. Clone this repo into your VM.
2. Change your directory (CD) into the repo.
3. Change your directory (CD) into the **my_application** folder.
4. Run: python **container-server.py** (Make sure to have pip installed).
5. Visit: **35.205.198.91:8080** and you will see the index page.
6. Read the index page.
7. Example: **To list all images visit the route: http://35.205.198.91:8080/images**
8. Go to: http://35.205.198.91:8080/images and you will see all the images.

**Note:** The IP 35.205.198.91 and port 8080 are examples used to test this API.
                                                                                              
### Docker Swarm

- Created with one mananger and two workers.
- Tested with NGINX as a service.

### DockerCMS Using a Restful API.

- In the **my_application** folder and named **container-server.py**.

### Running the NGINX as a service in Docker swarm. (Uses Manager and Two Workers)

- ```sudo docker swarm init```
- Get the code and copy and paste that code into the workers.
- To check they have joined: ```docker node ls```
- Creating: NGINX Web Server ```docker service create --replicas 5 -p 80:80 --name service1 nginx```
- To check: docker service ps service1

### Testing the DockerCMS

To test this API using Python go into the **Testing** folder to view all 16 tests. Another way to test is by using *curl* which can be viewed below.

#### Main Page (Index)

| **Test Type**  | **Command**   |
| -------------  |:-------------:|
| Main Page      | ```curl http://35.205.198.91:8080```  |

#### GET

| **Test Type**  | **Command**   |
| -------------  |:-------------:|
| View Containers      | ```curl http://35.205.198.91:8080/containers```  |
| View Running Containers      | ```curl http://35.205.198.91:8080/containers?state=running```  |
| Inspect a Specific Container      | ```curl http://35.205.198.91:8080/containers/<ID>```  |
| Dump Specific Container Logs.      | ```curl http://35.205.198.91:8080/containers/<ID>/logs```  |
| List All Service      | ```curl http://35.205.198.91:8080/services```  |
| List All Nodes in the Swarm      | ```curl http://35.205.198.91:8080/nodes```  |
| List All Images      | ```curl http://35.205.198.91:8080/images```  |

#### POST

| **Test Type**  | **Command**   |
| -------------  |:-------------:|
| Create a New Image      | ```curl -H 'Accept: application/json' -F file=@Dockerfile http://35.205.198.91:8080/images```  |
| Create a New Container      | ```curl -X POST -H 'Content-Type: application/json' http://35.205.198.91:8080/containers -d '{"image": "my-app"}'```  |

#### PATCH

| **Test Type**  | **Command**   |
| -------------  |:-------------:|
| Change a Container’s State      | ```curl -X PATCH -H 'Content-Type: application/json' http://35.205.198.91:8080/containers/b6cd8ea512c8 -d '{"state": "running/stopped"}'```  |
| Change a Specific Image’s Attributes      | ```curl -s -X PATCH -H 'Content-Type: application/json' http://35.205.198.91:8080/images/7f2619ed1768 -d '{"tag": "test:1.0"}'```  |

#### DELETE

| **Test Type**  | **Command**   |
| -------------  |:-------------:|
| Delete a Specific Container      | ```curl -s -X DELETE -H ‘Content-Type: application/json’ http://35.205.198.91:8080/containers/b6cd8ea512c8```  |
| Delete All Containers Including Running Ones      | ```curl -s -X DELETE -H ‘Content-Type: application/json’ http://35.205.198.91:8080/containers```  |
| Delete a Specific Image      | ```curl -s -X DELETE -H ‘Content-Type: application/json’ http://35.205.198.91:8080/images/7f2619ed1768```  |
| Delete All Images      | ```curl -s -X DELETE -H ‘Content-Type: application/json’ http://35.205.198.91:8080/images```  |
