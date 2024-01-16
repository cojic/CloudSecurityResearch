# Cloud Security
# Amazon Simple Storage Service (Amazon S3)

S3 is an object-level storage service.
Objects are a name/value pair of data or the ”contents” and the metadata. The container
storing the objects is called a ”Bucket”. The buckets are the highest-level namespace
in AWS.
When creating a bucket, the client needs to specify a bucket name and the AWS Region. AWS Region is a geographical area where AWS has data centers for storing data. Each AWS region is designed to be isolated from others. 
After creating a bucket the client can upload data to that bucket as objects. Each object is uniquely identified within the bucket by a key. This key serves as the object's unique identifier and can be used to access the object through an endpoint.

## Threat - Unauthorized access to sensitive data
Target resource - S3 bucket and its data.
The attacker can access and read sensitive data, compromising the confidentiality of the 
data.

![image](/documentation/images/T1.png)

## Attacks

### Bucket Enumeration

Bucket enumeration is a process of identifying misconfigured S3 buckets that are publicly accessible. This process can be used as a part of security analysis, or for malicious intent, to determine which objects are present within a given bucket. When an attacker successfully performs S3 bucket enumeration on misconfigured buckets, they can potentially gain access to various types of sensitive data depending on what is stored in those buckets.
Several methods can be used for finding S3 buckets. 

The attacker will target a misconfigured bucket. Some of the ways to locate them are by using Google Dorks, AWS CLI tools, CLI tools from Github, and websites.

#### Using Google Dorks to find S3 buckets
Google Dorks are powerful search queries that allow you to find specific information on the internet. <br>
Google Dorking, also known as Google hacking, can return information difficult to locate through simple search queries. This includes information not intended for public viewing, but that is inadequately protected and can, therefore, be "dorked" by a hacker.

You can use Google Dorks to discover S3 buckets associated with Amazon Web Services. Here are a couple of examples: 

**site:http://amazonaws.com inurl:".s3.amazonaws.com/"**
1. site:http://amazonaws.com: This part restricts the search to the domain "amazonaws.com." The site: operator is used to specify a particular domain or site where the search should be performed.
2. inurl:".s3.amazonaws.com/": This part of the query focuses on the URL structure. The inurl: operator is used to search for a specific string within the URL. In this case, it looks for URLs containing ".s3.amazonaws.com/". The . before "s3" is used to ensure that it is a specific part of the URL and not just any occurrence of "s3."

**site:http://s3.amazonaws.com intitle:index.of.bucket** 
1. site:http://s3.amazonaws.com: This restricts the search to the specified site, in this case, http://s3.amazonaws.com. It specifies that the search should focus on Amazon S3 buckets hosted on the Amazon Web Services (AWS) S3 domain.
2. intitle:index.of.bucket: This part of the query focuses on the title of the web pages. It's looking for pages that have the words "index" and "of" in the title and the word "bucket" in the content. This is a common pattern for the default index pages of open S3 buckets, which might expose the contents of the bucket.

#### Using AWS CLI tools find S3 buckets
After creating an AWS account and successfully installation and configuring AWS CLI, AWS CLI commands can be used to interact with S3 Buckets. 
Some of the examples:

**List all Files in an S3 Bucket with AWS CLI** <br>
To list all of the files of an S3 bucket with the AWS CLI, use the s3 ls command, passing in the --recursive parameter.
 ```
    aws s3 ls s3://YOUR_BUCKET --recursive --human-readable --summarize
 ```
The output of the command will show the date the objects were created, their file size, and their path.


The parameters we passed to the s3 ls command are the following:

1. **recursive**: performs the command on all files under the set prefix
2. **human-readable**: displays the file sizes in human-readable format
3. **summarize**: displays the total number of objects and their total size

**List all Files in a Folder of an S3 Bucket**
To list all files, located in a folder of an S3 bucket, use the s3 ls command, passing in the entire path to the folder and setting the --recursive parameter.
 ```
    aws s3 ls s3://YOUR_BUCKET/YOUR_FOLDER/ --recursive --human-readable --summarize
```

The output of the command only will show the files in the /my-folder-1 directory.



