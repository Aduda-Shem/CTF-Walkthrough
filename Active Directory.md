# ACTIVE DIRECTORY

Directory services developed by Microsoft to manage windows domain networks.

Stores information related objects, such as Computers, Users, Printers etc. (Acts like a phonebook for Windows)

Authenticates using kerberos - Non-windows devices such as Linux machines, firewalls etc. can also authenticate to Active Directory via RADIUS or LDAP


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


