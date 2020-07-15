# Deterministic Zelnode and Zelflux Manual Install Guide
This install guide will be using Ubuntu 18.04 as it is what is recommended by Zel's Team.

## Requirements
* Collateral (10K Basic/ 25K Super/ 100K BAMF) [Exchange List](https://www.coingecko.com/en/coins/zelcash#markets)
* Control wallet and will recommend to use [Zelcore](https://zel.network/project/zelcore/download.html)
* SSH client such as [MobaXterm](https://mobaxterm.mobatek.net/download.html) or [Putty](https://www.putty.org/)
* VPS that meets the required specs for the tier
  * BAMF | 8vCore | 32GB RAM | 600GB SSD | 6TB total monthly bandwidth @ 100mbps+
  * Super | 4vCore | 8GB RAM | 150GB SSD | 4TB total monthly bandwidth @ 100mbps+
  * Basic | 2vCore | 4GB RAM | 50GB SSD | 2.5TB total monthly bandwidth @ 100mbps+

## Install Zelcash and Zelbench
**1. Login as root, copy password you got from your VPS provider, and right click and paste. You won't see password being typed out but it's there so hit enter after pasting. Create a user, add user to the sudo group, install docker from their apt repo, add user to the docker group, and reboot. List of commands to do all this.**
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

_**Note: You will be prompted to add user info after you create a password. Just leave them blank and hit enter it is not required.**_

![initial](https://user-images.githubusercontent.com/41762330/78452503-62746080-7640-11ea-84fb-36da4feb86a3.gif)

**2.  Sign back in as the User you just created and update and upgrade packages and install required dependencies for zelcash.**
  * **sudo apt-get update && sudo apt-get upgrade -y**
  * **sudo apt-get install build-essential pkg-config libc6-dev m4 g++-multilib autoconf libtool ncurses-dev unzip git python python-zmq zlib1g-dev wget curl bsdmainutils automake -y**

![initial1](https://user-images.githubusercontent.com/41762330/78458638-d37b3e80-7667-11ea-9387-081095479c73.gif)

**3.  Create the Zelcash directory, Zelcash conf file, and bootstrap(optional but do recommend it for quick sync).**
  * **mkdir ~/.zelcash**
  * **touch ~/.zelcash/zelcash.conf**
  * **cat << EOF > ~/.zelcash/zelcash.conf**\
**rpcuser=USERNAME**\
**rpcpassword=PASSWORD**\
**rpcallowip=127.0.0.1**\
**rpcallowip=172.18.0.1**\
**rpcport=16124**\
**port=16125**\
**zelnode=1**\
**zelnodeprivkey=YOUR_ZELNODE_PK**\
**zelnodeoutpoint=YOUR_COLLATERAL_TXID**\
**zelnodeindex=TX_OUTPUT_INDEX**\
**server=1**\
**daemon=1**\
**txindex=1**\
**listen=1**\
**externalip=SERVER_IP_ADDR**\
**bind=SERVER_IP_ADDR**\
**addnode=explorer.zel.cash**\
**addnode=explorer2.zel.cash**\
**addnode=explorer.zel.zelcore.io**\
**addnode=blockbook.zel.network**\
**maxconnections=256**\
**EOF**

_**Note: Change rpcuser, rpcpassword, zelnodeprivkey, zelnodeoutpoint, zelnodeindex, externalip, and bind with your values. Best way to do this is copy this to a text editor such as notepad, replace values, then copy and paste it to the terminal.**_

**Optional Bootstrap to Sync Quick**
  * **wget https://www.dropbox.com/s/kyqe8ji3g1yetfx/zel-bootstrap.zip; unzip zel-bootstrap.zip -d ~/.zelcash; rm zel-bootstrap.zip** 

![initial2](https://user-images.githubusercontent.com/41762330/78462893-9a54c580-768b-11ea-9999-a502a11bd846.gif)

**4.  This guide will be using the Apt repo to install Zelcash and Zelbench since you have no choice but to use the Apt repo to install the Zelbench package. If you want to build Zelcash from source follow guide from [Zel's Gitbook](https://zel.gitbook.io/zelcurrency/installing-zel-daemon). After installing Zelcash and Zelbench execute the script to install the zkSNARK params.**
  * **echo 'deb https://apt.zel.cash/ all main' | sudo tee /etc/apt/sources.list.d/zelcash.list**
  * **gpg --keyserver keyserver.ubuntu.com --recv 4B69CA27A986265D**
  * **gpg --export 4B69CA27A986265D | sudo apt-key add -**
  * **sudo apt-get update**
  * **sudo apt install zelcash zelbench -y**
  * **bash zelcash-fetch-params.sh**

_**Note: If the first command failed to fetch the deb file try fetching it from Github using this line.\
echo 'deb https://zelcash.github.io/aptrepo/ all main' | sudo tee /etc/apt/sources.list.d/zelcash.list**_

![initial3](https://user-images.githubusercontent.com/41762330/78498810-5ef4de00-7701-11ea-9683-465726e44243.gif)

## Install Zelflux
**1.  Install Mongodb and Nodejs as it is required for Zelflux. Although there are few methods to installing Mongodb and Nodejs this guide will use the recommended method by most.**
  * **wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -**
  * **echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list**
  * **sudo apt-get update**
  * **sudo apt-get install mongodb-org -y**
  * **sudo service mongod start**
  * **sudo systemctl enable mongod**
  * **curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash**
  * **source ~/.profile**
  * **nvm install 12.16.1**

_**Note: Mongodb install is using a package for Ubuntu 18.04 so if you are using a different os go to [Mongodb's doc's](https://docs.mongodb.com/manual/administration/install-on-linux/) and use deb package for your os.**_

![initial4](https://user-images.githubusercontent.com/41762330/78499857-1856b200-7708-11ea-92e4-8ad3ec0bf0d8.gif)

**2.  Start Zelcash, clone Zelflux repo, install Zelflux, and have Zelflux run using a background service such as screen/tmux. This guide will use Pm2.**
  * **zelcashd >/dev/null 2>&1**
  * **git clone https://github.com/zelcash/zelflux.git**
  * **touch ~/zelflux/config/userconfig.js**
  * **cat << EOF > ~/zelflux/config/userconfig.js**\
**module.exports = {** <br />
**&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;initial: {** <br />
**&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;ipaddress: 'SERVER_IP_ADDRESS',** <br />
**&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;zelid: 'YOUR_ZELID',** <br />
**&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;testnet: false** <br />
**&#8199;&#8199;&#8199;&#8199;&#8199;&#8199;}** <br />
**&#8199;&#8199;&#8199;&#8199;}** <br />
**EOF** <br />

 _**Note: Change SERVER_IP_ADDRESS and YOUR_ZELID to your values. Just as you did in Step 3 of installing Zelcash copy this over to a text editor, replace values, then paste it to the terminal.**_

  * **npm i -g pm2**
  * **pm2 startup systemd -u $(whoami)**
  * **sudo env PATH=$PATH:/home/$(whoami)/.nvm/versions/node/v12.16.1/bin pm2 startup systemd -u $(whoami) --hp /home/$(whoami) > /dev/null**
  * **pm2 start ~/zelflux/start.sh --name zelflux**
  * **pm2 save**

![initial5](https://user-images.githubusercontent.com/41762330/78522935-e84cf480-7783-11ea-9b20-80371e0ba608.gif)

**Installation is now complete. You can now start your Zelnode from Zelcore/Zelmate. Please note that only Mongodb and Zelflux will restart on system restarts and that you would need to create a service for Zelcash on your own. This guide was mainly created to install Zelnode and Zelflux without using the script.**


