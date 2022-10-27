## windows server 中文版 含UI界面

### 控制台配置

1. 创建实例



2. 配置实例名，描述等

（配置安全组规则）



3. 5 min后重置实例密码



### 环境配置

1.  远程桌面连接（windows）： 

win + R ： mstsc 

目标地址：47.96.99.183（服务器公网IP ）

用户名： administrator

密码：Clover(996)

2. ssh环境安装

打开Windows Powershell（管理员）

- 查看是否安装OpenSSH

```shell
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```

- 安装ssh客户端

```shell
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
```

- 安装ssh服务端

```shell
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

- 启动并配置 OpenSSH 服务器

```sh
# Start the sshd service
Start-Service sshd

# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'

# Confirm the Firewall rule is configured. It should be created automatically by setup. Run the following to verify
if (!(Get-NetFirewallRule -Name "OpenSSH-Server-In-TCP" -ErrorAction SilentlyContinue | Select-Object Name, Enabled)) {
    Write-Output "Firewall Rule 'OpenSSH-Server-In-TCP' does not exist, creating it..."
    New-NetFirewallRule -Name 'OpenSSH-Server-In-TCP' -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
} else {
    Write-Output "Firewall rule 'OpenSSH-Server-In-TCP' has been created and exists."
}
```



3. 此时就可以在本地windows使用 ssh 登录服务器

```sh
ssh administrator@47.96.99.183
The authenticity of host '47.96.99.183 (47.96.99.183)' can't be established.
ED25519 key fingerprint is SHA256:wW+kRmMmmB7Av0Ls7vqVU01jNM+GcOq8RVdSpdLUsdo.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '47.96.99.183' (ED25519) to the list of known hosts.
administrator@47.96.99.183's password:
```

登录成功

```sh
administrator@StophemoECS C:\Users\Administrator>
```



4. 安装node.js
5. 安装Git
6. 安装Nginx

官网下载，解压

双击nginx.exe 启动

dos命令操作：

```sh
# 启动
nginx.exe 
	# 或者 
	start nginx	
# 关闭Nginx
	# 快速停止nginx
	nginx -s stop  
	# 完整有序的停止nginx
	nginx -s quit
	# 使用taskkill命令
	taskkill /f /t /im nginx.exe
```

try_files $uri $uri/ /index.html;
