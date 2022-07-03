# SCANNING and ENUMERATION
----------------------------------------------------------------------                                                                                     
## SCANNING WITH NMAP:

  `root@kali:-# arp-scan -l`
  
And look for vmware

  `root@kali:-# ifconfig`
  
Identifying your ip adress

   `root@kali:-# netdiscover -r 192.168.57.0/24`
   
Use ctrl+C to kill this session

    `root@kali:-# nmap -T4 -p- -A 192.168.57.134`
    
There are 65535 ports out there

     `root@kali:-# nmap --help`


## ENUMERATING HTTP AND HTTPS part 1

80/443 - 192.168.57.134

Dafult webpage -Apache -PHP

Information disclosure -page 404

Information disclosure - server headers disclose version information

Nikto is a web vulnerability scanner.

   `root@kali:-# nikto -h https://192.168.57.134`
   
If https doesn’t work try http instead
    `root@kali:-# nikto -h http://192.168.57.134`


Part 2
Dirbuster and dirb and go buster are used to do web busting

Running dirbuster;
      `root@kali:-/kioptrix# dirbuster&`
      
We inspect page source to look for comments or anything that is diclosed which shouldn’t be disclosed.

In response codes;

200 means OK

400 means an error

300 means redirect

500 means server errors


## ENUMERATING SMB
SMB is a file share.

In computer networking, Server Message Block (SMB), one version of which was also known as Common

Internet File System (CIFS), is a communication protocol for providing shared access to files, printers, and
serial ports between nodes on a network.

Metasploit is an exploitation framework
   `root@kali:-# msfvenom`
   
To startup metasploit framework

Metasploit framework - RECON,EXPLOIT,PAYLOAD,LOOT
     `Msf>smb`
     
To search smb
    `Msf5> use auxiliary/Scanner/smb/smb_version`
    `Msf5 auxiliary(Scanner/smb/smb_version) > info`
    `Msf5 auxiliary(Scanner/smb/smb_version) > options`
    `Msf5 auxiliary(Scanner/smb/smb_version) > set RHOSTS 192.168.57.139`
    `Msf5 auxiliary(Scanner/smb/smb_version) > run`
    
The ability to scan and enumerate will make you a great pemtester

Now lets look at a new tool called smbclient that will help us connect to the file shell out there
    `root@kali:-# smbclient -L \\\\192.168.57.134\\`
    `root@kali:-# smbclient \\\\192.168.57.134\\ADMIN$`
    `root@kali:-# smbclient \\\\192.168.57.134\\IPC$`

## ENUMERATING SSH
   `root@kali:-# ssh 192.168.57.134`
   `root@kali:-# ssh 192.168.57.134 -oKexAlgorithms=+diffie-hellman-group1-sha1`
   `root@kali:-# ssh 192.168.57.134 -oKexAlgorithms=+diffie-hellman-group1-sha1 -caes128-cbc`

##  Researching Potential vulnerabilities
-------------------------------------------
Enumeration is defined as the process of helping the attacker collect information about:

● Network resources

● Shares

● Users and/or groups

● Machine names

● Routing tables

● Applications and banners

● Auditing and service settings

● SNMP and DNS details

Enumeration will help us to identify the vulnerabilities present in the target system. This information will
help us to set our strategy and make the attack easier and more effective.
There are many different techniques used for enumeration. We are going to explore the most
commonly used ones. Before the “scanning” phase, we already knew what ports were open so
we partially know what we are going to enumerate:
• Extracting usernames using email IDs
• Extract information using the default password
• Brute Force Active Directory
• Extract information from LDAP (TCP/UDP 389)
• Global Catalog Service
• Extract usernames using SNMP (UDP 161) and SNMP trap (UDP 162)
• Extract information using DNS Zone transfer (TCP 53)
• Extract information using SMTP (TCP 25)
• Extract information using SMB (TCP 139)
• Extract information using Microsoft RPC Endpoint Mapper (TCP 135)
• Extract information using NetBIOS Name Service NBNS (TCP 137)
• Extract information using NTP Enumeration (UDP 123)
Enumeration Tools on Linux and Windows


## SMTP Enumeration
● NetScanTools Pro is a Windows tool with a graphical user interface, it is an email
generator and email relay testing tool.
● SMTP-user-enum is a tool that enumerates OS-level user accounts on Solaris (UNIX)
via the SMTP service.
● Metasploit offers the “auxiliary/scanner/SMTP/smtp_enum” module that helps to
enumerate usernames.

## NetBIOS Enumeration
● Nbtstat is a tool in Windows that displays protocols’ statistics, NetBIOS name tables and
name cache.
● SuperScan is a tool in Windows that scans ports and resolves hostnames.
● Hyana is a tool that shows user login names for Windows servers and domain
controllers.
● Netview is a command line tool to identify shared resources on a network.
SNMP Enumeration
● Rory McCune’s snmpwalk wrapper script helps automate the username enumeration
process for SNMPv3.
● OpUtils is a tool for Windows and Linux that helps to monitor, diagnose, and
troubleshoot IT resources.
● SNMP-check allows enumerating the SNMP devices and returns the output in a
human-readable format.

## LDAP Enumeration
● LDAP Admin Tool or JXplorer is a cross-platform LDAP browser and editor that can
be used to search, read, and edit any standard LDAP directory. It can be used on Linux,
Windows, and many other operating systems.
● Windapsearch is a Python script to help enumerate users, groups, and computers from a
Windows domain through LDAP queries.

## NTP Enumeration
● ntptrace is a utility available on Linux to trace a chain of NTP servers.
● ntpdc and ntpq are utilities available on Linux to monitor the operation of the NTP
daemon.

## DNS Enumeration
● nslookup is one of the oldest DNS querying tools to obtain a domain name to IP address
mapping and other DNS details.
● host or dig (domain information groper) are utilities available on Linux that help to query
DNS servers and perform DNS lookups.

## SMB enumeration
● SMBMap allows users to enumerate share drives across an entire domain.
Other Helpful Enumeration Tools Provided with Kali
● theHarvester gathers emails, subdomains, hosts, employee names, open ports, and
banners from different public sources like PGP key servers and SHODAN.
● Enum4linux is a tool to enumerate information from Windows and Samba systems.
● Devploit is a simple python script for Information Gathering.
● Red Hawk v2 is an all-in-one tool for Information Gathering.
● Metagoogil is a tool that utilizes the Google search engine to get metadata from the
documents available in the target domain.
