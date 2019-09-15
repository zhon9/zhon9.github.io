---
title: bat 脚本
date: 2019-09-10 15:36:58
tags: bat
---
### rename.bat
ren *.下载 *.

### rename2.bat
将当前目录的 aa (1).jpg 重命名 aa1.jpg
@Echo Off&SetLocal ENABLEDELAYEDEXPANSION
FOR %%a in (*) do (
echo 正在处理 %%a
set "name=%%a"
set "name=!name: (=!"
set "name=!name:)=!"
ren "%%a" "!name!"
)

### heiping.bat
start C:\Windows\System32\scrnsave.scr /s

### tree.bat
dir /o:-d 文件夹/b>list.txt


