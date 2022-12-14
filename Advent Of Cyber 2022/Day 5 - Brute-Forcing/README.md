![day5](https://user-images.githubusercontent.com/84150540/207712513-127e3ad9-4846-41a8-854d-a2b5e075f39b.png)
# The Story - He knows when you're awake
McSkidy asked Elf Recon McRed to search for any backdoor that the Bandit Yeti APT might have installed. If any such backdoor is found, we would learn that the bad guys might be using it to access systems on Santa’s network.  

Today’s task will discuss a few standard services and authentication. We will also learn to hack an authentication service using Hydra and VNC clients.

## Learning Objectives
-   Learn about common remote access services.
-   Recognize a listening VNC port in a port scan.
-   Use a tool to find the VNC server’s password.
-   Connect to the VNC server using a VNC client.

## Remote Access Services
**SSH** stands for **Secure Shell**. It was initially used in Unix-like systems for remote login. It provides the user with a command-line interface (CLI) that can be used to execute commands.

**RDP** stands for **Remote Desktop Protocol**; it is also known as Remote Desktop Connection (RDC) or simply Remote Desktop (RD). It provides a graphical user interface (GUI) to access an MS Windows system. When using Remote Desktop, the user can see their desktop and use the keyboard and mouse as if sitting at the computer.

**VNC** stands for **Virtual Network Computing**. It provides access to a graphical interface which allows the user to view the desktop and (optionally) control the mouse and keyboard. VNC is available for any system with a graphical interface, including MS Windows, Linux, and even macOS, Android and Raspberry Pi.

## Authentication
Authentication refers to the process where a system validates your identity. The process starts with the user claiming a specific unique identity, such as claiming to be the owner of a particular username. Furthermore, the user needs to prove their identity. This process is usually achieved by one, or more, of the following:

1. **Something you know** refers, in general, to something you can memorize, such as a password or a PIN (Personal Identification Number).
2. **Something you have** refers to something you own, hardware or software, such as a security token, a mobile phone, or a key file. The security token is a physical device that displays a number that changes periodically.
3. **Something you are** refers to biometric authentication, such as when using a fingerprint reader or a retina scan.

To learn more please refer to day 5 
## Tasks

### Task 1:  Use Hydra to find the VNC password of the target with IP address `MACHINE_IP`. What is the password?

Lets start off with a nmap SYN scan:
```bash
sudo nmap -sS MACHINE_IP
```
The terminal below shows we have 2 open ports **SSH** on port 22  and **VNC** on port 5900
![nmap](https://user-images.githubusercontent.com/84150540/207712234-454c51d7-0e9d-4150-8c11-3b2665bc3583.png)

Now that we've confirmed we have a VNC server up we can try and brute-force a password we can do this with hydra using the following command:
```bash
hydra -P /usr/share/wordlists/rockyou.txt vnc://10.10.100.47 
```
Since the host doesn't have any username for the VNC service  we dont add the -l switch. When we look at the results we find our password: ```1q2w3e4r```

![password VNC](https://user-images.githubusercontent.com/84150540/207712189-7284fd06-c995-48a1-9979-4b9f4ac022b8.png)


### Task 2:  Using a VNC client on the AttackBox, connect to the target of IP address `MACHINE_IP`. What is the flag written on the target’s screen?
In the terminal we write remmina and connect to the VNC share with the found password we find the final flag
![final flag](https://user-images.githubusercontent.com/84150540/207712423-08b9ef2b-8796-40c9-a918-d130ea5128d2.png)
