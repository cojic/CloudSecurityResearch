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
1.	Based on user ID: The API endpoints receive a user ID (from the client’s side) and access the user object based on this ID. For example: /api/trips/get_all_trips_for_user?user_id=777
2.	Based on object ID:	The API endpoint receives an ID of an object  (from the client’s side)  that is not a user object. For example:
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

### Broken Authentication

#### What is it?
Broken Authentication is a security vulnerability that occurs when the authentication of a web application is  flawed or improperly implemented.
When these mechanisms are compromised or misconfigured, attackers can exploit the vulnerabilities to gain unauthorized access to user accounts, impersonate other users, or hijack sessions. This can lead to severe security breaches and expose sensitive user information.

#### How does this happen
Broken authentication is typically caused by poorly implemented authentication and session management functions.

Authentication refers to the process of verifying the identity of users, typically through usernames and passwords, while session management involves maintaining and controlling the user's session after authentication. 
When these mechanisms are compromised or misconfigured, attackers can exploit the vulnerabilities to gain unauthorized access to user accounts, impersonate other users, or hijack sessions. This can lead to severe security breaches and expose sensitive user information

1. Poor credential management
Consumer credentials can be hijacked to gain access to the system. There are various ways that the hacker can steal critical information, such as the following:
•	Weak passwords: The consumer creates a weak password like '12345' or 'pass123'. The hacker can use various password-cracking techniques like rainbow tables and dictionaries to gain access to the system.
•	Weak cryptography: Using weak encryption techniques like base64 and weak hashing algorithms like SHA1 and MD5 make credentials vulnerable. This is why they must be stored using strong hashing algorithms that make password cracking challenging. 
2. Poor session management
Let’s assume you like playing online games. You log in to the application and make several interactions with the network. 

The application issues a session ID whenever you log in and records all your interactions. It is through this ID that the application communicates with you and responds to all your requests. 
The following points list the scenarios that can cause broken authentication.
•	Weak usernames and passwords.
•	Session fixation attacks.
•	URL rewriting.
•	Consumer identity details aren't protected when stored.
•	Consumer identity details are transferred over unencrypted connections.

#### Attack scenarios

#### Broad-based phishing campaigns
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/914a36c9-f2c1-41a3-b9d2-997714d4bee8)
<br> 
A broad-based phishing campaign recognizes that threat agents have to gain access to only a few accounts or one admin account to compromise the organization.
Anatomy of the attack:
1.	The attacker acquires a list of emails or phone numbers and designs a generic call to action that's relevant to that list (such as a fake Google login page).
2.	The phishing message is broadly distributed, and the attacker waits to see which credentials are collected.
3.	The attacker uses stolen credentials to access the data they are after or adopts that identity for a more targeted attack on a high-value employee.
<br>

#### Spear phishing campaigns
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/357613ed-32e2-4b0e-8f62-c119db3d9338)
<br>
Spear phishing is a targeted form of phishing that often involves more research in designing the target list and phishing message. As opposed to broad-based campaigns, spear phishing typically focuses on a small number of employees to evade automated filters. The level of social engineering is also more sophisticated, with messages being more personal and the malicious call-to-action playing on emotions such as curiosity, fear, or rewards. 
Anatomy of the attack:
1.	The attacker picks targets carefully, doing extensive research across available resources such as social media or web presence
2.	The attacker crafts a phishing message designed to appear legitimate, such as pretending to be a colleague and referencing a topical situation, such as a recent company party that the attacker learned of online.
3.	The victim is compelled to enter credentials by appealing to his or her emotions, such as a curiosity to see photos from the party behind a fake login page.
4.	The attacker uses the credentials from the high-value target to access sensitive data or execute the next stage of their attack.<br>

#### Credential stuffing
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/25616f5f-862f-4893-8d3d-dad1ef3a26b4)

<br>
Credential stuffing is a cyberattack method in which attackers use lists of compromised user credentials to breach into a system. The attack uses bots for automation and scale and is based on the assumption that many users reuse usernames and passwords across multiple services. Statistics show that about 0.1% of breached credentials attempted on another service will result in a successful login.

Anatomy of the attack: 
1.	Attacker acquires credentials from a website breach or password dump site.
2.	Automated tools are used to test credentials across a variety of different sites.
3.	When a successful login occurs, the attacker harvests the sensitive data or executes the next stage of their breach.<br>

