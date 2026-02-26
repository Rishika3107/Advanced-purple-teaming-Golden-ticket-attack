# Day 1: Initial Compromise & Payload Injection
The opening phase of the simulation involved external threat actors probing the organization’s segmented network and establishing initial persistence, while defenders
responded reactively, relying on manual detection and forensic investigation to uncover subtle signs of compromise.

---

# Red Team Perspective
The attackers commenced their campaign using ROG-ATK01.extlab, launching a deliberately stealth nmap scan (Fig 1.1) across the target subnets to evade detection and
identify potentially vulnerable systems. Their efforts revealed two endpoints: HOST-PRX01.eu.corp and SRV-BADPYR02.apac.int, each accepting SSH connections. Utilizing
previously compromised credentials belonging to user Sebastian, the red team established remote access and discreetly uploaded a custom JavaScript payload. By leveraging 
wscript.exe, they executed the heavily obfuscated malware, which transformed itself into an executable and silently initiated communication back to the rogue device over
non-standard TCP ports. With command-and-control channels operational, the attackers configured proxychains for further exploration and lateral movement, securing resilient 
persistent access as the first stage ended.

# Blue Team Perspective
Unaware of the ongoing intrusion due to advance adversarial tactics and authorized process usage, the blue team detected no alerts during the initial compromise. 
Suspecting unusual network behavior, defenders turned to proactive logging and asset inventory checks. Through meticulous review of NAC data (Fig 1.2), they identified
the presence of ROG-ATK01.extlab (a non-corporate device) on the network. Further analysis of firewall logs mapped SSH sessions linking the rogue host to the compromised
endpoints (Fig 1.3). Endpoint telemetry provided the next clue: investigators observed unfamiliar wscript.exe executions paired with suspicious JavaScript files and new
executables in abnormal directories (Fig 1.4). Disassembling the payload, they noted multi-layered obfuscation and persistent autorun logic, confirming the sophistication 
of the breach and highlighting the need for enhanced behavioural detection. (Fig 1.5)
