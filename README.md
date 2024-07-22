# FileTransfer_Fix-bugs
对jerryos的FileTransfer项目修复bug：epoll+线程池实现大文件传输（修复bug）
# 日期
2024.7.22
# 原作者项目地址
[FileTransfer](https://github.com/jerryos/FileTransfer)
# 说明
最近学习利用tcp文件传输，个人用Ubuntu向Linux开发板（性能弱爆了）传输文件，自己写的程序是读取源文件，一帧一帧（1KB）发送给开发板端，但是开发板cpu满速运行，一个6.4MB的文件竟然发送了46秒，然后用ftp测试了下，同一个文件竟然满cpu下才用了6秒钟，备受打击，不能接受。于是在GitHub上发现jerryos的FileTransfer项目，测试了下，6.4M的文件才用了1秒，开发板端cpu还没来得及百分之百就结束了，太惊艳了。但是有个致命问题：传输的文件不完整，MD5值不对，而且传输文件后，服务端cpu一直百分之百。另外issue上也有人提了这个问题，但是没有解决，而且是九年前的项目了，于是自己便拜读了源码，发现是客户端问题。最后一个块处理时，漏掉了对于最后一次发送时存在不满足小块情况的处理，于是修复了这个问题，测试传输两端MD5正常
