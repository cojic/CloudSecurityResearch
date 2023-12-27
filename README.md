# ZOSS Project

R2 40/2023 Manojlović Jelena

R2 25/2023 Mihajlović Sara

## Cloud Security 

The research analyzes threats and risks in the use of Cloud technologies. The aim is to understand different types of threats that can impact systems relying on Cloud infrastructure and identify the most effective protection strategies. 

## Project goal
The aim of this research is to explore and understand the architecture of the Cloud and its individual components.

It is crucial to identify and analyze the security vulnerabilities of this system. By decomposing the entire system and considering its components, we need to identify key areas that could be potential targets for attacks. Some of the areas research will focus on API security and API gateway [[1]](https://www.akamai.com/glossary/what-are-api-security-risks), Database and Storage management [[2]](https://socradar.io/aws-s3-bucket-takeover-vulnerability-risks-consequences-and-detection/), identity providers [[3]](https://sonraisecurity.com/blog/9-common-iam-risks-how-to-mitigate-them/). Besides this, the interesting part of the research will be to analyze application activity and access logging. 

![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/cf835d7b-510c-4f0b-bdec-7b5e94d91803)

By creating a threat model, we aim to illustrate possible attacks and the strategies that attackers may employ and to propose protection strategies to mitigate or eliminate potential attacks.

## Overview 
* ### [Modules](documentation/module-decomposition.md)  
  The document provides an overview of the architecture of the Cloud and its components.
* ### [Amazon S3 Threat Model](documentation/amazon%20s3.md)
  The document provides an overview of the threats and attacks for Amazon S3.
* ### [MySQL Threat Model](documentation/mysql.md)
  The document provides an overview  of the threats and attacks for MySQL Database.
* ### [APIs Threat Model](documentation/apis.md)
The document provides an overview  of the threats and attacks for APIs. 

## Literature
1. [What Are API Security Risks?](https://www.akamai.com/glossary/what-are-api-security-risks)
2. [AWS S3 Bucket Takeover Vulnerability: Risks, Consequences, and Detection](https://socradar.io/aws-s3-bucket-takeover-vulnerability-risks-consequences-and-detection/)
3. [9 Common IAM Risks & How to Mitigate Them](https://sonraisecurity.com/blog/9-common-iam-risks-how-to-mitigate-them/)