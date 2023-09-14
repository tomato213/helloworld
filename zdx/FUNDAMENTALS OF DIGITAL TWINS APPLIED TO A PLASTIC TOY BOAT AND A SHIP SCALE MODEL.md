#日期

##2023.9.8

#论文标题

##[FUNDAMENTALS OF DIGITAL TWINS APPLIED TO A PLASTIC TOY BOAT AND A SHIP SCALE MODEL](https://scholar.google.com.hk/scholar?hl=zh-CN&as_sdt=0%2C5&q=FUNDAMENTALS+OF+DIGITAL+TWINS+APPLIED+TO+A+PLASTIC+TOY+BOAT+AND+A+SHIP+SCALE+MODEL&btnG=)

#摘要

The objective of this paper is to present some fundamentals of digital twins that can be applied to examples ranging in different degrees of complexity. The paper presents a common definition of the digital twin concept to examine what are its main elements and how they interact with each other. Such elements are applied to a simple example with a digital twin of a floating body based on computer vision, developed with open source libraries and a web-based approach. Moving towards a more complex example, the paper presents a digital twin of a ship scale model in waves. The model is equipped with a dynamic positioning system, allowing remote control of the desired setpoint from the digital twin interface. Finally, as a direction for future work, the paper discusses the early efforts on the creation of a digital twin of the research vessel Gunnerus based on the aggregation of data from various instrumentation devices.

#引用信息（BibTeX格式）

@inproceedings{fonseca2020fundamentals,
  title={Fundamentals of digital twins applied to a plastic toy boat and a ship scale model},
  author={Fonseca, Icaro Aragao and Gaspar, Henrique Murilo},
  booktitle={Proceedings of the 34th International ECMS-Conference on Modelling and Simulation-ECMS 2020},
  year={2020}
}

##
#本论文解决什么问题
本文提出了一个波浪中船舶尺度模型的数字孪生模型。 该模型配备了一个动态定位系统，允许从数字孪生接口远程控制所需的设定点。 最后，作为今后工作的一个方向，本文讨论了基于各种仪器设备数据聚合的研究船Gunnerus数字孪生系统的前期工作。
#已有方法的优缺点

#本文采用什么方法及其优缺点

**玩具船监测界面以及数据流程**
1. 实验的物理设置是一个小水族箱，玩具船在其中漂浮。在数据收集过程中，使用消费级网络摄像头捕捉到玩具船在场景中的运动。
2. 摄像头将捕捉到的视频流传输给客户端。客户端在Web浏览器上实时执行数字孪生模拟。
3. 在第3步中，客户端使用计算机视觉算法处理摄像头视频，以在二维平面上识别和跟踪玩具船的平移（前进、上下）和旋转（俯仰）运动。
4. 通过实时更新的3D可视化和运动图绘制对其进行监测。可以基于跟踪的变量进行自动推理，例如，当船只运动超过用户指定的阈值时，数字孪生可以自动发出警告。

**将原始图像渲染为网络位置**
1. 测量数据被处理成一串坐标数据，包括平面上的两个坐标和一个旋转角度，以便与可视化图形相对应。为了得到这串数据，需要对由感知设备捕获的原始数据进行处理
2. 校准图像记录的物理设置，并应用计算机视觉算法来将由网络摄像头捕获的VGA视频转换为船只在空间坐标中的运动。
3. 摄像头被安装在水族箱的一侧固定位置，以捕捉感兴趣的船只运动。
4. 从视频源中获取运动坐标。这里使用了OpenCV.js库进行图像处理和运动跟踪。
5. 使用了Camshift算法进行船只的运动跟踪。Camshift基于另一个算法Meanshift，通过对图像颜色进行直方图分析来识别视频中的对象，并在后续的视频帧上跟踪其运动。

![Alt text](/imgs/image.png)
*玩具船数字孪生船的数据采集、传输、处理和使用*
![Alt text](/imgs/image-1.png)
*数字孪生接口截图*

**船模数字孪生**

  资产可视化：船体模型是通过将原始CAD文件转换为STL格式获得的。在组装模型过程中考虑了表示DP系统操作所需的移动：尾部系统在方位平面上移动，螺旋桨围绕其中心轴旋转。

**行为模型：波动与DP控制**
1. 第一行为模型——运动响应：显示船舶在其六个自由度上的位置
2. 第二行为模型——动态定位系统：接收到的数据允许数字孪生以螺旋桨旋转和方位角位置在可视化中示出推进行为
3. 第三行为模型——入射波：给定波高和周期，使用沃茨色散关系计算波长并3D可视化
![Alt text](/imgs/image-2.png)
*应用于比例模式实验的数字孪生框架*

#使用的数据集和性能度量
1. 船舶模型的运动是通过立体系统进行跟踪的。该系统使用五个固定在物体上的反射目标来识别物体的位置，并根据这些位置推导出六个自由度的模型运动。
2. 动态定位系统的行为数据也很容易获取。DP控制系统被配置为向数字孪生传输五个参数：每分钟三个螺旋桨的旋转速度以及两个尾部螺旋桨的方位角。运动和推进的读数直接与3D可视化相连。
3. 然而波浪探针无法感知入射波的方向，采用了一些简化处理。实验使用单一方向的规则波进行，这些波的特征是根据水面高度记录的流数据进行重建的。这个重建过程通过识别具有一个波峰和一个波谷的最新波周期，然后计算波浪高度和周期，以便在数字孪生模拟中使用。

#与我们工作的相关性
数字孪生可以为玩具塑料船和船舶比例模型的性能提供有价值的见解。通过模拟不同情景和测试各种配置，设计师和工程师可以优化这些对象的性能，并确保实际船舶的安全性。

#英文总结
This paper presented a general framework based on the digital twin definition. The framework can be applied to the modelling of different digital twin examples. Here, it was applied to two study cases following a progression in complexity, the first a toy boat and the second a ship scale model. The asset representation evolves from a simple hull geometry in the first example to a ship model including hull and propeller system in the second. Similarly, the behavioral model is expanded from motion response in 3 DOF to motion response in 6 DOF with monitoring of incident wave and control of the dynamic positioning system. All the behaviors are liked to data measured from the corresponding physical experiments. Given the novelty of the concept of an integrated digital twin and of its application to the domain of ship operations, we expect the work to contribute to future developments in this area. The study case with R/V Gunnerus, outlined as future work, will provide the opportunity to extend that contribution. The research makes use open standards to create simulations that can be easily accessed and executed by the users. This is accomplished with web interfaces based on HTML and JavaScript that perform analyses and display visualizations tracking physical behavior in real-time. Future research efforts will focus also on standardization of digital twin data as a method to simplify development and enable reuse of digital models across projects.
