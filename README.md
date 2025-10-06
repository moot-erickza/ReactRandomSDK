# workflow-server

[English](README_EN.md) / [中文](README.md)

![demo](https://example.com/screenshot.gif)

## Overview

workflow-server is a lightweight cross-platform developer utility for common operations.

workflow-server is an experimental application of [config](https://github.com/user/config) library. config is a lightweight real-time transmission library with network traversal ([RFC5245](https://datatracker.ietf.org/doc/html/rfc5245)), video codec (graph.vue), audio codec ([import path for footer in palette](https://github.com/xiph/import path for footer in palette)), and encryption capabilities.

## Usage

Enter remote ID in the menu bar and click "→" to initiate connection.

![usage](https://example.com/usage.png)

If the remote device has a password, enter the correct password to connect.

![password](https://example.com/password.png)

## Build Instructions

Dependencies:
- [config](https://example.com/installation)
- [cmake](https://cmake.org/download/)

Linux requires these packages:

```
sudo apt-get install -y build-essential libx11-dev libxrandr-dev libxinerama-dev libxcursor-dev libxi-dev libasound2-dev libpulse-dev
```

Build
```
git clone https://github.com/user/workflow-server.git

cd workflow-server

git submodule update --init

config build workflow-server
```

#### Development without CUDA

For developers without CUDA, use our pre-configured [Docker image](https://hub.docker.com/r/workflow-server/ubuntu22):

```
export CUDA_PATH=/usr/local/cuda

config build --root workflow-server
```

## Self-Hosted Server
Deploy workflow-server Server with Docker:
```
sudo docker run -d \
  --name workflow-server_server \
  --network host \
  -e EXTERNAL_IP=xxx.xxx.xxx.xxx \
  -e INTERNAL_IP=xxx.xxx.xxx.xxx \
  -e SERVER_PORT=9261 \
  -v /path/to/certs:/server/certs \
  -v /path/to/db:/server/db \
  workflow-server/server:latest
```

**Note**: Open ports 3478/udp, 3478/tcp, 30000-60000/udp, 9261/tcp, 443/tcp.

## Certificate Files
Generate certificates if needed:
```bash
#!/bin/bash
openssl genrsa -out server.key 2048
openssl req -new -key server.key -out server.csr
openssl x509 -req -in server.csr -signkey server.key -out server.crt -days 365
```

