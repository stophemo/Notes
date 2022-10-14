## ssh key

### 生成公钥

- 1.如果通过上面的方式找不到公钥，你就需要先生成公钥了：`ssh-keygen`
- 2.接着会确认存放公钥的地址，默认就是上面说的路径，直接enter键确认
- 3.接着会要求输入密码和确认密码，如果不想设置密码直接不输入内容 按enter键

```shell
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/windows/.ssh/id_rsa):
Created directory '/c/Users/windows/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/windows/.ssh/id_rsa
Your public key has been saved in /c/Users/windows/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:mYhTt3zc2aGyaKyK7i9/RsNR9+KvioC4jlsaD7MhgJw windows@DESKTOP-996996
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|        . .      |
|      .... .  .  |
|o .  o.+ =...+ . |
|oE  o...S.+.+ .  |
|.. . .+. o.o     |
|B o .. .+ ..     |
|o@.. .o+    .    |
|B==+++o ....     |
+----[SHA256]-----+

```



### 查看公钥

`cat ~/.ssh/id_rsa.pub`

```sh
$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCu6gy5BYEG+IkxsGOemG65jXhG/uO75dVCLX+hI1TCMOFZS6coBK0fIGsreVgvGaKhCMMuu3MbSeih8UIPjl7veijNQnDMUmXtVQyMmmqZpm4oQACv4z7ctcOO+W3nY56Yxx+Z1zPr7GayEhgoGCxMD9klQ0TM/o05FGtpR4IWb+YGGR0qGEDmLuLEIATHpYH0kmucGCIheVynWg48QRlj+3N50UvZ1kgkIm0jsfLH3162u5Ll6uKI6imH+mLppReTh7eb6yO6dyGSZXnuG98rHJGSy3GvIZ/zvJXKpBgY60rYocYRlGPWgl031lRvz3xNOB9Sbkzoqztl517kOz4PQ78+ycDKWDeS5Lq4qBGTy6FSp0whKEvm115Dhw0Az5kJDtpqaJxa2jdiDnPsSf0OCvYK+FElwpwrmLEGmGPG5iCFgLS1ZNGTEgqfni4c11MKNoIosb0r6OmBN5woyoGbJHgpTkG1JCsFaXgUExmvaxI5lC1txacE286OMV8/280= windows@DESKTOP-996996
```



### 测试

`ssh -T @github.com`

```sh
$ ssh -T git@github.com
Hi Stophemo! You've successfully authenticated, but GitHub does not provide shell access.
```

