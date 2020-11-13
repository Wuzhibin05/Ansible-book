# Ansible介绍

## 什么是Ansible?

Ansible是一种IT自动化工具。它可以配置系统，部署软件并协调更高级的IT任务，例如连续部署或零停机滚动更新。

**Ansible** 简单的说是一个配置管理系统(configuration management system)。你只需要可以使用 ssh 访问你的服务器或设备就行。它也不同于其他工具，因为它使用推送的方式，而不是像 puppet 等 那样使用拉取安装agent的方式。你可以将代码部署到任意数量的服务器上!

## Ansible能做什么？

 ansible可以帮助我们完成一些批量任务，或者完成一些需要经常重复的工作。比如：同时在100台服务器上安装nginx服务，并在安装后启动它们。比如：将某个文件一次性拷贝到100台服务器上。比如：每当有新服务器加入工作环境时，你都要为新服务器部署某个服务，也就是说你需要经常重复的完成相同的工作。这些场景中我们都可以使用到ansible。。

**包括：**拷贝文件、安装包、启动服务等等

## 常用自动化运维工具

```
Ansible：python，Agentless，中小型应用环境
Saltstack：python，一般需部署agent，执行效率更高
Puppet：ruby, 功能强大，配置复杂，重型,适合大型环境
Fabric：python，agentless
Chef：ruby，国内应用少
Cfengine
func
```

## 企业级自动化运维工具应用实战ansible

```
公司计划在年底做一次大型市场促销活动，全面冲刺下交易额，为明年的上市做准备。
公司要求各业务组对年底大促做准备，运维部要求所有业务容量进行三倍的扩容，
并搭建出多套环境可以共开发和测试人员做测试，运维老大为了在年底有所表现，
要求运维部门同学尽快实现，当你接到这个任务时，有没有更快的解决方案？
```

## Ansible发展史

```
Ansible
Michael DeHaan（ Cobbler 与 Func 作者）
名称来自《安德的游戏》中跨越时空的即时通信工具
2012-03-09，发布0.0.1版，2015-10-17，Red Hat宣布收购
官网：https://www.ansible.com/
官方文档：https://docs.ansible.com/
同类自动化工具GitHub关注程度（2016-07-10）
```

![image](a.architecture\images\fazhan.png)

## 特性

1> **模块化**：调用特定的模块，完成特定任务
2> Paramiko（python对ssh的实现），PyYAML，Jinja2（模板语言）三个关键模块
3> **支持自定义模块**
4> 基于**Python**语言实现
5> 部署简单，基于python和SSH(默认已安装)，agentless
6> 安全，基于OpenSSH
7> 支持playbook编排任务
8> **幂等性：**一个任务执行1遍和执行n遍效果一样，不因重复执行带来意外情况
9> 无需代理不依赖PKI（无需ssl）
10> 可使用任何编程语言写模块
11> **YAML格式**，编排任务，支持丰富的数据结构
12> 较强大的**多层解决方案**


