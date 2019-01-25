# centos6.5升级内核并安装docker

- centos6.5默认是2.6内核，不能安装docker，需要先升级内核

## 1. 升级内核

### 查看当前版本
- uname -r
- yum -y update nss (更新nss版本，解决curl的https报错问题)
- yum install -y device-mapper-libs libudev （更新依赖库）

### 安装elrepo yum 源（提供内核更新、硬件驱动等软件源支持）
- rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
- rpm -Uvh http://www.elrepo.org/elrepo-release-6-6.el6.elrepo.noarch.rpm
- 安装elrepo的时候发现 上面链接 出现404，可以用一下链接
- rpm -Uvh http://www.elrepo.org/elrepo-release-6-8.el6.elrepo.noarch.rpm

### 内核升级
- yum --enablerepo=elrepo-kernel -y install kernel-lt （kernel-ml）

### 引导文件修改（grub.conf）
- vim /etc/grub.conf： 将 default 设置为 0 ，default=0

### 重启
- reboot

### 注意：kvm环境下可能会有scsi_mod.scan找不到的问题，这时使用旧版内核进入系统，执行如下操作：
- echo 'add_drivers+="virtio_blk"' >/etc/dracut.conf.d/force-vitio_blk-to-ensure-boot.conf
- cd /boot
- dracut -f /boot/initramfs-4.6.0-1.el6.elrepo.x86_64.img 4.6.0-1.el6.elrepo.x86_64 （注意：这里的文件为你的内核文件）
- reboot
- 如有问题继续google


## 2. 安装docker
- yum install epel-release
- yum install docker-io
- service docker start