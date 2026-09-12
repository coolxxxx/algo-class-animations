# VOX 流式白板动画管线

工具：`geeklee/srt-whiteboard-animation`
本地路径：`F:\mangju\04_工具\画布工具\srt-whiteboard-animation\`

## 做一课

1. 准备无字线稿（暖纸底 #F5EBD7 / 极简手绘）
2. 写 `scene-xx.annotation.json`（region / sequence / startMs）
3. 渲染：
```powershell
$venv = "F:\mangju\04_工具\画布工具\srt-whiteboard-animation\.venv\Scripts\python.exe"
$skill = "F:\mangju\04_工具\画布工具\srt-whiteboard-animation"
& $venv $skill\scripts\render_stream_whiteboard.py image.png image.annotation.json out.mp4 --fps 24 --cap-long-edge 720
```
4. 多幕 ffmpeg concat 合并
5. 可选：用 text-whiteboard-video 的 tts/mix 加解说

## 与旧管线差别

| 旧 text-whiteboard-video | VOX srt-whiteboard |
|---|---|
| 整块软擦除 / 淡入 | **连续落笔 + 手部跟随** |
| 适合水彩整图 | 适合极简线稿 |
| ink:color 约 2:1 语义 | grid/skeleton 路径 + contour-wipe |

源项目：https://github.com/geeklee/srt-whiteboard-animation
