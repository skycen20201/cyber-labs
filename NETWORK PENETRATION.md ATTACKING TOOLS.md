"TOOLS AND COMMAND FOR NETWORK TEST ATTACK"

Nmap - port/service discovery, OS fingerprinting. Use to find open ports and running services
sudo nmap -sn -PE 192.168.254.0/24  - to check whos online only 
nmap -sn -T4 -n 192.168.254.0/24  - tells you what host is up with no port scan
nmap -p22,80,443 --open 192.168.254.0/24 - This will show only hosts that are actually responding on open ports — not just “alive.”
sudo ip neigh flush all- That will show only devices that respond to TCP connections (e.g., SSH, web servers).

nmap --script vuln -p22 192.168.168.130 -oN nmap_vuln_ssh - Check for known scriptable issues:
sudo nmap -sU -p 53,67,69 -T3 192.168.168.130 -oN nmap_udp - used to perform a specific UDP port scan on a target IP address


"after all the scanning use the command below to extract all ports that open"
OPENPORTS=$(grep -oP 'Ports: \K[^ ]+' ports.gnmap | tr ',' '\n' | cut -d'/' -f1 | paste -s -d,)
nmap -sC -sV -p"$OPENPORTS" -T4 -oA nmap_enum 192.168.168.130

  "MASSCAN SCANING"
  sudo masscan 192.168.168.0/24 -p22,80,443 --rate 1000 -oG masscan_quick.gnmap  - Quick scan a subnet for common ports
  sudo masscan 192.168.168.130 -p1-65535 --rate 2000 -oJ masscan_full.json -  Full TCP port sweep on a single host

  "AFTER ALL SCAN MASSCAN run the commands below to printout the output"
  sudo masscan 192.168.168.0/24 -p1-65535 --rate 1000 -oG masscan_all.gnmap
  grep "open" masscan_all.gnmap | awk '{print $2}' | sort -u > masscan_hosts.txt
  cat masscan_hosts.txt
  
