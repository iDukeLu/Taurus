# Docker CE 安装、卸载及启动停止

## 概述
Docker CE 是 Docker 公司发布的开源版 Docker 引擎，本文主要简单记录 CentOS 上 Docker CE 的安装、卸载及启动停止

## 前提条件
- 系统版本：CentOS 7 维护版本、不支持存档版本
- 必须开启 [centos-extras](https://wiki.centos.org/zh/AdditionalResources/Repositories) 附加软件库（默认：开启）
- 推荐使用 [overlay2](https://zh.wikipedia.org/zh-hans/OverlayFS) 文件存储驱动

> ps：overlay2 存储驱动配置可参考：[Docker overlayfs 存储驱动配置](https://docs.docker.com/storage/storagedriver/overlayfs-driver)

## 卸载老版本 Docker CE
如果有安装老版本的 Docker，可能会影响到当前版本到安装，故我们需先卸载老版本的 Docker 及其依赖

```
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

## 一、安装 Docker CE
官方提供了三种安装方式：
1. 设置 Docker 的 yum 源，通过 yum 进行安装
2. 下载 RPM 包，手动安装
3. 测试和开发环境下，可以用一些脚本安装

这里我们采用比较简单的第一种方式用 yum 进行安装
### 1. 设置存储库（首次安装时）
在新主机上首次安装 Docker CE 之前，需要设置 Docker 存储库。之后，您可以从存储库安装和更新 Docker。


    ```
    # 安装相关依赖
    sudo yum install -y yum-utils \
      device-mapper-persistent-data \
      lvm2
    
    # 设置稳定存储库
    sudo yum-config-manager \
             --add-repo \
             https://download.docker.com/linux/centos/docker-ce.repo
    ```

### 2. 安装 Docker CE
```
sudo yum install docker-ce docker-ce-cli containerd.io
```

## 二、卸载 Docker CE

```
# 卸载 Docker 包
sudo yum remove -y docker-ce

# 删除所有镜像、容器、数据卷或定制配置文件
sudo rm -rf /var/lib/docker
```

## 三、启动、重启、停止
### 1. 启动 Docker
```
systemctl start docker 或 service docker start
```

### 2. 重启 Docker
```
systemctl restart docker 或 service docker restart
```

### 3. 关闭 Docker
```
systemctl stop docker 或 service docker stop
```

### 4. 开机自启
```
systemctl enable docker
```
### 5. 重新加载配置文件
```
systemctl daemon-reload
```

---

参考：[Docker 产品手册/CentOS 安装](https://docs.docker.com/install/linux/docker-ce/centos)