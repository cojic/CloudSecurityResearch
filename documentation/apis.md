## API SECURITY

### API (Application Programming Interface)
APIs are mechanisms that enable two software components to communicate with each other using a set of definitions and protocols. In other words, API allows one software (or software component) to make its data and functionalities available for other programs.
The working principle of an API is commonly expressed through the request-response communication between a client and a server. The client is any front-end application that a user interacts with. The server is in charge of backend logic and database operations. In this scenario, an API works as a middle layer between the client and the server, making sending data requests and responses possible. <br>
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/f7aac767-8cfc-4df1-bf56-87d2cf826595) <br>
With the transition to cloud environments, APIs become more accessible. This transformation brings easier access to users but also increases exposure to threats and risks, requiring a special focus on security and data protection. The following text discusses the 2023 list of OWASP API vulnerabilities 


### API1:2023 BROKEN OBJECT-LEVEL AUTHORIZATION
The OWASP list of top 10 API vulnerabilities identifies Broken Object Level Authorization (BOLA) as the number one vulnerability. Almost every company has APIs that are vulnerable to BOLA and there are currently no direct solutions to mitigate this vulnerability (depending on business logic). 
Insecure Direct Object Reference (IDOR) and BOLA are the same thing. The name was changed from IDOR to BOLA as part of the project.
<br>
<img width="2288" alt="Untitled" src="https://github.com/cojic/CloudSecurityResearch/assets/102799668/536844ef-dfcb-42d0-980b-f84ca653fa72">
<br>

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

#### Attacks
There are four different types of BOLA attacks:
1.	URL tampering
<br> URL tampering is the simplest way to exploit a BOLA vulnerability and often requires little or no technical expertise. In this type of attack, we can simply change the value of a parameter in our web browser’s address bar. 
2.	Body manipulation
<br> Body manipulation is very similar to URL tampering, except that the attacker is modifying one or more values in the body of the document instead of in the URL. This can mean changing the values of radio buttons, checkboxes, or other form elements. It might also be possible to change hidden form values. 
3.	Cookie or JSON ID manipulation
<br> Cookies and JavaScript Object Notation (JSON) are both widely used behind the scenes to store and exchange data between client and server, helping make web pages more dynamic. When we log into a website, for example, the server may store a user or session ID value inside a cookie or JSON object. If the application contains an IDOR vulnerability, an attacker could change these values.   
4.	Path traversal, also called directory traversal, is a unique type of BOLA vulnerability that an attacker leverages to access or manipulate files or folders directly on the server that runs the web application. This is a level deeper than other types of IDOR attacks because it allows direct access to file system resources instead of database records. Path traversal can allow an attacker to access configuration files, discover user credentials, or even obtain a fully functional shell on the target. 

#### Mitigates 
•	Implement a proper authorization mechanism that relies on the user policies and hierarchy. This means ensuring that every request to access a specific object is authorized. Users should only be able to access the objects they are permitted to. This could involve implementing access control lists or role-based access control mechanisms, which regulate access based on the user’s role and permissions.<br>
•	Use the authorization mechanism to check if the logged-in user can perform the requested action on the record in every function that uses input from the client to access a record in the database.<br>
•	Prefer the use of random and unpredictable values as GUIDs for records' IDs. By making these IDs random or non-guessable, you can add an extra layer of security to your application and make it harder for attackers to exploit BOLA vulnerabilities.<br>
•	Implementing API gateways and rate limiting can also help prevent BOLA attacks. An API gateway can serve as a single entry point for all API requests, providing a layer of security by controlling how requests are handled. One of the security features provided by API gateways is rate limiting. This can prevent attackers from making too many requests in a short period, which is often a sign of a BOLA attack. By limiting the number of requests a user can make, you can slow down an attacker and potentially prevent a data breach. <br>
•	Validate user input, control parameters format, and manage parameter passing.
•	Write tests to evaluate the vulnerability of the authorization mechanism. Do not deploy changes that make the tests fail.

### API2: 2023 Broken Authentication
<br>
<img width="1289" alt="Untitled (1)" src="https://github.com/cojic/CloudSecurityResearch/assets/102799668/bb624656-6941-40e2-9220-24dc5d5aecf6">
<br>

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

#### Attacks

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
2.	Use strong passwords and proper credentials management.
3.	Place a limit on failed login attempts to 3 or a maximum of 5. Alert the system admin if you detect an attack — brute force, credential stuffing, or any other attack.
4.	Ensure that credential recovery, registration, and API pathways are not vulnerable to account enumeration attacks by using the same message for each outcome. 
5.	Generating new random session IDs with high entropy after login protects against hackers. Remember, those session IDs should not be present in the URL and invalidated after logout.
6.	Using encryption can help protect the communication between two parties from being intercepted and read by an attacker. This can include using HTTPS for web browsing, VPN for remote connections, and SSL or TLS for email.


### API3: 2023 Broken Object Property Level Authorization

#### What is it?
Broken Object Property Level Authorization is a significant vulnerability that can lead to unauthorized access, data breaches, and other detrimental impacts.
This new category deals with object properties level authorization, of individual property as opposed to BOLA.

API can enforce sufficient object-level authorization security measures, but this might still not be enough to protect it. More specific authorization that covers the objects and their characteristics is often required.

