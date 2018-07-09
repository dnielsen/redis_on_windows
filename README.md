# Running Redis on Linux on Windows 10 

Windows Subsystem for Linux

Yes, you heard right. Starting with the Windows 10 (v1709 - 2017-09, Fall Creators Update), you can run at least a half-dozen flavors of Linux on the Windows Subsystem for Linux (WSL), and you can run Redis on top of anyone of those flavors. No VM required. No Docker either.  Sure, you can download the Redis-CLI and connect to Redis Enterprise Cloud running Redis-as-a-Service on AWS, Azure, GCP, IBM Cloud, Pivotal Web Services or Heroku. I often encourage this for trying sample code. But now, for developers who use Windows 10, I  recommend running Redis on Linux on Windows. So here's how it works!

1. Enable Windows Subsystem for Linux
Follow the instructions on the Microsoft Docs webstie (https://docs.microsoft.com/en-us/windows/wsl/install-win10). The short version is: Open PowerShell as Administrator and run this command to enable Windows Subsystem for Linux (WSL): 
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
2. Reboot Windows, then install any of the Linux distros from the Windows Store at http://microsoft.com/store. For the purpose of these instructions, we will install Ubuntu:
- Ubuntu - https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6 (~200 mb)
- OpenSUSE - https://www.microsoft.com/store/apps/9njvjts82tjx
- SLES - https://www.microsoft.com/store/apps/9p32mwbh6cns
- Kali Linux - https://www.microsoft.com/en-us/p/kali-linux/9pkr34tncv07
- Debian GNU/Linux - https://www.microsoft.com/en-us/p/debian-gnu-linux/9msvkqc78pk6

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
So how is Ubuntu able to run on Windows?  Instead of calling the Linux Kernel, the system calls (syscalls) that these un-modified Linux libraries use are re-directed over to Windows. 

If you want to edit Windows files in Windows and in Linux,  keep your files in /mnt/c/ so you can edit them with either OS. Don't use Windows to "reach into the Linux file system." That can lead you down a path you will likely regret. 

WSLCONFIG

Run "Winver" to see what version of Windows you're running), you've got a command called "wslconfig." Try it out. It lists distros you have and controls which one starts when you type "bash."


