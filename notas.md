### 💡Laboratory:

**Description of the Scenario:** 

You are a network consultant and have been hired to improve the network architecture of a small company. The company currently has a network that has grown organically over time and is experiencing performance and security issues. Your task is to assess the current situation and propose improvements. You have the following information:

1. It is a LAN network of 10 computers and 1 web server 2.
2. The users state that the network is slow and there is no precise topology established
3. The network devices are obsolete
4. All the computers have access to the Internet and also to the company intranet, the latter through the local network web server.

**Questions and Challenges:**

1. **Assessment of the Current Situation:** 
    - What is the extent of the current network? How many devices and users are connected?
    - What specific performance or security issues has the company experienced?
2. **Network Topology:**
    - What network topology would you use for this company?
    - How should devices and servers be connected?
3. **Network equipment:** 
    - What type of network devices are needed (routers, switches, firewalls, etc.)?
    - What technical specifications must these devices meet?
4. Network Security:
    - What are the security measures required to protect the network?
    - How should security devices, such as firewall, be configured?
5. **Network Management:**
    - How will network devices be managed and monitored?
    - Will a network management system (NMS) or monitoring tools be implemented?
6. **Implementation Plan:** 
    - What is the implementation schedule for the proposed enhancements?
    - How will these changes be communicated to employees?
7. **Ongoing Maintenance:** 
    - What steps will be taken to ensure ongoing network maintenance and upgrades?
    - Will security policies and incident response procedures be established?
8. **Evaluation of Success:** 
    - How will the success of the enhancements be measured? What metrics will be used to evaluate network performance and security after implementation?
    
> ⚠️ **Remember: There are no wrong answers in terms of network topologies and devices, try to make the network as optimal as possible.** 


### 💡Lab: Design a LAN Network

With all the above mentioned download the free software from Cisco called Cisco Packet Tracer and solve the following challenge:

You are a network administrator hired by 4Geeks Academy. On your first day of work, the head of security and communications assigns you to design a LAN network connecting the 8 computers that make up the education department's network and deliver a budget estimate on the total cost of the network installation. To solve this challenge you must:

1. Download Cisco's free software: Cisco Packet Tracer, with this program you will be able to design a LAN network visually.
2. Research the prices and features of the network devices you will need to design your LAN and prepare a quotation.
3. Produce a technical report in which you explain the LAN design 2.

> 💡Hints: Choose the network topology you deem appropriate (There are no wrong answers), remember that it is not necessary to use all the network devices seen during your learning and that sometimes less is more. In your technical report, explain your choices and why this is the most optimal way to create a LAN.


### 💡Lab: Firewall Configuration

In the following lab we are going to learn how to configure a firewall with the help of cisco packet tracer, following these steps:

1. We open Cisco Packet Tracer and create a simulated environment with two computers connected to a Switch, the Switch will be connected to a router and the router to a web server as in the following image:

![Firewall Configuration](https://github.com/4GeeksAcademy/cybersecurity-syllabus/blob/main/assets/confirguracion-firewall.png?raw=true)

2. We configure PC0 and PC0 with static ip, clicking on each one and entering in the Desktop tab:

IP Address 192.168.1.2 / 192.168.1.3

Subnet Mask 255.255.255.0

Default gateway 192.168.1.10

We can ping each ip to verify that the connection between both PCs is established.

3. Configure the server IP:

IP Address 200.200.200.200

Subnet Mask 255.255.255.0

Default gateway 200.200.200.201

4. Configure the router in the FastEthernet0/0 and FastEthernet0/1 options.

The IP address will be the Default Gateway of the devices.

ip address 192.168.1.10 (For FastEthernet0/0) 200.200.200.201 (For FastEthernet0/1)

5. Ping from the client computers to the web server by pinging 200.200.200.200 to confirm that there is a connection between the two devices.

6. Log back in to the router and go to the cli tab where we enter the following commands

![Cli Tab](https://github.com/4GeeksAcademy/cybersecurity-syllabus/blob/main/assets/pestana-cli.png?raw=true)

7. We ping the server again from the client computers, all the packets sent will be lost, since from the router with the previous commands we programmed so that the ICMP protocol will be disabled and only the clients will be allowed to access the web service.

8. Finally from any client computer we will access the web service, entering the web browser option and entering 200.200.200.200 in the search engine. it will show us a page called index.html