The Broken Object Property Level Authorization category combines attacks that happen by gaining unauthorized access to sensitive information by way of Excessive Data Exposure (previously listed as number 3 in the 2019 OWASP API Security Top 10) or Mass Assignment. 

#### How does it happen?
Broken Object Property Level Authorization vulnerabilities occur when authorization isn’t performed at a granular enough level. Attackers can take advantage of these vulnerabilities to access or alter properties maliciously. 
APIs often overshare information in their responses, leaving it to the client to filter. This can expose sensitive data to attackers who intercept the traffic, potentially accessing private information like account numbers, emails, and access tokens. Additionally, attackers exploiting this vulnerability might modify object properties, leading to privilege escalation, data tampering, and bypassing security measures.<br>
Therefore, traditional security controls like Web Application Firewalls (WAFs) and API gateways lack contextual understanding of API activity and business logic. They struggle to identify sensitive data transmitted via APIs and fail to assess the risk exposure of the data. While they can employ basic message filtering using regular expressions to detect predefined sensitive data types, they cannot comprehend the API's context and specific business logic flow. 

#### Attacks
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


### API4: 2023 Unrestricted resource consumption 

#### What is it?
Unrestricted resource consumption is a frequently overlooked API vulnerability. API requests consume resources such as network, CPU, memory, and storage. When there are no restrictions on the number, content, or type of requests made by users, an attacker can exploit this vulnerability, impacting the APIs' availability and service rate. The following describes some of the techniques attackers can use:
<br> 
• Send a high volume of API requests to overload server resources. <br>
• Send specially crafted requests with large payloads or large file uploads or downloads that can excessively consume server resources.<br>
• Make targeted requests that lead to increases in operational costs. <br>

#### How does it happen?
Unrestricted resource consumption is rooted in security weaknesses that exist in APIs. These weaknesses include:

• Lack of resource limits: Many APIs fail to implement appropriate limits on client interactions or resource consumption. This allows attackers to exploit the API by overwhelming it with excessive requests or consuming excessive resources.<br>
• Insufficient input validation: APIs may lack proper validation mechanisms for incoming parameters and payloads. Without proper validation, attackers can manipulate input data to force resource consumption beyond acceptable limits. <br>
• Inadequate rate limiting: APIs often lack effective rate-limiting mechanisms to control the frequency of client interactions. Without rate limits, attackers can bombard the API with a high volume of requests, leading to resource exhaustion. <br>
• Poor query string and request body validation: APIs may not implement thorough validation for query string and request body parameters. Attackers can manipulate these parameters to control the number of records returned in the API response, leading to excessive resource consumption. <br> 

#### Attacks

#### Denial-of-Service Attack
A very popular example of an attack that exploits this vulnerability is distributed denial-of-service (DDoS) attacks targeting APIs. 
DDoS, or distributed denial of service, is a type of cyberattack that tries to make a website or network resource unavailable by flooding it with malicious traffic so that it is unable to operate.

In a distributed denial-of-service (DDoS) attack, an attacker overwhelms its target with unwanted internet traffic so that normal traffic can’t reach its intended destination.

During a DDoS attack, attackers use large numbers of exploited machines and connected devices across the Internet — including Internet of Things (IoT) devices, smartphones, personal computers, and network servers — to send a flood of traffic to targets.

Anatomy of the attack:
1. Infection and Botnet Formation:
Attackers use malware or exploit security vulnerabilities to infect devices.
Infected devices, known as bots or zombies, spread malware and join a botnet.
Botnets are formed, amplifying attack strength using numerous compromised devices.

3. Execution of Attack:
Attackers remotely instruct bots in the botnet to initiate a DDoS attack.
Bots flood the victim's IP address with requests, overwhelming the system.
Excessive traffic leads to a denial of service, disrupting normal access.

3. Consequences and Further Misuse:
Legitimate device owners become secondary victims or unknowing participants.
Attackers, often hard to identify, exploit the infected botnets for various attacks.
"Attack-for-hire" services enable inexperienced individuals to launch DDoS attacks using rented botnets.

#### Mitigates
• Use a solution that makes it easy to limit memory, CPU, number of restarts, file descriptors, and processes such as Containers / Serverless code (e.g. Lambdas). <br>
• Define and enforce a maximum size of data on all incoming parameters and payloads, such as maximum length for strings, maximum number of elements in arrays, and maximum upload file size (regardless of whether it is stored locally or in cloud storage). <br>
• Implement a limit on how often a client can interact with the API within a defined timeframe (rate limiting). <br>
• Rate limiting should be fine-tuned based on the business needs. Some API Endpoints might require stricter policies. <br>
• Limit/throttle how many times or how often a single API client/user can execute a single operation (e.g. validate an OTP, or request password recovery without visiting the one-time URL). <br>
• Add proper server-side validation for query string and request body parameters, specifically, the one that controls the number of records to be returned in the response. <br>
• Configure spending limits for all service providers/API integrations. When setting spending limits is not possible, billing alerts should be configured instead. <br>

### API5: 2023 Broken Function Level Authorization

#### What is it?
Function level authorization is a security mechanism used in software applications and APIs to control access to specific functions or actions based on the user’s level of privilege or authorization. 

Broken function level authorization refers to an application programming interface (API) vulnerability that allows unauthorized access to certain functions or features that should be restricted based on the user’s role or permissions. In other words, it is when hierarchical permission systems in APIs are broken or missing.

