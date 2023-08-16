# frp-docker:
Frp docker version bulit from fatedier/frp latest relase (100% oringal source code used from [fatedier/frp](https://github.com/fatedier/frp)).

Frp: A fast reverse proxy to help you expose a local server behind a NAT or firewall to the internet.

In order to keep the latest version, the image will be version checked and updated automatically every 4 hours from fatedier/frp original release.  

# Dockerhub:

frps docker image: [minsdatadocker/frps](https://hub.docker.com/r/minsdatadocker/frps)

frpc docker image: [minsdatadocker/frpc](https://hub.docker.com/r/minsdatadocker/frpc)

This image is supported for OS/ARCH below:  
linux/amd64  
linux/arm64  
linux/arm/v6  
linux/arm/v7  
linux/arm/v8  
linux/386  
linux/ppc64le  
linux/s390x  

# frps 
**1.Deploy**  
**Docker Run**  
```
docker run -d \
  --name frps \
  --restart unless-stopped \
  -v ~/frps.ini:/app/frps/frps_config/frps.ini \
  minsdatadocker/frps:latest  
```
**Docker-Compose**  
```
version: '3'
services:
  frps:
    image: minsdatadocker/frps:latest
    container_name: frps
    restart: unless-stopped
    volumes:
      - ~/frps.ini:/app/frps/frps_config/frps.ini
```
**2.Edit configuration file (frps.ini),**
**Please refer to [README](https://github.com/fatedier/frp#readme)**  
**Example**
```
# frps.ini
[common]
bind_port = 7000
```  
  
# frpc
**1.Deploy**  
**Docker Run**  
```
docker run -d \
  --name frpc \
  --restart unless-stopped \
  -v ~/frpc.ini:/app/frpc/frpc_config/frpc.ini \
  minsdatadocker/frpc:latest  
```
**Docker-Compose**  
```
version: '3'
services:
  frpc:
    image: minsdatadocker/frpc:latest
    container_name: frpc
    restart: unless-stopped
    volumes:
      - ~/frpc.ini:/app/frpc/frpc_config/frpc.ini
```
**2.Edit configuration file (frpc.ini),**
**Please refer to [README](https://github.com/fatedier/frp#readme)**  
**Example**
```
# frpc.ini
[common]
server_addr = x.x.x.x
server_port = 7000

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000
```
