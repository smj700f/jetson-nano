------------------螢幕不休息
### 螢幕不休息 (using `rest`)
gsettings set org.gnome.desktop.session idle-delay 0

------------------安裝pip3
pip3 --version
sudo apt-get update
sudo apt-get -y install python3-pip
pip3 --version
pip3 install --upgrade pip
pip3 --version

------------------安裝nano文字編輯器
sudo apt-get install nano

------------------建置虛擬記憶體
sudo swapon --show
sudo fallocate -l 6G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo bash -c 'echo "/swapfile swap swap defaults 0 0" >> /etc/fstab'
sudo swapon --show
sudo free -h

------------------設定虛擬記憶體使用率
cat /proc/sys/vm/swappiness
sudo nano /etc/sysctl.conf

/*-------------------------------*/寫入
vm.swappiness=10
/*-------------------------------*/寫入

------------------設定清除快取記憶體頻率
cat /proc/sys/vm/vfs_cache_pressure
sudo nano /etc/sysctl.conf

/*-------------------------------*/寫入
vm.vfs_cache_pressure = 500
/*-------------------------------*/寫入

------------------設定CUDA環境變數
sudo nano ~/.bashrc

/*-------------------------------*/寫入
export CUDA_HOME=/usr/local/cuda-10.2
export LD_LIBRARY_PATH=/usr/local/cuda-10.2/lib64:$LD_LIBRARY_PATH
export PATH=/usr/local/cuda-10.2/bin:$PATH
/*-------------------------------*/寫入

source ~/.bashrc
nvcc -V
------------------建置jtop資源監視器
sudo apt-get install python3-pip python3-dev build-essential
sudo -H pip3 install jetson-stats
sudo systemctl restart jetson_stats.service
sudo reboot

------------------安裝Pytorch 1.2.0
sudo apt-get install -y python3-pip libopenblas-base libopenmpi-dev

wget https://nvidia.box.com/shared/static/06vlvedmqpqstu1dym49fo7aapgfyyu9.whl -O torch-1.2.0a0+8554416-cp36-cp36m-linux_aarch64.whl
sudo apt-get install python3-pip libopenblas-base libopenmpi-dev
pip3 install Cython
pip3 install numpy torch-1.2.0a0+8554416-cp36-cp36m-linux_aarch64.whl

------------------安裝torchvision 0.4.0
pip3 install setuptools
sudo apt-get install -y libjpeg-dev libfreetype6-dev pkg-config libpng-dev libhdf5-serial-dev hdf5-tools libhdf5-dev

git clone --branch v0.4.0 https://github.com/pytorch/vision torchvision
cd torchvision
sudo python3 setup.py install
cd ..

------------------安裝Jetcam
git clone https://github.com/NVIDIA-AI-IOT/jetcam
cd jetcam
sudo python3 setup.py install
cd ..

------------------安裝Jupyter lab
sudo -H pip3 install --upgrade pip
pip3 install jupyter jupyterlab
sudo reboot

jupyter lab --generate-config
nano -c ~/.jupyter/jupyter_lab_config.py

/*-------------------------------*/寫入
c.ServerApp.allow_origin = '*'
c.ServerApp.ip = '0.0.0.0'
/*-------------------------------*/寫入

jupyter lab password

sudo nano /etc/systemd/system/jupyter.service

/*-------------------------------*/寫入
[Unit]
Description=Jupyter Notebook
[Service]
Type=simple
User=icshop
ExecStart=/home/icshop/.local/bin/jupyter-lab --port 8888 --no-browser
WorkingDirectory=/home/icshop/
[Install]
WantedBy=default.target
/*-------------------------------*/寫入

sudo systemctl enable jupyter
sudo systemctl start jupyter
sudo systemctl status jupyter

------------------安裝matplotlib
pip3 install matplotlib

------------------安裝opencv-python
pip3 install opencv-python

------------------安裝tkinter
--python 2
sudo apt-get install python-tk

--python 3
sudo apt-get install python3-tk

------------------設定python環境指令
--1優先、2次之
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 2

--切換環境模式
sudo update-alternatives --config python

--顯示清單
sudo update-alternatives --display python

--移除設定
sudo update-alternatives --remove-all python