When the function level authorization API is broken, attackers can bypass the security controls and access restricted functions or actions they cannot perform. This can lead to various security risks, such as unauthorized data access, modification, deletion, and privilege escalation attacks.

#### How does it happen?
Attackers can discover these flaws in APIs because API calls are structured and predictable, even in REST designs. This can be done in the absence of API documentation or schema definitions by reverse engineering client-side code and intercepting application traffic. Some API endpoints might also be exposed to regular, non-privileged users making them easier for attackers to discover.

Some of the main reasons that cause this vulnerability are: Proper, role-based access controls restrict access to specific functions or operations based on user roles and permissions. When these policies are improperly designed or implemented, unauthorized users can perform actions they should not have access to. <br>
1. Insufficient or weak access controls: 
2. The inadequate separation between admin and general functions: This could happen if the user functions are too complex and the developer is unable to create enough separation. <br>
3. Poor design or implementation of authorization mechanisms: APIs may have flaws in their authorization mechanisms, such as missing or insufficient checks for user roles or permissions or using predictable or easily guessable tokens or session IDs. <br>
4. Lack of proper input validation: APIs may not properly validate user input or parameters, which can lead to attackers manipulating authorization tokens or session IDs.<br>
5. Flaws in session management: APIs may have vulnerabilities in their session management mechanisms, such as weak session IDs or session fixation attacks, enabling attackers to hijack sessions and bypass authorization checks. <br>
6. Inadequate security testing: APIs may not undergo regular security testing to identify and address vulnerabilities, including BFLA flaws. <br>
   

#### Attack scenario
In the following attack scenario, the attacker manipulates the directory in the URI path and HTTP method to perform administrative functions.

The attacker uses a legitimate account and sends the following API request to retrieve the user information:<br>
GET https://api.example.com/v2/userid-1a-1234/userinfo<br>

The attacker uses a script or tool to manipulate the request, enumerating a range of URLs, and receives a valid response for the URL /all_userinfo. This is an unprotected administrative function that returns information for all users:<br>
GET https://api.example.com/v2/userid-1a-1234/all_userinfo<br>

The attacker expands the scope of his attack by manipulating the HTTP method of the API request to delete users, as follows:<br>
DELETE https://api.example.com/v2/userid-1a-2222
<br>
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/17c99b33-e60f-4bc2-8040-6785c02b1e69)
<br>


#### Mitigates
Your application should have a consistent and easy-to-analyze authorization module that is invoked from all your business functions. Frequently, such protection is provided by one or more components external to the application code.
<br>
• The enforcement mechanism(s) should deny all access by default, requiring explicit grants to specific roles for access to every function.<br>
• Review your API endpoints against function-level authorization flaws, while keeping in mind the business logic of the application and group hierarchy. <br>
• Make sure that all of your administrative controllers inherit from an administrative abstract controller that implements authorization checks based on the user's group/role. <br>
• Make sure that administrative functions inside a regular controller implement authorization checks based on the user's group and role. <br>
• Implement zero trust policies. 

### API6: 2023 Unrestricted Access to Sensitive Business Flows

#### What is it?
Unrestricted Access to Sensitive Business Flows involves exploitation of the business model behind the application. In these vulnerabilities, the API facilitates an unexpected and unwanted business flow. Most commonly, exploitation of this class of vulnerabilities might be called API Abuse or be associated with malicious bot traffic. 
 It allows attackers to potentially manipulate, exploit, or automate actions that can have a devastating impact on an organization. 

#### How does it happen?
Some of the main reasons this vulnerability occurs:<br>
• Insufficient Restrictions: APIs should enforce limitations on the actions users can perform, but in this case, they fail to do so.<br>
• Excessive Functionality: The API doesn't properly restrict or control certain functionalities, allowing them to be used in unintended or excessive ways.<br>
• Exploiting Gaps in Business Logic: Attackers exploit these gaps by repeatedly using specific API endpoints or methods in ways that the system doesn't expect or intend.<br>

#### Attacks

Each type of the following attacks targets weaknesses within the API's design, implementation, or usage.

#### API Abuse
Attackers exploit the API endpoints by using them in unintended ways. This might involve excessive use of certain functions or bypassing restrictions to gain unauthorized access or manipulate data. Some of the "use cases" attackers use are: <br>
• Fake Accounts: Attackers might use an unrestricted account creation API to generate hundreds or thousands of fake accounts, allowing them to overwhelm an application or engage in programmatic exploitation of their status as ‘authorized’ users. <br>
• Spamming: An API to add user-generated content, such as comments or reviews can allow an attacker to add malicious links or even simply advertisements into an application at a massive scale.  <br>
• Scalping: An API that allows direct purchasing without browsing through a web interface can allow an attacker to jump ahead of desired customers and purchase an inventory of items to resell at a higher price. <br>
• Content Scraping: Of course, APIs that provide data, whether about products, prices, or users, can be used to collect that data in bulk for malicious purposes. <br>

#### Rate Limiting Bypass
Attackers attempt to bypass rate-limiting mechanisms put in place to control the number of API requests a user or entity can make within a specified timeframe. By doing so, they can overwhelm the system or perform actions beyond allowed limits.

