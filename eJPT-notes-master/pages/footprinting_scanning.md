]# Footprinting & Scanning

This is the infrastrucutre part of the information gathering.

### Mapping a network

Mapping a network helps the pentester get an idea of how the network is structured.

### Ping sweep

Ping sweeping helps find all live hosts in a network range.

```
fping -a -g 192.168.1.0/24 2>/dev/null
nmap -sn 192.168.1.0/24
```

### OS fingerprinting

OS fingerprinting is the process of determinig the operating system used by a host on a network.

```
# OS Detection, no ping
nmap -Pn -O <target(s)>
```

### Port Scanning

Port scanning allows for discvoery of running daemons and services of each node on the network.

```
# TCP SYN scan or stealth scan
nmap -Ss -sU<target>

-sU (UDP)

# Scripts and version detection
nmap -sC -sV <target>

# All ports, scripts, version
nmap -sC -sV -p- <target>

-p
This would make your scan slow compared to the default (fast) scan, but you would get a much better idea of the open ports available on the target machine!

# UDP and Version check
nmap -sU -sV <target>

# Most used scan
# OS, version, scripts, traceroute, and all ports
nmap -A -p- <target>
-A (SCAN FOR EVERTHING)

# Find the host name of the scanned machine
cat /etc/hosts

# Nmap script to determine information about the NoSQL database (MongoDB).
nmap -p27017 --script=mongodb-info target-2 | less
OR 
nmap -p27017 --script=mongodb-databases target-2

# Nmap script to perform brute force password auditing against the MongoDB database
nmap -p27017 --script=mongodb-brute target-2

# Nmap script to determine information about the SQL database (MySQL).
run all scripts related to MySQL
nmap --script=mysql-* target-1
