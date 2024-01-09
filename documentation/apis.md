## API SECURITY

### API (Application Programming Interface)
APIs are mechanisms that enable two software components to communicate with each other using a set of definitions and protocols. In other words, API allows one software (or software component) to make its data and functionalities available for other programs.
The working principle of an API is commonly expressed through the request-response communication between a client and a server. The client is any front-end application that a user interacts with. The server is in charge of backend logic and database operations. In this scenario, an API works as a middle layer between the client and the server, making sending data requests and responses possible. <br>
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/f7aac767-8cfc-4df1-bf56-87d2cf826595) <br>
With the transition to cloud environments, APIs become more accessible. This transformation brings easier access to users but also increases exposure to threats and risks, requiring a special focus on security and data protection. The following text discusses the 2023 list of OWASP API vulnerabilities 


### BROKEN OBJECT-LEVEL AUTHORIZATION (BOLA)
The OWASP list of top 10 API vulnerabilities identifies Broken Object Level Authorization (BOLA) as the number one vulnerability. Almost every company has APIs that are vulnerable to BOLA and there are currently no direct solutions to mitigate this vulnerability (depending on business logic). 
Insecure Direct Object Reference (IDOR) and BOLA are the same thing. The name was changed from IDOR to BOLA as part of the project.

#### What is it?
Broken object-level authorization is a security vulnerability that occurs when an application or application programming interface (API) provides access to data objects based on the user’s role but fails to verify if the user is authorized to access those specific data objects. This vulnerability allows malicious users to bypass authorization and access sensitive data or execute unauthorized actions, to which they would otherwise not have access. 

There are two main types of BOLA:
1.	Based on user ID
a.	The API endpoints receive a user ID (from the client’s side) and access the user object based on this ID. For example: /api/trips/get_all_trips_for_user?user_id=777
2.	Based on object ID
a.	The API endpoint receives an ID of an object  (from the client’s side)  that is not a user object. For example:
/api/trips/receipts/download_as_pdf?receipt_id=1111. Here arises the main problem - is the user allowed to access the object with this object ID?

#### How does this happen?
BOLA vulnerabilities are often simple to exploit but can be difficult for developers to identify. 
BOLA vulnerabilities are often caused by insecure coding practices, such as failing to properly validate user input or check permissions before granting access to an object. This happens when an API uses overly permissive access controls or when API resources are not properly protected.
This leads to unauthorized information disclosure, modification, or destruction of all data.
Some of the main reasons for BOLA vulnerability:
1.	Insufficient checks during user request validation
2.	Weak or absent access controls based on user roles and permissions
3.	Incorrectly configured permissions for user roles
4.	Lack of context-aware authorization when granting access

#### Attack scenarios
There are four different types of BOLA attacks:
1.	URL tampering
a.	URL tampering is the simplest way to exploit a BOLA vulnerability and often requires little or no technical expertise. In this type of attack, we can simply change the value of a parameter in our web browser’s address bar. 
2.	Body manipulation
a.	Body manipulation is very similar to URL tampering, except that the attacker is modifying one or more values in the body of the document instead of in the URL. This can mean changing the values of radio buttons, checkboxes, or other form elements. It might also be possible to change hidden form values. 
3.	Cookie or JSON ID manipulation
a.	Cookies and JavaScript Object Notation (JSON) are both widely used behind the scenes to store and exchange data between client and server, helping make web pages more dynamic. When we log into a website, for example, the server may store a user or session ID value inside a cookie or JSON object. If the application contains an IDOR vulnerability, an attacker could change these values.   
4.	Path traversal, also called directory traversal, is a unique type of BOLA vulnerability that an attacker leverages to access or manipulate files or folders directly on the server that runs the web application. This is a level deeper than other types of IDOR attacks because it allows direct access to file system resources instead of database records. Path traversal can allow an attacker to access configuration files, discover user credentials, or even obtain a fully functional shell on the target. 

#### Mitigates 
•	Implement a proper authorization mechanism that relies on the user policies and hierarchy. This means ensuring that every request to access a specific object is authorized. A user should only be able to access the objects they have permission to. This could involve implementing access control lists or role-based access control mechanisms, which regulate access based on the user’s role and permissions.<br>
•	Use the authorization mechanism to check if the logged-in user has access to perform the requested action on the record in every function that uses input from the client to access a record in the database.<br>
•	Prefer the use of random and unpredictable values as GUIDs for records' IDs. By making these IDs random or non-guessable, you can add an extra layer of security to your application and make it harder for attackers to exploit BOLA vulnerabilities.<br>
•	Implementing API gateways and rate limiting can also help prevent BOLA attacks. An API gateway can serve as a single entry point for all API requests, providing a layer of security by controlling how requests are handled. One of the security features provided by API gateways is rate limiting. This can prevent attackers from making too many requests in a short period, which is often a sign of a BOLA attack. By limiting the number of requests a user can make, you can slow down an attacker and potentially prevent a data breach. <br>
•	Write tests to evaluate the vulnerability of the authorization mechanism. Do not deploy changes that make the tests fail.

## Literature
1. [What is API definition](https://www.altexsoft.com/blog/what-is-api-definition-types-specifications-documentation/) 
2. [OWASP TOP 10 API Security](https://owasp.org/API-Security/editions/2023/en/0x11-t10/)
3. [Insecure direct object reference](https://en.wikipedia.org/wiki/Insecure_direct_object_reference)
4. [Broken object-level authorization - BOLA](https://www.imperva.com/learn/application-security/broken-object-level-authorization-bola/)
5. [A deep dive on the most critical API vulnerability - BOLA](https://www.traceable.ai/blog-post/a-deep-dive-on-the-most-critical-api-vulnerability-bola-broken-object-level-authorization) 
6. [What is IDOR](https://www.varonis.com/blog/what-is-idor-insecure-direct-object-reference)
7. [Application security - BOLA](https://www.imperva.com/learn/application-security/broken-object-level-authorization-bola/) 
8. [OWASP TOP 10 API Security - BOLA](https://owasp.org/API-Security/editions/2023/en/0xa1-broken-object-level-authorization/) 
