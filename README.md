- [暫時沒有GUI系統畫面](#暫時禁用GUI系統畫面)
- [暫時有GUI系統畫面](#暫時啟用GUI系統畫面)
- [永久禁用GUI系統畫面](#永久禁用GUI系統畫面)
- [永久啟用GUI系統畫面](#永久啟用GUI系統畫面)
- [螢幕不休息](#螢幕不休息)
- [安裝pip3](#安裝pip3)
- [安裝nano文字編輯器](#安裝nano文字編輯器)
- [建置虛擬記憶體](#建置虛擬記憶體)
- [設定虛擬記憶體使用率](#設定虛擬記憶體使用率)
- [設定清除快取記憶體頻率](#設定清除快取記憶體頻率)
- [設定cuda環境變數](#設定cuda環境變數)
- [建置jtop資源監視器](#建置jtop資源監視器)
- [安裝pytorch](#安裝pytorch)
- [安裝torchvision](#安裝torchvision)
- [安裝jetcam](#安裝jetcam)
- [安裝jupyter](#安裝jupyter)
- [安裝matplotlib](#安裝matplotlib)
- [安裝opencv-python](#安裝opencv-python)
- [安裝tkinter](#安裝tkinter)
- [設定python環境指令](#設定python環境指令)
- [設定終端機預設路徑](#設定終端機預設路徑)
- [安裝SimpleScreenRecorder - 螢幕錄製](#安裝SimpleScreenRecorder)
## 暫時禁用GUI系統畫面
```
sudo init 3 

```
## 暫時啟用GUI系統畫面
```
sudo init 5 

```
## 永久禁用GUI系統畫面
```
sudo systemctl set-default multi-user.target

```
## 永久啟用GUI系統畫面
```
sudo systemctl set-default graphical.target

```
## 螢幕不休息
```
gsettings set org.gnome.desktop.session idle-delay 0

```
## 安裝pip3
```
sudo apt-get update
sudo apt-get -y install python3-pip
pip3 install --upgrade pip
pip3 --version

```
## 安裝nano文字編輯器
```
sudo apt-get install nano

```
## 建置虛擬記憶體
```
sudo swapon --show
sudo fallocate -l 6g /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo bash -c 'echo "/swapfile swap swap defaults 0 0" >> /etc/fstab'
sudo swapon --show
sudo free -h

```
## 設定虛擬記憶體使用率
```
cat /proc/sys/vm/swappiness
sudo nano /etc/sysctl.conf
```
#### 寫入
```
vm.swappiness=10
```

## 設定清除快取記憶體頻率
```
cat /proc/sys/vm/vfs_cache_pressure
sudo nano /etc/sysctl.conf

```
#### 寫入
```
vm.vfs_cache_pressure = 500
```

## 設定cuda環境變數
```
sudo nano ~/.bashrc

```
#### 寫入
```
export cuda_home=/usr/local/cuda-10.2
export ld_library_path=/usr/local/cuda-10.2/lib64:$ld_library_path
export path=/usr/local/cuda-10.2/bin:$path
```
```
source ~/.bashrc
nvcc -v

```
## 建置jtop資源監視器
```
sudo apt-get install python3-pip python3-dev build-essential
sudo -h pip3 install jetson-stats
sudo systemctl restart jetson_stats.service
sudo reboot

```

## 安裝pytorch
#### verion 1.2.0
- [配合jetson-nano系統版本-r32.3.1-jp4.3.0-20191217](https://developer.nvidia.com/jetson-nano-sd-card-image-r3231)
```
sudo apt-get install -y python3-pip libopenblas-base libopenmpi-dev

```
```
wget https://nvidia.box.com/shared/static/06vlvedmqpqstu1dym49fo7aapgfyyu9.whl -o torch-1.2.0a0+8554416-cp36-cp36m-linux_aarch64.whl
sudo apt-get install python3-pip libopenblas-base libopenmpi-dev
pip3 install cython
pip3 install numpy torch-1.2.0a0+8554416-cp36-cp36m-linux_aarch64.whl

```

## 安裝torchvision
#### torchvision 0.4.0
```
pip3 install setuptools
sudo apt-get install -y libjpeg-dev libfreetype6-dev pkg-config libpng-dev libhdf5-serial-dev hdf5-tools libhdf5-dev

```
```
git clone --branch v0.4.0 https://github.com/pytorch/vision torchvision
cd torchvision
sudo python3 setup.py install
cd ..

```
## 安裝jetcam
```
git clone https://github.com/nvidia-ai-iot/jetcam
cd jetcam
sudo python3 setup.py install
cd ..

```

## 安裝jupyter
#### jupyter lab
```
sudo -h pip3 install --upgrade pip
pip3 install jupyter jupyterlab
sudo reboot

```
```
jupyter lab --generate-config
nano -c ~/.jupyter/jupyter_lab_config.py

```
#### 寫入
```
c.serverapp.allow_origin = '*'
c.serverapp.ip = '0.0.0.0'
```
```
jupyter lab password

```
```
sudo nano /etc/systemd/system/jupyter.service

```
#### 寫入
```
[unit]
description=jupyter notebook
[service]
type=simple
user=icshop
execstart=/home/icshop/.local/bin/jupyter-lab --port 8888 --no-browser
workingdirectory=/home/icshop/
[install]
wantedby=default.target
```
```
sudo systemctl enable jupyter
sudo systemctl start jupyter
sudo systemctl status jupyter

```

## 安裝matplotlib
```
pip3 install matplotlib

```
## 安裝opencv-python
```
pip3 install opencv-python

```
## 安裝tkinter
#### python 2
```
sudo apt-get install python-tk

```
#### python 3
```
sudo apt-get install python3-tk

```
## 設定python環境指令
#### 設定python3.6 為1優先
```
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1
```
#### 設定python2.7 為2次之
```
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 2
```
#### 切換環境模式
```
sudo update-alternatives --config python

```
#### 顯示清單
```
sudo update-alternatives --display python

```
#### 移除設定
```
sudo update-alternatives --remove-all python

```
## 設定終端機預設路徑
```
gedit ~/.bashrc

```
#### 寫入
```
cd 你自己的路徑
```
## 安裝SimpleScreenRecorder
```
sudo add-apt-repository ppa:maarten-baert/simplescreenrecorder
sudo apt update
sudo apt install simplescreenrecorder

```
