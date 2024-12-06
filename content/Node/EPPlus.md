# EPPlus

## Document
- https://github.com/EPPlusSoftware/EPPlus/wiki
- https://epplussoftware.com/docs/6.1/api/index.html

## Example
- https://github.com/EPPlusSoftware/EPPlus.Sample.NetFramework

| No  | Sample                                        | Description                                                                                                                                                                              |
| --- | --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 01  | Getting started                               | Basic usage of EPPlus: create a workbook, fill with data and some basic styling                                                                                                          |
| 02  | Read workbook                                 | Read data from a workbook                                                                                                                                                                |
| 03  | Async/Await                                   | Using async/await methods for loading and saving data                                                                                                                                    |
| 04  | Loading data                                  | Load data into a worksheet from various types of objects and create a table.  It also demonstrates the Autofit columns feature.                                                          |
| 05  | Import and Export csv files and create charts | This sample shows how to load and save CSV files using the LoadFromText and SaveToText methods, how to use tables and how to use charts with more than one charttype and secondary axis. |
| 06  | Calculate formulas                            | How to calculate formulas and add custom/missing functions in a workbook                                                                                                                 |
| 07  | Open workbook and add data/chart              | Opens an existing workbook, adds some data and a pie chart.                                                                                                                              |
| 08  | Sales report                                  | Create a report with data from a SQL database.                                                                                                                                           |
| 09  | Performance and protection                    | Loads 65 000 rows, styles them and sets a password.                                                                                                                                      |
| 10  | Read data using Linq                          | This sample shows how to use Linq with the Cells collection to read sample 9.                                                                                                            |
| 11  | Conditional formatting                        | Demonstrates conditional formatting.                                                                                                                                                     |
| 12  | Data validation                               | How to add various types of data validation to a workbook and read existing validations.                                                                                                 |
| 13  | Filters                                       | How to apply filters in a worksheet, table or a pivot table                                                                                                                              |
| 14  | Shapes & Images                               | Shows how to add shapes and format them in different ways.                                                                                                                               |
| 15  | Chart Styling & Themes                        | Load a theme and create various charts and style them.                                                                                                                                   |
| 16  | Sparklines                                    | Demonstrates sparklines functionality.                                                                                                                                                   |
| 17  | FX report                                     | Exchange rates report with data from a SQL database. Demonstrates some of the chart capabilities of EPPlus                                                                               |
| 18  | Pivot tables                                  | Demonstrates the Pivot table functionality of EPPlus.                                                                                                                                    |
| 19  | Encryption and protection                     | This sample produces a quiz, where the template workbook is encrypted and password protected.                                                                                            |
| 20  | Create filesystem report                      | Demonstrates usage of styling, printer settings, rich text, pie-, doughnut- and bar-charts, freeze panes and row/column outlines                                                         |
| 21  | VBA - Visual Basic for Applications           | Demonstrates EPPlus support for VBA, includes a battleship game                                                                                                                          |
| 22  | Ignore errors                                 | Various samples on how to ignore error on cells.                                                                                                                                         |
| 23  | Comments                                      | Sample showing how to add notes and threaded comments.                                                                                                                                   |
| 24  | Slicers                                       | Sample showing how to add Pivot Table slicers and Tabel slicers.                                                                                                                         |
| 25  | Export to/from DataTable                      | Sample showing import/export rangedata with System.Data.DataTable                                                                                                                        |
| 26  | Form controls                                 | Sample showing how to add differnt form controls and how to group drawings.                                                                                                              |
| 27  | Custom styles for tables and slicers          | Sample showing how to create custom styles from tables, pivot tables and slicers.                                                                                                        |
| 28  | Tables                                        | Sample showing how to work with tables.                                                                                                                                                  |
| 29  | External links                                | Shows how to work with links to external workbooks                                                                                                                                       |
| 30  | Sorting Ranges                                | Shows how to work with the Sort method for ranges and tables                                                                                                                             |
| 31  | Html Export                                   | Shows how to export tables and ranges to HTML                                                                                                                                            |
| 32  | Json Export                                   | Shows how to export tables and ranges to JSON                                                                                                                                            |
| 33  | ToCollection                                  | Shows how to export data from worksheets and tables into an IEnumerable&lt;T&gt; where T is a class.                                                                                     |

## Reference
- [System.Data.DataTable](System.Data.DataTable.md)
- [System.IO](System.IO.md)
- [System.Data.SQLite](System.Data.SQLite.md)
- [Collections](Collections.md)
- [Anonymous-types](Anonymous-types.md)
- [select-clause](select-clause.md)

ExcelPackage.LicenseContext

```xml
<configuration>
  <appSettings>
    <add key="EPPlus:ExcelPackage.LicenseContext" value="NonCommercial" />
  </appSettings>
</configuration>
```