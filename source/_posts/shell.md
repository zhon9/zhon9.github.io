---
title: shell
date: 2020-04-24 21:19:55
tags: [shell]
---
<!-- more -->
ffmpeg 视频转gif
```bash
#!/bin/sh
start_time=18:32
duration=10
palette="palette.png"
filters="fps=15,scale=320:-1:flags=lanczos"

ffmpeg -v warning -ss $start_time -t $duration -i 1.mp4 -r 20 -vf "$filters,palettegen" -y palette.png
ffmpeg -v warning -ss $start_time -t $duration -i 1.mp4 -i palette.png -r 15 -lavfi "$filters [x]; [x][1:v] paletteuse" -y 1.gif
```
