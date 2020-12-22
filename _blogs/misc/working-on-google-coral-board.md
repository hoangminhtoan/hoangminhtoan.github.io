---
layout: post
subtitle: Setup Google Coral Board
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
last_modified_at: 2020-12-22 13:58:00 +0000
tags: [IoT, Coral Board]
---

# Contents
* [Get Started with the Dev Board](get-started-with-the-dev-board)
* [Setup additional Libs](setup-additional-libs)



### Get Started with the Dev Board
1. Flash the Board


2. Install TensorFlow Lite interpreterd
```
pip3 install https://github.com/google-coral/pycoral/releases/download/release-frogfish/tflite_runtime-2.5.0-cp37-cp37m-linux_aarch64.whl
```

### Setup additional Libs
1. Mount USB formatted to **ext** file system
sudo fdisk -l

# at the end is your device, e.g /dev/sda1

2. Create a swapfile on USB
* Check usage of RAM and swap partition
```
free -u
```

 * Add more space into swapfile
the Dev Board only has 1GB of RAM, therefore, I will create additional 8GB on swap paritifion on external SD card or USB
```
sudo mount /dev/sda1 /directory/to/board (e.g. /mnt) # mount SD card to directory on the board

sudo fallocate -l 8G /mnt/swapfile
sudo chmod 600 /mnt/swapfile
sudo mkswap /mnt/swapfile
sudo swapon /mnt/swapfile
sudo swapon -s  # show the status of sawp

3. Install OpenCV4.1.1
* Download OpenCV
```
git clone https://github.com/pjalusic/opencv4.1.1-for-google-coral.git
```

* Create soft link list or copy cv2.so file to /usr/local/lib/python3.7/dist-packages/

```
cp opencv4.1.1-for-google-coral/cv2.so /usr/local/lib/python3.7/dist-packages/cv2.so
```
or 
```
ln -sf opencv4.1.1-for-google-coral/cv2.so /usr/local/lib/python3.7/dist-packages/cv2.so
```

* Copy others .so files to /usr/local/lib
```
sudo cp -r opencv4.1.1-for-google-coral/libraries/. /usr/local/lib
```
or 
```
sudo ln -sf opencv4.1.1-for-google-coral/libraries/. /usr/local/lib
```

* Check if it works
```
python3  
`>>>` import cv2  
`>>>` cv2.__version__  
'4.1.1'
```


### References
 [Official Setting up Google Dev Board](https://coral.ai/docs/dev-board/get-started)  
 [TensorFlow Lite](https://www.tensorflow.org/lite/guide/python) [Install OpenCV on Google Dev Board](https://krakensystems.co/blog/2020/doing-machine-vision-on-google-coral)