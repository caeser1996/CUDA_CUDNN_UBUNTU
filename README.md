**Cudnn And CUDA setup for Ubuntu**

1. Get a VM wih Ubuntu 18.04
2. SSH into the VM
3. Install Nvidia Graphics Driver Using 
```Bash
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo ubuntu-drivers autoinstall
```
4. Above will install the latest driver required  for Nvidia Card used in VM
5. Check GCC version using 
```language
gcc --version
```
6. Install gcc-5 ,gcc-6, g++-5 ,g++-6
```
sudo apt install gcc-5 gcc-6 g++-5 g++-6
```
7. Update alternatives for GCC
```language
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 10
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 20

sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-6 10
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++6 20
```
8. Above will update the Alternatives for gcc now select the gcc compiler for system.
```language
sudo update-alternatives --config gcc
```
9. Above command will give the list of gcc option in the sytem.Select the gcc5 option .

```language
sudo update-alternatives --config g++
```
9. Above command will give the list of gcc option in the sytem.Select the g++ option .

10.  Now select the gcc version the way you did before in point no 5.Make sure you get the version 5 as return.
11. Restart the VM for the above changes to reflected in the system.Once restart is successfull check nvidia-smi by.
```language
nvidia-smi
```
----------
Below steps is for cuda installation

----------


12. Go the https://developer.nvidia.com/Cuda-10.1-download-archive-base?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=runfilelocal
for getting cuda download url .
13. Once you visit the site copy the download url from download link.It will look like 
https://developer.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda_10.1.105_418.39_linux.run
14. Now get the cuda run file in the vm using.
```language
wget https://developer.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda_10.1.105_418.39_linux.run
```

** Make sure to download above you should have a register nvidia account at https://developer.nvidia.com/

15. Run the file downloaded in step 14 using
```language
sudo sh cuda_10.1.105_418.39_linux.run
```
Accept all the terms and conditions.
Select Cuda Tollkit 10.1 and Cuda Demo Suite 10.1 and uncheck rest select install then it will install the above.

16. Once above is installed successfully update the cuda path using below steps
```language
sudo nano /etc/environment
```
It will open the environment.Add the below context into the path variable in environment file.
```language
/usr/local/cuda/bin:
```
17. Add LD_LIBRARY_PATH variable in environment just after path variable.
```language
LD_LIBRARY_PATH="/usr/local/cuda/lib64:usr/local/cuda-10.1/targets/x86_64-linux/lib"
```
** Make sure there are no spaces betweeen variable name and variable value.

18. Create a symlink between cuda-10.1 and cuda using 
```
sudo ln -s /usr/local/cuda-10.1 /usr/local/cuda

```
19. Update the environment into the system using.
```language
source /etc/environmnt
```
20. Now check nvc --version using .
```language
nvcc --version
```
Make sure after you hit the command you see the release version as 10.1.105
21. Generate the SSH keys for setting up the GIT using 
```language
ssh-keygen
```
** Continue press untill you see a rohmbus with stars and some unicode characters.

22. Get the ssh keys generated above by .
```language
cat ~/.ssh/id.rsa.pub
```
23. Copy the ssh key from the above command add it to repository and clone the project.
24. Install python 3.7 using below commands.
```language

sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install python3.7
sudo rm -rf /usr/bin/python
sudo ln -s /usr/bin/python3.7 /usr/bin/python
sudo apt install python3-pip
sudo apt install python-pip
pip install --upgrade pip
```

25. Check python version by python --version make sure you can can python 3.7.* as default python version.
26. Download CUDNN for the above package got to https://developer.nvidia.com/compute/machine-learning/cudnn/secure/7.6.5.32/Production/10.1_20191031/cudnn-10.1-linux-x64-v7.6.5.32.tgz


*** Make sure you have Nvidia Account to download this and transfer it to Virtual Machine using FTP.
27. Once done follow the below steps
```language
tar -xzvf cudnn-x.x-linux-x64-v7.6.5.32.tgz
sudo cp cuda/include/cudnn*.h /usr/local/cuda/include 
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda/lib64 
sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
```

28. Now install tensorflow-gpu in the system using.
```language
pip install tensorflow-gpu==2.3.1
```
29. Open python hitting python in the terminal once done check the tensoflow is using graphics dirver properly using .
```language
import tensorflow as tf
tf.test.is_gpu_available()
```

** Make sure you get True in return if not follow the above steps and check if you have missed anything.

