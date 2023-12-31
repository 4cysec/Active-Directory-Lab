<h1>Active-Directory-Lab</h1>

<h2>Description</h2>
A domain controller server is established with Active-Directory Domain Services(AD DS). Users are added manually and with a powershell script. The domain controller faces the internet while sharing an internal network with a Windows 10 client.  All of this is done within a virtual environment.

<h2>Languages and Utilities Used</h2>

- <b>Windows Command Line</b>
- <b>Powershell</b>
- <b>Active Directory Domain Service</b>


<h2>Environments Used </h2>

- <b>Virtualbox 7.0</b>
- <b>Windows 10 Pro</b>
- <b>Windows Server 2019</b> 


<h2>Project walk-through:</h2>


To view the detailed set up of the VM environment and lab please see Josh Madakor's youtube video <b>How to Setup a Basic Home Lab Running Active Directory (Oracle VirtualBox) | Add Users w/PowerShell</b> at https://www.youtube.com/watch?v=MHsI8hJmggI


Having the DC VM installed, the domain controller VM is configured through the following steps:

Go to settings-->Advanced Tab

Selecting Bidirectional for Shared Clipboard and Drag 'n' Drop allows for copying and pasting and 
dragging and dropping of files between the host and virtual machines.

![Screenshot 2023-12-22 194535](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/99ed1965-aee3-47a2-ae19-db3182551cc5)


![Screenshot 2023-12-22 195730](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/e09cd02d-f9ff-45f8-93dc-dc8569e5de8b)

Navigate to the Network configuration in the left pane--->Network

Set Adapter 1 to Attached to: NAT for the DC connection to the Internet


![Screenshot 2023-12-22 201501](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/596577bd-7d05-4f68-9d5a-43fe385ebe21)


Set Adapter 2 to Attached to: Internal for the DC connection to the internal network

![Screenshot 2023-12-22 201525](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/fd5e6729-5dcb-473b-9449-c7710eb97626)

Once the Server 2019 ISO is installed on the VM. The Domain Controller is configured below.

<p align="center"><b>Setup IP Addresses</b><br/>

To set up IP addressing to our NICs for External and Internal network click internet
icon bottom right corner of display. 

![Screenshot 2023-12-22 214111](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/e0ef3084-2058-4446-8e08-80027034d4bb)


![Screenshot 2023-12-22 214344](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/78353ba8-4621-4edd-b23e-64ab1cce3d36)


![Screenshot 2023-12-22 215737](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/bf14e3bc-5b96-43c1-8515-f566bfcb86f5)




-->Network Connections
  -->Change Adapter Settings
   -->Adapter1(Ethernet)
      -->details

![Screenshot 2023-12-22 215830](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/73b08200-83db-48ee-9e86-94f50b28294d)


      
-->Adapter2(Ethernet2)
      -->details

![Screenshot 2023-12-22 215912](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/d7c8f2ae-113d-46fa-9e44-8e09c062a3f4)

The Domain Controller will connect to the internet(external) through the home router
thus the first ethernet IP can be considered the external IP.

-->Right Click and rename the first adapter "Internet"

The second adapter has an auto configured IP address. 

The second adapter will face the internal network.

-->Rename adapter2 "Internal Net"

-->Go to properties within "Internal Net" adapter

-->Click Internet Protocol Version 4 

 ![Screenshot 2023-12-22 225407](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/f26a790f-e3b1-464a-8260-4e16ddb8803e)

Using Josh Madakor's Tutorial network information, the following is entered:
IP:  172.16.0.1
Mask: 255.255.255.0
DNS: 127.0.0.1

The Domain Controller will act as a Gateway so no entry.

Using default "self pinging" address for DNS. As DC will serve as the DNS.


![Screenshot 2023-12-22 234137](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/b03f78bd-8138-460b-ab7f-0cdfece1d69a)



<p align="left"><b>Install and Configure Active Directory Domain Services</b><br/>

