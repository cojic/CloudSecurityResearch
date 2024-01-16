### Abuse of Bucket Permissions
Aabuse of S3 bucket permissions refers to instances where the configuration and permissions of buckets are not properly managed, leading to security vulnerabilities, including unauthorized access, data exposure, and data leakage.

After identifying S3 buckets using Bucket Enumeration, attacker can test permissions they have. 

**READ Permission**
This permission allows reading the contents of the bucket. At the object level, it allows reading the contents as well as metadata of the object. 
Testing this can be done by accessing it via URL http://[name_of_bucket].s3.amazonaws.com. This same thing can be done by using the AWS CLI as well.
 ```
    aws s3 ls s3://[name_of_bucket]  --no-sign-request
 ```
No sign request switch that we used in the above command is used to specify not to use any credential to sign the request. A bucket that allows reading its contents will spit out all the contents once requested by any of the above methods. HTML request will show output on the XML page and the command line will give a list of files.
This image shows resoult of souch commands.
![Alt text](image.png)

**WRITE Permission**
This permission allows to create, overwrite, edit and delete objects in a bucket. This permission can be tested by the AWS CLI, with following command.
 ```
    aws s3 cp localfile s3://[name_of_bucket]/test_file.txt –-no-sign-request
 ```
A bucket that allows unrestricted file upload will show a message that the file has been uploaded. On following image, when command is run for first time, it showed error because s3 bucket blocked file uploads. Later on, permission are modified to allowe file uploads.
![Alt text](image-1.png)

**READ_ACP**
At bucket, level allows to read the bucket’s Access Control List and at the object level allows to read the object’s Access Control List.
 ```
    aws s3api get-bucket-acl --bucket [bucketname] --no-sign
    aws s3api get-object-acl --bucket [bucketname] --key index.html --no-sign-request
 ```
Once we execute both these commands, they will output a JSON describing the ACL policies for the resource being specified.
![Alt text](image-2.png)

**WRITE_ACP**
This policy at the bucket level allows setting access control list for the bucket. At the object level, allows setting access control list for the objects.
 ```
    aws s3api put-bucket-acl --bucket [bucketname] [ACLPERMISSIONS] --no-sign-request
    //To test for a single object, following command
    aws s3api put-object-acl --bucket [bucketname] --key file.txt [ACLPERMISSIONS] --no-sign-request
 ```


## Mitigates

#### Bucket policies:
- Administrators should set each and every permission/Action manually as per requirement and configure the bucket properly such that public access is blocked.
- Example of policy where the main problem is with the Action tag which is set to *. It means that to allow all the actions including reading write upload delete etc.
    ```
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "Statement1",
                "Effect": "Allow",
                "Principal": {
                    "AWS": ""
                },
                "Action": "",
                "Resource": [
                    "arn:aws:s3:::temp4blog",
                    "arn:aws:s3:::temp4blog/*"
                ]
            }
        ]
    }
    ```

#### Acces Controll:
- As mentioned in the previous attacks, it is always essential to pay attention to configurations such as setting up IAM user policies and S3 bucket policies, and implement principle of Least-Privilege.
- Don't allow public access to bucket.



