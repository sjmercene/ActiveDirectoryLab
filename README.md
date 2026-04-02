# 🌐Active Directory Home Lab (Windows Server 2022 + Windows 10)

## Overview
This project documents the setup of a Windows Active Directory home lab using **Windows Server 2022** and **Windows 10 Pro** in a virtualised environment.

The goal of this lab is to simulate a basic enterprise network by deploying a Domain Controller, configuring DNS, creating users and groups, joining a client machine to the domain, and validating authentication and connectivity.

This project was built to strengthen my practical skills in:

- Windows Server administration
- Active Directory Domain Services (AD DS)
- DNS configuration
- User and group management
- Domain joining
- Troubleshooting connectivity and authentication issues

## Objectives
- Create a virtual lab environment with a server and client machine
- Install and configure Windows Server 2022
- Promote the server to a Domain Controller
- Create and manage users, groups, and Organizational Units
- Install and configure a Windows 10 client
- Join the client machine to the domain
- Validate DNS, authentication, and connectivity
- Document the build process and troubleshooting steps

## Lab Environment
### Virtual Machines
- **DC01** – Windows Server 2022
- **CLIENT01** – Windows 10 Pro

### Planned Domain
- **corp.local**

## Technologies Used
- Windows Server 2022
- Windows 10 Pro
- Active Directory Domain Services
- DNS
- VirtualBox
- GitHub

## Planned Network Configuration
- Server Name: **DC01**
- Client Name: **CLIENT01**
- Domain Name: **corp.local**
- Server Role: **Domain Controller / DNS Server**

## Build Stages
1. Lab Setup
2. Windows Server Installation
3. Network Configuration
4. Active Directory Installation
5. Domain Controller Promotion
6. DNS Validation
7. User, Group, and OU Creation
8. Windows 10 Client Setup
9. Domain Join
10. Validation and Testing
11. Troubleshooting
12. Key Skills Demonstrated


## Step 1 – Lab Setup
Two virtual machines were created to simulate a small Windows domain environment:

- **DC01** – Windows Server 2022 system that will be promoted to Domain Controller
- **CLIENT01** – Windows 10 Pro workstation that will be joined to the domain

Both machines were configured with appropriate CPU, RAM, and storage resources for lab testing. The network adapter (bridged) was set to support communication between the systems for domain, DNS, and authentication testing.

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/1.Lab%20Setup%20Settings.JPG" width="900">

---

## Step 2 – Network Configuration

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/3.Setting%20up%20Static%20IP.JPG" width="900">

A static IP address was configured on the Domain Controller (DC01).

### Configuration:
- IP Address: 192.168.0.50  
- Subnet Mask: 255.255.255.0  
- Default Gateway: 192.168.0.1  
- DNS Server: 192.168.0.1 (temporary)

Static IP is required for a Domain Controller to ensure consistent communication for DNS and authentication services.

---
## Step 3 – Server Configuration

### Rename Server
<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/2.Rename%20Server.JPG" width="900">


The server was renamed to **DC01** to follow standard enterprise naming conventions for Domain Controllers.

A restart was required for the change to take effect.

### Running Tests
After configuring the static IP address, connectivity was verified using ICMP (ping) tests.

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/4.Succesful%20Ping.JPG " width="900">



Tests included:
- External IP (8.8.8.8) to confirm network access  
- Domain name (google.com) to confirm DNS resolution  

Both tests were successful, confirming the server is properly configured for network communication.

---

## Step 5 – Install Active Directory Domain Services

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/5.Server%20Selection.JPG" width="900">

The Active Directory Domain Services (AD DS) role was installed on DC01 using Server Manager.

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/6.Active%20Directory%20Install.JPG " width="900">

This role enables the server to manage authentication, users, and domain resources within a Windows network.

After installation, the server was ready to be promoted to a Domain Controller.

---

## Step 6 – Domain Controller Promotion

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/7.Add%20new%20Forest.JPG " width="900">

The server was promoted to a Domain Controller by creating a new Active Directory forest.

### Configuration:
- Domain Name: corp.local  
- NetBIOS Name: CORP  
- DNS Server: Installed automatically  

A Directory Services Restore Mode (DSRM) password was also configured.

