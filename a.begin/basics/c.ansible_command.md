# Ansible用命令管理主机

Ansible提供了一个命令行工具，在官方文档中起给命令行起了一个名字叫Ad-Hoc Commands。

ansible命令的格式是：

```shell
ansible <host-pattern> [options]
```

`ansible命令功能有哪些`

先不用深纠命令的语法，讲完module那节，就可以理解语法。先从感官上，通过下面的命令认识下ansible的命令行都可以做什么。

#### 检查ansible安装环境

检查所有的server，是否以bruce用户创建了ansible主机可以访问的环境。

```shell
ansible amo -m ping -u bruce
```


#### 执行命令


在所有的server上，以当前bash的同名用户，在远程主机执行“echo bash”

```shell
ansible all -a "/bin/echo hello"
```

```shell
[root@cdyf216 ansible]# ansible amo -a "/bin/echo hello"
192.168.8.137 | CHANGED | rc=0 >>
hello
```

#### 拷贝文件


拷贝文件/etc/host到远程机器（组）atlanta，位置为/tmp/hosts

```shell
ansible web -m copy -a "src=/etc/hosts dest=/tmp/hosts"
```


#### 安装包


远程机器（组）webservers安装yum包

```shell
ansible web -m yum -a "name=git state=present
```


#### 添加用户

```shell
ansible amo -m user -a "name=foo password=foo"
```


#### 下载git包

```shell
ansible web -m git -a "repo=git://foo.example.org/repo.git dest=/tmp/myapp version=HEAD"
```


#### 启动服务

```shell
ansible web -m service -a "name=httpd state=started"
```


#### 并行执行


启动10个并行进行执行重起

```shell
ansible kubesphere -a "/bin/echo hello" -f 3
```

#### 查看远程主机的全部系统信息！！！

```shell
ansible all -m setup
```