#### Business Logic Abuse
Exploiting flaws in the logic of the application's business processes accessed via the API. Attackers manipulate the sequence of actions or parameters to achieve results not intended by the system, such as accessing restricted data or performing unauthorized transactions.

#### Parameter Tampering
Modifying parameters within API requests to manipulate the system's behavior. Attackers might alter inputs (such as changing values in URLs, headers, or request bodies) to bypass security controls, access unauthorized resources, or execute unintended operations.

#### Automated Attacks (Bot Traffic)
Malicious bots can be used to automate attacks on APIs. These bots can flood the system with a high volume of requests, attempting to overload it, steal sensitive data, or cause disruption. Automated attacks can cause major consequences.

#### API Injection
Similar to traditional code injection attacks, where attackers inject malicious code or unexpected inputs into API requests to compromise the system's security, gain unauthorized access, or manipulate functionalities.

#### Mitigates
Detecting unrestricted access to sensitive business flow vulnerabilities is a challenge on its own. <br>
The mitigation planning should be done in two layers: <br>
• Business - identify the business flows that might harm the business if they are excessively used.<br>
• Engineering - choose the right protection mechanisms to mitigate the business risk. <br>

Constant monitoring of API access with flags for suspicious use can help detect excessive API calls. For example, flagging non-human patterns, such as repeat purchases, actions within seconds, or consumption of a large number of resources within a short period. <br>

Prevention requires regular code reviews focusing on API access controls and limits for excessive use. Developers need to think like an attacker and the ways they might exploit systems by creating too many resources within a particular period. <br>
Some of the protection mechanisms are more simple while others are more difficult to implement. One of the main ideas of protection is to slow down automated threats.
Protecting sensitive business flow means testing across scenarios. <br>
Other strategies include: <br>
• Requiring reauthentication for each API call <br>
• Employing multifactor authentication (MFA), captcha, or biometric identification <br>
• Blocking of IP addresses associated with Tor exit nodes and proxies <br>
• Denying access to unexpected client devices using device fingerprinting <br>
• Limiting or capping repeat activities for sensitive business flows <br>

Secure and limit access to APIs that are consumed directly by machines (such as developer and B2B APIs). They tend to be an easy target for attackers because they often don't implement all the required protection mechanisms

Additionally, some more mitigation techniques are listed below which can be helpful when dealing with API security. <br>
• Authentication and Authorization: Implement robust authentication and authorization mechanisms to ensure that only authorized users or systems can access sensitive business flows.
Role-Based Access Control: Assign roles and permissions to users, allowing them to access only the specific resources and actions necessary for their job functions. <br>
• API Tokens: Use API tokens for authentication and authorization. Tokens can be revoked or rotated to enhance security. <br>
• Rate Limiting: Implement rate limiting to prevent abuse and brute force attacks on APIs. <br>
• Logging and Monitoring: Maintain detailed logs of API access and monitor for any suspicious activity. Anomalies can be detected and addressed promptly. <br>
• Regular Security Testing: Conduct regular security assessments, including penetration testing and code reviews, to identify and fix vulnerabilities. <br>

### API7: 2023 Server Side Request Forgery

#### What is it?
Server-side request forgery (SSRF) is a vulnerability that lets a malicious hacker send a request from the back end of the software to another server or a local service. The server or service that receives that request believes that the request came from the application and is legitimate. <br>

An SSRF attack can force a server to connect to services within the organization that would otherwise be inaccessible to non-company users. Hackers could also force the server to connect to external systems to exfiltrate data such as usernames and passwords. <br>

This data can then be used to further exploit more valuable information, either by inputting it into the system directly or as the basis of an XSS attack against high-value targets within the company. <br>

The SSRF risk can not always be eliminated. While choosing a protection mechanism, it is important to consider the business risks and needs.

#### How does it happen?
SSRF flaws occur when an API is fetching a remote resource without validating the user-supplied URL. It enables an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall or a VPN.

Modern concepts in application development make SSRF more common and more dangerous. <br>

More common - the following concepts encourage developers to access an external resource based on user input: Webhooks, file fetching from URLs, custom SSO, and URL previews. <br>

More dangerous - Modern technologies like cloud providers, Kubernetes, and Docker expose management and control channels over HTTP on predictable, well-known paths. Those channels are an easy target for an SSRF attack.<br>

#### Attacks

In a Server-Side Request Forgery (SSRF) attack, the attacker can abuse functionality on the server to read or update internal resources. The attacker can supply or modify a URL to which the code running on the server will read or submit data, and by carefully selecting the URLs, the attacker may be able to read server configuration such as AWS metadata, connect to internal services like HTTP enabled databases or perform post requests towards internal services which are not intended to be exposed.

#### Types of SSRF Attacks
Server-side request forgery attacks usually exploit the trust between the server or another back-end system and the compromised application, allowing attackers to escalate the attacks to perform malicious actions. Here are some examples: <br>

#### SSRF Targeting the Server
SSRF attacks often target the server, with the attacker inducing the vulnerable application to send HTTP requests to the hosting server. Usually, the attacker provides a URL pointing to a loopback adapter. <br> 

For instance, an eCommerce application might allow users to see if a product is in stock by querying a REST API on the back end. It implements this function by passing a URL to the API via a front-end request—the browser makes an HTTP request to provide the user with the relevant information. <br>

