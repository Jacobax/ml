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
*拉取源码*
```
git clone https://github.com/v2fly/v2ray-core.git
```
```
cd v2ray-core && go mod download
```
```
CGO_ENABLED=0 GOOS=linux GOARCH=s390x go build -o $HOME/生成文件名 -trimpath -ldflags "-s -w -buildid=" ./main
```
_生成文件名通常为v2ray，可自行命名，所生成文件在当前文件夹或root目录下_
