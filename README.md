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

#
With an active session now established between the two machines, the attacker machine can start exploring the target. This includes inspecting privileges, gathering system information, and identifying any security measures present on the host.

![File_execution](https://github.com/user-attachments/assets/78882b6f-7a36-4f8a-8040-b711e7e841ec)
![Proccessess](https://github.com/user-attachments/assets/bfdbf6b7-109f-4392-a763-835634d82b09)

#
Within the LimaCharlie SIEM on the host machine, we can monitor the attacker's telemetry data. This includes detecting the active payload and identifying the IP address it's connected to.
![Lima_Charlie](https://github.com/user-attachments/assets/a5b1eec1-1b34-4663-a672-bbf235e51bc6)
![Network_file](https://github.com/user-attachments/assets/d6a40c04-8abb-4e05-9e37-d80004b0318e)

#
LimaCharlie allows us to check the payload’s hash through VirusTotal; however, since this payload was newly created, the scan will return clean.
![hash](https://github.com/user-attachments/assets/c024cdc3-19f1-4c95-8a34-0e8101230064)

#
Next, we can simulate a credential theft attack by extracting LSASS memory from the attacker's machine. On LimaCharlie, we can monitor the sensors, analyze the telemetry, and create rules to detect this sensitive process activity.
![SensitiveData](https://github.com/user-attachments/assets/51fd5fb5-8192-4c70-a0d3-889ab3f7fe7f)

![D R Rules](https://github.com/user-attachments/assets/e7b74752-27d1-4e02-9d6a-67d3879b3af1)

#
Moving beyond detection, we can now use LimaCharlie to craft a rule that identifies and blocks attacks from the Sliver server. On the Ubuntu machine, we’ll simulate a ransomware attack by trying to delete volume shadow copies. Through LimaCharlie, we can observe this activity in the telemetry and then create a rule to prevent the attack entirely. Once the rule is active in our SIEM, any further attempts from the Ubuntu machine to execute this attack will be unsuccessful.
