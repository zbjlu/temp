# temp

vscode:

GitHub Gist: 5f9cb7fb115c2f9283a0667c79c4d26a

ubuntu tools:

http://wps-community.org/download.html

google material:
 
https://material.io/

vnc-server:
server ip:
125.65.88.83:5991

teamviewer:
ID:
1197814804
pwd:
s84c1q



zephyr wiki:

IoT: Zephyr & Mcuboot

Downloading source code

mkdir zephyr && cd zephyr

repo init -u gitadmin@gitmirror.spreadtrum.com:sprd_IoT/zephyr -b unsc_marlin3_mcu

repo sync --no-tags -cq -j8

repo start --all unsc_marlin3_mcu


Setting Environment
Install the required packages in a Ubuntu host system with:

sudo apt-get install --no-install-recommends git cmake ninja-build gperf \
  ccache doxygen dfu-util device-tree-compiler python3-dev \
  python3-ply python3-pip python3-setuptools python3-wheel xz-utils file \
  make gcc-multilib autoconf automake libtool libffi-dev libssl-dev mtools \
  gcc-multilib g++-multilib
  
  
  
Install additional packages required for development with Zephyr:

cd zephyr  # or to your directory where zephyr is cloned

pip3 install --user -r scripts/requirements.txt

#or use below command if you suffer timeout error

pip3 --default-timeout=100 install --user -r scripts/requirements.txt

pip3 install --user cryptography paramiko IntelHex idna

For more details, please follow the guideline below.

 http://docs.zephyrproject.org/getting_started/getting_started.html
 

Building
make
After the compilation, the binaries can be found under dir build/images.
Note:the building environment will be extracted automatically for the first time.

