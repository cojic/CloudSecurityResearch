# Cloud Security
# MySQL Database
MySQL is an open-source Relational Database Management System (RDBMS) that enables users to store, manage, and retrieve structured data efficiently. MySQL provides the software framework to create, maintain, and interact with databases.

## Threat - Unauthorized access and manipulation of data
Unauthorized access and manipulation of data in MySQL can occur through SQL injection attacks, exploiting vulnerabilities in input handling and potentially compromising the integrity of the database.

![image](/documentation/images/T3.png)

## Attacks
### SQL Injection Attacks
SQL Injection is type of an injection attack that makes it possible to execute malicious SQL statements. Attackers can use SQL Injection vulnerabilities to bypass application security measures. SQL Injection statements can add, modify, and delete records in the database.

To make an SQL Injection attack, an attacker must first find vulnerable user inputs within the web page or web application. The attacker can create input content. Such content is often called a malicious payload and is the key part of the attack. After the attacker sends this content, malicious SQL commands are executed in the database.

### Mitigates
#### Input validation:
- The application code should never use the input directly. Best practis is to sanitize all input forms.

#### Parametrized queries and prepared statements:
- Parametrized queries involve using placeholders to represent data in SQL statements. Beause of that parameter values are treated as data, not executable code.
- Prepared statements involve pre-compiling SQL queries and separating them from specific data, treat client-supplied data as content of a parameter and never as a part of an SQL statement.

### Cross Site Scripting (XSS) 
XSS is a method that exploits website vulnerability by injecting scripts that will run at client’s side.
Attacker can try to trick the database to store this script as string. When there is a read request, this script together with other information is sent to the client browser. If the browser detects JavaScript code within the received data, it may try to execute it.

### Mitigates
#### Data filtering:
- Encoding characters into a format that is safe for rendering in a web browser, thereby prevent the execution of any malicious code.
#### HTTP Response headers:
- Use the Content-Type and X-Content-Type-Options headers can prevent XSS in HTTP responses that aren't intended to contain any HTML or JavaScript.
#### Content Security Policy:
- Use of Content Security Policy (CSP) can be used to reduce the severity of any XSS vulnerabilities that still occur.

## Threat - Loss of data
Loss of data in MySQL can result in overwhelming the server and causing service disruption, or encrypting database files, rendering them inaccessible and posing a threat to data integrity and availability.
[TODO] - Attacks
## Attacks
### DDoS Attacks (Distributed Denial of Service Attacks)
### Ransomware Attack

## Literature
1. https://satoricyber.com/mysql-security/mysql-security-common-threats-and-8-best-practices/
2. https://www.acunetix.com/websitesecurity/sql-injection/
3. https://portswigger.net/web-security/cross-site-scripting
TODO
4. [DATABASE SECURITY ATTACKS](https://d1wqtxts1xzle7.cloudfront.net/64235268/Database_Security_Attacks-libre.pdf?1597998955=&response-content-disposition=inline%3B+filename%3DDATABASE_SECURITY_ATTACKS.pdf&Expires=1703650901&Signature=Jd6scIuXA9j167eyebHwk5XbkGN6Wf9hnurKvmItsIGWpI5BYyKEOKbw11ntGGTb5OuWKtFg1cwqNIR5gQ2KQc2a3ViyunjYCrVY3RU3d7CjKPDqpbm5VkleJPt9V-CbaXEIiRVWUmFcaW5StB4oFwp~D6Jj46TQkEFVrQMUIPXkvb9feGx8XcamCZ2k64lJGYwAeYJyynfBf3vSkC6PSNVjzn1HltydxlYlZw8iG7dnqUTHq2hP1cFlFaEOHQv418YOPddUPnDxXXHLglczx3QSDEPv-FLOZyDmlKsP9W28IUbL8~6eW1uNc5JaSJ3t68pUwwI9xoiy4DjebBgOMA__&Key-Pair-Id=APKAJLOHF5GGSLRBV4ZA)