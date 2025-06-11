[[7-Managing Linux Process]]
[[0-History of Linux]]
#Linux #Linux_Concepts #FileSystem_Linux 

#### FHS and Dependency more in Linux And Probelms
>[!tip]+  FHS and Dependency more in Linux And
> - when develop Software on Linux it depend that there is Dependency must be installed before and that is make load on User or Administrator of Linux  so this Create Problem named **Dependency Hell**
***Package Group*** => that Contains Different Packages but in one Package Group that has one thing Share it like in desktop there is  Network Manager , disk Manager all of these installed in one bundle named Package Group

>[!note]+ Example for Package Management 
>- Package Types
>- **RPM** => in Fedora, REDHAT,AWS LINUX
>- **DEB** => UBuntu , Linux Mint , POPOS
>-  ZIPP=> SUS
>- APK => Aupine
>- -------
>- Package Management (UTILS, Command)
>- IUM /DNE => RPM
>- DPKG => DEB 
>- ZIPPER => ZIPP
>- APK => APK

Naming Convention of Packages 
RPM 
 `<package_name>-<version_num>-<release_num><distribution>.<arch>.rpm`   

>[!tip]+ ## Packages Command
>Command `dpkg`
>```bash
>sudo dpkg -i nsnake_3.0.1-2build4_amd64.deb
># to install Package on System by the PackageManager
>sudo dpkg -r nsnake
>dpkg -l 
># to show all package with important details
>dpkg -p [packageName] like Bash
># to get More Details about Specific Package installed on System
>dpkg -I nsnake_3.0.1-2build4_amd64.deb 
># get Details for Downloaded Packages that  not installed on System
>dpkg -L nsnake 
># to show all files  of installed Package
>dpkg -S 
># the Oppisite of -L command 
>```
> - #### `wget`
>  ```bash
>  wget (http://ge.archive.ubuntu.com/ubuntu/pool/universe/n/nsnake/nsnake_3.0.1-2build4_amd64.deb)
>  # Download Packages 
> ```


>[!faq]+  What is The Difference Between `wget` and `sudo apt`

>[!tip]+ `apt` Utils
>- ##### Before `apt`
>	-  to install Package in the old way using `dpkg`
>	must first download it then search for package then install all of this manual so here the Savior come to Automate it `apt`
>-------
>- ##### so what is apt ? 
>	- its Utils that Automate all this in one command that
>	- search for package and Downloads then install it in one Command and 
>	- also get the Packages based on Distro Type and architecture and version
>	- also install Dependency and sub Dependency so it solve Dependency Hell
>	```bash
>	sudo apt install nsnake
>	sudo apt update 
>	# it check for All installed Packages version from its repo # and it mark it as up-gradable to be upgrade using upgrade
>	sudo apt upgrade 
>	# after using apt update to mark all Packages Needed to update Now Upgrade install the new version but it dont delete the unneeded Dependency after update
>	sudo apt full-upgrade  
>	# it like upgrade but it also delete unneeded Dependency after update
>	```
> - ##### so how apt work?
> 	- it work by search on links of Resource in file `/etc/apt/source.list` 
> 	that have all resources that he should search for it to provide packages like searching in archive.Ubuntu.com
> 	![[Screenshot from 2025-06-10 20-34-39.png]]
> 	and Can modify this file to specific what is sources searching in it
> 	so we make search on `source.list` to get all uncommented links
> 	```bash
> 	cat /etc/apt/source.list | grep -v ^# 
> 	# to search for All available Sources links only
> 	cat /etc/apt/source.list | grep  ^#
> 	# to search for all Commented links only 
> 	```
> 	-  ###### Even apt has Update ;) 
> 		`apt` make basics command like install and update 
> 		but for more option and low level control use `apt-get` like if has Package that is not Verified use apt-get with options that is skip validate Packages Source 

>[!note]+ grep
>```bash
>grep -v ^T 
># -v it return for the oppisite of condition like in here it Search for all files that dont start with T 
># ^T means that T in first char 
>```

>[!note]+ ###### Universal Package Management
>- its installer that is installed by default on Most Distro not Related for Specific Distro or Architecture
>- install Packages Cross Distro that work on Several Distro
>- ####### Example 
>	- ######## Snap Store Managed b
>		-Managed by Canonical Same Company of Ubuntu 
>		- installed by default on Ubuntu Distro and has daemon (Service) on Background
>		 There is Snap Store GUI or  CLI
>		 ```bash
>		 sudo apt install snapd # if not installed by default
>		 sudo snap install snap-store # to install GUI
>		 sudo snap refresh # to update Snap Programs 
>		 ```
>	- ######## flatpak Store
>		- https://falthub.org
>	- ######## AppImage
>		- https://appimage.github.io
>		- Encapsulate All things Related to Application into one file
>		- its the nearest form to windows `1 file 1 Application`
>		- its not Require Dependency as all thing in one file
>		- no need to Follow FHS of linux 
