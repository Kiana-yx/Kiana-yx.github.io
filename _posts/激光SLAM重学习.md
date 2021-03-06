# 激光SLAM重学习

## 传感器

### URG-04LX

波特率115200，可设置

[ROS使用方法](https://blog.csdn.net/zzzztttttffffff/article/details/109259170)

```
安装
sudo apt-get install ros-melodic-urg-node

查询连接端口
rosrun urg_node getID /dev/ttyACM0

运行
rosrun urg_node urg_node

rviz -f laser
```

## 传感器介绍

1. 测距原理

    ![](https://pictures-kiana.oss-cn-beijing.aliyuncs.com/img/202205151051221.png)

    [三角测距](https://www.jianshu.com/p/b12b4a4a64a3)采用类似双目相机原理

    TOF法需要使用返回时间，显然长距离△t计算更精确

    | 三角测距                 | 飞行时间           |
    | ---------------------------- | ---------------------- |
    | 中近距离精度较高、远距离较差 | 测距范围广、测距精度高 |
    | 价格便宜                 | 价格昂贵           |
    | 易受干扰                 | 抗干扰能力强     |
    | 一般室内使用           | 室内室外皆可     |

## 水图片

![](https://pictures-kiana.oss-cn-beijing.aliyuncs.com/img/202205241040758.png)

![](https://pictures-kiana.oss-cn-beijing.aliyuncs.com/img/202205241042175.png)

## 激光SLAM

### 入门

1. [里程计标定](https://blog.csdn.net/weixin_45929038/article/details/122638114)

    ![](https://pictures-kiana.oss-cn-beijing.aliyuncs.com/img/202207151002119.png)

    直接相减求位姿差是在世界坐标系中的结果，而激光雷达的scan-matching的位姿差需要以上一时刻的位姿作为参考系，因此需要将直接相减的结果做一次旋转。

