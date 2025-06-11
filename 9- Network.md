[[8-Software Package Managment]] [[0-History of Linux]]
#Linux #Linux_network #SSH #Shell 

>[!tip]+ #### SSH (Secure Shell) Protocol
>- default port : 22 
>- it Follow Client Server Architecture 
>	- Sender has Client SSH 
>	- Receiver has Server SSH
>- ---
>- Packages to use it
>	- Putty =>  Windows To linux
>	- OpenSSH => Linux To Linux
>		- OpenSSH -server named opensshd
>		- OpenSSH -Client basilts  :0       :0               21:18   ?xdm?  46:54   0.00s /usr/li
>		- ssh-keygen => tools installed with OpenSSH
basilts  pts/1    ::1              23:25    0.00s  0.16s  0.01s w
=> installed by Default on Linux Distro 
>		- Connect to Server if has DNS or IP
>------------
>- ##### SSH Command  
>- First it Can Connect SSH Locally ```bash ssh basilts@localhost ```
>- if Connect To remote Server it maybe not recognize this server so it will give FingerPrint [[Fingerprint]] that for Secure and prevent Attack Name Man-in-the-Middle (MITM)
>- so when Connecting SSH with Server if the user of Client is Same as Server it will auto login as User of client to Server and Ask For Password
>- After Connecting To SSH-Server it will Store all Hosts Key and fingerprint in `./ssh/know_hosts file` so when Connect to it again it Will Compare FingerPrint that server Sent to Saved Fingerprint on `know_hosts` file Auto
>- `w` to see if the Login User
>-----------
>-----------
>- ##### Second Way To Connect
>- is With Connect To SSH-Server and Send Command to be Executed in It And return the Output on The Client Terminal 
> ```bash
> ssh basilts@localhost [Commadn that i want to send Once]
> ssh basilts@localhost pwd
> ssh basilts@localhost echo $0
>```
>---------
>---------
>- It can make Configuration to make Aliases To UserName And Password To Connect on SSH 
>```bash
>cd /.ssh 
>touch config # if not Created by Default
>nano config
># then add 
>aliasses to use in SSH like OracleLinux
>"
>Host OracleLinux
>  Hostname [ipAddress]
>  port 22
>  [UserName]
  " 
>ssh OracleLinux
># then it use The aliases to Connect To SSH 
>```
>

>[!note] SSH UserName And Password Over Network its Not the Secure way?
>- yes its not the Secure and dont using In Enterprise and they use Instead SSH with Key
>-##### what is SSH-keygen
>	-ssh key-gen is more Secure way to Connect with Server with SSH than send User Pass over Internet 
>	1.  it Follow Public /Private key As the User in Client Host Generate Public & Private key 
>	2. then Send Public key to Server then Server Encrypt Random Text with the Public key
>	3. then send the Encrypted text in Client Host User 
>	4. if User Decrypt the Text with The Private Key so The Connection is Established
>----
> - Command
>  ```bash
>  ssh-keygen 
>  # it creates Private and Public key in Folder /.ssh => id_rsa.pub & id_rsat
>  ssh-keygen -t [Algorthim of Crypto] like ed25519
>  # change the Crypto Algorthim like [dsa,ecdsa,ecdsa-sk,ed25519] 
>  ssh-agent 
>  # it saves all pass phrases in Memory and Automate sign in  with pass phrases to Read Private Key
>  ssh-copy-id -i id_rsa.pub [UserName @ IP of Server] like basilts@2.564.545.45
>  # instead of pass the Public Key by email to Server No You Can Use this Tools that get with openssh that is Pass Pub Key First time and Enter User and Password then it send the Key to Server to Save it then Go to Pub Key Authentication
> ```
> ----
> - ##### Configuration on SSH
> - to modify Configuration on SSH like Port or even if the SSH Connect with Key failed it give error not go to User Password Way 
> - So the File Config in `cd /etc/ssh/ssh_config` file `cd /etc/ssh then nano ssh_config`
> 	- then To Prevent User Pass Authentication `nano ssh_config` then search to `PasswordAuthentication` then make it no 
> 	- or even make Specific Groups Has User Pass Authentication and Group not => Linux Adminstrator
> -----------
> -----------

>[!tip]+ #### Transfer Files With SSH
> - Can Transfer Files with SSH with `scp` 
> - `scp` use SFTP over SSH and it Uses all SSH Authentication ways like pub private Key Authentication
> ```bash
> scp [fileName] [RemoteServer] :[path to save in RemoteServer]
> scp file1 OracleLinux:/home/basilts
>scp -r 
># -r options It transfer Recursively all Files under Directory
> ```
> ------------
> - `rsync` also as scp it uses SSH to Transfer Files with Addition Features like Synchronization with Directory and another Directory that When There is File on Host Client and on Server what is it will do and Transfer Directory
> -------
> - `wget`
> - Download Files From Links
>  ```bash
>  wget [link]
>  wget -i [file]
>  # -i Take File of Links then Downloads All Links  
>  wget -c ftp://sunsite.doc.ic.ac.uk/ls-lR.Z
>  # Continue getting a partially-downloaded file.
>  wget -O
>  # -O to Rename The Downloadable file 
> ```
> ---------
> - `curl` => Client URL 
> - Not Installed by Default on Most Linux Distro
> - Used for Interact with Websites and Internet Protocols like HTTP, FTP, ...etc
> - make REST API Calls
> ```bash
> sudo apt install curl -y
> curl parrot.live
> ```
> ----------------
> ##### Web Browsing on Terminal 
> - `w3m`
> ```bash
>  sudo apt install w3m
>  w3m www.google.com
> ```
> - **For advanced text-based features like tabs and better CSS parsing:** **ELinks** is a strong contender.
> - **For Browse modern, JavaScript-heavy websites in a terminal (especially remotely):** **Browsh** is unparalleled, but comes with the significant dependency of a full graphical browser engine.


>[!note] Shortcut of Files Location
>~/.local/share/applications



>[!faq] Topic To Research 
> - SSH and Graphical interface between Ssh-client and server transfer results and X11 package for Graphical Interface Xwindow in linux
> - make Current SSH as Tunnel for others Communication for Client Server
> - `scp` Command To Transfer Files with SFTP Over SSH