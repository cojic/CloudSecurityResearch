## Module Decomposition

![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/0e82644d-0f67-4f95-9afd-e26032ed2808)

The diagram illustrates a cloud-based application comprising microservices. Client-side functionalities are implemented through a mobile Android application and a web application built with React. Each microservice functions as an AWS Lambda function, each having its instance of an SQL database. Storage is facilitated through an S3 bucket. An off-the-shelf identity provider solution facilitates user registration, login, and overall user management. Microservices communicate via an SNS (Simple Notification Service) bus.

The application operates on a multitenancy model, where each web user belongs to a distinct tenant, and their domain is exclusively contained within it. However, the database is shared among tenants, enabling efficient data management and access control across the application.

This serves as a simplified representation of the system we'll be using as a reference in our research.
