# A Kubernetes based on-demand research computing environment on the MOC

### Visions and Goals of the Project
  This project is a research tool for users who may not have a deep technical knowledge of computing systems. This tool allows the user to do secure computation on large data sets in a cloud environment without having to worry about how the backend cloud processing is being done. Our goal for this project is to move this infrastructure from AWS onto the Mass Open Cloud and create a configuration script using Terraform to automate the setup of these cloud services so that other institutions can use set up their own secure computing environments on the MOC if they wish.
  
  The approach that our team has decided on for this project is to split up the various new technologies involved in this project among our team members. Each member will then learn about their respective technology and we will all join back together to share the findings of each member. At this stage, we will try to experiment with running simple tasks on each of these technologies (Running a simple task on the cloud, running a simple task in a container, etc.). Once each technology has been sufficiently explored we plan to work on starting to move pieces of the current implementation to the MOC. Each member will focus primarily on the technology that they spent time researching in the earlier stages and once individual pieces start to come together we plan to work on implementation testing. Towards the end of the project, if there is remaining time, we plan to automate the setup of this computing environment with Terraform so that if another institution wants to stand up their own computing environment on the MOC they can do so.

### Users/Personas Of The Project
- The end users are people who know the basic principles of programming but are not familiar with all other technologies that are provided in the MOC.

- The users should know how to program the instructions for processing their data but should not need deep knowledge of how the backend computations are actually happening

### Scope and Features of the Project
- Containerized computing environment stood up on the Mass Open Cloud
- Control the containers in the MOC with kubernetes ( Look into the red-hat implementation of kubernetes )
- Integrate with already existing middleware and frontend
- Stretch Goal - implement terraform to automate the control of containers

### Solution Concept
The components which make up Sid can be viewed as three sections.  The front end is where the user interacts with the software and tells it the job they would like to run.  The middleware includes the components that interact with and control the Kubernetes. This section tells the backend how it should perform its computations and what the user has requested. The back end is where all of the actual computation happens on the MOC. This section also includes kubernetes for controlling and managing container swarms.

![Alt text](https://github.com/BU-NU-CLOUD-F19/A_Kubernetes_based_on-demand_research_computing_environment_on_the_MOC/blob/master/images/front_middle_back.png)

This diagram shows at a very high level how a user interacts with Sid by requesting that Sid create a new job, and how Sid hands off the newly created job to the user to directly interact with

#### Front End 
- User AAA
- User Management
- User History
- How the user tells the tool what job they want to run
- Administrative Controls

#### Middleware 
- Heroku
- Launching and controlling jobs
- Logging

#### Back End 
![Alt text](https://github.com/BU-NU-CLOUD-F19/A_Kubernetes_based_on-demand_research_computing_environment_on_the_MOC/blob/master/images/layers.png)

### System Architecture
![Alt text](https://github.com/BU-NU-CLOUD-F19/A_Kubernetes_based_on-demand_research_computing_environment_on_the_MOC/blob/master/images/diagram.png)

### Acceptance criteria
The success or failure of this project will be determined by whether or not we are able to successfully move the backend computations for this tool to the MOC and maintain the same functionality that the tool currently has. Some stretch goals include automating the setup of this tool so that other institutions can set up similar frameworks with minimal work.

### Release Planning
*Release 1 (Week 4)*
- Be able to demonstrate something on MOC, Kubernetes and containers (exploratory phase)
  - MOC: Run a simple data processing computation on the MOC
  - Kubernetes: Manipulate one or more containers using Kubernetes
  - Containers: Create a container and run a program that has non-standard dependencies
  
 *Release 2 (Week 5)*
- Start creating teraform scripts for the various technologies

*Release 3 (Week 7)*
- Be able to use Kubernetes to create a container, and a working environment on MOC 
    
*Release 4 (Week 9)*
- Launch a sid container on the MOC and do some basic computation
    
*Release 5 (Week 11)*
- Write test cases for testing the success or failure of our integration between the frontend and backend
    
*Release 6 (Week 13)*
- Integrate the backend with the front end that has already been developed by the sid team.
    



