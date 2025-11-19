Introduction
This project demonstrates how to perform penetration testing on a vulnerable web application — OWASP Juice Shop — using Kali Linux and tools like Burp Suite.
It provides hands-on practice with common web vulnerabilities such as SQL Injection, Cross-Site Scripting (XSS), File Upload Vulnerabilities, and more.

Pre-requisites
Basic understanding of web application concepts (HTTP, HTTPS, web servers)

Familiarity with command-line interface (CLI)

Basic knowledge of HTML, JavaScript, and web development

Installed Kali Linux environment

Lab Setup
Network Diagram
lua

+------------------+       +------------------+
|   Attacker       | <----> |   Vulnerable App  |
| (Kali Linux)     |        | (OWASP Juice Shop)|
| (192.168.1.100)  |        |                  |
+------------------+       +------------------+
Setting Up OWASP Juice Shop
Install Docker:


sudo apt-get update
sudo apt-get install docker.io
sudo systemctl start docker
sudo systemctl enable docker
Pull Juice Shop Docker Image:


sudo docker pull bkimminich/juice-shop
Run Juice Shop Container:



sudo docker run -d -p 3000:3000 bkimminich/juice-shop
Access Juice Shop:

Open your browser and navigate to: http://localhost:3000

Tools Used
Kali Linux — Penetration testing operating system

OWASP Juice Shop — Vulnerable web application

Docker — Application containerization

Burp Suite — Web application security testing platform

Nmap — Network scanning tool

Tasks
Task 1: Identify Open Ports
Steps:

Open a terminal on Kali Linux.

Scan the server using Nmap:


nmap 192.168.1.100
Goal: Discover open ports and services running on the OWASP Juice Shop server.

Task 2: SQL Injection
Steps:

Launch Burp Suite and set your browser's proxy to 127.0.0.1:8080.

Intercept a login request.

Input the following payload:

pgsql

Username: ' OR '1'='1
Password: ' OR '1'='1
Goal: Bypass authentication using SQL Injection.

Task 3: Cross-Site Scripting (XSS)
Steps:

Find a user input field (e.g., search bar).

Insert a basic XSS payload:

html

<script>alert('XSS')</script>
Goal: Trigger an alert box, confirming a reflected XSS vulnerability.

Task 4: File Upload Vulnerability
Steps:

Navigate to a file upload page (e.g., profile picture upload).

Attempt to upload a malicious file (e.g., a PHP reverse shell).

Goal: Verify if file upload controls are bypassable.

Task 5: Directory Traversal
Steps:

Intercept a request with Burp Suite.

Modify parameters to attempt path traversal:

bash

../../../etc/passwd
Goal: Access sensitive files outside the web root directory.

Task 6: Cross-Site Request Forgery (CSRF)
Steps:

Create a malicious HTML form that submits a request on behalf of an authenticated user.

Load the form in the browser while logged into Juice Shop.

Goal: Perform actions without user consent, demonstrating CSRF.

Expected Results
Successfully discover open ports on the target machine.

Bypass login authentication via SQL Injection.

Trigger a pop-up via XSS payload.

Upload and execute or access a malicious file.

Access sensitive server files via directory traversal.

Perform actions without authorization via CSRF attack.

Additional Resources
OWASP Juice Shop Documentation

Burp Suite Documentation

Web Security Academy by PortSwigger

Kali Linux Documentation

License
This project is intended for educational purposes only.
Always perform penetration testing on systems you own or have explicit permission to test.

