# Logrotation-with-Logrotate
Setting up a log rotation (debian)
## Introduction of logrotate
logrotate is a utility in Linux designed to simplify the administration of log files on a system that generates a lot of log files. It works by periodically taking the current log files, renaming them, optionally compressing them, and generating a fresh file to which an application can continue sending its logs.

Here’s how it works:
 - Configuration: The basic configuration of logrotate is usually located at /etc/logrotate.conf, where you specify which log files to rotate, how often to rotate them, and what actions to perform during rotation.
 - Rotation: logrotate will periodically take the current log files, rename them, optionally compress them, and generate a fresh file to which an application can continue sending its logs.
 - Automation: The logrotate command is invoked automatically from cron, and most services have their own log rotation configuration that is implemented when they’re installed.
 - Customization: A system administrator can use the logrotate utility for their own needs as well. For example, if a Linux admin sets up a script to run, and has that script generating logs on a regular basis, it’s possible to set up logrotate to manage the log files.

By automating log rotation and compression, logrotate ensures your log files are kept in check, avoiding disk space overflow and maintaining a well-organized system. This prevents logs from filling up entire partitions and bringing systems to their knees in the process.


## Setting up logrotate

### Installation of logrotate

```
sudo apt-get update
sudo apt-get install logrotate
```

### Logrotate configuration
```
sudo nano /etc/logrotate.d/mylog
```
Copy and paste the configuration in the file.conf

This configuration will cause logrotate to rotate myfile.log when it reaches 1GB in size (size 1G). It will keep the last 4 copies of the log file (rotate 4), compress the log file copies except the last one (compress and delaycompress), silently ignore missing log files (missingok), and create new log files with permissions specified if the log file is deleted (create 0640 root adm).

### Testing the logrotate configuration
```
sudo logrotate --debug /etc/logrotate.d/mylog
```
This command will run logrotate in debug mode, meaning it will show you exactly what it would do, but without actually performing the actions.

Remember, logrotate is normally run as a daily cron job, so changes you make to the configuration won't take effect until the next day. If you want to force logrotate to run immediately, you can do so with the following command:
```
sudo logrotate -f /etc/logrotate.conf
```
### Execute logrotate 
```
sudo logrotate -f /etc/logrotate.conf (force the rotation)
sudo logrotate /etc/logrotate.conf (apply rotation if max size reached)
```


### Custom crontab
If you want setting a custom crontab:
```
crontab -3
```
Insert
```
* * * * * /usr/sbin/logrotate /etc/logrotate.conf
```
By default logrotate run once a day


# Author
<b>Xiao Li Savio Feng</b>
