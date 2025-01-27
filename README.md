# Network analysis lab

## Objective
To analyze and secure network infrastructure by leveraging advanced cybersecurity tools and techniques, identifying vulnerabilities, detecting threats, and implementing measures to enhance network integrity, performance, and resilience.



### Skills Learned

- Utilize tools like Wireshark and tcpdump to monitor, capture, and analyze network traffic for anomalies and potential threats
-  Implement and managed intrusion detection, and prevention systems to safeguard network infrastructure
-  Performed deep packet inspection to uncover hidden threats, malware, or unauthorized data exfiltration
-  Develop and deploy secure network architectures that mitigate vulnerabilities and reduce attack surfaces
-  Identifyed, assessed, and responded to security incidents and potential breaches within a network



### Tools Used

- Wire Shark
-  tcpdump
-  Snort
-  Suricata
-  Domaintools
-  Cyberchef
-  Virus Total


## Steps
1. First I opened a terminal and navigated to the directory that contained the sample PCAP file that contained network traffic from a host infected with the lockbit malware. I then ran the tcpdump -tt -r 2021-09-14.pcap command to display the PCAP file with tcpdump and identified an area of unusually high http traffic between the ip address 10.0.0[.]168 and 103.232.55[.]148. I then refined my search to specifically display traffic from port 80 and the IP address 10.0.0[.]168 with GET and POST request. I then noticed that one of the GET request contained a .exe file called .audiodg.exe, I then took the destination ip address to domaintools.com to evaluate it using OSINT. I then perfomred a search in the PCAP file for specific packets containing the audiodg.exe by utilizng the following command: tcpdump -tt -r 2021-09-14.pcap -A | grep "audiodg.exe" -A 500 | less. Once inside the packet I noticed a an encoded URL within the header of the packet, I then copied this URL and headed to Cyberchef to begin decoding the URL. Then I took the decoded URL over to Virus Total to confirm if this is in fact a known malicious URL. After this I took note of all identified IOC for further analysis and reporting.

*Ref 1.1:![Screenshot 2025-01-27 104923](https://github.com/user-attachments/assets/65d0e70f-16f7-4610-a0c7-26f5ab9f958c)
*Ref 1.2:![Screenshot 2025-01-27 105401](https://github.com/user-attachments/assets/f31eb6db-9eab-464b-881a-f00faa7b0ca6)
*Ref 1.3:![Screenshot 2025-01-27 114333](https://github.com/user-attachments/assets/f5d89b80-e87f-4e76-9c8c-f9454bcd8bb0)
*Ref 1.4:![Screenshot 2025-01-27 115208](https://github.com/user-attachments/assets/71f87afc-afb3-4721-b8ba-390e0a9d0e8a)
*Ref 1.5:![Screenshot 2025-01-27 120113](https://github.com/user-attachments/assets/f00b3281-6d8f-4979-b2f5-5878e3810e2e)
*Ref 1.6:![Screenshot 2025-01-27 121635](https://github.com/user-attachments/assets/07833eb8-2dca-4230-8f3b-6eea2048403f) ![Screenshot 2025-01-27 121814](https://github.com/user-attachments/assets/a8f5e42e-ea09-43f3-aa16-94b3cd44fde5)
*Ref 1.7:![Screenshot 2025-01-27 122216](https://github.com/user-attachments/assets/275a9f3a-43f9-4e56-8465-08d303b5be1e)

2. 
