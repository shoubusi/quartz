---
tags: SqlServer
---
# SQL Server 扩展事件

## 操作步骤

使用基于查询批处理跟踪（Query Batch Tracking）模板的扩展事件会话（Extended Event Sessions）跟踪所有活动的会话。

![](../../attachment/Pasted%20image%2020221024170510.png)

![](../../attachment/Pasted%20image%2020221024170912.png)

![](../../attachment/Pasted%20image%2020221024170831.png)

![](../../attachment/Pasted%20image%2020221024171130.png)

请按照以下的步骤配置一个收集 SQL Server 工作负载的扩展事件：

1. 打开 SQL Server Management Studio.
2. 连接到生产环境的服务器中数据库实例
3. 展开 SQL Server 实例>管理（Management）> 扩展事件（Extended Event）。
4. 右键会话（Sessions）>新建会话向导
5. 为该会话输入一个新的名字，例如：Query Batch Tracking.
6. 单击 下一步 ，然后选择 使用此事件会话模板 选项。
7. 在下拉列表中选择 查询批处理跟踪 模板，然后单击 下一步。
8. 在 捕获全局字段（Capture Global Fields） 页面，勾选中 client_hostname（客户端计算机名称）和 database_name（数据库名称）。
9. 单击 下一步 直到 指定会话数据存储（Specify Session Data Storage）页面，然后选中 将数据保存到文件供以后分析（Save data to a file for later analysis）选项。
10. 在 服务器上的文件名（File name on server）选项中，浏览到您希望该跟踪文件保存的路径。例如：`C: \Temp\QueryBatchTracking.xel`。
11. 如果您没有指定特殊的路径，跟踪文件将保存在日志文件夹的默认路径。例如：`C: \Program Files\Microsoft SQL Server\MSSQL[version].MSSQLSERVER\     MSSQL\Log\ ueryBatchTracking.xel`。但是，默认的路径可能会被更改。所以，     最好指定一下该跟踪文件的保存路径。
12. 确认 启用文件滚动更新（Enable file rollover）选项已激活，以及完整的存储数据的大小设为 500 MB。例如，最大的文件大小= 100 MB 和最大文件数为 5 。500 MB 是推荐的一个数值，如果有需要也可以设为更大。
13. 单击 完成 ，然后单击 关闭。
14. 在 SQL Server Management Studio 的对象资源管理器（Object Explorer）中，展开 SQL Server 实例并导航到管理>扩展事件>会话。
15. 右键 Query Batch Tracking（或者是你在第 5 步指定的名称）>启动会话。
16. 在重现问题或者启动 20 分钟之后，停止这个扩展会话。重新操作第 13 步，然后右键 Query Batch Tracking（或者是你在第 5 步中设定的名称）>停止会话。

注意：

- 所有的这些设定都将会立即生效，无需关闭和重启 SQL Server。
- 使用完这个扩展事件的会话后，可以不删除它，因为停止这个会话后，便停止 了跟踪，不会对服务器造成任何影响，而且如果有需要可以在将来再直接使用 它。 
- 在排查一个特殊的问题时，您可以在重现特殊问题时使用 查询批处理跟踪 会话。 不过，对于 SQL Server CPU 的使用率特别高的性能问题时（例如：大于 80 ％-85 ％），启动和停止会话的时间间隔应该少于 5 分钟，如果 CPU 使用率高于90 ％，则不建议使用这个会话。
- 当要发送跟踪文件给技术支持中心用于分析时，建议临时停止并重新启动这个扩展事件会话。以确保收集到最新的数据到扩展事件的跟踪文件中。操作步骤如下：展开 SQL Server 实例，导航到管理>扩展事件>会话，右键 Query Batch Tracking（在第 5 步中指定的名称）>停止 Session。如果在复制跟踪文件之后还 要继续使用这个会话，则右键这个会话>启动会话。 
- 您也可以使用查询批处理抽样（Query Batch Sampling）模板。不过，这个模板 默认只收集 20 ％的活动会话，这意味着您可以运行这个会话更长的时间。但是 这个模板收集的数据是不完整的。这个模板主要用于获得 SQL Server 工作负载 的总览，不适用于排查性能问题。所以，在通常情况下，不建议使用该模板。 除非是技术支持中心要求您使用。


## 使用“system health”捕捉锁和死锁

SQL Server 2012 或者更高的版本中默认开启了一个名为“system_health”的扩展事件 会话。该会话可以使用于捕捉死锁报告和相关的数据库锁。为确保该 system_health 的会话可以捕捉几周甚至几个月的性能数据，建议增加这个会话的数据存储空间。 请按照以下的步骤进行设置：

![](../../attachment/Pasted%20image%2020221024171908.png)

