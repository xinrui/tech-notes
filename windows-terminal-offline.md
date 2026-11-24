# 如何离线安装windows terminal？

1. 先去github release下载一个preinstallkit大包

2. 安装microsoft UI Xaml（可能的依赖项）

3. 使用以下命令：
```
Add-AppxProvisionedPackage `
    -Online `
    -PackagePath "D:\OfflineApps\Terminal\Microsoft.WindowsTerminal.msixbundle" `
    -LicensePath "D:\OfflineApps\Terminal\License.xml"
```
不安装license文件会导致应用打不开，使用管理员权限运行可以发现这一点。
