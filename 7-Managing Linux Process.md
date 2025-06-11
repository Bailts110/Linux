[[0-History of Linux]] [[6- File Permission]]
#Linux #Linux_Concepts #Linux 

### Process
>[!tip]+ Process0.
>All Process in Linux Start From one Process named `systV` if The distro is so old
>- if  so it `init` the next after `systV`
>- and the new version now is `systemd`
>- ------------
>- any Process running in Background by User or kernel or Process of System Named **Daemon**  its like Service in Windows like FTP , HTTP Services

>[!tip] Process Command
>`ps` show Snapshot not live of the Process running in this session 
>```bash
>pstree # very important Command show The tree of All Process
>ps => # show Process running in Terminal Session and for current user 
>ps -l # give More Details of Terminal Process like PPID
>ps -e # show All Process running on all System
>
 >```
 >---------
 >-To show Live Process Running use old command like `top`
 >or newer like`htop`
 >```bash
 >top # show Live Details of Running Process like Task Manager old Command
 >------
 >htop # Recommended Command use it task Manager 
 >----
 >sleep 10m # sleep for time 
 >
 >``` 
 >------
 >-------
 >- `kill` Command 
 >The Kill Command doesnt Kill Process it send Signal To Kernel then kernel send Interrupt Signal to Code Currently Running 
 >```bash
 >kill -SIGHUB PID
 ># it Restart Process with Same PID
 >kill - SIGINT PID
 ># Stop the Process like ctrl-C
 >kill -SIGTERM  PID
 ># kill Process Graceful mean If Process has Child Process it Ensure to kill Child Process First then kill Parent Process to Prevent Zombie Child Process 
 >kill -SIGKILL PID
 ># BruteForce Kill means Immediately
 >```
 >- every kill Type has Numeric Representation so you can type it instead of word 
 >	- SIGHUB => -1
 >	- SIGINT => -2
 >	- SIGTERM=> -15
 >	- SIGKILL => -9
 >---------
 >- `killall` is like `kill` but you pass to it name of process and it kill all Process with this name 
 >```bash
 >sleep 40
 >sleep 50 
 >killall -9 sleep # so it kill two running Sleep
 >```

#### Background and Jobs
>[!top]+ Jobs and Background daemon
>to take Advantage of MultiTasking in Linux we run Background Process with Command `&` after any Command like 
>```bash
>sleep 10 & # & tell that this Command execute in Background 
>jobs # show Background Process
>fg # to fetch background Job to Forground 
>``` 
>- `ctrl-Z`to Make Command running in Forground Running in Background like `sleep 100` then click `ctrl-Z` to run in background `fg` to fetch Background Job to run in Forground



>[!tip] Container and Ubuntu Process
>First Process run in Container is the First Process in Container like in ubuntu Container `bash` is the first Process Running in Container not `systemd` 
>and if run `ps -elf` you see two running process 
>so where is the kernel ?? The Container take it From host Kernel OS and all of the Running Process in Container is User Space  

>[!tip] SSH ./etc/init.d
>ssh installed by Default on ./etc/init.d
>![[Screenshot from 2025-06-10 04-40-56.png]]
>- to start SSH service on Background you have two ways 
>	- old way for Docker Container that dont have **systemd** or old Distro 
>		- ``./ssh start``
>	- The Second way tha normal t for Linux distro on VM or anything that have **systemd**
>		- that using `systemctl` that is Interface of **systemd** that enable to manage Service like Start , Stop , status ,enable
>		```bash
>		systemctl start ssh
>		systemctl status ssh
>		systemctl stop ssh
>		 ```
>	