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

- The system must be updated before installing Suricata to ensure that the system is stable, secure, and compatible with the latest security patches.
- using the commands: *sudo apt update -y*
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/5efb002473dd8d3e230322077a4169812cb378f9/images/suricata%20update1.png"/>
  Task 1.1: Image 1

 - I encountered the “NO_PUBKEY ED65462EC8D5E4C5” error while trying to update the Kali Linux system, which is a GPG (Gnu Privacy Guard) key error. A GPG key error in Kali system means APT cannot find the key to verify Kali’s repository. The solution is to add the correct public key to APT’s key ring or file. The Offensive Security organization had lost access to their old repository signing key (ID ED444FF07D8D0BF6) so initiated and published a new key (ID ED65462EC8D5E4C5) for older Kali versions (Arun, 2025).
 - To fix this issue, the updated key file package was downloaded and installed using the GPG method, placing the key file directly into the directory. The system was successfully updated as seen below.

 - The commands: *sudo wget* with the url of the keyring file from the source, along with *-o* command indicating the file path to where the file should be downloaded and stored.  
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/5efb002473dd8d3e230322077a4169812cb378f9/images/suricata-download-keyfile.png"/>
Task 1.2: Image 2

- The *sha1sum* command was used along with the file and hash to check the integrity of the file ensuring nothing was altered.
- Then the *gpn --no-default-keyring -keyring* command was used with the file path and *-K* option to let the system know to bypass the default key file, use the one newly stored, and listing the public keys in the file.
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/a1bfcb429fb482469d90a8bcd4faf81402598f6d/images/FileHashIntegrity.png">
Task 1.3: Image 3

- The system was now updated.
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/70ff62cdae88128e1bf7712738436c78e673ad03/images/system%20updated1.2.png">
Task 1.4: Image 4

### 2. Intall Suricata
- Suricata was installed using command: *sudo apt install suricata -y*, then starting suricata service with commands: *sudo systemctl start suricata sudo *.
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/89a5fa7f36a9791f2fb9f9a5f0793294f9bc8ad9/images/suricata%20installed.png">
Task 2.1: Image 5

- Suricata was started and the status was actively running using commands: *systemctl status suricata*.
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/89a5fa7f36a9791f2fb9f9a5f0793294f9bc8ad9/images/suricataStaus.png">
Task 2.2: Image 6

### 3. Determined IP address, then edit the /etc/suricata/suricata.yaml file and add the IP address as Home_Net.
- Determine the IP address using *ifconfig eth0* command.
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/0a3794b299f77c94863f7baa238ea7929106cc32/images/IPaddressOfSystem.png">
Task 3.1: Image 7

- Edit file with command: *nano /etc/suricata/suricata.yaml*, then scroll down to the address groups and add the IP address as Home_Net commenting out the other address.
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/0a3794b299f77c94863f7baa238ea7929106cc32/images/alteringYamlFile.png">
Task 3.2: Image 8

### 4.  Create a *local.rules* file to  /etc/suricata/suricata.yaml file.
- The /etc/suricata/suricata.yaml file, the /var/lib/suricata/rules/local.rules file, and the /etc/suricata/rules file were edited to add a rule file (local.rules) to log alerts of any attempt to access Facebook website.
- The local.rules file were created in these file by scrolling or searching for rule-files location and added/typing in the local.rules file.  
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/0a3794b299f77c94863f7baa238ea7929106cc32/images/etcSuricataRules%20file.png">
Task 4.1: Image 9

### 5. Add the test rule into the "local.rules" file.
- Rule was added to the local.rules file with command: *nano /var/lib/suricata/rules/local.rules*, and the rule added *"drop dns any any -> any any (msg:"DNS Facebook"; content:"facebook"; 
classtype:policy-violation; sid:39398144; rev:1;)"*
- Suricata was updated based on the new rule using commands: *sudo suricata-update*.
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/caea3d54a0542e30c9a14f3f2d0560b02a18dd18/images/facebook%20rule.png">
Task 5.1: Image 10

### 6. Suricata was tested with the new rule
- Suricata was tested using command: *suricata -T -S /etc/suricata/rules/local.rules*, and the rule working.
<img src="https://github.com/Shan-light/Intrusion-Detection-and-Prevention-Lab/blob/7a9d99ec285bab1fafcb42998a0bca95c58f0635/images/ruleTested%26updated.png">
Task 6.1: Image 11

### 7. Facebook website was tested.
- Facebook.com was tested using the "curl" command to test the output from the website.
- 
