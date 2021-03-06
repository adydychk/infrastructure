# Packages description needed for building Intel® Media SDK
The prupose of this guide is to clarify why Intel® Media SDK need specific packages and the dependencies of packages.

### Packages from Intel® Media Server Studio
OpenCL™
```bash
intel-opencl-xxx-xxx.x86_64.rpm
intel-opencl-cpu-xxx-.x86_64.rpm
intel-opencl-devel-xxx-xxx.x86_64.rpm
```
Intel® Media SDK can be built without OpenCL™ packages but you will get the product without some features.  
How to build without OpenCL™? - Simply don`t install these packages on your system. Build scripts will automatically generate needed make files.

LibVA
```bash
libva-xxx-xxx.el7.centos.x86_64.rpm
libva-devel-xxx-xxx.el7.centos.x86_64.rpm   # Needed for headers in /usr/include/va
```

[LibDRM](https://01.org/linuxgraphics/community/libdrm)  
It is the cross-driver middleware which allows user-space applications to communicate with the Kernel by the means of the DRI protocol.  
**LibDRM is dependency of LibVA.**
```bash
libdrm-xxx-xxx.el7.centos.x86_64.rpm
libdrm-devel-xxx-xxx.el7.centos.x86_64.rpm
```
LibDRM may be from OS repositories but it is not recommended! LibVA can use some features of LibDRM which can absent in the version from OS repositories.  
In case of CentOS 7.3:  
It already has `libdrm` - so it should be removed. In CentOS 7.3 `libdrm` is a dependency of `plymouth`. Uninstalling of `plymouth` should not damage your system if you don`t use GUI.


### System`s packages
Here is a list of recommended packages
```bash
sudo yum groupinstall "Development Tools"
sudo yum install cmake git
sudo yum install libX11 libXext libXfixes libGL libGL-devel libX11-devel 
```
Purpose of these packages:  
`Development Tools` are mainly needed for compilers (such as gcc, g++) and other things which are useful for building the product.  

`cmake` and `git` are needed only on pre-build stage.  

`libX11 libXext libXfixes libGL libGL-devel libX11-devel` all these packages are needed while building the product.


### Tip
Here is full list of needed packages (most of them are installed automatically as dependencies of anothers):
```bash
sudo yum groupinstall "Development Tools"
sudo yum install cmake autogen autoconf automake git
sudo yum install libX11 libX11-devel libXext libXext-devel libXfixes libXfixes-devel mesa-dri-drivers libGL libGL-devel numactl-devel numad
```
