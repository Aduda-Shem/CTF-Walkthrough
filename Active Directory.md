# ACTIVE DIRECTORY

Directory services developed by Microsoft to manage windows domain networks.

Stores information related objects, such as Computers, Users, Printers etc. (Acts like a phonebook for Windows)

Authenticates using kerberos - Non-windows devices such as Linux machines, firewalls etc. can also authenticate to Active Directory via RADIUS or LDAP

The RADIUS server authenticates the user credentials and checks the user's access privileges against its central database, which can be in a flat-file format or stored on an external storage source such as SQL Server or Active Directory Server.

LDAP - core protocol behind AD

Active directory is the most commonly used to identify management service in the world.
Can be exploited without ever attacking patchable exploits. instead we abuse features, trust, components, and more.

# PHYSICAL ACTIVE DIRECTORY COMPONENTS
# Domain Controller
A domain controller is a server with the AD DS server role installed that has specifically been promoted to a domain controller.

Functions:

- Host a copy of the AD DS directory store.
- Provides authentication and authorization services
- Replicate updates to other domain controllers in the domain and forest
- Allow administrative access to manage user accounts and network resources.

# AD DS Data Store
This contains the database files and processes that store and manage directory information for users, services, and applications

Functions:

- Consists of the Ntds.dit(contains everything in domain controller including password hashes) file
- Is stored by default in the %systemRoot%\NTDS folder on all domain controllers
- Is accessible only through the domain controller processes and protocols

# ATTACKING ACTIVE DIRECTORY 
First we need to find our way into the network through abusing features of windows.

# 1.LLMNR POISONING - LINK LOCAL MULTICAST & NAME RESOLUTION
used to Identify hosts when DNS fails ti do so.

Previously known as NBT_NS.

Key flaw is that the services utilize a user's username and NTLMV2 hash when appropriately responded to.

We will use a tool called `Responder`

`python Responder.py -I tun0 -rdw -V`

Run the tool and wait for connection :

STEPS:
- Run Responder
- An Event occurs
- Get some hashes
- Crack the hashes 


