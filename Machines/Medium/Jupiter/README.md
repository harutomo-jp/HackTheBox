# HackTheBox - Jupiter

### Rating: MEDIUM

nmap scan, find port 80 is open hosting http

website is basic, nothing found through directory traversal

virtualhost enumeration finds a virtual host address kiosk.jupiter.htb

using gobuster: ```gobuster vhost -u http://jupiter.htb/ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain```

add new virtual hosts to /etc/hosts file

kiosk.jupiter.htb is a grafana site