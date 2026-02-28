# Day 3: Deepening Active Directory Control & Exploitation
On the final day, the red team capitalized on their privileged position within Active Directory to solidify their dominance by tampering with critical security groups 
and computer accounts, while the blue team’s defensive measures began to catch up, albeit too late to prevent major compromise.

# Red Team Perspective
With unimpeded access to the domain controller and possession of forged Golden Tickets, the red team shifted their attention to manipulating core AD security structures. 
They strategically added a user account to a highly sensitive group, thereby broadening both the footprint and reach of their malicious access. Not only did they modify
group memberships, but they also created a new domain computer object, embedding it within the Domain Admin group using the compromised administrator credentials. These
actions enabled red team operators to establish enduring persistence, escalate further privileges, and potentially facilitate backdoor operations or data exfiltration for
future campaigns. By the end of Day 3, the attackers had realized their ultimate objective: complete and resilient administrative control over the Active Directory ecosystem,
with the ability to manage privileged accounts and computer objects at will.

# Blue Team Perspective
On the defensive front, the blue team finally received actionable alerts from their SIEM and endpoint monitoring solutions, specifically noting lateral movement events and 
group membership changes. However, the timing of these notifications meant that defenders were only just becoming aware of the depth of red team incursion. By the time 
analysts could review AD logs and investigate suspicious modifications, the attackers had already succeeded in altering sensitive group configurations and adding new computer
accounts under highly privileged groups. The revelations highlighted not only the technical adeptness of the adversaries but also emphasized critical delays in detection and
response. Post-incident reviews confirmed that earlier gaps in alert logic, particularly for domain object creation and group membership changes, had greatly limited the blue
team's effectiveness during the most pivotal moments of the attack.

