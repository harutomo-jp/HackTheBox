<p align="center"><img src="./img/codifylogo.png" width="100"></p>

### HackTheBox - Codify

<b>Machine Rating:</b> Easy

---

Upon receiving the machine IP address, begin recon by performing a nmap scan.

```sudo nmap -sS -O -sV -p- -vvv --script=vuln -oN nmap-scan.txt 10.10.11.239```

