# git仓库地址：https://github.com/nondanee/UnblockNeteaseMusic

### 本地教程：https://www.sevesum.com/118.html
```
cd D:\myproject\git_Repositories\UnblockNeteaseMusic
node app.js -p 32777 	//powershell中执行
node app.js -p 32777	//gitbash中执行，加个&后台执行也可以
```
退出终端后本地的监听就结束，功能失效。
感觉应该也可以用资源管理器运行
``` "C:\Program Files\nodejs\node.exe" D:\myproject\git_Repositories\UnblockNeteaseMusic\app.js" -p 32777 ```
![image](https://user-images.githubusercontent.com/18462281/113167190-0f92b080-9276-11eb-8dc2-90a89d8eb785.png)
![image](https://user-images.githubusercontent.com/18462281/113167244-1caf9f80-9276-11eb-8f2a-1f93c806ec7d.png)

为什么程序一执行命令框消失，后台什么程序都没有

给IOS使用有点不一样，使用该命令```node app.js -e https://music.163.com -p 32777:32778```
参考：[https://github.com/nondanee/UnblockNeteaseMusic/issues/368](https://github.com/nondanee/UnblockNeteaseMusic/issues/368)
可以在本地起两个线程
```
node app.js -p 32779 //给PC用
node app.js -e https://music.163.com -p 32777:32778  //给IOS设备用
```

eg： 可以加上验证的参数  -t username:password

### 服务器搭建 ：https://merlinblog.xyz/wiki/neteasemusic.html
服务器不建议搭建给本地用，服务器是最不推荐的方法了。
```
#注册nodejs
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt install -y nodejs git 
#下载git仓库
git clone https://github.com/nondanee/UnblockNeteaseMusic.git
cd UnblockNeteaseMusic
#运行js脚本
node app.js -p 8848
```
可以自己写个服务，用systemd工具启动，只给IOS用电话就一个服务，还要给PC用就再起一个服务
```
vi /etc/systemd/system/UnblockNeteaseMusic.service

#文件中写入以下内容
[Unit]
After=network-online.target

[Service]
ExecStart=/usr/bin/node /root/UnblockNeteaseMusic/app.js -e https://music.163.com -p 32777:32778
Restart=1


[Install]
WantedBy=multi-user.target

#主要就是ExecStart的这个命令
systemctl daemon-reload
systemctl start  UnblockNeteaseMusic

vi /etc/systemd/system/UnblockNeteaseMusicPC.service

#文件中写入以下内容
[Unit]
After=UnblockNeteaseMusic.service

[Service]
ExecStart=/usr/bin/node /root/UnblockNeteaseMusic/app.js -p 32779
Restart=1


[Install]
WantedBy=multi-user.target

#这个js挺稳定的一般不会遇到崩溃的时候吧，以防服务器抽风 设置个Restart
#如果是要更新git仓库，再启动该服务
netstat -lpt
kill -9 XXX
#kill掉对应的进程，重启服务即可

```

### openwrt上可以搞个，加上ddns在家里或者在外面就都可以用了
