## shell

通过/bin/sh在远程节点上执行命令。如果一个操作你可以通过Module yum，copy操作实现，那么你不要使用shell或者command这样通用的命令module。因为通用的命令module不会根据具体操作的特点进行status的判断，所以当没有必要再重新执行的时候，它还是要重新执行一遍。

### 支持$home，支持$HOME和"<", ">", "|", ";" and "&"。
* 支持$home
  ```yaml
  - name: test $home
    shell: echo "Test1" > ~/tmp/test1
  ```
* 支持&&  
  ```  yaml
  - shell: service jboss start && chkconfig jboss on
  ```

* 支持>>
  ```yaml
  - shell: echo foo >> /tmp/testfoo
  ```

### 调用脚本

* 调用脚本
  ```yaml
  - shell: somescript.sh >> somelog.txt
  ```

* 执行命令前，改变工作目录

  ```yaml
  - shell: somescript.sh >> somelog.txt
    args:
      chdir: somedir/
  ```

* 在执行命令钱改变工作目录，并且在文件somelog.txt不存在时执行命令。

  ```yaml
  - shell: somescript.sh >> somelog.txt
    args:
      chdir: somedir/
      creates: somelog.txt
  ```

* 指定用bash运行命令

  ```yaml
  - shell: cat < /tmp/*txt
    args:
      executable: /bin/bash
  ```

- 执行多行shell脚本内容

  ```yaml
  - name: Shutdown koca-studio.
    shell: |
      pid=`ps -ef | grep {{studio_name}} | grep -v grep | awk '{print $2}'`
      if [ -n "$pid" ]
      then
      echo "kill -9 的pid:" $pid
      kill -9 $pid
      fi
  
      exit 0
  ```

