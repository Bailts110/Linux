#Linux #FileSystem_Linux #
[[4-Users]]
[[0-History of Linux]] 
[[2-Linux Command]]

>[!tip] Absolute path vs Relative Path
>- Absolute is begin from the begging to the current or selected path like `/home/basilts/Downloads/`
>- Relative Path is begin from the current path of execute Command or Shell Script like `./Downloads/`

#### File Management Command
```bash
sudo tree # display the entire Directory Content as Hierarecy with Human Readable way 
stat [file] # All Details of File
```

>[!info]+ File Structure in Linux
> Any file in Linux Consist of 
>	- File Name
>	- Data Block
>	- inode => Metadata of file

#### Link in linux
>[!tip] HardLink vs SoftLink
>- Hardlink => is making another **Independent** fileName with Same Metadata ,Inode. but Different in FileName 
>and use
>```bash
> ln [Original_fileName] [new hardlink_FileName]
> ln Original hardlink
> ```
>---------------------
>- Softlink or SymbolicLink => is making another Dependent File that Act as shortcut or Reference to the Original File and Has Different Metadata and Inode of the Original
>	```
>	ln -s Original Softlink
>	```

>[!faq]+ So what is Happend if We delete The Original File?
>- in hardlink => no thing happend and it act normal because it independent file 
>-  in softlink => it dont work and Shell gives warning that no thing softlink reference on it