**List only the Filenames of an S3 Bucket**
To only list the filenames of an S3 bucket, we have to: 
1. Use the s3api list-objects command.
2. Set the --output parameter to text.
3. Use the --query parameter to filter the output of the command.

 ```
    aws s3api list-objects --bucket YOUR_BUCKET --output text --query "Contents[].{Key: Key}"
```

The output of the command will show all the filenames, or in other words, path names in the S3 bucket.


To list only the filenames in a specific folder, add the --prefix parameter to the command:
 
 ```
    aws s3api list-objects --bucket YOUR_BUCKET --prefix "my-folder/" --output text --query "Contents[].{Key: Key}"
 ```
Output to a file can be redirected to the local file system, using the command: <br>

 ```
    aws s3api list-objects --bucket YOUR_BUCKET --prefix "my-folder-1/" --output text --query "Contents[].{Key: Key}" > file-names.txt
 ```

#### Using CLI tools from GitHub to find S3 buckets
GitHub hosts a range of online tools that aid in finding S3 buckets associated with a website. Some of the tools are Slurp, Bucket_finder, S3Scanner, Cloudlist, Lazy S3, Dumpster Diver, and many more. The main purpose of these tools is to find buckets, scan them, and dump their data. 

#### S3Scanner
S3Scanner uses a list of entries to digest. With this list, it will try to find available S3 buckets. Several formats can be used (bucket name, domain name, full S3 URL, or bucket:region).


**Examples**
1. Scan AWS buckets listed in a file with 8 threads: 
 ```
    $ s3scanner --threads 8 scan --buckets-file ./bucket-names.txt
 ```
2. Scan a bucket in Digital Ocean Spaces: 
 ```
    $ s3scanner --endpoint-url https://sfo2.digitaloceanspaces.com scan --bucket my-bucket
 ```
3. Dump a single AWS bucket: 
 ```
    $ s3scanner dump --bucket my-bucket-to-dump
 ```
4. Scan a single Dreamhost Objects bucket that uses the host address style and an invalid SSL cert: 
 ```
    $ s3scanner --endpoint-url https://objects.dreamhost.com --endpoint-address-style host --insecure scan --bucket my-bucket
```

#### Finding S3 Buckets Using Websites
Several websites offer services to discover open S3 buckets and other cloud storage repositories. One such website is: https://buckets.grayhatwarfare.com/results/colliershouston <br>
By searching for an organization's name, you can filter and browse through the contents of their open S3 buckets.


### Mitigates
#### Limit Public Access: 
- Apply S3 Block Public Access settings to prevent accidental public exposure of data, ensuring that only authorized users have access. 

#### Implement access control:   
- Use bucket policies that define who can access the bucket and what actions they can perform.  
- Implement Least Privilege: Apply strict IAM policies to users, groups, and roles.
- Use Object-Level Access Control: If it is required to manage permissions for each object within a bucket independently use ACLs (Access Control Lists) that are applied at the object level.
- A bucket becomes vulnerable to this type of attack when it is made public, and for this reason, this practice should be avoided.

#### Enable Logging and Monitoring: 
- Enable access logging for S3 buckets and integrate them with AWS CloudTrail. This helps you monitor and detect any unauthorized access attempts or suspicious activities. Specifically, CloudTrail can be used to detect actions for enumerating the contents of S3 bucket, monitoring changes in bucket policies, and tracking user activities.

#### Encrypt Sensitive Data:
- After public buckets are found, the attacker can see the data inside the bucket. Use server-side encryption so Amazon S3 will encrypt objects before saving them and then decrypts the objects when downloading them.


### Data Exfiltration

Data exfiltration is a type of security breach that leads to the unauthorized transfer of sensitive data from the compromised S3 bucket to external endpoints.

After identifying misconfigured S3 buckets often achieved through Bucket Enumeration, an attacker can find and exploit vulnerabilities in the S3 bucket by analyzing the security measures applied to the bucket. If the attacker gains unauthorized access to the bucket, he can use data exfiltration methods to transfer sensitive data.

**Types of data exfiltration attacks and how do they happen**
After attackers successfully target misconfigured S3 Buckets, data exfiltration takes place.
Some of the ways are described in the following.

