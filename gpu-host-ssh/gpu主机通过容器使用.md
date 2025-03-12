# 通过docker 使用gpu机器

## 快速使用
```shell
docker run -d -p 8822:22 --gpus all --privileged --name gpu-docker-host ghcr.io/nxt5656/devops-docker-images:gpu-docker-host
```