### Covenant 

Before nstalling Covenant we have to install .net framework
mkdir -p $HOME/dotnet && tar zxf dotnet-sdk-3.1.418-linux-x64.tar.gz -C $HOME/dotnet
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet

git clone --recurse-submodules https://github.com/cobbr/Covenant

dotnet run

Login URL: https://127.0.0.1:7443/home/index


Grunts: User sessions

####  PIVOTING
HACK THE FIRST MACHINE

### METASPLOIT PIVOTING
meterpreter>> run arp_scanner -r 

msf >> route add 10.10.10.2 255.255.255.0 session_Number

search tcp scanner
aux/scanner/portscan/tcp


https://www.youtube.com/watch?v=0lJ0a3E4lWc

# Metasploit has an AutoRoute meterpreter script that will allow us to attack this second network through our first compromised machine.

background

use post/multi/manage/autoroute

info

### SOCKS PROXY

### PROXY CHAINS