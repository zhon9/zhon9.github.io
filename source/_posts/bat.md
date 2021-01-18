---
title: batch file
date: 2019-09-10 15:36:58
tags: bat
---
### rename.bat
```bat
ren *.下载 *.
```

### rename2.bat
将当前目录的 aa (1).jpg 重命名 aa1.jpg
```bat
@Echo Off&SetLocal ENABLEDELAYEDEXPANSION
FOR %%a in (*) do (
echo 正在处理 %%a
set "name=%%a"
set "name=!name: (=!"
set "name=!name:)=!"
ren "%%a" "!name!"
)
```

### heiping.bat
```bat
start C:\Windows\System32\scrnsave.scr /s
```

### tree.bat
```bat
dir /o:-d 文件夹/b>list.txt
```

### testping.bat
来网通知
```bat
@setlocal enableextensions enabledelayedexpansion
@echo off
set ipaddr=www.baidu.com
set oldstate=neither
:loop
ping -n 1 !ipaddr! >nul: 2>nul:
if !errorlevel!==0 start wmplayer e:\system.wav
timeout 2
goto :loop
endlocal
```

### testping2.bat
网络状态改变通知
```bat
@setlocal enableextensions enabledelayedexpansion
@echo off
set ipaddr=www.baidu.com
set oldstate=neither
:loop
set state=up
ping -n 1 !ipaddr! >nul: 2>nul:
if not !errorlevel!==0 set state=down
if not !state!==!oldstate! (
    echo.Link is !state!
    start wmplayer e:\system.wav
    set oldstate=!state!
)
ping -n 2 127.1 >nul: 2>nul:
goto :loop
endlocal
```

### youtube-dl.bat
youtube-dl
```bat
@echo off
:download
set /p input=input video link:
set input=%input:&=^^^&%
youtube-dl --proxy socks5://127.0.0.1:10808 -f bestvideo[ext=mp4]+bestaudio[ext=m4a]/bestvideo+bestaudio --merge-output-format mp4 %input%
goto :download
```

### 图片第一帧生成图片
```bat
ffmpeg -i a.mp4 -y -f image2 -frames 1 a.jpg
```

### pdf 转 epub
```bat
docker run -ti --rm -v /share:/temp dodeeric/pdf2epubex pdf2epubEX 1.pdf
```