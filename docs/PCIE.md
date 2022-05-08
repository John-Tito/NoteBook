# PCIE
1. 参考资料
    <table border="1" cellpadding="1" cellspacing="1">
        <tbody>
        <tr>
            <td style="width:162px;">作者</td>
            <td>博客</td>
        </tr>
        <tr>
            <td style="width:162px;">1、<a href="https://blog.csdn.net/cllovexyh" id="uid">CLGo</a>&nbsp;</td>
            <td><a href="https://blog.csdn.net/cllovexyh/article/details/79828833">PCIe学习（一）：PCIe基础及生成PIO例程分析</a>
            </td>
        </tr>
        <tr>
            <td style="width:162px;">2、Spring</td>
            <td><a href="https://zhuanlan.zhihu.com/PCI-Express">PCI-E协议</a></td>
        </tr>
        <tr>
            <td style="width:162px;">3、</td>
            <td>Xilinx FPGA 高速串行传输技术与应用</td>
        </tr>
        <tr>
            <td style="width:162px;">4、<a href="https://blog.csdn.net/wenjia7803">meper</a>&nbsp;</td>
            <td><a
                    href="https://blog.csdn.net/wenjia7803/article/details/80086284">基于FPGA的PCIe接口设计---01_PCIe基本概念</a>
            </td>
        </tr>
        <tr>
            <td style="width:162px;">5、<a href="https://blog.csdn.net/jackxu8">Jack-Xu</a>&nbsp;</td>
            <td><a href="https://blog.csdn.net/jackxu8/article/details/53288385">一步一步开始FPGA逻辑设计 - 高速接口之PCIe</a></td>
        </tr>
        <tr>
            <td style="width:162px;">6、<a href="https://blog.csdn.net/huan09900990">huan09900990</a></td>
            <td><a href="https://blog.csdn.net/huan09900990/article/details/81321975">Altera FPGA PCIE 例程仿真</a></td>
        </tr>
        <tr>
            <td style="width:162px;">7、<a href="https://blog.csdn.net/fzhykx">fzhykx</a></td>
            <td><a href="https://blog.csdn.net/fzhykx/article/details/80702170">xlinx_pcie_ip 使用笔记</a></td>
        </tr>
        <tr>
            <td style="width:162px;">8、<a href="https://blog.csdn.net/jiangwei0512">jiangwei0512</a></td>
            <td><a href="https://blog.csdn.net/jiangwei0512/article/details/51603525">PCI/PCIe基础——配置空间</a></td>
        </tr>
        </tbody>
    </table> 
2. PCIE基础
   1. Lane  
        	所谓的Lane，是指一组差分信号的组合，包括发送和接收。一个发送方向的差分信号包括TX+和TX-两条线，接收亦然。所以一条lane有四条物理连线。发送和接收是同时进行的，故为全双工。  
        	所谓的Link，是指两个PCIe部件的链接，通常是由端口和lane组成。（通常有多条lane）比如我们有一个X2的链路，意思是指这条链路是两条lane组成，一共8条物理连线。链路上传送的是编码之后的数据，比如Gen1/Gen2所采用的8b/10b编码，Gen3之后改成了128b/130b编码。Link初始化以及link建立过程（或者称之为链路训练，Link Training）是在设备上电或者链路重新建立链接是发生的。  
        	多条lane组成的link，有效的扩展了link的带宽。Lane的初始化和多条lane的组合优化，是在link的初始化训练过程（Link Training）中实现的。  
        	x1,x2,x4,x8,x16,x32,差分线对数依次增加，带宽依次增大。  
        	Link的初始化和协商，确定lane宽度以及速率，是不需要操作系统或者软件参与的，纯粹是芯片的硬件行为。  
        	PCIe链路是没有边带信号的，当然也没有单独的时钟线。PCIe的时钟是编码嵌入在link里的。接收端依靠同样的逻辑解析出时钟和数据。  
        	对于每一条lane上的差分信号，差分信号的电压(D+减D-)大约在800mV~1.2V之间。对于D+或者D-的单端电压大约在400-600mV之间。  
   2. PCIE 拓扑结构
      <img src="assets\FPGA.assets\image-20210615165455883.png" alt="image-20210615165455883" style="zoom:50%;" />  
   3. PCIE 层次结构
      <img src="assets\FPGA.assets\image-20210615162233094.png" alt="image-20210615162233094" style="zoom: 80%;" />  
   4. PICE TLP(事务层包)数据包类型  
      <img src="assets\FPGA.assets\image-20210615170341674.png" alt="image-20210615170341674" style="zoom:50%;" />  
   5. TLP数据包结构  
      ![image-20210615171701041](.\assets\FPGA.assets\image-20210615171701041.png)  
      1. 4DW TLP 标头
         <img src="assets\FPGA.assets\image-20210615172254734.png" alt="image-20210615172254734" style="zoom:50%;" />  
         1. Fmt  和 Type
            <img src="assets\FPGA.assets\image-20210615172939764.png" alt="image-20210615172939764" style="zoom:50%;" />
         2. TC  
            当前TLP传送类型:TC0\~TC7,默认TC0  
         3. TD  
            TLP Digest是否有效  
         4. EP  
            当前数据是否有效  
         5. Attr  
            地址转换相关  
         6. Length  
            TLP有效负载数据长度(DW)  
            <img src="assets\FPGA.assets\image-20210616090910131.png" alt="image-20210616090910131" style="zoom:50%;" />  