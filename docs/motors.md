	1. 有刷电机
		
		
	2. 无刷电机
			
		
	3. 步进电机系统
	步进电机是直流电机具有场配置在该转子中永磁铁的形式，两个，三个或四个线圈组，称为阶段，放置在转子周围的定子。绕组连接到外部逻辑驱动器，该驱动器按顺序向绕组提供电压脉冲。电机响应这些脉冲并在指令下执行启动、停止和反向操作。
	来自 <https://www.chuandong.com/tech/tech42310.html> 
	依靠定子线圈序列通电，顺次在不同的角度形成磁场，推拉定子旋转
	优点：可以省掉用于测量电机转角的传感器。因此在结构上和价格上有一定的优势。而且它的位置和速度控制相对简单。
	缺点：第一，与同等功率的电机相比载荷比较小，没有角度传感器的情况下不能输出大力矩。第二，功耗相对较大，要么全开，要么全关。所以要么接近满功耗，要么就不能出力。第三，如果步进电机动态过载，它会滑相。
	因此步进电机一般只用于载荷较小而且十分确定、位置精度要求并不非常高，对体积敏感或在较低价格想要做到较高可靠性的场合。最常见的就是光驱、扫描仪、复印机等等。
	
	
	
	来自 <https://zhuanlan.zhihu.com/p/166098851> 
	
	
	4. 伺服电机系统
	原理：伺服主要靠脉冲来定位，基本上可以这样理解，伺服电机接收到1个脉冲，就会旋转1个脉冲对应的角度，从而实现位移，因为，伺服电机本身具备发出脉冲的功能，所以伺服电机每旋转一个角度，都会发出对应数量的脉冲，这样，和伺服电机接受的脉冲形成了呼应，或者叫闭环，如此一来，系统就会知道发了多少脉冲给伺服电机，同时又收了多少脉冲回来，这样，就能够很精确的控制电机的转动，从而实现精确的定位。
	来自 <https://www.chuandong.com/tech/tech32294.html> 
	电机类型：有刷电机/无刷电机
	5. 舵机系统
	由pwm波进入内部电路产生一个偏置电压，触发电机通过减速齿轮带动电位器移动，使电压差为零时，电机停转，从而达到伺服的效果。
	来自 <https://www.chuandong.com/tech/tech32509.html> 
	
	
