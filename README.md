Tool for comparing csv files between 2 folders

# Requirements

* Python3
* colorama
* Click

# Installation

You can install directly from github with the following command:

```bash
pip3 install git+https://github.com/felipevicens/csv-compare.git
```

# How to use it

Sometimes you need to compare 2 versions of the Excel file where someone made an small change and you can't see where was made. If the excel file have lot of sheets the difficulty is high.

Having that, the suggested procedure is to convert the excel book in a splitted csv files per version (Old and New) and try to compare both to find where are the changes.

You will need first to generate a folder with the CSVs files per excel book. The procedure is automated using the following steps:

1. Press Alt + F11
1. Right clic on a sheet and select Insert > module
1. Paste the code below:

```Javascript
  Sub SplitWorkbook()
  Dim FileExtStr As String
  Dim FileFormatNum As Long
  Dim xWs As Worksheet
  Dim xWb As Workbook
  Dim FolderName As String
  Application.ScreenUpdating = False
  Set xWb = Application.ThisWorkbook
  DateString = Format(Now, "yyyy-mm-dd_hh-mm-ss")
  FolderName = xWb.Path & "" & xWb.Name & " " & DateString
  MkDir FolderName
  For Each xWs In xWb.Worksheets
      xWs.Copy
      FileExtStr = ".csv": FileFormatNum = 6
      xFile = FolderName & "" & Application.ActiveWorkbook.Sheets(1).Name & FileExtStr
      Application.ActiveWorkbook.SaveAs xFile, FileFormat:=FileFormatNum
      Application.ActiveWorkbook.Close False
  Next
  MsgBox "You can find the files in " & FolderName
  Application.ScreenUpdating = True
  End Sub
```

1. Press F5 to execute the code. It Takes some time. You can grab a coffe :)
1. The files will be generated in the Spreadsheet saved folder.

Having the two folders with the csv files to compare, you can run the command:

```bash
csv-compare <FOLDER_OLD> <FOLDER_NEW>
```

To print the help:

```bash
csv-compare --help
```

# Author

Felipe Vicens <fjvicens@edgecloudlabs.com>