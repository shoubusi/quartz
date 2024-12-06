---
date created: 2024-06-20
date modified: 2024-06-27
type: Node
tags:
  - SolidPractices
  - BestPractices
  - knowledge
archived: false
---

# SolidPractices: Importing Files from Folders

## 1) Preface

- 本文档旨在分享关于将 CAD 文件从 Windows®文件资源管理器文件夹结构导入 SOLIDWORKS PDM 文件库的各种指南，以确保在 SOLIDWORKS PDM 文件库中建立和维护所有文件引用。
- 提供一般准则，适用于 SOLIDWORKS 文件及其他具有 SOLIDWORKS PDM 插件来管理文件引用的文件类型。
- 此过程适用于将每个文件的一个版本导入 SOLIDWORKS PDM 的情况，导入多个文件版本时最好使用 SOLIDWORKS PDM XML 导入工具。
- 可通过 SOLIDWORKS 知识库和 SOLIDWORKS 服务合作伙伴获得帮助，如有其他问题可联系 SOLIDWORKS 现场服务。

## 2) Task Summary

- 客户需要将大量文件从一个或多个 Windows 文件资源管理器文件夹移动到 SOLIDWORKS PDM 文件库视图中，将文件组织到 SOLIDWORKS PDM 文件库中的项目文件夹中，并建立这些文件之间的文件引用。

## 3) Understanding SOLIDWORKS File References

- 打开 SOLIDWORKS 文件时会执行动态搜索以查找文件的引用，允许父文件在不同位置查找引用。
- SOLIDWORKS 有完善的文件引用搜索过程，可在 SOLIDWORKS 帮助中搜索“Search Routine for Referenced Documents”查看。
- 可使用 SOLIDWORKS Document Manager API 读取和更新 SOLIDWORKS 文件引用，无需在 SOLIDWORKS 应用程序中打开文件。
- 了解 SOLIDWORKS Toolbox 和 Design Library，SOLIDWORKS Toolbox 功能与 SOLIDWORKS PDM 完全集成，最好在运行导入之前将 Toolbox 库加载到库中，还需要将 Design Library 文件添加到库中，但没有类似于 Toolbox 文件的管理功能。

## 4) Understanding SOLIDWORKS PDM File References

- 将文件添加到 SOLIDWORKS PDM 文件库后，软件不会评估文件引用，在启动签入过程时，SOLIDWORKS PDM 会搜索引用。
- 在签入过程中，会出现一个引用对话框，显示引用树，指示文件是否未找到或是否存在于库之外，软件会在签入过程中将引用写入 SOLIDWORKS PDM 数据库。
- SOLIDWORKS PDM 必须在库中存在文件才能管理文件引用，SOLIDWORKS PDM 的“Where-Used”和“Contains”选项卡不会显示存储在库之外的文件。
- 在库中移动或重命名文件时，SOLIDWORKS PDM 会在数据库中记录新的引用名称和位置，父引用会在本地视图中更新，但不会更新 SOLIDWORKS PDM 存档文件夹或其他客户端计算机上的本地缓存版本中的父文件。
- 可使用“Update References”工具查找和连接与父文件丢失的引用，该工具可选择一个文件并在文件库中搜索文件的引用，然后从匹配结果列表中选择并更新文件引用，该工具旨在一次修复一个父文件。

## 5) Import Strategies

- 确定将数据集导入 SOLIDWORKS PDM 的最佳过程需要对现有数据集的状态与数据导入的理想状态进行全面审查，有几种常见的导入数据方法可供考虑。
- 导入所有文件到一个文件夹中，然后将文件移动到子文件夹是一个简单的过程，但对于大型数据集可能会出现性能问题。
- 使用参考搜索路径是一种有效的解决方案，但需要确保指定所有必需的路径。
- 使用相对路径导入文件，前提是现有数据集存储在与库的文件夹结构匹配的文件夹结构中。
- 使用预处理修复工具，现有数据集可能包含不正确的引用或结构，建议使用自定义程序将现有数据集编译到正确的目录结构中，并在需要时读取文件引用并进行更正。
- 使用“Pack and Go”功能，在导入 SOLIDWORKS PDM 时确保引用在目标位置更新。

## 6) Do's and Don'ts

- 注意依赖参考搜索路径的风险，因为该过程非常动态，结果难以预测，并且可能会选择错误的文件。
- 注意本地库视图之外的流氓文件，确保对引用文件的位置进行控制，以防止 CAD 参考搜索过程找到原始文件而不是使用本地库视图中的新副本。
- 估计工作量时，考虑数据集的质量、是否需要修改数据集以及数据集的大小和组成。
- 评估策略和数据质量时，使用各种策略和小数据集测试导入，以验证导入策略，并使用自定义工具扫描和评估整个数据集。
