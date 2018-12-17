---------------------Server环境准备-----------------------------
1.  准备ubuntu 64 位server系统（虚拟机or 其他）
2.  配置好网络(允许其访问互联网)；设置好本机时间；设置本机开放8080端口
3.  切换到root权限  sudo su
4.  依次执行 apt-get upgrade
                   apt-get update
                   apt-get install
5.   安装docker:
      apt-get install docker.io
      启动docker:
      service docker.io start
6.   安装 git
      apt-get install git

-------------------docker操作-------------------------------
7.   执行  git clone https://github.com/yanghdx/docker-discuz.git
      进入docker-discuz目录

8.   按照如下安装discuz
      （若图片不清晰，请到此处查看https://github.com/yanghdx/docker-discuz）