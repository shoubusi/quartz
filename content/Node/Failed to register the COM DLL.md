---
customer:
user:
tags:
  - Issue
type: Issue
subject:
archived: false
date created: 2024-08-20
date modified: 2024-08-20
---

# 如何对未能在客户端系统上正确分发、加载的 PDM 插件进行故障诊断？

%%
How can a user troubleshoot SOLIDWORKS Enterprise PDM API add-in DLLs that fails to distribute or fails to load with error 'Failed to register the COM DLL' on client systems?
%%
## 现象

登录 PDM 后，报错提示 `Failed to register the COM DLL`

![](../attachment/634b51006e10f75bc79b3da8b0764c0.jpg)

**插件分发过程：**
* SOLIDWORKS PDM API 插件自动在用户登录时分发。 
* 插件在用户登录时自动从档案服务器中加入，并被下载到客户端，然后注册到本地应用程序数据文件夹（_%localappdata%_）。  

**注册失败的原因可能有：**
- 客户端系统缺少依赖项 (例如 Microsoft Visual C++ Redistributable 和 Microsoft .NET Framework)
- 加密和杀毒软件
- 操作系统账号权限不足

## 故障排除步骤

### 检查依赖项安装情况

安装文件在 SolidWorks 的安装镜像的 PreReqs 文件夹中。
- Microsoft Visual C++ : 所有 `VCRedist` 文件夹中的 x86 和 x64，共计 10 个安装文件
- .NET Framework : `\PreReqs\dotNetFx\NDP472-KB4054530-x86-x64-AllOS-ENU.exe` 和 `dotnetfx35.exe`，共计 2 个安装文件

![](../attachment/8cbf8d6e850ea6221976ef2234b9cf03.png)

虽然安装 SOLIDWORKS 时已经自动安装过 Microsoft Visual C++ 和 .NET Framework ，但现在要再次确认一遍 Microsoft Visual C++ 和 .NET Framework 已经安装，每一个安装文件都运行一遍， 直到安装界面显示“修复”选项表明已安装。

打开 [Windows 事件查看器](../SW/CAD/故障排除/Windows事件查看器.md) ，可能有更多信息。

![](../attachment/36dc214097c594bd823cf970a704340a.png)

例如上图指明缺少 Microsoft Visual C++ 2005

### 判断是否是 DLL 文件的问题

尝试从 PDM 安装目录的默认数据文件夹中加载 Dispatch.CAF 插件，如果也能出现注册失败现象，排除插件本身原因。

### 移除并重新添加插件

1. 导出插件；
2. 从 PDM 管理工具删除插件；
3. 重新添加插件。

### 关闭杀毒和加密软件

### 重新注册

尝试手动重新注册 SOLIDWORKS PDM API：[^1]

1. 打开命令提示符（以管理员身份运行）。
2. 将目录更改为“`..\Program Files\SolidWorks Corp\SOLIDWORKS PDM`”。
3. 键入 `REGSVR32 EdmInterface.dll`
4. 确定此操作是否解决问题。

要在出现问题的客户端上完全加载库的插件 DLL，请执行以下操作：

1. 关闭所有打开的应用程序。如果已激活，请从托盘图标退出 SOLIDWORKS PDM。
2. 打开 Windows 任务管理器并终止“explorer.exe”进程。
3. 转至“文件”>“运行新任务”> 键入“explorer”> 单击“确定”，以重新启动“explorer.exe”。
4. 浏览到：`C:\Users\[用户配置文件]\AppData\Local\SOLIDWORKS\SOLIDWORKS PDM\Plugins\[库名称]`
5. 删除此位置中的所有文件夹。文件夹看上去类似于 `{C52D573B-057B-4CB3-A357-4FE531251826}`
6. 观察第 4 步中的本地插件文件夹。
7. 打开第二个 Windows 文件资源管理器实例并登录到库。

客户端计算机将从存档服务器中检索库插件，使用每个插件的 GUID 创建文件夹，然后提取插件 DLL 并对其进行注册。

[^1]: [[S-049035]]