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

Install glmark2
------------
	pip3 install setuptools mako
	sudo apt build-dep mesa libdrm

	git clone https://github.com/glmark2/glmark2.git
	cd glmark2
	meson setup build -Dflavors=x11-glesv2 
	ninja -C build
	sudo ninja -C build install

	#run benchmark
	glmark2-es2 --off-screen
	#extern terminal: sudo env DISPLAY=:10.0 glmark2-es2 --off-screen
	
![Untitled](https://github.com/RomanSereda/orangepi-zero2-gpu-enable/assets/31166559/fbee0507-57d9-4e1b-980e-4013684db004)


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