From the Server Manager Dashboard

-->Go to Add roles and features

![Screenshot 2023-12-23 232709](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/4a528cbc-fccc-40a8-8ef8-5e0a446bf9b5)

[Before You Begin] --> Click Next

[Installation Type] --> Select Role-based or feature based installation
                    -->Click Next

 [Server Selection] --> With Domain Controller and External IP selected Click Next                  
                   
                   
![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/adc05821-d203-4845-b64f-b3428e4222d2)

[Server Roles] --> Select Active Directory Domain Services
               --> Click Add Features
               --> Click Next

 ![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/7b68a97d-3f29-4ae8-a1d9-113b003544f7)

 [Features] --> Click Next(with pre selected boxes)

 [AD DS] --> Click Next

[Confirmation] -->Click Install

After Installation of AD DS

Click on alert notification and link "Promote this server to domain controller"

![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/c9023405-2e0b-44bd-ada3-367a8c8fe6db)

[Deployment Configuration]--> Select add a new forest
    Provide a domain name. (Mydomainlab.com) used in this example.

![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/712a6c34-ce24-4699-8bdb-caf9978554ee)

[Domain Controller Options] --> Enter chosen password

[DNS Options]--> Click Next(no selection)

[Additional Options] --> Next

[Paths] --> Next

[Review Options] --> Next

[Prerequisites Check]--> Install


<p align="left"><b>Creating Domain, Organizational Unit & New User</b><br/>

After installation and reboot
--> Click Start Icon
   --> Windows Administrative Tools Folder
     --> Click Active Directory Users and Computers
The created domain can be seen in the left pane: mydomainlab.com

![Screenshot 2023-12-24 221835](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/c05ec5fa-c31c-4f5c-992a-b71b2735fe71)


--> Right Click domain(in this case mydomainlab.com)
   -->New
     --> Organizational Unit
       -->Name the organizational unit(named _ADMINS in this lab)
       

![Screenshot 2023-12-24 222030](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/8a7735ae-166e-44f4-b031-e11298aa6b54)



This creates a folder _ADMINS
--> Right click _Admins
  -->New
    --> User
 Fill user name, logon name and password(Jon Doe, a-jdoe for this lab)
 For the purpose of the lab, "password never expires" was checked.

 ![Screenshot 2023-12-24 230052](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/de956ef6-a055-4e67-821c-fec9d3635a44)

To make the new user an admin
-->Right click on the user
  -->Properties
    -->Member Of tab
      -->Click Add
         -->Name assigned user group(Domain Admins)
           --> Apply
             -->OK

![Screenshot 2023-12-24 231838](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/2c849e27-a8a2-4f1b-8049-b7e369153915)

The new admin user jdoe was created and can now log into the domain as Jon Doe.

![Screenshot 2023-12-25 001820](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/a403c71a-992f-444c-a612-77d8ea003651) 

___________________________________________________________________________________________________________________________________________________________________________

<p align="left"><b>Internal Network Set Up</b><br/>

Install Routing and Remote Access/Network Address Translation(NAT)

Will allow the client on the internal network to gain access to the external internet.

On Server Manager Dashboard -->Add roles and features
[Before You Begin] --> Next
[Installation Type] with Role-based or featured-based installation selected --> Next
[Server Selection] with server selected --> Next
[Server Roles] select Remote Access --> Next
[Features] --> Next
[Remote Access] --> Next
[Role Services] Select Routing -->Add Features
DirectAccess and VPN(RAS) and Routing Selected --> Next
[WebServer ROle (IIS)] --> Next
[Role Services] --> Next
[Confirmation] --> Install
Close box after install

![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/d3ea9f11-ace4-4aed-ac0b-1408c320dc85)

In Server Manager Dashboard --> Tools (top right)

![Screenshot 2023-12-30 021444](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/f7e6290f-01af-4c7a-9fb0-987d2b5bf511)

