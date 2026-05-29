# BPI-RT2 OpenWrt Build Guide

## 🛠 Prerequisites

### 1. Build Environment
This project requires a Linux environment for cross-compilation.
* **Supported OS:** Ubuntu 22.04 LTS

### 2. Required Dependencies
You will need to install the essential compilation tools and libraries. The exact package names may vary slightly depending on your Linux distribution. 

Run the following command to install all necessary dependencies on Ubuntu 22.04:

```
sudo apt update
sudo apt install -y \
  build-essential clang flex bison gawk gettext git \
  libncurses5-dev libssl-dev python3 python3-distutils python3-setuptools \
  rsync unzip zlib1g-dev file wget curl quilt subversion swig time xsltproc
```

## Quickstart
Follow these steps to configure and build the firmware:

1. Load Target Configuration
Initialize the environment with the specific configuration for the BPI-RT2 board:

```
make preconfig_BPI-RT2
```

2. Update Package Feeds
Obtain the latest package definitions from feeds.conf / feeds.conf.default:

```
./scripts/feeds update -a
```

3. Install Package Feeds
Install symlinks for all obtained packages into the package/feeds/ directory:

```
./scripts/feeds install -a
```

4. Customize Firmware (Optional)
Select your preferred configuration for the toolchain, target system, and firmware packages:

```
make menuconfig
```

5. Customize Kernel (Optional)
Select your preferred configuration for Linux kernel drivers, filesystem support, and specific kernel features:

```
make kernel_menuconfig
```

6. Build the Firmware
Start the compilation process. This will download all necessary sources, build the cross-compile toolchain, and then cross-compile the GNU/Linux kernel and all chosen applications for your target system:

```
make
```

💡 Pro-Tip for Compilation: > * To significantly speed up the build process, you can use multiple threads by appending -j$(nproc) (e.g., make -j8).

If the build fails, append V=s to output detailed build logs for debugging (e.g., make -j1 V=s).