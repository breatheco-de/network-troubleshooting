 
# Instructions

## 1. Introduction

This time we introduce you to what could be the 4Geeks Academy network at one of our sites. It is a scenario that is commonly seen in many business environments.
We have a router that represents the connection between several networks in the same company. In this case they correspond to 3 different areas, the student campus, the marketing department and the IT department.

As you can see all the networks have class C private addresses that you can see in the notes in their respective colored area.

For this practice we must do the following:

- Configure the DHCP server of each network so that the devices can obtain IP addresses dynamically.
- Configure the links between devices.
- Configure the campus WiFi network
- Configure the Intranet server
- Configure access list to restrict access to the Intranet from campus
Advance to the next page to get started.

## 2. IP Addresses

As you can see in each colored area the IP addresses of the networks are listed, and each one has a `/24` mask that can also be expressed as `255.255.255.0`, which means that for each network you can assign addresses from 1 to 254, for example:

```text
192.168.0.0.0 - Network address
192.168.0.1 - First assignable address
192.168.0.254 - Last assignable address
192.168.0.255 - Broadcast address
```
**Based on this, configure the following:** 

- Assign the first address of the network to the gateway on the router, according to the corresponding interface.
- Configure static ip addresses on the servers, using the annotations on each network.
- All interfaces must be enabled for connectivity.
Remember that in the case of the router you must verify that all the interfaces are turned on, as well as save the configuration in NVRAM so that the changes persist after a reboot.
At the end of this step you should have connectivity between the servers and the router.

## 3. DHCP Servers

Once the connection between the servers and the rest of the network is established, it is time to use them to assign addresses to the other devices.
In each of them you must configure a pool of addresses that will be used to assign them to the devices that connect to the network. The values that make up each pool are as follows:

- **Default Gateway:** Router ip address, i.e. the first address of the network (Example 192.168.0.1).
-  DNS Server:** This is the domain name server, in this case it uses `192.168.2.10` which corresponds to the intranet server that provides this service.
- **Start Ip Address:** Corresponds to the address from which the IP addresses will start to be assigned. In this case it starts from network address 100 (Example: 192.168.2.100).
- **Subnet Mask:** This is the subnet mask which in this case is `255.255.255.0`.
- **Maximum number of users:** The maximum number of users must be `100`.
Once you have set these values, you must press the `Save` button to save the changes to the pool. The rest of the values are left as default.
In the `Settings` option of the `Config` tab you must statically configure the Default gateway and DNS. Remember that the gateway for each network is the first assignable address of the ip address range of your network, while the DNS points to the Intranet server: 192.168.2.10.
Remember to vary the corresponding network addresses for each server. When you have configured them all, it is time to activate the DHCP option on each end device so that they acquire connectivity.

## 4. WiFi network

As part of the campus network we have a wireless access point that must be configured. This device will extend our network via WiFi, incorporating the wireless devices as if they were part of the wired network and securely using a password.

In the wireless port of the `AccessPoint` you must configure the following:

- **SSID:** 4geeks
-  **Authentication:** WPA2-PSK
-  **PSK Pass Phrase:** 4geekswifi
-  **Encryption type:** AES

These are the basic parameters that must be configured to have wireless access. After that you must configure the same parameters in the wireless devices (Laptop and Smartphone) in their respective `Wireless` interfaces for them to connect to the network.

## 5. Intranet Server

This server represents the internal services used in the 4geeks network. In this case it provides DNS and Web services, which are configured in the `Services` tab.
The web server is already loaded with the page to be displayed and you just need to activate it with both HTTP and HTTPS protocols.
The DNS service must be activated and a record will be added to point the `4geeks.com` address to the intranet. You must configure the following:

- **Name:** 4geeks.com
- **Type:** A Record
- **Address:** 192.168.2.10

 
Press the `Add` button to create the record. 
If you followed the notes in step 3 correctly, the Intranet server should have the ip `192.168.2.10` statically configured. Now, if you access the browser from the desktop of any of the PCs on the network, you can see the `4geeks.com` page.

## 6. Access list

So far so good, but we have a security flaw. Our intranet is exposed to people coming to campus and this compromises the integrity of our information. You must prevent access to the intranet from the campus, but without affecting the DNS service that is vital to the normal functioning of the network, nor block access from the other 4geeks departments that need access to the intranet.

This is achieved with an access list, which are rules that the Router will use to determine whether or not to allow the passage of certain information coming through its interfaces.

In this case, 3 rules must be configured for the interface of the campus network:

1. Deny access to packets going to the server using port 80.
2. Deny access to packets going to the server using port 443.
3. Allow all other connections.

Ports 80 and 443 correspond to the HTTP and HTTPS protocols respectively, and are the ones used by browsers to access web pages, and therefore must be blocked. To do this we will go into the command line interface of the router in the `CLI` tab where you must execute the following commands:

1. `enable`.
*Activate the terminal with administrative privileges* 2.
2. `config terminal`
*Enter configuration mode
3. `interface gigabit 0/0` *Enter the gigabit 0/0 configuration.
*Enters the campus network interface configuration* .
4. `ip access-group 100 in` 
*Add the interface into the access list group '100' to filter incoming connections* 
5. `exit` *Exit the interface configuration* 
6. `access-list 100 deny tcp any host 192.168.2.10 eq www` 
*Add a rule to the `access-list 100` to disallow packets to the intranet server using port 80.*
7. `access-list 100 deny tcp any host 192.168.2.10 eq 443` 
*Add a rule to the access list '100' to disallow packets to the intranet server using port 443* 
8. `access-list 100 permit ip any any` 
*Rule to allow all other network traffic. Must be specified last*
9. `do write`
*Saves the configuration in NVRAM.*

You can verify the operation of this access list by trying to access 4geeks.com from a campus PC, which should return a `Requested timeout` error, although a ping test should work correctly.