1. 打开 SQL Server Management Studio。
2. 连接到生产环境中的 SQL Server 实例。
3. 展开 SQL Server 实例，然后导航到管理（Management）>扩展事件（Extended Event）>会话（Sessions）>右键 system_health> 属性（Properties）。
4. 在数据存储（Data Storage）页面，单击 event_file 行，然后确认最大文件大小（Maximum file size）是否大于 5MB。默认的设置一般只指定存储 20 MB 的数据。
5. 如果总的存储数据是少于 500 MB 的，将默认的 event_file 删除，然后单击添加，在新增行的类型下拉中选择 event_file。
6. 确认启用文件滚动更新（Enable file rollover）已经勾选，以及总的存储数据大概为 500 MB。例如：最大的文件大小 = 100 MB，最大文件数为 5 。500MB 是推荐的一个数值，如果有需要也可以设为更大。
7. 最后，确认这个“system_health”会话已经开启。

注意：

- 当要收集这个跟踪文件发送给技术支持中心进行分析时，建议先临时停止该会话， 然后重新启动。这样可以确保捕捉到最新的数据到扩展事件的跟踪文件中。操作方法如下：展开 SQL Server 实例并导航到管理（Management）>扩展事件 （Extended Event）>会话（Sessions）>右键 system health>停止会话，然后再右键 选择启动会话。
- 该 system_health 扩展事件会话会持续开启，因为这是 SQL Server 中默认配置的。

## 捕捉阻塞中的锁

要捕捉阻塞的报告，请按照以下的步骤创建一个新的扩展事件会话：

![](../../attachment/Pasted%20image%2020221024172018.png)

![](../../attachment/Pasted%20image%2020221024172130.png)

1. 打开 SQL Server Management Studio。
2. 连接到生产环境中的 SQL Server 实例。
3. 展开 SQL Server 实例并 导航到管 理（Management）>扩 展事件（Extended Event）。
4. 右键会话（session）>新建会话向导（New Session Wizard）。
5. 在会话名称处输入一个名称。例如，输入 BlockingLocks。
6. 单击下一步>选择 不使用模板 选项>下一步。
7. 在选择要捕捉的事件页面，双击 blocked_process_report 事件（或者通过单击向右的箭头）将该事件添加到右侧的所选事件列表中。
8. 单击下一步直到指定会话数据存储页面，勾选将保存数据到文件供以后分析。
9. 单击浏览为服务器上的文件名制定该跟踪文件要保存的路径。例如：`C:\Temp\BlockingLocks.xel`。
10. **注意** ：如果您没有指定文件的路径，文件会保存在默认的日志文件夹中。例如：`C:\Program Files\Microsoft SQL Server\MSSQL[version].MSSQLSERVER\MSSQL\Log\BlockingLocks.xel`。但是，该默认路径有时会发送改变，所以最好     是为该文件指定一下要保存的路径。
11. 单击完成，然后关闭。
12. 在对象资源管理器中，右键 SQL Server 实例>属性>高级，然后设置阻塞的进程阈值（Blocked Process Threshold）为 20 秒。如果在测试环境中，可以设置为 5 秒。
13. 展开 SQL Server 实例并导航 到管 理（Management）>扩展 事件（Extended Event）>Sessions>BlockingLocks（在第 5 步中指定的名称）>启动会话。

**注意：**

- 当您需要分析 SQL Server 的性能时，最好只使用阻塞的扩展会话。如果在捕捉了几个星期的数据之后，还是没有找到任何的原因，您应该通过设置阻塞的进程阈值为 0 以停止该会话。这个步骤可以参考步骤 11 ，在 SQL Server 实例的属性>高级中设置。 
- 不论什么情况下，请都不要将阻塞的进程阈值的值设置低于 5 。如果这个值是小于 20 的，会捕捉很多的阻塞的事件。但是，在一个非常繁忙的 SQL Server 中，建议将数值增加到 30 。 
- 所有的这些设置都将立即生效，无需停止和重启 SQL Server。
- 当要收集这个跟踪文件发送给技术支持中心进行分析时，建议先临时停止该会话， 然后重新开启。这样可以确保捕捉到最新的数据到扩展事件的跟踪文件中。操作方 法如下：展开 SQL Server 实例并导航到管理（Management）>扩展事件 （Extended Event）>会话（Sessions）>右键 BlockingLocks（第 5 步中指定的名称）>停止会话，然后再右键选择启动会话。如果您想在复制了跟踪文件之后继续使用这个会话，请右键单击该会话>启动会话。


## 输出文件
XEL 格式文件

## 分析 SQL 跟踪数据

您可以使用 SQL Server 探查工具来查看 SQL 跟踪和 TRC 文件格式。

您可以在 SQL Server Management Studio 中打开扩展事件会话进行分析。

VARs 可以使用 SOLIDWORKS Log Parser tool（Reseller 版本）进行扩展事件会话， 该工具在知识库解决方案 [[../../Solution/S-067430]] 中提供。使用日志分析器工具的一个优点是，它可以生成图表并提取阻塞详细信息报告。

本节仅介绍日志分析器工具支持的以下主要扩展事件：
- 对于 SQL 工作负载分析：rpc_completed 和 sql_batch_completed. 
- 对于数据库锁、死锁或阻塞链等关键性能指标：wait_info, xml_deadlock_report 和 blocked_process_report.


## 参考
[S-067430](../../Solution/S-067430.md)