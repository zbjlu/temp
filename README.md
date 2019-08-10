# temp

git 官网：

https://git-scm.com/book/zh/v2

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

repo init -u https://github.com/unisoc/manifests.git -b master

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

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++======+++++++++++++++++++++++++++

# zircon资料

https://fuchsia.dev/fuchsia-src/zircon/ddk

# 加速ipc/rpc性能

http://delivery.acm.org/10.1145/3330000/3322218/p671-du.pdf?ip=121.12.147.248&id=3322218&acc=ACTIVE%20SERVICE&key=BF85BBA5741FDC6E%2E83F2654D43953101%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&__acm__=1565427651_417503d92dd5159d82d32fa5dd64caf8

https://ipads.se.sjtu.edu.cn/_media/publications/skybridge-eurosys19.pdf

# 自研学习

https://developer.tizen.org/development/api-references/native-application?redirect=https://developer.tizen.org/dev-guide/5.0.0/org.tizen.native.mobile.apireference/group__CAPI__TELEPHONY__INFORMATION.html

https://nodejs.org/zh-cn/docs/
