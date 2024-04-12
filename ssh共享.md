# SSH 如何共享
Senario: Mac生成了SSH private&public key
1. 在MAC
```
cd /User/用户名/.ssh
cp id_rsa id_rsa.pub u盘路径
```
2. 把U盘插到windows上，首先先转到该电脑的用户上

   
3. 管理员方式打开powershell
```sys
cd ~
```

```sys
cd .\.ssh\
Set-Service -Name ssh-agent -StartupType Automatic
Get-Service ssh-agent | Select-Object -Property Name, StartType, Status
```
4.这里应该返回
```
Status   Name               DisplayName
------   ----               -----------
Running  ssh-agent          OpenSSH Authentication Agent
```
5. 将Mac生成的私钥添加认证
```sys
PS C:\Users\luxury\.ssh> ssh-add.exe .\id_rsa
```
应该返回```Identity added: .\id_rsa (sidneysun@Sidneys-Computer.local)```
