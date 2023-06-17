# Samba Installation and Configuration in Linux

objectives:

the installation steps necessary to use Samba

install samba from the package repository

```jsx
apt-get update && apt-get install samba samba-common
```

next is to create a directory we want to share

```jsx
mkdir -p /home/sambashare
```

make a backup of the smb.conf file

```jsx
cp -pf /etc/samba/smb.conf /etc/samba/smb.conf.bak
```

open the samba config file and add the following configuration

```jsx
vi /etc/samba/smb.conf

[sambashare]
	comment = Samba on kali linux
	path = /home/sambashare
	read only = no
	writeable = yes
	browsable = yes
	guest ok = yes
	force user = nobody
```

![Untitled](Samba%20Installation%20and%20Configuration%20in%20Linux%208e5a7e15b31e49389513f286ce91d76d/Untitled.png)

save file and give the share folder permissions

```jsx
chmod -R 775 /samba/sambashare/
chown -R nobody:nogroup /samba/sambashare/
```

restart the samba service

```jsx
service smbd restart
```

![Untitled](Samba%20Installation%20and%20Configuration%20in%20Linux%208e5a7e15b31e49389513f286ce91d76d/Untitled%201.png)

goto windows file manager and enter the ip address of the linux machine on the folder path of the windows file manager to connect to the file share \\<ip-address>

![Untitled](Samba%20Installation%20and%20Configuration%20in%20Linux%208e5a7e15b31e49389513f286ce91d76d/Untitled%202.png)

![Untitled](Samba%20Installation%20and%20Configuration%20in%20Linux%208e5a7e15b31e49389513f286ce91d76d/Untitled%203.png)

for a Secure Samba Folder;

first create a group and add user to the group to access the samba server

```jsx
addgroup smbgrp
useradd smbadmin -G smbgrp
```

![Untitled](Samba%20Installation%20and%20Configuration%20in%20Linux%208e5a7e15b31e49389513f286ce91d76d/Untitled%204.png)

next;

create a folder you want to secure and add the necessary permissions

```jsx
mkdir -p /home/sambashare/secured/
chmod 770 /home/sambashare/secured/
chown root:smbgrp /home/sambashare/secured/
```

![Untitled](Samba%20Installation%20and%20Configuration%20in%20Linux%208e5a7e15b31e49389513f286ce91d76d/Untitled%205.png)

edit the smb.conf file and add the following 

```jsx
[Secured]
	path = /home/sambashare/secured
	valid users = @smbgrp
	guest ok = no
	writeble = yes
	browsable = yes

```

![Untitled](Samba%20Installation%20and%20Configuration%20in%20Linux%208e5a7e15b31e49389513f286ce91d76d/Untitled%206.png)

save and restart the samba service

```jsx
service smbd restart
```

goto windows and access the secured folder

![Untitled](Samba%20Installation%20and%20Configuration%20in%20Linux%208e5a7e15b31e49389513f286ce91d76d/Untitled%207.png)

![Untitled](Samba%20Installation%20and%20Configuration%20in%20Linux%208e5a7e15b31e49389513f286ce91d76d/Untitled%208.png)

open the secured share folder

![Untitled](Samba%20Installation%20and%20Configuration%20in%20Linux%208e5a7e15b31e49389513f286ce91d76d/Untitled%209.png)

it now asks for credentials in other to access the folder.

thanks for your time.
