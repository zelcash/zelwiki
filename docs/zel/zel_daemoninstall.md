This guide walks through the step-by-step process of building the Zel daemon/CLI from the open-source repository on Github <br><br>
[Zel Github](https://github.com/zelcash/zelcash)<br>

!!! info "Recommended System Specs:"
    2 or more CPU threads <br>
    64-bit Linux (Ubuntu 18.04)<br>
    4+ GB RAM<br>
    25+ GB Storage<br>

!!! warning
    If setting up a ZelNode, follow XXXX Guide<br>
    Running a standard p2p node does not reward ZEL

---

### Building for Linux

!!! info
    We officially support Ubuntu 18.04 LTS "Bionic Beaver". Source has been tested for most popular Ubuntu, Debian & Fedora distros.

---

#### Install Ubuntu/Debian dependencies
```bash
sudo apt-get update && sudo apt-get upgrade -y && 
sudo apt-get install build-essential pkg-config libc6-dev m4 \
g++-multilib autoconf libtool ncurses-dev unzip git python \
python-zmq zlib1g-dev wget curl bsdmainutils automake -y
```

#### Install Fedora dependencies

!!! warning
    Only do this step if not using Ubuntu/Debian

```bash
sudo dnf install git pkgconfig automake autoconf ncurses-devel \
python python-zmq wget gtest-devel gcc gcc-c++ libtool curl patch -y
```

#### Build zelcashd
```bash
git clone https://github.com/zelcash/zelcash.git &&
cd zelcash &&
git checkout master &&
./zcutil/build.sh -j$(nproc)
```

#### Fetch Parameter files
```
./zcutil/fetch-params.sh
```

#### Create Config File
```bash
mkdir ~/.zelcash
echo "rpcuser=username" >> ~/.zelcash/zelcash.conf
echo "rpcpassword=`head -c 32 /dev/urandom | base64`" >> ~/.zelcash/zelcash.conf 
echo "rpcallowip=127.0.0.1" >> ~/.zelcash/zelcash.conf
echo "addnode=explorer.zel.cash" >> ~/.zelcash/zelcash.conf
echo "addnode=explorer.zel.zelcore.io" >> ~/.zelcash/zelcash.conf
echo "txindex=1" >> ~/.zelcash/zelcash.conf
echo "server=1" >> ~/.zelcash/zelcash.conf
```

#### Run zelcashd
```bash
./src/zelcashd
```

---

### Building for Mac

---

#### Install Dependencies
```
xcode-select --install 
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew install cmake autoconf libtool automake coreutils pkgconfig gmp wget
brew install gcc5 --without-multilib
```

#### Build
```
git clone https://github.com/zelcash/zelcash.git
cd zelcash
git checkout master
./zcutil/build.sh -j$(sysctl -n hw.ncpu)
```

#### Fetch Parameter files
```
./zcutil/fetch-params.sh
```

#### Create Config File
```
mkdir ~/.zelcash
echo "rpcuser=username" >> ~/.zelcash/zelcash.conf
echo "rpcpassword=`head -c 32 /dev/urandom | base64`" >> ~/.zelcash/zelcash.conf
echo "rpcallowip=127.0.0.1" >> ~/.zelcash/zelcash.conf
echo "addnode=explorer.zel.cash" >> ~/.zelcash/zelcash.conf
echo "addnode=explorer.zel.zelcore.io" >> ~/.zelcash/zelcash.conf
echo "txindex=1" >> ~/.zelcash/zelcash.conf
echo "server=1" >> ~/.zelcash/zelcash.conf
```

#### Run zelcashd
```
./src/zelcashd
```

---

### Building for Windows

---

#### Install Dependencies
```
sudo apt-get install build-essential pkg-config libc6-dev m4 g++-multilib autoconf libtool ncurses-dev cmake unzip git python zlib1g-dev wget bsdmainutils automake mingw-w64 curl
```
#### Build zelcashd
```
git clone https://github.com/zelcash/zelcash.git
cd zelcash
git checkout master
./zcutil/build-win.sh -j$(nproc)
```
#### Create Config File
Create folder: `#!css %AppData%/Roaming/zelcash` <br> Create a *.txt file `#!css zelcash.conf` in above folder. Copy/paste the below into TXT file and save, 
then close.<br> <b> Change RPC username & password</b>
```
rpcuser=randomusername
rpcpassword=RandomPasswordChangeme
rpcallowip=127.0.0.1 
addnode=explorer.zel.cash
addnode=explorer.zel.zelcore.io
txindex=1
server=1
```

#### Fetch Parameter Files
Create folder `#!css %AppData%/Roaming/ZcashParams` <br>
Download the below links into this folder
???+ info "Download the below links into this folder"
    https://zelcore.io/zelcore/sapling-output.params  
    https://zelcore.io/zelcore/sapling-spend.params  
    https://zelcore.io/zelcore/sprout-groth16.params  
    https://zelcore.io/zelcore/sprout-proving.key  
    https://zelcore.io/zelcore/sprout-verifying.key

#### Run zelcashd
```
zelcashd.exe
```

---

### Install using APT repo

----

!!! tip
    The APT repo works with many popular Ubuntu & Debian distros.

```bash
echo 'deb https://zelcash.github.io/aptrepo/ all main' | sudo tee /etc/apt/sources.list.d/zelcash.list &&
gpg --keyserver keyserver.ubuntu.com --recv 4B69CA27A986265D &&
gpg --export 4B69CA27A986265D | sudo apt-key add - &&
sudo apt-get update &&
sudo apt-get install zelcash
```
This installs `#!css zelcashd`, `#!css zelcash-cli`, `#!css zelcash-tx` & `#!css zelcash-fetch-params.sh`
```bash
bash zelcash-fetch-params.sh
```

!!! note
    Create Config File as shown in the [example](#create-config-file)
