# Running Redis on Linux in Windows 10 

## Windows Subsystem for Linux

Yes, you heard right. Starting with Windows 10 (v1709 - 2017-09, [Fall Creators Update](https://blogs.msdn.microsoft.com/commandline/2017/10/11/whats-new-in-wsl-in-windows-10-fall-creators-update/)), you can run at least a half-dozen flavors of Linux on the Windows Subsystem for Linux (WSL), and you can run Redis on top of that. No VM required. No Docker either.  Sure, you can [download the Redis-CLI](https://github.com/dmajkic/redis/downloads "redis-2.4.5-win32-win64.zip") and connect to [Redis Enterprise Cloud](https://redislabs.com/redis-enterprise/cloud/ "Redis database-as-a-service") running Redis-as-a-Service on [AWS, Azure, GCP, Pivotal Web Services or Heroku](https://redislabs.com/redis-enterprise/cloud/access/ "Redis Enterprise Cloud"). But ever since [Jessica Dean](https://twitter.com/jldeen "Jessica Dean on Twitter") explained how WSL works at the [SVDevOps Meetup](https://www.meetup.com/SVDevOps/events/235908130/ "Getting started with BASH on Windows 10"), I recommend Windows 10 users run Redis on their own dev machines.

## How do I know if I have Windows 10 or WSL?

Run "Winver" to see what version of Windows you're running. Starting with version 10, you've got a command called "wslconfig." It lists distros you have and controls which one starts when you type "bash." Try it out!

## How to set it up!

1. To enable Windows Subsystem for Linux, follow the instructions on [Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/install-win10#install-the-windows-subsystem-for-linux "Install the Windows Subsystem for LInux"). The short version is: Open PowerShell as Administrator and run this command to enable Windows Subsystem for Linux (WSL): 
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
2. Reboot Windows after making the change. Note you only need to do this one time. 

3. Download and install one of the supported Linux distros from the [Windows Store](http://microsoft.com/store "Windows Store").
- [Ubuntu 16.4](https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6) 
- [Ubuntu 18.4](https://www.microsoft.com/en-us/p/ubuntu-1804/9n9tngvndl3q)
- [Kali Linux](https://www.microsoft.com/en-us/p/kali-linux/9pkr34tncv07)
- [Debian GNU/Linux](https://www.microsoft.com/en-us/p/debian-gnu-linux/9msvkqc78pk6)

4. Launch installed Distro from the Windows Store and then install redis-server. For the purpose of demonstration, we are providing examples for Ubuntu, Debian, etc. (Note: You need to wait for initialization and create login at first time)
```
> sudo apt-get update 
> sudo apt-get upgrade
> sudo apt-get install redis-server
```
5. Optional: edit /etc/redis/redis.conf and change the line “bind 127.0.0.1” to “bind 0.0.0.0”
```
> sudo nano /etc/redis/redis.conf
> // change the line, then save and close the file
```
6. Restart the Redis server to make sure it is running:
```
> sudo service redis-server restart
```
7. Execute a simple Redis commend to verify your Redis server is running and available: 
```
> redis-cli 
127.0.0.1:6379> set user1 "Salvatore"
127.0.0.1:6379> get user1
"Salvatore"
```
8. To stop your Redis server: 
```
> sudo service redis-server stop
```
  
## Bonus: How does Ubuntu run within Windows?  

Instead of calling the Linux Kernel, the system calls (syscalls) that these un-modified Linux libraries use are re-directed over to Windows, which performs the work, instead of Linux. 

If you want to edit Windows files in Windows AND in Linux, then keep your files in /mnt/c/ so you can edit them with either OS. Don't use Windows to "reach into the Linux file system." As Scott Hanselman says on his [WSL blog post](https://www.hanselman.com/blog/VIDEOHowToRunLinuxAndBashOnWindows10AnniversaryUpdate.aspx "The year of Linux on the (Windows) Desktop - WSL Tips and Tricks"), "There be dragons!"



