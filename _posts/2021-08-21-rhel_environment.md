---
layout: post
title:  "Deploy the Red Hat Certification Environment"
date:   2021-08-21 00:00:00
categories: post computer linux kvm
---

这篇文章将会详细描述如何部署RHCSA/RHCE(基于RHel 8)环境，以及解决AMD CPU出现的kvm/qemu虚拟机无法正常启动的问题。

<!--more-->

# 安装VMWare Workstation 16

安装过程省略，注意安装“增强型键盘驱动程序”。

# 新建RHel 8虚拟机

左上角单击**文件**，选择**新建虚拟机**或者按**Ctrl+N**以新建虚拟机。

![](http://icing.fun/img/post/2021/08/21/1.jpg)

选择**自定义**，单击**下一步**。

![](http://icing.fun/img/post/2021/08/21/2.jpg)

硬件兼容性不作修改，保持**Workstation 16**。

![](http://icing.fun/img/post/2021/08/21/3.jpg)

选择**稍后安装操作系统**，单击**下一步**。

![](http://icing.fun/img/post/2021/08/21/4.jpg)

选择**Linux**，版本**Red Hat Enterprise Linux 8 64位**。

![](http://icing.fun/img/post/2021/08/21/5.jpg)

虚拟机名称可以随便填一个，别忘了是**RHCSA**还是**RHCE**就好。

![](http://icing.fun/img/post/2021/08/21/6.jpg)

**处理器数量**选择**4**，**每个处理器的内核数量**保持不变（默认为1）。

*注：在VMWare vSphere ESXi中**处理器数量**应该对应的是**虚拟 CPU (vCPU)
总数**，即我们日常所说的**物理CPU个数(Socket)**。**每个处理器的内核数量**对应**Cores per Socket**即物理机上CPU的线程数。*

![](http://icing.fun/img/post/2021/08/21/7.jpg)

虚拟机的内存分配**12288MB**。

![](http://icing.fun/img/post/2021/08/21/8.jpg)

**网络类型**使用默认设置（NAT网络地址转换协议）。

![](http://icing.fun/img/post/2021/08/21/9.jpg)

**I/O控制器**使用默认设置（LSI Logic）。

![](http://icing.fun/img/post/2021/08/21/10.jpg)

**虚拟磁盘类型**使用默认设置（NVMe）。

![](http://icing.fun/img/post/2021/08/21/11.jpg)

**选择磁盘**中选择**创建新虚拟磁盘**。单击**下一步**。

![](http://icing.fun/img/post/2021/08/21/12.jpg)

**最大磁盘大小**填入**100**，选择**将虚拟磁盘存储为单个文件**。

![](http://icing.fun/img/post/2021/08/21/13.jpg)

磁盘文件名可以自定义。

![](http://icing.fun/img/post/2021/08/21/14.jpg)

单击**完成**。

![](http://icing.fun/img/post/2021/08/21/15.jpg)

在主界面下选中刚刚创建好的虚拟机，单击**编辑虚拟机设置**。

![](http://icing.fun/img/post/2021/08/21/16.jpg)

在弹出的设置框中单击最下面的**添加**。

![](http://icing.fun/img/post/2021/08/21/17.jpg)

选择**硬盘**。单击**下一步**。

![](http://icing.fun/img/post/2021/08/21/18.jpg)

**磁盘类型**同样使用**NVMe**。

![](http://icing.fun/img/post/2021/08/21/19.jpg)

选择**使用现有的虚拟磁盘**，单击**下一步**。

![](http://icing.fun/img/post/2021/08/21/20.jpg)

单击**浏览**。

![](http://icing.fun/img/post/2021/08/21/21.jpg)

在弹出的资源管理器中选择下载好的vmdk文件。单击**打开**。

![](http://icing.fun/img/post/2021/08/21/22.jpg)

单击**完成**。

![](http://icing.fun/img/post/2021/08/21/23.jpg)

选择**处理器**，勾选**虚拟化 Intel VT-x/EPT 或 AMD-V/RVI**。

![](http://icing.fun/img/post/2021/08/21/24.jpg)

选择**显示器**，**取消**勾选**加速3D图形**。

![](http://icing.fun/img/post/2021/08/21/25.jpg)

选择**CD/DVD(SATA)**，选择**使用ISO映像文件**，单击**浏览**。

![](http://icing.fun/img/post/2021/08/21/26.jpg)

Intel CPU选择**RHEL8-setup-20210129更新.iso**，AMD CPU选择**RHEL8-setup-20210819更新.iso**

![](http://icing.fun/img/post/2021/08/21/27.jpg)

**设备状态**勾选**启动时连接**。

![](http://icing.fun/img/post/2021/08/21/28.jpg)

单击**确认**。

![](http://icing.fun/img/post/2021/08/21/29.jpg)

选择**开启此虚拟机**。

![](http://icing.fun/img/post/2021/08/21/30.jpg)

在虚拟机界面，`boot:`后面输入需要的环境。然后坐和放宽。

![](http://icing.fun/img/post/2021/08/21/31.jpg)

稍等一会儿就会出现一个红色的提示**Invalid timezone**，此时单击**Time & Date**。

![](http://icing.fun/img/post/2021/08/21/32.jpg)

时区选择上海。单击**Done**.

![](http://icing.fun/img/post/2021/08/21/33.jpg)

单击**Begin Installation**，坐和放宽。

![](http://icing.fun/img/post/2021/08/21/34.jpg)
![](http://icing.fun/img/post/2021/08/21/35.jpg)

等到出现**Reboot**的时候，单击**Reboot**重启虚拟机。

![](http://icing.fun/img/post/2021/08/21/36.jpg)

在用户选择页面，单击**Not listed?**。

![](http://icing.fun/img/post/2021/08/21/37.jpg)

Username为**root**，Password为**Asimov**。

![](http://icing.fun/img/post/2021/08/21/38.jpg)
![](http://icing.fun/img/post/2021/08/21/39.jpg)

然后进入RHel 8的GNOME桌面。单击左上角的**Activities**， 选择**Terminal**。

![](http://icing.fun/img/post/2021/08/21/40.jpg)

输入`virt-manager`，弹出KVM图形化控制台。

![](http://icing.fun/img/post/2021/08/21/41.jpg)

输入`rht-vmctl fullreset all`，在对话栏中输入`y`并回车。

*注：如果是Intel CPU，应该会显示成功；如果是AMD CPU，会像下图一样显示错误。*

![](http://icing.fun/img/post/2021/08/21/42.jpg)

AMD CPU的用户需要在终端中输入：

```shell
sudo tee /etc/modprobe.d/qemu-system-x86.conf << EOF
options kvm ignore_msrs=1
EOF
```

*注：此命令行是当模块参数 ignore_msrs 设置为1时，未知 MSR 读取将返回0，并且 MSR 写入将被丢弃。同时在这两种情况下会向dmesg打印一条消息，以告知用户有关信息。*

![](http://icing.fun/img/post/2021/08/21/43.jpg)

`sudo reboot`重启虚拟机。

![](http://icing.fun/img/post/2021/08/21/44.jpg)

重启之后，再次输入`rht-vmctl fullreset all`，在对话栏中输入`y`并回车。就可以看到成功了。

![](http://icing.fun/img/post/2021/08/21/45.jpg)

