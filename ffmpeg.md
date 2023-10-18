视频推流（ts）

ffmpeg -re -stream_loop -1 -i 文件名  -f rtp_mpegts rtp://组播IP:PORT

-stream_loop number 循环次数 -1 无限循环

-re 按照帧率发送

-i 数据源 摄像头（“/dev/video0”）

-f 文件格式

-s 分辨率 720x480