#### Password spraying 
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/b11d6449-ae65-443f-9bd5-8c518dbc9fb9)

<br>
Password spraying is another form of brute force attack whereby an attacker takes advantage of our tendency to rely on common passwords such as “password1” (which according to Pwned Passwords has appeared in a data breach over 2.3 million times!).
Anatomy of the attack:
1.	The attacker uses a small list of commonly used passwords that match the complexity policy of the domain.
2.	Instead of trying multiple passwords for one user, the attacker uses the same common password across many different accounts which helps avoid detection.
3.	Once the attacker encounters a successful login, the attacker harvests the sensitive data or executes the next stage of their breach.
4.	<br> 

#### Man-in-the-middle (MITM) attacks
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/ebbc38e8-6a40-46e2-a530-a4ea505ad07b)
<br>
A MitM attack on an organization is a highly targeted attack that can result in a full take of credentials and data-in-transit if executed correctly. After intercepting a network connection, an attacker can also take advantage of “session hijacking” which compromises the web session by stealing the session token.
Anatomy of the attack
1.	The attacker intercepts a network connection, often by leveraging tools to mimic a legitimate wifi access point (such as Starbucks Wifi).
2.	If data is encrypted, an attacker may attempt to decrypt data by tricking the user into installing a malicious certificate or other technique.
3.	If the attack is successful before the initial authentication, the credentials may be stolen as the attacker is monitoring all the user inputs.
4.	Alternatively, the attacker steals the session token and can authenticate into the account and execute the next stage of their breach.

#### Mitigates
The following are the ways of preventing broken authentication attacks:
1.	Implement multi-factor authentication (MFA) to verify the consumer's identity. Examples include One-Time Password (OTP) messaged or emailed to the user. This step will prevent brute force attacks, credential stuffing, and stolen credential reuse attacks.
2.	Use weak-password checks by forcing users to include a mix of small letters, capital letters, alphanumeric symbols, and special characters while creating passwords. It would be best to follow NIST 800-63 B's guidelines in section 5.1.1 for memorized secrets.
3.	Place a limit on failed login attempts to 3 or a maximum of 5. Alert the system admin if you detect an attack — brute force, credential stuffing, or any other attack.
4.	Ensure that credential recovery, registration, and API pathways are not vulnerable to account enumeration attacks by using the same message for each outcome. 
5.	Generating new random session IDs with high entropy after login protects against hackers. Remember, those session IDs should not be present in the URL and invalidated after logout.



### Broken Object Property Level Authorization

#### What is it?
Broken Object Property Level Authorization is a significant vulnerability that can lead to unauthorized access, data breaches, and other detrimental impacts.
This new category deals with object properties level authorization, of individual property as opposed to BOLA.

API can enforce sufficient object-level authorization security measures, but this might still not be enough to protect it. More specific authorization that covers the objects and their characteristics is often required.

The Broken Object Property Level Authorization category combines attacks that happen by gaining unauthorized access to sensitive information by way of Excessive Data Exposure (previously listed as number 3 in the 2019 OWASP API Security Top 10) or Mass Assignment. 

#### How does it happen?
Broken Object Property Level Authorization vulnerabilities occur when authorization isn’t performed at a granular enough level. Attackers can take advantage of these vulnerabilities to access or alter properties maliciously. 
APIs often overshare information in their responses, leaving it to the client to filter. This can expose sensitive data to attackers who intercept the traffic, potentially accessing private information like account numbers, emails, and access tokens. Additionally, attackers exploiting this vulnerability might modify object properties, leading to privilege escalation, data tampering, and bypassing security measures.<br>
Therefore, traditional security controls like Web Application Firewalls (WAFs) and API gateways lack contextual understanding of API activity and business logic. They struggle to identify sensitive data transmitted via APIs and fail to assess the risk exposure of the data. While they can employ basic message filtering using regular expressions to detect predefined sensitive data types, they cannot comprehend the API's context and specific business logic flow. 

#### Attack scenario
The example below shows submitting a POST request to an API to retrieve stored information.   <br>
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/8954ebf6-d352-424c-ab83-51d42cbd69fc) <br>

