# Breached Part I - Adversary on Linux Host!

Welcome to the "Breached Part I - Adversary on Linux Host!" lab.

In this lab, you will step into the shoes of a cyber security analyst and investigate a compromised Linux host. Your mission is to uncover the details of a security breach and understand the techniques used by an adversary to compromise the system.


The lab consists of four challenges, each presenting you with a different piece of evidence related to the breach. Your task is to carefully analyze the provided log files and snapshots to piece together the events that occurred during the attack.


## Challenge 1: Authentication Logs 1
In this challenge, you will analyze the authentication logs of the compromised Linux host. These logs contain information about successful and failed login attempts, providing valuable insights into the initial access by the attacker.


## Challenge 2: Authentication Logs 2
In this challenge, you will dive deeper into the authentication logs to identify evidence of a brute-force attack. Brute forcing involves attempting various passwords until the correct one is discovered. Your goal is to identify the patterns and techniques employed by the attacker during the brute force phase.


## Challenge 3: Bash History
In this challenge, you will examine the bash history of the compromised Linux host. The bash history contains a chronological record of commands executed by the attacker. By analyzing this history, you can uncover the specific commands used by the attacker to gain unauthorized access and install their malware on the system.


## Challenge 4: Running Process
In the final challenge, you will analyze a snapshot of the running processes on the compromised host. This snapshot provides an overview of the processes executed at the time of the breach. By examining this information, you can identify any suspicious or malicious processes initiated by the attacker.


Throughout the lab, pay close attention to timestamps, command syntax, and any anomalous or suspicious activities.

Remember, this lab is designed to enhance your skills in incident response and analysis. It will provide you with hands-on experience in investigating a compromised Linux host and understanding the tactics employed by adversaries. Good luck, and enjoy the challenge!

# Breached Part II - Adversary Move to Windows!
 
In this lab, you will continue your investigation as the adversary expands their intrusion into a Windows host on the same network. Your mission is to detect and analyze the activities carried out by the attacker on the compromised Windows machine.

The lab comprises three challenges, each focusing on a specific aspect of the attacker's actions:


## Challenge 1: Authentication Logs
In this challenge, you will delve into the Windows authentication logs to identify evidence of brute force attempts. Analyze the event logs related to authentication to uncover any suspicious or failed login attempts that may indicate the attacker's efforts to gain unauthorized access through password guessing or brute force techniques.


## Challenge 2: Powershell History Logs
In this challenge, you will investigate the PowerShell history logs on the compromised Windows host. PowerShell is a powerful scripting language often used by attackers. Your task is to search for events in the Windows event logs that capture PowerShell commands executed by the attacker. Specifically, focus on identifying PowerShell commands that download and execute additional malware on the compromised Windows machine.


## Challenge 3: Get-Process
In the final challenge, you will examine the results of the "Get-Process" command, which displays the list of running processes on the compromised Windows host. Study the output of this command carefully to identify any suspicious or malicious processes initiated by the attacker. Look for any unfamiliar or abnormal processes that may indicate the presence of malware or unauthorized activity.


Remember, this lab is designed to enhance your skills in incident response and analysis. It provides hands-on experience in investigating a compromised Windows host and understanding the tactics employed by adversaries. Good luck with the challenges and enjoy the learning experience!
