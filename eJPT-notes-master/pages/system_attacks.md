# System Attacks


#### Malware "Malicious Software"

Malware is any software used to misuse computer systems with the intent to:

- Cause denial of service
- Spy on users activity
- Get unauthorized contorl over one or more computer systems
- Cause other maclicious activities 

## Password Cracking

### Check the hash algorithm used to hash the password present in the shadow file by checking
/etc/login.defs

grep -A 18 ENCRYPT_METHOD /etc/login.defs

### Copy the entry for the "admin" user and save it into a new file.
tail -n 1 /etc/shadow > admin.hash

### Unshadow
On linux the username/password details are stored in the following 2 files
/etc/passwd (All usernames)
/etc/shadow (password hash is stored in /etc/shadow)

Why use unshadow
The unshadow command will basically combine the data of /etc/passwd and /etc/shadow to create 1 file with username and password details.

```
unshadow /etc/passwd /etc/shadow > /file_to_crack.txt
```

### John The Ripper
Test JTR
/usr/sbin/john --test

```
john --wordlist=<path to wordlist> -users=usersfile hashfile

```
### JTR on the shadow file.
john /etc/shadow --wordlist=/root/Desktop/wordlists/1000000-password-seclists.txt

### Crack a password protected Microsoft file
1. Make sure the office2john is in the JTR folder (JTR FOLDER PATH: /usr/share/john/)

2. Dowload the office2john 
extract the crackable information from the file using the office2john python script.
~# wget https://raw.githubusercontent.com/magnumripper/JohnTheRipper/bleeding-jumbo/run/office2john.py

3. ### Extract the password hash of the word file
office2john.py MS_Word_Document.docx > hash.txt

4. Run John on the extracted hash of the word file.
john /root/Desktop/MS_FILE_HASH --wordlist=/root//Desktop/wordlists/1000000-password-seclists.txt 


### HASHCAT
hashcat -m 1800 -a 0 admin.hash /root/Desktop/wordlists/1000000-password-seclists.txt
