### 解决node-sass安装问题

解决办法：
主要是windows平台缺少编译环境，（注意要使用管理员权限的命令行）
- 1、先运行： npm install -g node-gyp
- 2、然后运行：运行 npm install --global --production windows-build-tools 可以自动安装跨平台的编译器：gym注：第二句执行下载好msi文件卡着不懂不安装 ， 手动去对应的目录底下安装一下 在执行一边。
- 3、npm install node-sass -g（若失败先执行npm uninstall node-sass -g）