git仓库地址：https://github.com/nondanee/UnblockNeteaseMusic

本地教程：https://www.sevesum.com/118.html

服务器搭建：https://merlinblog.xyz/wiki/neteasemusic.html
- 注册nodejs
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt install -y nodejs git 
- 下载git仓库
git clone https://github.com/nondanee/UnblockNeteaseMusic.git
cd UnblockNeteaseMusic
- 运行js脚本
node app.js -p 8848
可以自己写个服务，用systemd工具启动

openwrt上可以搞个，加上ddns在家里或者在外面就都可以用了
