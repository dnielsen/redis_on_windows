# redis_on_windows

Running Redis on Linux on Windows 10

Yes, you heard right. You can run at least a half-dozen flavors of Linux on Windows 10, and you can run Redis on top of any of them. No VM required. No Docker either.  Sure, you can download the Redis-CLI and connect to Redis Cloud running Redis-as-a-Service on AWS, Azure, GCP, IBM Cloud, Pivotal Web Services or Heroku. I often encourage this for trying sample code. But now, for developers who use Windows 10, I mostly recommend running Redis on Linux on Windows 10. 

To get set up on Windows 10, open PowerShell as Administrator and run this command to enable the Windows Subsystem for Linux (WSL): 
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
Next, reboot Windows, then install Ubuntu (or any of the Linux distros) from the Windows Store at http://microsoft.com/store. Ubuntu is a 1.8GB download.
- Ubuntu (1.8GB download) - https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6?rtc=1
- OpenSUSE - https://www.microsoft.com/store/apps/9njvjts82tjx
- SLES - https://www.microsoft.com/store/apps/9p32mwbh6cns
- Kali Linux - https://www.microsoft.com/en-us/p/kali-linux/9pkr34tncv07
- Debian GNU/Linux - https://www.microsoft.com/en-us/p/debian-gnu-linux/9msvkqc78pk6

Next, use cmd.exe to install the redis-server:
```
> sudo apt-get install redis-server
```
Next, edit /etc/redis/redis.conf and change the line “bind 127.0.0.1” to “bind 0.0.0.0”

Restart the Redis service:
```
> sudo service redis-server restart
Execute a simple Redis commend to verify your Redis-Server instance is running and available: 
> redis-cli 
127.0.0.1:6379> set user1 "Salvatore"
127.0.0.1:6379> get user1
"Salvatore"
```
