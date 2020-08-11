---
layout: post
subtitle: Setup JetsonNano
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
last_modified_at: 2020-08-11 13:58:00 +0000
tags: [IoT, JetsonNano]
---

## Step 1. Preparation
* Jetson Nano
* 5V 4A Barrel Jack Power Supply
* Micro USB cable
* SD Card (64GB or 128GB)
* Network card or Edimax EW-7811Un
* Header jumper - which should be supplied with the most recent versions

## Step 2. Download JetPack & Install on SD Card
* Jetson Nano Developer Kit SD Card Image
* [JetPack 4.4](https://developer.nvidia.com/embedded/downloads)

## Step 3. Setup Environment
* [Upgrade a Swap File](#updgrade-a-swap-file)
* [Install Remote Desktop Service](#install-a-remote-desktop-service)
* [Install Deep Learning Frameworks](#install-deep-learning-frameworks)

### Upgrade a Swap File

```
echo "********** Update System **********"
sudo apt-get update
sudo apt-get upgrade

echo "********** Create Swap File **********"
sudo fallocate -l 8G /var/swapfile
sudo chmod 600 /var/swapfile
sudo mkswap /var/swapfile
sudo swapon /var/swapfile
sudo bash -c 'echo "/var/swapfile swap swap defaults 0 0" >> /etc/fstab'
sudo apt-get update
sudo apt-get upgrade
```

### Install a Remote Desktop Service


### Install Deep Learning Frameworks

```
echo "********* Installing Pytorch ***********"
# For Python 2.7
#wget https://nvidia.box.com/shared/static/1v2cc4ro6zvsbu0p8h6qcuaqco1qcsif.whl -O torch-1.4.0-cp27-cp27mu-linux_aarch64.whl
#sudo apt-get install libopenblas-base libopenmpi-dev 
#pip install future torch-1.4.0-cp27-cp27mu-linux_aarch64.whl

# For Python 3.6
# Check pytorch and torchversion in README
wget https://nvidia.box.com/shared/static/ncgzus5o23uck9i5oth2n8n06k340l6k.whl -O torch-1.1.0-cp36-cp36m-linux_aarch64.whl
pip apt-get install python3-pip libopenblas-base libopenmpi-dev 
pip install Cython
pip install numpy torch-1.1.0-cp36-cp36m-linux_aarch64.whl

echo "********* Installing TorchVision ***********"
sudo apt-get install libjpeg-dev zlib1g-dev
git clone --branch v0.3.0 https://github.com/pytorch/vision torchvision   # see below for version of torchvision to download
cd torchvision
python setup.py install
cd ../  # attempting to load torchvision from build dir will result in import error
pip install 'pillow<7' # always needed for Python 2.7, not needed torchvision v0.5.0+ with Python 3.6


echo "********* Installing Tensorflow ***********"
sudo apt-get update
sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran
pip install -U numpy grpcio absl-py py-cpuinfo psutil portpicker six mock requests gast h5py astor termcolor protobuf keras-applications keras-preprocessing wrapt google-pasta setuptools testresources
pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v43 tensorflow-gpu==2.0.2+nv20.1
```

### References
* [Setting up Jetson Nano](https://github.com/hoangminhtoan/Setup_Envs)


