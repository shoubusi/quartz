---
type: Node
tags:
  - SolidPractices
  - BestPractices
  - knowledge
archived: false
---
Searching in SOLIDWORKS PDM

这份文件是关于SOLIDWORKS PDM（产品数据管理）中的搜索功能的SolidPractices指南，由Dassault Systèmes公司发布。以下是其核心内容的概要：

1. **前言**：强调了SOLIDWORKS PDM用户依赖于搜索功能来定位数据仓库中的内容，并介绍了本文档的目的是提供搜索文件和快速返回准确搜索结果的最佳方法。

2. **概述**：介绍了SOLIDWORKS PDM数据仓库由Microsoft® SQL Server®数据库（包含元数据）和存档服务器（包含文件的实际版本）组成。用户可以从安装了SOLIDWORKS PDM客户端的系统上执行两种搜索：元数据搜索（数据库的SQL查询）和内容搜索（搜索存档服务器上物理文件中的数据或信息）。

3. **搜索功能改进历史**：
   - 2020年：引入了AND, OR, NOT等搜索运算符的使用。
   - 2017年：允许在离线模式下搜索本地文件。
   - 2016年：可以使用Windows Search Service进行内容搜索。
   - 2015年：引入了Windows Explorer中的版本号列。
   - 2012年：引入了嵌入式搜索工具。

4. **快速获取良好结果**：
   - 自定义搜索结果列。
   - 设置搜索卡的默认值。
   - 创建收藏夹搜索。
   - 对SQL Server进行调整以提高搜索速度。
   - 如何填写搜索卡以及手动停止搜索。
   - 搜索问题的错误日志。

5. **命令行搜索**：
   - 从命令行打开搜索工具的图形用户界面(GUI)。
   - 命令行选项。

6. **内容搜索**：
   - SOLIDWORKS PDM Professional提供了通过Microsoft Windows Search Service或Microsoft Indexing Service搜索存档服务器文件结构中的内容和属性的功能。
   - 描述了内容搜索的设置和启用步骤。

文件还包含了修订历史、使用指南和反馈请求，以及对SOLIDWORKS PDM数据库的SQL调整建议，强调不要手动创建索引。此外，还提供了如何优化搜索卡选择以加快SQL查询速度的建议。