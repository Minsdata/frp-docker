[README](README.md) | [中文文档](README_zh.md)
<p align="left">
    <a href="https://github.com/minsdata/frp-docker/releases/latest" style="display: inline-block;">
        <img src="https://img.shields.io/github/release/minsdata/frp-docker.svg?style=for-the-badge&color=green" alt="Latest Release" width="150" height="32">
    </a>
</p>
<p align="center">
    <a href="https://hub.docker.com/u/minsdatadocker">
        <img src="https://cdn.iconscout.com/icon/free/png-256/docker-226091.png" alt="Docker Logo" width="150">
    </a>
</p>

<p align="center">
    <a href="https://hub.docker.com/r/minsdatadocker/frps">
        <img src="https://img.shields.io/badge/Docker%20Image-minsdatadocker%2Ffrps-blue?style=for-the-badge" alt="Docker Image" width="240" height="32">
    </a>
    <a href="https://hub.docker.com/r/minsdatadocker/frps">
        <img src="https://img.shields.io/docker/stars/minsdatadocker/frps.svg?style=for-the-badge" alt="Docker Stars" width="140" height="32">
    </a>
    <a href="https://hub.docker.com/r/minsdatadocker/frps">
        <img src="https://img.shields.io/docker/pulls/minsdatadocker/frps.svg?style=for-the-badge" alt="Docker Pulls" width="140" height="32">
    </a>
</p>

<p align="center">
    <a href="https://hub.docker.com/r/minsdatadocker/frpc">
        <img src="https://img.shields.io/badge/Docker%20Image-minsdatadocker%2Ffrpc-blue?style=for-the-badge" alt="Docker Image" width="240" height="32">
    </a>
    <a href="https://hub.docker.com/r/minsdatadocker/frpc">
        <img src="https://img.shields.io/docker/stars/minsdatadocker/frpc.svg?style=for-the-badge" alt="Docker Stars" width="140" height="32">
    </a>
    <a href="https://hub.docker.com/r/minsdatadocker/frpc">
        <img src="https://img.shields.io/docker/pulls/minsdatadocker/frpc.svg?style=for-the-badge" alt="Docker Pulls" width="140" height="32">
    </a>
</p>  
  
# frp-docker:  
此Frp docker 版本由 [fatedier/frp](https://github.com/fatedier/frp) 原生的最新版本源代码构建。  
  
Frp：一种快速反向代理，可帮助您将 NAT 或防火墙后面的本地服务器暴露给互联网。  
  
为了保持最新版本，镜像将每6小时自动对[fatedier/frp](https://github.com/fatedier/frp)源代码进行一次版本检查和更新。  
  
# Dockerhub:  
  
frps docker 版本镜像: [minsdatadocker/frps](https://hub.docker.com/r/minsdatadocker/frps)  
  
frpc docker 版本镜像: [minsdatadocker/frpc](https://hub.docker.com/r/minsdatadocker/frpc)  
  
此映像支持以下 系统/架构:  
linux/amd64  
linux/arm64  
linux/arm/v6  
linux/arm/v7  
linux/arm/v8   
linux/ppc64le  
linux/s390x  
  
# frps（服务端）  
**1.部署**  
**注意：请根据自己的网络配置去设置环境变量：“BIND_ADDR” “BIND_PORT” “TOKEN”**  
- **Docker Run**  
```
docker run -d \
  --name frps \
  --restart unless-stopped \
  -e BIND_ADDR=0.0.0.0 \
  -e BIND_PORT=7000 \
  -e TOKEN=YOURTOKEN \
  -v ~/frps.ini:/app/frps/frps.ini \
  minsdatadocker/frps:latest  
```
- **Docker-Compose**  
```
version: '3'
services:
  frps:
    image: minsdatadocker/frps:latest
    container_name: frps
    restart: unless-stopped
    environment: 
    - ENV BIND_ADDR=0.0.0.0
    - BIND_PORT=7000
    - TOKEN=YOURTOKEN
    volumes:
      - ~/frps.ini:/app/frps/frps.ini
```
**2.编辑配置文件 (frps.ini),**  
- **首次启动你可能需要使用环境变量，之后可以删除frps.ini文件中的环境变量，自行配置参数**  
**具体参数请参考 [README](https://github.com/fatedier/frp#readme)**  
- **示例**
```
# frps.ini
[common]
bind_addr = 0.0.0.0
bind_port = 7000
token = YOURTOKEN
```  
  
# frpc（客户端） 
**1.部署**  
**注意：请根据自己的网络配置去设置环境变量："SERVER_ADDR" "SERVER_PORT" "TOKEN"**  
- **Docker Run**  
```
docker run -d \
  --name frpc \
  --restart unless-stopped \
  -e SERVER_ADDR=172.17.0.1 \
  -e SERVER_PORT=7000 \
  -e TOKEN=YOURTOKEN \
  -v ~/frpc.ini:/app/frpc/frpc.ini \
  minsdatadocker/frpc:latest  
```
- **Docker-Compose**  
```
version: '3'
services:
  frpc:
    image: minsdatadocker/frpc:latest
    container_name: frpc
    restart: unless-stopped
    environment: 
    - SERVER_ADDR=172.17.0.1
    - SERVER_PORT=7000
    - TOKEN=YOURTOKEN
    volumes:
      - ~/frpc.ini:/app/frpc/frpc.ini
```
**2.Edit configuration file (frpc.ini),**  
- **首次启动你可能需要使用环境变量，之后可以删除frpc.ini文件中的环境变量，自行配置参数**  
**具体参数请参考 [README](https://github.com/fatedier/frp#readme)**  
- **示例**
```
# frpc.ini
[common]
server_addr = 172.17.0.1
server_port = 7000
token = YOURTOKEN


[ssh]
type = tcp
local_ip = 172.17.0.1
local_port = 22
remote_port = 6000
```