However, attackers can exploit this functionality by modifying requests and specifying a local URL like the admin host, inducing the server to retrieve the admin URL’s contents. Normally, only authorized users can access the admin, but attackers can use this workaround to bypass access controls and obtain full administrative access. It works because the server thinks the request comes from a trusted location.<br>

#### SSRF Targeting the Back End 
Another way that SSRF exploits trust is when an application server can interact with back-end systems that users cannot normally access. These systems typically have a private, non-routable IP address with a weak internal security posture. An unauthorized user can access protected functionality by interacting with a back-end system. <br>

For instance, attackers can exploit administrative interfaces at the back end by submitting a request for the admin URL’s content.

#### Blind SSRF
Blind SSRF attacks occur when the host server does not return visible data to the attackers. They work by focusing on performing malicious actions rather than accessing sensitive data. An attacker may tamper with user permissions or sensitive files on the server. For instance, the attacker might change the URL for the API call to induce the server to retrieve a large file repeatedly. Eventually, the server could crash, causing a denial of service (DoS). <br>

#### Mitigates

#### Input Validation and Sanitization
Implementing strict input validation rules can help prevent an attacker from injecting malicious payloads into requests. Sanitizing user inputs by stripping out any potentially harmful characters or patterns can further reduce the risk of SSRF attacks, as it helps ensure that user-supplied data is processed securely and appropriately. <br>

#### Secure URL Parsers and Access Controls
Implementing a secure URL parser can help prevent an attacker from manipulating URLs to access restricted internal resources. Access controls, on the other hand, ensure that only authorized users and systems can interact with sensitive data and resources. By combining secure URL parsing with robust access controls, you can greatly minimize the potential for SSRF attacks on your web applications.

#### Use allowlists for URLs and IP addresses
Restrict the range of allowed URLs and IP addresses to minimize the attack surface and prevent unauthorized access to internal resources.

#### Monitoring and Logging
By implementing real-time monitoring and logging mechanisms, you can identify unusual patterns or signs of SSRF attacks and respond quickly to mitigate the threat. 

#### Regular security testing
Regular security testing is crucial to identify vulnerabilities in web applications and address them proactively.


### API8: 2023 Security misconfiguration

#### What is it?
Security misconfigurations are the errors and oversights made during an API’s configuration, implementation, or maintenance that can lead to security vulnerabilities. This happens when developers/ IT teams have not followed security best practices in implementing and configuring APIs. <br>
A security misconfiguration is a security vulnerability that arises while configuring an application, website, or server. <br>
It simply means that essential API security settings were implemented incorrectly, or not at all, leaving dangerous gaps and weaknesses in the API. Threat actors can exploit these gaps to orchestrate massive attacks and data breaches. <br>

![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/fd7a8604-71de-4d73-b207-42f792a16b58)
<br>

These misconfigurations may occur at different levels of the API stack, including the API server, API gateway, client application, the infrastructure supporting the API, network level, system level, application level, and so on. Almost no difference exists in how these misconfigurations affect web apps and APIs. <br>

#### How does it happen?
A security misconfiguration occurs when system or application configuration settings are missing or are erroneously implemented, allowing unauthorized access. Common security misconfigurations can occur as a result of leaving default settings unchanged, erroneous configuration changes, or other technical issues. They can occur in applications, cloud infrastructure, networks, and elsewhere. Human mistake accounts for a substantial proportion of security misconfiguration. <br>
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/9a8b6d65-5ff3-4b10-b387-96424f1683a8)
<br>
 Here are eight common issues:
<br>
• Human error
<br>
The most unfortunate part is that the issue occurred due to human error and not a malicious attack. It seems like every few days there is yet another data breach, ransomware threat, or a new security flaw, and companies or organizations must do more to be proactive in how they store sensitive data online.
<br>
• Poor or weak encryption
<br>
The lack of encryption for data at rest and/or data in transit in applications or cloud instances can potentially expose confidential information. For example, an administrator may overlook configuring a cloud provider’s native encryption solution or they may misconfigure key management for data at rest.
<br>
• Excess privilege
<br>
Excess privilege happens if an employee or a contractor is given more administrative rights or access than what is required for their job. For example, someone could be given excessive data access permissions for cloud storage containers. This often happens when an employee has moved roles within the organization, is a new hire but had privileges mirrored from an incorrect account, or has left the organization but didn’t have their access revoked on time.
<br>
• Misconfigured logging
Misconfigured logging happens as a result of logging settings being set incorrectly for an application, system or network. This type of misconfiguration could occur in a cloud network where logging is turned off, when there isn’t enough storage to capture logs, or when logs capture insufficient information. In these situations, the effectiveness of using logs to detect network intrusions could be impacted.
<br>
• Improper versioning
<br>
Misconfigurations due to improper versioning typically happen in storage applications. Versioning is typically used as an extra layer of data protection and/or data retention. For instance, in Amazon S3, versioning is a means of keeping multiple variants of an object in the same bucket. If object versioning is disabled in S3 buckets due to a misconfiguration, you may not be able to preserve and recover overwritten and deleted S3 objects.
<br>
• Insecure services
<br>
Applications, whether they are on-premises or hosted in a cloud, should be configured to have secure authentication and data exchange. An example of an insecure service is when SSL has not been configured appropriately. Another example is when a service has been set to  exchange credentials in plain text form.
<br>
• Misconfigurations related to security tools
<br>
Security tool misconfigurations could occur if a user does not install the latest signature files of an anti-malware tool, a user fails to enable antivirus software, a firewall is accidentally disabled or ports are left open on a firewall.
<br>
• Using out-of-the-box settings
<br>
Out-of-the-box settings are typically configured to provide a good user experience. However, leaving out-of-the-box settings unchanged can also sometimes allow them to be easily exploited. Attackers can take advantage of default passwords, ports that are open by default, or unused user accounts.
<br>

