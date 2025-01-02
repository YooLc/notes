# 判定训练

题目来自: [COMP481 Review Problems - Luay K. Nakhleh](https://www.cs.rice.edu/~nakhleh/COMP481/final_review_sp06.pdf)

答案: [COMP481 Review Problems (Solution) - Luay K. Nakhleh](https://www.cs.rice.edu/~nakhleh/COMP481/final_review_sp06_sol.pdf)

## 判定工具

### Rice's Theorem

### 总结

[判定问题 - 鹤翔万里的笔记本](https://note.tonycrane.cc/cs/tcs/toc/topic4/)

## 训练题

??? tips "比较有意义的题"
    $L_1$ 到 $L_4$ 的分析是后面很多题目的基础, 还有 $L_{26}$ 构造值得学习.

    $L_{39}$ 作为一个递归语言，其分析不是很容易，可以学习一下.

对以下给定的语言，判断它们: (I) 递归, (II) 递归可枚举且非递归, (III) 非递归可枚举. 根据 Few Shot 的学习方式，我展开了前几题的答案，可以摸索一下大致思路.

1. \( L_1 = \{ '' M '' \mid M \) is a TM and there exists an input on which \( M \) halts in less than \( |'' M ''| \) steps \(\} \)

    ???+ note "Answer"
        $L_1$ 是**递归**的，存在图灵机 $M^*$ 判定 $L_1$:
        
        1. 给定输入 $w$, 如果 $w$ 不是合法图灵机编码，拒绝 (之后省略这步)
        2. 计算 $|'' M ''|$
        3. 枚举 $M$ 的所有长度不超过 $|'' M ''|$ 的输入，模拟 $M$ 的运行，如果在 $|'' M ''|$ 步内停机，接受，否则拒绝

        这个例子重点在于步数有限，同时这也意味着输入串长度有限 (枚举更长的输入串没有意义，因为走不到)，图灵机可以一一枚举.

2. \( L_2 = \{ '' M '' \mid M \) is a TM and \( |L(M)| \leq 3 \) \(\} \)

    ???+ note "Answer"
        $L_2$ 是**非递归可枚举**的, 下面证明 $\overline{H} \le L_2$, 即 $\overline{H}$ 可以归约到 $L_2$.
        
        对于 $\overline{H}$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M'\ ''$, $M'$ 对于输入 $x$:

        1. 擦掉输入串 $x$
        2. 将 $''Mw''$ 拷贝到带上
        3. 模拟 $M$ 在 $w$ 上的运行，如果 $M$ 在 $w$ 上停机，接受，否则拒绝

        规约的证明:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 不接受任何串 $\Rightarrow |L(M')|\le 3 \Rightarrow M' \in L_2$
        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M'$ 接受所有串 $\Rightarrow |L(M')|>3 \Rightarrow M' \notin L_2$

        **扩展**: 如果将语言改为 \( L = \{ '' M '' \mid M \) is a TM and \( |L(M)| = 3 \) \(\} \): 可以任选一个有 3 个串的集合 $A$, 在 $M'$ 的第一步前添加如果 $x \in A$ 就接受, 这样一来 $''Mw'' \in \overline{H} \Rightarrow L(M') = 3$.

3. \( L_3 = \{ '' M '' \mid M \) is a TM and \( |L(M)| \geq 3 \) \(\} \)

    ???+ note "Answer"
        $L_3$ 是**递归可枚举且非递归**的.
        
        **递归可枚举**:

        构造图灵机 $M'$, 对于输入 $''M''$:

        1. 枚举所有 $M$ 可能的输入串 $x$, 模拟 $M$ 的运行
        2. 如果找到了至少 3 个停机的输入，就接受

        上面的枚举需要是“对角线式”的，先枚举所有长度为 1 的串，单步模拟，再枚举长度为 2 的串，两步模拟，以此类推. (后面的题都如此, 就不再一一约定了)

        **非递归**:
        
        证明 $H \le L_3$, 即 $H$ 可以归约到 $L_3$.

        对于 $H$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M'\ ''$, $M'$ 对于输入 $x$:

        1. 擦掉输入串 $x$
        2. 将 $''Mw''$ 拷贝到带上
        3. 模拟 $M$ 在 $w$ 上的运行，如果 $M$ 在 $w$ 上停机，接受，否则拒绝

        规约的证明:

        - $''Mw'' \in H \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M'$ 接受所有串 $\Rightarrow |L(M')|\ge 3 \Rightarrow M' \in L_3$
        - $''Mw'' \notin H \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 不接受任何串 $\Rightarrow |L(M')|<3 \Rightarrow M' \notin L_3$

        这一部分的构造和上一题很相似，只不过是从 $\overline{H}$ 换成了 $H$, 这取决于条件中的不等号方向.

4. \( L_4 = \{ '' M '' \mid M \) is a TM that accepts all even numbers \(\} \)

    ???+ note "Answer"
        $L_4$ 是**非递归可枚举的**. 需证明 $\overline{H} \le L_4$.

        对于 $\overline{H}$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M'\ ''$, $M'$ 对于输入 $x$:

        1. 计算 $|x|$
        2. 模拟 $M$ 在 $w$ 上运行 $|x|$ 步
        3. 如果 $|x|$ 步内停机，就拒绝，否则接受

        规约的证明:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 接受所有串, 那自然也就接受了全部偶数 $\Rightarrow M' \in L_4$
        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上 $k$ 步内停机 $\Rightarrow M'$ 拒绝所有 $|x| \ge k$ 的串 $w$ $\Rightarrow M'$ 拒绝无限多个偶数 $\Rightarrow M' \notin L_4$

        **注**: 这里将是否接受与输入串 $w$ 长度结合的技巧值得学习.
        
        **扩展**:

        1. 修改为 $L = \{ '' M '' \mid M$ is a TM that does not accept all even numbers$\}$: 此时变成递归可枚举，可以用图灵机 $M;$ 枚举所有偶数输入给 $M$, 如果 $M$ 不接受某个偶数，就接受. 这样可以半判定 $M$ 接受的是不是所有偶数.

        2. 修改为 $L = \{ '' M '' \mid M$ is a TM that rejects all even numbers$\}$: 此时变成 RE 非 R, 可以证明 $H \le L$. 这个改版和原版的关系，与 $L_3$ 和 $L_2$ 的关系相似.

5. \( L_5 = \{ '' M '' \mid M \) is a TM and \( L(M) \) is finite \(\} \)

    ??? note "Answer"
        $L_5$ 是**非递归可枚举**的，类似 $L_2$ 的构造:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 不接受任何串 $\Rightarrow L(M') = 0$ 有限 $\Rightarrow M' \in L_5$
        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M'$ 接受所有串 $\Rightarrow L(M')$ 并非有限, $\Rightarrow M' \notin L_5$

6. \( L_6 = \{ '' M '' \mid M \) is a TM and \( L(M) \) is infinite \(\} \)

    ??? note "Answer"
        $L_6$ 也是**非递归可枚举**的，是不是和想的不太一样?

        用 $L_3$ 的构造可以证明 $H \le L_6$, 这只意味着 $L_6$ 是非递归的:

        - $''Mw'' \in H \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M'$ 接受所有串 $\Rightarrow L(M')$ 无限 $\Rightarrow M' \in L_6$
        - $''Mw'' \notin H \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 不接受任何串 $\Rightarrow L(M') = 0$ 有限 $\Rightarrow M' \notin L_6$

        但事实上也可以找到规约证明 $\overline{H} \le L_6$, 而这和 $L_4$ 类似:

        对于 $\overline{H}$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M'\ ''$, $M'$ 对于输入 $x$:

        1. 计算 $|x|$
        2. 模拟 $M$ 在 $w$ 上运行 $|x|$ 步
        3. 如果 $|x|$ 步内停机，就接受，否则拒绝

        规约的证明:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 不接受任何串 $\Rightarrow L(M') = 0$ 有限 $\Rightarrow M' \in L_6$
        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上 $k$ 步内停机 $\Rightarrow M'$ 接受所有 $|w| \ge k$ 的串 $w$ $\Rightarrow L(M')$ 无限 $\Rightarrow M' \notin L_6$

7. \( L_7 = \{ '' M '' \mid M \) is a TM and \( L(M) \) is countable \(\} \)

    ??? note "Answer"
        $L_7$ 是**递归**的: 这是全部图灵机编码的集合，注意:
        - 对于一个语言，其内容是可数无限多的，比如对于 $\Sigma^*$ 可以按照字典序一一枚举串长为 $1, 2, \cdots$ 的串，给它们编号，就建立了与 $N_+$ 的一一映射.
        - 而语言的个数是不可数无穷多的, 是 $2^{\Sigma^*}$.

8. \( L_8 = \{ '' M '' \mid M \) is a TM and \( L(M) \) is uncountable \(\} \)

    ??? note "Answer"
        $L_8$ 是**递归**的: $L_8=\varnothing$, 没有一个语言有不可数无穷多个元素.

9. \( L_9 = \{ '' M_1, M_2 '' \mid M_1 \) and \( M_2 \) are two TMs, and \( \varepsilon \in L(M_1) \cup L(M_2) \} \)

    ??? note "Answer"
        $L_9$ 是**递归可枚举非递归**的:

        **递归可枚举**:

        构造图灵机 $M'$ 可以半判定, 对于输入 $''M_1, M_2''$, 并行模拟 $M_1$ 和 $M_2$:

        1. 模拟 $M_1$ 输入为 $\varepsilon$
        2. 模拟 $M_2$ 输入为 $\varepsilon$
        3. 两台机器有一个停机就停机

        **非递归**:

        证明 $H \le L_9$, 即 $H$ 可以归约到 $L_9$.

        对于 $H$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M', M'\ ''$, $M'$ 对于输入 $x$:

        1. 模拟 $M$ 在 $w$ 上的运行，如果停机就接受，否则拒绝

        规约的证明:

        - $''Mw'' \in H \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M_1$ 和 $M_2$ 接受所有的串 $\Rightarrow \varepsilon \in L(M_1) \cup L(M_2) \Rightarrow ''M_1, M_2'' \in L_9$
        - $''Mw'' \notin H \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M_1$ 和 $M_2$ 拒绝所有输入 $\Rightarrow \varepsilon \notin L(M_1) \cup L(M_2) \Rightarrow ''M_1, M_2'' \notin L_9$

10. \( L_{10} = \{ '' M_1, M_2 '' \mid M_1 \) and \( M_2 \) are two TMs, and \( \varepsilon \in L(M_1) \cap L(M_2) \} \)

    ??? note "Answer"
        $L_{10}$ 是**递归可枚举非递归**的，与 $L_9$ 类似，只不过证明递归可枚举改成两台都停机才停机.

11. \( L_{11} = \{ '' M_1, M_2 '' \mid M_1 \) and \( M_2 \) are two TMs, and \( \varepsilon \in L(M_1) \setminus L(M_2) \} \)

    ??? note "Answer"
        $L_{11}$ 是**非递归可枚举**的，条件等价于 $\varepsilon \in L(M_1) $ 且 $\varepsilon \notin L(M_2)$, 证明 $\overline{H} \le L_{11}$:

        对于 $\overline{H}$ 的输入 $''Mw''$, 构造映射 $\tau(''Mw'') = ''M_1, M_2''$, 对于输入 $x$:

        1. 模拟 $M$ 在 $w$ 上的运行
            - 如果 $M$ 停机，$M_1$ 拒绝，而 $M_2$ 接受
            - 如果 $M$ 不停机，$M_1$ 接受，$M_2$ 拒绝
        
        规约的证明:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow$ $M_1$ 接受所有串，$M_2$ 拒绝所有串 $\Rightarrow \varepsilon \in L(M_1) \setminus L(M_2) = \Sigma^* \Rightarrow ''M_1, M_2'' \in L_{11}$
        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow$ $M_1$ 拒绝所有串，$M_2$ 接受所有串 $\Rightarrow \varepsilon \notin L(M_1) \setminus L(M_2) = \varnothing \Rightarrow ''M_1, M_2'' \notin L_{11}$

12. \( L_{12} = \{ '' M '' \mid M \) is a TM, \( M_0 \) is a TM that halts on all inputs, and \( ''M_0'' \in L(M) \} \)

    ??? note "Answer"
        $L_{12}$ 是**递归可枚举非递归**的.

        **递归可枚举**:
        
        构造图灵机 $M'$ 半判定, 对于输入 $''M''$:
        
        1. 模拟 $M$ 输入 $''M_0''$ 的情况, 如果 $M$ 停机就接受.

        **非递归**:

        使用 Rice's Theorem 可以证明.

13. \( L_{13} = \{ '' M '' \mid M \) is a TM, \( M_0 \) is a TM that halts on all inputs, and \( ''M'' \in L(M_0) \} \)

    ??? note "Answer"
        $L_{13}$ 是**递归**的. $L(M_0) = \Sigma^*$, 所以 $L_{13}$ 是所有图灵机编码的集合.

14. \( L_{14} = \{ '' M, x '' \mid M \) is a TM, \( x \) is a string, and there exists a TM, \( M' \), such that \( x \notin L(M) \cap L(M') \} \)

    ??? note "Answer"
        $L_{14}$ 是**递归**的, 取 $M'$ 拒绝所有输入的图灵机，这样的话，所有 $''Mx''$ 都属于 $L_{14}$.

15. \( L_{15} = \{ '' M '' \mid M \) is a TM, and there exists an input on which \( M \) halts within 1000 steps \(\} \)

    ??? note "Answer"
        $L_{15}$ 是**递归**的，构造图灵机 $M$ 枚举所有 $w (|w| \le 1000)$, 模拟 $M$ 的运行，如果在 $1000$ 步内停机，接受, 如果都不存在，就拒绝.

16. \( L_{16} = \{ '' M '' \mid M \) is a TM, and there exists an input whose length is less than 100, on which \( M \) halts \(\} \)

    ??? note "Answer"
        $L_{16}$ 是**递归可枚举非递归**的.

        **递归可枚举**:

        构造图灵机 $M'$ 半判定, 枚举所有 $w (|w| < 100)$, 模拟 $M$ 的运行，如果存在一个 $w$ 使其停机，就接受.

        **非递归**:

        证明 $H \le L_{16}$, 即 $H$ 可以归约到 $L_{16}$.

        对于 $H$ 问题的输入 $''Mx''$, 映射 $\tau(''Mx'') = ''M'\ ''$, $M'$ 对于输入 $w$:

        1. 模拟 $M$ 在 $x$ 上的运行，停机与否都与 $M$ 一致

        规约的证明:

        - $''Mx'' \in H \Rightarrow M$ 在 $x$ 上停机 $\Rightarrow M'$ 对所有输入都停机 $\Rightarrow \exists w,\ |w| < 100, M$ 在 $w$ 上停机 $\Rightarrow ''M'' \in L_{16}$
        - $''Mx'' \notin H \Rightarrow M$ 在 $x$ 上不停机 $\Rightarrow M'$ 对所有输入都不停机 $\Rightarrow \forall w,\ |w| < 100, M$ 在 $w$ 上不停机 $\Rightarrow ''M'' \notin L_{16}$

17. \( L_{17} = \{ '' M '' \mid M \) is a TM, and \( M \) is the only TM that accepts \( L(M) \} \)

    ??? note "Answer"
        $L_{17}$ 是**递归**的，$L_{17}=\varnothing$, 没有一个图灵机是唯一接受自己语言的, 因为可以对起做一点点改动，中间加一些无意义动作，最后还是可以接受相同的语言.

18. \( L_{18} = \{ (k, x, M_1, M_2, \ldots, M_k) \mid k \) is a natural number, \( x \) is a string, \( M_i \) is a TM for all \( 1 \leq i \leq k \), and at least \( k/2 \) TMs of \( M_1, \ldots, M_k \) halt on \( x \) \(\} \)

    ??? note "Answer"
        $L_{18}$ 是**递归可枚举非递归**的.

        **递归可枚举**:

        构造图灵机 $M'$ 半判定, 对于输入 $(k, x, M_1, M_2, \ldots, M_k)$, 并行模拟每台图灵机对于输入 $x$ 的运行情况，一旦有至少 $k/2$ 台停机，就接受.

        **非递归**:

        证明 $H \le L_{18}$, 即 $H$ 可以归约到 $L_{18}$.

        对于 $H$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = (1, w, M')$, $M$ 对于输入 $x$:

        1. 模拟 $M$ 在 $w$ 上的运行，如果停机就接受，否则拒绝

        规约的证明:

        - $''Mw'' \in H \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M'$ 停机 $\Rightarrow (1, w, M') \in L_{18}$
        - $''Mw'' \notin H \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 不停机 $\Rightarrow (1, w, M') \notin L_{18}$

19. \( L_{19} = \{ ''M'' \mid M \) is a TM, and \( |M| < 1000 \) \(\} \)

    ??? note "Answer"
        $L_{19}$ 是**递归**的，可以构造图灵机 $M$ 按照字典序枚举所有合法的长度 $< 1000$ 的图灵机编码.

20. \( L_{20} = \{ ''M'' \mid \exists x, \, |x| \equiv_5 1, \, \text{and } x \in L(M) \} \)

    ??? note "Answer"
        $L_{20}$ 是**递归可枚举非递归**的.

        **递归可枚举**:

        构造图灵机 $M'$ 半判定, 对于输入 $''M''$: 枚举所有符合条件的输入 $x$, 如果找到一个 $x$ 使得 $|x| \equiv_5 1$ 且 $x \in L(M)$, 就接受.

        **非递归**:

        使用 Rice's Theorem 或者构造一个规约，证明 $H \le L_{20}$ 都可以, 构造的话可以参考 $L_{16}$.


21. \( L_{21} = \{ ''M'' \mid M \) is a TM, and \( M \) halts on all palindromes \(\} \)

    ??? note "Answer"
        $L_{21}$ 是**非递归可枚举**的, 这道题很像 $L_4$:

        可以证明 $\overline{H} \le L_{21}$, 即 $\overline{H}$ 可以归约到 $L_{21}$.

        对于 $\overline{H}$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M'\ ''$, $M'$ 对于输入 $x$:

        1. 计算 $|x|$
        2. 模拟 $M$ 在 $w$ 上的运行 $|x|$ 步
        3. 如果 $|x|$ 步内停机，就拒绝，否则接受

        规约的证明:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 接受所有串 $\Rightarrow M'$ 在所有回文串上停机 $\Rightarrow ''M'' \in L_{21}$
        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M'$ 拒绝所有 $|x| \ge k$ 的串 $w$ $\Rightarrow \exists$ 回文串 $ww^R$ 被 $M'$ 拒绝 $\Rightarrow ''M'' \notin L_{21}$

22. \( L_{22} = \{ ''M'' \mid M \) is a TM, and \( L(M) \cap \{ a^{2^n} \mid n \geq 0 \} \) is empty \(\} \)

    ??? note "Answer"
        $L_{22}$ 是**非递归可枚举**的, 构造类似 $L_2$, 让 $L(M)$ 分别是 $\varnothing$ 和 $\Sigma^*$ 分类讨论.

23. \( L_{23} = \{ ''M, k'' \mid M \) is a TM, and \( |\{ w \in L(M) : w \in a^*b^* \}| \geq k \) \(\} \)

    ??? note "Answer"
        $L_{23}$ 是**递归可枚举非递归**的.

        **递归可枚举**: 按照长度枚举所有 $a^*b^*$, 模拟 $M$ 看其是否接受, 统计 $L(M)$ 中的符合条件的串数目，如果大于等于 $k$ 就接受.

        **非递归**: 构造类似 $L_2$.

24. \( L_{24} = \{ ''M'' \mid M \) is a TM that halts on all inputs and \( L(M) = L' \) for some undecidable language \( L' \) \(\} \)

    ??? note "Answer"
        $L_{24}$ 是**递归**的，既然 $M$ 对所有的输入都停机，那么 $L(M)$ 是可判定的，因此 $L_{24}=\varnothing$.

25. \( L_{25} = \{ ''M'' \mid M \) is a TM, and \( M \) accepts (at least) two strings of different lengths \(\} \)

    ??? note "Answer"
        $L_{25}$ 是**递归可枚举非递归**的.

        **递归可枚举**: 构造图灵机 $M'$ 半判定, 对于输入 $''M''$:按照长度枚举串，并记住某个长度是否存在一个串被 $M$ 接受，如果有两个不同长度的串被接受，就接受.

        **非递归**: 构造类似 $L_2$, 也可用 Rice's Theorem.

26. \( L_{26} = \{ ''M'' \mid M \) is a TM such that both \( L(M) \) and \( \overline{L(M)} \) are infinite \(\} \)

    ??? note "Answer"
        $L_{26}$ 是**非递归可枚举**的

        证明 $\overline{H} \le L_{26}$, 即 $\overline{H}$ 可以归约到 $L_{26}$.

        对于 $\overline{H}$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M'\ ''$, $M'$ 对于输入 $x$:

        1. 计算 $|x|$
        2. 如果 $|x|$ 是奇数，就接受
        3. 否则，模拟 $M$ 在 $w$ 上运行，如果停机就接受，否则拒绝

        规约的证明:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 接受所有奇数长度的串 $\Rightarrow L(M')$ 和 $\overline{L(M')}$ 都是无限的 $\Rightarrow ''M'\ '' \in L_{26}$
        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M'$ 接受所有串 $\Rightarrow \overline{L(M')} = \varnothing$ 有限 $\Rightarrow ''M'\ '' \notin L_{26}$