After installation, the server restarted and was successfully configured as a Domain Controller. The system now operates under the **corp.local** domain.

<br>

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/9.Succesful%20NS%20look%20UP.JPG " width="900">

### DNS Validation

The `nslookup` command was used to verify DNS functionality.

The domain **corp.local** successfully resolved to the Domain Controller's IP address (192.168.0.50), confirming proper DNS configuration.

Note: Initial commands were mistakenly entered inside nslookup interactive mode, which only accepts DNS queries.

---

## Step 8 – Identity Management (OUs, Users, Groups)

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/10.Creating%20new%20OUs.JPG " width="900">

Organizational Units (OUs) were created to structure the domain into departments:
- IT
- HR
- Sales

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/11.%20Creating%20Example%20Users.JPG " width="900">

Users were created within each OU to simulate real enterprise accounts.


<br>


<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/13.Creating%20Groups.JPG " width="900">

Security groups were created for each department to manage access and permissions.

<br>

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/14.%20Adding%20users%20to%20group.JPG " width="900">

Users were assigned to their respective groups, demonstrating group-based access control.


<br>


## Step 10 – Domain Join and Authentication

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/15.Configuring%20CLIENT01.JPG" width="900">

A static IP configuration and correct DNS settings were critical to ensure reliable communication with the Domain Controller.

<br>

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/16.Entering%20Domain.JPG " width="900">

The domain join process was performed using the domain name (corp.local), with DNS resolving the Domain Controller’s IP address.
The Windows 10 client (CLIENT01) was successfully joined to the **corp.local** domain using domain administrator credentials.

This step allows the client machine to authenticate against the Domain Controller and access domain resources.

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/16.Entering%20User%20details.JPG " width="900">

The configuration was validated by logging into the client machine using a domain user account.

This confirms that:
- Active Directory authentication is working
- DNS resolution is functioning correctly
- The client is fully integrated into the domain environment

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/16.Proof.JPG " width="900">

<br>

## What I Learned

This project provided hands-on experience building and troubleshooting a Windows domain environment.

Key learnings included:
- The importance of DNS in Active Directory environments
- Differences between NAT and Bridged networking in virtual machines
- How domain authentication works in enterprise environments
- The role of Organizational Units and group-based access control

## Conclusion

This lab successfully simulated a basic enterprise network environment, including a Domain Controller, DNS server, and client system.

The setup demonstrates practical skills in system administration, networking, and troubleshooting, which are essential for roles in IT support and cybersecurity.



## Troubleshooting
This section will include any installation, network, DNS, or domain join issues encountered during the lab build.

### OU Removing Deletion Protection Error

<img src="https://github.com/sjmercene/sjmercene/blob/Active-Directory-Images/14.%20Removing%20Deletion%20Protection%20Error.JPG " width="900">

While managing Organizational Units, an error occurred when attempting to delete an OU:

"You do not have sufficient privileges to delete this object, or it is protected from accidental deletion."

#### Cause
Active Directory protects OUs from accidental deletion by default as a safety mechanism.

#### Resolution
- Enabled **Advanced Features** in Active Directory Users and Computers  
- Accessed the OU properties  
- Disabled "Protect object from accidental deletion"  

After removing this protection, the OU could be deleted successfully.

### Windows Installation Error
During the Windows 10 installation, an error appeared:
"Windows cannot read the <ProductKey> setting from the unattended answer file"
This was caused by the virtual machine attempting an unattended installation with an invalid configuration.
### Fix:
The VM was recreated with the **“Skip Unattended Installation”** option selected, allowing for a manual installation. This resolved the issue.

### Network Connectivity Issue (NAT vs Bridged)

Initial connectivity tests failed with "Destination host unreachable" errors.

#### Cause
The virtual machines were configured using NAT networking, which isolates each VM and prevents direct communication between them.

#### Resolution
Both virtual machines were reconfigured to use **Bridged Adapter**, allowing them to exist on the same network and communicate directly.

After this change, connectivity between the Domain Controller and client machine was successfully established.

## Key Skills Demonstrated
- Windows Server administration
- Active Directory deployment
- DNS and networking fundamentals
- Identity and access management
- Troubleshooting in a virtual lab environment
- Documentation for technical projects

