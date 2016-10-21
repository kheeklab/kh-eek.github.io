---
published: true
title: enable Windows subsystem for Linux
layout: post
---
# Installation Guide

## Prerequisites

1. Your PC must be running a 64-bit version of Windows 10 Anniversary Update build 14393 or later


>To find your PC's CPU architecture and Windows version/build number, open Settings>System>About. Look for the OS Build and System Type fields.
<!--more-->

![system status](https://www.davijournal.com/images/system.png)

If your build is below 14393, try checking for updates.

### Installation

In order to run Bash on Windows, you will need to manually:

1. Turn-on Developer Mode
2. Enable the "Windows Subsystem for Linux (beta)" feature via the GUI or the command-line:

### Turn on Developer Mode

1. Open Settings -> Update and Security -> For developers
2. Select the Developer Mode radio button

![update & security](https://www.davijournal.com/images/updateandsecurity.png)

### Enable the Windows Subsystem for Linux feature (GUI)

1. From Start, search for "Turn Windows features on or off" (type 'turn')
2. Select Windows Subsystem for Linux (beta)

![windows feartures](https://www.davijournal.com/images/windowsfeatures.png)

3. Click OK

### Enable the Windows Subsystem for Linux feature (command-line)

Open a PowerShell prompt as administrator and run:

```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

### After enabling Windows Subsystem for Linux
#### Restart your computer when prompted

>It is important that you DO restart when prompted as some of the infrastructure which Bash on Windows requires can only be loaded during Windows' boot-up sequence.

### Run Bash on Windows

1. Open a command prompt
2. Run ```bash```

![bash shell install](https://www.davijournal.com/images/bashshellinstall.png) 

After you have accepted the License, the Ubuntu user-mode image will be downloaded and a "Bash on Ubuntu on Windows" shortcut will be added to your start menu.

To launch Bash on Windows, either run ```bash``` at a cmd/PowerShell command-prompt, or use the start menu shortcut.

After installation your Linux file system components will be located at: ```C:\Users\<Windows user name>\AppData\Local\lxss\``` This directory is marked as a system file which are hidden by default. **Accessing this location directly is not advised** due to caching between the Linux and Windows file systems. Check out [Microsoft blog post](https://blogs.msdn.microsoft.com/wsl/2016/06/15/wsl-file-system-support/) for more information.

> **Note:** The first time you install Bash on Windows, you will be prompted to create a UNIX username and password - this can be different from, and has no relationship to, your Windows username and password. More information on the UNIX username and password can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/user_support).

### Reference 

https://msdn.microsoft.com/en-us/commandline/wsl/install_guide
