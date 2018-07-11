# Running Redis on Linux in Windows 10 

## Windows Subsystem for Linux

Yes, you heard right. Starting with Windows 10 (v1709 - 2017-09, Fall Creators Update), you can run at least a half-dozen flavors of Linux on the Windows Subsystem for Linux (WSL), and you can run Redis on top of that. No VM required. No Docker either.  Sure, you can [download the Redis-CLI](https://github.com/dmajkic/redis/downloads "redis-2.4.5-win32-win64.zip") and connect to [Redis Enterprise Cloud](https://redislabs.com/redis-enterprise/cloud/ "Redis database-as-a-service") running Redis-as-a-Service on [AWS, Azure, GCP, Pivotal Web Services or Heroku](https://redislabs.com/redis-enterprise/cloud/access/ "Redis Enterprise Cloud"). I've recommended this in the past for trying simple Redis commands from a Windows machine. But ever since [Jessica Dean](https://twitter.com/jldeen "Jessica Dean on Twitter") explained how it works in her talk at the [SVDevOps Meetup](https://www.meetup.com/SVDevOps/events/235908130/ "Getting started with BASH on Windows 10"), I recommend Windows 10 users run Redis on their own machines.

## How do I know if I have Windows 10

Run "Winver" to see what version of Windows you're running. Starting with version 10, you've got a command called "wslconfig." It lists distros you have and controls which one starts when you type "bash." Try it out!

## Here's how to set it up!

1. To enable Windows Subsystem for Linux, follow the instructions on [Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10#install-the-windows-subsystem-for-linux "Install the Windows Subsystem for LInux"). The short version is: Open PowerShell as Administrator and run this command to enable Windows Subsystem for Linux (WSL): 
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
Reboot Windows after making the change. Note you only need to do this one time. 

2. Download and install one of the supported Linux distros from the [Windows Store](http://microsoft.com/store "Windows Store"). 
- [Ubuntu](https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6) (~200 mb)
- [Kali Linux](https://www.microsoft.com/en-us/p/kali-linux/9pkr34tncv07)
- [Debian GNU/Linux](https://www.microsoft.com/en-us/p/debian-gnu-linux/9msvkqc78pk6)
For the purpose of instructions, we installed Ubuntu.

3. Launch installed Distro from the Windows Store and then install redis-server. (note: you need to wait for initialization and create login at first time)
```
> sudo apt-get update 
> sudo apt-get upgrade
> sudo apt-get install redis-server
```
4. Optional: edit /etc/redis/redis.conf and change the line “bind 127.0.0.1” to “bind 0.0.0.0”
```
> sudo nano /etc/redis/redis.conf
> // change the line, then save and close the file
```
5. Run command to restart service to make sure Redis is running:
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
8. To stop Redis you need to back to running Distro and stop the service:
	> sudo service redis-server stop
  
## So how does Ubuntu run within Windows?  

Instead of calling the Linux Kernel, the system calls (syscalls) that these un-modified Linux libraries use are re-directed over to Windows, which performs the work, instead of Linux. 

If you want to edit Windows files in Windows AND in Linux, then keep your files in /mnt/c/ so you can edit them with either OS. Don't use Windows to "reach into the Linux file system." As Scott Hanselman says on his [WSL blog post](https://www.hanselman.com/blog/VIDEOHowToRunLinuxAndBashOnWindows10AnniversaryUpdate.aspx "The year of Linux on the (Windows) Desktop - WSL Tips and Tricks"), "There be dragons!"



