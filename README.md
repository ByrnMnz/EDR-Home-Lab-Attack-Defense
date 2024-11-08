# EDR Home Lab: Attack Defense

## Project
This lab focuses on replicating a real-world cyberattack scenario with endpoint detection and response. Following Eric Capuano's online guide, I'll employ virtual machines to create both attacker and target environments. The attack machine will leverage the 'Sliver' C2 framework to infiltrate a Windows endpoint, which will be monitored by 'LimaCharlie' acting as the EDR solution.

Eric Capuano's Guide: https://blog.ecapuano.com/p/so-you-want-to-be-a-soc-analyst-intro?utm_campaign=post&utm_medium=web

## Setup
The initial step in this lab involves configuring both the attacker and target machines. The attacker machine will operate on Ubuntu Server, while the target machine will run Windows 11. To ensure the lab runs without issues, Microsoft Defender and certain other security settings on the Windows machine will need to be disabled. Sliver will be installed on the Ubuntu machine as the main attack tool, while LimaCharlie will be set up on the Windows machine as the EDR solution. LimaCharlie will have a sensor connected to the Windows endpoint and will be configured to import sysmon logs for monitoring.

## Windows 11 Machine configurations
![Win11_Protection_off](https://github.com/user-attachments/assets/e822f4ee-a4fe-479e-9a3b-06f66463337e)

![Registry](https://github.com/user-attachments/assets/f344f1ca-e628-4111-9009-6dbddb5e2bf7)

![Sensors](https://github.com/user-attachments/assets/c0caeb25-40f3-4d80-98eb-41c629020f43)

## Installing Ubuntu Server:
![Server_Maching](https://github.com/user-attachments/assets/0e4dba71-9438-4828-9e17-df0fe3d97f4d)

## Attacking & Defending
We’ll generate a payload in Sliver and deploy it onto the Windows host. 
Once the malware is executed on the target machine, we’ll establish a command-and-control session to interact with the endpoint via the command prompt.

#
![Sliver](https://github.com/user-attachments/assets/e57b9ef5-da44-413c-b173-c09420416ac1)

![Malware](https://github.com/user-attachments/assets/650f65ff-64b7-4826-9cdc-b2aeb85838bb)

![Session](https://github.com/user-attachments/assets/ed365d2e-c8f8-4fc5-9c51-dcd5bf18ae4f)
