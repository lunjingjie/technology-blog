environment：CentOS 7.9（7.x）

#### 1.旧版本docker卸载

```shell
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine \
                  docker-ce
```

#### 2.安装docker

- 安装yum工具

```shell
yum install -y yum-utils \
           device-mapper-persistent-data \
           lvm2 --skip-broken
```

- 更新本地镜像源

```shell
# 设置docker镜像源
yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
    
sed -i 's/download.docker.com/mirrors.aliyun.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo

yum makecache fast
```

- 安装docker

```shell
yum install -y docker-ce
```

#### 3.启动docker

- 关闭防火墙（可选），避免各种端口出现访问问题

```shell
# 关闭
systemctl stop firewalld
# 禁止开机启动防火墙
systemctl disable firewalld
```

- 启动docker

```shell
systemctl start docker  # 启动docker服务
systemctl stop docker  # 停止docker服务
systemctl restart docker  # 重启docker服务
docker -v # 查看版本
```

- 配置镜像加速

```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://soxxp5r5.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

#### 4.安装docker-compose

- 安装

``` shell
# 安装
curl -L https://github.com/docker/compose/releases/download/1.23.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```

- 修改文件权限

```
# 修改权限
chmod +x /usr/local/bin/docker-compose
```

- Base自动补全命令

```shell
# 补全命令
curl -L https://raw.githubusercontent.com/docker/compose/1.29.1/contrib/completion/bash/docker-compose > /etc/bash_completion.d/docker-compose
```

#### 5.拉取mysql镜像

- 官网查看镜像

https://hub.docker.com/_/registry

- 拉取镜像

```shell
docker pull mysql
docker images # 查看镜像
```

- 运行镜像

```shell
docker run --name 容器名称 -e MYSQL_ROOT_PASSWORD=管理员密码 -d mysql:tag -p 3306:3306 # tag为版本号，若最新为latest，-p为映射端口

–name：指定容器名称
-p：指定端口映射
-d：让容器后台运行
```

- 进入容器

```shell
docker exec -it 容器名称 bash
---------------------------------------------------------
docker exec ：进入容器内部，执行一个命令
-it : 给当前进入的容器创建一个标准输入、输出终端，允许我们与容器交互
nacos-quick：要进入的容器的名称
bash：进入容器后执行的命令，bash是一个linux终端交互命令
```