27. \( L_{27} = \{ ''M, x, k'' \mid M \) is a TM, and \( M \) does not halt on \( x \) within \( k \) steps \(\} \)

    ??? note "Answer"
        $L_{27}$ 是**递归**的，构造图灵机 $M'$ 模拟 $M$ 在 $x$ 上的运行，如果在 $k$ 步内停机，就拒绝，否则接受.

28. \( L_{28} = \{ ''M'' \mid M \) is a TM, and \( |L(M)| \) is prime \(\} \)

    ??? note "Answer"
        $L_{28}$ 是**非递归可枚举**的，证明类似 $L_2$ 的扩展 $|L(M) = 3|$ 的情况.

        如果想在 $|L(M)|$ 有限的情况下来证明，可以有下面的构造:

        对于 $\overline{H}$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M'\ ''$, $M'$ 对于输入 $x$:

        1. 如果 $x$ 是 $\Sigma^*$ 字典序前 $3$ 个串, 接受
        2. 如果 $x$ 是第 $4$ 个串，模拟 $M$ 在 $w$ 上的运行，如果停机就接受，否则拒绝
        3. 其他情况直接拒绝

        规约的证明:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 接受前 $3$ 个串 $\Rightarrow |L(M')| = 3$ 是素数 $\Rightarrow ''M'\ '' \in L_{28}$

        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M'$ 接受第 $4$ 个串 $\Rightarrow |L(M')| = 4$ 不是素数 $\Rightarrow ''M'\ '' \notin L_{28}$

