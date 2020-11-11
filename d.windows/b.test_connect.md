# Ansible服务端配置和测试管理Windows服务器(服务端操作)

### 安装python相关模块

```shell
pip install pywinrm
```

### 1. 添加windows客户端连接信息

编辑/etc/ansible/hosts，添加客户端主机信息(ansible服务端的配置)

```ini
[windows]

192.168.8.131 ansible_ssh_user="Administrator" ansible_ssh_pass="zteict123" ansible_ssh_port=5985 ansible_connection="winrm" ansible_winrm_server_cert_validation=ignore
```

### 2. 测试ping探测windows客户主机是否存活

执行命令

```shell
ansible 192.168.8.131 -m win_ping
```

### 3. 测试文件管理

测试在windows主机执行远程创建目录

```shell
ansible 192.168.8.131 -m win_file -a 'dest=c:\config_dir state=directory'
```

测试将ansible主机上的/etc/hosts文件同步到windows主机的指定目录下

```shell
 ansible 192.168.8.131 -m win_copy -a 'src=/etc/hosts dest=c:\config_dir\hosts.txt
```

删除文件

```shell
ansible 192.168.8.131 -m win_file -a 'dest=c:\config_dir\hosts.txt state=absent'
```

删除目录

```shell
ansible 192.168.8.131 -m win_file -a 'dest=c:\config_dir2 state=absent'
```

### 3. 测试远程执行cmd命令

```shell
ansible 172.16.10.23 -m win_shell -a 'ipconfig'
```

### 4. 远程重启windows服务器

```shell
ansible 172.16.10.23 -m win_reboot

ansible 172.16.10.23 -m win_shell -a 'shutdown -r -t 0'
```

### 5. 测试创建用户(远程在windows客户端上创建用户)

```shell
ansible 172.16.10.23 -m win_user -a "name=testuser1 passwd=123456"
```



### 6. Windows服务管理

Ansible命令格式：

```shell
ansible [远程主机IP地址] -m win_shell -a “net stop|start 服务名”
```

此外，Ansible还可以远程管理Windows的IIS服务、Apache等Web服务，利用Ansible实现批量更新Web应用，如代码发布、版本更新等。