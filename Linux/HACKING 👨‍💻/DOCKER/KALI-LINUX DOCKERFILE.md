#docker

```bash
FROM kalilinux/kali-rolling

RUN apt update -y ; apt upgrade -y ; apt autoremove -y ; apt install git -y ; apt install python3 -y ; apt install python3-pip -y

RUN apt install bettercap -y && apt install metasploit-framework -y

RUN apt install hydra -y && apt install nmap -y && apt install aircrack-ng -y && apt install crackmapexec -y && apt install wfuzz -y && apt install gobuster -y && apt install john -y && apt install crunch -y && apt install netcat-traditional -y && apt install hping3 -y

RUN apt install python3-impacket -y && apt install arp-scan -y && apt install impacket-scripts -y && apt install airgeddon -y && apt install set -y

RUN apt install nano -y && apt install whatweb -y && apt install net-tools -y && apt install iputils-ping -y && apt install exploitdb -y

RUN apt install wpscan -y && apt install sqlmap -y && apt install wifite -y && apt install ffuf -y

RUN apt install macchanger -y && apt install dsniff -y
```

### BUILD
```bash
docker build -t kali-img .
```

### RUN
```bash
docker run -dit --privileged --network=host --name kali-cont kali-img
```



---
- [[DOCKER-MANUAL]]