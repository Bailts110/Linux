[[5- File Management]] [[0-History of Linux]]
#shell #FileSystem_Linux #Linux #User_Linux 

#### 1- File OwnerShip
The Owner of file or Dir who Create it by default his Primary Group is the Group of File 
[[4-Users]] for See more about User and Group 

>[!note]+ Groups Ownership file 
>when Change Primary Group of User all his Home Directory Files will change auto their Group Ownership to new Primary Group  

>[!tip]+ Change OwnerShip of File 
>Change Ownership of File To User or Group using  `chown`  
>----
>```bash
>sudo chown [UserName] [GroupName if want to change]  [fileName] 
>sudo chown BSTS:BSTS file1
>sudo chown BSTS file1 # to change Ownership of User only not group
>sudo chown  :group2   # to change Ownership of Group only not User
>-------
>sudo chgrp [groupName] [fileName] # change group of file 
>```

#### 2- Permission
	-read => r=4 
	-write => w=2
	-excute => x=1

>[!tip]+ Permission of user in File
>3 type of UserPermission
>- User(Owner) => r,w,x
>- Group Permission => rw,x
>- Other => r,w ,
-------------
----------
> [!tip]+ *Numeric Representation* 
> - Read(R) => 4
> - Write(w) =>2
> - Execute => 1
> So if User Has in File RW so 4+2=6
> - When Type `ls -l` it display
> ```bash
> -rw-r--r-- 1 Basil Bai
> ```
> - so first `-` Represent if is File or dir
> - second 3 `---` for File Permission for **Owner** like `-rw-` so it can Read and Write not Execute 
> - the Third 3 for **Group** Permission on file 
> - the last 3 for **Other** 

--------------------
----------------------------
>[!tip]+ change File Permission using `chmod`
>```bash
> chmod u=rwx,g=rx,o-r [fileName]
> chmod u+rwx, g+rwx,o-r file1
> chmod ug+rw file1
># u for User mode
># g for Group
># other
>```
>- you can Also change Permission of file using Numeric Number of Permission as we said --> r=4,w=3,x=1
>```bash
>chmod 744 file1 # it means chmod u+rwx g+ o+r
>chmod 645 file1 
># it means u+rw g+r o+rx
>```

>[!faq]+ in here we learn how to Change Permission of File For Owner or Group or User but **question Here Can I Change Permission of file for Specific User ???**

>[!tip] Change File Permission for Specific User Access Control list (ACL) by `setfacl`
>to See ACL of File use 
>```bash
>getfacl file1 # it Gets The full Access Control list
>```
>-----
>- `setfacl` To Set ACL to Specific User on file
>```bash
>setfacl -m u:basilts:rw  file1
># this Set Access Control For File for Specific User 
>
>```