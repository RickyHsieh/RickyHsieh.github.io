---
title: Docker學習筆記-docker如何執行容器?
description: 了解docker如何執行容器
date: 2023-11-19 18:49:00+0000
image:
categories:
    - Docker
---

## Docker 如何執行容器


### 1. 列出正在運行的container
`docker ps` 和 `docker container ls` 這兩個命令在Docker中的作用是相同的。他們都用於列出當前正在運行的容器。
```
docker container ls
```
```
docker ps
```

### 2. 列出container正在使用多少資源
即時顯示容器的正在使用多少系統資源，EX: CPU、記憶體、網路流量、磁碟空間
```
docker container stats
```