>[!tip]+ Linux FileSystem Partioning vs Windows Partioning
> - in windows follow one=>one with virtual Disk Partition and Physical Disk to make it Simple to User like 
> ```bash
>  \:C\Programs # so in Here C is Separate Partition that assign to Physical Drive C and Programs is must be in physical Drive (C)
>  D:\Games # also Here D is Separate Partition that assign to Physical Drive D:\ and Folder Games must be in hard Disk D
>  ```  
>  - Linux Not Follow this Pattern or Strategy it Follow that Can Virtual FileSystem is Combination from Many Files Allocated in Different Physical Disks but its Important to make Linux Understand What this Path refers to in Physical Disk like 
> 	```
 /home/Basilts/Games
> 	 it can be (/) in Drive C --->
> 	 (home) in Drive D --->
> 	 (Basilts) in Drive C --->
> 	 (Games in Drive D)  

#### FileSystem Hierarchy Standard (FHS)

 >[!info] Standard Installed by Default with linux Distro inhertied from UNIX or get by IEEE &Linux Foundation
 so in this every Linux Distro Installed with it Default Hierarchy Directories and Files like /bin ,/etc . with Kernel 
 https://refspecs.linuxfoundation.org/FHS_3.0/index.html
 
 
 >[!faq]+ What If Linux Distro Want to Delete unwanted Dire or change it Locations ?
 > - To make it must Provide SymbolicLink or Softlink that refers To changed Directory or replace it with Deleted To Follow Standard of FHS
 > -  Why Follow this Standard ?
 > Because there is alot of Legacy Program that predict that these Directory location in Default that Follow Standard
 > and also any Programs Developed Now Will Follow The Standard 

>[!example]+ Example of FHS Dir that Installed with Kernel by Default
>- /etc => Contains Configuration Files like Configration of Users =>/etc/shadow , Groups /etc/groups ,/etc/sudoers,/etc/hosts
>------------
>- /home => User home Directories
>- ----------
>- /lib =>Essential Shared Liberaries and Kernel Modules
>- -------------
>- /media => mount Point for a Auto mounted media like CD,DVD
>- ------------
>- /root => Home Directories For the Root user
>- --------------
>- /srv => Data for Services Provided by this System its like Program Files in Windows Contains The Library of Specific App
>- ------------------
>- /temp => Temporary Files
>- -------------
>- /bin => for  Excutable File Application for  FileSystem and that not 
>- --------------
>- /proc => Interface of Kernel Space that have Process Details
>	- cpuinfo
>	- memoinfo 
>- ----------
>- /run => for Temp Storage for runtime
>- ------------
>- /dev => for Devices 
>- ----------------
>- /var => for Repeated changed Variable like log file
>- 

### File Command
```bash
File [fileName] # give Type of file 
File da.sh      # excutable File /bin/sh Script 
more [fileName] # Represent File Content with Good Scroll by Percnet of Content
less [fileName] # same as more but line by line 
```

>[!tip]+ in Here The very Important Command in FileSystem is Searching Files
> - we start it with `find` command that uses BruteForce Technique that Search file by file and dont Use Index To Search for File so yes Its very Slow 
>  ```bash
>  find [FolderSelected to Start Search] -type [Type of Search] -name file name
>  find /var -type f -name d*.log
>  ```

#### xargs or Argument in Linux
>[!tip] xargs
> - xargs refer to Argument in linux and useful to make Command on Output of group of file due to find or else and it uses more with Command `find`
> ```bash
> find . -name "*.txt" | xargs -I {} cp {} {}.bak
> # make copy of files result of search
> 
>  ```
>  - in here first it find all files with .txt then pass it to pipes to xargs as Argument ,,
>  - -----------
>  - ( -I ) means Replace String or Substitution that means any place you use ( {} ) will be replaced with the file you can think of it like Variable so you can exchange it with var or else but {} is Standard then other command that make Copy   
>  - --------------------------------
>  - -------------------------------
>  - another Example 
>  ```bash
>ls ff? | xargs -I {} mkdir {}.d 
># take the output and make Folder of it 
>  ```
>  ```bash
>  ls *.log | xargs -I {} sed -i '/debug/d' {}
>  # Take the Output and edit on files Forward without Temp
>  # and delete lines Contain debug
>  ```
> - in Here `sed` means Stream Editor that Edit or Process Text in Files Auto or with Pipes
> -  `-i` means in-place editing that mean `sed` will edit on files forward without making Temp Copy 
> - `"/debug"` this pattern that means any line Contains "debug"  
> - `d` in `"/debug/d"` Deleted Command in `sed`
>  ___________________
>  ________________

---------------------------

>[!tip] locate Command
>- `locate` is Powerful Command That Depend on DB Index of Files So its Faster than `find`
>- locate Maybe not installed by default on linux Distro
>but need update DB index to become on-date
> ```bash
> locate -r report.pdf  
> # now it Search on every where on System about file 
> # -r option for Regular Expression
> ```
>-------------------------
>```bash
>locate temp | xargs -I {} rm -v {} 
># delete all Files Contains with Name Temp like "temp.txt" or "temporary.log" and Represent it after delete
># -v that responsible to write name of Files after Delete 
>```
>--------------------
>-------------------
>```bash
>locate ' *.config' | grep ngnix | xargs -I {} cp {} /home/user/nginx-config/
># search for Files with exe .config then search for it for word ngnix then copy it to selected path
>```
>--------------------
>---------------------
>```bash
>locate '*.bak' | xargs -I {} rm -v {}
># delete all bakup file
>```
>```bash
>locate design | grep '.pdf$' | xargs -I {} xdg-open {}
># search for Files pdf with Name design then open it 
># xdg-open command that use to open a file or URL
>```
>

#Linux_Compression
#### Compression
>[!tip]+ `tar` Compression
>- in Linux You Can use `tar` Command to Make Collect All Folder Contnet Structure in one File or Also Make Compression that low the size 
>----------------
>```bash
>tar -cvf log.tar var/log/
># Compress Folder log 
># -c => Create archive 
># -f => option to ouput file Name to Compress 
># -v => give details of Compress Process like the Files that Compressed ,Error if exit
>```
>----------------
>----------------
>- uncompressed Files or Extract archive file  
>```bash
>tar -xvf log.tar -C /home/basilts
># -x => Extract the archive file 
># -C => the ouput path for output Files 
>--------------
>tar -tf log.tar
># to See the Contents of Compressed Files
>```
>----------------------
>--------------------
>- Compressed Size with `tar`
>- first Algorithm using `-z`  
> ```bash
> tar -cvzf log.tar.gz var/log/
> # -z Compress size option to .gz
>```
>- second Algorithm using `-j` and its take more longer than `-z` but make well Compression than it
> ``` bash 
> tar -cjvf log.tar.bz var/log/
>```
>

>[!tip]+ Compress The Size of File using `gzip` 
> - its Tool to Compress Size but it Compress on Same File that it dont make Copy Compressed no , if File named ben10 so it turn it into ben10.gz and the overwrite originalfile 
> - ----------
> ```bash 
> gzip /var/log/boot.log
> # it Compress Size of this file 
> gzip -k boot.log
> # -k prevent override on old file 
> gzip -d boot.log.gz
> to unCompress or Extract File 
> ``` 


>[!summary]

> [!warning]
> This is a warning callout. Be aware of the potential issues.

>[!quote]

>[!example] dad

>[!tldr] hjh

>[!todo]

>[!help]

>[!done]

>[!fail]

>[!danger]

>[!attention]

>[!bug]

>[!faq]

