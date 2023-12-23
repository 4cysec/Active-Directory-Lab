<h1>Active-Directory-Lab</h1>

<h2>Description</h2>
A domain controller server is established with Active-Directory Domain Services(AD DS). Users are added manually and with a powershell script. The Domain Controller faces the internet while sharing an internal network with a Windows 10 client.  All of this is done within a virtual environment.

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

Set Adaptor 1 to Attached to: NAT for the DC connection to the Internet


![Screenshot 2023-12-22 201501](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/596577bd-7d05-4f68-9d5a-43fe385ebe21)


Set Adaptor 2 to Attached to: Internal for the DC connection to the internal network

![Screenshot 2023-12-22 201525](https://github.com/4cysec/Active-Directory-Lab/assets/149924544/fd5e6729-5dcb-473b-9449-c7710eb97626)

Once the Server 2019 ISO is installed on the VM. The Domain Controller is configured below.

<p align="left"><b>Setup IP Addresses</b><br/>




<p align="left"><b>Install and Configure Active Directory Domain Services</b><br/>





    
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
