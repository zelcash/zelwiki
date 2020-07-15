# Deterministic Zelnode and Zelflux Install Guide
**_Note: All test runs of this install script have only been done on VPS platforms and most likely will not work on personal home servers. USE AT OWN RISK._**

This guide will be using the install script on Vultr's VPS platform
## Requirements
* Collateral (10K Basic/ 25K Super/ 100K BAMF) [Exchange List](https://www.coingecko.com/en/coins/zelcash#markets)
* Control wallet and will recommend to use [Zelcore](https://zel.network/project/zelcore/download.html)
* SSH client such as [MobaXterm](https://mobaxterm.mobatek.net/download.html) or [Putty](https://www.putty.org/)
* VPS that meets the required specs for the tier
  * BAMF | 8vCore | 32GB RAM | 600GB SSD | 6TB total monthly bandwidth @ 100mbps+
  * Super | 4vCore | 8GB RAM | 150GB SSD | 4TB total monthly bandwidth @ 100mbps+
  * Basic | 2vCore | 4GB RAM | 50GB SSD | 2.5TB total monthly bandwidth @ 100mbps+
## Setting up Control Wallet
**1. Login to your Zelcore account and set automatic log out to never.**

![Screenshot_1](https://user-images.githubusercontent.com/47246006/75715564-76fcbc00-5c82-11ea-9311-7ca22a586ca8.png)
##
**2. Select Zel from your portfolio, click on the 3 dots in top right corner to see options, and start full node.**

![Screenshot_3](https://user-images.githubusercontent.com/47246006/75739057-b8a85980-5cb8-11ea-8557-e32e3b191339.png)
##
**3. If you don't have a Sapling address create one first and backup your private keys. To create a Sapling address click on Receive and then New Sapling Address. Now click on Tools, Wallet Management, then Import/Export. Click to choose path on Export option and export to a location of your choice. Save this offline somewhere safe. Also backup the wallet.dat file which you could find in your appdata roaming folder(Windows), library app folder(Mac), or .zelcash(Linux).**

![Screenshot_4](https://user-images.githubusercontent.com/47246006/75717570-34d57980-5c86-11ea-8d32-152f82b24e50.png)
![Screenshot_5](https://user-images.githubusercontent.com/47246006/75717580-39019700-5c86-11ea-9ca1-127f968d9c93.png)
##
**4. Click on Receiving Address and copy one of your transparent address you want to send your collateral to. Send the exact amount of Zel for your Zelnode collateral to the transparent address you just copied all in one transaction no more no less. Keep in mind with this upgrade to deterministic Zelnodes you now how to wait 100 confirmations(3.5 hours) before starting your Zelnode. So before moving on to the next step go do something and kill some time.**
## 
**5. Now time to setup the Zelnode on the VPS. Whether you use Vultr, Digital Ocean, or Hetzner make sure you select the right server with the hardware specs you need for the Zelnode you are trying to setup. You will fail to get the Zelnode on the network if you try on a server that doesn't meet the requirements. Following images are from Vultr and for a Basic Zelnode.**
  * **Deploy new server**
  * **Select a location**
  * **Choose Ubuntu 18.04 as your OS(recommended)**
  * **Name your server, and deploy**

**Will not go into how to use SSH keys but will recommend for you to look it up. Once server is ready click on it to get server info.**

![Screenshot_9](https://user-images.githubusercontent.com/47246006/75767686-0bedcc80-5cf8-11ea-89a1-5086fca8a08d.png)
![Screenshot_10](https://user-images.githubusercontent.com/47246006/75767676-0abc9f80-5cf8-11ea-8fef-340ab10ad1c7.png)
![Screenshot_11](https://user-images.githubusercontent.com/47246006/75768580-794e2d00-5cf9-11ea-8721-0fde5055bf89.png)
![Screenshot_12](https://user-images.githubusercontent.com/47246006/75767682-0b553600-5cf8-11ea-95a6-96b0fe191173.png)
![Screenshot_13](https://user-images.githubusercontent.com/47246006/75767684-0bedcc80-5cf8-11ea-8932-95e10fe510a2.png)
![Screenshot_1](https://user-images.githubusercontent.com/47246006/75769639-63416c00-5cfb-11ea-91eb-473bdcf996a7.png)
## 

**5. To access your server open up your SSH client and add your IP address. Will be using MobaXterm for this guide.**
  * **Click Session**
  * **SSH as your session type**
  * **Your VPS IP address in Remote Host and give it a name under Bookmark Settings**

![Screenshot_6](https://user-images.githubusercontent.com/47246006/75771775-7d7d4900-5cff-11ea-8703-59c800635665.png)
![Screenshot_7](https://user-images.githubusercontent.com/47246006/75771777-7e15df80-5cff-11ea-86b7-9d9435fb63bc.png)
![Screenshot_8](https://user-images.githubusercontent.com/47246006/75771780-7e15df80-5cff-11ea-9bf9-45c5e472b6d7.png)
##
**6. Login as root, copy password you got from your VPS provider, and right click and paste. You won't see password being typed out but it's there so hit enter after pasting. Create a user, add user to the sudo group, install docker from their apt repo, add user to the docker group, and reboot. List of commands to do all this.**
  * **adduser USERNAME** _Change USERNAME to name of your choice and replace USERNAME with one you chose in following commands._
  * **adduser USERNAME sudo**
  * **sudo apt-get update**
  * **sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common -y**
  * **curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -**
  * **sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"**
  * **sudo apt-get update**
  * **sudo apt-get install docker-ce docker-ce-cli containerd.io -y**
  * **adduser USERNAME docker**
  * **reboot**

_*Note you will be prompted to add user info after you create a password. Just leave them blank and hit enter it is not required._

![Screenshot_10](https://user-images.githubusercontent.com/41762330/78404707-d0bf1180-75b3-11ea-9c16-73ae538b379a.png)
![Screenshot_11](https://user-images.githubusercontent.com/41762330/78403968-49bd6980-75b2-11ea-8b40-a005d90259c5.png)
##
**7. Back to your full node on Zelcore. In the Zelnodes section which is in the bottom right select the Zelnode Wizard to start your Zelnode configuration. You will be prompted to backup keys but since you did it earlier you could just select skip.** 
  * **Select the tier** 
  * **Add your VPS IP address in front of the port(Ctrl+v to paste)** 
  * **Select the available output**
  * **Give the Zelnode an alias**

![Screenshot_1](https://user-images.githubusercontent.com/47246006/75741303-0d4ed300-5cbf-11ea-9124-5171b7852974.png)
![Screenshot_1](https://user-images.githubusercontent.com/47246006/75775764-8114ce00-5d07-11ea-8da3-a82dfd41fd83.png)
![Screenshot_2](https://user-images.githubusercontent.com/47246006/75775762-807c3780-5d07-11ea-9d99-2e579a26e2bd.png)
![Screenshot_3](https://user-images.githubusercontent.com/47246006/75775763-8114ce00-5d07-11ea-9073-387d533eac27.png)
![Screenshot_4](https://user-images.githubusercontent.com/47246006/75775982-f08abd80-5d07-11ea-8f86-466847e8114c.png)
##
**8. Open up a text editor such as notepad and copy paste the Zelnode private key, transaction id, and the output index just as I have it in image below. This will make it easier to just copy and paste when you run the install script as it will prompt you for this info during the install. Save and continue. Assuming you have waited 100 confirms since making the collateral transaction click Activate my Zelnode if not click on the X and you could start it once you have the confirmations.**

![Screenshot_5](https://user-images.githubusercontent.com/47246006/75776706-57f53d00-5d09-11ea-8af7-288e58405099.png)
##
**9. Back on your SSH client log back in to your VPS but this time as the user you created. Do not login as root. Once logged in run the following command and install will begin**
> bash -i <(curl -s https://raw.githubusercontent.com/dk808/deterministic-zelnode-script/master/install.sh)
##
**10. Script will prompt you the list below.**
  * **Confirmation of SSH port you're using select yes unless you changed it**
  * **Confirmation of IP address of VPS script detected**
  * **To add swap space if none is detected**
  * **Zelnode Private Key**(this is first value you copied to the text editor)
  * **Zelnode Collateral TxID**(second value on text editor)
  * **Collateral TxID output index**(last value on the text editor)
  * **Ask if you want to bootstrap Mongodb db for zelcash and I highly recommend you select Yes**
  * **Your ZelID** _You could find this under Apps in your Zelcore wallet._

**_Note: Your ZelID is not your username but the set of values under the QR code as shown in the clip below._**

![zelid](https://user-images.githubusercontent.com/41762330/77859200-d506bb80-71bc-11ea-8367-eae48e9b0689.gif)

**_Note: If you selected to bootstrap Mongodb it could take awhile during the loop that refreshes every 30 sec. as not only are you waiting for chain to sync but also Mongodb to sync. When refresh loop first starts do not worry if you don't see a block number next to "Mongodb on block" as it takes a few min for Zelflux to start up in the background. Loop will stop on it's own once it's synced._**

![Screenshot_20](https://user-images.githubusercontent.com/41762330/79070078-1a7cbb80-7c88-11ea-92cb-201a35fa8fb6.png)
![Screenshot_21](https://user-images.githubusercontent.com/41762330/79070080-1a7cbb80-7c88-11ea-9ed3-e1a8b85e2463.png)

**At the end of the install it will give some tips on a few commands and IPaddress:port for you to enter as your url on Chrome to access Zelflux. Once the refresh loop ends at end of script start your Zelnode from Zelcore/Zelmate if you haven't already and wait about 5-10 min and enter `zelcash-cli getzelnodestatus` to check status of your Zelnode. You are now a Zelnode op. Any further support please join [Zel's Discord](https://discord.gg/xhdMgwc)**

![Screenshot_24](https://user-images.githubusercontent.com/41762330/79070182-ddfd8f80-7c88-11ea-9d52-72c605d8b5d3.png)

**Any donations are welcomed and appreciated. Thanks.**

CruxID: dk808@zel.crux

BTC: 18i3ba5wkG8XoYT3y8JP58yWwvMgEkHNHK

ZEL: t1RaebuW5iav8QBVwuZ7WCx5SCaYm2WH2Sk

ETH: 0x9ec5f94f680da4f0be8b6492020c84d60f99b5b7

LTC: LSvzrnPmpvNb4M9D9GHgMA3HA8ixQjigsT