# VulnServer for Beginners Buffer Overflow Python and Reverse Shell Exploitation
VulnServer is a great tool for beginners who want to learn how to find buffer overflow vulnerabilities and develop exploit scripts using Python. This guide will walk you through the basics of stack-based buffer overflow and show you how to create a reverse shell exploit step by step.


![Immunity Debugger Screenshot](Screenshots/1.png)


## What You Will Learn

In this documentation, you will learn how to:  

- Use spiking to identify the vulnerable command in the program  
- Find the correct offset to overwrite the EIP (Instruction Pointer)  
- Detect and eliminate bad characters that may interfere with shellcode execution  
- Use `mona.py` to locate modules with the necessary assembly instructions  
- Develop an exploit script to inject shellcode  
- Generate and execute a reverse TCP shell using `msfvenom`  

This guide is beginner-friendly and includes step-by-step explanations with Python scripting and reverse shell execution.  

## About VulnServer  

[VulnServer](https://github.com/stephenbradshaw/vulnserver) is a Windows-based multithreaded TCP server that listens for client connections on port **9999** (by default). It includes multiple commands, some of which are intentionally vulnerable to buffer overflow attacks.  

### Why Use VulnServer?  
- It is designed for learning **buffer overflow exploitation** in a controlled environment.  
- Each vulnerability requires a slightly different approach to exploit, helping improve your skills.  
- Though it mimics a basic server, it has no real-world functionality beyond being a **safe target for testing exploits**.  
- This tool is ideal for those wanting to **learn, test, and practice buffer overflow attacks** in a safe way. 🚀


## Setting Up the Environment  

Before we start analyzing **VulnServer**, we need to set up our environment.  

### Machines Used:  
- **Target Machine (Victim):** Windows 7 x86 Starter Edition (running VulnServer on port **9999**)  
- **Attacker Machine:** Kali Linux (used to find and exploit the vulnerability)  

### Steps:  
1. Run **VulnServer** on the **Windows machine** and make sure it is listening on port **9999**.  
2. Use the **Kali Linux machine** to test and exploit the vulnerability.  

![Immunity Debugger Screenshot](Screenshots/2.png)



## Connecting to VulnServer  
Now, switch to your **Kali Linux** (or any other preferred penetration testing OS) and try to connect to the **VulnServer** running on port **9999** using **Netcat**:  

```bash
nc -v 10.0.2.15 9999
```

![Netcat Screenshot](Screenshots/3.png) 




## Attaching VulnServer to Immunity Debugger  
Now, switch back to the **Windows machine** and attach the **VulnServer** program to **Immunity Debugger**. This will allow us to monitor the **registers** and **stack** while testing for vulnerabilities.

![Immunity Debugger Screenshot](Screenshots/4.png) 

![Immunity Debugger Screenshot](Screenshots/5.png) 

It should looks like this after we’ve successfully attached the process into Immunity Debugger.

![Immunity Debugger Screenshot](Screenshots/6.png)


## Finding Buffer Overflow Vulnerabilities  

Once the environment is set up, we can start identifying vulnerabilities in the **VulnServer** binary. The first step is to perform **spiking** on the available commands to check for potential buffer overflow issues.  

Typically, we create a **spiking template file** for each command to test them individually. However, in this guide, we will focus on testing the **TRUN** command.

![Immunity Debugger Screenshot](Screenshots/7.png)


### 1. Spiking (Checking for Buffer Overflow Vulnerability)  

The first step is to determine whether the **TRUN** command is vulnerable to a **buffer overflow**.  

To do this, we create a **spiking template file** for the **TRUN** command and save it as `trun.spk`.

![Immunity Debugger Screenshot](Screenshots/8.png)

### Breakdown of the Spiking Template Functions  

- `s_readline` : Reads the binary banner.  
- `s_string` : Places the string in each iteration of spiking.  
- `s_string_variable` : Appends the fuzzed string into the spike.  

Before starting the spiking process, run **Wireshark** to capture network packets for further analysis.
