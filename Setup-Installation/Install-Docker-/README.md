# Install-Docker
Install Docker in Ubuntu 18.04

###### Update apt
```
$ sudo apt update
$ sudo apt upgrade
```

###### Install prerequiste packages

```
$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```

###### Add the Docker repositories 

```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" # q to quit
$ sudo apt update
```
###### Add Docker's official GPG key
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
###### Docker's official repo
```
$ sudo add-apt-repository "deb [arch=amd64] 
 > https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
 ```
 ###### Update and install Docker CE
```
$ sudo apt-get update
$ sudo apt-get install docker-ce
```
###### Check Docker version

```
$ docker version
or
$ docker -v
```
###### To remove the requirement of 'sudo' add user name to group
```
$ sudo usermod -aG docker Username
```
###### To login 
```
$ ssu - Username
```

# GPU Version

```

$ curl -sL https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$ curl -sL https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
$ sudo apt update
$ sudo apt install nvidia-docker2 -y
$ sudo pkill -SIGHUP dockerd
$ sudo docker run --runtime=nvidia --rm nvidia/cuda nvidia-smi

```


After installation of Docker

## Process 1:


######  Obtain the all-in-one image from Docker Hub
```
$ docker pull ufoym/deepo
```

 
###### Reboot server 

```
$ sudo reboot
```
###### Check
```
$ docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi
```

- If encountered following problems :

```
$ docker run --runtime=nvidia -it nvcr.io/nvidia/tlt-streamanalytics:v1.0_py2 /bin/bash

docker: Error response from daemon: Unknown runtime specified nvidia.
See 'docker run --help'.
```
- Try:

```
$ sudo pkill -SIGHUP dockerd
$ sudo apt install -y nvidia-docker2
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```

```
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.40/containers/json: dial unix /var/run/docker.sock: connect: permission denied

--- in terminal type:

$ sudo chmod 666 /var/run/docker.sock
```






## Process 2

###### Set GPC

```
$ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
```

###### Update apt
```
$ sudo apt-get update
```
###### Install nvidia-docker 
```
$ sudo apt-get install -y nvidia-docker2
$ sudo pkill -SIGHUP docker
```
###### Check
```
$ docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi
```


## Usages

```
# check 
$ docker --version
$ docker ps

# make a new container and mount current directory to docker 

$ docker run --name "test" --gpus all -v "${PWD}" -it ufoym/deepo bash

# start container;
$ docker start test
# attach contatiner:
$ docker attach test
```
- To mount the desire derectory:
```
# From ubuntu terminal
$  docker run --gpus all -v "${PWD}:/workspace" -it ufoym/deepo bash
---------------------------

$ docker run --gpus all -it -v "${PWD}:/docker(my desire folder in root)" -v /host/config:/config ufoym/deepo bash # mounting root 
# this will show something like this in terminal :
$ root@481e15b91d22:/docker 
```

or 

```
$ docker run --gpus all -it -v /host/data:/data -v /host/config:/config ufoym/deepo bash
```




## Check python libraries  after mounting 

e.g. Checking tensorflow , pytorch, opencv

```
$ root@481e15b91d22:/docker # python3

Python 3.6.9 (default, Apr 18 2020, 01:56:04) 
[GCC 8.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
>>> import tensorflow as tf
>>> tf.test.is_gpu_available()
.......

True

>>> tf.__version__
'2.2.0'
>>> import torch
>>> torch.__version__
'1.6.0.dev20200609+cu101'
>>> import cv2
>>> cv2.__version__
'4.3.0'
```


## To uninstall Docker 
```
# Check :
$ dpkg -l | grep -i docker
# Remove Docker:

$ sudo apt-get purge -y docker-engine docker docker.io docker-ce docker-ce-cli
$ sudo apt-get autoremove -y --purge docker-engine docker docker.io docker-ce  

# Remove image, container :
$ sudo rm -rf /var/lib/docker /etc/docker
$ sudo rm /etc/apparmor.d/docker
$ sudo groupdel docker
$ sudo rm -rf /var/run/docker.sock
```


## References 
* https://www.hostinger.com/tutorials/how-to-install-docker-on-ubuntu
* https://hub.docker.com/r/ufoym/deepo/
* https://github.com/NVIDIA/nvidia-docker/issues/838
* https://github.com/Laudarisd/deepo