#### Misconfigured ACL
If the bucket has misconfigured ACL(Access Control Lists) permissions, you can use this command to download data from an S3 bucket to your local system. 
 ```
    aws s3 sync s3://<bucket>/<path> </local/path>
 ```

#### EC2 Metadata IP
AWS provides instance metadata for EC2 instances via a private HTTP interface only accessible to the virtual server itself. While this does not have any significance from an external perspective, it can however be a valuable feature to leverage in SSRF-related attacks. The categories of metadata are exposed to all EC2 instances via the following URL: http://169.254.169.254/latest/meta-data/

#### Leaked Keys
Attackers may stumble on leaked AWS Client ID and Client Secret Keys on Github, and Gitlab. If an attacker gets access to the keys associated with an Amazon Relational Database (RDS) and takes snapshots of these resources, they can deploy a new RDS database based on the snapshot. And when they do that they get to reset the passwords associated with the database. So now they’ve got access to all of your data without actually having to have the passwords required on the RDS instance. It’s the same case with the EBS (Elastic Block Store) snapshot. For example, assuming they’re able to create an SSH key pair in your account, they could launch a new instance from the snapshot and assign their key pair to the instance, giving them full access to the data of the original instance. If they can’t create SSH keys in your account, they might try to mount the snapshot to an existing instance they can already access. 

#### Unsecured EC2 Instances
EC2 instances running data storage services like Elasticsearch and MongoDB, which by default don’t have any credential requirements to interact with the data store also add up to one of the common issues that lead to data exfiltration. If the security groups are not set up properly you can inadvertently expose, for example, the Elasticsearch port (9200) out to the Internet. If that happens, you can bet that somebody is going to find it and dump its entire data set. It’s become so common that adversaries have gone through the trouble of creating ransomware that fully hijacks the data store and encrypts the data within it. To find publicly exposed Elasticsearch databases, an attacker will use the following dork on Shodan; <br>
port:”9200″ elastic

#### Application abuse
A crafty attacker will bang on a web application long enough to find a vulnerability that they can use to exfiltrate data from the system. This technique is very effective because most web applications need access to some degree of sensitive data to be of any use. A good example is the Facebook Data breach where three software flaws in Facebook’s systems allowed hackers to break into user accounts. 

### Mitigates

#### Acces Control
As mentioned in the previous attack, it is essential to pay attention to configurations such as setting up IAM user policies, S3 bucket policies, VPC (Virtual Private Cloud) endpoint policies, and SCPs (AWS Organizations Service Control Policies).  

A majority of modern use cases in Amazon S3 no longer require the use of ACLs, and it is recommended to keep ACLs disabled except in unusual circumstances where it is needed to control access for each object individually.
With ACL disabled, it is recommended to use the policies mentioned above.

#### Keep buckets not publicly accessible

Unless you explicitly require anyone on the internet to be able to read or write to your S3 bucket, make sure that your S3 bucket is not public. Some of the ways to block public access are:
**Use S3 Block Public Access**
This sets up centralized control to limit public access to S3 resources, regardless of how the resources are created.
**Identify policies that allow wildcard identity and wildcard action**
Wildcard Identity (example: "Principal": "*") means that anyone can access resources. Also, Wildcard Action means that the user can perform any action with targeted resources. After identifying, those needs to be avoided by any cost, unless there is specific logic that requires those.
**Implementing ongoing detective controls** 
Consider implementing ongoing detective controls by using the s3-bucket-public-read-prohibited and s3-bucket-public-write-prohibited managed AWS Config Rules.

Also, it is important to use tools, such as AWS Trusted Advisor, to inspect Amazon S3 implementation.

#### Implement least privilege access
It is recommended to grant only permissions that are required to perform a task. Implementing least-privilege access is fundamental in reducing security risk and the impact that could result from errors or malicious intent.
Amazon S3 actions and Permissions Boundaries for IAM Entities, 
Bucket policies and user policies, Access control list (ACL) overview, and Service Control Policies are tools for implementing least privilege access.

#### IAM roles
Its recommended to avoid storing AWS credentials directly in the application or Amazon EC2 instance. These are long-term credentials that are not automatically rotated and could have a significant business impact if they are compromised. 

