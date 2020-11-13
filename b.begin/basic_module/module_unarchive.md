## Unarchive

### 功能说明

解压压缩文件到指定目录。

### 示例

- 解压文件到远程目录

```yaml
- name: Extract foo.tgz into /var/lib/foo
  unarchive:
    src: foo.tgz
    dest: /var/lib/foo
```

- 解压远程主机的文件到远程主机

```yaml
- name: Unarchive a file that is already on the remote machine
  unarchive:
    src: /tmp/foo.zip
    dest: /usr/local/bin
    remote_src: yes
```

- 下载文件夹解压

```yaml
- name: Unarchive a file that needs to be downloaded (added in 2.0)
  unarchive:
    src: https://example.com/example.zip
    dest: /usr/local/bin
    remote_src: yes
```

- 额外选项

```yaml
- name: Unarchive a file with extra options
  unarchive:
    src: /tmp/foo.zip
    dest: /usr/local/bin
    extra_opts:
    - --transform
    - s/^xxx/yyy/
```