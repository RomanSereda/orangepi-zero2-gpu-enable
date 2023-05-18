Install image
------------
#### [Download and  install the image on the sd card Orangepizero2_3.0.6_ubuntu_jammy_desktop_xfce_linux5.16.17.img](https://drive.google.com/file/d/1qTtGsdRtx4EtQQIXGP-6RgXL6NTIjvmw/view?usp=share_link "Download and  install the image on the sd card Orangepizero2_3.0.6_ubuntu_jammy_desktop_xfce_linux5.16.17.img")

	# insert sd-card, turn on, wait 5 min, off-on power supply
	# connect usb-uart-tll. set pytty serial: COM8 (8 for me), speed 115200
	# login: orangepi  password: orangepi

	 sudo orangepi-config

	# network->wifi, set wifi password.
	# set pytty ssh: 192.168.x.x, port 22.
	
Update
------------
	sudo nano /etc/apt/sources.list
	# uncomment deb-src

	sudo apt update
	sudo apt upgrade

	sudo apt install glslang-tools mesa-utils clinfo flex bison cmake meson ninja-build bc python3-pip build-essential 
	sudo apt install libncurses5-dev xfonts-base libjpeg-dev libpng-dev mesa-opencl-icd ocl-icd-opencl-dev libunwind-dev

	pip3 install setuptools mako
	sudo apt build-dep mesa libdrm

Clear snap
------------
	sudo snap remove --purge cups
	sudo snap remove --purge chromium
	sudo snap remove --purge gnome-3-38-2004
	sudo snap remove --purge gtk-common-themes
	sudo snap remove --purge snapd-desktop-integration
	sudo snap remove --purge bare
	sudo snap remove --purge core20
	sudo snap remove --purge snapd
	sudo systemctl disable snapd.service
	sudo systemctl disable snapd.socket
	sudo apt purge snap
	rm -rf ~/snap
	sudo rm -rf /snap
	sudo rm -rf /var/snap
	sudo rm -rf /var/lib/snapd

Install glmark2
------------
	git clone https://github.com/glmark2/glmark2.git
	cd glmark2
	meson setup build -Dflavors=x11-glesv2 
	ninja -C build
	sudo ninja -C build install

	#run benchmark
	glmark2-es2 --off-screen

Remote desktop
------------
	sudo apt-get install xrdp xorgxrdp
	sudo systemctl enable xrdp
	sudo systemctl status xrdp

	#login: root  password: orangepi - for windows rdp

Compile and install mesa
------------
	pip3 install setuptools mako
	sudo apt build-dep mesa libdrm

	wget https://archive.mesa3d.org/mesa-23.1.0.tar.xz
	tar -xf mesa-23.1.0.tar.xz
	mv mesa-23.1.0 mesa-source
	cd mesa-source
	export MESA_INSTALLDIR=/usr
	meson setup build/ -Dprefix=/usr -Dgallium-drivers=panfrost -Dtools=drm-shim -Dvulkan-drivers=panfrost -Dllvm=disabled
	ninja -C build/
	sudo ninja -C build/ install

Boost
------------
	size="4G" && file_swap=/swapfile_$size.img && sudo touch $file_swap && sudo fallocate -l $size /$file_swap && sudo mkswap /$file_swap && sudo swapon -p 20 /$file_swap
	wget https://boostorg.jfrog.io/artifactory/main/release/1.82.0/source/boost_1_82_0.tar.gz
	tar xzvf boost_1_82_0.tar.gz
	cd boost_1_82_0/
	./bootstrap.sh --prefix=/usr/
	./b2
	sudo ./b2 install


