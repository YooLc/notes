# 期末历年卷

## 2023-2024 秋冬学期

来源: [23-24秋冬 汇编与接口 回忆卷](https://www.cc98.org/topic/5804583)

### 填空题 (10*2)

1. A7 BCD, unpacked BCD

2. 保护模式下，() 寄存器指向栈当前位置，（）寄存器指向当前栈帧顶部

3. segment register contains () for descriptor

5. 保护模式下，base = 00360000, limit=10H, G=1, 段的范围（十六进制）

6. 假设端口地址分别为 300H，302H，304H，308H，应该把哪两个地址接入到 A1 A0

6. basic input device (), basic output device

7. 8254 contains () counter, each is ()-bit

8. 实模式下，中断向量的地址在 0A0H-0A3H，求中断向量号

9. 写出指令，能把 F2h 写入到 bp 为基地址的一个字的数据写到寄存器 ax 中。

???+ note "答案"

    答案仅供参考，如果有问题欢迎提出~

    1. 0xA7 = 167, Packed BCD: 0x0167, Unpacked BCD: 0x010607
    2. esp, ebp
    3. 选择值 (selector)
    4. TODO
    5. AD1 接入 A0, AD2 接入 A1. 使用偶地址端口是为了避免将 $\overline{\text{BHE}}$ 信号也加入解码
    6. 题意不是很清楚
    7. 3, 16
    8. 0A0h / 4 = (1010 0000)$_2$ / 4 = (0010 1000)$_2$ = 0x28 = 40 号中断
    9. 题意不是很清楚


### 选择题 (15*2)

1. () 把汇编语言翻译成机器语言
2. A=… B=… 求 CF 和 OF
3. 哪个向量化指令集是向量长度可以在运行时变化（选项有 AVX SSE SVE）
4. 哪个指令不会改变 AL 的值

    A. xchg AL, AL

    B. cmp AL, 0

    C. test AL, AL

    D. 以上都对

5. 下面哪个寻址是对的

    A. mov ax, [eax + esp + 2]

    B. mov ax, [eax + esp * 2 + 2]

    C. mov ax, [eax + esp * 4]

    D. mov ax, [eax + esp * 8 + 2]

6. 以下哪个指令不会改变 CF (选项有 neg add 正确答案忘了)

7. 下面指令等价于 `edx <- edx + 4*ebx + 8`

    A. `mov edx, [edx + 4*ebx + 8]`

    B. `lea edx, [edx + 4*ebx + 8]`

    C. `mov edx, offset edx + 4*ebx + 8`

    D. `add edx, 4*ebx + 8`

???+ note "答案"

    1. 汇编器
    2. 略, 注意 CF 是无符号溢出, OF 是有符号溢出
    3. SVE: 可选向量长度，只需要保持是 128 的倍数
    4. D 都不改变: xchg AL, AL 不改变 AL 的值，cmp AL, 0 会改变 ZF, test AL, AL 会改变 ZF
    5. A, 因为 esp 不能在 (base, scale, index, disp) 中作为 index 寄存器
    6. `inc` 和 `dec` 不改变 CF
    7. B, lea 用于计算有效地址，而地址恰好是 edx + 4*ebx + 8

### 大题

1. 页表为 10-10-13，9-9-9-21 写出对应的页大小，页表级数，虚拟地址空间大小
2. 给了从内存 30100h 到 301A0 的地址里的数据 ds = 3000h, ss=3001h, bx=100h, si=2h, bp=0F2h。下面一段指令，写出操作后 ax 的值
```asm
    mov ax, [bx] 
    mov ax, 1[bx]
    mov ax, [bx][si]
    mov ax, [bp]
```

3. 给出一段指令，写出操作后 eax 的值
```asm
test eax, eax
jg .L1
je .L2
lea eax, [edi + 5]
ret 
L2: 
    mov eax, edi
    sar eax, 2
    ret
L1:
    mov eax, edi
    ret
```

(1) edi=0 (2) edi=100 (3) edi=-30

???+ note "答案"

    1. 
        1. 10-10-13:
            - 页大小: $2^{13} = 8$ KiB.
            - 页表级数: 2 级页表
            - 虚拟地址空间大小 $2^{33} = 8$ GiB
        2. 9-9-9-21:
            - 页大小: $2^{21} = 2$ MiB
            - 页表级数: 3 级页表
            - 虚拟地址空间大小 $2^{48} =  256$ TiB
    2. 

    ```asm
        mov ax, [bx]     ; ax <- MEM[30100h], [bx] = ds:[bx]
        mov ax, 1[bx]    ; ax <- MEM[30101h], 1[bx] = ds:[bx + 1]
        mov ax, [bx][si] ; ax <- MEM[30102h], [bx][si] = ds:[bx + si]
        mov ax, [bp]     ; ax <- MEM[30102h], [bp] = ss:[bp], 3001:00F2h = 30102h
    ```
    

### 代码填空

1. 82C55 端口地址分别是 4000h, 4001h, 4002h, 40003h, Group A B 均在 mode 0 下
    1. 假设 A 是输入，B C 是输出。
    2. 把数据从 A 中读入，并将这个数据输出到 B C 中。

2. 8254 的端口地址分别为 4000h, 4001h, 4002h, 4003h，输入频率是 2Mhz
    1. 假设 Counter 2 使用模式 0，count 是 50000（C350h），写出配置的过程
    2. 我们从 Counter 2 中读数据。
    3. 假设用 Counter 0，要频率为 8Khz，写出配置的过程。

3. 16550 给了一段代码，（具体不记得了，最开始写入的控制字是 10001000，设置的 divisor 值时先写了 00h，再写了 0F0h）
    1. 求 divisor 和 baud rate
    2. 多少个 start bit，data bits，多少个 parity bit（如果有，是 even/odd），多少个 stop bit
    3. 给了一段波形，问接收到的数据位是多少。

## 2022-2023 秋冬学期

来源: [22-23秋冬 汇编与接口 回忆卷 & 笔记](https://www.cc98.org/topic/5510882)

### 不定项选择

中断向量18H的中断向量表地址是多少？
AX是0x1000, ADD AX, AX后，CF和OF标志位各是多少？
long mode中，默认的地址的长度和默认的Operand size都是多少？（64位，32位）
哪个寻址指令是错的？（ESP的问题）
哪一条指令能分配嵌套的栈？（ENTER）
MOV [53H], AL 指令，此时的BHE和BLE信号
TEST AX, AX相当于？（相当于CMP AX, 0）
什么指令能把结构冒险转换为数据冒险？（条件移动指令cmove）
一个vector能容纳的最大元素的个数称作？（vectorization factor）
哪一个指令集支持可变长vector？（AVX）
82C55的端口地址分别是XXX，XXX...，那么应该使用哪两根数据线？（端口地址相隔4位，用A2和A3）
8254的largest initial counts，相当于BCD码的多少（应该是0和10000）
哪个不是16550支持的error？（支持的有Overrun, Parity, Framing）
哪些是x86架构支持的模式（选项：Long mode, virtual 8086 mode, real mode, protected mode）
不同粒度（G, granularity bit）下的segment size计算
How to access the SIMD units? (Four choices)
哪条指令是原子操作？（选项好像是INC, XCHG, XADD, CMPXCHG）
哪些属于指令前缀？（REP，LOCK，Operand-size Override）
检测数据依赖的方法有哪些？（GCD, Delta, Banerjee）
CPU 和设备通信的方式有哪些？（Isolated I/O, Memory mapped I/O）

### 代码填空

1. 82C55

2. 8254

3. 16550