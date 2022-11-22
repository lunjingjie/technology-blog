### 环境：centos 7.x

1.查看虚拟机ip

```shell
ifconfig
```

2.安装docker

3.安装gitlab

4.安装gitlab-runner

5.配置gitlab-runner

6.编写gitlab-ci.yml文件执行自动化部署步骤



### 相关问题：

1.当虚拟机ip改变时，gitlab的clone地址没有变化

如虚拟机ip地址为192.168.119.141，而gitlab的clone地址为192.168.119.129

##### 解决方法

- 修改gitlab配置文件gitlab.yml

```shell
docker exec -it gitlab bash # 进入gitlab容器
vi /opt/gitlab/embedded/service/gitlab-rails/config/gitlab.yml # 修改配置文件，把host修改为当前ip
vi /etc/gitlab/gitlab.rb # 修改gitlab.rb，把external_url修改为当前ip
docker restart gitlab # 重启gitlab服务
docker ps # 查看当前gitlab服务是否启动完成
```





