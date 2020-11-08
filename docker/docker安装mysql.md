## 拉取镜像
```sh
docker pull mysql:5.7
```


## 设置文件映射路径
```sh
mkdir -p /data/dockerdata/mysql/conf
mkdir -p /data/dockerdata/mysql/logs
mkdir -p /data/dockerdata/mysql/mysql
```
## 配置个人设置

```shell
cd /data/dockerdata/mysql/conf/
vi my.cnf
```
```
## my.cnf
[client]
default-character-set=utf8mb4
[mysql]
default-character-set=utf8mb4
[mysqld]
  #取消 group 严格模式
　sql-mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
　character-set-server=utf8mb4
```
## 执行运行docker 命令

```shell
docker run --restart always -p 3306:3306 --name mysql -v /data/dockerdata/mysql/conf/my.cnf:/etc/mysql/my.cnf -v /data/dockerdata/mysql/logs:/logs -v /data/dockerdata/mysql/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7
```
+ --restart always 设置docker 重启容器自动重启
+ -p 端口映射
+ --name mysq 设置容器名
+ -v 文件映射
+ -e MYSQL_ROOT_PASSWORD=root 设置mysql密码
+ -d 后台运行容器，并返回容器ID

## 进入容器

```
docker exec -it  mysql  /bin/bash
mysql -uroot -proot
```
