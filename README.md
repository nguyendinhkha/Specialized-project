# Project Objectives
The primary objective of this project is to develop 'A Web-based Deception Strategy Framework Using Reinforcement Learning (RL)'. This defensive framework aims to integrate the adaptive learning capabilities of Reinforcement Learning (RL) with HoneyHTTPD, a customizable web server used to create a deceptive web environment. The goal is to create a system that not only deceives attackers but also learns from their tactics, thereby improving the defensive strategy over time. Honeypots simulate services or systems to deceive attackers, collecting information on the methods and purposes of the attack. This not only helps protect the actual system but also provides valuable data to enhance understanding of cybersecurity threats.

# Overview of HoneyHTTPD
HoneyHTTPD is an HTTP server designed to simulate vulnerable websites and services, acting as a honeypot. It offers high customisability, allowing users to configure fake webpages and record the behaviour of attackers. HoneyHTTPD's strength lies in its ability to mimic real websites, thereby attracting attackers while capturing essential information for analysing and improving security systems.

# Integrating Reinforcement Learning with HoneyHTTPD
The Reinforcement Learning (RL) model is integrated into HoneyHTTPD to enhance its ability to detect and counter threats. The RL model learns from each attack, automatically adjusting its strategy to optimize protection. 
The integration process involves developing and training the RL model, as well as establishing an interface between the model and HoneyHTTPD to ensure continuous and accurate information exchange between the two systems.

# Simulating the DVWA Login Page
HoneyHTTPD is configured to simulate the login page of the Damn Vulnerable Web Application (DVWA), a web application prone to attacks. The goal is to create an attractive and realistic environment to lure attackers. Details on configuring, designing the login page, and how HoneyHTTPD handles incoming requests and its responses.

# System Implementation
System Configuration Setup Steps:

Firstly, we need to edit the config.json file, one of the crucial files when running HoneyHTTPD.

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/6f5b8045-388c-436f-8ccb-48ed362e4814)
Code snippet of the config.json configuration file

-  The config.json file configures HoneyHTTPD to use both HTTP and HTTPS, with an ApacheServer module handler set up for each protocol, corresponding to ports 8000 and 8443. It also specifies loggers, with FileLogger active, and the default domain as localhost.
-  To use HTTPS mode, we need to initialize an SSL certificate, a matter of creating an SSL certificate for the web server, helping encrypt communication between the server and clients. SSL certificates are also known as HTTPS certificates, and they help protect users' privacy and security.

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/a3fe4475-b1c6-4cf2-a412-1b112a899070)
Initializing an SSL certificate.

Then, we run HoneyHTTPD to mimic the login webpage and wait for attackers to attack that fake webpage.

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/825673cc-286e-41ea-b554-fd907c96c528)
Main interface when HoneyHTTPD is running

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/cd72ad9b-9250-4c5a-b415-1a9ab54cdc01)
Mock login page interface of DVWA 

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/dbcc6580-60e2-487c-9e46-ad2e94419629)
![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/b91c4220-a2b2-4c39-b787-e49a979714b6)
Figure 2.2: Code snippet for the mock login page interface of DVWA

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/0f9be807-684a-4e5b-930e-974a7ae8cef1)
The on_GET method in the ApacheServer class serves HTML content when the login page URL is requested. 

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/966b8c92-afe3-4a6b-851d-f99fd1d8e19e)
-  In the on_POST method of the server class handling the login URL, the team will simulate the login authentication process. When the attacker logs in with the correct username and password, HoneyHTTPD will respond with "Login successful" to let the attacker know they have successfully accessed the website.

# Experimentation and Evaluation

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/5a94c823-30e6-4c40-84b2-24e2bac09329)

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/fcf6e2a0-52cb-4a17-96f5-587a1eaf038e)
Figure 3: The curl command is used to request content from the HoneyHTTPD server running on port 8443 with HTTPS security protocol. 

-   The result of the curl command displays an HTML/CSS code snippet, which is the source of the simulated DVWA login page served by HoneyHTTPD.

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/f0593ce9-bdf9-4839-baf4-eb6596874879)
HoneyHTTPD has received a GET HTTP request and responded with 200 OK

-  The attacker proceeds to access the DVWA login page: 
![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/080ccb56-5b95-4838-b109-d92e18ea7118)

-  HoneyHTTPD has noticed a GET HTTP request has been sent and proceeded to respond with the simulated DVWA webpage:
![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/91db28a4-cfe2-47a9-90d5-6d08e4a1637f)

-  When the attacker successfully logs in, HoneyHTTPD will display the text "Login Successful" :
![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/23c6449c-d46f-4a5c-9963-6d2e1c8ee115)

-  However, HoneyHTTPD has logged this access in a log file for the administrator to observe login attempts:
![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/fccf944d-8f6e-4b24-8903-0ea278966824)

-  When the administrator checks the log file to view the access flow to the website:
![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/5dad34bc-c1c4-42b3-8bfa-4f01c7ebdbc5)

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/797edf4f-3988-4ea7-94d7-dce965035c52)

![image](https://github.com/nguyendinhkha/Specialized-project/assets/82517228/1f22e746-29d6-4cd1-91e2-2c2995f5effc)

-  It can be seen that HoneyHTTPD has logged access attempts to the simulated DVWA website in the "server-https-8443.log" file. HoneyHTTPD records these website visits and responds in a pre-configured manner. This makes the attacker believe they have successfully accessed the website without being detected.

-  HoneyHTTPD has successfully simulated a DVWA login webpage and deceived attackers into thinking they have successfully attacked and logged into the official DVWA website. However, HoneyHTTPD still only responds with simple information to illustrate interaction with the attacker, unable to respond with the complete content of the webpage when the attacker successfully logs in.




