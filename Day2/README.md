# Day 2: Active Directory Enumeration & Privilege Escalation
The second phase of the engagement shifted toward sophisticated Active Directory attacks, with the red team exploiting privilege misconfigurations to escalate access, 
while the blue team accelerated forensic reviews to reveal the full extent of domain compromise.

# Red Team Perspective
Building on established persistence, the red team turned their attention to Active Directory enumeration and privilege escalation. A targeted review of account
permissions revealed that Sebastian held the powerful "WriteAccountRestrictions" privilege on DC1.corp.int. The attackers exploited this misconfiguration by searching 
for service accounts with registered SPNs, setting their sights on svc_john, the HTTP service account. After requesting a Kerberos ticket for svc_john and cracking it 
offline with Hashcat, the team acquired valuable credentials. They then manipulated the msDS-AllowedToActOnBehalfOfOtherIdentity attribute, enabling Sebastian to impersonate
privileged accounts. Using Impacket’s secretsdump.py, the attackers executed a DCSync attack, extracting NTLM hashes for both Administrator and krbtgt. This allowed them to 
forge Golden Kerberos tickets, securing unobstructed, near-invisible domain admin access.

# Blue Team Perspective
By Day 2, the blue team had clearly identified compromised endpoints and users but remained uncertain about the adversaries’ next moves. As activity escalated, alerts 
started arriving from Splunk SIEM and the EDR system. Recognizing the gravity of the situation, defenders proactively hunted for all logs associated with Sebastian, the
compromised account. During this investigation, security analysts observed anomalous actions originating from alternate domain controllers, confirming that Sebastian was 
not only active but traversing multiple DCs, conducting lateral movement. The team detected that Sebastian had altered the msDS-AllowedToActOnBehalfOfOtherIdentity attribute,
a major sign of privilege escalation. Critically, despite uncovering attribute changes, defenders failed to receive any direct alert about the specific target user, exposing 
a significant loophole in their monitoring solutions. EDR logs were used to verify the unauthorized lateral activity, affirming the attackers’ ability to move stealthily
between domain controllers.
