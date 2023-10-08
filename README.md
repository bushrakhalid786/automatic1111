## Prerequisites
We need the following environment for the installation:
- Ubuntu 22.04
- Kernel 15XXX
- Python 3.10.6
- CUDA 11.8

## Installation Steps

### Update and Upgrade

```bash
sudo apt update && sudo apt upgrade

### to install the GNU Compiler Collection (GCC)
sudo apt install gcc
sudo apt install make
sudo apt install zlib1g-dev
sudo apt install aria2

### Python 3.10.6 !!! this version 

wget https://www.python.org/ftp/python/3.10.6/Python-3.10.6.tgz
tar -zxvf Python-3.10.6.tgz
cd Python-3.10.6 
./configure --prefix=/usr
make
make test 
sudo make install
sudo apt install python3-venv

### We can check Pip

which pip3


### cd .. to root directory

git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git

### cd stable-diffusion-webui
./webui.sh


###Install GFPGAN
cd /stable-diffusion-webui/models/GFPGAN
wget https://github.com/TencentARC/GFPGAN/releases/download/v1.3.0/GFPGANv1.3.pth
wget https://github.com/TencentARC/GFPGAN/releases/download/v1.3.0/GFPGANv1.4.pth

### cd ../../stable-diffusion-webui
source ./venv/bin/activate

cd repositories
git clone https://github.com/facebookresearch/xformers.git
cd xformers
git submodule update --init --recursive
pip install -r requirements.txt 
pip install e .
###this will take 1 or 2 hours ???

###then you can run with this commmand from stable-diffusion-webui dir
./webui.sh --share --xformers 


#### Inacse your CUDA 11.8 Driver is not installed.
#### https://developer.nvidia.com/cuda-11-8-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_local

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2204-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt update ##ignore this errors
sudo apt -y install cuda

### We can check CUDA
nvidia-smi
####

## I recommend to add these Models, Checkpoints, Lora
### Models:
### Base Model SDXL 

https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/tree/main
### Refiner SDXL
https://huggingface.co/stabilityai/stable-diffusion-xl-refiner-1.0/tree/main
 
 
### Checkpoints
### command wget https://civitai.com/api/download/models/{modelVersionId} --content-disposition
https://civitai.com/models/133005/juggernaut-xl
https://civitai.com/models/125703/protovision-xl-high-fidelity-3d-photorealism-anime-hyperrealism-no-refiner-needed
https://civitai.com/models/120964/rundiffusion-xl
https://civitai.com/models/135366/inkpunk-xl
 
 
### Loras
https://civitai.com/models/120723/detailedeyesxl
https://civitai.com/models/122359/detail-tweaker-xl
 
## Install Extensions (you cannot install extensions through web UI when you run with --share flag. run without share flag)
./webui.sh  --xformers
### from your computer terminal
ssh -N -L 7860:127.0.0.1:7860 -i "SD-key.pem" ubuntu@ec2-13-50-99-183.eu-north-1.compute.amazonaws.com

## Controlnet
cd sd-webui-controlnet/
## https://huggingface.co/lllyasviel/ControlNet-v1-1/tree/main
wget https://huggingface.co/lllyasviel/sd_control_collection/blob/main/diffusers_xl_canny_mid.safetensors