Instead, use an IAM role to manage temporary credentials for applications or services that need to access Amazon S3.

When you use a role, you don't have to distribute long-term credentials (such as a username and password or access keys) to an Amazon EC2 instance or AWS service, such as AWS Lambda. The role supplies temporary permissions that applications can use when they make calls to other AWS resources.

#### Encrypt Sensitive Data
For protecting data at rest, and reducing the risk of unauthorized access to sensitive data can be used server-side encryption, as mentioned earlier.
**Server-side encryption** with Amazon S3 managed keys (SSE-S3) is the default encryption configuration for every bucket in Amazon S3. To use a different type of encryption, you can either specify the type of server-side encryption to use in your S3 PUT requests, or you can set the default encryption configuration in the destination bucket. Server-side encryption options that Amazon S3 provides are Server-side encryption with AWS Key Management Service (AWS KMS) keys (SSE-KMS), Dual-layer server-side encryption with AWS Key Management Service (AWS KMS) keys (DSSE-KMS), Server-side encryption with customer-provided keys (SSE-C). 
**Client-side encryption** needs a developer to manage the encryption process, the encryption keys, and related tools. manage the encryption process, the encryption keys, and related tools. There are many Amazon S3 client-side encryption options.

####  Encryption of data in transit
HTTPS (TLS) is recommended to use, to help prevent potential attackers' encryption of data in transit. It is recommended to allow only encrypted connections over HTTPS (TLS) by using the was: SecureTransport condition in your Amazon S3 bucket policies.

#### "Write Once Read Many" model
With S3 Object Lock, you can store objects by using a WORM model. S3 Object Lock can help prevent accidental or inappropriate deletion of data.
S3 Object Lock can be used to help protect your AWS CloudTrail logs.

#### Enable Logging and Monitoring
Analyzing CloudTrail logs can be used to identify and respond to data exfiltration attempts by monitoring S3 data events, and analyzing logs for unauthorized object copies.

#### Consider using VPC endpoints for Amazon S3 access
A virtual private cloud (VPC) endpoint for Amazon S3 is a logical entity within a VPC that allows connectivity only to Amazon S3. VPC endpoints provide multiple ways to control access to your S3 bucket and help prevent traffic from traversing the open internet.

## Threat - Taking control over data
Target resource - S3 bucket and its data.
The attacker has the ability to access, manipulate data, and take control of the bucket, compromising the confidentiality, integrity, and availability of the data. 

![image](/documentation/images/T2.png)

## Attacks

### Subdoman takeover - Bucket takeover
Sub domain Takeover attack is when an attacker is able to gain control of a company’s subdomain hosted on a cloud service such as AWS, github etc. because of the DNS entries pointing to that service is not being removed. This allows attacker to set up a phishing page on that sub-domain or serve malicious content.

Subdomain takeover in amazon s3: Each bucket pointing to a specific domain or subdomain. So sometimes, when s3 buckets is no longer in use customer delete them from their account, but forgets to remove the DNS entry pointing to that subdomain it may escalate to a subdomain takeover because amazon allow non existing bucket names to be claimed again on any other account.

Since Amazon S3 buckets’ contents can be retrieved over HTTP, they can be used to store and serve static assets such as images, videos, stylesheets, user upload content, or complete static websites. An S3 bucket is accessed by, for example URL our.company.com.s3-website.ap-south-1.amazonaws.com”. Organizations tend to create custom subdomains like “our.company.com”. Custom subdomains are created by adding DNS CNAME record like the one below:

Type	    Name Content	                                    TTL	
CNAME blog	our.company.com.s3-website-us-east-1.amazonaws.com	3000

Later when this bucket is deleted from AWS S3, we still have the DNS record pointing to the bucket URL: since it wasn’t removed, it now points to a bucket that doesn’t exist anymore.In such a case, pointing the browser to blog.char49.com would return a page like the one below:
![Alt text](/documentation/images/bucketNotFound.png)
What if someone else creates a new bucket with the same name? Then, that person will be in control of what content is served by our subdomain, thus we’re victims of subdomain takeover. 