Select domain controller name local(DomConlocal)
-->Right Click on selection above
  -->Configure and Enable Routing and Remote Access

![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/5ace9e2f-aa39-4fdd-a825-d31480783e32)

   --> Next

Select Network address translation --> Next

Select the Internet set up in previous steps as public interface --> Next

![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/8f5d473b-c089-4fcc-ad3a-555fe761fada)

--> Finish 

Setting up DHCP

DHCP will assign IP address to the Windows clients within the internal network

In Server Manager Dashboard --> Add roles and features
[Before You Begin] --> Next
[Installation Type] with Role-based or featured-based installation selected --> Next
[Server Selection] with server selected --> Next
[Server Roles] select DHCP server --> Add Features --> Next
[Features] --> Next
[DHCP Server] --> Next
[Confirmation] --> Install
Close box after install

In Server Manager Dashboard --> Tools(top right menu)
                            --> DHCP
Select Domain(Expands Directory)-->Right click IPv4
                                --> New Scope --> Next
Provide name. In this case the IP Address range from Josh Madakor's example
 -->172.16.01.100-200 --> Next
 Start IP: 172.16.01.100
 End IP:  172.16.01.200
 Length:  24
 Subnet Mask: 255.255.255.0

![Screenshot 2023-12-30 180751](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/6478eda9-50af-4de4-bd19-93d0b9a34362)

![Screenshot 2023-12-30 181029](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/d864b0d7-42dc-4086-832c-2ff3e7fb0f86)

--> Next
[Add Exclusions and Delay] --> Next

[Lease Duration] 8 days pre selected as duration of time assigned IP addressing is valid for clients
               --> Next
[Configure DHCP Options] Yes...selected --> Next

[Router (Default Gateway)] The domain controller will act as the router of network traffic from 
the internal network to the Internet. Thus, the IP address of the DC Server is used.
-->172.16.0.1 -->Add--> Next

![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/c49d8d59-ab1f-4a50-a463-c52fc6e35359)

[Domain Name and DNS Servers] The DC Server with Active Directory Domain Services acts as the DNS
                              --> Next
[WINS Servers] --> Next

[Activate Scope] Yes...selected --> Next --> Finish

In DHCP Box --> Right Click DC directory-->Click Authorize
           
![Screenshot 2023-12-30 185140](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/30898304-d725-44c3-b65f-f7b2d9413671)

            
--> Right Click DC directory--> Refresh


Green check marks on IPv4/IPv6 icons indicate successful configuration.


_____________________________________________________________________________________________________________________________________________________________________

<p align="center"><b>User Additions Using Powershell Script</b><br/>

Using Josh Madakor's powershell script and a notepad file with generated user names(seen below),
new users will be added to the directory in an automated fashion. This greatly shortens 
time in comparison to adding users manually.

![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/3a0d1475-bf56-40f9-81b8-38ac47a4186a)

  In Windows
  --> Start 
      --> Windows Powershell
          --> Right Click Windows Powershell ISE          
            --> More 
               --> Run as administrator
For the purpose of the lab, security will be bypassed to execute script with the following:

PS C:\Windows\system32>Set-ExecutionPolicy Unrestricted --> Enter

--> Click Yes to All

![Screenshot 2023-12-30 221327](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/c2289641-0534-4fa6-a16a-557be9399034)

--> Click Open Script Folder
  --> Select Create Users script file

Navigate to location of script file(Desktop of user Jon Doe in this example)

--> Click Run Script

![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/8e64d752-5a2a-4d57-be04-193e34d857ac)


![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/134c774e-185b-4c22-baa6-62f67676e9fb)

Navigating back to the Active Directory, a new Users folder was created and is populated with the added
users

![image](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/8d478ce4-cc94-48c6-bdd1-52a96b7e76ad)

_____________________________________________________________________________________________________________________________________________________________________________





<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
