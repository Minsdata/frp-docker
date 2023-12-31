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
Frp docker version bulit from  [fatedier/frp](https://github.com/fatedier/frp) oringal source code latest relase.

Frp: A fast reverse proxy to help you expose a local server behind a NAT or firewall to the internet.

In order to keep the latest version, the image will be version checked and updated automatically every 24 hours from  [fatedier/frp](https://github.com/fatedier/frp) original release.  

# Dockerhub:

frps docker image: [minsdatadocker/frps](https://hub.docker.com/r/minsdatadocker/frps)

frpc docker image: [minsdatadocker/frpc](https://hub.docker.com/r/minsdatadocker/frpc)

This image is supported for OS/ARCH below:  
linux/amd64  
linux/arm64  
linux/arm/v6  
linux/arm/v7  
linux/arm/v8   
linux/ppc64le  
linux/s390x  

# frps 
**1.Deploy**  
**Note: Please configure environment variables according to your own network configuration:**  
--**BIND_ADDR = the ip address of your server**  
--**BIND_PORT = the port that your server uses frp service**  
--**TOKEN = the secret token for frp service**  
- **Docker Run (Example)**  
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
- **Docker-Compose (Example)**  
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
**2.Edit configuration file (frps.ini),**  
- **You may need to use environment variables for the first startup, and then you can delete the environment variables in the frps.ini file and configure them yourself**  
**Please refer to [README](https://github.com/fatedier/frp#readme)**  
- **Example**
```
# frps.ini
[common]
bind_addr = 0.0.0.0
bind_port = 7000
token = YOURTOKEN
```  
  
# frpc
**1.Deploy**  
**Note: Please configure environment variables according to your own network configuration :**  
--**SERVER_ADDR = the ip address of your server (frps)**  
--**SERVER_PORT = the port that your server uses frp service (frps)**  
--**TOKEN = the secret token for frp service**  
- **Docker Run (Example)**  
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
- **Docker-Compose (Example)**  
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
- **You may need to use environment variables for the first startup, and then you can delete the environment variables in the frpc.ini file and configure them yourself**  
**Please refer to [README](https://github.com/fatedier/frp#readme)**  
- **Example**
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
