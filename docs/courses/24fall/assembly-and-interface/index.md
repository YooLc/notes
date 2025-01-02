# 汇编与接口

!!! 课程简介
    本课程由 [蔡铭](https://person.zju.edu.cn/0002444) 老师主讲，课程内容正如其名，鲜明地分成了两个模块:
    
    - **汇编模块**: 主要在前 8 周讲授，覆盖 x86 汇编语言的基本内容。相较于小白老师的《汇编语言》，本课程会额外扩展保护模式、长模式等有关 32 位和 64 位 x86 系统的内容，还涉及了 x86 汇编的编码规则，函数调用规则，内存寻址方式等等。 但同时，本课程设计上手编写汇编程序的部分只有第一个大作业，不会像《汇编语言》一样有很多练手的机会。这一部分适合选修过《汇编语言》或《汇编语言程序设计基础》的同学来进阶。

    - **接口模块**: 主要在后 8 周讲授，主要包括 8088 / 8086 时代的常见硬件接口芯片: 82C55 通信芯片，8254 计数芯片，16550 时钟芯片以及 DAC0830 数模转换芯片。这一部分偏硬件，需要一定《数字逻辑设计》的基础。课程会介绍以上芯片的器件构成，引脚功能，运行方式以及使用 8088 / 8086 微处理器进行编程的方法。这一部分会让我们对 x86 处理器 `in, out` 指令有更深的理解，同时补充一些软硬件结合的知识。

!!! tip "课程考核"
    平时占比 30%, 期末占比 70%。 平时成绩由两次 Project 组成，每个 Project 基本上有半个学期的时间来完成。期末考试的形式由老师在课上与同学们协商，老师说闭卷考试会提供必要的信息，无需死记硬背，同时题目会相对比较简单，因此本学期同学们选择了闭卷形式。