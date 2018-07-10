# Running Redis on Linux on Windows 10 

## Windows Subsystem for Linux

Yes, you heard right. Starting with Windows 10 (v1709 - 2017-09, Fall Creators Update), you can run at least a half-dozen flavors of Linux on the Windows Subsystem for Linux (WSL), and you can run Redis on top of that. No VM required. No Docker either.  Sure, you can download the Redis-CLI and connect to [Redis Enterprise Cloud](https://redislabs.com/redis-enterprise/cloud/ "Redis database-as-a-service") running Redis-as-a-Service on AWS, Azure, GCP, IBM Cloud, Pivotal Web Services or Heroku. I often encourage this for trying sample code. But since [Jessica Dean](https://twitter.com/jldeen "Jessica Dean on Twitter") explained how it works at [SVDevOps Meetup](https://www.meetup.com/SVDevOps/events/235908130/ "Getting started with BASH on Windows 10"), I recommend Windows 10 users run Redis on their own machines.

## How do I know if I have Windows 10

Run "Winver" to see what version of Windows you're running. Starting with version 10, you've got a command called "wslconfig." It lists distros you have and controls which one starts when you type "bash." Try it out!

## Here's how to set it up!

1. Enable Windows Subsystem for Linux
Follow the instructions on [Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10#install-the-windows-subsystem-for-linux "Install the Windows Subsystem for LInux"). The short version is: Open PowerShell as Administrator and run this command to enable Windows Subsystem for Linux (WSL): 
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
2. Reboot Windows, then install any of the Linux distros from the Windows Store at http://microsoft.com/store. For the purpose of these instructions, we will install Ubuntu:
- [Ubuntu](https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6) (~200 mb)
- [OpenSUSE](https://www.microsoft.com/store/apps/9njvjts82tjx)
- [SLES](https://www.microsoft.com/store/apps/9p32mwbh6cns)
- [Kali Linux](https://www.microsoft.com/en-us/p/kali-linux/9pkr34tncv07)
- [Debian GNU/Linux](https://www.microsoft.com/en-us/p/debian-gnu-linux/9msvkqc78pk6)

3. Launch Ubuntu to install the redis-server. Here is the example for Ubuntu: (note: you may need to create a new Login and Password)
```
> sudo apt-get update
> sudo apt-get install redis-server
```
4. Edit /etc/redis/redis.conf and change the line “bind 127.0.0.1” to “bind 0.0.0.0”
```
> sudo nano /etc/redis/redis.conf
```
5. Restart the Redis service:
```
> sudo service redis-server restart
```

6. Execute a simple Redis commend to verify your Redis-Server instance is running and available: 
```
> redis-cli 
127.0.0.1:6379> set user1 "Salvatore"
127.0.0.1:6379> get user1
"Salvatore"
```
## So how is Ubuntu able to run on Windows?  

Instead of calling the Linux Kernel, the system calls (syscalls) that these un-modified Linux libraries use are re-directed over to Windows. 

If you want to edit Windows files in Windows and in Linux,  keep your files in /mnt/c/ so you can edit them with either OS. Don't use Windows to "reach into the Linux file system." As Scott Hanselman says on his [WSL blog post](https://www.hanselman.com/blog/VIDEOHowToRunLinuxAndBashOnWindows10AnniversaryUpdate.aspx "The year of Linux on the (Windows) Desktop - WSL Tips and Tricks"), "There be dragons!"



