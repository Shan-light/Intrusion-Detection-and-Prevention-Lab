# Intrusion-Detection-and-Prevention-Lab
Suricata was install and configure on a MARS Kali Linux environment to act as both an Intrusion Detection System (IDS) and an Intrusion Protection System (IPS).

## Objective
Install and configure Suricata on a Kali Linux system.

Demonstrate and understand the difference between IDS and IPS modes of suricata.

Gain practical experience in network traffic monitoring, rule configuration, and alert generation.

Simulate real-world intrusion scenarios to observe how Suricata detects and prevents threats in real-time.

### Skills Learned
- Network Security Fundamentals - Understanding core concepts of Intrusion Detection Systems (IDS) and Intrusion Prevention Systems (IPS)
- Passive mode (detects threats and generates alerts- IDS) and active mode (blocks or prevents detected malicious traffic from entering the network - IPS).
- Suricata Installation and Configuration - Installing Suricata on a Kali Linux environment
- Configuring Suricata to operate in IDS and IPS modes
- Managing Suricata rule sets and YAML configuration files
- Traffic Analysis and Threat Detection - analyzing real-time network traffic, Suricata logs and alerts
- Identify malicious activity based on predefined rule sets
- Linux System Administration - Editing system config files with vim, nano, or other CLI editors
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- Suricata - a network sercurity tool used to monitor network traffic in real-time to detect and prevent malicious activity.Suricata can be integrated into Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Kali Linux Terminal

## Steps

### 1. Update the Kali Linux Operating System (OS).

- The system was updated before installing Suricata to ensure that the system is stable, secure, and compatible with the latest security patches.
- using the commands" sudo apt update -y


I encountered the “NO_PUBKEY ED65462EC8D5E4C5” error while trying to update the Kali Linux system, which is a GPG (Gnu Privacy Guard) key error. A GPG key error in Kali system means APT cannot find the key to verify Kali’s repository. The solution is to add the correct public key to APT’s key ring or file. The Offensive Security organization had lost access to their old repository signing key (ID ED444FF07D8D0BF6) so initiated and published a new key (ID ED65462EC8D5E4C5) for older Kali versions (Arun, 2025). 




*Ref 1: Network Diagram*
