
# API ATTACKS

An API attack refers to any hostile or attempted hostile usage of an API (Application Programming Interface).
Attackers exploit vulnerabilities in API endpoints to gain unauthorized access, compromise data, disrupt services, or perform other malicious activities. 

Understanding the different types of API attacks is crucial for implementing effective security measures. Below are some of the most common API attack vectors.

### Injection attacks 
The API injection can be a command injection attack. It means the API will bring a system command to the server. 
The command, when executed, can delete user directories or even the entire site from the server. SQL injections are a common variant of this threat.

### DoS/DDoS (Distributed Denial of Service) Attacks
A denial of service  (DOS) attack  occurs when  an attacker disrupts the services  by intentionally sending a large amount of traffic to overwhelm the system.
This prevents the  system from processing the request of legitimate users and thus denying them from using the service. In the context of cloud computing, 
the DOS attack can be targeted to the applications running on the cloud or it can target the cloud platform infrastructure. 
A distributed denial-of-service (DDoS) attack is a DoS attack that uses multiple computers or machines to flood a targeted resource. 

### Authentication Hijacking
Session hijacking, also known as TCP session hijacking, is a method of taking over a web user session by surreptitiously obtaining the session ID and masquerading as the authorized user. Once the user's session ID has been accessed, the attacker can masquerade as that user and do anything the user is authorized to do on the network.
A byproduct of this type of attack is the ability to gain access to a server without having to authenticate to it. Once the attacker hijacks a session, they no longer have to worry about authenticating to the server as long as the communication session remains active. The attacker enjoys the same server access as the compromised user because the user has already authenticated to the server prior to the attack.

Some of the basic session hijack techniques are:
1. **Predictable Sessions Token ID:** Some websites create session IDs predictably, making them easier to guess. Attackers can analyze patterns in captured IDs to predict valid session IDs, potentially accessing user sessions.
2. **Man-in-the-Browser Attack:** Attackers infect a user's computer with malware. This malware alters transaction details on web pages without the user's knowledge, enabling unauthorized transactions or modifications.
3. **Cross-Site Scripting (XSS):** Cybercriminals exploit vulnerabilities to insert harmful scripts into web pages. If session cookies lack HttpOnly protection, attackers can access session keys, allowing session hijacking.
4. **Session Sidejacking:** Through packet sniffing, attackers intercept session cookies from a user's network traffic. If only the login pages use encryption (TLS) and not the entire session, attackers can impersonate the user within the web application.
5. **Session Fixation Attacks:** These attacks steal a valid, unauthenticated session ID. Attackers trick users into authenticating with this ID, granting access to the victim's session. Variations include hiding session tokens in URLs, form fields, or session cookies.
Each of these threats exploits weaknesses in web applications or user behaviors to gain unauthorized access, manipulate transactions, or impersonate users. Protecting against them involves implementing secure session management practices, using encryption throughout sessions, and preventing script injections or predictable session token generation.
Session hijack attacks are usually waged against busy networks with a high number of active communication sessions. The high network utilization not only provides the attacker with a large number of sessions to exploit, but it can also provide the attacker with a shroud of protection due to a large number of active sessions on the server.

### Parameter Tempering
Parameter tampering is a form of web attack that involves manipulating or interfering with the application business logic that is exchanged between client and server to alter application data, 
such as user credentials, permissions, and price information.

1. **Impact of manipulating URL query strings**
Attackers may tamper with the URL query string to perform malicious actions, such as stealing data. By manipulating query strings, they can access information from a database,
understand the architecture of a web application or even execute commands on the web server.

2. **Impact of manipulating HTTP POST data**
Since query strings are fairly simple, many web applications use the POST method to pass data between pages.
POST data is not displayed by browsers, so it is considered a safe way to retrieve information. However, attackers can still modify the data to gain access to sensitive information.

3. **Impact of manipulating HTTP headers**
Headers are commonly used by HTTP requests and responses to deliver information about the HTTP message.
 A referer header is included in the HTTP request header. It contains the URL of the webpage from which the request originated and enables websites to identify the location of visitors.
