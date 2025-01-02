# 课件例题

## λ 演算

1. $\lambda$ 演算消歧约定:

    - ⼀个函数抽象的函数体将尽最⼤可能向右扩展
        - $\lambda x.MN$ 是函数抽象 $\lambda x.(MN)$
        - $(\lambda x.M)N$ 是函数应用
    - 函数应⽤是左结合的
        - $MNP$ 意味着 $(MN)P$ 而非 $M(NP)$
    
    例子:

    - $\lambda x.(\lambda y.xyz)x = \lambda x.((\lambda y.((xy)z))x)$
    - $(\lambda x.\lambda y.\lambda z. M)NPQ = ((((\lambda x.\lambda y.\lambda z M)N)P)Q)$

2. 自由变量与绑定变量:

3. 闭项: t 封闭: $FV(t)=\varnothing$. $t$ 相对 $t'$ 封闭: $FV(t)\cap BV(t')=\varnothing$