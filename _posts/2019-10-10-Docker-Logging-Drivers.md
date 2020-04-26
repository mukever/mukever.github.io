---
layout:     post
title:      Docker使用
subtitle:   Logging Drivers
date:       2019-10-10
author:     志祥
header-img: img/post-plant-gallery8.jpg
catalog: true
tags:
  - Docker
---

## Docker Logging Drivers 是什么？

存储和访问Container 的日志是管理容器的重要部分。Docker Logging Drivers 允许我们选择自己的日志实现来满足我们的特殊需求。

### 查看当前默认的Docker Logging Drivers

```bash
➜  ~ docker info|grep Logging
 Logging Driver: json-file
```

#### 修改当前Logging Drivers 默认配置。

在docker的官方文档中，有关于docker daemon 的简单介绍。

![]( https://tva1.sinaimg.cn/large/007S8ZIlgy1ge7bxuvb99j31fk0p6jy0.jpg)

你可以在这里找到关于docker[daemon链接]( https://docs.docker.com/engine/reference/commandline/dockerd/)



```bash
sudo vi /etc/docker/daemon.json
```

添加下面的内容

```json
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "15m"
  }
}
```

重启docker 服务


```bash
sudo systemctl restart docker
```

使用新的配置，覆盖系统默认的docker logging drivers 配置。启动docker容器

```bash
docker run --log-driver json-file --log-opt max-size=50m nginx
```



##### 在这里你可以找到[官方的配置文档](https://docs.docker.com/config/containers/logging/configure/)