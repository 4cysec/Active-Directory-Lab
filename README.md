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


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/99ed1965-aee3-47a2-ae19-db3182551cc5" width="500" height="300" />
     
                                                                                                                                          


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/e09cd02d-f9ff-45f8-93dc-dc8569e5de8b" width="500" height="300" />




Navigate to the Network configuration in the left pane--->Network

Set Adapter 1 to Attached to: NAT for the DC connection to the Internet


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/596577bd-7d05-4f68-9d5a-43fe385ebe21" width="500" height="300" />



Set Adapter 2 to Attached to: Internal for the DC connection to the internal network


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/fd5e6729-5dcb-473b-9449-c7710eb97626" width="500" height="300" />



Once the Server 2019 ISO is installed on the VM. The Domain Controller is configured below.

___________________________________________________________________________________________________________________________________________________________________

<p align="center"><b>Setting up IP Addresses</b><br/>



To set up IP addressing to our NICs for External and Internal network click internet
icon in the bottom right corner of display. 



<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/e0ef3084-2058-4446-8e08-80027034d4bb" width="500" height="300" />



<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/78353ba8-4621-4edd-b23e-64ab1cce3d36" width="500" height="300" />



<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/bf14e3bc-5b96-43c1-8515-f566bfcb86f5" width="500" height="300" />



-->Network Connections
  -->Change Adapter Settings
   -->Adapter1(Ethernet)
      -->details


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/73b08200-83db-48ee-9e86-94f50b28294d" width="500" height="300" />
      



      
-->Adapter2(Ethernet2)
      -->details

<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/d7c8f2ae-113d-46fa-9e44-8e09c062a3f4" width="500" height="300" />


The Domain Controller will connect to the internet(external) through the home router
thus the first ethernet IP can be considered the external IP.

-->Right Click and rename the first adapter "Internet"

The second adapter has an auto configured IP address. 

The second adapter will face the internal network.

-->Rename adapter2 "Internal Net"

-->Go to properties within "Internal Net" adapter

-->Click Internet Protocol Version 4 

<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/f26a790f-e3b1-464a-8260-4e16ddb8803e" width="500" height="300" />
 

Using Josh Madakor's Tutorial network information, the following is entered:
IP:  172.16.0.1
Mask: 255.255.255.0
DNS: 127.0.0.1

The Domain Controller will act as a Gateway so no entry.

Using default "self pinging" address for DNS. As DC will serve as the DNS.


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/b03f78bd-8138-460b-ab7f-0cdfece1d69a" width="500" height="300" />

________________________________________________________________________________________________________________________________________________________________________


<p align="center"><b>Install and Configure Active Directory Domain Services</b><br/>

From the Server Manager Dashboard

-->Go to Add roles and features

<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/4a528cbc-fccc-40a8-8ef8-5e0a446bf9b5" width="500" height="300" />


[Before You Begin] --> Click Next

[Installation Type] --> Select Role-based or feature based installation
                    -->Click Next

 [Server Selection] --> With Domain Controller and External IP selected Click Next                  
                   
 
 <img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/adc05821-d203-4845-b64f-b3428e4222d2" width="500" height="300" />                  


[Server Roles] --> Select Active Directory Domain Services
               --> Click Add Features
               --> Click Next
               

<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/7b68a97d-3f29-4ae8-a1d9-113b003544f7" width="500" height="300" />
 

 [Features] --> Click Next(with pre selected boxes)

 [AD DS] --> Click Next

[Confirmation] -->Click Install

After Installation of AD DS

Click on alert notification and link "Promote this server to domain controller"

<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/c9023405-2e0b-44bd-ada3-367a8c8fe6db" width="500" height="300" />


[Deployment Configuration]--> Select add a new forest
    Provide a domain name. (Mydomainlab.com) used in this example.

<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/712a6c34-ce24-4699-8bdb-caf9978554ee" width="500" height="300" />


[Domain Controller Options] --> Enter chosen password

[DNS Options]--> Click Next(no selection)

[Additional Options] --> Next

[Paths] --> Next

[Review Options] --> Next

[Prerequisites Check]--> Install

______________________________________________________________________________________________________________________________________________________________________

<p align="center"><b>Creating Domain, Organizational Unit & New User</b><br/>

After installation and reboot
--> Click Start Icon
   --> Windows Administrative Tools Folder
     --> Click Active Directory Users and Computers
The created domain can be seen in the left pane: mydomainlab.com


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/c05ec5fa-c31c-4f5c-992a-b71b2735fe71" width="500" height="300" />



--> Right Click domain(in this case mydomainlab.com)
   -->New
     --> Organizational Unit
       -->Name the organizational unit(named _ADMINS in this lab)


       
<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/8a7735ae-166e-44f4-b031-e11298aa6b54" width="500" height="300" />



This creates a folder _ADMINS
--> Right click _Admins
  -->New
    --> User
 Fill user name, logon name and password(Jon Doe, a-jdoe for this lab)
 For the purpose of the lab, "password never expires" was checked.


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/de956ef6-a055-4e67-821c-fec9d3635a44" width="500" height="300" />
 

To make the new user an admin
-->Right click on the user
  -->Properties
    -->Member Of tab
      -->Click Add
         -->Name assigned user group(Domain Admins)
           --> Apply
             -->OK

<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/2c849e27-a8a2-4f1b-8049-b7e369153915" width="500" height="300" />


The new admin user jdoe was created and can now log into the domain as Jon Doe.


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/a403c71a-992f-444c-a612-77d8ea003651" width="500" height="300" />


___________________________________________________________________________________________________________________________________________________________________________

<p align="center"><b>Internal Network Set Up</b><br/>

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


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/d3ea9f11-ace4-4aed-ac0b-1408c320dc85" width="500" height="300" />


