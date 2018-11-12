---
layout:     post
title:      "使用VBA批量将目录下的所有excel文件的所有sheet隐藏列，锁定列，并加保护密码"
subtitle:   ""
date:       2018-05-18
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    false
tags:
    - VBA
---

>最近朋友有一个批量处理大量excel的需求，需要将每个excel中的每个sheet里面的指定列隐藏，指定列锁定，还要加密。加起来总共有1万多张sheet，如果一张张sheet的人工操作，那真是得无聊死了。于是我帮忙找了一下办法。在网上找了各种例子，然后拼接起来，完美完成任务。

```vb
Sub LoopAllExcelFilesInFolder()
'PURPOSE: To loop through all Excel files in a user specified folder and perform a set task on them
'SOURCE: www.TheSpreadsheetGuru.com

Dim wb As Workbook
Dim myPath As String
Dim myFile As String
Dim myExtension As String
Dim FldrPicker As FileDialog

'Optimize Macro Speed
  Application.ScreenUpdating = False
  Application.EnableEvents = False
  Application.Calculation = xlCalculationManual

'Retrieve Target Folder Path From User
  Set FldrPicker = Application.FileDialog(msoFileDialogFolderPicker)

    With FldrPicker
      .Title = "Select A Target Folder"
      .AllowMultiSelect = False
        If .Show <> -1 Then GoTo NextCode
        myPath = .SelectedItems(1) & "\"
    End With

'In Case of Cancel
NextCode:
  myPath = myPath
  If myPath = "" Then GoTo ResetSettings

'Target File Extension (must include wildcard "*")
  myExtension = "*.xls*"

'Target Path with Ending Extention
  myFile = Dir(myPath & myExtension)

'Loop through each Excel file in folder
  Do While myFile <> ""
    'Set variable equal to opened workbook
      Set wb = Workbooks.Open(Filename:=myPath & myFile)
    
    'Ensure Workbook has opened before moving on to next line of code
      DoEvents
      
    '隐藏指定列，解锁指定列，设置锁定密码
    
    For Each sht In wb.Sheets
        sht.Columns("H:K").Hidden = True
        sht.Range("B:C").Locked = False
        sht.Protect "1234"
        sht.Protect AllowInsertingRows:=True
    Next
    'Save and Close Workbook
      wb.Close SaveChanges:=True
      
      
    'Ensure Workbook has closed before moving on to next line of code
      DoEvents

    'Get next file name
      myFile = Dir
  Loop

'Message Box when tasks are completed
  MsgBox "Task Complete!"

ResetSettings:
  'Reset Macro Optimization Settings
    Application.EnableEvents = True
    Application.Calculation = xlCalculationAutomatic
    Application.ScreenUpdating = True

End Sub
```
