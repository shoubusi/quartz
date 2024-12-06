---
type: Node
tags:
  - obsidian
date created: 2024-11-25
date modified: 2024-11-25
---

# Obsidian Better Export PDF

https://github.com/l1xnan/obsidian-better-export-pdf

## Export Multiple Markdown Files

### Quick Export

Select the folder in the sidebar, right-click the menu `Export folder to PDF`, you can export the entire folder contents to a PDF file.

Note: This does not guarantee the file export order.

### Custom Export

Create a new table of contents note, add something like the following, need to add a `toc: true` document property:

```md
---
toc: true
---

## Table of Contents

[[Note1|Title1]]
[[Note2]]
[[Note2]]
```

This allows the plugin to export the notes in the order of the internal links. The anchor point of the exported PDF table of contents supports clicking to jump.

### Folder Batch Export

Select the folder in the sidebar, right-click the menu `Export each file to PDF`, you can batch export each file of the entire folder to PDF file.

### Export as One Page

In the export dialog, select `Custom` for **Page Size** and set **Margin** to `None`. Set the page size according to the document's requirements.
