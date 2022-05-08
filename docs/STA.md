# 静态时序分析理论
## 竞争冒险
## 时序分析理论
1. $T_{jitter}$ ： 时钟抖动，取决于时钟质量 
2. $T_{skew}$ ：时钟偏斜，取决于布线和负载
3. $T_{co}$：发端寄存器时钟到输出时间，取决于芯片工艺
4. $T_{logic}$：组合逻辑延迟，主要影响因素为代码风格
5. $T_{routing}$：两级寄存器间布线延迟，主要影响因素为布局布线策略
6. $T_{su}$：收端寄存器建立时间，取决于芯片工艺
7. $T_{skew}$：时钟偏移，时钟同一边沿到达两个寄存器时钟端口的时间差，在同步设计中可忽略
8. $F_{max}≥{1\over(T_{co}+T_{logic}+T_{routing}+T_{su}−T_{skew}})$ ： 设计最大频率
9. $T_{setup} Slack$ ：数据所需时间 - 数据到达时间 (锁存沿到最近的上一个发起沿) ：锁存沿之前上个发起数据达到稳定的余量时间
    1. 寄存器到寄存器
        1. $数据所需时间 = 锁存沿 + 锁存时钟网络延迟 - 收端寄存器建立时间 - 建立不确定性$
        2. $数据到达时间 = 发起沿 + 发起时钟网络延迟 + 发端寄存器输出时间 + 数据延迟$
    2. 输入端口到寄存器
        1. $数据所需时间 = 锁存沿 + 锁存时钟网络延迟 - 收端寄存器建立时间 - 建立不确定性$
        2. $数据到达时间 = 发起沿 + 时钟网络延迟 + 最大输入延迟 + 数据延迟$
    3. 寄存器到输出端口
        1. $数据所需时间 = 锁存沿 + 时钟网络延迟 - 最小输出延迟$
        2. $数据到达时间 = 发起沿 + 发起时钟网络延迟 + 发端寄存器输出时间 + 数据延迟$
10. $T_{hold} Slack$ ：数据到达时间 - 数据所需时间 (发起沿到最近的上一个锁存沿)/(锁存沿到最近的下一个发起沿) ：锁存沿之后上个发起数据需要保持的余量时间
    1. 寄存器到寄存器
        1. $数据所需时间 = 锁存沿 + 锁存时钟网络延迟 + 收端寄存器保持时间 + 保持不确定性$
        2. $数据到达时间 = 发起沿 + 发起时钟网络延迟 + 发端寄存器输出时间 + 数据延迟$
    2. 输入端口到寄存器
        1. $数据所需时间 = 锁存沿 + 锁存时钟网络延迟 + 收端寄存器保持时间 + 保持不确定性$
        2. $数据到达时间 = 发起沿 + 时钟网络延迟 + 最小输入延迟 + 数据延迟$
    3. 寄存器到输出端口
        1. $数据所需时间 = 锁存沿 + 时钟网络延迟 - 最小输出延迟$
        2. $数据到达时间 = 发起沿 + 发起时钟网络延迟 + 发端寄存器输出时间 + 数据延迟$
11. $T_{recovery} Slack$ ：锁存沿之前上个控制信号达到稳定的余量时间
12. $T_{removel}$ :
## 时序优化
1. 流水线,在关键路径中插入寄存器
2. 寄存器平衡,调整寄存器位置
3. 操作符平衡,调整操作符的位置和级联
4. 消除优先级
5. 减少扇出,逻辑复制
6. 关键信号后移