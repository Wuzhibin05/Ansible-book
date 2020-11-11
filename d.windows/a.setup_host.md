# windows主机配置

## 一、主机需求

为了满足ansible主机和windows主机之间的通讯，windows主机必须满足以下需求：

- 被管理主机支持以下版本：Windows 7, 8.1, and 10, 和 Windows Server 2008, 2008 R2, 2012, 2012 R2, 2016, and 2019。
- 必须安装PowerShell 3.0 及以上版本和NET 4.0 版本。
- 创建WinRM监听器。

**注意：**Windows Server 2008只能安装3.0，安装新版本的会导致脚本执行失败。

## 二、升级PowerShell和NET Framework

- 执行升级

```powershell
$url = "https://raw.githubusercontent.com/jborean93/ansible-windows/master/scripts/Upgrade-PowerShell.ps1"
$file = "$env:temp\Upgrade-PowerShell.ps1"
$username = "Administrator"
$password = "Rd2@jzcf"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force

# Version can be 3.0, 4.0 or 5.1
&$file -Version 5.1 -Username $username -Password $password -Verbose
```

PowerShell 5.1下载地址：

http://download.microsoft.com/download/6/F/5/6F5FF66C-6775-42B0-86C4-47D41F2DA187/Win8.1AndW2K12R2-KB3191564-x64.msu

net framework 4.5下载地址：

https://download.microsoft.com/download/B/A/4/BA4A7E71-2906-4B2D-A0E1-80CF16844F5F/dotNetFx45_Full_setup.exe

- 

```powershell
# This isn't needed but is a good security practice to complete
Set-ExecutionPolicy -ExecutionPolicy Restricted -Force

$reg_winlogon_path = "HKLM:\Software\Microsoft\Windows NT\CurrentVersion\Winlogon"
Set-ItemProperty -Path $reg_winlogon_path -Name AutoAdminLogon -Value 0
Remove-ItemProperty -Path $reg_winlogon_path -Name DefaultUserName -ErrorAction SilentlyContinue
Remove-ItemProperty -Path $reg_winlogon_path -Name DefaultPassword -ErrorAction SilentlyContinue
```

- 检查版本号： get-host



![image-20201111112050919](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201111112050919.png)

## 三、设置WinRM





```powershell
$url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)

powershell.exe -ExecutionPolicy ByPass -File $file
```



打开powershell终端，按以下步骤执行命令(正常情况不会报错，如果有报错，请检查输入的命令是否正确，或者手动输入命令进行配置)

 

### 1. 查看powershell执行策略

```powershell
get-executionpolicy
```

### 2. 更改powershell执行策略为remotesigned

```powershell
set-executionpolicy remotesigned
```

### 3. 配置winrm service并启动服务

```powershell
winrm quickconfig
```

### 4. 查看winrm service启动监听状态

```powershell
winrm enumerate winrm/config/listener
```

### 5. 修改winrm配置，启用远程连接认证

```powershell
winrm set winrm/config/service/auth '@{Basic="true"}'

winrm set winrm/config/service '@{AllowUnencrypted="true"}'
```

## 四、防火墙设置

- 通过命令winrm enumerate winrm/config/listener检查winrm服务正确启动之后

- 打开防火墙高级配置，选择入站规则，在点击新建规则

- 填写信任端口5985

 ![image-20201111131418885](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201111131418885.png)

- 添加防火墙信任规则，允许5985端口通过

![image-20201111131452311](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201111131452311.png)

- 填写新建规则名称 ansible

**注意：杀毒软件会阻止ansible执行powershell脚本，这里需要自己手动允许下**

