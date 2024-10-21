# Introduction

In my Homelab I have a Turing Pi 2 _(or 2.5 as it is officially called)_ with 4 nodes:

- 1x RPi4 CM4 8GB
- 2x Turing RK1 16GB
- 1x Turing RK1 32GB

# The board-management-controller (BMC)

This thing is great but at the same time kind of a pain in the ass.

By inserting a SD-card into the board, one can transfer image files onto the BMC and flash the nodes directly from those images.

Additionally, it allows for mounting the storage of the nodes on the BMC, that is if the board supports it _(currently this only worked for my CM4, I could not get it working on the RK1)_.

## Flashing a node

```shell
tpi flash -n X -l -i /mnt/sdcard/images/your-desired-image
# e.g.
tpi flash -n 2 -l -i /mnt/sdcard/images/ubuntu-24.04-preinstalled-server-arm64-turing-rk1.img
```

## Mounting storage of node

```shell
# replace X with node number, mount options: msd, normal
tpi advanced <msd|normal> -n X

# to mount
tpi advanced msd -n X # MSD stands for mass-storage-device (I think...)
# to reset
tpi advanced normal -n X
```

## Get a terminal on node

```shell
# picocom is your friend
picocom /dev/ttySx -b 115200 # Replace x with serial terminal of device
# Beware, the nodes are not ordered in terms of serial devices
# For ease of use, I setup these symbolic links
ln -s /dev/ttyS2 ttyNode1
ln -s /dev/ttyS1 ttyNode2
ln -s /dev/ttyS4 ttyNode3
ln -s /dev/ttyS5 ttyNode4
```

# The nodes

It is such a pain