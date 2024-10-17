# Active Directory Lab

## Documentation

Here are the tasks to accomplish in Active Directory:

![image](https://github.com/user-attachments/assets/593d3343-cd8a-4809-b2e5-09d0f9900246)

Our first task is to add the hires into AD. The lab instructed me to do three of them. We had to set their full name, email, display name, and make sure that they change the password at next logon. I did two of them through the terminal and the other through the GUI.

![image](https://github.com/user-attachments/assets/66fe5b55-c237-4bb5-ac95-eef66c20fd1d)

![image](https://github.com/user-attachments/assets/f21cd15c-5c82-4148-bb91-81030d32accf)
Added!

![image](https://github.com/user-attachments/assets/824b0905-10c6-41b3-8726-e1733fa7dea7)

Now we have to remove a couple users, Mike O’Hare and Paul Valencia.
![image](https://github.com/user-attachments/assets/7e60e28d-cfa1-41ab-97e6-46da1ad66e02)

Now, I have to unlock Adam Masters account because he can’t remember his password.
![image](https://github.com/user-attachments/assets/2d9d73e1-733f-45a4-9235-ea7aafa06cf0)

Next, we are tasked with creating a new Security Group called “Analysts” and adding our new hires into the group, under the IT hive. I was able to trace the OU and DC path through the “IT” hive’s properties.

![image](https://github.com/user-attachments/assets/fd39a01c-6aab-4667-b3b4-b823a3b40fc0)

We were able to successfully add the users to the group.
Now, I have to duplicate a group policy “Logon Banner”, rename it, and modify it for the Analysts OU.

![image](https://github.com/user-attachments/assets/8f68eba8-6f17-4813-8cbd-fbd9acf2be34)

In order to enforce the GPO I have to link it, and then modify it. I’m tasked with modifying Password policy settings for users in the group, allowing them to access PowerShell and CMD. In terms of computer settings, I need to ensure Logon Banner is applied and that removable media is blocked from access. To edit this, it was suggested I hop into Group Policy Management rather than try and modify it from Powershell.

![image](https://github.com/user-attachments/assets/95c1edf1-4409-4a3e-9dc0-543d3507e561)

Done, now we have to add a computer to our domain and change the OU that it resides in.

The host we need to join the INLANEFREIGHT domain is named: ACADEMY-IAD-W10. We have the credentials to the host. 
To add the computer to the domain from the localhost GUI, I had to hop into the control panel and manually edit the domain

![image](https://github.com/user-attachments/assets/1556df4b-565a-401c-9d5c-2482d1687dc9)

![image](https://github.com/user-attachments/assets/db202fc9-037e-4213-8741-7a8626551036)

Done!
