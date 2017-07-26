# 点云特征描述

3D点云特征描述与提取是点云信息处理中的最基础也是最关键的一部分，点云的识别、分割、重采样、配准、曲面重建等处理大部分算法，都严重依赖特征描述与提取的结果。从尺度上来分，一般分为局部特征描述和全局特征描述。<http://robotica.unileon.es/index.php/PCL/OpenNI_tutorial_4:_3D_object_recognition_(descriptors)>有各种描述子较为详细的介绍。
下面给出常用的PFH、FPFH、SHOT、RoPS使用实例。

* **PFH**

参考文献：
(1) R.B. Rusu, N. Blodow, Z.C. Marton, M. Beetz. Aligning Point Cloud Views using Persistent Feature Histograms. In Proceedings of the 21st IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), Nice, France, September 22-26 2008.
(2) R.B. Rusu, Z.C. Marton, N. Blodow, M. Beetz. Learning Informative Point Classes for the Acquisition of Object Model Maps. In Proceedings of the 10th International Conference on Control, Automation, Robotics and Vision (ICARCV), Hanoi, Vietnam, December 17-20 2008.