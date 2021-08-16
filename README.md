# Setting up your local machine for deep learning

It's not an easy task to get your ML/DL workstation environment up and running.If you are a windows user or only tried cloud platforms like google colab then this guide is certainly for you ! 

----------------------------------------------------------------------------------------------------

## My system 
device: Lenovo Legion Y530-15ICH

GPU: GeForce GTX 1060 (6GB)

HDD type : GPT

RAM: 16GB

----------------------------------------------------------------------------------------------------

## OS
Any linux distro that is deep learning compatible can be used. you can also use windows but the installation is a little bit trickier. This guide contains steps to setup `Ubuntu 20.04` for deep learning.

############image ubuntu############ 

**Installing Ubuntu 20.04**:

I tried a dual boot for Ubuntu alongside windows and it worked.

steps:

1- Download `ubuntu20.04 LTS` from here [link](https://ubuntu.com/download/desktop)

2- Download rufus which is a usb bootloader from here [link](https://rufus.ie/en/)

3- Get an empty flash USB drive (4GB is fine) but (8-16 GB recommended).

3- Free some space for your new OS from the disk management in windows by shrinking the volume of one of your disks (make sure the new unallocated space suits your needs) this link may help [link](https://www.youtube.com/watch?v=tJiakVgAtn4)

4- Using rufus boot ubuntu on the flash drive (make sure you don't have any important files on it as it will be formatted. ) [link](https://www.youtube.com/watch?v=xnisuFk-cDg)

5- This step is tricky as it differs from device to another but the main goal is the same. disable secure booting and enable UEFI/ legacy booting depending on your device .follow this link here to check your deviice booting [link](https://www.youtube.com/watch?v=QvI8di8I1Ao)

6- Go to the boot menu in your device and choose the usb drive .

7- ollow the install instructions by the prompt windows. this may help [link](https://www.youtube.com/watch?v=G7ffzC4S0A4)

----------------------------------------------------------------------------------------------------

## Nvidia driver-460

steps:

1- From your applications menu search for software and updates

2- select the additional drivers tab 

3- I chose nvidia-460 driver and the rest of this guide is based on it (you can choose other drivers but you have to choose other compatible CUDA toolkit and cuDNN ). click apply changes .

4- click ctrl+alt+T to open terminal and type `reboot` to restart your system 

5- click ctrl+alt+T to open terminal  and type `nvidia-smi` to check driver install you should expect something like this 

----------------------------------------------------------------------------------------------------

## cuda Toolkit 11.2 

warning never try sudo apt install cuda-toolkit as it's locked to cuda 10.1 which is not compatible with new drivers.

steps:

1- Go to [link](https://developer.nvidia.com/cuda-11.2.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=2004&target_type=deblocal) open terminal and use the best installation commands provided.

2- After finishing the installation it's important to add CUDA to your path.
open terminal and type this command to open the bashrc file 

```bash
sudo nano ~/.bashrc
```
copy and add these lines to the end of the bashrc file 
```bash
export PATH=/usr/local/cuda-11.2/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-11.2/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
export CUDA_HOME=/usr/local/cuda
```
3- perform a system reboot 
```bash
reboot
```
4- verify cuda toolkit installation using this command
```bash
nvcc -V
```
you should expect something like this 

----------------------------------------------------------------------------------------------------

## cuDNN 8.1

steps :

1-To download cuDNN you need to have a nvidia developer account which is easy to make. Then fill their 2-min survey and agree to the terms and conditions and choose archived versions

2- I tried the debian installation and it worked (you can try other installations too) for debian installations download runtime,developer and samples library as shown here 

3- open terminal and type the following commands :

    sudo apt-get install libfreeimage3 libfreeimage-dev
then

`cd Downloads/`

To install runtime library:

    sudo dpkg -i libcudnn8_x.x.x-1+cudax.x_amd64.deb

(use tab to fill the x's with the version you downloaded)
  
To install the developer library, for example:

    sudo dpkg -i libcudnn8-dev_8.x.x.x-1+cudax.x_amd64.deb


To install the code samples and the cuDNN library documentation, for example:

    sudo dpkg -i libcudnn8-samples_8.x.x.x-1+cudax.x_amd64.deb


### verifying cuDNN installation


Procedure

   Copy the cuDNN samples to a writable path.

    $cp -r /usr/src/cudnn_samples_v8/ $HOME

   Go to the writable path.

    $ cd  $HOME/cudnn_samples_v8/mnistCUDNN

   Compile the mnistCUDNN sample.

    $make clean && make

   Run the mnistCUDNN sample.

    $ ./mnistCUDNN

   If cuDNN is properly installed and running on your Linux system, you will see a message similar to the following:

    Test passed!
----------------------------------------------------------------------------------------------------
By far the hardest part should have passed the rest is the easy stuff.

**Install Chrome**  
[link](https://www.google.com/chrome)

 -  ` sudo dpkg -i google-chrome-stable_current_amd64.deb`

----------------------------------------------------------------------------------------------------

**Install Development Tools**:

 - ` sudo apt install build-essential pkg-config cmake cmake-qt-gui ninja-build valgrind`

----------------------------------------------------------------------------------------------------

**Install Git**:

```sh
 sudo apt install git
 git config --global user.name "Name"
 git config --global user.email "name@domain.com"
 
```


----------------------------------------------------------------------------------------------------

**Install Python 3**:

- ` sudo apt install python3 python3-wheel python3-pip python3-venv python3-dev python3-setuptools`

