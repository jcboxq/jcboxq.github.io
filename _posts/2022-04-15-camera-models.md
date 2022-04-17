---
title: 相机模型
tags: 3DV
mathjax: true
---

## 问题描述
作为一个三维视觉从业人员，你是否被各种各样的相机搞得头昏脑涨？你是否对如何标定这些相机不知所措？今天，就让我们走近科学，走近相机模型。
<!--more-->

## 常见相机分类
1. Pinhole Camera(针孔相机、平面相机)
2. Omnidirectional Camera(Panoramic Camera, Spherical Camera, 全向相机)

    根据实现方式分为：
    * Fisheye Camera(Dioptric Camera, 鱼眼相机, 折射相机)
    * Catadioptric Camera(折反射相机)

    ![omni_cam](/assets/images/omni_cam.jpg){:height="50%" width="50%"}

## 常用相机模型
由**投影模型**和**畸变模型**两部分构成
### 投影模型
1. **Pinhole Camera Model**: [fu fv pu pv skew=0]，只适用于针孔相机;
2. **Kannala-Brandt Camera Model**: [fu fv pu pv k1 k2 k3 k4]，为解决鱼眼相机建模而提出[1]，但适用于所有类型相机；

    ![fisheye1](/assets/images/fisheye1.png){:height="50%" width="50%"}![fisheye2](/assets/images/fisheye2.png){:height="50%" width="50%"}

    鱼眼相机的投影方式有很多种，其中最常见的是 Equidistant Projection (这也是为什么有的标定工具直接用 Equidistant 指代 KB Camera Model)。在待标定鱼眼相机投影方式未知的情况下，可以用泰勒级数展开统一建模所有类型的投影函数，又观察到折射角$\theta_d$是入射角$\theta$的奇函数，因此可以舍弃偶次项，只保留奇次项：

    ![kb](/assets/images/kb.png){:height="75%" width="75%"}

3. **Unified Omnidirectional Camera Model (Mei Camera Model)**: [$\xi$ fu fv pu pv]，为解决 catadioptric camera 建模而提出[3]，适用于针孔相机和 catadioptric camera，用此类模型近似建模鱼眼相机精度有限；

    ![mei1](/assets/images/mei1.png){:height="70%" width="70%"}

    投影过程[4]：

    ![mei_formula](/assets/images/mei_formula.png){:height="75%" width="75%"}

    $\xi$的不同值对应的反射镜面类型：

    ![mei2](/assets/images/mei2.png){:height="60%" width="60%"}

4. **Scaramuzza Camera Model**: [fu fv pu pv a0 a2 a3 a4]，在 Unified Omnidirectional Camera Model 的基础上，为了同样适用于鱼眼相机而提出[5]，适用于所有类型相机；

    和 KB Camera Model 同样的思路，用泰勒级数展开统一建模所有类型的投影过程[6]:

    ![scaramuzza1](/assets/images/scaramuzza1.png){:height="70%" width="70%"}
    ![scaramuzza2](/assets/images/scaramuzza2.png){:height="70%" width="70%"}

### 畸变模型
畸变模型指的理想图像平面到真实图像平面的变换模型, 也就是 Normalize 平面上的畸变模型。
1. **radial-tangential**: [k1 k2 p1 p2]

    相机畸变通常由径向畸变和切向畸变构成, 如下图所示：

    ![radtan1](/assets/images/radtan1.png){:height="50%" width="50%"}

    径向畸变的形成原因是镜头制造工艺不完美，使得镜头形状存在缺陷, 通常又分为桶性畸变和枕形畸变：

    ![radtan2](/assets/images/radtan2.jpeg){:height="75%" width="75%"}

    切向畸变又分为薄透镜畸变和离心畸变等，薄透镜畸变则是因为透镜存在一定的细微倾斜造成的；离心畸变的形成原因是镜头是由多个透镜组合而成的，而各个透镜的光轴不在同一条中心线上。

    radtan 畸变模型数学表达式：

    ![radtan3](/assets/images/radtan3.png){:height="75%" width="75%"}

2. **fov**: [$\omega$]

    fov 畸变模型数学表达式：

    ![fov](/assets/images/fov.png){:height="75%" width="75%"}

## 常用标定工具
1. OpenCV: Pinhole + Radtan , cv::fisheye: Pinhole + Equi , cv::omnidir: Omni + Radtan
2. Matlab-based toolbox
3. [Kalibr](https://github.com/ethz-asl/kalibr/wiki/supported-models): Kaibr 在 SLAM 领域比较出名，它提供多相机系统、相机-IMU系统互标定的功能
4. CamOdoCal: Lionel Heng 博士在ETH博士后期间的工作
5. DSO: Pinhole + Equi / Radtan / FOV
6. VINS: Pinhole / Omni + Radtan
7. SVO: Pinhole + FOV , Scaramuzza

* 注意事项：上一节所述的各种相机模型在不同的标定工具中实现、命名、归类（投影模型 or 畸变模型）或有不同，需要仔细甄别，加以区分，以免混用误用。

## 参考
1. [Kannala-Brandt Camera Model](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=1642666)
2. [Fisheye Lens Projections](http://michel.thoby.free.fr/Fisheye_history_short/Projections/Models_of_classical_projections.html)
3. [Mei Camera Model](https://www.robots.ox.ac.uk/~cmei/articles/single_viewpoint_calib_mei_07.pdf)
4. [Mei Camera Model Projection Formulas](https://blog.csdn.net/OKasy/article/details/90665534)
5. [Scaramuzza Camera Model](https://hal.inria.fr/file/index/docid/359941/filename/Scaramuzza_IROS06.pdf)
6. [Scaramuzza Camera Model Formulas](https://rpg.ifi.uzh.ch/docs/omnidirectional_camera.pdf)