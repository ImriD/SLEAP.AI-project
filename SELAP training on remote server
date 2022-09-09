*Guide for runing SLEAP on a remout server:*
the guide was developed for bilding a remoute machine for tracking Sunflour moovment using AI progrem (SLAEP.AI) in Linode platform using Obunto 18:

start by connecting to your linode
`ssh root@(your.linode.IP)`

first time you do this it will ask you if you trust this connection
output will look like this:
`The authenticity of host .... can't be established.`
`ECDSA key fingerprint is SHA256:i1qhmrkAmM/ypwvicHQFGPtVk6BxvMhgbm4Pf3yzBE0.
Are you sure you want to continue connecting (yes/no)?`

type `yes` and continue to enter your password (you won't see yourself typing..!):
`root@(your.linode.IP)'s password:`

(It will spit out some stuff we don't care about and your in.  as can be indicated by where your typing line looking something like this:
`root@localhost:~#`)
 
now we need to install a few packeges... but before we begin lets update the operating system:
`sudo apt update && apt upgrade`


we start with downloading and then installing Anaconda:
https://www.digitalocean.com/community/tutorials/how-to-install-anaconda-on-ubuntu-18-04-quickstart

`wget https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh`

`bash Anaconda3-2021.05-Linux-x86_64.sh`

this will look something like this:

    ===================================
    End User License Agreement - Anaconda Individual Edition
    ===================================
        
    Copyright 2015-2021, Anaconda, Inc.
    ...
    ...
    ...
    Do you accept the license terms? [yes|no]
    
type `yes`  and then confirm again with enter and it will install for a while...

    Anaconda3 will now be installed into this location:
    /root/anaconda3
    
    
    
      - Press ENTER to confirm the location
      - Press CTRL-C to abort the installation
      - Or specify a different location below
    ...
    ...
    ...
It will ask if you want to init conda. type `yes` again...
this will time out - so if you don't reply in time you will need to manually do it but only after adding conda to the PATH:
`export PATH="/root/anaconda3/bin:$PATH"`
`conda init`

Now we want to create our environment:
`conda create --name my_env python=3.7`

When this is done you can reboot the machine - sorry... be patient...
`reboot`

After you log back in you want to activate your environment:
`conda activate my_env`

in our env we can now install the nvidia drivers 
`sudo apt-get install build-essential`
`sudo apt-get -y install --no-install-recommends nvidia-driver-440`
and specify tensorflow should use the ***cudatoolkit=10.1***
`conda install tensorflow-gpu cudatoolkit=10.1`

before you install sleap you can run python and see if the gpu is recognized:
`python`

    >>> import tensorflow as tf
output shoud look like this:

    2021-11-09 10:09:14.302439: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.10.1
    
if this worked you can also try this:

    >>> tf.config.list_physical_devices('GPU')
response should look like this:

    2021-11-09 10:09:25.501141: I tensorflow/compiler/jit/xla_cpu_device.cc:41] Not creating XLA devices, tf_xla_enable_xla_devices not set
    ...
    ...
	2021-11-09 10:09:26.083519: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1720] Found device 0 with properties:
	pciBusID: 0000:00:02.0 name: Quadro RTX 6000 computeCapability: 7.5
	coreClock: 1.77GHz coreCount: 72 deviceMemorySize: 23.65GiB deviceMemoryBandwidth: 625.94GiB/s
	...
	...
	2021-11-09 10:09:26.101672: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1862] Adding visible gpu devices: 0
	[PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
 
if this worked you should be able to `pip install sleap`
in the future we may need to specify the version here as well:`pip install sleap==1.1.5`

now lets create a folder for our project:
`mkdir  destination_folder_name`
you may want to add more subfolders depending on what you are planning...

to move files to the linode you can either `exit` and use *scp* in the current terminal or open a new terminal.

you can use ***scp*** to move files like this.
`scp -r junk.txt root@173.255.236.221:/root/destination_folder_name`
 (to **download** files later you use scp 'in reverse' also from your machine :)
`scp -r root@173.255.236.221:/root/destination_folder_name/filename/ /Users/user/Desktop` 
here is an entire guide if you have any trouble with scp
https://www.linode.com/docs/guides/download-files-from-your-linode/

if you use **several files** it might make sense to zip them first so install **zip and unzip**:
`sudo apt-get install zip && apt-get install unzip`

after that you can use sleap as you would in colab:
for training: `sleap-train multi_instance.json something.pkg.slp`

for tracking:

    !sleap-track  video_name.mp4 \
         --frames 0-1450\ #nmber of frames
         --tracking.tracker simple \
         --tracking.target_instance_count 1\ #number of plants to fined
         --tracking.clean_instance_count 1\ #number of plants to  leave
         --tracking.min_new_track_points 4\ # minimum number of nodes for ditect a plant
         -m number.multi_instance 
    
for inspaction: `sleap-inspect video_name.mp4.predictions.slp` #Get traking info

(to zip directory:
`root@localhost:~/directory# zip -r example.zip 211110_095246.multi_instance`We )