**Attack scenario**

During enumeration, attacker can find multiple subdomains one of them is ‘our.company.com’. When attacker tries to access this domain using the browser, the URL raises a ‘404 NOT FOUND’, with some additional information like shown in previous image.
Since this error message indicates that there is no S3 bucket. Elliot can reuse/reclaim this bucket with folowing command:
 ```
    aws s3api create-bucket -bucket our.company.com -region eu-west-2 -create-bucket-configuration LocationConstraint=eu-west-2
 ```
 After creation, he applied a policy to the bucket which will allow him to serve static content from this.
 ```
    aws s3api put-bucket-policy — bucket assets.ecorp.net -policy file://malicious_policy.json
 ```

 Now the takeover bucket is up and ready to use, attacker can decide to showcase the harm it can do to the organization. So he uploads a fake login page that resembles Our Organization.
```
    aws s3 sync ./static/ s3://our.company.com
    Note: /static is the local directory that consists of the malicious login page.
    aws s3 website s3://our.company.net/ — index-document index.html — error-document index.html
```
Now when someone acces login page, this webpage is being served from our domain name. Since attacker now controls the S3 bucket he can further perform several malicious attacks such as: Hosting Phishing websites, Hosting Malware, Bypassing CSP policies, Stealing Cookie’s, Man-in-the-browser attacks.


## Mitigates

#### Acces Controll:
- As mentioned in the previous attacks, it is always essential to pay attention to configurations such as setting up IAM user policies and S3 bucket policies, and implement principle of Least-Privilege.

#### DNS records examination:
- It is my recommendation that developers or IT engineers examine their organization’s DNS records every time there is a termination of a S3 bucket. This will ensure there are no DNS/CNAME entries that point to non-existent S3 buckets which could potentially be exploited.

#### Monitor subdomains:
- Regularly monitor subdomains to ensure taht they are pointing to the correct S3 bucket.




## Threat - Data Manipulation/Corruption 
Target resource - S3 bucket and it's data.
Attackers can exploit vulnerabilities to maliciously modify information, compromising the integrity and reliability of the affected data, leading to potential misinformation, unauthorized access, or system malfunctions.

![image](/documentation/images/T4.png)

## Attacks

### S3 Ransomware Attack
Ransomware Attack is when an attacker gains access to a victim’s system and encrypts the sensitive data on it. This is accompanied by a threat to delete or publicly release the data.
The most straightforward way for an attacker to perform ransomware on a bucket is by gaining access to, copying and deleting the information in the bucket -- or otherwise denying access to it to anyone else. Instead of storing the data in its own account, the attacker can encrypt the data locally and store it on the compromised bucket in the victim’s environment.

This attack method has four types of combinations that are interesting to distinguish between: data deletion when versioning is not enabled, data deletion when it is, deleting a KMS(AWS Key Management Service) key used to encrypt the bucket (should the bucket be encrypted with a KMS key) and deleting the information on the bucket using lifecycle rules. Each of those methods requires the ability to access the information in the bucket first what would include performing the following functions:  
• Listing the objects in the buckets with the s3:ListBucket permission granted to a specific identity or, if the bucket is open for use publicly, by its ACL  
• If the bucket is KMS encrypted, decrypting the information on the bucket using kms:Decrypt on the KMS key with which it is encrypted  
• Reading the contents of the objects using s3:GetObject   

#### Data Deletion When Versioning Is Not Enabled  
When the bucket does not have versioning enabled on it, it’s enough to be able to delete an 
object using s3:DeleteObject. Another way is by overwriting it with a different value, possibly ciphertext generated by encrypting the original data locally using s3:PutObject or by the bucket being public for overwriting due to its ACL. 

Command for deleting all data
 ```
     aws s3 rm --recursive s3://your_bucket_name
 ```

For overwriting files attacker can create a blank file and systematically replace every object in the bucket, in effect to make the data unusable, as shown below.
  ```
      # Create an empty file locally
      touch emptyfile.txt

      # Get a list of all objects in the bucket
      aws s3 ls s3://ransom-test-with-versioning --recursive | awk '{print $4}' > objects.txt

      # Read the file line by line
      while IFS= read -r line
      do
        # Copy the empty file to each object in the bucket
        aws s3 cp emptyfile.txt s3://ransom-test-with-versioning/$line
      done < objects.txt

      # Remove the local files
      rm emptyfile.txt objects.txt
 ```

