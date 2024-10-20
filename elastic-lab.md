# Developing a Dashboard & Visualization via Elastic

## Overview

Through HTB's VM, security events and incidents were pre-programmed into the Elastic interface. It was my assignment to complete four tasks/visualizations.

## Documentation

Task one was to assemble a visualization consisting of failed login attempts from all users. 

First, I filtered the visualization to only include events with the event code of 4625, which is the Windows event code for when a user fails to login.

![image](https://github.com/user-attachments/assets/3208b5a9-90f9-46f4-939f-86cd3e982dae)

Per the task, I also filtered out the specific usernames shown below:

![image](https://github.com/user-attachments/assets/322c9e00-c6c1-4fc2-8560-7506a2936afb)

I configured a table to be able to cleanly show the failed login data. The NOT user.name : *$ omits all system accounts from the search. The “Security” keyword ensures that all Security logs are accounted for and not any other unrelated system logs. I included the username, host system that the event was logged by, the logon type, and the number of times the user tried to login.

![image](https://github.com/user-attachments/assets/fd0e787c-04bf-4165-988b-7e6ff3f4978d)
<img width="468" alt="image" src="https://github.com/user-attachments/assets/58597e92-d60f-4c66-8ad3-8bd71fc35bbc">

My next step was to find the failed login attempts to disabled accounts. This is important because we don’t know if the attacker has the login info, as it is impossible to login to disabled accounts. I was able to use the ‘SubStatus’ filter and the code “0xc0000072” that indicates a disabled account. We only found one incident for this by the user ‘anni’.

![image](https://github.com/user-attachments/assets/db9a7055-e67e-48c3-903a-793a8f00cf48)

A side task was to filter the login attempts to admin accounts. I did this simply through the “user.name:*admin*” KQL query that filters all login attempts to an ‘admin’ account (or any account with ‘admin’ in it).

![image](https://github.com/user-attachments/assets/e6f3cf6d-b36d-4ece-af48-535c86c76e22)

My next task was to filter successful RDP logins. For this task, I had to filter a different event code, which was 4624 (successful Windows logins). I also had to filter the logon type to RemoteInteractive as that indicates an RDP. 

<img width="418" alt="image" src="https://github.com/user-attachments/assets/89c1f118-c4a4-4ded-8c6c-2a72419997ef">

I also changed up the table configuration to where we could see the IP that the user connected from. We can see that ‘svc-sql1’ connected from ‘192.168.28.130’ to the ‘PKI’ host twice.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/a809dc04-ee2f-44dd-8bd4-458be4581d78">

My last task was to record all events of administrative accounts being either added or removed from the server.

The event code 4732 indicates that a member has been added to a security-enabled local group. The event code 4733 indicated that a member has been removed from a security-enabled local group. So, I filtered for one of these two codes. Under the group name, I used ‘administrators’.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/d1e3bab2-06a5-4301-9a69-d1f0105dc304">

As you can see, this provided me with a dashboard of admin account activity, telling me when users were added or unadded from the administrators group. The second column is the SID token used during the process.  The fifth column tells us what host the user was added on.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/2dcc2b62-20ab-4da2-bcba-e9ce6efb1870">

Altogether, after the dashboard of SOC alerts looks like this: 

<img width="1431" alt="image" src="https://github.com/user-attachments/assets/bb6ca37c-a525-4ddd-a7dd-5d48b4554adb">


Done!











