[[3- Linux Stream]]
[[0-History of Linux]]
#Linux #Shell #User_Linux

[[Drawing 2025-06-07 22.32.55.excalidraw]]


>[!mote] To access all Users in Linux (Root,Normal,System) use
>`cat /etc/passwd` and we see many sentense follow form 
>that :: `UserName:UID:PID:Comment:HomeDirectory:Shell if login User`
>like `basilts:x:1000:1000:Basilts:/home/basilts:/bin/bash`

### User Permission 

>[!tip]+ you Can go to Root with `sudo -i`
>and there is File is `sudoers` that has name of users that can make Permision as Root if using `sudo` before any command,,,,
> and to Edit file `sudoers` use `visudo`

#### Adding User
>[!tip]+ User Setting Command
>```bash
>useradd BSTS -c "Basilts Mosalam" -m -p  -s -g password  
># -c is the Comm 
># -m to make HomeDir to user 
># -p to make UnHashed Password To user
># -g create Primary Group for user !!! and if want to create Auto Primary Group of his Name dont type -g
># -s Change default to bash
> userdel BSTS -r  
> # to delete User and -r to delete all its related files ,HomeDir
>mkhomedir_helper BSTS # to add HomeDir to User that hasnt it
>passwd BSTS # to Change User Password + newPass will be Hashed
>su - BSTS  # to change user 
>usermod -l -aG g1 BSTS Ahmed # -l to change username of user 
># -aG to append Group to user as -G is to add group and -a to append
>```

#### Grouping User
>[!tip]+ User Setting Group Command
>```bash
>cat /etc/group # to Get all Group 
groups # to see all groups join in it
sudo groupadd group1 # to add Group
sudo groupdel group1 # Delete Group
>usermod -aG -rG g1 BSTS  
># -aG to append Group to user as -G is to add group and -a to append
># -rG to Remove Group From User
>usermod -g  g1 BSTS 
># To change Primary Group of User
>```
>when using `groups` you will see group named as userName and this because that linux by default make Primary group named as user and cant User exist without have Primary group

