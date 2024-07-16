# VM Machine Setting
<hr/>
### Monitor Server
IP  : 20.214.182.107

DNS : ymmonitor.koreacentral.cloudapp.azure.com

* Login with cupadmin & public_key

<hr/>
## First Login
* Change password

	<img src = "./images/vm/vm-01.png" width = "60%"></img>

* Sudo permission
	* `sudo nano /etc/sudoers`
	* Add `cupadmin ALL=NOPASSWD: ALL`

* Mount additional disk
	* `lsblk -o NAME,HCTL,SIZE,MOUNTPOINT |grep -i "sd"`

	<img src = "./images/vm/vm-02.png" width = "80%"></img>

* Write new partition
	* `sudo fdisk /dev/sdc`
	* `n` &rarr; `p` &rarr; `1` &rarr; `Enter` &rarr; `+256M` &rarr; `p`
	* Save with `w`

	<img src = "./images/vm/vm-03.png" width = "80%"></img>

* Format with ext4
	* `sudo mkfs.ext4 /dev/sdc`
	
	<img src = "./images/vm/vm-04.png" width = "80%"></img>
	
* Mount
	* `sudo mkdir /monitor`
	* `sudo mount /dev/sdc /monitor`
	* `sudo chown cupadmin:cupadmin /monitor`
	
	<img src = "./images/vm/vm-05.png" width = "80%"></img>
	
* Auto mount (After reboot)
	* Find `uuid`
		* `sudo blkid` 
		
	<img src = "./images/vm/vm-06.png" width = "100%"></img>

	* Edit `/etc/fstab`
	
	<img src = "./images/vm/vm-07.png" width = "100%"></img>
		
* Update packages
	* `sudo apt update`

* (option) Install emacs
	* `sudo apt install emacs`

* Timezone
	* `sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime`