## Module Decomposition

### Cloud computing
Cloud computing means storing and accessing the data and programs on remote servers that are hosted on the internet instead of the computer’s hard drive or local server.

### Cloud architecture
Cloud architecture is the blueprint for how all the different parts of a cloud-based system fit together and work.<br>
Cloud architecture involves figuring out how to organize servers, databases, networks, and applications in the cloud.<br>

These components typically refer to a frontend, backend, and internet [[1]](https://www.geeksforgeeks.org/architecture-of-cloud-computing/).<br>
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/ce8a1631-7b64-43e8-b945-88fa9395af68)

#### Frontend
Frontend refers to the client side of a cloud computing system. It contains all the user interfaces and applications that are used by the client to access services/resources.

#### Internet
Internet connection acts as the medium between frontend and backend and establishes the interaction and communication between frontend and backend.
Alternatively, some organizations use intranet or intercloud as their network connection.

#### Backend
The backend, in a cloud environment architecture, refers to the very cloud itself. The backend systems enable the front end of cloud architecture to function.
Cloud service vendors build and develop these backend systems to host and manage their respective systems, applications, data, and other digital assets.

##### Application
Application in the backend refers to a software or platform to which the client accesses. This means it provides the service in the backend as per the client's requirement.

##### Service
Service in the backend refers to the major three types of cloud-based services SaaS, PaaS, and IaaS [[2]](https://www.cloudflare.com/learning/cloud/what-is-the-cloud/). Also manages which type of service the user accesses.<br>

##### Cloud runtime
Cloud runtime in the backend provides the execution and Runtime platform to the Virtual machine.

##### Storage
Storage in the backend provides flexible and scalable storage service and management of stored data. It handles tasks such as data replication, encryption, and ensuring high availability and durability of stored information.

##### Infrastructure
Cloud Infrastructure in the backend refers to the hardware and software components of the cloud like it includes servers, storage, network devices, virtualization software, etc.

##### Management
Management in the backend refers to the management of backend components like application, service, runtime cloud, storage, infrastructure, and other security mechanisms, etc.

##### Security
Security in the backend refers to the implementation of different security mechanisms in the backend for securing cloud resources, systems, files, and infrastructure to end-users.

### Cloud-based web application example
The following diagram illustrates a simplified version of a cloud-based microservice application.<br>
Each microservice functions as an AWS Lambda function [[3]](https://aws.amazon.com/lambda/), each having its instance of an SQL database. Microservices communicate via an SNS (Simple Notification Service) bus [[4]](https://aws.amazon.com/sns/).<br>
The identity provider is responsible for user management. The login flow, signup flow, token generation, etc, happen through it.<br>
Amazon Simple Storage Service (Amazon S3) [[5]](https://aws.amazon.com/s3/) is an object storage service, that was used to store assets. Cloudfront was used for managing multimedia in communication with the S3 bucket [[6]](https://aws.amazon.com/cloudfront/).<br>
AWS X-Ray [[7]](https://aws.amazon.com/xray/) integrates with CloudWatch [[8]](https://aws.amazon.com/cloudwatch/) for application health monitoring. Those tools make it easier for users to read, filter, and organize logs.<br>
Client-side functionalities are implemented through a mobile Android application and a web application built (Single Page Application). <br>
The API gateway intercepts all incoming client requests and sends them through the API management system, which handles a variety of necessary functions [[9]](https://aws.amazon.com/api-gateway/).

![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/ed55cfef-3c09-45c4-8942-8148dd37b9c3)

Android and web application users are accessing the server via the same path, which is shown in the following diagram. Android users access the server via an Android device, which has an application installed on it. Web users access the server via an application, that is placed on some domain.<br>
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/5eb94dce-1b26-4269-afb8-5024a41012e3)


## References
1. [Architecture of Cloud Computing](https://www.geeksforgeeks.org/architecture-of-cloud-computing/)
2. [What is cloud computing?](https://www.cloudflare.com/learning/cloud/what-is-the-cloud/)
3. [AWS Lambda](https://aws.amazon.com/lambda/)
4. [Simple Notification Service](https://aws.amazon.com/sns/)
5. [Amazon S3](https://aws.amazon.com/s3/)
6. [Amazon CloudFront](https://aws.amazon.com/cloudfront/)
7. [AWS X-Ray](https://aws.amazon.com/xray/)
8. [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/)
9. [API Gateway](https://aws.amazon.com/api-gateway/)
