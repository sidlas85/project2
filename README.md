I worked on a Red Team vs. Blue Team scenario in which I played the role of both pentester and SOC analyst.

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

IP Address: 192.168.1.105 Please note that this VM is in the network solely for the purpose of testing alerts.

## Day 1 Activity File: Red Team

### Monitoring Setup Instructions

- As the you attack a web server today, it will send all of the attack info to an ELK server.

- The following setup commands need to be run on the **Capstone** machine before the attack takes place in order to make sure the server is collecting logs.

- Be sure to complete these steps before starting the attack instructions.

**Instructions**

- Double click on the 'HyperV Manager' Icon on the Desktop to open the HyperV Manager.

- Choose the `Capstone` machine from the list of Virtual Machines and double-click it to get a terminal window.

- Login to the machine using the credentials: `vagrant:tnargav`

- Switch to the root user with `sudo su`

#### Setup Filebeat

Run the following commands:
- `filebeat modules enable apache`
- `filebeat setup`

The output should look like this
![image](https://user-images.githubusercontent.com/101371476/165664933-be770da9-89ea-456c-8591-4cb6b6b3b322.png)


#### Setup Metricbeat

Run the following commands:
- `metricbeat modules enable apache`
- `metricbeat setup`

The output should look like this:

![image](https://user-images.githubusercontent.com/101371476/165665145-60a96a5b-b177-4838-9445-4db71a1e7729.png)


#### Setup Packetbeat

Run the following command:
- `packetbeat setup`

The output should look like this:

![image](https://user-images.githubusercontent.com/101371476/165665255-1e7327ea-5370-462f-8b6b-81f53fee13ff.png)


Restart all 3 services. Run the following commands:
- `systemctl restart filebeat`
- `systemctl restart metricbeat`
- `systemctl restart packetbeat`

These restart commands should not give any output:

![image](https://user-images.githubusercontent.com/101371476/165665392-71ba00b4-8222-4828-a682-66f9583d37df.png)


Once all three of these have been enabled, close the terminal window for this machine and proceed with your attack.

---

### Attack!

Today, you will act as an offensive security Red Team to exploit a vulnerable Capstone VM.

You will need to use the following tools, in no particular order:
- Firefox
- Hydra
- Nmap
- John the Ripper
- Metasploit
- curl
- MSVenom

### Setup

Your entire attack will take place using the `Kali Linux` Machine.

- Inside the HyperV Manager, double-click on the `Kali` machine to bring up the VM login window.

- Login with the credentials: `root:toor`

### Instructions

Complete the following to find the flag:

- Discover the IP address of the Linux web server.
- 192.168.1.105
- Locate the hidden directory on the web server.
-  - **Hint**: Use a browser to see which web pages will load, and/or use a tool like `dirb` to find URLs on the target site.
- ![pj1](https://user-images.githubusercontent.com/101371476/165666418-6a919f6e-dc84-450b-a744-9d59ea832c8a.PNG)
- http://192.168.1,105/company_folders/secret_folder
- Brute force the password for the hidden directory using the hydra command:
    - **Hint**: You may need to use `gunzip` to unzip `rockyou.txt.gz` before running Hydra.
    - **Hint**: `hydra -l <username> -P <wordlist> -s <port> -f -vV <victim.server.ip.address> http-get <path/to/secret/directory>
    - `
    `hydra -l ashton -P /usr/share/wordlists/rockyou.txt -s 80 -f -vV 192.168.1.105 http-get /company_folders/secret_folder`
<img width="271" alt="p2 attack (2)" src="https://user-images.githubusercontent.com/101371476/165668111-afd0c602-84a7-4609-814c-04111c49e276.PNG">
![front red 5](https://user-images.githubusercontent.com/101371476/165815861-49220d78-ff6c-4aeb-b551-b74e9ca15681.PNG)

- Break the hashed password with the Crack Station website or John the Ripper.
- linux4u
- Connect to the server via WebDav.
    - **Hint**: Look for WebDAV connection instructions in the file located in the secret directory. Note that these instructions may have an old IP Address in them, so you will need to use the IP address you have discovered.
    - <img width="696" alt="password b4 hash" src="https://user-images.githubusercontent.com/101371476/165816938-3691d8c8-d6fa-4754-9ee3-663026f00796.PNG">
![front red 7](https://user-images.githubusercontent.com/101371476/165817187-5d5347e2-0694-4905-a040-e6037bfc0364.PNG)

- Upload a PHP reverse shell payload.
    - **Hint**: Try using your scripting skills! MSVenom may also be helpful.
    - ![front red 10](https://user-images.githubusercontent.com/101371476/165817412-0fa8d618-fedb-4541-8e11-fca24c510969.PNG)

- Execute payload that you uploaded to the site to open up a meterpreter session.
- Find and capture the flag.
- <img width="625" alt="pj 9" src="https://user-images.githubusercontent.com/101371476/165818212-d71e9985-458d-477e-81c5-d715a60cc592.PNG">


After you have captured the flag, show it to your instructor.

Be sure to save important files (e.g., scan results) and take screenshots as you work through the assessment. You'll use them again when creating your presentation.

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.


## Day 2 Activity File: Incident Analysis with Kibana


Today, you will use Kibana to analyze logs taken during the Red Team attack. As you analyze, you will use the data to develop ideas for new alerts that can improve your monitoring.

**Important**: Any time you use data in a dashboard to justify an answer, take a screenshot. You'll need these screenshots when you develop your presentation on Day 3 of this project.

:warning: **Heads Up**: To complete today's part of the project, you must complete steps 1-6 from the last class. Finding the flag isn't critical, but you want to get past the point of uploading the reverse shell script.

### Instructions

Even though you already know what you did to exploit the target, analyzing the logs is still valuable. It will teach you:
- What your attack looks like from a defender's perspective.

- How stealthy or detectable your tactics are.

- Which kinds of alarms and alerts SOC and IR professionals can set to spot attacks like yours while they occur, rather than after.



#### Adding Kibana Log Data

To start viewing logs in Kibana, we will need to import our filebeat, metricbeat and packetbeat data.

Double-click the Google Chrome icon on the Windows host's desktop to launch Kibana. If it doesn't load as the default page, navigate to http://192.168.1.105:5601.

This will open 4 tabs automatically, but for now, we only want to use the first tab.

Click on the `Explore My Own` link to get started.

##### Adding Appache logs
Click on `Add Log Data`
![image](https://user-images.githubusercontent.com/101371476/165818809-a9d7aeea-9ece-40c2-a5e6-2efd5226f37f.png)


Click on `Apache logs` 

![image](https://user-images.githubusercontent.com/101371476/165818917-3cdea9d3-2848-4b15-a33f-b865c43bba05.png)


Scroll to the bottom of the page. 
Click on `Check Data`
You should see a message highlighted in green: `Data successfully received from this module`

![image](https://user-images.githubusercontent.com/101371476/165819040-fdff769f-879f-4a04-9a90-a91fedf93b41.png)


Return to the Home screen by moving back 2 pages.

##### Adding System Logs
Click on `Add Log Data`


![image](https://user-images.githubusercontent.com/101371476/165819236-3dc84e58-c35a-41bd-8b2f-ca8de1b32b58.png)



Click on `System logs` 

![image](https://user-images.githubusercontent.com/101371476/165819315-bb7b63da-ac0b-4df3-a44d-20c9ffe40464.png)


Scroll to the bottom of the page. 
Click on `Check Data`
You should see a message highlighted in green: `Data successfully received from this module`

![image](https://user-images.githubusercontent.com/101371476/165819421-75309ad7-5737-404f-8598-e53a28ffe061.png)


Return to the Home screen by moving back 2 pages.

#### Adding Apache Metrics
Click on `Add Metric Data`

![image](https://user-images.githubusercontent.com/101371476/165819595-9533a0a7-218b-4e77-b9e2-0dcfba291838.png)


Click on `Apache Metrics` 

![image](https://user-images.githubusercontent.com/101371476/165819668-e0f23009-3f88-4803-83b8-c70af1beda0f.png)


Scroll to the bottom of the page. 
Click on `Check Data`
You should see a message highlighted in green: `Data successfully received from this module`

![image](https://user-images.githubusercontent.com/101371476/165819747-54c2d624-20c8-486f-9ea5-397cc4796a04.png)


Return to the Home screen by moving back 2 pages.

#### Adding System Metrics
Click on `Add Metric Data`

![image](https://user-images.githubusercontent.com/101371476/165819881-a8697563-c727-4fa6-8ed7-1cc61591f097.png)


Click on `System Metrics` 

![image](https://user-images.githubusercontent.com/101371476/165819980-d4d1de40-12a1-48dc-8a9c-97e22ee21eb9.png)


Scroll to the bottom of the page. 
Click on `Check Data`
You should see a message highlighted in green: `Data successfully received from this module`

![image](https://user-images.githubusercontent.com/101371476/165820093-d60a8cca-d7c1-400e-8a81-2601c8f15621.png)


Close Google Chrome and all of it's tabs. Double click on Chrome to re-open it.

#### Dashboard Creation

Create a Kibana dashboard using the pre-built visualizations. On the left navigation panel, click on **Dashboards**.

Click on **Create dashboard** in the upper right hand side. 

![image](https://user-images.githubusercontent.com/101371476/165820210-85303afd-33b8-4ebf-9215-0c826ee348f2.png)


On the new page click on **Add an existing** to add the following existing reports:

- `HTTP status codes for the top queries [Packetbeat] ECS`
- `Top 10 HTTP requests [Packetbeat] ECS`
- `Network Traffic Between Hosts [Packetbeat Flows] ECS`
- `Top Hosts Creating Traffic [Packetbeat Flows] ECS`
- `Connections over time [Packetbeat Flows] ECS`
- `HTTP error codes [Packetbeat] ECS`
- `Errors vs successful transactions [Packetbeat] ECS`
- `HTTP Transactions [Packetbeat] ECS`

**Example for adding the first report:**

![image](https://user-images.githubusercontent.com/101371476/165820343-1e1fb467-27bc-4c3a-b2f6-c0dea6f86cb0.png)


![image](https://user-images.githubusercontent.com/101371476/165820433-c601dae1-b6d4-4b60-8340-4335bae862a6.png)


The remaining steps will be a process of self-discovery to be completed without screen shot examples.

Get familiar with running search queries in the `Discover` screen with Packetbeat. This will be located on your fourth tab in Chrome. 

- On the Discover page, locate the search field.
- Start typing `source` and notice the suggestions that come up.
- Search for the `source.ip` of your attacking machine.
- Use `AND` and `NOT` to further filter you search and look for communications between your attacking machine and the victim machine.
- Other things to look for: 
	- `url`
	- `status_code`
	- `error_code`

After creating your dashboard and becoming familiar with the search syntax, use these tools to answer the questions below:


1. Identify the offensive traffic.
   - Identify the traffic between your machine and the web machine:
   - Port Scan
   - <img width="953" alt="p2 blue 5" src="https://user-images.githubusercontent.com/101371476/165821650-90eaf51b-fad2-4282-9efb-33a78df84c4f.PNG">

     - When did the interaction occur?
     - ![image](https://user-images.githubusercontent.com/101371476/165821805-4d4016b6-112d-443f-bb05-36dc46ebf9ab.png)

     - What responses did the victim send back?
     - Ans: 200, 304, 400, 401, 404,
     - What data is concerning from the Blue Team perspective?
     - The amount of traffic is huge and during a short amount of time, indicating that an attack was conducted

2. Find the request for the hidden directory.
![blue new3](https://user-images.githubusercontent.com/101371476/165823133-d9e7c7c2-bc53-4733-89e5-a4f4c202ff0b.PNG)

   - In your attack, you found a secret folder. Let's look at that interaction between these two machines.
     - How many requests were made to this directory? At what time and from which IP address(es)?
     - 1 the folder was request 37,113
     - 2 04/27/2022 @ 17:51
     - 3 192.168.1.90 -< 192.168.1.105
     - Which files were requested? What information did they contain?
     - _doc
     - Ryan's password hash
     - What kind of alarm would you set to detect this behavior in the future?
     - To send an alert when any IP that is not whitelisted, tries to acess this directory
     - Identify at least one way to harden the vulnerable machine that would mitigate this attack.
     - removing the directory from the server
     -  rmdir -r

3. Identify the brute force attack.

   <img width="395" alt="blue new new" src="https://user-images.githubusercontent.com/101371476/165842992-c6a88b39-f2c6-4e41-a74c-b763aa31d78d.PNG">
   <img width="691" alt="blue new new 2" src="https://user-images.githubusercontent.com/101371476/165847694-15996de4-10c9-4ec4-84c7-1d2f87c28761.PNG">


   - After identifying the hidden directory, you used Hydra to brute-force the target server. Answer the following questions:
     - Can you identify packets specifically from Hydra?
     - find it in the above picture

     - How many requests were made in the brute-force attack?
     - 371,867
     - How many requests had the attacker made before discovering the correct password in this one?
     - it was little less than 10,200 only 3 successul
     - <img width="415" alt="blue attempt failed" src="https://user-images.githubusercontent.com/101371476/165851241-a2511b40-feaf-430f-b108-efe1fae1e708.PNG">

     - What kind of alarm would you set to detect this behavior in the future and at what threshold(s)?
     - I  will set an alarm to alert if this error code comes back a certain amount of times in a timeframe, such as 5 times within a 30 minute window.
     - Identify at least one way to harden the vulnerable machine that would mitigate this attack.
     - limit the amount of times a failed password can happen and block all IP addresses that are not approved for company use.

4. Find the WebDav connection.
   - Use your dashboard to answer the following questions:
     - How many requests were made to this directory? 
     - 20
     - Which file(s) were requested?
     - passwd.dav file was requested aslo shell.php
     - What kind of alarm would you set to detect such access in the future?
     - Alarms should be set for any IP that is not whitelisted and for any IP outside the server range.
     - Identify at least one way to harden the vulnerable machine that would mitigate this attack.
     - No one should be able to access this server from the web and only from whitelisted IPs

5. Identify the reverse shell and meterpreter traffic.
   - To finish off the attack, you uploaded a PHP reverse shell and started a meterpreter shell session. Answer the following questions:
   - <img width="832" alt="blue new5" src="https://user-

     - Can you identify traffic from the meterpreter session?
     - <img width="832" alt="blue new5" src="https://user-images.githubusercontent.com/101371476/165855331-b4eaabab-9b85-407d-bc38-fb1ec20a9de8.PNG">

     - What kinds of alarms would you set to detect this behavior in the future?
	flag any traffic where a .php file is uploaded
     - Identify at least one way to harden the vulnerable machine that would mitigate this attack.
	lock down outgoing connectivity to allow only specific remote IP addresses and ports for the required services.


---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
