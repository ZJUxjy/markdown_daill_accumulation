# 记录一个遇到的vcdode内置终端运行错误问题

今天遇到了一个很离谱的问题，vs code内置终端用不了了。。。点击终端问题如下：

```
You must install or update .NET to run this application.

App: C:\Users\94806\.dotnet\tools\.store\powershell\7.2.7\powershell\7.2.7\tools\net6.0\any\win\pwsh.dll
Architecture: x64
Framework: 'Microsoft.WindowsDesktop.App', version '6.0.0' (x64)
.NET location: C:\Program Files\dotnet\

The following frameworks were found:
  5.0.14 at [C:\Program Files\dotnet\shared\Microsoft.WindowsDesktop.App]

Learn about framework resolution:
https://aka.ms/dotnet/app-launch-failed

To install missing framework, download:
https://aka.ms/dotnet-core-applaunch?framework=Microsoft.WindowsDesktop.App&framework_version=6.0.0&arch=x64&rid=win10-x64
```

---

## 解决方法：
到巨硬那里吧.NET框架补上 orz ~~~~

链接：
>[Download .NET 6.0 Desktop Runtime](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-desktop-6.0.10-windows-x64-installer)
>[Download .NET 6.0 Core Runtime](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-6.0.10-windows-x64-installer)

上面两个链接是windows_x64版本的，如果平台不一样到[Download .NET 6.0 (Linux, macOS, and Windows) (microsoft.com)](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)选择自己的版本。

---

## 问题分析

可能是之前给电脑硬盘腾空间，vs简化了一些东西导致的，巨硬这东西做的，，，总之就是非常无语。 TAT

