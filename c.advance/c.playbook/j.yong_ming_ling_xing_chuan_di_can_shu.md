# ssssssssssssssssss

为了使Playbook更灵活、通用性更强，允许用户在执行的时候传入变量的值，这个时候就需要用到“额外变量”。

## 定义命令行变量

在release.yml文件里，hosts和user都定义为变量，需要从命令行传递变量值。

```
---

- hosts: '{{ hosts }}'
  remote_user: '{{ user }}'

  tasks:
     - ...

```

## 使用命令行变量

在命令行里面传值得的方法：  
```
ansible-playbook e33_var_in_command.yml --extra-vars "hosts=web user=root"
```

还可以用json格式传递参数：  
```
ansible-playbook e33_var_in_command.yml --extra-vars "{'hosts':'vm-rhel7-1', 'user':'root'}"
```

还可以将参数放在文件里面：  
```
ansible-playbook e33_var_in_command.yml --extra-vars "@vars.json"
```
