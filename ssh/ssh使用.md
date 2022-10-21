# 用ssh在git账户中添加key

.ssh路径：`C:\Users\94806\.ssh`，一般就是用户文件夹下面

使用cmd或powershell生成ssh-key：
`ssh-keygen -t rsa -C "你的邮箱"`
![[ssh_key_gen.webp]]
在`Enter file in which to save the key (C:\Users\94806/.ssh/id_rsa):`后面写你想把key生成到那个文件当中（若没有会创建），然后敲两下回车即可；若你要设置密码，在这两次输入密码即可
![[ssh文件结构.jpg]]

在gitlab添加key时，复制.pub文件里的内容并添加，可以设置key的有效期和名字
![[gitlab中添加key.png]]

在.config文件中添加下面的内容
```
Host gitlab.com                                                              
     HostName gitlab.com                                                      
     PreferredAuthentications publickey                                           
     IdentityFile ~/.ssh/id_rsa_gitlab_948062294
```
即可指定在gitlab连接时使用哪个key

用`User {名字}`可以指定不同账号的key
```
Host github.com                                                                  
     HostName github.com                                                          
     PreferredAuthentications publickey    
     User {ZJUxjy}                                       
     IdentityFile ~/.ssh/id_rsa_github_948062294
```