#### Attacks
Security misconfiguration attacks are hackers’ favorites because they can be easily exploited using automated tools. Cloud-native applications are a popular target. <br>

Attackers can abuse your application’s structure and modify software components. This attack type is hard to control if your app is delivered to mobile devices because your business and presentation layers are deployed on a device, not a server. <br>

Some of the attack types are:

#### Brute force attacks
The impact of not implementing a secure password policy is that bad actors will use brute force attacks to gain unauthorized access to your system. They will run a series of standard usernames and passwords until they will successfully authenticate in your application.  

#### Code injection attacks
The impact of bad code and deficient coding practices open the door for code injection attacks. The inadequate coding techniques, such as a lack of precise input and output data validation, will leave your application vulnerable to security misconfiguration attacks. <br>

The impact of your software being out of date or flaws not being fixed will allow hackers to use code injection attacks to inject malicious code. The patch management process is mandatory to avoid any injection techniques and prevent your application from executing any wicked lines of code. <br>

The impact of installing or enabling unused features increases your application security risks of misconfiguration and vulnerabilities. If you do not remove unnecessary features, samples, documentation, and components, you allow attackers to inject malicious code through the code injection technique. 

#### Directory traversal attacks
The impact of lack of security hardening on directory listing will allow attackers to access your directories, files, and commands outside the root directory. These are common issues, especially for web applications built on off-the-shelf frameworks such as WordPress. Cybercriminals can access your app’s source code, app configurations, and system files. They can also modify URLs making your app execute and deliver random files on the server. Devices and apps that have HTTP-based interfaces are a possible target of directory traversal attacks. 

#### Mitigates
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/24aea0d1-56e3-43b6-9a3f-3321599a0b4b)
<br>

#### Adopt Repeatable Hardening Processes
This streamlines the deployment of properly configured web applications and servers. You should also ensure that configurations across environments (development, production, and testing) are in sync but with different authorizations.

#### Automate Repetitive Tasks
An automated process does a better job of repetitive configuration tasks than humans. So, automate as many tasks as you can across development and production to sanitize configuration and verify security settings. Leveraging a solution like Aqua will help automate security tasks at each step.

#### Regularly Update Software
As a best practice, you must regularly update your software, especially when using third-party code. They often contain patches or fixes for any vulnerabilities that were detected recently.

#### Conduct Frequent Audits
Employ periodic inspection to detect and mitigate potential security misconfigurations and appsec risks. Here again, Aqua can give you all the information you need to conduct an audit at any time. Aqua tracks and monitors each step accurately and delivers end-to-end visibility.

#### Build Segmented Architecture
It is crucial to build a robust application architecture that is secure and segmented to create effective separation between components and assets. It is a good strategy to leverage containerization or cloud security groups (ACLs).

#### Avoid Unused Features
As a part of the installation process, you need to remove any unused features, documentation, components, and samples, and make the application a minimal platform.

Other best practices to prevent security misconfiguration attacks are: <br>

• Emphasize the importance of security configurations to your team and the best practices to achieve absolute security <br>
• Eliminate cloud storage permissions and verify predefined privileges in the software <br>
• Avoid enabling directory browsing and turn off non-essential functionalities <br>
• Do not allow debugging tools to access the server or display internal errors publicly <br>
• Ensure that you update all your packages and libraries <br>

### API9: 2023 Improper Inventory Management

#### What is it?
Maintaining a complete, up-to-date API inventory with accurate documentation is critical to understanding potential exposure and risk. An outdated or incomplete inventory results in unknown gaps in the API attack surface and makes it difficult to identify older versions of APIs that should be decommissioned. Similarly, inaccurate documentation results in risks such as unknown exposure of sensitive data and makes it difficult to identify vulnerabilities that need to be remediated.
<br>
Unknown APIs, referred to as shadow APIs, and forgotten APIs, referred to as zombie APIs, are typically not monitored or protected by security tools. Even known API endpoints may have unknown or undocumented functionality, referred to as shadow parameters. As a result, these APIs and the infrastructure that serves them are often unpatched and vulnerable to attacks.

#### How does it happen?
Running multiple versions of an API requires additional management resources from the API provider and expands the attack surface.
An API has a "documentation blindspot" if: <br>
• The purpose of an API host is unclear, and there are no explicit answers to the following questions. <br>
• It depends on which environment is the API running in (e.g. production, staging, test, development). <br>
• It is not clear who should have network access to the API (e.g. public, internal, partners), <br>
• There is no clear knowledge of which API version is running <br>
• There is no documentation or the existing documentation is not updated. <br>
• There is no retirement plan for each API version. <br>
• The host's inventory is missing or outdated. <br>