This data can be used to optimize caching and for analytics and logging.
Attackers can modify the referer header to make it look like it came from the original site. 
By submitting a malicious string, they can construct arbitrary HTTP responses and launch many kinds of attacks, including cross-user defacement or web and browser cache poisoning. 
They may also hijack pages or initiate cross-site scripting attacks.

5. **Impact of manipulating website cookies**
The web server creates cookies to store user preferences and other data, such as timestamps and session tokens.
An attacker can modify or poison a cookie to bypass authentication to access a user's account and view, manipulate, or exfiltrate sensitive data.


### Man-in-the-middle risks
APIs are subject to increased risk from man-in-the-middle attacks when the transmission is not encrypted
or signed or when there is a problem setting up a secure session. A man-in-the-middle attack in cyber security qualifies as any circumstance where a threat actor places themselves between 
a user and an entity such as a network, website, or application to obtain information. 
Main types of MITM Attacks:
1. IP Spoofing: Manipulating Internet Protocol (IP) addresses to deceive users and gather sensitive data.
2. DNS Spoofing: Forging Domain Name System (DNS) records to redirect users to fake websites for unauthorized data collection.
3. HTTPS Spoofing: Redirection from secure HTTPS to unencrypted HTTP, allowing unauthorized data tracking and theft.
4. Email Hijacking: Unauthorized access to email accounts for monitoring transactions or manipulating users into fraudulent actions.
5. Wi-Fi Eavesdropping: Intercepting data transmitted over deceptive public Wi-Fi networks to extract sensitive information.
6. SSL Hijacking: Intercepting Secure Sockets Layer (SSL) connections to steal encrypted data between users and servers.
7. Session Hijacking: Unauthorized access to browser session data, especially cookies storing sensitive user information.

# MITIGATES

### Clearly define the data type
 Developers must define the specific data types, like string or alphanumeric characters, that the web application accepts.
 ### Control parameter passing
 ### Control parameters with incorrect format
 ### Never store critical data in hidden parameters
 Critical data, such as product prices, order numbers, etc., should never be stored in hidden parameters or cookies since doing this can pose a major security risk and increase the possibility of a parameter tampering attack.


### Use end-to-end encryption
Where possible, instruct employees to turn on encryption for emails and other communication channels. For added security, only use communications software that offers encryption right out of the box. Some applications automatically turn on encryption in the background—such as WhatsApp Messenger, for example. However, if employees wish to verify that their messages are indeed encrypted, they will need to carry out a special process, such as scanning and comparing QR codes available in the WhatsApp application on each person's phone.

### Use a virtual private network (VPN) when connecting to the internet
VPNs encrypt the data traveling between the devices and the VPN server. Encrypted traffic is harder to modify.

### Deploy multi-factor authentication (MFA)
 So you do not rely on passwords alone, organizations should encourage the use of MFA for access to devices and online services. This practice has quickly become organizations' best defense against threats.

### Implement an API Gateway
An API gateway serves as a single entry point for all API traffic, providing a layer of abstraction between your application and the underlying services. This can simplify the management of your API, improve its performance, and enhance its security.

The API gateway can enforce security policies, perform input validation and sanitization, implement rate limiting and throttling, and provide other security features. It can also monitor API traffic, detect unusual patterns, and respond to potential threats.

### API monitoring
Finally, monitoring API usage is necessary for the entire time the API is in production. API analytics can provide extensive insight into the usage, behavior, and security of your APIs. While this is important for managing API performance, monitoring APIs for sudden abnormal spikes in usage or changes in patterns can also help you identify a compromised API or an unauthorized user trying to break into your system. Another aspect of Red Hat 3scale API Management includes comprehensive API analytics to track the usage of your APIs.

## Literature
1. [Parameter Tempering](https://www.techtarget.com/searchsecurity/definition/parameter-tampering)
2. [Protecting your apis against attack and hijack](https://docs.broadcom.com/doc/protecting-your-apis-against-attack-and-hijack)
3. [What is api gateway](https://www.tibco.com/reference-center/what-is-an-api-gateway)
4. [Man in the middle attack](https://www.strongdm.com/blog/man-in-the-middle-attack)
5. [DOS vs DDOS](https://www.fortinet.com/resources/cyberglossary/dos-vs-ddos)
6. [Api injection attacks prevention](https://www.computer.org/publications/tech-news/trends/api-injection-attacks-prevention)