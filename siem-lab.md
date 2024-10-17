# SIEM Lab

## Overview

I created a SIEM emulation that I can run from my home. I configured a VM and utilized Microsoft Azure and Sentinel in order to detect network traffic and security incidents or vulnerabilities.

I documented the process below.

## Documentation

The resource group is the container for all of the things I’m going to be creating:

<img width="468" alt="image" src="https://github.com/user-attachments/assets/136c1197-7a8f-4e1f-bb6c-410fcf93c171">

I chose Windows 11 Pro as my operating system for this VM.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/ef42f840-5927-496c-949e-1f0aaa0bfb79">

I decided to leave this option allowed initially, in order to see the brute force attempts to RDP into my network.

I was able to deploy Microsoft Sentinel to my resource group. This will allow us to streamline our SIEM through their user interface.

<img width="346" alt="image" src="https://github.com/user-attachments/assets/0022840d-ab7c-493b-9251-84148e9b72f5">

Now, we can access this interface (which is empty for now): 

![image](https://github.com/user-attachments/assets/a6c260ee-d9f7-471b-9f5f-d4d537f49a3a)



Then, I installed Windows Security Events under the Data connectors tab in Sentinel, in order to be able to send the data and logs from my VM to the interface.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/a28c70ff-d702-4559-85b9-4fa69a499945">

It gives us two agents, as one of them is a legacy agent. I used the ‘Windows Security Events via AMA’ as that’s the one being supported and I didn't want to risk anything with the legacy agent.

Then, I configured the data collection rule in order to send the logs to Sentinel. 

<img width="468" alt="image" src="https://github.com/user-attachments/assets/37d141e7-3dc8-48a4-b6ce-af17db273b29">
<img width="468" alt="image" src="https://github.com/user-attachments/assets/c532575e-bc58-4f4f-8f66-2675eb9b105f">



This option wasn't preset, I had to manually check my VM to collect data from it. I enabled the option that allows it to capture all security events so our interface will be thorough.

<img width="343" alt="image" src="https://github.com/user-attachments/assets/61350aa1-2943-4586-a639-204581d70cc3">

I ran the ‘SecurityEvent’ query in order to see if there was any traffic. 
<img width="468" alt="image" src="https://github.com/user-attachments/assets/85769c19-1f3e-47f5-8ae7-5d5d09516158">


There is some traffic as you can see here. System accounts are signing in, so it is not particularly a worry. I implemented a new Sentinel rule that allows me to see if a user account is able to brute-force his or her way into my network.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/ed16412c-af91-4934-bb43-7d07a7db48c8">

If a non-system account is successfully able to access the network, it will notify me. Thankfully, there are no results found. We’re going to turn this into a rule that can notify me if someone accesses the network every five minutes.

This is the configuration for the Sentinel rule (quick note, I forgot to change the rule period, so I went ahead and changed that to 5 minutes): 
![image](https://github.com/user-attachments/assets/2b231818-85af-4129-8a02-8f3d463901a8)

After downloading the RDP file, I was able to connect to my VM to test the Sentinel alert.


As you can see here, Sentinel caught my RDP login. After seeing this incident, I was able to close it under this reasoning:

<img width="226" alt="image" src="https://github.com/user-attachments/assets/3b864b81-e15e-435d-ae62-d130d42ca5c8">

Although, the logic wasn't wrong. The rule did exactly what I wanted it to!

After a couple of days, I looked back at the logs to see just how many brute force attempts were logged from user accounts.

![image](https://github.com/user-attachments/assets/a1ded922-e63b-497f-9af7-2f0d5c80815c)

As you can see, there were attempts logged nearly every minute to RDP into my VM. I was able to trace some of these IPs to places like Dubai, Cambodia, Russia, etc. 

There were around 2400 attempts to access my open RDP port. All failed, but still a ton of attempts. Thankfully, no incidents.

Running a query to see the failed logins, it seems most of the hackers tried to login directly to my administrator account. Interestingly, some tried using general names to guess a username. 

![image](https://github.com/user-attachments/assets/4f43659a-4c99-4dc6-bd6d-d11aec4a6151)


