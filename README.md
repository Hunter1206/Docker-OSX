# Docker-OSX

![Running mac osx in a docker container](/running-mac-inside-docker-qemu.png?raw=true "OSX KVM DOCKER")

Run Mac in a Docker container! Run near native OSX-KVM in Docker! X11 Forwarding!

Author: Sick.Codes https://sick.codes/

Credits: OSX-KVM project among many others: https://github.com/kholia/OSX-KVM/blob/master/CREDITS.md

```
git clone https://github.com/sickcodes/Docker-OSX.git

cd Docker-OSX

docker build -t docker-osx .

docker run --privileged -v /tmp/.X11-unix:/tmp/.X11-unix docker-osx

# press ctrl G if your mouse gets stuck

```

# Start the same container later (persistent disk)
```
# look at it
docker ps --all --filter "ancestor=docker-osx"

# boot my old one
docker start $(docker ps -q --all --filter "ancestor=docker-osx")
```

# Additional Boot Instructions

```

# Boot the macOS Base System

# Click Disk Utility

# Erase the biggest disk

# Partition that disk and subtract 1GB and press Apply

# Click Reinstall macOS

```

# Backup the disk

your image will be stored in:

/var/lib/docker/overlay2/...../arch/OSX-KVM/home/arch/OSX-KVM/mac_hdd_ng.img
```
# find your container's root folder

docker inspect $(docker ps -q --all --filter "ancestor=docker-osx") | grep UpperDir

# In the folder from the above command, your image is inside ./home/arch/OSX-KVM/mac_hdd_ng.img

# then sudo cp it somewhere. Don't do it while the container is running tho, it bugs out.

```


# Wipe old images

```

# WARNING deletes all old images, but saves disk space if you make too many containers

docker system prune --all
docker image prune --all

```


# Instant OSX-KVM in a BOX!
This Dockerfile automates the installation of OSX-KVM inside a docker container.

It will build a 32GB Mojave Disk.

You can change the size and version using build arguments (see below).

This file builds on top of the work done by Dhiru Kholia and many others on the OSX-KVM project.


# Custom Build
```

docker build -t docker-osx:latest \
--build-arg VERSION=10.14.6 \
--build-arg SIZE=200G

docker run --privileged -v /tmp/.X11-unix:/tmp/.X11-unix docker-osx:latest

```

## Todo:
```
# persistent disk with least amount of pre-build errands.
```