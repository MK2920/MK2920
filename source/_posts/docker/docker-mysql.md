---
title: docker 之 mysql 安装部署 
date: 2022-08-29 11:49:00
category: 
- docker
- mysql
tags: 
- docker
- mysql
---

## 搜索安装 mysql 

- 搜索 mysql
  ```shell
  docker search mysql
  ```
  也可以访问 [https://hub.docker.com/_/mysql/tags](https://hub.docker.com/_/mysql/tags) Mysql 镜像库

- 拉取
  ```shell
  docker pull mysql:latest
  ```

- 查看镜像
  ```shell
  docker images
  ```

- 启动容器
  ```shell
  docker run --name mysql-name -p 3306:3306 -v /opt/docker/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=password -d mysql:5.7
  ```
  - `-p 3306:3306` 将容器的 3306 端口映射到主机的 3306 端口
  - `-v /opt/docker/mysql/conf:/etc/mysql/conf.d` 将主机 /opt/docker/mysql/conf 目录挂载到容器的 /etc/mysql/conf.d
  - `-e MYSQL_ROOT_PASSWORD=123456` 初始化 root 密码
  - `-d` 后台运行容器，并返回容器ID
  - `mysql:5.7` name:tag

## 配置文件

- 进入容器内部
```shell
docker exec -i -t mysql-name bin/bash
```
其中 `91a0` 是容器ID 的前四位 , 容器ID 太长 , 无需全部写上

- 添加用户 , `admin` 是账号 , `25s14q` 是密码
```shell
rabbitmqctl add_user admin 25s14q
```

- 设置用户权限 , 赋予 `admin` 用户所有权限
```shell
rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"
```

- 设置用户角色 , 赋予 `admin` 用户 `administrator` 角色
```shell
rabbitmqctl set_user_tags admin administrator
```

- 查看用户设置
```shell
rabbitmqctl list_users
```
