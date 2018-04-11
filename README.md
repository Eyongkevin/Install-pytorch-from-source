
# Install pytorch from source
-------------------
Here, I describe a simple and efficient way to install pytorch from source. I also sight out some of the problems encountered during installation and how to solve them.

I am using **Ubuntu v16.4, python v3.6, CUDA v8, and cuDNN  v7.1.**

**NB:** *Make sure **cuDNN** is v6 and above. I will recomment v7 and above.*

## Steps

- **I recommend you do this in an environment. With Anaconda, create an env.**

    `conda create -n envName python=3.6 anaconda`
    
    
- **Make sure g++ is installed and up to date.**

    `sudo apt-get install g++ cmake`
    
    
- **Install some dependencies**

    `conda install numpy pyyaml mkl setuptools cffi`
    
    
- **Clone the repository**

    `git clone https://github.com/pytorch/pytorch.git`
    
    
- **move to pytorch directory and update submodule git**

    `cd pytorch`
    
    `git submodule update --init`
    
    
- **install pytorch**

    `python setup.py install`
    
After all installation has been done. Close the terminal, open a new terminal, activate the environment, start python and import torch.

## Problem faced when importing torch

### 1. undefined symbol: mkl_lapack_sgelqf
this is because you have an older version of **mkl**. But more importantly it seems to be loaded into the process already. Maybe you can install mkl from anaconda or intel channels: `conda install mkl=2018 -c anaconda or conda install mkl=2018 -c intel`

**NB:** *mkl should have been updated when installing dependencies above.*

### 2. ModuleNotFoundError: No module named 'torch._C'
The problem is that you have a folder called torch in the same directory which is being picked up. Do this: cd .. (to change directory), and then start python and import torch, it should work.

**NB:** *When you clone pytorch, it creates a folder called **pytorch**, so if you happen to start python and import torch in a directory containing this **pytorch** folder, this folder will be picked up instead, hence leading to the error above.*
