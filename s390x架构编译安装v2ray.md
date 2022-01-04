*安装go*
```
wget https://go.dev/dl/go1.17.5.linux-s390x.tar.gz -O - | tar -xz -C /usr/local/
```
```
vi ~/.profile
```
```
export PATH=$PATH:/usr/local/go/bin
export PATH=$PATH:$HOME/.cargo/bin
export GOROOT=/usr/local/go
export GOBIN=$GOROOT/bin
export PATH=$PATH:$GOBIN
```
```
source ~/.profile
```
```
go version
```
*编译v2ray*
拉取源码
```
git clone https://github.com/v2fly/v2ray-core.git
```
```
cd v2ray-core && go mod download
```
编译
```
CGO_ENABLED=0 GOOS=linux GOARCH=s390x go build -o $HOME/生成文件名 -trimpath -ldflags "-s -w -buildid=" ./main
```
_生成文件名通常为v2ray，可自行命名，所生成文件在当前文件夹或root目录下_  

移动至Linux运行目录
```
mv 所生成文件名 /usr/bin/
```
*v2ray配置*
```
mkdir /etc/配置文件夹名
```
```
vi /etc/配置文件夹名/config.json
```
填入改好后的配置模板并保存  
---
**后台服务运行**  
```
vi /etc/systemd/system/服务名称.service
```
填入并保存
```
[Unit]
Description=服务名称 Service
After=network.target nss-lookup.target

[Service]
User=nobody
CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_BIND_SERVICE
AmbientCapabilities=CAP_NET_ADMIN CAP_NET_BIND_SERVICE
NoNewPrivileges=true
ExecStart=/usr/bin/执行文件名 run -config /etc/执行文件名/config.json
Restart=on-failure
RestartPreventExitStatus=23

[Install]
WantedBy=multi-user.target
```
重载systemctl服务
```
systemctl daemon-reload
```
运行
```
systemctl start 执行文件名
```
开机自启
```
systemctl enable 执行文件名
```
查看运行状态
```
systemctl status 执行文件名
```
_即前面编译生成的文件_  
**注意执行文件路径及配置文件路径与所添加服务内容必须一致**
**以上所有待定文件名及文件夹名通常为v2ray，可自行命名**
