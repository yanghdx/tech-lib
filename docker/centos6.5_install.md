# centos6.5升级内核并安装docker

### 查看当前版本
- uname -r
- yum -y update nss (更新nss版本，解决curl的https报错问题)

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