The visibility and inventory of sensitive data flows play an important role as part of an incident response plan, in case a breach happens on the third-party side.
An API has a "data flow blindspot" if: <br>
• There is a "sensitive data flow" where the API shares sensitive data with a third party. <br>
• There is no business justification or approval of the flow. <br>
• There is no inventory or visibility of the flow. <br>
• There is no deep visibility of which type of sensitive data is shared. <br>

 Also, there is research conducted between manually created API documentation (or schema definitions) in the form of Open API Specification (OAS) vs. what is deployed in production APIs. 
 <br> These gaps fall into the following three categories: Shadow API Endpoints, Shadow Parameters, and Parameter Definition Discrepancies.
 
#### Shadow API Endpoints 
API endpoints that are missing from the OAS or have no OAS at all. This sensitive data sharing may be intentional as part of the design or necessary for functionality. As a result, organizations augment with additional security controls such as stronger authentication or encrypted transport to ensure the data is sufficiently protected. In the example, you can see additional HTTP security headers to help protect the data, such as x-frame-options for mitigating cross-frame scripting attacks and x-xss-protection for mitigating cross-site scripting attacks. Some organizations may also mask data being returned to a client to avoid cases where someone intercepts traffic or views data outside of the intended client application. Relying on the client-side code to filter or obscure such sensitive data is typically not appropriate since attackers regularly bypass client-side web application and mobile application codes and call APIs directly.

#### Shadow Parameters
API endpoints are known to exist but API documentation is missing many parameters. As a result, the API documentation does not cover most of the attack surface.

#### Parameter Definition Discrepancies 
In addition to many missing parameters, data types that lack needed details such as “String” instead of “UUID” or “DateTime” will leave APIs vulnerable. Message filters used by traditional security controls will allow any input through the API to be processed by the backend. These controls rely on a positive security approach and explicitly written rules and policies when enforcing requests against API schema definitions.

#### Attacks
Attacks targeting this vulnerability might exploit flaws in inventory tracking, mismanagement of resources, or improper handling of inventory-related data via APIs.

• API Abuse: Attackers exploit APIs to manipulate inventory data, including adding or removing items, altering quantities, or causing inconsistencies in the inventory system.

• Parameter Manipulation: Hackers might attempt to manipulate parameters within API requests to trick the system into displaying incorrect inventory levels or granting unauthorized access to inventory data.

• Injection Attacks: This could involve injecting malicious code or malformed input into API requests to disrupt inventory management systems, potentially causing data corruption or system failure.

• Denial of Service (DoS) Attacks: Floods of requests through APIs can overwhelm the inventory management system, causing it to become unresponsive or crash, disrupting business operations.

• Data Exfiltration: Exploiting vulnerabilities in inventory APIs could allow attackers to steal sensitive inventory data, such as product details, pricing, or customer information.

• Tampering with Inventory Records: Manipulating inventory records through API vulnerabilities can result in incorrect stock levels, leading to financial loss, customer dissatisfaction, or incorrect business decisions.

#### Mitigates
Proper management involves the deletion of unused assets, adherence to OWASP guidelines, a robust upgrade and rollout strategy, and regular security maintenance throughout the API lifecycle.

#### Avoiding Improper Asset Management
• Delete Unused APIs: Remove APIs that aren’t in use to prevent forgotten, unpatched vulnerabilities. <br>
• OWASP Recommendations: Follow OWASP guidelines, including:
  - **Inventory Management:** Maintain a comprehensive list of APIs with version, access, environment, and lifecycle details.
  - **Integrated Services:** Understand data flow, access, sensitivity, and role within the API system.
- **Upgrade Strategy:** Perform risk analysis for newer versions, considering security improvements and backward compatibility.
- **API Rollout Strategy:** Develop a documented strategy covering the entire API lifecycle, including retirement.
- **Regular Security Patches:** Apply updates and security patches consistently to prevent vulnerabilities.
  
### API10: 2023 Unsafe Consumption of APIs

