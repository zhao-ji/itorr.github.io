## nmap 简介

### 概要

- nmap (network mapper)
    - nmap -A targetip (全面进攻型扫描)

- nmap 主要功能

    - Host Discovery(主机发现)
    > nmap -sn 192.168.1.1/24

    - Port Scanning(端口扫描)
    > nmap -F 192.168.1.250(快速扫描前100个热门端口)
    > nmap 192.168.1.250 -p 80 (指定端口扫描)
    > nmap -r 192.168.1.1 (顺序扫描端口)

    - Version Detection(版本侦测)
    > nmap -sV 192.168.1.250

    - OS Detection(操作系统侦测)
    > sudo nmap -O 192.168.1.250(需要超级用户权限)

    - FireWall/IDS evasion(防火墙/IDS避规)


