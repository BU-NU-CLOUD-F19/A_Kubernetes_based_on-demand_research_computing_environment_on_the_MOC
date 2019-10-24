# A Kubernetes based on-demand research computing environment on the MOC

### Visions and Goals of the Project
Sid is a research tool developed by the Harvard-MIT Data Center (HMDC) designed to give researchers a way to easily launch secure cloud-based scientific computing environments. Sid users can simply login to the web UI, select their desired computing environment (e.g., R Studio, Jupyter Notebook) and data source (e.g., Dataverse, Google Drive), and access it through their browser within minutes. In the background, Sid spawns a new Linux container, mounts the selected data source, and configures the network routes necessary for SSL-secured user access. This tool allows users to harness the storage and processing capabilites of a cloud platform without needing to know the ins and outs of Linux system administration or cloud computing.

Currently, teams at the HMDC are actively developing Sid and preparing it for launch sometime in late 2019. On launch, Sid's backend container infrastructure (i.e. the system for launching scientific computing containers upon user request) will be powered solely by Amazon Elastic Kubernetes Service (EKS). Our goal for this semester is to diversify Sid's infrastructure by porting it over to the Massachusetts Open Cloud (MOC) OpenShift cluster. By the end of the project, a Sid user will be able to launch the same scientific computing containers on MOC OpenShift that they can launch on Amazon EKS. And because Sid and OpenShift (via [okd](https://www.okd.io/)) are both open-source projects, other universities and research organizations will be able to set up their own instances of Sid without having to rely on (or pay for) Amazon's proprietary cloud infrastructure.

Our team will work closely with the HMDC to make this port possible. We will begin by installing Sid's node.js-based frontend and middleware on our local machines (for development) and on virtual machines in the MOC (for staging); in production, these components will run on Heroku. We will then set up a [minishift cluster](https://www.okd.io/minishift/) in our development environment and attempt to provision it with the objects (e.g., ServiceAccounts, Roles, etc.) normally used with Kubernetes on Amazon EKS. As we encounter incompatibilities preventing unmodified use of the Kubernetes objects on OpenShift (e.g., due to [incompatibility between OpenShift Routes and Kubernetes Ingress](https://blog.openshift.com/kubernetes-ingress-vs-openshift-route/)), we will modify or remake the objects to be compatible, or work with the HMDC to develop a workaround in the middleware. Each of these compatibility upgrade tasks will be assigned to 1-2 team members. As Sid and OpenShift are both complex platforms with several moving pieces, each team member will also spend significant time researching unfamiliar technologies and discussing with the HMDC team. Once we are able to successfully deploy Sid-on-OpenShift in both our development and staging environments, we will begin rollout on the MOC's production OpenShift cluster. 

### Open Questions & Risks
At the moment, our only open question is if there's any scenario where Sid's backend *needs* to be coupled to the infrastructure underlying the chosen orchestration platform (Kubernetes or OpenShift) that would need to be provisioned in some custom fashion with a tool like Ansible or Terraform. We plan to answer this question in our next meeting with our mentor.

Our main risk is that there is some fundamental incompatibility between Sid and OpenShift that would prevent our port from succeeding. In that unfortunate scenario, our backup plan is to create an automated way to deploy Sid on a "pure" Kubernetes cluster running on MOC virtual machines.

### Users/Personas Of The Project
- Although Sid's end users will primarily be scientists and researchers wishing to utilize cloud computing environments, as a backend project, our primary users are the administrators and developers of Sid.

- Sid's users should require no knowledge of the backend platforms on which their scientific computing containers are running. Our users (Sid administrators) should only need to know how to deploy a project on an OpenShift cluster in order to stand up their backend.

### Scope and Features of the Project
- Containerized scientific computing environment backed by the Massachusetts Open Cloud
- Modify Sid's current Kubernetes-based backend to run on OpenShift
- If necessary, modify Sid middleware to workaround OpenShift/Kubernetes incompatibilites
- Backup Plan: if unable to make Sid support OpenShift, create an automated way to deploy Sid on a "pure" Kubernetes cluster running on MOC VMs

### Solution Concept
The components which make up Sid can be viewed as three sections.  The front end is where the user interacts with the software and tells it the job they would like to run.  The middleware includes the components that interact with and control the Kubernetes. This section tells the backend how it should perform its computations and what the user has requested. The back end is where all of the actual containers are created (currently on AWS, but soon to be on the MOC). While Amazon EKS uses Kubernetes to orchestrate containers, the MOC uses OpenShift for this purpose. Since OpenShift is largely derivative of Kubernetes, the two platforms are mostly-compatible.

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
The success or failure of this project will be determined by whether or not we are able to successfully port Sid's current Kubernetes-based deployment over to OpenShift and deploy it on the MOC OpenShift cluster. In the event that this isn't possible, we plan to create an automated way to deploy Sid on a "pure" Kubernetes cluster running on MOC virtual machines.

### Release Planning
*Release 1 (Week 4)* - [Demo Slides](https://docs.google.com/presentation/d/1tONxR0E2NzLYkqCQG6fzuDhMQk2QpP-2fmViq-Ou81M/edit?usp=sharing)
- Stand up local development and MOC-staging environments containing Sid frontend, Sid middleware, and a clean install of minishift
- Begin attempted deployment of Sid backend on minishift development environments
  
 *Release 2 (Week 5)* - [Demo Slides](https://docs.google.com/presentation/d/1q-JB5S5ALB6MFz91jiJ9DxOGtkPKCC74TCi_kamO8As/edit?usp=sharing)
- Identify and document any incompatibilities preventing proper operation of Sid backend on OpenShift
- Begin compatibility upgrades

*Release 3 (Week 7)* - [Demo Slides](https://docs.google.com/presentation/d/125MDdIVHqzH7i-qDa3nRinpl7wkIrtO5x-3KIZQwHZE/edit?usp=sharing)
- Finish addressing incompatibilites that we can handle within OpenShift
- Begin working with HMDC to workaround any remaining incompatibilities in middleware
- Begin work with MOC staff to prepare for rollout on MOC production OpenShift cluster
    
*Release 4 (Week 9)*
- Sucessfully deploy Sid backend to staging environment
- Continue work with MOC staff to prepare for rollout on MOC production OpenShift cluster
    
*Release 5 (Week 11)*
- Rollout Sid backend on MOC production OpenShift
- Write end-to-end test cases for testing integration success
    
*Release 6 (Week 13)*
- Finalize documentation
- Complete switchover from using staging instances of Sid's frontend and middleware to production instances
- Handoff to HMDC team
