<div align="center">

## Delete a File Unrecoverable\(Safe\)


</div>

### Description

This will create a function that you can.

That function will delete your file safely, but first its contents will be overwriten by DOTS(.)

Give it a try(I checked this with EasyRecovery Professional Edition: I couldn't recover my testfile :-) 

----

Soon I'll release my StuffX1 program containing a huge collection of my homemade handy subs and functions :-)
 
### More Info
 
file= A file


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[TV2kNET\.net](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/tv2knet-net.md)
**Level**          |Intermediate
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |VB 6\.0
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__1-1.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/tv2knet-net-delete-a-file-unrecoverable-safe__1-31813/archive/master.zip)

### API Declarations

```
'none
```


### Source Code

```
Option Explicit
Declare Function DeleteFile Lib "kernel32" Alias "DeleteFileA" (ByVal lpFileName As String) As Long
Public Function FastDelete(IOFilePath As String) As Long
'-----------------------------------
'-  FastDelete(IOFilePath)
'-  IOFilePath is the location of a file
'-  that you want to delete.
'-
'- It will delete that file real fast
'-
'-  By T-Virus Creations
'- http://www.tvirusonline.be
'- email: tvirus4ever@yahoo.co.uk
'-
'-----------------------------------
On Error Resume Next
Open IOFilePath For Output As #1 ' Open File
'Automatic Delete Of Content
Close #1 ' Close File
DeleteFile IOFilePath
FastDelete = 0
End Function
Public Function GetFileSize(File As String) As Long
'-----------------------------------
'-  GetFileSize(File)
'-  File is the location of a file.
'-
'- It will return the size of the file
'-   size can be a little wrong :(
'-
'-  By T-Virus Creations
'- http://www.tvirusonline.be
'- email: tvirus4ever@yahoo.co.uk
'-
'-----------------------------------
Dim out As String
Dim t As String
Open File For Input As #1 ' Open File
While EOF(1) = False
Input #1, t
If out = "" Then
out = t
GoTo 10
End If
out = out + t
10
Wend
Close #1 ' Close File
GetFileSize = Len(out) ' + 2
End Function
Public Sub SaveBogus(File As String, Blocks As Long, BlockSize As Long, UseDoEvents As Boolean)
'-----------------------------------
'-  SaveBogus(File , Blocks, BlockSize, UseDoEvents)
'-  File is the location of a file.
'-  Blocks= The amount of block
'-  BlockSize= The size in bytes of one block
'-  UseDoEvents= Use this when working with big files, else could freeze
'-
'-  Saves a string full with dots
'-
'-  By T-Virus Creations
'- http://www.tvirusonline.be
'- email: tvirus4ever@yahoo.co.uk
'-
'-----------------------------------
Open File For Output As #1
Dim SStr As String
Dim i As Long
For i = 1 To Blocks ' - 2
SStr = SStr + String(BlockSize, ".") 'Chr(Rnd(10) * 100))
If UseDoEvents = True Then
DoEvents
End If
Next
Print #1, SStr
Close #1
End Sub
Public Sub SafeDelete(File As String)
'-----------------------------------
'-  SafeDelete(File)
'-  File is the location of a file.
'-
'- It will delete File fast and safe.
'-
'-  By T-Virus Creations
'- http://www.tvirusonline.be
'- email: tvirus4ever@yahoo.co.uk
'-
'-----------------------------------
On Error Resume Next
SaveBogus File, GetFileSize(File), 1, True
Open File For Output As #1 ' Open File
'Automatic Delete Of Content
Close #1 ' Close File
DeleteFile File
End Sub
```