#### What is it?
This vulnerability means an API integrates with third-party APIs and services that can endanger it. For instance, if developers use weaker security standards for third-party APIs, threat actors can get to the target API by compromising those other APIs first. Third-party services may allow them to bypass authentication and manipulate API responses.
<br>
This type of attack has created significant problems for companies. By identifying and compromising other APIs or services that your APIs interact with, attackers may gain access to your systems. These attacks can be somewhat difficult to detect immediately as traffic through the third party may appear to be authorized and authenticated, so even if you have robust security controls and alerts in place, you may not get flagged unless attackers then try to access unauthorized areas.
<br>
![image](https://github.com/cojic/CloudSecurityResearch/assets/102799668/d971d634-466b-4002-a8e1-1bcf08b7677f)

<br>

#### How does it happen?
Developers tend to trust data received from third-party APIs more than user input. This is especially true for APIs offered by well-known companies. Because of that, developers tend to adopt weaker security standards, for instance, regarding input validation and sanitization. <br>

The API might be vulnerable if: <br>

• Interacts with other APIs over an unencrypted channel; <br>
• Does not properly validate and sanitize data gathered from other APIs before processing it or passing it to downstream components; <br>
• Blindly follows redirections; <br>
• Does not limit the number of resources available to process third-party service responses; <br>
• Does not implement timeouts for interactions with third-party services; <br>

#### Attacks
Common examples of API attacks include MITM attacks, where an attacker intercepts and alters the communication between two systems; injection attacks, where malicious data is inserted to exploit a system vulnerability; and DDoS attacks, where an overwhelming amount of traffic is directed toward an API to disrupt service.


#### Mittigates
To mitigate the risks associated with unsafe API consumption, organizations should adopt the following strategies: <br>

• Implement Strong Authentication and Authorization Mechanisms: APIs should enforce secure authentication protocols, such as OAuth or JSON Web Tokens (JWT), and rigorously validate user permissions before granting access to sensitive data or functionality. <br>
• Perform Input Validation and Sanitization: All user-supplied input should be thoroughly validated and sanitized to prevent injection attacks and other malicious input. This includes validating data types, length, format, and encoding. <br>
• Use Secure Communication Protocols: APIs should always employ secure communication channels, such as HTTPS, to encrypt data in transit and protect against eavesdropping and data interception. <br>
• Implement Access Controls and Secure Object References: APIs must enforce proper access controls to ensure clients can only access authorized resources. Additionally, internal object references should be abstracted or obfuscated to prevent direct manipulation by clients. <br>
• Regularly Update and Patch APIs: Keeping APIs up to date with the latest security patches and updates is crucial to address any known vulnerabilities promptly. <br>
• Conduct Security Testing and Code Reviews: Regular security testing, including penetration testing and code reviews, is vital for identifying and addressing any security weaknesses or vulnerabilities in the API implementation. <be>
By following these mitigation strategies, organizations can significantly reduce the risk of unsafe API consumption and enhance the overall security of their systems.


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
19. [OWASP TOP 10 API Security - Unrestricted resource consumption ](https://owasp.org/API-Security/editions/2023/en/0xa4-unrestricted-resource-consumption/)
20. [Unrestricted Resource Consumption](https://resilientx.com/blog/owasp-top-10-api-security-unrestricted-resource-consumption/)
21. [API4:2023 Unrestricted Resource Consumption](https://salt.security/blog/api4-2023-unrestricted-resource-consumption)
22. [API5:2023 Broken Function Level Authorization](https://owasp.org/API-Security/editions/2023/en/0xa5-broken-function-level-authorization/)
23. [Broken Function Level Authorization](https://salt.security/blog/api5-2023-broken-function-level-authorization)
24. [PI5:2019 Broken Function Level Authorization: The What, Impact, Sample Exploit, and Prevention Methods](https://www.indusface.com/blog/broken-function-level-authorization/)
25. [K000135872: Broken function level authorization | APIs and the OWASP Top 10 guide (2023)](https://my.f5.com/s/article/K000135872)
26. [API6:2023 Unrestricted Access to Sensitive Business Flows](https://owasp.org/API-Security/editions/2023/en/0xa6-unrestricted-access-to-sensitive-business-flows/)
27. [OWASP Top 10 API security risks: Unrestricted access to sensitive business flows](https://blog.barracuda.com/2023/07/10/owasp-top-10-api-unrestricted-access-senstive-business-flows)
28. [2023 OWASP Top-10 Series: API6:2023 Unrestricted Access to Sensitive Business Flows](https://lab.wallarm.com/api62023-unrestricted-access-to-sensitive-business-flows/)
29. [API7:2023 Server Side Request Forgery](https://owasp.org/API-Security/editions/2023/en/0xa7-server-side-request-forgery/)
30. [Server Side Request Forgery](https://owasp.org/www-community/attacks/Server_Side_Request_Forgery)
31. [How to Prevent Server-Side Request Forgery](https://www.evolvesecurity.com/blog-posts/how-to-prevent-server-side-request-forgery)
32. [API8:2023 Security Misconfiguration](https://owasp.org/API-Security/editions/2023/en/0xa8-security-misconfiguration/)
33. [Security Misconfiguration: Impact, Examples and Prevention](https://www.balbix.com/insights/security-misconfiguration-impact-examples-and-prevention/)
34. [Security Misconfiguration: Types, Examples & Prevention Tips](https://www.aquasec.com/cloud-native-academy/supply-chain-security/security-misconfigurations/)
35. [The Impact of Security Misconfiguration and How to Avoid It?](https://www.flowmatters.com/blog/the-impact-of-security-misconfiguration-and-how-to-avoid-it/)
36. [API9:2023 Improper Inventory Management](https://owasp.org/API-Security/editions/2023/en/0xa9-improper-inventory-management/)
37. [Improper Inventory Management](https://salt.security/blog/api9-2023-improper-assets-management)
38. [Improper Assets Management](https://www.traceable.ai/owasp-api/improper-assets-management)
39. [OWASP API Top Ten Deep Dive Part 5](https://www.wwt.com/blog/owasp-api-top-ten-deep-dive-part-5)
40. [OWASP Top 10 API Security Risks – 2023](https://equixly.com/blog/2023/11/28/owasp-api-security-top-10/)
41. [OWASP Top 10 API security risks: Unsafe consumption of APIs](https://blog.barracuda.com/2023/08/16/owasp-top-10-api-unsafe-consumption-apis)
42. [OWASP API 10: Unsafe Consumption of APIs](https://aspiainfotech.com/2023/12/01/unsafe-consumption-of-apis-owasp-api/)
43. [Unsafe Consumption of APIs](https://owasp.org/API-Security/editions/2023/en/0xaa-unsafe-consumption-of-apis/)
44. [What Are API Security Risks?](https://www.akamai.com/glossary/what-are-api-security-risks)
