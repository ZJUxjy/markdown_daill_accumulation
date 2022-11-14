
安装docker后，docker会自动创建2个发行版

-   docker-desktop
-   docker-desktop-data

1. 关闭docker、docker-desktop
2. 关闭所有发行版`wsl --shutdown`
3. docker导出，`wsl --export docker-desktop-data D:\Docker\wsl\data\docker-desktop-data.tar`，`wsl --export docker-desktop D:\Docker\wsl\data\docker-desktop.tar`，
效果：
```bash
PS D:\Docker\wsl\data> pwd
Path
----
D:\Docker\wsl\data
PS D:\Docker\wsl\data> ls
    目录: D:\Docker\wsl\data
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        2022/11/10     10:28     4054753280 docker-desktop-data.tar
-a----        2022/11/10     10:28       58941440 docker-desktop.tar
```
4. 迁移回来`wsl --import docker-desktop-data D:\Docker\wsl\data\ D:\Docker\wsl\data\docker-desktop-data.tar`
效果：
```bash
目录: D:\Docker\wsl\data
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        2022/11/10     10:28     4054753280 docker-desktop-data.tar
-a----        2022/11/10     10:28       58941440 docker-desktop.tar
-a----        2022/11/10     11:11    22815965184 ext4.vhdx
```
重启docker发现image、容器都还在