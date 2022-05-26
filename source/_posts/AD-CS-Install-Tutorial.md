---
title: 安装 Active Directory 证书服务
date: 2022-05-21 21:41:58
tags: windows server
category: 学习笔记
---
## `系统信息`

操作系统:

Windows Server 2008 R2 Datacenter x64

下载:

[ed2k](ed2k://|file|cn_windows_server_2008_r2_standard_enterprise_datacenter_and_web_with_sp1_vl_build_x64_dvd_617396.iso|3368962048|7C210CAC37A05F459758BCC1F4478F9E|/)

## `安装 Active Directory 域服务`

- 在 `服务器管理器` 中选择 `添加角色`

- 勾选 `Active Directory 域服务` , 在 `添加角色向导` 中点击 `添加必须的功能`

![AD-CS-Install-Tutorial_01](./AD-CS-Install-Tutorial_01.jpg)

- 点击 `安装` 按钮完成Active Directory 域服务的安装, 安装完成后点击 `关闭该向导并启动 Active Directory 域服务 安装向导(dcpromo.exe)` 

![AD-CS-Install-Tutorial_02](./AD-CS-Install-Tutorial_02.jpg)

- 选中 `在林中新建域` , 点击 `下一步`

> 如果出现如图所示的错误, 需要在控制面板中给 `Administrator` 账户设置密码
> 
> ![AD-CS-Install-Tutorial_03](./AD-CS-Install-Tutorial_03.jpg)

- 在 `命名林根域` 页面中输入根域的名字, 在接下来的 `设置林功能级别` 页面中设置基本为 `Windows Server 2008 R2`

- 如果提示静态IP分配, 则按照需求选择选项. 此处选择 `是`

![AD-CS-Install-Tutorial_04](./AD-CS-Install-Tutorial_04.jpg)

- 提示 `无法创建该 DNS 服务器的委派` , 选择 `是`

![AD-CS-Install-Tutorial_05](./AD-CS-Install-Tutorial_05.jpg)

- 为 Administrator 分配密码

![AD-CS-Install-Tutorial_06](./AD-CS-Install-Tutorial_06.jpg)

- 等待配置完成后, Active Directory 域服务 则已安装完毕

## `安装 Active Directory 证书服务`

- 上部分操作完成后, 显示需要重启, 选择 `不立即重新启动`

- 以管理员运行命令提示符后运行命令 `net group "Domain Admins" <登录用户名> /add`

- 重新启动 Windows Server 2008

- 在 `添加角色向导` 中选中 `Active Directory 证书服务`

- 在下一页中选中 `证书颁发机构 Web 注册`

- `指定安装类型` 选择 `企业`

> 在没有将当前用户添加到 `Domain Admins` 或 `Enterprise Admins` 用户组中时, `企业` 选项将无法选择

- CA类型选择 `根CA`, `新建私钥` 并保持默认设置

- 完成安装后, 可以在 IIS 管理器 中 `Default Web Site` 网站中找到 `certsrv` 选项

![AD-CS-Install-Tutorial_07](./AD-CS-Install-Tutorial_07.jpg)

> ## 注意:
>
> 在访问证书签发的 Web 页面时需要使用 IP 地址进行访问, 并完成身份认证, 否则会出现以下错误信息
>
> ![AD-CS-Install-Tutorial_08](./AD-CS-Install-Tutorial_08.jpg)
>
> 注: 使用 Windows 自带认证时可能出现无法登录的错误