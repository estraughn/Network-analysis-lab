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
-  Malware Bazaar


## Steps
1. First I opened a terminal and navigated to the directory that contained the sample PCAP file that contained network traffic from a host infected with the lockbit malware. I then ran the tcpdump -tt -r 2021-09-14.pcap command to display the PCAP file with tcpdump and identified an area of unusually high http traffic between the ip address 10.0.0[.]168 and 103.232.55[.]148. I then refined my search to specifically display traffic from port 80 and the IP address 10.0.0[.]168 with GET and POST request. I then noticed that one of the GET request contained a .exe file called .audiodg.exe, I then took the destination ip address to domaintools.com to evaluate it using OSINT. I then perfomred a search in the PCAP file for specific packets containing the audiodg.exe by utilizng the following command: tcpdump -tt -r 2021-09-14.pcap -A | grep "audiodg.exe" -A 500 | less. Once inside the packet I noticed a an encoded URL within the header of the packet, I then copied this URL and headed to Cyberchef to begin decoding the URL. Then I took the decoded URL over to Virus Total to confirm if this is in fact a known malicious URL. After this I took note of all identified IOC for further analysis and reporting.

*Ref 1.1:![Screenshot 2025-01-27 104923](https://github.com/user-attachments/assets/65d0e70f-16f7-4610-a0c7-26f5ab9f958c)

*Ref 1.2:![Screenshot 2025-01-27 105401](https://github.com/user-attachments/assets/f31eb6db-9eab-464b-881a-f00faa7b0ca6)

*Ref 1.3:![Screenshot 2025-01-27 114333](https://github.com/user-attachments/assets/f5d89b80-e87f-4e76-9c8c-f9454bcd8bb0)

*Ref 1.4:![Screenshot 2025-01-27 115208](https://github.com/user-attachments/assets/71f87afc-afb3-4721-b8ba-390e0a9d0e8a)

*Ref 1.5:![Screenshot 2025-01-27 120113](https://github.com/user-attachments/assets/f00b3281-6d8f-4979-b2f5-5878e3810e2e)

*Ref 1.6:![Screenshot 2025-01-27 121635](https://github.com/user-attachments/assets/07833eb8-2dca-4230-8f3b-6eea2048403f) ![Screenshot 2025-01-27 121814](https://github.com/user-attachments/assets/a8f5e42e-ea09-43f3-aa16-94b3cd44fde5)

*Ref 1.7:![Screenshot 2025-01-27 122216](https://github.com/user-attachments/assets/275a9f3a-43f9-4e56-8465-08d303b5be1e)

2. Next I loaded the PCAP file into Wire Shark for a deeper packet analysis. First I utilized the statistics feature to take note of the highest amount of traffic between the host endpoint and the malicious ip address. I then found the packet that contained the malicious executable and followed the HTTP stream. I then took note of the response from the server which started with MZ and stated "this program cannot me run in DOS mode" indicating the end user downloaded an executable file from the server. I then exported the malicious file .audiodg.exe to my desktop and obtained the SHA256 hash so I could run it through the Malware Bazaar database and find out more about this specific malware.  

*Ref 2.1:![Screenshot 2025-01-27 175005](https://github.com/user-attachments/assets/96cf605d-ab45-42ff-bdbe-3b664259bf64)

*Ref 2.2:![Screenshot 2025-01-27 175735](https://github.com/user-attachments/assets/01e883a7-866f-4423-a390-9ef5a3d02bb0)

*Ref 2.3:![Screenshot 2025-01-27 183645](https://github.com/user-attachments/assets/dc6fce12-1836-4cb9-a352-f1dc4b572f6f)

*Ref 2.4:![Screenshot 2025-01-27 184002](https://github.com/user-attachments/assets/40e35b30-2e62-489b-a4e7-ae145b67b56e)

*Ref 2.5:![Screenshot 2025-01-27 184204](https://github.com/user-attachments/assets/777d1b04-7d48-459f-a34d-0c0dff49a183)

3. Now that the analysis is done it is time to implement new IDS/IPS rules to help mitigate future network intrusions, so here I will be creating a sample rule within snort. First I navigated to the etc/snort/rules/local.rules directory and utlized the nano command to create a new snort rule. I then tested out the new rule by utilizing the hping command from another terminal window and observed the response via snort.

*Ref 3.1:![Screenshot 2025-01-28 151954](https://github.com/user-attachments/assets/d1681c30-0d67-4eb0-90e8-0708b1eb7096)

*Ref 3.2:![Screenshot 2025-01-28 152944](https://github.com/user-attachments/assets/638dd767-3936-4558-9c77-fa4e1abcbfca)

*Ref 3.3:![Screenshot 2025-01-28 152825](https://github.com/user-attachments/assets/1a8f90eb-4d35-47c8-865c-a21a8d39c930)