In this case, the API is retrieving stored credit card information, specifically the primary account number (PAN) and card verification value (CVV) code.  this type of data is deemed to be sensitive and must be protected appropriately.
This sensitive data sharing may be intentional as part of the design or necessary for functionality. 

As a result, organizations augment with additional security controls such as stronger authentication or encrypted transport to ensure the data is sufficiently protected. In the example, you can see additional HTTP security headers to help protect the data, such as x-frame-options for mitigating cross-frame scripting attacks and x-xss-protection for mitigating cross-site scripting attacks.  Relying on the client-side code to filter or obscure such sensitive data is typically not appropriate since attackers regularly bypass client-side web applications and mobile application code and call APIs directly. 
<br>
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/642fee48-1fcc-4cd8-b235-0453c1b6e852)
<br>
In the second example above, the attacker has changed the API call to update their account, escalate their role and privileges to an “admin” role, and  bypass single-sign-on (SSO).  If successful, the attacker  can then perform actions within the application as an administrator.

#### Mitigates
To mitigate the risks associated with Broken Object Property Level Authorization, implement the following preventive measures:

•	Validate Access
Ensure that users have appropriate access to object properties exposed through API endpoints. Only expose properties that users should be able to access based on their privileges.<br>
•	Selective Data Return
Cherry-pick specific properties to return instead of exposing all object properties. Avoid using generic methods that may inadvertently expose sensitive data.
<br>
•	Avoid Mass Assignment
Avoid automatically binding client inputs to code variables, internal objects, or object properties. Only allow changes to properties that should be updated by the client, and validate modifications against authorization rules.
<br>
•	Schema-Based Response Validation
Implement a schema-based response validation mechanism to enforce the expected data returned by API methods. Define and enforce data structures to ensure consistency and security.
<br>
•	Minimum Data Exposure
Keep the returned data structures to the minimum required by the business or functional requirements of the endpoint. Avoid exposing unnecessary information that could pose security risks.


## Literature
1. [What is API definition](https://www.altexsoft.com/blog/what-is-api-definition-types-specifications-documentation/) 
2. [OWASP TOP 10 API Security](https://owasp.org/API-Security/editions/2023/en/0x11-t10/)
3. [Insecure direct object reference](https://en.wikipedia.org/wiki/Insecure_direct_object_reference)
4. [Broken object-level authorization - BOLA](https://www.imperva.com/learn/application-security/broken-object-level-authorization-bola/)
5. [A deep dive on the most critical API vulnerability - BOLA](https://www.traceable.ai/blog-post/a-deep-dive-on-the-most-critical-api-vulnerability-bola-broken-object-level-authorization) 
6. [What is IDOR](https://www.varonis.com/blog/what-is-idor-insecure-direct-object-reference)
7. [Application security - BOLA](https://www.imperva.com/learn/application-security/broken-object-level-authorization-bola/) 
8. [OWASP TOP 10 API Security - BOLA](https://owasp.org/API-Security/editions/2023/en/0xa1-broken-object-level-authorization/)
9. [OWASP TOP 10 API Security - Broken Authentication](https://owasp.org/API-Security/editions/2023/en/0xa2-broken-authentication/) 
10. [What is Broken Authentication](https://www.loginradius.com/blog/identity/what-is-broken-authentication/ )
11. [Credential stuffing](https://www.imperva.com/learn/application-security/credential-stuffing/ )
12. [Man in the middle attack](https://www.imperva.com/learn/application-security/man-in-the-middle-attack-mitm/ )
13. [5 Identity Attacks that Exploit Your Broken Authentication](https://www.okta.com/resources/whitepaper/5-identity-attacks-that-exploit-your-broken-authentication/ )
14. [Broken object property level authorization](https://lab.wallarm.com/api32023-broken-object-property-level-authorization/)
15. [OWASP Top 10 API Security: Broken Object Property Level Authorization](https://resilientx.com/blog/owasp-top-10-api-security-broken-object-property-level-authorization/) 
16. [API3:2023 Broken Object Property Level Authorization]( https://salt.security/blog/api3-2023-broken-object-property-level-authorization) 
17. [Excessive Data Exposure](https://owasp.org/API-Security/editions/2019/en/0xa3-excessive-data-exposure/) 
18. [Mass Assigment]( https://owasp.org/API-Security/editions/2019/en/0xa6-mass-assignment/) 

