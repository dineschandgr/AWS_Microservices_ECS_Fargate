# AWS_Microservices_ECS_Fargate
Deploying Microservices to AWS ECS Fargate

1. Create 3 separate fargate task definitions for 3 individual microservices
2. Add 3 containers for every service as follows
    1. Microservice Docker image from Docker Hub
    2. Xray docker image
    3. Envoy proxy docker image as side car pattern
3. Create a fargate service from the task definition
4. Configure load balancer and add listener and target group
5. Set load balancer health check path to actuator path
6.  Create a name space and enable service discovery for microservice as follows. The private dns is creatd in route 53.
    Every time a task ip is changed, the DNS is automatically updated
  
    1. movie-catalog-service.microservice.io (servicename.namespace)  
    2. movie-info-service.microservice.io (servicename.namespace)
    3. ratings-data-service.microservice.io (servicename.namespace)
    
7.  Use App mesh for managing microservices. Create the following

    1. Create mesh
    2. virtual node
    3. virtual service

8. Map the virtual node to the fargate service

Important Configurations

1. Add the security group of microservices containers to the RDS security group for port 3306 with type Myssql/Aurora
2. Exclude port 3306 in proxy configuration for app mesh
3. Provide environment variables for the Movie Info and Ratings data service in Movie catalog service


Refer to the following github repo for the source code and the steps to execute

https://github.com/dineschandgr/ratings-data-repo-codepipeline
https://github.com/dineschandgr/movie-info-repo-codepipeline
https://github.com/dineschandgr/movie-catalog-repo-codepipeline

https://github.com/dineschandgr/Microservices_Spring_Boot

Task Definition Config

<img width="500" alt="Task Def" src="https://github.com/dineschandgr/AWS_Microservices_ECS_Fargate/blob/master/containers_task_definition.png">


<img width="500" alt="Task def " src="https://github.com/dineschandgr/AWS_Microservices_ECS_Fargate/blob/master/containers_task_definition_1.png">

Service Config

<img width="500" alt="Service" src="https://github.com/dineschandgr/AWS_Microservices_ECS_Fargate/blob/master/Service.JPG">

Environment Variables

<img width="500" alt="Env Variables" src="https://github.com/dineschandgr/AWS_Microservices_ECS_Fargate/blob/master/env_variables.PNG">

Xray Distributed tracing

<img width="500" alt="Xray" src="https://github.com/dineschandgr/AWS_Microservices_ECS_Fargate/blob/master/microservices_xray.bmp">

<img width="500" alt="Xray" src="https://github.com/dineschandgr/AWS_Microservices_ECS_Fargate/blob/master/microservices_xray_1.bmp">