#### Data Deletion When Versioning Is Enabled  
If versioning is enabled, the attacker would have to have access to functions for listing all the 
versions using s3:ListBucketVersions or by means of the bucket being public for listing due to 
its ACL. It would then need to be able to perform s3:DeleteObjectVersion so it can remove all 
previous versions of the object in the bucket in addition to deleting/overwriting the current 
version. 

Command to delete remaining backups
```
    aws s3api list-object-versions \
    --bucket my-bucket \
    --output json | jq -r '.Versions[] | .Key + " " + .VersionId' | while read key versionId
    do
      aws s3api delete-object \
      --bucket my-bucket \
      --key "$key" \
      --version-id "$versionId"
    done
```

#### KMS Key Deletion  
If the bucket is KMS encrypted, there’s another way the attacker can make the objects in the bucket unavailable. If it can successfully delete the KMS key with which the objects were encrypted, there is no way for anyone to decrypt the bucket. To do so, the attacker will need to have permissions to perform kms:ScheduleKeyDeletion on the KMS key in question. 

Command for scheduling key deletion
 ```
    aws kms schedule-key-deletion --key-id <new-key-id>
 ```

#### Managing Lifecycle Configuration  
S3 buckets have a very useful mechanism for managing “Lifecycle Rules” by performing actions, such as transitioning versions of objects between storage classes, automatically expiring current versions of an object and permanently deleting previous versions of a bucket. Combining the ability to expire an object and then have it permanently deleted is potent. A attacker that gains the ability to configure lifecycle 
will be able to configure the bucket to “self destruct” its objects. To be able to manage lifecycle configuration on a bucket, a attacker would need to have permission s3:PutLifecycleConfiguration. 

Code shows manipulation with bucket life-cycle rules by setting them to delete objects automatically after a certain period and by bypassing the need for direct deletion permissions.
```
    aws s3api put-bucket-lifecycle-configuration \
    --bucket my-bucket \
    --lifecycle-configuration '{
      "Rules": [
        {
          "ID": "Delete older versions",
          "Status": "Enabled",
          "Filter": {
            "Prefix": ""
          },
          "NoncurrentVersionExpiration": {
            "NoncurrentDays": 1
          }
        }
      ]
    }'
 ```


#### Encrypt / Re-encrypt objects
Encrypt / Re-encrypt objects with encryption key of attacker. Encryption key can be local or stored in a remote account. In this way, the encryption key is the only way the victim can decrypt the files.
 ```
    aws s3 cp s3://my-bucket/ s3://my-bucket/ --recursive --sse-c AES256 --sse-c-key $encryption_key
 ```
Once a customer key encrypts the object, the victim will receive again the following error when trying to access the encrypted files:
![Alt text](/documentation/images/image.png)
 
#### Attack path for ransomware 
• Attacker creates a KMS key in their own AWS account and provides “the world” access to use that KMS key for encryption. This means that it could be used by any AWS user/role/account to encrypt, but not decrypt objects in S3.
• Attacker identifies a target S3 bucket and gains write-level access to it. 
• Attacker checks the configuration of the bucket to determine if it is able to be targeted by ransomware. This would include checking if S3 Object Versioning is enabled and if multi-factor authentication delete (MFA delete) is enabled. If Object Versioning is enabled, but MFA delete is disabled, the attacker can just disable the Object Versioning. If both Object Versioning and MFA delete are enabled, it would be required to delete remaining backups first.
• Attacker uses the AWS API to replace each object in a bucket with a new copy of itself, but this time, it can be encrypted with the attackers KMS key.
• Attacker schedules the deletion of the KMS key that was used for this attack.
• Attacker uploads a final file such as “ransom-note.txt” without encryption, which instructs the target on how to get their files back.

The following screenshot shows an example of a file that was targeted for a ransomware attack. As you can see, the account ID that owns the KMS key that was used to encrypt the object is different than the account ID of the account that owns the object.
![Alt text](/documentation/images/image-1.png)

