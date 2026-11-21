## **What is Active Directory?**

Active Directory is a Service Developed by Microsoft to manage windows domain networks. It Stores Information Related to objects such as Users, Groups, GPOs, Computers, Printers etc...

it Authenticates using Kerberos Tickets.

non-Windows devices such as linux, can also authenticate in Active Directory by using RADIUS or LDAP.

Active Directory is the most commonly used identity management service in the world, 95% of Fortune 1000 Companies implement this service in their networks.

## **Active Directory Components**

--- **PHYSICAL AD COMPONENTS** ---

**1. Domain Controller**

A domain controller is a type of server that processes requests for authentication from users within a computer domain. Domain controllers are most commonly used in Windows Active Directory (AD) domains but are also used with other types of identity management systems.

![[Pasted image 20251219190655.png]]

_**What is a domain controller used for?**_

The primary function of domain controllers is **to authenticate and validate users on a network**, including group policies, user credentials, and computer names to determine and validate user access.

**2. The AD DS Data Store**

The AD DS data store contains the database files and processes that store and manage directory information for users, services, and applications.

• Consist of_ **Ntds.dit**_ _file_

--- **LOGICAL AD COMPONENTS** ---

**1. The AD DS Schema**

• Defines every type of object that can be stored in the directory

• enforces rules regarding object creation and configuration

![[Pasted image 20251219190710.png]]

**2. Domains**

Domains are used to group and manage objects in the organization.

![[Pasted image 20251219190715.png]]

**3. Trees**

A Tree is a hierarchy of domains in AD DS

![[Pasted image 20251219190719.png]]

**4. Forests**

Forest is a Collection of one or more domain trees.

![[Pasted image 20251219190724.png]]

**5. Organizational Units (OUs)**

OUs are the Active Directory containers that contain users, groups, computers and other OUs.

![[Pasted image 20251219190731.png]]

**6. Trusts**

![[Pasted image 20251219190739.png]]

**7. Objects**

![[Pasted image 20251219190744.png]]