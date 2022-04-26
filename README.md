I worked on a Red Team vs Blue Team scenario in our second project in which I played the role of both pentester and SOC analyst.

As the Red Team, I attacked a vulnerable VM within my environment, ultimately gaining root access to the machine. As Blue Team, I used Kibana to review logs taken during the Day 1 engagement. I used the logs to extract hard data and visualizations for my report.

Then, I interpreted my log data to suggest mitigation measures for each exploit that I successfully performed.

In this project, I applied knowledge of the following skills and tools:

Penetration testing with Kali Linux.
Log and incident analysis with Kibana.
System hardening and configuration.
Reporting, documentation, and communication.
Lab Environment

In this unit, I used the Red vs Blue lab environment located in Windows Azure Lab Services. Used the Hyper-V Manager to access the nested machines:

ELK machine credentials: The same ELK setup that I created in Project 1. It holds the Kibana dashboards.

Username:
Password:
IP Address: 192.168.1.100
Kali: A standard Kali Linux machine I used in the penetration test on Day 1.

Username:
Password:
IP Address: 192.168.1.90
Capstone: Filebeat and Metricbeat are installed and will forward logs to the ELK machine.

IP Address: 192.168.1.105 

Using the Dashboards I added the following reports:

HTTP status codes for the top queries [Packetbeat] ECS
Top 10 HTTP requests [Packetbeat] ECS
Network Traffic Between Hosts [Packetbeat Flows] ECS
Top Hosts Creating Traffic [Packetbeat Flows] ECS
Connections over time [Packetbeat Flows] ECS
HTTP error codes [Packetbeat] ECS
Errors vs successful transactions [Packetbeat] ECS
HTTP Transactions [Packetbeat] ECS
Using the search queries in the Discover screen with packetbeat I was tasked with the following:

Identify the offensive traffic.
Find the request for the hidden directory.
Identify the brute force attack.
Find the WebDAV connection.
Identify the reverse shell and meterpreter traffic.