The next screenshot shows what happens when the object owner uses a pre-signed URL to try to view the object. Access is denied because even though the object owner has permission to view the object, they don’t have permission to use the KMS key to decrypt the encrypted object.
![Alt text](/documentation/images/image-2.png)


### Mitigates

#### Acces Controll:
- As mentioned in the previous attacks, it is essential to pay attention to configurations such as setting up IAM user policies and S3 bucket policies. Principle of Least-Privilege should be implemented for both.
- Enforce multi-factor authentication (MFA) everywhere possible for everyone (both for the AWS web console and for AWS access keys)

#### Enable Logging and Monitoring:
- Like in previous attacks, analyzing CloudTrail logs it can be used to identify and respond to data tampering attempts by monitoring S3 data events, analyzing logs for unauthorized object copies and changes.

#### Pre-receive hooks:
- Create pre-receive hooks in your Git repositories [git hooks](https://githooks.com/) to monitor for commits that may accidentally contain credentials and deny them before a developer pushes their access keys or credentials.
#### S3 Object Versioning and MFA Delete:
- This is perhaps the most important, but potentially very expensive. S3 Object Versioning allows S3 objects to be “versioned”, which means that if a file is modified, then both copies are kept in the bucket as a sort of “history”. S3 Object Versioning is not enough on its own, because an attacker could just disable the versioning and overwrite/delete any existing versions that are in the bucket without the worry of a new version being created. To combat this, AWS offers the feature of multi-factor authentication delete in S3 buckets. Having MFA delete enabled forces MFA to be used to do either of the following two things:
 - Change the versioning state of the specified S3 bucket (i.e. disable versioning)
 - Permanently delete an object version




## Literature
1. [S3 Bucket Enumeration and Exploitation](https://www.geeksforgeeks.org/s3-bucket-enumeration-and-exploitation/)
2. [Misconfigured AWS S3 Bucket Enumeration](https://medium.com/@narenndhrareddy/misconfigured-aws-s3-bucket-enumeration-7a01d2f8611b)
3. [S3 Bucket Enumeration: Research and Insights](https://medium.com/@aka.0x4C3DD/s3-bucket-enumeration-research-and-insights-674da26c049e)
4. [Hidden Risks of Amazon S3 Misconfigurations](https://blog.qualys.com/vulnerabilities-threat-research/2023/12/18/hidden-risks-of-amazon-s3-misconfigurations)
5. [Exfiltrating S3 Data with Bucket Replication Policies](https://hackingthe.cloud/aws/exploitation/s3-bucket-replication-exfiltration/)
6. [AWS S3 Bucket Takeover Vulnerability: Risks, Consequences, and Detection](https://socradar.io/aws-s3-bucket-takeover-vulnerability-risks-consequences-and-detection/)
7. [Data Exfiltration through S3 Server Access Logs](https://hackingthe.cloud/aws/exploitation/s3_server_access_logs/)
8. [Security best practices for Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)
9. [Data Exfiltration on cloud](https://www.shehackske.com/how-to/data-exfiltration-on-cloud-1606/)
10. [Security best practices for Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)
11. [List all Files in an S3 Bucket with AWS CLI](https://bobbyhadz.com/blog/aws-cli-list-all-files-in-bucket)
12. [S3Scanner](https://pypi.org/project/S3Scanner/)
13. [S3 Ransomware: Attack Vector](https://rhinosecuritylabs.com/aws/s3-ransomware-part-1-attack-vector/)
14. Misconfigurations Leading to AWS S3 Ransomware Exposure: Hard Facts and Mitigation Techniques 
15. [Ransomware in the Cloud: Breaking Down The Attack Vectors](https://www.dig.security/post/understand-ransomware-to-protect-your-data-in-the-cloud)
16. [Subdomain Takeover via Abandoned Amazon S3 Bucket](https://char49.com/articles/subdomain-takeover-via-abandoned-amazon-s3-bucket)
17. [Sub-Domain Take Over — AWS S3 Bucket](https://towardsaws.com/subdomain-takeover-aws-s3-bucket-4699815d1b62)