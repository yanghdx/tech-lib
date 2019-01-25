# Centos6/7升级安装git

### 第一步：卸载旧的git版本
- yum remove git

### 第二步：下载git
- wget --no-check-certificatehttps://www.kernel.org/pub/software/scm/git/git-2.8.4.tar.gz

### 第三步：解压
- tar -zxf git-2.8.4.tar.gz

### 第四步：安装依赖包
- yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
- yum install  gcc perl-ExtUtils-MakeMaker

### 第五步：编译安装
- cd git-2.8.4
- mkdir -p  /usr/local/git
- make prefix=/usr/local/git all
- make prefix=/usr/local/git install 

### 第六步：添加环境变量
- vim /etc/profile
- export PATH=$PATH:/usr/local/git/bin

### 第七步：使配置生效
- source /etc/profile
- git --version