29. \( L_{29} = \{ ''M'' \mid \) there exists \( x \in \Sigma^* \) such that for every \( y \in L(M), xy \notin L(M) \} \)

    ??? note "Answer"
        $L_{29}$ 是**非递归可枚举**的.

30. \( L_{30} = \{ ''M'' \mid \) there exist \( x, y \in \Sigma^* \) such that either \( x \in L(M) \) or \( y \notin L(M) \} \)

    ??? note "Answer"
        $L_{30}$ 是**递归**的, $L_{30}$ 是全部图灵机编码的集合. 取 $x=y$, 好话坏话全让它说了.

        **扩展**:

        修改为 $L = \{ '' M '' \mid M$ is a TM, and there exist $x, y \in \Sigma^*$ such that $x \in L(M)$ and $y \notin L(M)\}$.

        此时变为**非递归可枚举**的, 证明 $\overline{H} \le L$.

        对于 $\overline{H}$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M'\ ''$, $M'$ 对于输入 $x$:

        1. 如果 $x=\varepsilon$, 接受
        2. 否则，模拟 $M$ 在 $w$ 上的运行，如果停机就拒绝，否则接受

        规约的证明:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M'$ 只接受 $\varepsilon$ $\Rightarrow \exists x = \varepsilon, y = a, \varepsilon \in L(M)$ and $a \notin L(M) \Rightarrow ''M'\ '' \in L$
        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M'$ 接受所有串 $\Rightarrow \notexists y \in \Sigma^*$, $y \notin L(M) \Rightarrow ''M'\ '' \notin L$

