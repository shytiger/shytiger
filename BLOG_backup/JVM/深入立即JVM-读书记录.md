---
title: <<深入立即JVM>>读书记录
date: 2020-10-30 15:14:35
tags:
---

# 引言
- 解释器与编译器
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201030154041907.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwODkyNTEx,size_16,color_FFFFFF,t_70#pic_center)
  - 解释器： 
    - 在线运行程序
    - 每次数据不一样时，解释器仍然需要加载程序解释运行
  - 编译器：
    - 离线，先 将程序编译 生成 可执行程序（exe,字节码或会变语言）
    - 每次数据不一样时，只用加载可执行文件 和数据 就可以运行，不用重新编译


- Exact VM 准确内存管理
- HotSpot 热点探测技术
- 即时编译与提前编译(AOT)
  - 即时编译： i
    - 优点：减少即使编译带来的预热时间，改善“第一次运行慢”
    - 缺点：破坏了“一次编写，导出运行”，显著降低了Java链接过程的动态性

# 第一章 走进Java
- 自己编译JDK
  [JDK都没手动编译过，敢说自己是Java程序员吗？实战编译Java源码（JDK源码,JVM）视频教程](https://www.bilibili.com/video/BV1zT4y177Zf)
-[JVM参数设置官方文档](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html)
- [Java虚拟机规范官方](https://docs.oracle.com/javase/specs/jvms/se8/html/)