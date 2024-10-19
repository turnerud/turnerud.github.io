# Network Enumeration Lab

## Documentation (in progress)

Lab Instructions:
A company hired us to test their IT security defenses, including their IDS and IPS systems. Our client wants to increase their IT security and will, therefore, make specific improvements to their IDS/IPS systems after each successful test. Our goal is to find out specific information from the given situations. The machine is protected by IDS/IPS systems. The idea is to do this quietly so the systems aren’t alerted.

First, the client wants to know if we can identify which OS their provided machine is running on.
I ran a very general nmap scan of the IP just to see what ports were open. After I did that, I specified a certain port and used -sV to find the details from that specific port (22). I could’ve probably just used -O in hindsight and that would’ve been a quieter way of doing it.

![image](https://github.com/user-attachments/assets/74201ecb-7e68-4260-b96f-86a1dfa97351)

After this first test, the administrators tightened up their IDS/IPS and firewall.

After the configurations are transferred to the system, our client wants to know if it is possible to find out our target’s DNS server version.

I remembered that DNS queries are made over UDP port 53 most of the time. I specified that port. I used -sU in order to run a UDP scan. Then I used -sV in order to get the full server version.

![image](https://github.com/user-attachments/assets/6588b110-ef3a-4350-ae13-499b239d28c2)

Our next task is to find the version of the running services, per our client. The admin again, tightened up the firewall and IDS/IPS rules.

*in progress*



