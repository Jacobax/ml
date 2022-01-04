# ml-model
免流模板  
使用请自行修改port、id和path，其中path为广东电信免流路径  
---
**后台服务运行**
```
vi /etc/systemd/system/服务名称.service
```
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
_服务名和执行文件名通常为v2ray以便辨识，有些机器安装v2ray会被封号，改名简单规避一下，作用随缘_
