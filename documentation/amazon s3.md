# Cloud Security
# Amazon Simple Storage Service (Amazon S3)

Amazon S3 is an object storage service that stores data as objects within buckets.
When creating a bucket, the client needs to specify a bucket name and the AWS Region. AWS Region is a geographical area where AWS has data centers for storing data. Each AWS region is designed to be isolated from others. 
After creating a bucket the client can upload data to that bucket as objects. Each object is uniquely identified within the bucket by a key. This key serves as the object's unique identifier and can be used to access the object through an endpoint.

## Threat - Unauthorized access to sensitive data
Target resource - S3 bucket and it's data.
The attacker has the ability to access and read sensitive data, compromising the confidentiality of the 
data.

![image](/documentation/images/T1.png)

## Attacks

### Bucket Enumeration

Bucket enumeration is a process of identifying misconfigured S3 buckets that are publicly accessible. This process can be used as a part of security analysis, or for malicious intent, ant it aims to determine which objects are present within a given bucket. When an attacker successfully performs S3 bucket enumeration on misconfigured buckets, they can potentially gain access to various types of sensitive data depending on what is stored in those buckets.
There are several methods that can be used for finding S3 buckets. 
- AWS CLI can list all S3 buckets in some account with appropriate IAM credentials.
- Third party tools like Bucket Finder and S3 Scanner, and others can scan for publicly accessible buckets and display the results, including bucket names and associated URLs.


### Mitigates
#### Limit Public Access: 
- Apply S3 Block Public Access settings to prevent accidental public exposure of data, ensuring that only authorized users have access. 

#### Implement access control:   
- Use bucket policies that define who can access the bucket and what actions they can perform.  
- Implement Least Privilege: Apply strict IAM policies to users, groups, and roles.
- Use Object-Level Access Control: If it is required to manage ermissions for each object within a bucket independently use ACLs (Access Control Lists) that are applied at the object level.
- A bucket becomes vulnerable to this type of attack when it is made public, and for this reason, this practice should be avoided.

#### Enable Logging and Monitoring: 
- Enable access logging for S3 buckets and integrate them with AWS CloudTrail. This helps you monitor and detect any unauthorized access attempts or suspicious activities. Specifically CloudTrail can be used to detect actions for enumerating the contents of S3 bucket, monitoring changes in bucket policies, and tracking user activities.

#### Encrypt Sensitive Data:
- After public buckets are found, the attacker can see the data inside bucket. Use server-side encryption so Amazon S3 will encrypt objects before saving them and then decrypts the objects when download them.


### Data Exfiltration

Data exfiltration is a type of security breach that leads to the unauthorized transfer of sensitive data from the compromised S3 bucket to external endpoints.

After identifying misconfigured S3 buckets often achieved through the Bucket Enumeration, an attacker can find and exploit vulnerabilities of the S3 bucket by analyzing the security measures applied to the bucket. If the attacker gains unauthorized access to the bucket, he can use data exfiltration methods to transfer sensitive data.
One such method is leveraging S3 data replication, which allows the copying of objects to another bucket, or exfiltration through S3 Server Access Logs


### Mitigates

#### Acces Controll:
- As mentioned in the previous attack, it is essential to pay attention to configurations such as setting up IAM policies and Bucket-Level policies. 

#### Encrypt Sensitive Data:
- For protecting data at rest, and reducing the risk of unauthorized access to sensitive data can be used server-side encryption, as mentioned earlier

#### Enable Logging and Monitoring: 
- Similarly, analyzing CloudTrail logs it can be used to identify and respond to data exfiltration attempts by monitoring S3 data events, analyzing logs for unauthorized object copies.

#### "Write Once Read Many" model
- With S3 Object Lock, you can store objects by using a WORM model. S3 Object Lock can help prevent accidental or inappropriate deletion of data.
- S3 Object Lock can be used to help protect your AWS CloudTrail logs.

#### Consider using VPC endpoints for Amazon S3 access
- A virtual private cloud (VPC) endpoint for Amazon S3 is a logical entity within a VPC that allows connectivity only to Amazon S3. VPC endpoints provide multiple ways to control access to your S3 bucket, and help prevent traffic from traversing the open internet.


## Threat - Taking control over data
Target resource - S3 bucket and it's data.
The attacker has the ability to access, manipulate data, and take control of the bucket, compromising the confidentiality, integrity, and availability of the data. 

![image](/documentation/images/T2.png)

## Attacks
### Bucket Takeover
Bucket Takeover allows access over private storage and data inside it, and takes full control of the content within the bucket.

After identifying misconfigured S3 buckets, often achieved through the Bucket Enumeration attacker can now search for configuration settings and security measures implemented on the identified bucket, including IAM and bucket policies. If attacker can exploit found vounrabilities and gains unauthorized access to the bucket. If vulnerabilities are found, the attacker can exploit them to gain unauthorized access.
Upon successful unauthorized access, the attacker now has the ability to manipulate the bucket's configuration. This includes making changes to IAM roles, policies, and other settings. With this the attacker can effectively take control of the compromised S3 bucket.
Compromised buckets can further be used in other malicious activities including Exfiltration, Phishing and supply chain attacks, also attacker is now able to upload a malicious file into the bucket that can trigger a malware or ransomware across the network. 

### Mitigates
#### Acces Controll:
- As mentioned in the previous attacks, acces control is essential when configuring S3 bucket. 

#### Encrypt Sensitive Data:
- Using server-side encription. Server-side encryption can help reduce risk to your data by encrypting the data with a key that is stored in a different mechanism than the mechanism that stores the data itself.
- Using Client-side encryption – In this case, you manage the encryption process, the encryption keys, and related tools. This can aditionally help reduce risk to data.

#### Enable Logging and Monitoring: 
- Analyzing CloudTrail logs for changes to bucket configurations, unauthorized object copies, and tracking user activities can help in identifying potential takeover attempts, allowing for timely intervention, access revocation, and mitigation of security risks.


### Additional Mitigation - Use of AWS Trusted Advisor:
- Use AWS Trusted Advisor, which offers automated recommendations for securing resources like S3 buckets.


## Literature
1. [S3 Bucket Enumeration and Exploitation](https://www.geeksforgeeks.org/s3-bucket-enumeration-and-exploitation/)
2. [Misconfigured AWS S3 Bucket Enumeration](https://medium.com/@narenndhrareddy/misconfigured-aws-s3-bucket-enumeration-7a01d2f8611b)
3. [S3 Bucket Enumeration: Research and Insights](https://medium.com/@aka.0x4C3DD/s3-bucket-enumeration-research-and-insights-674da26c049e)
4. [Hidden Risks of Amazon S3 Misconfigurations](https://blog.qualys.com/vulnerabilities-threat-research/2023/12/18/hidden-risks-of-amazon-s3-misconfigurations)
5. [Exfiltrating S3 Data with Bucket Replication Policies](https://hackingthe.cloud/aws/exploitation/s3-bucket-replication-exfiltration/)
6. [AWS S3 Bucket Takeover Vulnerability: Risks, Consequences, and Detection](https://socradar.io/aws-s3-bucket-takeover-vulnerability-risks-consequences-and-detection/)
7. [Data Exfiltration through S3 Server Access Logs](https://hackingthe.cloud/aws/exploitation/s3_server_access_logs/)
8. [Security best practices for Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)
