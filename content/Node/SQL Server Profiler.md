---
tags: SqlServer
---
# SQL Server Profiler

## 操作步骤
[[../../Solution/S-057205]]

1. 打开 SQL Server Profiler。点击 Windows 开始 — 所有程序 — Microsoft SQL Server — 性能工具。您也可以从 SQL Server Management Studio 中的工具 —SQL Server Profiler 打开该工具。
2. 单击文件>新建跟踪，在弹出的窗口中连接至数据库所在的 SQL Server 实例。
3. 在跟踪属性的常规窗口，在模板下拉列表中选择 Standard 模板
4. 在跟踪名称中输入一个名称。例如：TraceTest01.
5. 勾选 保存到文件 的选项及设定一个本地的路径用于保存该跟踪文件。然后单击保存。
6. 更改设置最大文件大小为 50 。默认的 5 MB 通常都太小了以致于在最后产生了多个文件。
7. 在事件选择页面，选中显示所有列选项。
8. 右键 DatabaseName 列>选择列，这一列后期可以快速的以数据库名称对数据进行筛选。
9. 在 事件选择 页面，右键 HostName 列>选择列。这一列后期可以快速的以客户端的计算机名对数据进行筛选。
10. 单击 运行。
11. 如果任务只是收集 SQL Server 的工作负载，可以让它运行 20 分钟。但是，如果运行跟踪的原因是为了特定的问题，请执行导致性能问题的操作。例如：检入先前浏览的文件。
12. 完成出现性能问题的操作后，在 SQL Server Profiler 中单击 停止所选跟踪（红色停止按钮）。
![](../../attachment/Pasted%20image%2020221024164649.png)

## 输出文件