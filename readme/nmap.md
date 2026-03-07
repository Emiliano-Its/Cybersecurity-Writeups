# Nmap

Nmap is a tool for scanning a host, we need a ip address

* Install:

```
sudo apt install nmap -y
```

Example of usage:

```
nmap -sV -sC -p [PORT] [IP] -Pn -n -vvv
```

-sV: Find Version scan

-sC: Default script activate

-p-: For all ports - 65,535)-p

\--top-ports 1000

\--open: only ourput the open ports

-oA \[NAME]: storage the results in all the formats with the “\[NAME]”

-sn: Disable port scanning

\--disable-arp-ping

-n: disbale dns resolution

-vvv: report while the scan is running



[-T \[1-5\]](https://nmap.org/book/performance-timing-templates.html) : define the timming, agressivnes of our scan.

\-

D RND \[NUMBER]: define random ip address source

\--source-port \[PORT]: escpecify the source port number

ENGINE

-sT: Full TCP SCAN, more accurate, least stealthy.

-sA= Acknowldge flag scan (check FIREWALLS)

-sS= SYN flag scan

-sSU= UDP and SYN scan (for dns, it could help)

TIming:

* `-T 0` / `-T paranoid`
* `-T 1` / `-T sneaky`
* `-T 2` / `-T polite`
* `-T 3` / `-T normal`
* `-T 4` / `-T aggressive`
* `-T 5` / `-T insane`

\--script=

### Nmap Scripting Engine (NSE)