31. \( L_{31} = \{ ''M'' \mid \) there exists a TM \( M'\) such that \( ''M'' \neq ''M'\ '' \) and \( L(M) = L(M') \} \)

    ??? note "Answer"
        $L_{31}$ 是**递归**的，$L_{31} = \overline{L__{17}}$.

32. \( L_{32} = \{ ''M_1, M_2'' \mid L(M_1) \leq_m L(M_2) \} \)

33. \( L_{33} = \{ ''M'' \mid M \) does not accept any string \( w \) such that 001 is a prefix of \( w \) \(\} \)

    ??? note "Answer"
        $L_{33}$ 是**非递归可枚举**的. 规约类似 $L_2$.

34. \( L_{34} = \{ ''M, x'' \mid M \) does not accept any string \( w \) such that \( x \) is a prefix of \( w \) \(\} \)

    ??? note "Answer"
        $L_{34}$ 是**非递归可枚举**的. 同样地, 规约类似 $L_2$.

35. \( L_{35} = \{ ''M, x'' \mid x \) is a prefix of \( ''M'' \) \(\} \)

    ??? note "Answer"
        $L_{35}$ 是**递归**的，构造图灵机 $M$ 直接判断 $x$ 是否为 $''M''$ 前缀即可.

36. \( L_{36} = \{ ''M_1, M_2, M_3'' \mid L(M_1) = L(M_2) \cup L(M_3) \} \)

    ??? note "Answer"
        $L_{36}$ 是**非递归可枚举**的.

        证明 $\overline{H} \le L_{36}$, 即 $\overline{H}$ 可以归约到 $L_{36}$.

        对于 $\overline{H}$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M_1, M_2, M_3''$, $M_1$ 对于输入 $x$:

        1. 模拟 $M$ 在 $w$ 上的运行，如果停机就接受，否则拒绝

        $M_2$ 和 $M_3$ 拒绝所有串.

        规约的证明:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M_1$ 拒绝任何输入 $\Rightarrow L(M_1) = \varnothing = L(M_2) \cup L(M_3) \Rightarrow ''M_1, M_2, M_3'' \in L_{36}$

        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M_1$ 接受所有串 $\Rightarrow L(M_1) = \Sigma^* \neq L(M_2) \cup L(M_3) \Rightarrow ''M_1, M_2, M_3'' \notin L_{36}$

37. \( L_{37} = \{ ''M_1, M_2, M_3'' \mid L(M_1) \subseteq L(M_2) \cup L(M_3) \} \)

    ??? note "Answer"
        $L_{37}$ 是**非递归可枚举**的. 类似 $L_36$ 的证明, 如果非要真子集的话，就改一下 $M_2$ 让它接受一个串就行:

        证明 $\overline{H} \le L_{37}$, 即 $\overline{H}$ 可以归约到 $L_{37}$.

        对于 $\overline{H}$ 问题的输入 $''Mw''$, 映射 $\tau(''Mw'') = ''M_1, M_2, M_3''$, $M_1$ 对于输入 $x$:

        1. 模拟 $M$ 在 $w$ 上的运行，如果停机就接受，否则拒绝

        $M_2$ 只接受 $\Sigma^*$ 的第一个串, $M_3$ 拒绝所有串.

        规约的证明:

        - $''Mw'' \in \overline{H} \Rightarrow M$ 在 $w$ 上不停机 $\Rightarrow M_1$ 拒绝任何输入 $\Rightarrow L(M_1) = \varnothing \subseteq L(M_2) \cup L(M_3) \Rightarrow ''M_1, M_2, M_3'' \in L_{37}$
        - $''Mw'' \notin \overline{H} \Rightarrow M$ 在 $w$ 上停机 $\Rightarrow M_1$ 接受所有串 $\Rightarrow L(M_1) = \Sigma^* \not\subseteq L(M_2) \cup L(M_3) \Rightarrow ''M_1, M_2, M_3'' \notin L_{37}$

38. \( L_{38} = \{ ''M_1'' \mid \) there exist two TMs \( M_2 \) and \( M_3 \) such that \( L(M_1) \subseteq L(M_2) \cup L(M_3) \} \)

    ??? note "Answer"
        $L_{38}$ 是**递归**的，$L_{38}$ 是全部图灵机编码的集合. 取 $M_2$ 和 $M_3$ 接受所有的串.

39. \( L_{39} = \{ ''M, w'' \mid M \) is a TM that accepts \( w \) using at most \( 2^{|w|} \) squares of its tape \(\} \)
    
    ??? note "Answer"
        $L_{39}$ 是**递归**的

        我们的思路是，我们一定能够在**有限步内判断**出 $M$ 是否最多使用 $2^{|w|}$ 个方格就能接受 $w$.

        记 $M$ 的状态数为 $m$, 字母表大小为 $k$, 记 $r=|w|$. 如果 $M$ 用了至多 $2^r$ 个方格，那么 $M$ 至多有 $\alpha = mk^{2^r}2^r$ 种格局 (枚举状态，带子内容，带头位置).

        如果 $M$ 在 $w$ 上运行了超过 $\alpha$ 步，而且它没有使用超过 $2^r$ 个方格，那么根据鸽巢原理，它的格局一定与之前的某个格局相同，也就是陷入了死循环.

        因此，我们只需要构造图灵机 $M^*$, 模拟 $M$ 在 $w$ 上 $\alpha + 1$ 步，如果 $M$ 在 $\alpha$ 步内接受，那么 $M^*$ 接受, 如果拒绝，$M^*$ 拒绝. 如果 $M$ 使用了超过 $2^r$ 个方格，或者到 $\alpha +1$ 步还没有停机，也拒绝.

        这样，我们就使用 $M^*$ 判定了 $L_{39}$.