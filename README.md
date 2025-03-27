# VulnServer for Beginners Buffer Overflow Python and Reverse Shell Exploitation
VulnServer is a great tool for beginners who want to learn how to find buffer overflow vulnerabilities and develop exploit scripts using Python. This guide will walk you through the basics of stack-based buffer overflow and show you how to create a reverse shell exploit step by step.

## **Setting Up The Environment**
- Start the VulnServer program on Windows.
- Attach it to **Immunity Debugger**.

![Immunity Debugger Screenshot](images/immunity_debugger.png)

## **Finding Buffer Overflow Vulnerabilities**
1. **Spiking** - Determine if the command is vulnerable to buffer overflow.
2. **Finding Offset** - Calculate the correct padding size.
3. **Finding Bad Characters** - Identify bad characters that terminate shellcode.

![Finding Offset](images/finding_offset.png)
