# 马里兰大学锂电池数据集 CALCE，基于 Python 的锂电池寿命预测（Remaining Useful Life，RUL）& （End Of Life，EOL）

**相关论文：** 欢迎引用！

- D. Chen, W. Hong, and X. Zhou, "Transformer Network for Remaining Useful Life Prediction of Lithium-Ion Batteries", IEEE Access, 2022. [PDF download](https://github.com/XiuzeZhou/xiuzezhou.github.io/tree/main/pub/Transformer.pdf)

**主要库版本：** 

- pytorch 1.6.0

- pandas 0.24.2

**关于代码的说明：**

最近经常收到有同学问代码中一些问题，现汇总如下：

(1) SOH 的由来，它 dec 计算的部分，减去3.8和减去3.4代表着什么。

就是取放电电压在 [3.4, 3.8] 之间的容量作为 电池的 SOH。因为现在 SOH 还没有稳定的定义，所以这个区间的数值不一定就是这两个，你可以选择放电电压在 [3.3, 3.8], [3.5, 3.8] 之间的容量作为 SOH 也没问题。因为容量预测的时候可能不太准确，不可能满充满放，所以选择电池在中间这段放电的时候的电容量来作为 SOH。

这部分的具体分析，可以查看论文的分析。

- Tian, J., Xiong, R., Shen, W., Lu, J., & Yang, X. G. (2021). Deep neural network battery charging curve prediction using 30 points collected in 10 min. Joule, 5(6), 1521-1534.

- Lin, C., Xu, J., Shi, M., & Mei, X. Constant Current Charging Time Based Fast State-of-Health Estimation for Lithium-Ion Batteries. Available at SSRN 4018988.

(2) build_sequences(text, window_size) 函数生成的预测数据为什么是序列不是下一个点？

序列[1, 2, 3, 4, 5]， build_sequences 函数生成的 x=[[1, 2, 3], [2, 3, 4]], y=[[2, 3, 4], [3, 4, 5]]的目的有两个：

一种是用序列预测序列，即 x=[1, 2, 3] 预测 y=[2, 3, 4]，x=[2, 3, 4] 预测 y=[3, 4, 5]；

一种是用序列预测下一个点，即 x=[1, 2, 3] 预测 y=[4]，x=[2, 3, 4] 预测 y=[5]；

本次实验中，我采用后者。所以，代码中，我训练的时候最后是取了train_y的最后一列：

y = np.reshape(train_y[:,-1]/Rated_Capacity,(-1,1)).astype(np.float32)

**版本更新** 

- 2022年5月9日，添加高斯拟合方法：Gaussian fitting.ipynb

- 2022年2月24日，修改部分变量的名字

- 2022年2月6日，解决错误“Tensor for argument #2 ‘mat1’ is on CPU, but expected it to be on GPU (while checking arguments for addmm)”

- 2021年12月1日， 添加数据读取模块

    如果原始数据集无法成功读取，可以直接选择加载我已经提取出来的数据：NASA.npy

    Battery = np.load('NASA.npy', allow_pickle=True)

    Battery = Battery.item()

 **有任何问题，欢迎留言！**

**Homepage:** http://zhouxiuze.com

**个人博客：** http://snailwish.com

**个人邮箱：** zhouxiuze@foxmail.com

**更多内容**

1. 马里兰大学锂电池数据集 CALCE，基于 Python 的锂电池寿命预测: https://snailwish.com/437/

2. NASA 锂电池数据集，基于 Python 的锂电池寿命预测: https://snailwish.com/395/

3. NASA 锂电池数据集，基于 python 的 MLP 锂电池寿命预测: https://snailwish.com/427/

4. NASA 和 CALCE 锂电池数据集，基于 Pytorch 的 RNN、LSTM、GRU 寿命预测: https://snailwish.com/497/

5. 基于 Pytorch 的 Transformer 锂电池寿命预测: https://snailwish.com/555/

6. 锂电池研究之七——基于 Pytorch 的高斯函数拟合时间序列数据: https://snailwish.com/576/