In Server Manager Dashboard --> Tools (top right)


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/f7e6290f-01af-4c7a-9fb0-987d2b5bf511" width="500" height="300" />


Select domain controller name local(DomConlocal)
-->Right Click on selection above
  -->Configure and Enable Routing and Remote Access


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/5ace9e2f-aa39-4fdd-a825-d31480783e32" width="500" height="300" />


   --> Next

Select Network address translation --> Next

Select the Internet set up in previous steps as public interface --> Next


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/8f5d473b-c089-4fcc-ad3a-555fe761fada" width="500" height="300" />


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


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/6478eda9-50af-4de4-bd19-93d0b9a34362" width="500" height="300" />


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/d864b0d7-42dc-4086-832c-2ff3e7fb0f86" width="500" height="300" />


--> Next
[Add Exclusions and Delay] --> Next

[Lease Duration] 8 days pre selected as duration of time assigned IP addressing is valid for clients
               --> Next
[Configure DHCP Options] Yes...selected --> Next

[Router (Default Gateway)] The domain controller will act as the router of network traffic from 
the internal network to the Internet. Thus, the IP address of the DC Server is used.
-->172.16.0.1 -->Add--> Next


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/c49d8d59-ab1f-4a50-a463-c52fc6e35359" width="500" height="300" />


[Domain Name and DNS Servers] The DC Server with Active Directory Domain Services acts as the DNS
                              --> Next
[WINS Servers] --> Next

[Activate Scope] Yes...selected --> Next --> Finish

In DHCP Box --> Right Click DC directory-->Click Authorize


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/30898304-d725-44c3-b65f-f7b2d9413671" width="500" height="300" />           

            
--> Right Click DC directory--> Refresh


Green check marks on IPv4/IPv6 icons indicate successful configuration.

Under IPv4 directory-->Select and right click Server Options-->Configure Options

-->Check box 003 Router option

-->Add domain controller's IP address as gateway: 172.16.0.1 for this lab -->Add--> Apply


_____________________________________________________________________________________________________________________________________________________________________

<p align="center"><b>User Additions Using Powershell Script</b><br/>

Using Josh Madakor's powershell script and a notepad file with generated user names(seen below),
new users will be added to the directory in an automated fashion. This greatly shortens 
time in comparison to adding users manually.


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/3a0d1475-bf56-40f9-81b8-38ac47a4186a" width="500" height="300" />


  In Windows
  --> Start 
      --> Windows Powershell
          --> Right Click Windows Powershell ISE          
            --> More 
               --> Run as administrator
For the purpose of the lab, security will be bypassed to execute script with the following:

PS C:\Windows\system32>Set-ExecutionPolicy Unrestricted --> Enter

--> Click Yes to All


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/c2289641-0534-4fa6-a16a-557be9399034" width="500" height="300" />


--> Click Open Script Folder
  --> Select Create Users script file

Navigate to location of script file(Desktop of user Jon Doe in this example)

--> Click Run Script

<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/8e64d752-5a2a-4d57-be04-193e34d857ac" width="500" height="300" />


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/134c774e-185b-4c22-baa6-62f67676e9fb" width="500" height="300" />


Navigating back to the Active Directory, a new Users folder was created and is populated with the added
users


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/8d478ce4-cc94-48c6-bdd1-52a96b7e76ad" width="500" height="300" />


_____________________________________________________________________________________________________________________________________________________________________________

<p align="center"><b>Adding A Windows Client</b><br/>

Now the virtual Windows 10 computer will be added to our system.  This is the same as a business/corporate
computer or laptop that is a part of the business's network.


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/daecd6a8-a0d2-4463-bc2a-f41f98d72025" width="500" height="300" />


In the Virtual Box Manager -->Click New
                          --> Provide Name(Windows Client1)
                          -->Choose Windows ISO file location(skip unattended installation checked)
                          -->Windows 10 64 bit in dropdown(Iff applicable. It may be auto configured)
                          -->Next
    Choose hardware and disk configurations and click finish.

With the Windows VM highlighted, go to settings-->Advanced Tab

Selecting Bidirectional for Shared Clipboard and Drag 'n' Drop allows for copying and pasting and 
dragging and dropping of files between the host and virtual machines.

Navigate to the Network in the left pane--->Network

Set Adapter 1 to Attached to: "Internal" for the client's connection to the internal network

Run the Windows Client1 VM

Navigate through the Windows Setup screens for installation of Windows 1

Note:  In this lab "No product key" option is picked. Furthermore, Windows 10 Pro version is 
       installed. Custom Copy is installed as the virtual PC is blank.

When setting up Windows after installation for this lab, no internet, limited set up, and 
username of "User" without any password is chosen.

After Installation run Windows Client1 machine

Network Connectivity can be checked:

Open command prompt type CMD in search prompt in Windows.

ping a website for response ex. www.yahoo.com


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/02613fc0-1431-478b-a8a2-63f59074be0a" width="500" height="300" />


Reply indicates connectivity is successful.

Renaming/Joining the Domain is done as follows:

Right Click Start-->System-->Rename This PC(Advanced) --> Change

Computer Name: WindowsClient1

Domain: mydomainlab.com

--> Ok


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/2d1bdbca-1036-4879-a103-8d4d56c8b870" width="500" height="300" />


Username/Password is entered using admin credentials from the DC. a-jdoe/Password1

After the set up, it is now possible to sign into the WindowsClient1 host with one of our previously generated
accounts.

Choosing user John Bartram and signing in as other user into mydomainlab.com. 


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/e328a5f9-1d67-4402-83f7-ce94f1accb09" width="500" height="300" />


<img src="https://github.com/4cysec/Active-Directory-Lab/assets/149924544/d39896f1-40be-46d4-a66e-c8cc703838d3" width="500" height="300" />




<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
